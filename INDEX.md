# OpenOva Documentation Index

Central index of all documentation across OpenOva repositories.

---

## Handbook (Central Documentation)

**Repository:** [handbook](https://github.com/openova-io/handbook)

### Architecture Decision Records (ADRs)
| Document | Description |
|----------|-------------|
| [ADR-MICROSERVICES-ARCHITECTURE](handbook/docs/adrs/ADR-MICROSERVICES-ARCHITECTURE.md) | Microservices architecture decisions |
| [ADR-IMAGE-REGISTRY](handbook/docs/adrs/ADR-IMAGE-REGISTRY.md) | Image registry strategy (no Harbor) |
| [ADR-SECURITY-SCANNING](handbook/docs/adrs/ADR-SECURITY-SCANNING.md) | Trivy CI/CD scanning |
| [ADR-OPERATIONAL-RESILIENCE](handbook/docs/adrs/ADR-OPERATIONAL-RESILIENCE.md) | Operational resilience patterns |
| [ADR-PROGRESSIVE-DELIVERY](handbook/docs/adrs/ADR-PROGRESSIVE-DELIVERY.md) | Progressive delivery strategy |
| [ADR-MULTI-REGION-STRATEGY](handbook/docs/adrs/ADR-MULTI-REGION-STRATEGY.md) | Multi-region deployment |
| [ADR-ZERO-HUMAN-INTERVENTION-OPS](handbook/docs/adrs/ADR-ZERO-HUMAN-INTERVENTION-OPS.md) | Zero human intervention operations |
| [ADR-PLATFORM-ENGINEERING-TOOLS](handbook/docs/adrs/ADR-PLATFORM-ENGINEERING-TOOLS.md) | Platform engineering tooling |
| [ADR-REPOSITORY-STRUCTURE](handbook/docs/adrs/ADR-REPOSITORY-STRUCTURE.md) | Repository organization |
| [ADR-AIRGAP-COMPLIANCE](handbook/docs/adrs/ADR-AIRGAP-COMPLIANCE.md) | Air-gap compliance strategy |

### Technical Specifications (SPECs)
| Document | Description |
|----------|-------------|
| [SPEC-PLATFORM-TECH-STACK](handbook/docs/specs/SPEC-PLATFORM-TECH-STACK.md) | Platform technology stack |
| [SPEC-DNS-FAILOVER](handbook/docs/specs/SPEC-DNS-FAILOVER.md) | DNS failover configuration |
| [SPEC-LLM-GATEWAY](handbook/docs/specs/SPEC-LLM-GATEWAY.md) | LLM Gateway specification |
| [SPEC-CIRCUIT-BREAKER](handbook/docs/specs/SPEC-CIRCUIT-BREAKER.md) | Circuit breaker patterns |
| [SPEC-AUTO-REMEDIATION](handbook/docs/specs/SPEC-AUTO-REMEDIATION.md) | Auto-remediation workflows |

### Blueprints (Deployable Configurations)
| Document | Description |
|----------|-------------|
| [BLUEPRINT-NAMESPACE](handbook/docs/blueprints/BLUEPRINT-NAMESPACE.md) | Namespace configuration |
| [BLUEPRINT-DEPLOYMENT](handbook/docs/blueprints/BLUEPRINT-DEPLOYMENT.md) | Deployment templates |
| [BLUEPRINT-DESTINATION-RULE](handbook/docs/blueprints/BLUEPRINT-DESTINATION-RULE.md) | Istio destination rules |
| [BLUEPRINT-DNS-FAILOVER](handbook/docs/blueprints/BLUEPRINT-DNS-FAILOVER.md) | DNS failover setup |
| [BLUEPRINT-LLM-GATEWAY](handbook/docs/blueprints/BLUEPRINT-LLM-GATEWAY.md) | LLM Gateway deployment |

### Runbooks (Operational Procedures)
| Document | Description |
|----------|-------------|
| [RUNBOOK-PLATFORM](handbook/docs/runbooks/RUNBOOK-PLATFORM.md) | Platform operations |
| [RUNBOOK-DNS-FAILOVER](handbook/docs/runbooks/RUNBOOK-DNS-FAILOVER.md) | DNS failover procedures |

---

## Component Repositories

### Infrastructure

#### Terraform
**Repository:** [terraform](https://github.com/openova-io/terraform)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CONTABO-VPS-INFRASTRUCTURE](terraform/docs/ADR-CONTABO-VPS-INFRASTRUCTURE.md) | ADR | Contabo VPS infrastructure decision |
| [SPEC-CLOUD-COST-COMPARISON](terraform/docs/SPEC-CLOUD-COST-COMPARISON.md) | SPEC | Cloud provider cost analysis |
| [SPEC-INFRASTRUCTURE-SETUP](terraform/docs/SPEC-INFRASTRUCTURE-SETUP.md) | SPEC | Infrastructure setup guide |

---

### GitOps & Delivery

#### Flux
**Repository:** [flux](https://github.com/openova-io/flux)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-FLUX-GITOPS](flux/docs/ADR-FLUX-GITOPS.md) | ADR | Flux GitOps decision |
| [ADR-GITOPS-RELEASE-MANAGEMENT](flux/docs/ADR-GITOPS-RELEASE-MANAGEMENT.md) | ADR | Release management strategy |
| [SPEC-FLUX-STRUCTURE](flux/docs/SPEC-FLUX-STRUCTURE.md) | SPEC | Flux directory structure |

---

### Networking

#### Istio
**Repository:** [istio](https://github.com/openova-io/istio)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-ISTIO-SERVICE-MESH](istio/docs/ADR-ISTIO-SERVICE-MESH.md) | ADR | Istio service mesh decision |

#### Cilium
**Repository:** [cilium](https://github.com/openova-io/cilium)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CNI-CILIUM-EBPF](cilium/docs/ADR-CNI-CILIUM-EBPF.md) | ADR | Cilium CNI with eBPF decision |

---

### Observability

#### Grafana
**Repository:** [grafana](https://github.com/openova-io/grafana)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-OBSERVABILITY-STACK](grafana/docs/ADR-OBSERVABILITY-STACK.md) | ADR | Grafana LGTM stack decision |
| [SPEC-OBSERVABILITY-STACK](grafana/docs/SPEC-OBSERVABILITY-STACK.md) | SPEC | Observability configuration |

---

### Security

#### External Secrets
**Repository:** [external-secrets](https://github.com/openova-io/external-secrets)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-SECRETS-MANAGEMENT](external-secrets/docs/ADR-SECRETS-MANAGEMENT.md) | ADR | Secrets management decision |
| [SPEC-SECRETS-CONFIGURATION](external-secrets/docs/SPEC-SECRETS-CONFIGURATION.md) | SPEC | Secrets configuration |

#### Cert-Manager
**Repository:** [cert-manager](https://github.com/openova-io/cert-manager)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-TLS-CERTIFICATES](cert-manager/docs/ADR-TLS-CERTIFICATES.md) | ADR | TLS certificate management |

#### Kyverno
**Repository:** [kyverno](https://github.com/openova-io/kyverno)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-POLICY-ENGINE](kyverno/docs/ADR-POLICY-ENGINE.md) | ADR | Policy engine decision |

---

### Data

#### CNPG (PostgreSQL)
**Repository:** [cnpg](https://github.com/openova-io/cnpg)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-DATABASE-POSTGRESQL](cnpg/docs/ADR-DATABASE-POSTGRESQL.md) | ADR | PostgreSQL operator decision |

#### MongoDB
**Repository:** [mongodb](https://github.com/openova-io/mongodb)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-DATABASE-MONGODB](mongodb/docs/ADR-DATABASE-MONGODB.md) | ADR | MongoDB operator decision |

#### Dragonfly
**Repository:** [dragonfly](https://github.com/openova-io/dragonfly)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-CACHING-DRAGONFLY](dragonfly/docs/ADR-CACHING-DRAGONFLY.md) | ADR | Dragonfly caching decision |

#### Redpanda
**Repository:** [redpanda](https://github.com/openova-io/redpanda)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-EVENT-STREAMING-REDPANDA](redpanda/docs/ADR-EVENT-STREAMING-REDPANDA.md) | ADR | Event streaming decision |

---

### Storage & Backup

#### MinIO
**Repository:** [minio](https://github.com/openova-io/minio)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-OBJECT-STORAGE](minio/docs/ADR-OBJECT-STORAGE.md) | ADR | Object storage decision |

#### Velero
**Repository:** [velero](https://github.com/openova-io/velero)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-BACKUP-CLOUDFLARE-R2](velero/docs/ADR-BACKUP-CLOUDFLARE-R2.md) | ADR | Backup to Cloudflare R2 |

---

### Scaling

#### KEDA
**Repository:** [keda](https://github.com/openova-io/keda)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-WORKLOAD-MANAGEMENT](keda/docs/ADR-WORKLOAD-MANAGEMENT.md) | ADR | Workload autoscaling decision |

---

### Applications

#### Stalwart
**Repository:** [stalwart](https://github.com/openova-io/stalwart)
| Document | Type | Description |
|----------|------|-------------|
| [ADR-EMAIL-PLATFORM](stalwart/docs/ADR-EMAIL-PLATFORM.md) | ADR | Email platform decision |

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
