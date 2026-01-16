# ADR: Platform Engineering Tools

**Status:** Accepted
**Date:** 2024-09-01

## Context

Crossplane and Backstage are commonly recommended for Kubernetes platforms.

## Decision

Do NOT adopt Crossplane or Backstage for MVP.

## Crossplane: Not Required

| Factor | Issue |
|--------|-------|
| Provider | No Crossplane provider for Contabo |
| Abstraction | Not needed (single cloud) |
| Resources | ~500MB overhead |

**Reconsider when:** Multi-cloud needed, DBaaS portability required

## Backstage: Not Required

| Factor | Issue |
|--------|-------|
| Team size | Single developer |
| Catalog | Small codebase |
| Resources | ~1GB overhead |

**Reconsider when:** Team grows beyond 3 developers

## What OpenOva Uses (MVP)

| Category | Tool |
|----------|------|
| IaC | Terraform |
| GitOps | Flux |
| Secrets | SOPS + ESO |
| Observability | Grafana Stack |

## Consequences

**Positive:** Reduced complexity, lower overhead, faster MVP
**Negative:** No self-service portal, manual catalog management
