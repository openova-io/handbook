# OpenOva Documentation Index

Central index of all documentation across OpenOva repositories.

---

## Handbook (Central Documentation)

**Repository:** [handbook](https://github.com/openova-io/handbook)

### Architecture Decision Records (ADRs)
| Document | Description |
|----------|-------------|
| [ADR-MICROSERVICES-ARCHITECTURE](./docs/adrs/ADR-MICROSERVICES-ARCHITECTURE.md) | Microservices architecture decisions |
| [ADR-IMAGE-REGISTRY](./docs/adrs/ADR-IMAGE-REGISTRY.md) | Image registry strategy (no Harbor) |
| [ADR-SECURITY-SCANNING](./docs/adrs/ADR-SECURITY-SCANNING.md) | Trivy CI/CD scanning |
| [ADR-OPERATIONAL-RESILIENCE](./docs/adrs/ADR-OPERATIONAL-RESILIENCE.md) | Operational resilience patterns |
| [ADR-PROGRESSIVE-DELIVERY](./docs/adrs/ADR-PROGRESSIVE-DELIVERY.md) | Progressive delivery strategy |
| [ADR-MULTI-REGION-STRATEGY](./docs/adrs/ADR-MULTI-REGION-STRATEGY.md) | Multi-region deployment |
| [ADR-ZERO-HUMAN-INTERVENTION-OPS](./docs/adrs/ADR-ZERO-HUMAN-INTERVENTION-OPS.md) | Zero human intervention operations |
| [ADR-PLATFORM-ENGINEERING-TOOLS](./docs/adrs/ADR-PLATFORM-ENGINEERING-TOOLS.md) | Platform engineering tooling |
| [ADR-REPOSITORY-STRUCTURE](./docs/adrs/ADR-REPOSITORY-STRUCTURE.md) | Repository organization |
| [ADR-AIRGAP-COMPLIANCE](./docs/adrs/ADR-AIRGAP-COMPLIANCE.md) | Air-gap compliance strategy |

### Technical Specifications (SPECs)
| Document | Description |
|----------|-------------|
| [SPEC-PLATFORM-TECH-STACK](./docs/specs/SPEC-PLATFORM-TECH-STACK.md) | Platform technology stack |
| [SPEC-DNS-FAILOVER](./docs/specs/SPEC-DNS-FAILOVER.md) | DNS failover configuration |
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

### Infrastructure

#### Terraform
**Repository:** [terraform](https://github.com/openova-io/terraform)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CONTABO-VPS-INFRASTRUCTURE](https://github.com/openova-io/terraform/blob/main/docs/ADR-CONTABO-VPS-INFRASTRUCTURE.md) | ADR | Contabo VPS infrastructure decision |
| [SPEC-CLOUD-COST-COMPARISON](https://github.com/openova-io/terraform/blob/main/docs/SPEC-CLOUD-COST-COMPARISON.md) | SPEC | Cloud provider cost analysis |
| [SPEC-INFRASTRUCTURE-SETUP](https://github.com/openova-io/terraform/blob/main/docs/SPEC-INFRASTRUCTURE-SETUP.md) | SPEC | Infrastructure setup guide |

---

### GitOps & Delivery

#### Flux
**Repository:** [flux](https://github.com/openova-io/flux)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-FLUX-GITOPS](https://github.com/openova-io/flux/blob/main/docs/ADR-FLUX-GITOPS.md) | ADR | Flux GitOps decision |
| [ADR-GITOPS-RELEASE-MANAGEMENT](https://github.com/openova-io/flux/blob/main/docs/ADR-GITOPS-RELEASE-MANAGEMENT.md) | ADR | Release management strategy |
| [SPEC-FLUX-STRUCTURE](https://github.com/openova-io/flux/blob/main/docs/SPEC-FLUX-STRUCTURE.md) | SPEC | Flux directory structure |

---

### Networking

#### Istio
**Repository:** [istio](https://github.com/openova-io/istio)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-ISTIO-SERVICE-MESH](https://github.com/openova-io/istio/blob/main/docs/ADR-ISTIO-SERVICE-MESH.md) | ADR | Istio service mesh decision |

#### Cilium
**Repository:** [cilium](https://github.com/openova-io/cilium)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CNI-CILIUM-EBPF](https://github.com/openova-io/cilium/blob/main/docs/ADR-CNI-CILIUM-EBPF.md) | ADR | Cilium CNI with eBPF decision |

---

### Observability

#### Grafana
**Repository:** [grafana](https://github.com/openova-io/grafana)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-OBSERVABILITY-STACK](https://github.com/openova-io/grafana/blob/main/docs/ADR-OBSERVABILITY-STACK.md) | ADR | Grafana LGTM stack decision |
| [SPEC-OBSERVABILITY-STACK](https://github.com/openova-io/grafana/blob/main/docs/SPEC-OBSERVABILITY-STACK.md) | SPEC | Observability configuration |

---

### Security

#### External Secrets
**Repository:** [external-secrets](https://github.com/openova-io/external-secrets)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-SECRETS-MANAGEMENT](https://github.com/openova-io/external-secrets/blob/main/docs/ADR-SECRETS-MANAGEMENT.md) | ADR | Secrets management decision |
| [SPEC-SECRETS-CONFIGURATION](https://github.com/openova-io/external-secrets/blob/main/docs/SPEC-SECRETS-CONFIGURATION.md) | SPEC | Secrets configuration |

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

### Data

#### CNPG (PostgreSQL)
**Repository:** [cnpg](https://github.com/openova-io/cnpg)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-DATABASE-POSTGRESQL](https://github.com/openova-io/cnpg/blob/main/docs/ADR-DATABASE-POSTGRESQL.md) | ADR | PostgreSQL operator decision |

#### MongoDB
**Repository:** [mongodb](https://github.com/openova-io/mongodb)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-DATABASE-MONGODB](https://github.com/openova-io/mongodb/blob/main/docs/ADR-DATABASE-MONGODB.md) | ADR | MongoDB operator decision |

#### Dragonfly
**Repository:** [dragonfly](https://github.com/openova-io/dragonfly)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CACHING-DRAGONFLY](https://github.com/openova-io/dragonfly/blob/main/docs/ADR-CACHING-DRAGONFLY.md) | ADR | Dragonfly caching decision |

#### Redpanda
**Repository:** [redpanda](https://github.com/openova-io/redpanda)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-EVENT-STREAMING-REDPANDA](https://github.com/openova-io/redpanda/blob/main/docs/ADR-EVENT-STREAMING-REDPANDA.md) | ADR | Event streaming decision |

---

### Storage & Backup

#### MinIO
**Repository:** [minio](https://github.com/openova-io/minio)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-OBJECT-STORAGE](https://github.com/openova-io/minio/blob/main/docs/ADR-OBJECT-STORAGE.md) | ADR | Object storage decision |

#### Velero
**Repository:** [velero](https://github.com/openova-io/velero)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-BACKUP-CLOUDFLARE-R2](https://github.com/openova-io/velero/blob/main/docs/ADR-BACKUP-CLOUDFLARE-R2.md) | ADR | Backup to Cloudflare R2 |

---

### Scaling

#### KEDA
**Repository:** [keda](https://github.com/openova-io/keda)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-WORKLOAD-MANAGEMENT](https://github.com/openova-io/keda/blob/main/docs/ADR-WORKLOAD-MANAGEMENT.md) | ADR | Workload autoscaling decision |

---

### Applications

#### Stalwart
**Repository:** [stalwart](https://github.com/openova-io/stalwart)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-EMAIL-PLATFORM](https://github.com/openova-io/stalwart/blob/main/docs/ADR-EMAIL-PLATFORM.md) | ADR | Email platform decision |

---

## Document Types

| Type | Purpose | Location |
|------|---------|----------|
| **ADR** | Architecture Decision Records - WHY we made decisions | `docs/adrs/` or component `docs/` |
| **SPEC** | Technical Specifications - HOW things work | `docs/specs/` or component `docs/` |
| **BLUEPRINT** | Deployable Configurations - WHAT to deploy | `docs/blueprints/` |
| **RUNBOOK** | Operational Procedures - HOW to operate | `docs/runbooks/` |

---

*Part of [OpenOva](https://github.com/openova-io)*
