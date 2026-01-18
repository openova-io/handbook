# ADR: Repository Structure

**Status:** Accepted
**Date:** 2024-10-01

## Context

The platform consists of multiple infrastructure components needing clear organization.

## Decision

Adopt product-centric repository structure with one repository per component.

## Structure

```
openova-io/
├── handbook/           # Central documentation
├── terraform/          # Infrastructure as Code
├── flux/               # GitOps configuration
├── cilium/             # CNI + Service Mesh
├── gitea/              # Self-hosted Git
├── k8gb/               # Global Server Load Balancing
├── grafana/            # Observability
├── external-secrets/   # Secrets management
├── kyverno/            # Policy engine
├── cnpg/               # PostgreSQL
├── mongodb/            # MongoDB
├── dragonfly/          # Cache
├── redpanda/           # Streaming
├── minio/              # Object storage
├── velero/             # Backup
├── cert-manager/       # TLS
├── keda/               # Autoscaling
└── stalwart/           # Email
```

## Rationale

- **Independent versioning** - Each component versions separately
- **Flux integration** - Each repo is a GitRepository source
- **Clear ownership** - CODEOWNERS per repository
- **Co-located docs** - Documentation lives with code

## Alternatives Considered

| Alternative | Why Rejected |
|-------------|--------------|
| Monorepo | Coupled deployments |

## Consequences

**Positive:** Clean separation, independent releases, GitOps-native
**Negative:** Many repos, cross-repo coordination needed
