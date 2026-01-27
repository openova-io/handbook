# OpenOva Documentation Index

Central index of all documentation across OpenOva repositories.

**Updated:** 2026-01-27

---

## Quick Links

| Resource | Description |
|----------|-------------|
| [Bootstrap Wizard](https://github.com/openova-io/bootstrap) | Platform onboarding and provisioning |
| [Platform Tech Stack](./docs/specs/SPEC-PLATFORM-TECH-STACK.md) | Complete technology stack |
| [Multi-Region Strategy](./docs/adrs/ADR-MULTI-REGION-STRATEGY.md) | DR architecture |

---

## Bootstrap (Platform Onboarding)

**Repository:** [bootstrap](https://github.com/openova-io/bootstrap)

Managed UI for bootstrapping organization-specific Kubernetes infrastructure from OpenOva blueprints.

| Document | Description |
|----------|-------------|
| [README](https://github.com/openova-io/bootstrap/blob/main/README.md) | Overview and usage |
| [ADR-BOOTSTRAP-ARCHITECTURE](https://github.com/openova-io/bootstrap/blob/main/docs/ADR-BOOTSTRAP-ARCHITECTURE.md) | Blueprint vs instance architecture |
| [SPEC-WIZARD-FLOW](https://github.com/openova-io/bootstrap/blob/main/docs/SPEC-WIZARD-FLOW.md) | Interactive wizard specification |

---

## Handbook (Central Documentation)

**Repository:** [handbook](https://github.com/openova-io/handbook)

### Architecture Decision Records (ADRs)

| Document | Description |
|----------|-------------|
| [ADR-MICROSERVICES-ARCHITECTURE](./docs/adrs/ADR-MICROSERVICES-ARCHITECTURE.md) | Microservices architecture decisions |
| [ADR-IMAGE-REGISTRY](./docs/adrs/ADR-IMAGE-REGISTRY.md) | Harbor container registry (mandatory) |
| [ADR-SECURITY-SCANNING](./docs/adrs/ADR-SECURITY-SCANNING.md) | Trivy CI/CD + Harbor + Runtime scanning |
| [ADR-OPERATIONAL-RESILIENCE](./docs/adrs/ADR-OPERATIONAL-RESILIENCE.md) | Cilium resilience patterns |
| [ADR-PROGRESSIVE-DELIVERY](./docs/adrs/ADR-PROGRESSIVE-DELIVERY.md) | Progressive delivery strategy |
| [ADR-MULTI-REGION-STRATEGY](./docs/adrs/ADR-MULTI-REGION-STRATEGY.md) | Multi-region independent clusters |
| [ADR-ZERO-HUMAN-INTERVENTION-OPS](./docs/adrs/ADR-ZERO-HUMAN-INTERVENTION-OPS.md) | Zero human intervention operations |
| [ADR-OPEN-BANKING-BLUEPRINT](./docs/adrs/ADR-OPEN-BANKING-BLUEPRINT.md) | Open Banking vertical blueprint |
| [ADR-PLATFORM-ENGINEERING-TOOLS](./docs/adrs/ADR-PLATFORM-ENGINEERING-TOOLS.md) | Crossplane, Backstage, Flux |
| [ADR-REPOSITORY-STRUCTURE](./docs/adrs/ADR-REPOSITORY-STRUCTURE.md) | Repository organization |
| [ADR-AIRGAP-COMPLIANCE](./docs/adrs/ADR-AIRGAP-COMPLIANCE.md) | Air-gap compliance strategy |

### Technical Specifications (SPECs)

| Document | Description |
|----------|-------------|
| [SPEC-PLATFORM-TECH-STACK](./docs/specs/SPEC-PLATFORM-TECH-STACK.md) | Complete platform technology stack |
| [SPEC-LLM-GATEWAY](./docs/specs/SPEC-LLM-GATEWAY.md) | LLM Gateway specification |
| [SPEC-CIRCUIT-BREAKER](./docs/specs/SPEC-CIRCUIT-BREAKER.md) | Cilium circuit breaker patterns |
| [SPEC-AUTO-REMEDIATION](./docs/specs/SPEC-AUTO-REMEDIATION.md) | Auto-remediation workflows |
| [SPEC-OPEN-BANKING-ARCHITECTURE](./docs/specs/SPEC-OPEN-BANKING-ARCHITECTURE.md) | Open Banking architecture |

### Blueprints (Deployable Configurations)

| Document | Description |
|----------|-------------|
| [BLUEPRINT-NAMESPACE](./docs/blueprints/BLUEPRINT-NAMESPACE.md) | Namespace configuration |
| [BLUEPRINT-DEPLOYMENT](./docs/blueprints/BLUEPRINT-DEPLOYMENT.md) | Deployment templates |
| [BLUEPRINT-LLM-GATEWAY](./docs/blueprints/BLUEPRINT-LLM-GATEWAY.md) | LLM Gateway deployment |
| [BLUEPRINT-OPEN-BANKING](./docs/blueprints/BLUEPRINT-OPEN-BANKING.md) | Open Banking sandbox |

### Runbooks (Operational Procedures)

| Document | Description |
|----------|-------------|
| [RUNBOOK-PLATFORM](./docs/runbooks/RUNBOOK-PLATFORM.md) | Platform operations |

---

## Component Repositories

### Infrastructure & Provisioning

#### Terraform
**Repository:** [terraform](https://github.com/openova-io/terraform)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-INFRASTRUCTURE](https://github.com/openova-io/terraform/blob/main/docs/ADR-INFRASTRUCTURE.md) | ADR | Infrastructure provisioning (bootstrap only) |

#### Crossplane
**Repository:** [crossplane](https://github.com/openova-io/crossplane)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CROSSPLANE](https://github.com/openova-io/crossplane/blob/main/docs/ADR-CROSSPLANE.md) | ADR | Day-2 cloud resource provisioning |

---

### GitOps, Git & IDP

#### Flux
**Repository:** [flux](https://github.com/openova-io/flux)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-FLUX-GITOPS](https://github.com/openova-io/flux/blob/main/docs/ADR-FLUX-GITOPS.md) | ADR | Flux GitOps decision |
| [SPEC-FLUX-STRUCTURE](https://github.com/openova-io/flux/blob/main/docs/SPEC-FLUX-STRUCTURE.md) | SPEC | Flux directory structure |

#### Gitea
**Repository:** [gitea](https://github.com/openova-io/gitea)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-GITEA](https://github.com/openova-io/gitea/blob/main/docs/ADR-GITEA.md) | ADR | Gitea as internal Git provider |

#### Backstage
**Repository:** [backstage](https://github.com/openova-io/backstage)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-BACKSTAGE-IDP](https://github.com/openova-io/backstage/blob/main/docs/ADR-BACKSTAGE-IDP.md) | ADR | Internal Developer Platform |

---

### Networking & Service Mesh

#### Cilium
**Repository:** [cilium](https://github.com/openova-io/cilium)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CNI-CILIUM-EBPF](https://github.com/openova-io/cilium/blob/main/docs/ADR-CNI-CILIUM-EBPF.md) | ADR | Cilium CNI with eBPF |
| [ADR-CILIUM-SERVICE-MESH](https://github.com/openova-io/cilium/blob/main/docs/ADR-CILIUM-SERVICE-MESH.md) | ADR | Cilium Service Mesh (replaces Istio) |

#### k8gb
**Repository:** [k8gb](https://github.com/openova-io/k8gb)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-K8GB-GSLB](https://github.com/openova-io/k8gb/blob/main/docs/ADR-K8GB-GSLB.md) | ADR | Global Server Load Balancing |
| [BLUEPRINT-K8GB](https://github.com/openova-io/k8gb/blob/main/docs/BLUEPRINT-K8GB.md) | BLUEPRINT | k8gb deployment manifests |
| [RUNBOOK-K8GB](https://github.com/openova-io/k8gb/blob/main/docs/RUNBOOK-K8GB.md) | RUNBOOK | k8gb operations |

#### ExternalDNS
**Repository:** [external-dns](https://github.com/openova-io/external-dns)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-EXTERNAL-DNS](https://github.com/openova-io/external-dns/blob/main/docs/ADR-EXTERNAL-DNS.md) | ADR | DNS record synchronization |

---

### Failover & Resilience

#### Failover Controller
**Repository:** [failover-controller](https://github.com/openova-io/failover-controller)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-FAILOVER-CONTROLLER](https://github.com/openova-io/failover-controller/blob/main/docs/ADR-FAILOVER-CONTROLLER.md) | ADR | Generic failover orchestration |

---

### Observability

#### Grafana
**Repository:** [grafana](https://github.com/openova-io/grafana)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-OBSERVABILITY-STACK](https://github.com/openova-io/grafana/blob/main/docs/ADR-OBSERVABILITY-STACK.md) | ADR | Grafana LGTM stack (includes configuration) |

---

### Security

#### External Secrets
**Repository:** [external-secrets](https://github.com/openova-io/external-secrets)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-SECRETS-MANAGEMENT](https://github.com/openova-io/external-secrets/blob/main/docs/ADR-SECRETS-MANAGEMENT.md) | ADR | ESO + Vault (PushSecrets) |

#### Vault
**Repository:** [vault](https://github.com/openova-io/vault)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-VAULT](https://github.com/openova-io/vault/blob/main/docs/ADR-VAULT.md) | ADR | Secrets backend (self-hosted) |

#### Cert-Manager
**Repository:** [cert-manager](https://github.com/openova-io/cert-manager)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-TLS-CERTIFICATES](https://github.com/openova-io/cert-manager/blob/main/docs/ADR-TLS-CERTIFICATES.md) | ADR | TLS certificate management |

#### Kyverno
**Repository:** [kyverno](https://github.com/openova-io/kyverno)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-POLICY-ENGINE](https://github.com/openova-io/kyverno/blob/main/docs/ADR-POLICY-ENGINE.md) | ADR | Policy engine decision |

---

### Storage & Registry

#### Harbor
**Repository:** [harbor](https://github.com/openova-io/harbor)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-HARBOR-REGISTRY](https://github.com/openova-io/harbor/blob/main/docs/ADR-HARBOR-REGISTRY.md) | ADR | Container registry (mandatory) |

#### MinIO
**Repository:** [minio](https://github.com/openova-io/minio)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-OBJECT-STORAGE](https://github.com/openova-io/minio/blob/main/docs/ADR-OBJECT-STORAGE.md) | ADR | Tiered object storage |

#### Velero
**Repository:** [velero](https://github.com/openova-io/velero)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-BACKUP](https://github.com/openova-io/velero/blob/main/docs/ADR-BACKUP.md) | ADR | Backup to archival S3 |

---

### Scaling

#### VPA
**Repository:** [vpa](https://github.com/openova-io/vpa)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-VPA](https://github.com/openova-io/vpa/blob/main/docs/ADR-VPA.md) | ADR | Vertical Pod Autoscaler |

#### KEDA
**Repository:** [keda](https://github.com/openova-io/keda)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-WORKLOAD-MANAGEMENT](https://github.com/openova-io/keda/blob/main/docs/ADR-WORKLOAD-MANAGEMENT.md) | ADR | Event-driven autoscaling |

---

### Data Services (À La Carte)

#### CNPG (PostgreSQL)
**Repository:** [cnpg](https://github.com/openova-io/cnpg)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-DATABASE-POSTGRESQL](https://github.com/openova-io/cnpg/blob/main/docs/ADR-DATABASE-POSTGRESQL.md) | ADR | PostgreSQL operator (WAL streaming DR) |

#### MongoDB
**Repository:** [mongodb](https://github.com/openova-io/mongodb)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-DATABASE-MONGODB](https://github.com/openova-io/mongodb/blob/main/docs/ADR-DATABASE-MONGODB.md) | ADR | MongoDB operator (CDC via Debezium) |

#### Valkey
**Repository:** [valkey](https://github.com/openova-io/valkey)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CACHING-VALKEY](https://github.com/openova-io/valkey/blob/main/docs/ADR-CACHING-VALKEY.md) | ADR | Redis-compatible cache (BSD-3, REPLICAOF DR) |

#### Redpanda
**Repository:** [redpanda](https://github.com/openova-io/redpanda)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-EVENT-STREAMING-REDPANDA](https://github.com/openova-io/redpanda/blob/main/docs/ADR-EVENT-STREAMING-REDPANDA.md) | ADR | Kafka-compatible streaming (MirrorMaker2 DR) |

---

### Communication (À La Carte)

#### Stalwart
**Repository:** [stalwart](https://github.com/openova-io/stalwart)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-EMAIL-PLATFORM](https://github.com/openova-io/stalwart/blob/main/docs/ADR-EMAIL-PLATFORM.md) | ADR | Email server (JMAP/IMAP/SMTP) |

#### STUNner
**Repository:** [stunner](https://github.com/openova-io/stunner)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-WEBRTC-GATEWAY](https://github.com/openova-io/stunner/blob/main/docs/ADR-WEBRTC-GATEWAY.md) | ADR | WebRTC gateway |

---

### Identity (À La Carte)

#### Keycloak
**Repository:** [keycloak](https://github.com/openova-io/keycloak)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-KEYCLOAK](https://github.com/openova-io/keycloak/blob/main/docs/ADR-KEYCLOAK.md) | ADR | OIDC/OAuth/FAPI Authorization Server |

---

### Monetization (À La Carte)

#### OpenMeter
**Repository:** [openmeter](https://github.com/openova-io/openmeter)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-OPENMETER](https://github.com/openova-io/openmeter/blob/main/docs/ADR-OPENMETER.md) | ADR | Usage metering for APIs |

#### Lago
**Repository:** [lago](https://github.com/openova-io/lago)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-LAGO](https://github.com/openova-io/lago/blob/main/docs/ADR-LAGO.md) | ADR | Usage-based billing and invoicing |

---

### Meta Blueprints (Vertical Solutions)

Meta blueprints bundle a la carte components with custom services for specific industry verticals.

#### Open Banking
**Repository:** [open-banking](https://github.com/openova-io/open-banking)

Bundles: Keycloak + OpenMeter + Lago + custom services for PSD2/FAPI compliance.

| Document | Type | Description |
|----------|------|-------------|
| [ADR-OPEN-BANKING-SERVICES](https://github.com/openova-io/open-banking/blob/main/docs/ADR-OPEN-BANKING-SERVICES.md) | ADR | Custom Open Banking services (ext-authz, APIs) |

---

## Document Types

| Type | Purpose | Location |
|------|---------|----------|
| **ADR** | Architecture Decision Records - WHY we made decisions | `docs/adrs/` or component `docs/` |
| **SPEC** | Technical Specifications - HOW things work | `docs/specs/` or component `docs/` |
| **BLUEPRINT** | Deployable Configurations - WHAT to deploy | `docs/blueprints/` |
| **RUNBOOK** | Operational Procedures - HOW to operate | `docs/runbooks/` |

---

## Component Summary

### Mandatory Components

| Component | Purpose |
|-----------|---------|
| Terraform | Bootstrap IaC |
| Crossplane | Day-2 cloud provisioning |
| Cilium | CNI + Service Mesh (eBPF) |
| Coraza | WAF |
| Flux | GitOps |
| Gitea | Internal Git server |
| cert-manager | TLS certificates |
| External Secrets | Secrets operator |
| Vault | Secrets backend |
| Kyverno | Policy engine |
| VPA | Vertical autoscaling |
| KEDA | Horizontal autoscaling |
| Grafana Stack | Observability |
| OpenTelemetry | Application tracing |
| Harbor | Container registry |
| MinIO | Object storage |
| Velero | Backup |
| ExternalDNS | DNS sync |
| k8gb | GSLB (authoritative DNS) |
| Failover Controller | Failover orchestration |
| Backstage | IDP |

### À La Carte Components

| Category | Component | Purpose |
|----------|-----------|---------|
| Data | CNPG | PostgreSQL |
| Data | MongoDB | Document database |
| Data | Redpanda | Event streaming |
| Data | Valkey | Cache |
| Communication | Stalwart | Email |
| Communication | STUNner | WebRTC |
| Identity | Keycloak | OIDC/OAuth/FAPI Authorization Server |
| Monetization | OpenMeter | Usage metering |
| Monetization | Lago | Billing and invoicing |

### Meta Blueprints (Vertical Solutions)

| Blueprint | Bundles | Purpose |
|-----------|---------|---------|
| Open Banking | Keycloak + OpenMeter + Lago + custom services | PSD2/FAPI fintech sandbox with monetization |

---

*Part of [OpenOva](https://github.com/openova-io)*
