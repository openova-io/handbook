# openova Handbook

Central documentation hub for the openova kubernetes platform.

## Contents

| Directory | Description |
|-----------|-------------|
| [adrs/](./adrs/) | Architecture Decision Records |
| [architecture/](./architecture/) | Platform architecture documentation |
| [guides/](./guides/) | How-to guides and tutorials |
| [operations/](./operations/) | Operational procedures |
| [runbooks/](./runbooks/) | Incident response runbooks |
| [security/](./security/) | Security documentation |
| [services/](./services/) | Platform services for tenants |
| [technical/](./technical/) | Technical specifications |

## Quick Links

### Architecture
- [Deployment Architecture](./architecture/DEPLOYMENT_ARCHITECTURE.md)
- [Platform Tech Stack](./technical/PLATFORM_TECH_STACK.md)

### Platform Services
- [LLM Gateway](./services/LLM_GATEWAY.md) - OpenAI-compatible LLM API
- [DNS Failover](./technical/DNS_FAILOVER_SPEC.md) - High availability DNS

### Operations
- [Vendor Evaluation](./operations/VENDOR_EVALUATION.md)
- [Infrastructure Agreements](./operations/INFRASTRUCTURE_AGREEMENTS.md)

### Key ADRs
- [ADR-001: Microservices Platform](./adrs/ADR-001-microservices-architecture.md)
- [ADR-018: Harbor Registry](./adrs/ADR-018-IMAGE-REGISTRY-NO-HARBOR.md)
- [ADR-037: Zero Human Intervention Ops](./adrs/ADR-037-ZERO-HUMAN-INTERVENTION-OPS.md)
- [ADR-040: Repository Structure](./adrs/ADR-040-REPOSITORY-STRUCTURE.md)

## Component Documentation

Each infrastructure component has its own repository with dedicated documentation:

| Component | Repository | ADR |
|-----------|------------|-----|
| Istio | [openova-io/istio](https://github.com/openova-io/istio) | ADR-008 |
| Cilium | [openova-io/cilium](https://github.com/openova-io/cilium) | ADR-025 |
| CNPG | [openova-io/cnpg](https://github.com/openova-io/cnpg) | ADR-021 |
| Flux | [openova-io/flux](https://github.com/openova-io/flux) | ADR-016 |
| Grafana | [openova-io/grafana](https://github.com/openova-io/grafana) | ADR-020, ADR-024, ADR-028, ADR-029 |

---

*Part of [openova](https://github.com/openova-io)*
