# SPEC: Circuit Breaker Configuration

**Updated:** 2026-01-17

## Overview

Circuit breaker patterns using **Cilium Service Mesh** (CiliumEnvoyConfig) for automatic outlier detection and ejection.

## Circuit Breaker Strategy

| Service Tier | ejectionTime | Consecutive Errors | maxEjectionPercent |
|--------------|--------------|--------------------|--------------------|
| Critical | 30s | 3 | 50% |
| Standard | 30s | 5 | 50% |
| Background | 60s | 10 | 75% |

## Configuration Parameters

| Parameter | Purpose | Default |
|-----------|---------|---------|
| `consecutive_5xx` | Errors before ejection | 5 |
| `interval` | Analysis time window | 10s |
| `base_ejection_time` | Minimum ejection time | 30s |
| `max_ejection_percent` | Max ejected endpoints | 50% |

## CiliumEnvoyConfig Example

```yaml
apiVersion: cilium.io/v2
kind: CiliumEnvoyConfig
metadata:
  name: service-circuit-breaker
  namespace: default
spec:
  services:
    - name: my-service
      namespace: default
  resources:
    - "@type": type.googleapis.com/envoy.config.cluster.v3.Cluster
      name: my-service
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

## HTTPRoute with Retries (Gateway API)

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: service-route
spec:
  parentRefs:
    - name: cilium-gateway
  hostnames:
    - "app.example.com"
  rules:
    - matches:
        - path:
            type: PathPrefix
            value: /
      backendRefs:
        - name: my-service
          port: 80
      timeouts:
        request: 30s
      retry:
        attempts: 3
        backoff:
          initialInterval: 100ms
          maxInterval: 10s
```

## Health Probe Strategy

| Probe Type | Purpose | Failure Action |
|------------|---------|----------------|
| Startup | Wait for initialization | Block traffic |
| Readiness | Can accept traffic | Remove from LB |
| Liveness | Process healthy | Restart pod |

### Standard Probe Configuration

```yaml
startupProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 5
  failureThreshold: 30

readinessProbe:
  httpGet:
    path: /health/ready
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10
  failureThreshold: 3

livenessProbe:
  httpGet:
    path: /health/live
    port: 8080
  initialDelaySeconds: 15
  periodSeconds: 20
  failureThreshold: 3
```

## SLO Configuration

| SLI | SLO Target | Alert Threshold |
|-----|------------|-----------------|
| Availability | 99.9% | <99.5% for 5m |
| Latency (p95) | <500ms | >1s for 5m |
| Error Rate | <0.1% | >1% for 5m |

## Migration from Istio

| Istio Concept | Cilium Equivalent |
|---------------|-------------------|
| DestinationRule | CiliumEnvoyConfig |
| VirtualService | HTTPRoute (Gateway API) |
| outlierDetection | outlier_detection in Cluster config |
| connectionPool | circuit_breakers in Cluster config |

## Related

- [ADR-OPERATIONAL-RESILIENCE](../adrs/ADR-OPERATIONAL-RESILIENCE.md)
- [ADR-CILIUM-SERVICE-MESH](../../cilium/docs/ADR-CILIUM-SERVICE-MESH.md)
- [BLUEPRINT-DESTINATION-RULE](../blueprints/BLUEPRINT-DESTINATION-RULE.md)
