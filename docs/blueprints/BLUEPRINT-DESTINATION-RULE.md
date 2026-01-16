# BLUEPRINT: Istio DestinationRule

## Overview

Circuit breaker and load balancing configuration for Istio service mesh.

## Standard DestinationRule

```yaml
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: <service>-destination
  namespace: <tenant>-prod
spec:
  host: <service>.<tenant>-prod.svc.cluster.local
  trafficPolicy:
    connectionPool:
      tcp:
        maxConnections: 100
        connectTimeout: 5s
      http:
        h2UpgradePolicy: UPGRADE
        http1MaxPendingRequests: 100
        http2MaxRequests: 1000
        maxRequestsPerConnection: 100
        maxRetries: 3
    outlierDetection:
      consecutive5xxErrors: 5
      interval: 10s
      baseEjectionTime: 30s
      maxEjectionPercent: 50
      minHealthPercent: 30
    loadBalancer:
      simple: LEAST_REQUEST
```

## Critical Service (Database Proxy)

```yaml
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: <tenant>-db-proxy
  namespace: <tenant>-prod
spec:
  host: <tenant>-db-proxy.<tenant>-prod.svc.cluster.local
  trafficPolicy:
    connectionPool:
      tcp:
        maxConnections: 50
        connectTimeout: 3s
      http:
        http1MaxPendingRequests: 50
        maxRetries: 2
    outlierDetection:
      consecutive5xxErrors: 3
      interval: 5s
      baseEjectionTime: 30s
      maxEjectionPercent: 50
      minHealthPercent: 50
```

## Background Service (Workers)

```yaml
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: <tenant>-worker
  namespace: <tenant>-prod
spec:
  host: <tenant>-worker.<tenant>-prod.svc.cluster.local
  trafficPolicy:
    connectionPool:
      tcp:
        maxConnections: 200
        connectTimeout: 10s
      http:
        http1MaxPendingRequests: 200
        maxRetries: 5
    outlierDetection:
      consecutive5xxErrors: 10
      interval: 30s
      baseEjectionTime: 60s
      maxEjectionPercent: 75
```

## Tier Configuration Reference

| Tier | consecutiveErrors | baseEjectionTime | maxEjectionPercent |
|------|-------------------|------------------|-------------------|
| Critical | 3 | 30s | 50% |
| Standard | 5 | 30s | 50% |
| Background | 10 | 60s | 75% |

## Related

- [SPEC-CIRCUIT-BREAKER](../specs/SPEC-CIRCUIT-BREAKER.md)
- [ADR-OPERATIONAL-RESILIENCE](../adrs/ADR-OPERATIONAL-RESILIENCE.md)
