# OpenOva Handbook

Central documentation hub for the OpenOva kubernetes platform.

## Documentation Structure

All documentation is organized in the `docs/` directory:

```
handbook/docs/
├── adrs/           # Architecture Decision Records (WHY)
├── specs/          # Technical Specifications (HOW it works)
├── blueprints/     # Deployable Configurations (WHAT to deploy)
├── runbooks/       # Operational Procedures (HOW to operate)
└── README.md       # Documentation index
```

## Quick Links

- **[Documentation Index](./docs/README.md)** - Start here

### Key Documents

- [Platform Tech Stack](./docs/specs/SPEC-PLATFORM-TECH-STACK.md)
- [DNS Failover](./docs/specs/SPEC-DNS-FAILOVER.md)
- [Platform Runbook](./docs/runbooks/RUNBOOK-PLATFORM.md)

### Key ADRs

- [ADR: Microservices Architecture](./docs/adrs/ADR-MICROSERVICES-ARCHITECTURE.md)
- [ADR: Zero Human Intervention Ops](./docs/adrs/ADR-ZERO-HUMAN-INTERVENTION-OPS.md)
- [ADR: Repository Structure](./docs/adrs/ADR-REPOSITORY-STRUCTURE.md)

## Component Documentation

Each infrastructure component has documentation in its own repository:

| Component | Repository | Documentation |
|-----------|------------|---------------|
| Terraform | [terraform](https://github.com/openova-io/terraform) | `docs/` |
| Flux | [flux](https://github.com/openova-io/flux) | `docs/` |
| Istio | [istio](https://github.com/openova-io/istio) | `docs/` |
| Cilium | [cilium](https://github.com/openova-io/cilium) | `docs/` |
| Grafana | [grafana](https://github.com/openova-io/grafana) | `docs/` |
| External Secrets | [external-secrets](https://github.com/openova-io/external-secrets) | `docs/` |
| CNPG | [cnpg](https://github.com/openova-io/cnpg) | `docs/` |
| MongoDB | [mongodb](https://github.com/openova-io/mongodb) | `docs/` |
| Dragonfly | [dragonfly](https://github.com/openova-io/dragonfly) | `docs/` |
| Redpanda | [redpanda](https://github.com/openova-io/redpanda) | `docs/` |
| Kyverno | [kyverno](https://github.com/openova-io/kyverno) | `docs/` |
| KEDA | [keda](https://github.com/openova-io/keda) | `docs/` |
| Velero | [velero](https://github.com/openova-io/velero) | `docs/` |
| cert-manager | [cert-manager](https://github.com/openova-io/cert-manager) | `docs/` |
| MinIO | [minio](https://github.com/openova-io/minio) | `docs/` |
| Stalwart | [stalwart](https://github.com/openova-io/stalwart) | `docs/` |

---

*Part of [OpenOva](https://github.com/openova-io)*
