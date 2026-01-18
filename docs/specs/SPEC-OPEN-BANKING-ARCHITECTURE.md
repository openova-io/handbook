# SPEC: Open Banking Architecture

**Version:** 1.0
**Date:** 2026-01-18

## Overview

This specification details the technical architecture for the OpenOva Open Banking Blueprint, providing fintech sandbox environments with full PSD2/Open Banking compliance capabilities.

---

## 1. System Architecture

### 1.1 High-Level Architecture

```
                                    Internet
                                        |
                                        v
+-----------------------------------------------------------------------+
|                         Cloud Load Balancer                            |
|                    (Hetzner LB / OCI LB / etc.)                       |
+-----------------------------------------------------------------------+
                                        |
                                        v
+-----------------------------------------------------------------------+
|                    Cilium Ingress Controller (Envoy)                   |
|  +------------------------------------------------------------------+ |
|  | - TLS/mTLS termination (eIDAS certificates)                      | |
|  | - L7 routing (HTTPRoute)                                         | |
|  | - Rate limiting (per-TPP quotas)                                 | |
|  | - ext_authz callouts                                             | |
|  | - Access logging (regulatory audit trail)                        | |
|  | - Coraza WAF (OWASP CRS)                                        | |
|  +------------------------------------------------------------------+ |
+-----------------------------------------------------------------------+
          |                    |                      |
          v                    v                      v
+------------------+  +------------------+  +------------------+
|   ext_authz      |  |    Keycloak      |  |  Open Banking    |
|    Service       |  |  (FAPI AuthZ)    |  |    Services      |
|                  |  |                  |  |                  |
| - eIDAS validate |  | - Token issue    |  | - Accounts API   |
| - TPP lookup     |  | - Consent flows  |  | - Payments API   |
| - Consent check  |  | - SCA orchestr.  |  | - Consents API   |
| - Quota check    |  |                  |  | - Events API     |
+------------------+  +------------------+  +------------------+
          |                    |                      |
          v                    v                      v
+-----------------------------------------------------------------------+
|                         Data Layer                                     |
|  +-------------+  +-------------+  +-------------+  +-------------+   |
|  |   CNPG      |  |   Valkey    |  |  Redpanda   |  |   MinIO     |   |
|  | (Postgres)  |  |   (Cache)   |  |  (Events)   |  |  (Objects)  |   |
|  +-------------+  +-------------+  +-------------+  +-------------+   |
+-----------------------------------------------------------------------+
          |
          v
+-----------------------------------------------------------------------+
|                      Metering & Billing                                |
|  +------------------+  +------------------+  +------------------+      |
|  |    OpenMeter     |  |       Lago       |  |  Payment Gateway |      |
|  |   (Metering)     |  |    (Billing)     |  | (Stripe/Adyen)   |      |
|  +------------------+  +------------------+  +------------------+      |
+-----------------------------------------------------------------------+
```

### 1.2 Request Flow

```
TPP Request
    |
    | 1. TLS handshake (mTLS with eIDAS cert)
    v
+-------------------+
| Cilium Ingress    |
| (Envoy)           |
+-------------------+
    |
    | 2. Extract client certificate
    | 3. Call ext_authz
    v
+-------------------+       +-------------------+
| ext_authz Service |<----->| Valkey (quota)    |
+-------------------+       +-------------------+
    |       |
    |       | 4. Validate eIDAS cert
    |       | 5. Lookup TPP in registry
    |       | 6. Verify consent (if required)
    |       | 7. Check/decrement quota
    |       v
    |   +-------------------+
    |   | CNPG (TPP/Consent)|
    |   +-------------------+
    |
    | 8. Return allow/deny with headers
    v
+-------------------+
| Backend Service   |
| (Accounts/Payments|
|  /Consents API)   |
+-------------------+
    |
    | 9. Process request
    | 10. Async: emit access log
    v
+-------------------+       +-------------------+       +-------------------+
| Redpanda          |------>| OpenMeter         |------>| Lago              |
| (Access logs)     |       | (Aggregate usage) |       | (Invoice/Bill)    |
+-------------------+       +-------------------+       +-------------------+
```

