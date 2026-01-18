# ADR: Open Banking Meta Blueprint

**Status:** Accepted
**Date:** 2026-01-18
**Category:** Meta Blueprint (Vertical Solution)

## Context

Open Banking is a heavily regulated domain requiring specific capabilities beyond standard API management:

- TPP (Third Party Provider) management and lifecycle
- eIDAS certificate validation
- PSD2-compliant Strong Customer Authentication (SCA)
- Consent management
- FAPI (Financial-grade API) compliance
- Sandbox environments for fintech testing
- Regulatory reporting and SLA compliance
- API monetization (prepaid credits and post-paid billing)

Generic API gateways (Kong, Tyk, Traefik) do not address these requirements out-of-the-box. A specialized Open Banking Blueprint is needed.

## Decision

Create an **Open Banking Meta Blueprint** that bundles:

1. **A La Carte Components** (reusable independently):
   - Keycloak (Identity) - FAPI Authorization Server
   - OpenMeter (Monetization) - Usage metering
   - Lago (Monetization) - Billing and invoicing

2. **Custom Services** (Open Banking specific):
   - ext-authz, accounts-api, payments-api, consents-api, tpp-management, sandbox-data

### Architecture Concept

```
Meta Blueprint = A La Carte Components + Custom Services

Open Banking Meta Blueprint
├── Keycloak (a la carte)      ─► Can be used standalone for any OIDC/OAuth needs
├── OpenMeter (a la carte)     ─► Can be used standalone for any usage metering
├── Lago (a la carte)          ─► Can be used standalone for any billing needs
└── Custom Services            ─► Open Banking specific (NOT reusable)
```

### Core Gateway Architecture

```
Envoy (Data Plane) + Specialized Services (Control Plane)
```

**NOT** adding another API gateway layer (Kong/Tyk) - instead, leveraging existing Cilium/Envoy investment with purpose-built Open Banking components.

## Rationale

### Why Envoy at the Heart (Not Kong/Tyk)

| Aspect | Kong/Tyk Approach | Envoy + Services Approach |
|--------|-------------------|---------------------------|
| Consistency | Different proxy than service mesh | Same Envoy everywhere (Cilium) |
| Observability | Separate metrics pipeline | Unified with Cilium/Grafana |
| Customization | Plugin system (Lua/Go) | Standard services (any language) |
| Open Banking logic | Shoehorn into plugins | Purpose-built services |
| Operational burden | Another database, HA setup | Stateless ext_authz |

### Why Specialized Blueprint (Not Generic API Gateway)

Open Banking requirements that generic gateways don't provide:

| Requirement | Generic API Gateway | Open Banking Blueprint |
|-------------|---------------------|------------------------|
| TPP onboarding/validation | No | Yes |
| eIDAS certificate validation | No | Yes |
| FAPI compliance | Partial | Full |
| Consent management | No | Yes |
| SCA orchestration | No | Yes |
| Sandbox with mock data | No | Yes |
| Regulatory reporting | Limited | Full |
| Multi-spec support (UK OB, Berlin Group) | No | Yes |

## Architecture

### Component Stack

```
+------------------------------------------------------------------+
|                    TPP Developer Portal                           |
|                 (Backstage + Open Banking Plugin)                 |
+------------------------------------------------------------------+
                              |
+------------------------------------------------------------------+
|                   FAPI Authorization Server                       |
|                   (Keycloak + FAPI Profile)                       |
|         - TPP authentication (eIDAS mTLS)                         |
|         - Consent management                                      |
|         - SCA orchestration                                       |
+------------------------------------------------------------------+
                              |
+------------------------------------------------------------------+
|                    API Gateway Layer                              |
|                   (Cilium Envoy + Coraza)                         |
|         - mTLS termination                                        |
|         - Per-TPP rate limiting                                   |
|         - Request/response logging (regulatory)                   |
|         - ext_authz callouts                                      |
+------------------------------------------------------------------+
                              |
+------------------------------------------------------------------+
|                  Open Banking API Services                        |
|    +----------+  +----------+  +----------+  +----------+        |
|    | Accounts |  | Payments |  | Consents |  |  Events  |        |
|    |   API    |  |   API    |  |   API    |  |   API    |        |
|    +----------+  +----------+  +----------+  +----------+        |
+------------------------------------------------------------------+
                              |
+------------------------------------------------------------------+
|                    Sandbox Data Layer                             |
|         - Mock accounts/transactions generator                    |
|         - Test TPP certificates                                   |
|         - Scenario simulation                                     |
+------------------------------------------------------------------+
```

### Envoy ext_authz Flow

```
TPP Request (with eIDAS cert)
          |
          v
+------------------------+
|    Cilium Ingress      |
|       (Envoy)          |
|                        |
|  1. mTLS termination   |
|  2. Extract cert info  |
|  3. ext_authz call ---------> +------------------+
|  4. Rate limit check   |      |  Auth Service    |
|  5. Route to backend   |      |  (ext_authz)     |
+------------------------+      |                  |
          |                     | - Validate cert  |
          |                     | - Check TPP reg  |
          |                     | - Verify consent |
          |                     | - Token validate |
          v                     +------------------+
+------------------------+
|   Backend Services     |
+------------------------+
```

