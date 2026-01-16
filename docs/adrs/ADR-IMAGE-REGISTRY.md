# ADR: Image Registry - Harbor

**Status:** Accepted
**Date:** 2024-06-01
**Updated:** 2026-01-16

## Context

Container images require a registry for:
- Secure storage and distribution
- Vulnerability scanning
- Multi-region replication for DR
- Air-gap deployments
- Access control and audit

## Decision

**Harbor is mandatory** as the container registry for all OpenOva deployments.

## Rationale

| Requirement | Harbor | External Registry (ghcr.io) |
|-------------|--------|----------------------------|
| Multi-region replication | ✅ Built-in | ❌ |
| Vulnerability scanning | ✅ Trivy integrated | ⚠️ Depends on provider |
| Air-gap support | ✅ Self-hosted | ❌ |
| RBAC | ✅ Full control | ⚠️ Provider-specific |
| Audit logging | ✅ Complete | ⚠️ Limited |
| No external dependency | ✅ | ❌ |

## Architecture

```mermaid
flowchart TB
    subgraph Region1["Region 1"]
        H1[Harbor Primary]
        CI1[CI/CD Pipeline]
    end

    subgraph Region2["Region 2"]
        H2[Harbor Replica]
    end

    CI1 -->|"Push images"| H1
    H1 -->|"Replicate"| H2
    H1 -->|"Pull"| K8s1[Kubernetes Region 1]
    H2 -->|"Pull"| K8s2[Kubernetes Region 2]
```

## Features Used

| Feature | Purpose |
|---------|---------|
| Registry replication | Cross-region image sync for DR |
| Trivy scanning | Vulnerability detection |
| Robot accounts | CI/CD authentication |
| Project quotas | Resource management |
| Audit logs | Compliance and security |

## Multi-Region Replication

Harbor supports push and pull-based replication:

```mermaid
sequenceDiagram
    participant CI as CI/CD
    participant H1 as Harbor Region 1
    participant H2 as Harbor Region 2

    CI->>H1: Push image:v1.0
    H1->>H1: Scan with Trivy
    H1->>H2: Replicate image:v1.0
    Note over H2: Available for DR
```

**Replication modes:**
- **Push-based**: Primary pushes to replicas (default)
- **Pull-based**: Replicas pull from primary
- **Bidirectional**: Both push and pull (active-active)

## Resource Requirements

| Component | CPU | Memory |
|-----------|-----|--------|
| Harbor Core | 0.5 | 512Mi |
| Registry | 0.5 | 512Mi |
| Database (PostgreSQL) | 0.5 | 512Mi |
| Redis | 0.25 | 256Mi |
| Trivy | 0.5 | 1Gi |
| **Total** | **2.25** | **2.75Gi** |

## Consequences

**Positive:**
- Complete control over image lifecycle
- Built-in vulnerability scanning
- Multi-region replication for DR
- Air-gap ready
- Audit trail for compliance

**Negative:**
- Resource overhead (~3GB RAM)
- Operational responsibility
- Backup requirements (handled by Velero)

## Related

- [ADR-SECURITY-SCANNING](./ADR-SECURITY-SCANNING.md)
- [ADR-MULTI-REGION-STRATEGY](./ADR-MULTI-REGION-STRATEGY.md)
