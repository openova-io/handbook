# OpenOva Platform Documentation Index

> **Kubernetes platform infrastructure documentation for multi-tenant cloud operations**
>
> Last updated: 2026-01-12

---

## Quick Navigation

| Section | Description |
|---------|-------------|
| [Platform Overview](#platform-overview) | Architecture, deployment, and technology stack |
| [Platform Services](#platform-services) | Reusable platform service specifications |
| [Security](#security) | Security architecture and compliance |
| [Operations](#operations) | Runbooks, vendor agreements, and SLAs |
| [Architecture Decisions](#architecture-decision-records-adrs) | All ADRs across openova-io repositories |
| [Infrastructure Components](#infrastructure-component-repositories) | Per-component documentation |

---

## Platform Overview

### Summary

| Category | Documents | Location |
|----------|-----------|----------|
| Architecture | 1 | handbook |
| Technical Specs | 2 | handbook |
| Platform Services | 1 | handbook |
| Security | 1 | handbook |
| Operations | 2 | handbook |
| Runbooks | 1 | handbook |
| ADRs (handbook) | 10 | handbook |
| ADRs (other repos) | 21 | distributed |
| **Total (handbook)** | **18** | - |
| **Total (all repos)** | **42** | - |

---

## This Repository (handbook)

### Architecture

| Document | Description |
|----------|-------------|
| [DEPLOYMENT_ARCHITECTURE.md](architecture/DEPLOYMENT_ARCHITECTURE.md) | Kubernetes deployment patterns, multi-tenant isolation, resource quotas |

### Technical Specifications

| Document | Description |
|----------|-------------|
| [PLATFORM_TECH_STACK.md](technical/PLATFORM_TECH_STACK.md) | Complete platform technology stack and version matrix |
| [DNS_FAILOVER_SPEC.md](technical/DNS_FAILOVER_SPEC.md) | DNS-based failover, health checks, and disaster recovery |

### Platform Services

| Document | Description |
|----------|-------------|
| [LLM_GATEWAY.md](services/LLM_GATEWAY.md) | LLM Gateway service specification for AI workloads |

### Security

| Document | Description |
|----------|-------------|
| [SECURITY_ARCHITECTURE.md](security/SECURITY_ARCHITECTURE.md) | Zero-trust security model, mTLS, RBAC, audit logging |

### Operations

| Document | Description |
|----------|-------------|
| [INFRASTRUCTURE_AGREEMENTS.md](operations/INFRASTRUCTURE_AGREEMENTS.md) | Cloud provider SLAs, support agreements, escalation paths |
| [VENDOR_EVALUATION.md](operations/VENDOR_EVALUATION.md) | Vendor evaluation criteria and selection matrix |

### Runbooks

| Document | Description |
|----------|-------------|
| [RUNBOOK.md](runbooks/RUNBOOK.md) | Incident response procedures, escalation, and recovery playbooks |

### Architecture Decision Records (ADRs)

| ADR | Title | Status |
|-----|-------|--------|
| [ADR-001](adrs/ADR-001-microservices-architecture.md) | Microservices Architecture | Accepted |
| [ADR-018](adrs/ADR-018-IMAGE-REGISTRY-NO-HARBOR.md) | Image Registry (No Harbor) | Accepted |
| [ADR-019](adrs/ADR-019-TRIVY-CICD-SCANNING.md) | Trivy CI/CD Scanning | Accepted |
| [ADR-034](adrs/ADR-034-OPERATIONAL-RESILIENCE.md) | Operational Resilience | Accepted |
| [ADR-035](adrs/ADR-035-PROGRESSIVE-DELIVERY.md) | Progressive Delivery | Accepted |
| [ADR-036](adrs/ADR-036-MULTI-REGION-STRATEGY.md) | Multi-Region Strategy | Accepted |
| [ADR-037](adrs/ADR-037-ZERO-HUMAN-INTERVENTION-OPS.md) | Zero Human Intervention Ops | Accepted |
| [ADR-038](adrs/ADR-038-PLATFORM-ENGINEERING-TOOLS.md) | Platform Engineering Tools | Accepted |
| [ADR-040](adrs/ADR-040-REPOSITORY-STRUCTURE.md) | Repository Structure | Accepted |
| [ADR-043](adrs/ADR-043-AIRGAP-COMPLIANCE.md) | Air-Gap Compliance | Accepted |

---

## Infrastructure Component Repositories

### Core Infrastructure

#### terraform - Infrastructure as Code

| Document | Description |
|----------|-------------|
| [INFRASTRUCTURE_SETUP.md](https://github.com/openova-io/terraform/blob/main/docs/INFRASTRUCTURE_SETUP.md) | Infrastructure provisioning guide |
| [CLOUD_PROVIDER_COST_COMPARISON.md](https://github.com/openova-io/terraform/blob/main/docs/CLOUD_PROVIDER_COST_COMPARISON.md) | Cost analysis across providers |
| [ADR-014](https://github.com/openova-io/terraform/blob/main/docs/ADR-014-CONTABO-VPS-INFRASTRUCTURE.md) | Contabo VPS Infrastructure |

#### flux - GitOps Delivery

| Document | Description |
|----------|-------------|
| [ADR-016](https://github.com/openova-io/flux/blob/main/docs/ADR-016-FLUX-GITOPS.md) | Flux GitOps Strategy |
| [ADR-041](https://github.com/openova-io/flux/blob/main/docs/ADR-041-GITOPS-RELEASE-MANAGEMENT.md) | GitOps Release Management |

---

### Networking & Service Mesh

#### istio - Service Mesh & API Gateway

| Document | Description |
|----------|-------------|
| [ADR-008](https://github.com/openova-io/istio/blob/main/docs/ADR-008-REMOVE-KONG-USE-ISTIO.md) | Remove Kong, Use Istio |

#### cilium - Container Networking (CNI)

| Document | Description |
|----------|-------------|
| [ADR-025](https://github.com/openova-io/cilium/blob/main/docs/ADR-025-CNI-CILIUM-EBPF.md) | Cilium with eBPF |

---

### Observability Stack

#### grafana - Unified Observability (LGTM Stack)

| Document | Description |
|----------|-------------|
| [OBSERVABILITY_STACK.md](https://github.com/openova-io/grafana/blob/main/docs/OBSERVABILITY_STACK.md) | Complete LGTM stack overview |
| [ADR-020](https://github.com/openova-io/grafana/blob/main/docs/ADR-020-LOGGING-GRAFANA-LOKI.md) | Logging with Grafana Loki |
| [ADR-024](https://github.com/openova-io/grafana/blob/main/docs/ADR-024-DISTRIBUTED-TRACING-GRAFANA-TEMPO.md) | Distributed Tracing with Tempo |
| [ADR-028](https://github.com/openova-io/grafana/blob/main/docs/ADR-028-UNIFIED-OBSERVABILITY-GRAFANA-ALLOY.md) | Unified Observability with Alloy |
| [ADR-029](https://github.com/openova-io/grafana/blob/main/docs/ADR-029-METRICS-MIMIR-OTEL.md) | Metrics with Mimir + OpenTelemetry |

---

### Data Layer

#### cnpg - PostgreSQL (CloudNativePG)

| Document | Description |
|----------|-------------|
| [ADR-021](https://github.com/openova-io/cnpg/blob/main/docs/ADR-021-DATABASE-OPERATORS-CNPG-MONGODB.md) | Database Operators (CNPG) |

#### mongodb - Document Database

| Document | Description |
|----------|-------------|
| [ADR-021](https://github.com/openova-io/mongodb/blob/main/docs/ADR-021-DATABASE-OPERATORS-CNPG-MONGODB.md) | Database Operators (MongoDB) |

#### dragonfly - In-Memory Cache

| Document | Description |
|----------|-------------|
| [ADR-027](https://github.com/openova-io/dragonfly/blob/main/docs/ADR-027-CACHING-DRAGONFLY.md) | Dragonfly Caching Layer |

#### redpanda - Event Streaming

| Document | Description |
|----------|-------------|
| [ADR-026](https://github.com/openova-io/redpanda/blob/main/docs/ADR-026-EVENT-STREAMING-REDPANDA.md) | Event Streaming with Redpanda |

#### minio - Object Storage

| Document | Description |
|----------|-------------|
| [ADR-012](https://github.com/openova-io/minio/blob/main/docs/ADR-012-MINIO-BLOCK-STORAGE.md) | MinIO Object Storage |

---

### Security & Compliance

#### external-secrets - Secrets Management

| Document | Description |
|----------|-------------|
| [SECRETS_MANAGEMENT.md](https://github.com/openova-io/external-secrets/blob/main/docs/SECRETS_MANAGEMENT.md) | Secrets management guide |
| [ADR-013](https://github.com/openova-io/external-secrets/blob/main/docs/ADR-013-SECRETS-SOPS-ESO.md) | SOPS + External Secrets Operator |
| [ADR-039](https://github.com/openova-io/external-secrets/blob/main/docs/ADR-039-SECRETS-MANAGEMENT-INFISICAL.md) | Infisical Integration |

#### kyverno - Policy Engine

| Document | Description |
|----------|-------------|
| [ADR-031](https://github.com/openova-io/kyverno/blob/main/docs/ADR-031-POD-SECURITY-NETWORK-POLICIES.md) | Pod Security & Network Policies |
| [ADR-032](https://github.com/openova-io/kyverno/blob/main/docs/ADR-032-KYVERNO-POLICY-ENGINE.md) | Kyverno Policy Engine |

#### cert-manager - TLS Certificate Management

| Document | Description |
|----------|-------------|
| [ADR-017](https://github.com/openova-io/cert-manager/blob/main/docs/ADR-017-CERT-MANAGER-HTTP01.md) | cert-manager with HTTP01 |

---

### Platform Services

#### keda - Event-Driven Autoscaling

| Document | Description |
|----------|-------------|
| [ADR-030](https://github.com/openova-io/keda/blob/main/docs/ADR-030-K8S-WORKLOAD-MANAGEMENT.md) | KEDA Workload Management |

#### velero - Backup & Disaster Recovery

| Document | Description |
|----------|-------------|
| [ADR-023](https://github.com/openova-io/velero/blob/main/docs/ADR-023-BACKUP-CLOUDFLARE-R2.md) | Velero + Cloudflare R2 |

#### stalwart - Email Platform

| Document | Description |
|----------|-------------|
| [ADR-022](https://github.com/openova-io/stalwart/blob/main/docs/ADR-022-EMAIL-PLATFORM-STALWART.md) | Stalwart Email Server |

---

## Complete ADR Index

### ADRs by Category

#### Platform Architecture (handbook)

| ADR | Title | Description |
|-----|-------|-------------|
| ADR-001 | Microservices Architecture | Service decomposition patterns |
| ADR-034 | Operational Resilience | Circuit breakers, retries, SLOs |
| ADR-035 | Progressive Delivery | Canary deployments, feature flags |
| ADR-036 | Multi-Region Strategy | Cross-region deployment patterns |
| ADR-037 | Zero Human Intervention | Fully automated operations |
| ADR-038 | Platform Engineering Tools | Crossplane, Backstage integration |
| ADR-040 | Repository Structure | Multi-product repository layout |
| ADR-043 | Air-Gap Compliance | Regulated environment support |

#### CI/CD & Security (handbook + repos)

| ADR | Repository | Title |
|-----|------------|-------|
| ADR-016 | flux | Flux GitOps |
| ADR-017 | cert-manager | TLS Certificate Management |
| ADR-018 | handbook | Image Registry (No Harbor) |
| ADR-019 | handbook | Trivy CI/CD Scanning |
| ADR-041 | flux | GitOps Release Management |

#### Infrastructure (repos)

| ADR | Repository | Title |
|-----|------------|-------|
| ADR-008 | istio | Service Mesh (Istio) |
| ADR-014 | terraform | Contabo VPS Infrastructure |
| ADR-025 | cilium | CNI with eBPF |

#### Data & Storage (repos)

| ADR | Repository | Title |
|-----|------------|-------|
| ADR-012 | minio | Object Storage |
| ADR-021 | cnpg/mongodb | Database Operators |
| ADR-023 | velero | Backup to R2 |
| ADR-026 | redpanda | Event Streaming |
| ADR-027 | dragonfly | Caching Layer |

#### Observability (grafana)

| ADR | Repository | Title |
|-----|------------|-------|
| ADR-020 | grafana | Logging (Loki) |
| ADR-024 | grafana | Tracing (Tempo) |
| ADR-028 | grafana | Collector (Alloy) |
| ADR-029 | grafana | Metrics (Mimir + OTel) |

#### Security & Policy (repos)

| ADR | Repository | Title |
|-----|------------|-------|
| ADR-013 | external-secrets | SOPS + ESO |
| ADR-031 | kyverno | Pod Security |
| ADR-032 | kyverno | Policy Engine |
| ADR-039 | external-secrets | Infisical |

#### Platform Services (repos)

| ADR | Repository | Title |
|-----|------------|-------|
| ADR-022 | stalwart | Email Platform |
| ADR-030 | keda | Workload Autoscaling |

---

## Repository Map

```
openova-io/
├── handbook/          # This repo - central platform documentation
│   ├── adrs/          # Platform-wide architecture decisions
│   ├── architecture/  # Deployment architecture
│   ├── operations/    # Vendor agreements, infrastructure ops
│   ├── runbooks/      # Incident response procedures
│   ├── security/      # Security architecture
│   ├── services/      # Platform service specifications
│   └── technical/     # Tech stack, DNS failover specs
│
├── terraform/         # Infrastructure as Code (Contabo VPS)
├── flux/              # GitOps configuration and releases
├── grafana/           # Observability stack (LGTM)
├── external-secrets/  # Secrets management (SOPS, ESO, Infisical)
├── kyverno/           # Policy engine and pod security
├── istio/             # Service mesh and API gateway
├── cilium/            # Container networking (eBPF)
├── cnpg/              # PostgreSQL operator
├── mongodb/           # MongoDB operator
├── dragonfly/         # Redis-compatible cache
├── redpanda/          # Kafka-compatible streaming
├── minio/             # S3-compatible object storage
├── velero/            # Backup and disaster recovery
├── cert-manager/      # TLS certificate automation
├── keda/              # Event-driven autoscaling
├── stalwart/          # Email server
└── stunner/           # WebRTC TURN server
```

---

## Related Documentation

For tenant-specific application documentation, see:

| Organization | Repository | Description |
|--------------|------------|-------------|
| [talentmesh-io](https://github.com/talentmesh-io) | [handbook](https://github.com/talentmesh-io/handbook) | Talent Mesh product documentation |

---

*Generated: 2026-01-12 | Total Documents: 42 | Total ADRs: 31*
