# OpenOva Documentation Index

Central index of all documentation across OpenOva repositories.

**Updated:** 2026-01-16

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

Wizard/CLI for bootstrapping organization-specific Kubernetes infrastructure from OpenOva blueprints.

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
| [ADR-OPERATIONAL-RESILIENCE](./docs/adrs/ADR-OPERATIONAL-RESILIENCE.md) | Istio resilience patterns |
| [ADR-PROGRESSIVE-DELIVERY](./docs/adrs/ADR-PROGRESSIVE-DELIVERY.md) | Progressive delivery strategy |
| [ADR-MULTI-REGION-STRATEGY](./docs/adrs/ADR-MULTI-REGION-STRATEGY.md) | Multi-region independent clusters |
| [ADR-ZERO-HUMAN-INTERVENTION-OPS](./docs/adrs/ADR-ZERO-HUMAN-INTERVENTION-OPS.md) | Zero human intervention operations |
| [ADR-PLATFORM-ENGINEERING-TOOLS](./docs/adrs/ADR-PLATFORM-ENGINEERING-TOOLS.md) | Crossplane, Backstage, Flux |
| [ADR-REPOSITORY-STRUCTURE](./docs/adrs/ADR-REPOSITORY-STRUCTURE.md) | Repository organization |
| [ADR-AIRGAP-COMPLIANCE](./docs/adrs/ADR-AIRGAP-COMPLIANCE.md) | Air-gap compliance strategy |

### Technical Specifications (SPECs)

| Document | Description |
|----------|-------------|
| [SPEC-PLATFORM-TECH-STACK](./docs/specs/SPEC-PLATFORM-TECH-STACK.md) | Complete platform technology stack |
| [SPEC-DNS-FAILOVER](./docs/specs/SPEC-DNS-FAILOVER.md) | k8gb + ExternalDNS configuration |
| [SPEC-LLM-GATEWAY](./docs/specs/SPEC-LLM-GATEWAY.md) | LLM Gateway specification |
| [SPEC-CIRCUIT-BREAKER](./docs/specs/SPEC-CIRCUIT-BREAKER.md) | Circuit breaker patterns |
| [SPEC-AUTO-REMEDIATION](./docs/specs/SPEC-AUTO-REMEDIATION.md) | Auto-remediation workflows |

### Blueprints (Deployable Configurations)

| Document | Description |
|----------|-------------|
| [BLUEPRINT-NAMESPACE](./docs/blueprints/BLUEPRINT-NAMESPACE.md) | Namespace configuration |
| [BLUEPRINT-DEPLOYMENT](./docs/blueprints/BLUEPRINT-DEPLOYMENT.md) | Deployment templates |
| [BLUEPRINT-DESTINATION-RULE](./docs/blueprints/BLUEPRINT-DESTINATION-RULE.md) | Istio destination rules |
| [BLUEPRINT-DNS-FAILOVER](./docs/blueprints/BLUEPRINT-DNS-FAILOVER.md) | DNS failover setup |
| [BLUEPRINT-LLM-GATEWAY](./docs/blueprints/BLUEPRINT-LLM-GATEWAY.md) | LLM Gateway deployment |

### Runbooks (Operational Procedures)

| Document | Description |
|----------|-------------|
| [RUNBOOK-PLATFORM](./docs/runbooks/RUNBOOK-PLATFORM.md) | Platform operations |
| [RUNBOOK-DNS-FAILOVER](./docs/runbooks/RUNBOOK-DNS-FAILOVER.md) | DNS failover procedures |

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

### GitOps & IDP

#### Flux
**Repository:** [flux](https://github.com/openova-io/flux)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-FLUX-GITOPS](https://github.com/openova-io/flux/blob/main/docs/ADR-FLUX-GITOPS.md) | ADR | Flux GitOps decision |
| [SPEC-FLUX-STRUCTURE](https://github.com/openova-io/flux/blob/main/docs/SPEC-FLUX-STRUCTURE.md) | SPEC | Flux directory structure |

#### Backstage
**Repository:** [backstage](https://github.com/openova-io/backstage)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-BACKSTAGE-IDP](https://github.com/openova-io/backstage/blob/main/docs/ADR-BACKSTAGE-IDP.md) | ADR | Internal Developer Platform |

---

### Networking

#### Istio
**Repository:** [istio](https://github.com/openova-io/istio)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-ISTIO-SERVICE-MESH](https://github.com/openova-io/istio/blob/main/docs/ADR-ISTIO-SERVICE-MESH.md) | ADR | Istio service mesh (modes: Ambient/Waypoint/Sidecar) |

#### Cilium
**Repository:** [cilium](https://github.com/openova-io/cilium)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CNI-CILIUM-EBPF](https://github.com/openova-io/cilium/blob/main/docs/ADR-CNI-CILIUM-EBPF.md) | ADR | Cilium CNI with eBPF |

#### k8gb
**Repository:** [k8gb](https://github.com/openova-io/k8gb)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-K8GB-GSLB](https://github.com/openova-io/k8gb/blob/main/docs/ADR-K8GB-GSLB.md) | ADR | Global Server Load Balancing |

#### ExternalDNS
**Repository:** [external-dns](https://github.com/openova-io/external-dns)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-EXTERNAL-DNS](https://github.com/openova-io/external-dns/blob/main/docs/ADR-EXTERNAL-DNS.md) | ADR | DNS record synchronization |

---

### Observability

#### Grafana
**Repository:** [grafana](https://github.com/openova-io/grafana)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-OBSERVABILITY-STACK](https://github.com/openova-io/grafana/blob/main/docs/ADR-OBSERVABILITY-STACK.md) | ADR | Grafana LGTM stack |
| [SPEC-OBSERVABILITY-STACK](https://github.com/openova-io/grafana/blob/main/docs/SPEC-OBSERVABILITY-STACK.md) | SPEC | Observability configuration |

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

#### Dragonfly
**Repository:** [dragonfly](https://github.com/openova-io/dragonfly)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CACHING-DRAGONFLY](https://github.com/openova-io/dragonfly/blob/main/docs/ADR-CACHING-DRAGONFLY.md) | ADR | Redis-compatible cache (REPLICAOF DR) |

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
| Cilium | CNI with eBPF |
| Istio | Service mesh |
| Coraza | WAF |
| Flux | GitOps |
| cert-manager | TLS certificates |
| External Secrets | Secrets operator |
| Vault | Secrets backend |
| Kyverno | Policy engine |
| VPA | Vertical autoscaling |
| KEDA | Horizontal autoscaling |
| Grafana Stack | Observability |
| Harbor | Container registry |
| MinIO | Object storage |
| Velero | Backup |
| ExternalDNS | DNS sync |
| k8gb | GSLB |
| Backstage | IDP |

### À La Carte Components

| Component | Purpose |
|-----------|---------|
| CNPG | PostgreSQL |
| MongoDB | Document database |
| Redpanda | Event streaming |
| Dragonfly | Cache |
| Stalwart | Email |
| STUNner | WebRTC |

---

*Part of [OpenOva](https://github.com/openova-io)*
