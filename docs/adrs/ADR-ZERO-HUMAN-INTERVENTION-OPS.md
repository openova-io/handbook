# ADR: Zero Human Intervention Operations

**Status:** Accepted
**Date:** 2024-09-01

## Context

With a single-developer team, manual operations are unsustainable.

## Decision

Implement fully automated operations:
- **Auto-remediation** via GitHub Actions triggered by Alertmanager
- **Cost control** with automated budget enforcement
- **Secret rotation** via CronJobs
- **Compliance automation** for data subject requests

## Rationale

Single developer cannot be on-call 24/7. Full automation provides consistent incident response with near-zero ops burden.

## Auto-Remediation Strategy

| Alert | Auto-Action |
|-------|-------------|
| HighMemoryUsage | Scale up deployment |
| PodCrashLoopBackOff | Restart pod |
| HighErrorRate | Trigger rollback |
| CertificateExpiringSoon | Trigger renewal |
| BudgetExceeded | Block scale-up |

## Cost Control

- **Monthly Budget:** €15 (~$16.50)
- **Warning threshold:** 80%
- **Block threshold:** 100%

## Consequences

**Positive:** No on-call burden, consistent response, cost predictability
**Negative:** Complex setup, risk of automated issues, may miss novel failures

## Related Documents

- [SPEC-AUTO-REMEDIATION](../specs/SPEC-AUTO-REMEDIATION.md)
- [RUNBOOK-PLATFORM](../runbooks/RUNBOOK-PLATFORM.md)
