# BLUEPRINT: Open Banking

**Version:** 1.0
**Date:** 2026-01-18
**Type:** A La Carte Blueprint

## Overview

Deploy a complete Open Banking sandbox environment with PSD2/FAPI compliance, TPP management, and API monetization.

---

## Prerequisites

### Required Components (Mandatory Stack)

- Cilium Service Mesh (Envoy-based ingress)
- Coraza WAF
- CNPG (PostgreSQL)
- Valkey (Redis-compatible cache)
- Redpanda (Event streaming)
- Grafana Stack (Observability)
- Backstage (Developer portal)
- External Secrets + Vault

### Resource Requirements

| Resource | Minimum | Recommended |
|----------|---------|-------------|
| CPU | 8 cores | 16 cores |
| Memory | 12 Gi | 24 Gi |
| Storage | 120 Gi | 250 Gi |

---

## Components Deployed

### Core Components

| Component | Purpose | Repository |
|-----------|---------|------------|
| Keycloak | FAPI Authorization Server | openova-io/keycloak |
| OpenMeter | Usage metering | openova-io/openmeter |
| Lago | Billing and invoicing | openova-io/lago |

### Open Banking Services

| Service | Purpose | Repository |
|---------|---------|------------|
| ext-authz | Central auth decision | openova-io/open-banking |
| accounts-api | Accounts API | openova-io/open-banking |
| payments-api | Payments API | openova-io/open-banking |
| consents-api | Consent management API | openova-io/open-banking |
| tpp-management | TPP registry | openova-io/open-banking |
| sandbox-data | Mock data service | openova-io/open-banking |

---

## Deployment

### Step 1: Enable Open Banking Blueprint

In Backstage or via GitOps:

```yaml
# flux/clusters/<cluster>/open-banking.yaml
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: open-banking
  namespace: flux-system
spec:
  interval: 10m
  path: ./open-banking/deploy
  prune: true
  sourceRef:
    kind: GitRepository
    name: openova-blueprints
  postBuild:
    substitute:
      TENANT: ${TENANT}
      DOMAIN: ${DOMAIN}
```

### Step 2: Configure Keycloak

Create FAPI realm configuration:

```yaml
# open-banking/config/keycloak-realm.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: keycloak-realm-config
  namespace: open-banking
data:
  realm.json: |
    {
      "realm": "open-banking",
      "enabled": true,
      "sslRequired": "all",
      "clients": [],
      "roles": {
        "realm": [
          {"name": "AISP", "description": "Account Information Service Provider"},
          {"name": "PISP", "description": "Payment Initiation Service Provider"},
          {"name": "CBPII", "description": "Card Based Payment Instrument Issuer"}
        ]
      }
    }
```

### Step 3: Configure TPP Directory

Upload eIDAS trust anchors:

```yaml
# open-banking/config/eidas-trust-anchors.yaml
apiVersion: v1
kind: Secret
metadata:
  name: eidas-trust-anchors
  namespace: open-banking
type: Opaque
stringData:
  root-ca.pem: |
    -----BEGIN CERTIFICATE-----
    # eIDAS Root CA certificate
    -----END CERTIFICATE-----
  intermediate-ca.pem: |
    -----BEGIN CERTIFICATE-----
    # eIDAS Intermediate CA certificate
    -----END CERTIFICATE-----
```

### Step 4: Configure Billing Plans

```yaml
# open-banking/config/billing-plans.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: lago-plans
  namespace: open-banking-metering
data:
  plans.yaml: |
    plans:
      - name: sandbox
        code: sandbox
        interval: monthly
        amount_cents: 0
        trial_period: 30
        charges:
          - metric: api_calls
            model: package
            properties:
              package_size: 10000
              free_units: 10000

      - name: starter-prepaid
        code: starter-prepaid
        interval: one_time
        amount_cents: 10000
        charges:
          - metric: api_calls
            model: package
            properties:
              package_size: 100000

      - name: growth
        code: growth
        interval: monthly
        amount_cents: 50000
        charges:
          - metric: api_calls
            model: graduated
            properties:
              ranges:
                - from: 0
                  to: 50000
                  unit_amount: "0"
                - from: 50001
                  unit_amount: "0.005"

      - name: enterprise
        code: enterprise
        interval: monthly
        amount_cents: 0
        charges:
          - metric: api_calls
            model: volume
            properties:
              ranges:
                - from: 0
                  to: 100000
                  unit_amount: "0.003"
                - from: 100001
                  to: 1000000
                  unit_amount: "0.002"
                - from: 1000001
                  unit_amount: "0.001"
```

### Step 5: Configure Gateway Routes

