# SPEC: Circuit Breaker Configuration

## Overview

Circuit breaker patterns using Istio DestinationRule for automatic outlier detection and ejection.

## Circuit Breaker Strategy

| Service Tier | ejectionTime | Consecutive Errors | maxEjectionPercent |
|--------------|--------------|--------------------|--------------------|
| Critical | 30s | 3 | 50% |
| Standard | 30s | 5 | 50% |
| Background | 60s | 10 | 75% |

## Configuration Parameters

| Parameter | Purpose | Default |
|-----------|---------|---------|
| `consecutiveErrors` | Errors before ejection | 5 |
| `interval` | Analysis time window | 10s |
| `baseEjectionTime` | Minimum ejection time | 30s |
| `maxEjectionPercent` | Max ejected endpoints | 50% |

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

## Related

- [ADR-OPERATIONAL-RESILIENCE](../adrs/ADR-OPERATIONAL-RESILIENCE.md)
- [BLUEPRINT-DESTINATION-RULE](../blueprints/BLUEPRINT-DESTINATION-RULE.md)
