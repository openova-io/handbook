# OpenOva Documentation Index

Central documentation hub for the OpenOva Kubernetes platform.

**Updated:** 2026-02-07

---

## Handbook Documents

Stitching documents that provide platform-wide perspective.

| Document | Description |
|----------|-------------|
| [Platform Tech Stack](PLATFORM-TECH-STACK.md) | Technology stack overview |
| [Repository Structure](REPOSITORY-STRUCTURE.md) | Repository organization and namespaces |
| [SRE Handbook](SRE.md) | Site reliability engineering practices |

---

## Component Documentation

Each component has a single README.md with complete documentation.

### Infrastructure

| Component | Description |
|-----------|-------------|
| [Bootstrap](../bootstrap/README.md) | Platform bootstrap wizard |
| [Terraform](../terraform/README.md) | Infrastructure as Code (bootstrap) |
| [Flux](../flux/README.md) | GitOps delivery engine |

### Networking & Service Mesh

| Component | Description |
|-----------|-------------|
| [Cilium](../cilium/README.md) | CNI + Service Mesh |
| [k8gb](../k8gb/README.md) | Global Server Load Balancing |

### Security

| Component | Description |
|-----------|-------------|
| [External Secrets](../external-secrets/README.md) | Secrets management (ESO) |
| [Trivy](../trivy/README.md) | Security scanning |
| [Harbor](../harbor/README.md) | Container registry |

### Storage & Backup

| Component | Description |
|-----------|-------------|
| [Velero](../velero/README.md) | Backup and restore |

### Data Services (À La Carte)

| Component | Description |
|-----------|-------------|
| CNPG | PostgreSQL operator |
| MongoDB | Document database |
| Redpanda | Event streaming |
| Valkey | Redis-compatible cache |

### Blueprints (À La Carte)

| Blueprint | Description |
|-----------|-------------|
| [Open Banking](../open-banking/README.md) | Fintech sandbox (PSD2/FAPI) |

---

## Component Summary

### Mandatory Components

| Component | Purpose |
|-----------|---------|
| Terraform | Bootstrap IaC |
| Crossplane | Day-2 cloud provisioning |
| Cilium | CNI + Service Mesh |
| Flux | GitOps |
| Gitea | Internal Git + CI/CD |
| External Secrets | Secrets operator |
| Vault | Secrets backend |
| Kyverno | Policy engine |
| Trivy | Security scanning |
| Grafana Stack | Observability |
| Harbor | Container registry |
| MinIO | Object storage |
| Velero | Backup |
| k8gb | GSLB |
| Backstage | Developer portal |

### À La Carte Components

| Category | Components |
|----------|------------|
| Data | CNPG, MongoDB, Redpanda, Valkey |
| Communication | Stalwart, STUNner |
| Identity | Keycloak |
| Monetization | OpenMeter, Lago |
| Blueprints | Open Banking |

---

*Part of [OpenOva](https://openova.io)*