---

## 2. Component Specifications

### 2.1 Keycloak (FAPI Authorization Server)

**Purpose:** OAuth 2.0 / OpenID Connect provider with FAPI (Financial-grade API) compliance.

**Version:** 24.x or later (FAPI 2.0 certified)

**Configuration:**

```yaml
# Keycloak Realm Configuration
realm: open-banking
clients:
  - clientId: tpp-registration
    protocol: openid-connect
    publicClient: false
    clientAuthenticatorType: client-x509
    attributes:
      x509.subjectdn: ".*"
      x509.allow-regex-pattern-comparison: true

# FAPI Profile Settings
fapi:
  profile: fapi2-message-signing
  mtls:
    enabled: true
    certificateAuthority: eidas-trust-anchor
  par:
    enabled: true  # Pushed Authorization Requests
  jarm:
    enabled: true  # JWT Secured Authorization Response Mode
```

**Features Required:**

| Feature | Purpose |
|---------|---------|
| mTLS Client Auth | TPP authentication via eIDAS certificates |
| PAR (Pushed Auth Requests) | Secure authorization initiation |
| JARM | Signed authorization responses |
| Consent Management | User consent lifecycle |
| Dynamic Client Registration | TPP onboarding |
| Token Exchange | Delegation flows |

**Resource Requirements:**

```yaml
resources:
  requests:
    cpu: 500m
    memory: 1Gi
  limits:
    cpu: 2
    memory: 4Gi
replicas: 2  # HA deployment
```

### 2.2 ext_authz Service

**Purpose:** Central authorization decision point called by Envoy for every API request.

**Interface:** Envoy External Authorization gRPC API v3

**Decision Flow:**

```go
// Pseudo-code for ext_authz decision logic

func Check(ctx context.Context, req *auth.CheckRequest) (*auth.CheckResponse, error) {
    // 1. Extract client certificate from connection
    cert := extractClientCert(req)
    if cert == nil {
        return deny("missing_client_certificate", 401)
    }

    // 2. Validate eIDAS certificate
    if !validateEIDASCert(cert) {
        return deny("invalid_certificate", 401)
    }

    // 3. Lookup TPP in registry
    tpp, err := tppRegistry.Lookup(cert.Subject)
    if err != nil || tpp == nil {
        return deny("tpp_not_registered", 403)
    }
    if tpp.Status != "active" {
        return deny("tpp_suspended", 403)
    }

    // 4. Extract and validate access token
    token := extractBearerToken(req)
    claims, err := validateToken(token)
    if err != nil {
        return deny("invalid_token", 401)
    }

    // 5. Verify consent (for account access)
    if requiresConsent(req.Attributes.Request.Http.Path) {
        consent, err := consentService.Verify(claims.ConsentID, req.Attributes.Request.Http.Path)
        if err != nil || !consent.Valid {
            return deny("consent_invalid", 403)
        }
    }

    // 6. Check/decrement quota (for prepaid) or increment counter (for post-paid)
    quotaOK, remaining := quotaService.CheckAndDecrement(tpp.ID, getEndpointCost(req))
    if !quotaOK {
        return deny("quota_exceeded", 429)
    }

    // 7. Return allow with enrichment headers
    return allow(map[string]string{
        "X-TPP-ID":              tpp.ID,
        "X-TPP-Name":            tpp.Name,
        "X-Consent-ID":          claims.ConsentID,
        "X-PSU-ID":              claims.PSUID,
        "X-Credits-Remaining":   strconv.FormatInt(remaining, 10),
        "X-Request-ID":          generateRequestID(),
    })
}
```

**Configuration:**

