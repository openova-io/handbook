# BLUEPRINT: Namespace Structure

## Overview

Standard namespace structure for OpenOva platform deployments.

## Namespace Categories

| Namespace | Purpose | Owner |
|-----------|---------|-------|
| `kube-system` | Kubernetes system | Platform |
| `flux-system` | GitOps controllers | Platform |
| `cilium-gateway` | Cilium Gateway and Service Mesh | Platform |
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
  name: cilium-gateway
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
---
apiVersion: v1
kind: Namespace
metadata:
  name: platform-services
  labels:
    app.kubernetes.io/part-of: openova
    openova.io/component: platform
---
apiVersion: v1
kind: Namespace
metadata:
  name: databases
  labels:
    app.kubernetes.io/part-of: openova
    openova.io/component: data
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
---
apiVersion: v1
kind: Namespace
metadata:
  name: <tenant>-staging
  labels:
    app.kubernetes.io/part-of: <tenant>
    openova.io/tenant: <tenant>
    openova.io/environment: staging
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
