# ADR: Multi-Region Strategy

**Status:** Accepted (Future)
**Date:** 2024-09-01

## Context

For disaster recovery and latency optimization, multi-region deployment may be needed.

## Decision

Adopt Active-Passive with GeoDNS:
- **Primary:** Europe (Contabo Germany)
- **Secondary:** India (Contabo Mumbai) - Future
- **Routing:** GeoDNS for latency-based routing
- **Replication:** Asynchronous with regional read replicas

## Rationale

Active-Passive provides cost-effective DR with acceptable RPO/RTO for MVP. Active-Active is too complex and expensive.

| Strategy | Complexity | Cost | Selected |
|----------|------------|------|----------|
| Single region | Low | $ | Current |
| Active-Passive | Medium | $$ | **Future** |
| Active-Active | High | $$$ | No |

## Consequences

**Positive:** DR capability, improved ME latency, regional compliance
**Negative:** Increased cost, replication lag, split-brain risk

## Implementation Phases

1. Current: Single region (Europe)
2. Future: Add India as hot standby
3. Future: GeoDNS for automatic routing