```yaml
# ext_authz service config
server:
  port: 9001
  grpc:
    maxConcurrentStreams: 1000

eidas:
  trustAnchors:
    - /certs/eidas-root-ca.pem
    - /certs/eidas-intermediate-ca.pem
  ocsp:
    enabled: true
    responderURL: https://ocsp.eidas.europa.eu

tppRegistry:
  database:
    host: cnpg-cluster-rw.open-banking.svc
    database: tpp_registry

consentService:
  endpoint: http://consent-service.open-banking.svc:8080

quotaService:
  valkey:
    host: valkey-master.open-banking.svc
    port: 6379
  prepaidScript: /scripts/decrement.lua
```

### 2.3 OpenMeter (Usage Metering)

**Purpose:** Aggregate API usage events for billing.

**Version:** Latest (Apache 2.0)

**Architecture:**

```
Envoy Access Logs --> Redpanda --> OpenMeter Ingest --> OpenMeter Query API
                                         |
                                         v
                                   +----------+
                                   | ClickHouse|
                                   | (Storage) |
                                   +----------+
```

**Event Schema:**

```json
{
  "specversion": "1.0",
  "type": "api.request",
  "source": "open-banking-gateway",
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "time": "2026-01-18T12:00:00Z",
  "data": {
    "tpp_id": "tpp-acme-123",
    "endpoint": "/accounts",
    "method": "GET",
    "status_code": 200,
    "response_time_ms": 45,
    "request_size_bytes": 256,
    "response_size_bytes": 1024
  }
}
```

**Meter Configuration:**

```yaml
# OpenMeter meter definitions
meters:
  - slug: api_calls
    description: Total API calls
    eventType: api.request
    aggregation: COUNT
    groupBy:
      - tpp_id
      - endpoint

  - slug: api_calls_by_status
    description: API calls by status code
    eventType: api.request
    aggregation: COUNT
    groupBy:
      - tpp_id
      - status_code

  - slug: data_transferred
    description: Total data transferred
    eventType: api.request
    aggregation: SUM
    valueProperty: $.response_size_bytes
    groupBy:
      - tpp_id
```

### 2.4 Lago (Billing)

**Purpose:** Usage-based billing and invoicing.

**Version:** Latest (AGPL-3.0, self-hosted)

**Integration:**

```
OpenMeter --> Lago API --> Invoices --> Payment Gateway
                |
                v
         +-------------+
         | PostgreSQL  |
         | (Billing DB)|
         +-------------+
```

**Billing Models:**

```yaml
# Lago plan definitions

# Plan 1: Prepaid Credits
plans:
  - name: prepaid-starter
    code: prepaid-starter
    interval: one_time
    amount_cents: 10000  # $100
    charges:
      - billable_metric_code: api_calls
        charge_model: package
        properties:
          package_size: 100000  # 100k calls per $100

# Plan 2: Subscription + Overage
  - name: subscription-growth
    code: subscription-growth
    interval: monthly
    amount_cents: 50000  # $500/month
    charges:
      - billable_metric_code: api_calls
        charge_model: graduated
        properties:
          graduated_ranges:
            - from_value: 0
              to_value: 50000
              per_unit_amount: "0"  # Included
            - from_value: 50001
              to_value: null
              per_unit_amount: "0.005"  # $0.005 per call overage

# Plan 3: Enterprise Post-paid
  - name: enterprise-custom
    code: enterprise-custom
    interval: monthly
    amount_cents: 0  # Custom pricing
    charges:
      - billable_metric_code: api_calls
        charge_model: volume
        properties:
          volume_ranges:
            - from_value: 0
              to_value: 100000
              per_unit_amount: "0.003"
            - from_value: 100001
              to_value: 1000000
              per_unit_amount: "0.002"
            - from_value: 1000001
              to_value: null
              per_unit_amount: "0.001"
```

### 2.5 Valkey (Quota Cache)

**Purpose:** Real-time quota tracking for prepaid credits.

**Data Structures:**

