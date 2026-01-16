# ADR: Operational Resilience Patterns

**Status:** Accepted
**Date:** 2024-09-01

## Context

Services need resilience patterns to handle failures gracefully.

## Decision

Implement resilience at the mesh level using Istio:
- Circuit breakers via DestinationRule
- Health probes via Kubernetes
- SLO-based alerting via Grafana

## Rationale

Using Istio provides language-agnostic resilience without code changes. All services automatically get circuit breakers, retries, and timeouts.

## Alternatives Considered

| Alternative | Why Rejected |
|-------------|--------------|
| Application libraries | Per-language implementation, inconsistent |
| Service mesh alternatives | Already using Istio |

## Consequences

**Positive:** Consistent resilience, no code changes, centralized management
**Negative:** Istio dependency, configuration complexity

## Related Documents

- [SPEC-CIRCUIT-BREAKER](../specs/SPEC-CIRCUIT-BREAKER.md)
- [BLUEPRINT-DESTINATION-RULE](../blueprints/BLUEPRINT-DESTINATION-RULE.md)