### Monetization Architecture

```
+------------------------------------------------------------------+
|                      Metering Pipeline                            |
|                                                                   |
|   Envoy Access   -->  Redpanda  -->  OpenMeter  -->  Lago        |
|      Logs            (Kafka)        (Metering)      (Billing)    |
|                                          |                        |
|                                          v                        |
|                                    +----------+                   |
|                                    |  Valkey  |                   |
|                                    |  (Quota  |                   |
|                                    |   Cache) |                   |
|                                    +----------+                   |
+------------------------------------------------------------------+
```

## Components

### A La Carte Components (Reusable Independently)

These are standalone components that can be used for any application, not just Open Banking.

| Component | Category | Purpose | License |
|-----------|----------|---------|---------|
| Keycloak | Identity | OIDC/OAuth/FAPI Authorization Server | Apache 2.0 |
| OpenMeter | Monetization | Usage metering for any API | Apache 2.0 |
| Lago | Monetization | Billing and invoicing | AGPL-3.0 |

### Custom Services (Open Banking Specific)

| Service | Purpose |
|---------|---------|
| ext_authz Service | Central auth decision point (eIDAS, consent, TPP) |
| TPP Management Service | TPP onboarding, lifecycle, directory integration |
| Consent Management Service | Consent storage, query, revocation |
| eIDAS Validator Service | Certificate chain validation against trust anchors |
| Mock Banking APIs | Sandbox accounts, payments, transactions |
| Backstage Open Banking Plugin | TPP portal, usage dashboard |

### Existing Components Leveraged

| Component | Role in Open Banking |
|-----------|---------------------|
| Cilium/Envoy | API Gateway (mTLS, routing, rate limiting) |
| Coraza | WAF (OWASP CRS) |
| Valkey | Quota cache (real-time credit tracking) |
| Redpanda | Metering event streaming |
| Grafana Stack | Observability and regulatory dashboards |
| Backstage | TPP Developer Portal |
| CNPG | Consent and TPP data storage |

## Monetization Models

### Supported Models

| Model | Implementation |
|-------|----------------|
| Prepaid (Credits) | Atomic decrement in Valkey, block at zero |
| Post-paid | Meter usage, invoice at period end |
| Subscription + Overage | Included quota + per-call overage |
| Tiered | Different rates at different volumes |
| Endpoint-based | Different costs per API (Payments vs Accounts) |

### Prepaid Flow

```
TPP buys credits --> Lago --> Sync to Valkey
                                    |
Request --> Envoy --> ext_authz --> Valkey: atomic DECR
                                    |
                              balance > 0 --> ALLOW
                              balance <= 0 --> BLOCK (402)
```

### Post-paid Flow

```
Request --> Envoy --> Access Log --> Redpanda --> OpenMeter
                                                      |
End of Period:                                  Calculate usage
                                                      |
                                                  Lago invoice
```

## Open Banking Standards Supported

| Standard | Region | Status |
|----------|--------|--------|
| UK Open Banking | UK | Primary |
| Berlin Group (NextGenPSD2) | EU | Planned |
| STET | France | Planned |
| Polish API | Poland | Planned |

## Resource Requirements

| Component | CPU | Memory | Storage |
|-----------|-----|--------|---------|
| Keycloak | 1 | 2Gi | 10Gi |
| OpenMeter | 0.5 | 1Gi | 50Gi |
| Lago | 0.5 | 1Gi | 20Gi |
| ext_authz Service | 0.5 | 512Mi | - |
| TPP Management | 0.25 | 256Mi | 5Gi |
| Consent Management | 0.25 | 256Mi | 10Gi |
| Mock Banking APIs | 0.5 | 512Mi | 20Gi |
| **Total** | **3.5** | **5.5Gi** | **115Gi** |

## Consequences

### Positive

- Leverages existing Cilium/Envoy investment (no new proxy)
- Full control over Open Banking logic (not constrained by plugin architecture)
- Unified observability with Grafana stack
- Can adapt to different Open Banking specs (UK, EU, etc.)
- Open Banking services become differentiating IP
- Supports both prepaid and post-paid monetization

### Negative

- More upfront development than buying off-the-shelf
- Need to maintain Open Banking spec compliance
- Keycloak adds operational complexity
- Requires Open Banking domain expertise

### Risks

| Risk | Mitigation |
|------|------------|
| Spec compliance drift | Automated conformance testing |
| Security vulnerabilities | Regular security audits, Trivy scanning |
| Performance at scale | Load testing, Valkey for real-time quota |
| Regulatory changes | Modular architecture for spec updates |

## Related

- [SPEC-OPEN-BANKING-ARCHITECTURE](../specs/SPEC-OPEN-BANKING-ARCHITECTURE.md)
- [BLUEPRINT-OPEN-BANKING](../blueprints/BLUEPRINT-OPEN-BANKING.md)
- [ADR-CILIUM-SERVICE-MESH](https://github.com/openova-io/cilium/blob/main/docs/ADR-CILIUM-SERVICE-MESH.md)
