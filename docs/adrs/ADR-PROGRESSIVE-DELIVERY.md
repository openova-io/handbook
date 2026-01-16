# ADR: Progressive Delivery

**Status:** Accepted
**Date:** 2024-09-01

## Context

Deployments need safe rollout strategies to minimize blast radius.

## Decision

Implement progressive delivery using:
- **Flagger** for canary deployments with automatic rollback
- **Flipt** for feature flags

## Rationale

### Flagger Selection
- Flux-native integration
- Automatic rollback on metric degradation
- No ArgoCD dependency

### Flipt Selection
- Zero cost (open source)
- Simple self-hosted deployment
- Sufficient features for MVP

## Alternatives Considered

| Tool | Why Rejected |
|------|--------------|
| Argo Rollouts | ArgoCD dependency |
| LaunchDarkly | Cost |
| Unleash | Complex setup |

## Consequences

**Positive:** Reduced deployment risk, automatic rollback, controlled rollouts
**Negative:** Additional infrastructure, SDK integration for flags

## Related Documents

- [SPEC-CANARY-DEPLOYMENT](../specs/SPEC-CANARY-DEPLOYMENT.md)
- [SPEC-FEATURE-FLAGS](../specs/SPEC-FEATURE-FLAGS.md)
