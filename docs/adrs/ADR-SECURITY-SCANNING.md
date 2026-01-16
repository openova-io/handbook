# ADR: Security Scanning with Trivy

**Status:** Accepted
**Date:** 2024-06-01

## Context

Container images and Kubernetes configurations need vulnerability scanning.

## Decision

Use Trivy for CI/CD-integrated security scanning.

## Rationale

- **Comprehensive** - Single tool for images, K8s manifests, IaC
- **Active development** - Aqua Security backing
- **Zero cost** - Open source
- **Fast** - Minimal CI pipeline impact

## Alternatives Considered

| Alternative | Why Not Selected |
|-------------|------------------|
| Snyk | Cost for full features |
| Grype | Less comprehensive |
| Harbor scanning | Requires Harbor deployment |

## Consequences

**Positive:** Unified scanning, shift-left security, no Harbor dependency
**Negative:** No registry-level scanning, manual workflow integration