```
# Per-TPP credit balance
credits:tpp:{tpp_id} = {remaining_credits}

# Per-TPP rate limit counters
ratelimit:tpp:{tpp_id}:window:{window_id} = {count}

# TPP metadata cache
tpp:meta:{tpp_id} = {json: name, status, plan, ...}
```

**Atomic Decrement Script:**

```lua
-- decrement.lua
-- Atomic check-and-decrement for prepaid credits

local key = KEYS[1]
local cost = tonumber(ARGV[1])
local current = tonumber(redis.call('GET', key) or 0)

if current >= cost then
    local new_balance = redis.call('DECRBY', key, cost)
    return new_balance
else
    return -1  -- Insufficient credits
end
```

---

## 3. Open Banking API Specifications

### 3.1 Supported Standards

| Standard | Version | Status |
|----------|---------|--------|
| UK Open Banking | 3.1.10 | Supported |
| Berlin Group NextGenPSD2 | 1.3.8 | Planned |
| STET | 1.4.2 | Planned |

### 3.2 API Endpoints

```yaml
# Accounts API
/accounts:
  GET: List accounts (requires consent)
/accounts/{accountId}:
  GET: Get account details
/accounts/{accountId}/balances:
  GET: Get account balances
/accounts/{accountId}/transactions:
  GET: Get account transactions

# Payments API
/payments:
  POST: Initiate payment
/payments/{paymentId}:
  GET: Get payment status

# Consents API
/consents:
  POST: Create consent request
/consents/{consentId}:
  GET: Get consent status
  DELETE: Revoke consent

# Events API (Webhooks)
/event-subscriptions:
  POST: Subscribe to events
  GET: List subscriptions
/event-subscriptions/{subscriptionId}:
  DELETE: Unsubscribe
```

### 3.3 Response Headers

All responses include:

```http
X-Request-ID: {uuid}
X-TPP-ID: {tpp_id}
X-Fapi-Interaction-Id: {interaction_id}
X-Credits-Remaining: {balance}  # For prepaid plans
X-RateLimit-Limit: {limit}
X-RateLimit-Remaining: {remaining}
X-RateLimit-Reset: {timestamp}
```

---

## 4. Security Specifications

### 4.1 mTLS with eIDAS Certificates

**Certificate Validation:**

```
1. Verify certificate chain against eIDAS trust anchors
2. Check certificate not expired
3. Verify OCSP status (not revoked)
4. Extract TPP authorization number from certificate
5. Validate roles (AISP, PISP, CBPII) against requested operation
```

**Supported Certificate Types:**

| Type | OID | Roles |
|------|-----|-------|
| QWAC | 0.4.0.19495.2.1 | Transport (mTLS) |
| QSealC | 0.4.0.19495.2.2 | Signing (JWS) |

### 4.2 Token Security

**Token Requirements:**

- JWT with RS256 or PS256 signature
- Issued by Keycloak (FAPI profile)
- Contains: tpp_id, consent_id, psu_id, scope, exp

**Token Validation:**

```yaml
jwt:
  issuer: https://auth.openbanking.{tenant}.openova.io
  audience: open-banking-api
  algorithms:
    - RS256
    - PS256
  clockSkew: 30s
```

### 4.3 Rate Limiting

**Default Limits:**

| Tier | Requests/Second | Requests/Day |
|------|-----------------|--------------|
| Sandbox | 10 | 10,000 |
| Starter | 50 | 100,000 |
| Growth | 200 | 500,000 |
| Enterprise | Custom | Custom |

**Rate Limit Headers:**

```http
X-RateLimit-Limit: 200
X-RateLimit-Remaining: 150
X-RateLimit-Reset: 1705579200
Retry-After: 60  # Only on 429 responses
```

---

## 5. Sandbox Specifications

### 5.1 Test Data

**Mock Accounts:**

