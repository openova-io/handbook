# ADR: Image Registry - No Harbor for MVP

**Status:** Accepted
**Date:** 2024-06-01

## Context

Container images need a registry. Options: self-hosted (Harbor) or managed (ghcr.io).

## Decision

Use GitHub Container Registry (ghcr.io) directly. Do NOT deploy Harbor for MVP.

## Rationale

- **Resource constraints** - 24GB total RAM, Harbor requires ~2GB
- **Single developer** - No team requiring role-based access
- **GitHub native** - Already using GitHub Actions
- **No air-gap** - Internet connectivity available

## When to Reconsider

- Air-gapped environments required
- Enterprise RBAC for image access needed
- Multi-region image replication needed

## Consequences

**Positive:** Zero resource consumption, no maintenance, native GitHub integration
**Negative:** External service dependency, no offline capability