```yaml
# open-banking/gateway/httproute.yaml
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: open-banking-api
  namespace: open-banking
spec:
  parentRefs:
    - name: cilium-gateway
      namespace: cilium-system
  hostnames:
    - "api.openbanking.${TENANT}.${DOMAIN}"
  rules:
    # Accounts API
    - matches:
        - path:
            type: PathPrefix
            value: /accounts
      filters:
        - type: ExtensionRef
          extensionRef:
            group: cilium.io
            kind: CiliumEnvoyConfig
            name: ext-authz-filter
      backendRefs:
        - name: accounts-api
          port: 8080

    # Payments API
    - matches:
        - path:
            type: PathPrefix
            value: /payments
      filters:
        - type: ExtensionRef
          extensionRef:
            group: cilium.io
            kind: CiliumEnvoyConfig
            name: ext-authz-filter
      backendRefs:
        - name: payments-api
          port: 8080

    # Consents API
    - matches:
        - path:
            type: PathPrefix
            value: /consents
      backendRefs:
        - name: consents-api
          port: 8080
```

---

## Configuration Options

### Basic Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| `TENANT` | Tenant identifier | Required |
| `DOMAIN` | Base domain | Required |
| `OB_STANDARD` | Open Banking standard | `uk-ob-3.1` |
| `SANDBOX_ENABLED` | Enable sandbox mode | `true` |

### Advanced Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| `KEYCLOAK_REPLICAS` | Keycloak replicas | `2` |
| `RATE_LIMIT_RPS` | Default rate limit (req/sec) | `100` |
| `PREPAID_ENABLED` | Enable prepaid credits | `true` |
| `POSTPAID_ENABLED` | Enable post-paid billing | `true` |

---

## Validation

### Health Checks

```bash
# Check all components are running
kubectl get pods -n open-banking
kubectl get pods -n open-banking-metering

# Check Keycloak is ready
curl -k https://auth.openbanking.${TENANT}.${DOMAIN}/health

# Check API is responding
curl -k https://api.openbanking.${TENANT}.${DOMAIN}/health
```

### Smoke Tests

```bash
# Test with sandbox credentials
export CERT=/path/to/test-aisp.pem
export KEY=/path/to/test-aisp-key.pem

# Get access token
TOKEN=$(curl -X POST \
  --cert $CERT --key $KEY \
  https://auth.openbanking.${TENANT}.${DOMAIN}/realms/open-banking/protocol/openid-connect/token \
  -d "grant_type=client_credentials&client_id=test-aisp" | jq -r '.access_token')

# Call Accounts API
curl -H "Authorization: Bearer $TOKEN" \
  --cert $CERT --key $KEY \
  https://api.openbanking.${TENANT}.${DOMAIN}/accounts
```

---

## Monitoring

### Grafana Dashboards

After deployment, the following dashboards are available in Grafana:

| Dashboard | URL |
|-----------|-----|
| API Overview | `/d/open-banking-overview` |
| TPP Analytics | `/d/open-banking-tpp` |
| SLA Compliance | `/d/open-banking-sla` |
| Monetization | `/d/open-banking-revenue` |

### Key Metrics

| Metric | Target |
|--------|--------|
| API Availability | > 99.5% |
| P99 Latency | < 1000ms |
| Error Rate | < 1% |

---

## Operations

### TPP Onboarding

1. TPP submits registration via Developer Portal (Backstage)
2. Validate eIDAS certificate
3. Create TPP record in registry
4. Assign billing plan
5. Issue sandbox credentials

### Consent Management

```bash
# List active consents for a TPP
kubectl exec -it deploy/consents-api -n open-banking -- \
  consent-cli list --tpp-id=<tpp_id>

# Revoke a consent
kubectl exec -it deploy/consents-api -n open-banking -- \
  consent-cli revoke --consent-id=<consent_id>
```

### Billing Operations

```bash
# View TPP usage
kubectl exec -it deploy/lago -n open-banking-metering -- \
  lago customers usage --external-id=<tpp_id>

# Generate invoice
kubectl exec -it deploy/lago -n open-banking-metering -- \
  lago invoices create --customer-external-id=<tpp_id>
```

---

## Troubleshooting

### Common Issues

| Issue | Cause | Resolution |
|-------|-------|------------|
| 401 Unauthorized | Invalid/expired certificate | Check eIDAS cert validity |
| 403 Forbidden | TPP not registered | Verify TPP onboarding complete |
| 429 Too Many Requests | Quota exceeded | Check billing plan limits |
| 502 Bad Gateway | Backend unavailable | Check pod health |

### Debug Mode

Enable debug logging:

```yaml
# Patch ext-authz deployment
kubectl patch deployment ext-authz -n open-banking \
  -p '{"spec":{"template":{"spec":{"containers":[{"name":"ext-authz","env":[{"name":"LOG_LEVEL","value":"debug"}]}]}}}}'
```

---

## Related

- [ADR-OPEN-BANKING-BLUEPRINT](../adrs/ADR-OPEN-BANKING-BLUEPRINT.md)
- [SPEC-OPEN-BANKING-ARCHITECTURE](../specs/SPEC-OPEN-BANKING-ARCHITECTURE.md)
- [RUNBOOK-OPEN-BANKING](../runbooks/RUNBOOK-OPEN-BANKING.md)