| Account ID | Type | Currency | Balance |
|------------|------|----------|---------|
| acc-001 | Current | GBP | 1,500.00 |
| acc-002 | Savings | GBP | 25,000.00 |
| acc-003 | Current | EUR | 3,200.50 |

**Test TPP Certificates:**

Pre-generated test certificates for sandbox testing:

```
/sandbox/certs/
  ├── test-aisp.pem       # AISP certificate
  ├── test-aisp-key.pem   # AISP private key
  ├── test-pisp.pem       # PISP certificate
  ├── test-pisp-key.pem   # PISP private key
  └── test-cbpii.pem      # CBPII certificate
```

### 5.2 Sandbox Modes

| Mode | Behavior |
|------|----------|
| Happy Path | All requests succeed |
| Error Simulation | Configurable error responses |
| Latency Injection | Configurable response delays |
| Scenario Playback | Replay recorded production scenarios |

---

## 6. Observability

### 6.1 Metrics

**Prometheus Metrics:**

```
# Request metrics
open_banking_requests_total{tpp_id, endpoint, method, status}
open_banking_request_duration_seconds{tpp_id, endpoint, quantile}

# Quota metrics
open_banking_credits_remaining{tpp_id}
open_banking_quota_exceeded_total{tpp_id}

# Auth metrics
open_banking_auth_success_total{tpp_id, auth_type}
open_banking_auth_failure_total{tpp_id, auth_type, reason}
```

### 6.2 Grafana Dashboards

**Dashboards Included:**

| Dashboard | Purpose |
|-----------|---------|
| API Overview | Request rates, latencies, error rates |
| TPP Analytics | Per-TPP usage, quotas, errors |
| SLA Compliance | Uptime, response times vs SLA targets |
| Regulatory | Audit trail, consent lifecycle |
| Monetization | Revenue, usage by plan, churn |

### 6.3 Alerting

**Critical Alerts:**

```yaml
alerts:
  - name: HighErrorRate
    expr: sum(rate(open_banking_requests_total{status=~"5.."}[5m])) / sum(rate(open_banking_requests_total[5m])) > 0.01
    for: 5m
    severity: critical

  - name: SLABreach
    expr: histogram_quantile(0.99, rate(open_banking_request_duration_seconds_bucket[5m])) > 1
    for: 10m
    severity: warning

  - name: QuotaExhausted
    expr: open_banking_credits_remaining < 1000
    for: 1m
    severity: warning
```

---

## 7. Deployment

### 7.1 Namespace Structure

```
open-banking/                    # Main namespace
  ├── keycloak                   # FAPI AuthZ server
  ├── ext-authz                  # Authorization service
  ├── accounts-api               # Accounts API service
  ├── payments-api               # Payments API service
  ├── consents-api               # Consents API service
  ├── tpp-management             # TPP registry service
  └── sandbox-data               # Mock data service

open-banking-metering/           # Metering namespace
  ├── openmeter                  # Usage metering
  └── lago                       # Billing
```

### 7.2 Resource Totals

| Component | Replicas | CPU | Memory |
|-----------|----------|-----|--------|
| Keycloak | 2 | 2 | 4Gi |
| ext_authz | 3 | 1.5 | 1.5Gi |
| Accounts API | 2 | 1 | 1Gi |
| Payments API | 2 | 1 | 1Gi |
| Consents API | 2 | 0.5 | 512Mi |
| TPP Management | 2 | 0.5 | 512Mi |
| OpenMeter | 2 | 1 | 2Gi |
| Lago | 2 | 1 | 2Gi |
| **Total** | **17** | **8.5** | **12.5Gi** |

---

## Related Documents

- [ADR-OPEN-BANKING-BLUEPRINT](../adrs/ADR-OPEN-BANKING-BLUEPRINT.md)
- [BLUEPRINT-OPEN-BANKING](../blueprints/BLUEPRINT-OPEN-BANKING.md)
- [RUNBOOK-OPEN-BANKING](../runbooks/RUNBOOK-OPEN-BANKING.md)
