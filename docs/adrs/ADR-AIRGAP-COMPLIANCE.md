# ADR: Air-Gap Compliance

**Status:** Accepted (Future)
**Date:** 2024-11-01

## Context

Regulated industries require air-gapped deployments with no internet connectivity.

## Decision

Define air-gap architecture using:
- **DMZ Transfer Zone** for content transfer
- **Harbor** for local container registry
- **Gitea** for local Git server
- **ChartMuseum** for Helm charts
- **Cilium** for network isolation

## Rationale

| Requirement | Source |
|-------------|--------|
| Financial services | PCI-DSS, SOX |
| Government | FedRAMP, NIST |
| Defense | IL4/IL5 |
| Healthcare | HIPAA |

## Architecture

```
Internet Zone → DMZ (Transfer + Scan) → Air-Gapped Production
```

Transfer procedure:
1. Pull images/repos in connected zone
2. Security scan in DMZ
3. Physical media or diode transfer
4. Push to air-gapped registry/Git
5. Flux reconciles from internal sources

## MVP Status

Air-gap support is NOT required for MVP. This defines future enterprise architecture.

## Prerequisites

- Harbor deployment
- Gitea deployment
- ChartMuseum deployment
- Transfer automation scripts

## Consequences

**Positive:** Regulated industry access, premium pricing, security posture
**Negative:** Additional infrastructure, manual transfers, version lag
