# BLUEPRINT: Cilium Circuit Breaker (CiliumEnvoyConfig)

## Overview

Circuit breaker and load balancing configuration for Cilium Service Mesh using CiliumEnvoyConfig.

## Standard Circuit Breaker

```yaml
apiVersion: cilium.io/v2
kind: CiliumEnvoyConfig
metadata:
  name: <service>-circuit-breaker
  namespace: <tenant>-prod
spec:
  services:
    - name: <service>
      namespace: <tenant>-prod
  resources:
    - "@type": type.googleapis.com/envoy.config.cluster.v3.Cluster
      name: <service>
      connect_timeout: 5s
      circuit_breakers:
        thresholds:
          - priority: DEFAULT
            max_connections: 100
            max_pending_requests: 100
            max_requests: 1000
            max_retries: 3
      outlier_detection:
        consecutive_5xx: 5
        interval: 10s
        base_ejection_time: 30s
        max_ejection_percent: 50
```

## Critical Service (Database Proxy)

```yaml
apiVersion: cilium.io/v2
kind: CiliumEnvoyConfig
metadata:
  name: <tenant>-db-proxy-circuit-breaker
  namespace: <tenant>-prod
spec:
  services:
    - name: <tenant>-db-proxy
      namespace: <tenant>-prod
  resources:
    - "@type": type.googleapis.com/envoy.config.cluster.v3.Cluster
      name: <tenant>-db-proxy
      connect_timeout: 3s
      circuit_breakers:
        thresholds:
          - priority: DEFAULT
            max_connections: 50
            max_pending_requests: 50
            max_retries: 2
      outlier_detection:
        consecutive_5xx: 3
        interval: 5s
        base_ejection_time: 30s
        max_ejection_percent: 50
```

## Background Service (Workers)

```yaml
apiVersion: cilium.io/v2
kind: CiliumEnvoyConfig
metadata:
  name: <tenant>-worker-circuit-breaker
  namespace: <tenant>-prod
spec:
  services:
    - name: <tenant>-worker
      namespace: <tenant>-prod
  resources:
    - "@type": type.googleapis.com/envoy.config.cluster.v3.Cluster
      name: <tenant>-worker
      connect_timeout: 10s
      circuit_breakers:
        thresholds:
          - priority: DEFAULT
            max_connections: 200
            max_pending_requests: 200
            max_retries: 5
      outlier_detection:
        consecutive_5xx: 10
        interval: 30s
        base_ejection_time: 60s
        max_ejection_percent: 75
```

## HTTPRoute with Retries (Gateway API)

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: <service>-route
  namespace: <tenant>-prod
spec:
  parentRefs:
    - name: cilium-gateway
      namespace: cilium-gateway
  hostnames:
    - "app.<domain>"
  rules:
    - matches:
        - path:
            type: PathPrefix
            value: /
      backendRefs:
        - name: <service>
          port: 80
      timeouts:
        request: 30s
      retry:
        attempts: 3
        backoff:
          initialInterval: 100ms
          maxInterval: 10s
```

## Tier Configuration Reference

| Tier | consecutiveErrors | baseEjectionTime | maxEjectionPercent |
|------|-------------------|------------------|-------------------|
| Critical | 3 | 30s | 50% |
| Standard | 5 | 30s | 50% |
| Background | 10 | 60s | 75% |

## Migration from Istio DestinationRule

| Istio Concept | Cilium Equivalent |
|---------------|-------------------|
| DestinationRule | CiliumEnvoyConfig |
| VirtualService | HTTPRoute (Gateway API) |
| outlierDetection | outlier_detection in Cluster config |
| connectionPool | circuit_breakers in Cluster config |

## Related

- [SPEC-CIRCUIT-BREAKER](../specs/SPEC-CIRCUIT-BREAKER.md)
- [ADR-OPERATIONAL-RESILIENCE](../adrs/ADR-OPERATIONAL-RESILIENCE.md)
- [ADR-CILIUM-SERVICE-MESH](../../cilium/docs/ADR-CILIUM-SERVICE-MESH.md)
