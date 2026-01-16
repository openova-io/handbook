# BLUEPRINT: Namespace Structure

## Overview

Standard namespace structure for OpenOva platform deployments.

## Namespace Categories

| Namespace | Purpose | Owner |
|-----------|---------|-------|
| `kube-system` | Kubernetes system | Platform |
| `flux-system` | GitOps controllers | Platform |
| `istio-system` | Service mesh | Platform |
| `monitoring` | Observability stack | Platform |
| `platform-services` | Shared platform services | Platform |
| `databases` | Database operators | Platform |
| `<tenant>-*` | Tenant workloads | Tenant |

## Platform Namespaces

```yaml
---
apiVersion: v1
kind: Namespace
metadata:
  name: flux-system
  labels:
    app.kubernetes.io/part-of: openova
    openova.io/component: gitops
---
apiVersion: v1
kind: Namespace
metadata:
  name: istio-system
  labels:
    app.kubernetes.io/part-of: openova
    openova.io/component: mesh
---
apiVersion: v1
kind: Namespace
metadata:
  name: monitoring
  labels:
    app.kubernetes.io/part-of: openova
    openova.io/component: observability
    istio.io/dataplane-mode: ambient
---
apiVersion: v1
kind: Namespace
metadata:
  name: platform-services
  labels:
    app.kubernetes.io/part-of: openova
    openova.io/component: platform
    istio.io/dataplane-mode: ambient
---
apiVersion: v1
kind: Namespace
metadata:
  name: databases
  labels:
    app.kubernetes.io/part-of: openova
    openova.io/component: data
    istio.io/dataplane-mode: ambient
```

## Tenant Namespace Template

```yaml
---
apiVersion: v1
kind: Namespace
metadata:
  name: <tenant>-prod
  labels:
    app.kubernetes.io/part-of: <tenant>
    openova.io/tenant: <tenant>
    openova.io/environment: production
    istio.io/dataplane-mode: ambient
---
apiVersion: v1
kind: Namespace
metadata:
  name: <tenant>-staging
  labels:
    app.kubernetes.io/part-of: <tenant>
    openova.io/tenant: <tenant>
    openova.io/environment: staging
    istio.io/dataplane-mode: ambient
```

## Resource Quotas

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: <tenant>-quota
  namespace: <tenant>-prod
spec:
  hard:
    requests.cpu: "4"
    requests.memory: 8Gi
    limits.cpu: "8"
    limits.memory: 16Gi
    persistentvolumeclaims: "10"
    pods: "50"
```

## Network Policy (Default Deny)

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-all
  namespace: <tenant>-prod
spec:
  podSelector: {}
  policyTypes:
    - Ingress
    - Egress
```

## Related

- [SPEC-PLATFORM-TECH-STACK](../specs/SPEC-PLATFORM-TECH-STACK.md)
- [ADR-REPOSITORY-STRUCTURE](../adrs/ADR-REPOSITORY-STRUCTURE.md)
