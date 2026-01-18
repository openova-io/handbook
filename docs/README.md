# OpenOva Platform Documentation

Central documentation hub for the OpenOva kubernetes platform.

## Document Types

| Type | Purpose | Naming |
|------|---------|--------|
| **ADR** | Architecture Decision Records (WHY) | `ADR-XXX-name.md` (numbered) |
| **SPEC** | Technical Specifications (HOW it works) | `SPEC-name.md` |
| **BLUEPRINT** | Deployable Configurations (WHAT to deploy) | `BLUEPRINT-name.md` |
| **RUNBOOK** | Operational Procedures (HOW to operate) | `RUNBOOK-name.md` |
| **README** | Navigation Entry Points | `README.md` |

## Directory Structure

```
handbook/docs/
├── adrs/                    # Architecture Decision Records
├── specs/                   # Technical Specifications
├── blueprints/              # Deployable Configurations
├── runbooks/                # Operational Procedures
└── README.md                # This file
```

## Quick Navigation

### Architecture Decisions (ADRs)

Platform-wide decisions that span multiple components:

- [ADR-001: Microservices Architecture](./adrs/ADR-001-MICROSERVICES-ARCHITECTURE.md)
- [ADR-018: Image Registry (No Harbor)](./adrs/ADR-018-IMAGE-REGISTRY-NO-HARBOR.md)
- [ADR-019: Security Scanning (Trivy)](./adrs/ADR-019-SECURITY-SCANNING-TRIVY.md)
- [ADR-034: Operational Resilience](./adrs/ADR-034-OPERATIONAL-RESILIENCE.md)
- [ADR-035: Progressive Delivery](./adrs/ADR-035-PROGRESSIVE-DELIVERY.md)
- [ADR-036: Multi-Region Strategy](./adrs/ADR-036-MULTI-REGION-STRATEGY.md)
- [ADR-037: Zero Human Intervention Ops](./adrs/ADR-037-ZERO-HUMAN-INTERVENTION-OPS.md)
- [ADR-038: Platform Engineering Tools](./adrs/ADR-038-PLATFORM-ENGINEERING-TOOLS.md)
- [ADR-040: Repository Structure](./adrs/ADR-040-REPOSITORY-STRUCTURE.md)
- [ADR-043: Air-Gap Compliance](./adrs/ADR-043-AIRGAP-COMPLIANCE.md)

### Technical Specifications

- [SPEC-DNS-FAILOVER](./specs/SPEC-DNS-FAILOVER.md) - DNS-based high availability
- [SPEC-PLATFORM-TECH-STACK](./specs/SPEC-PLATFORM-TECH-STACK.md) - Technology choices
- [SPEC-LLM-GATEWAY](./specs/SPEC-LLM-GATEWAY.md) - LLM Gateway service

### Operational Runbooks

- [RUNBOOK-PLATFORM](./runbooks/RUNBOOK-PLATFORM.md) - Platform operations

### Blueprints

- [BLUEPRINT-NAMESPACE](./blueprints/BLUEPRINT-NAMESPACE.md) - Namespace structure
- [BLUEPRINT-DEPLOYMENT](./blueprints/BLUEPRINT-DEPLOYMENT.md) - Deployment architecture

## Component Documentation

Each infrastructure component has its own repository with dedicated documentation:

| Component | Repository | Primary ADR |
|-----------|------------|-------------|
| Terraform | [terraform](https://github.com/openova-io/terraform) | ADR-014 |
| Flux | [flux](https://github.com/openova-io/flux) | ADR-016 |
| Cilium | [cilium](https://github.com/openova-io/cilium) | ADR-025, ADR-CILIUM-SERVICE-MESH |
| Gitea | [gitea](https://github.com/openova-io/gitea) | ADR-GITEA |
| k8gb | [k8gb](https://github.com/openova-io/k8gb) | ADR-K8GB-GSLB |
| Grafana | [grafana](https://github.com/openova-io/grafana) | ADR-020, ADR-024, ADR-028, ADR-029 |
| External Secrets | [external-secrets](https://github.com/openova-io/external-secrets) | ADR-013, ADR-039 |
| Kyverno | [kyverno](https://github.com/openova-io/kyverno) | ADR-031, ADR-032 |
| CNPG | [cnpg](https://github.com/openova-io/cnpg) | ADR-021 |
| MongoDB | [mongodb](https://github.com/openova-io/mongodb) | ADR-021 |
| Dragonfly | [dragonfly](https://github.com/openova-io/dragonfly) | ADR-027 |
| Redpanda | [redpanda](https://github.com/openova-io/redpanda) | ADR-026 |
| MinIO | [minio](https://github.com/openova-io/minio) | ADR-012 |
| Velero | [velero](https://github.com/openova-io/velero) | ADR-023 |
| cert-manager | [cert-manager](https://github.com/openova-io/cert-manager) | ADR-017 |
| KEDA | [keda](https://github.com/openova-io/keda) | ADR-030 |
| Stalwart | [stalwart](https://github.com/openova-io/stalwart) | ADR-022 |

---

*Part of [OpenOva](https://openova.io)*
