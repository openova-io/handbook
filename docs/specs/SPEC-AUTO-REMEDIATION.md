# SPEC: Auto-Remediation System

**Updated:** 2026-01-17

## Overview

Fully automated incident response via **Gitea Actions** triggered by Alertmanager webhooks.

## Architecture

```mermaid
flowchart LR
    Alert[Alert Fires] --> AM[Alertmanager]
    AM --> GA[Gitea Actions]
    GA --> Remediate[Auto-Remediate]
    Remediate --> Verify[Verify Fix]
    Verify -->|Success| Resolve[Resolve Alert]
    Verify -->|Failure| Log[Log for Analysis]
```

## Alert-to-Action Mapping

| Alert | Auto-Action | Verification | Fallback |
|-------|-------------|--------------|----------|
| HighMemoryUsage | Scale up deployment | Check memory usage | Log |
| PodCrashLoopBackOff | Restart pod | Check pod status | Check deployments |
| HighErrorRate | Trigger rollback | Check error rate | Log |
| DatabaseConnectionExhausted | Restart PgBouncer | Check connections | Alert |
| CertificateExpiringSoon | Trigger renewal | Check cert expiry | Alert |
| HighLatency | Scale affected service | Check latency | Log |
| BudgetWarning | Log warning | N/A | Block scale-up |
| BudgetExceeded | Block scale-up | N/A | Alert |
| GslbEndpointDown | Check k8gb status | Verify DNS | Alert |
| SplitBrainWitnessUnreachable | Check witness | Verify quorum | Alert |

## Gitea Actions Workflow

```yaml
# .gitea/workflows/auto-remediation.yaml
name: Auto-Remediation
on:
  repository_dispatch:
    types: [alertmanager]

jobs:
  remediate:
    runs-on: ubuntu-latest
    steps:
      - name: Setup kubectl
        uses: azure/setup-kubectl@v3

      - name: Configure kubeconfig
        run: |
          echo "${{ secrets.KUBECONFIG }}" | base64 -d > kubeconfig
          export KUBECONFIG=kubeconfig

      - name: Parse alert
        id: alert
        run: |
          echo "alert_name=${{ github.event.client_payload.alertname }}" >> $GITHUB_OUTPUT
          echo "namespace=${{ github.event.client_payload.namespace }}" >> $GITHUB_OUTPUT

      - name: Remediate HighMemoryUsage
        if: steps.alert.outputs.alert_name == 'HighMemoryUsage'
        run: |
          kubectl scale deployment ${{ github.event.client_payload.deployment }} \
            -n ${{ steps.alert.outputs.namespace }} \
            --replicas=$(($(kubectl get deployment ${{ github.event.client_payload.deployment }} \
              -n ${{ steps.alert.outputs.namespace }} -o jsonpath='{.spec.replicas}')+1))

      - name: Remediate PodCrashLoopBackOff
        if: steps.alert.outputs.alert_name == 'PodCrashLoopBackOff'
        run: |
          kubectl delete pod ${{ github.event.client_payload.pod }} \
            -n ${{ steps.alert.outputs.namespace }}

      - name: Remediate HighErrorRate
        if: steps.alert.outputs.alert_name == 'HighErrorRate'
        run: |
          flux reconcile kustomization ${{ github.event.client_payload.app }} \
            --with-source -n flux-system

      - name: Verify fix
        run: |
          sleep 60
          # Check if alert is resolved
          curl -s http://alertmanager.monitoring:9093/api/v2/alerts | \
            jq -e '.[] | select(.labels.alertname == "${{ steps.alert.outputs.alert_name }}") | select(.status.state == "active")' && \
            echo "::warning::Alert still active" || echo "Alert resolved"
```

## Budget Control

| Threshold | Action |
|-----------|--------|
| 80% of €15 | Warning log |
| 100% of €15 | Block scale-up |

## Secret Rotation Schedule

| Secret Type | Frequency | Method |
|-------------|-----------|--------|
| Database credentials | Monthly | CronJob + ESO |
| JWT signing keys | 30 days | CronJob |
| TLS certificates | Auto | cert-manager |
| Gitea tokens | 90 days | CronJob + ESO |

## GDPR Automation

| Process | Schedule | CronJob |
|---------|----------|---------|
| Data subject requests | Daily 2 AM | `process-data-requests` |
| Data retention | Weekly Sunday 3 AM | `enforce-data-retention` |
| Audit log cleanup | Monthly | `cleanup-audit-logs` |

## Alertmanager Webhook Configuration

```yaml
receivers:
  - name: gitea-actions
    webhook_configs:
      - url: https://gitea.<domain>/api/v1/repos/<org>/platform/actions/dispatches
        http_config:
          authorization:
            type: Bearer
            credentials_file: /etc/alertmanager/gitea-token
        send_resolved: true

route:
  receiver: gitea-actions
  group_by: ['alertname', 'namespace']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 4h
  routes:
    - match:
        severity: critical
      receiver: gitea-actions
      group_wait: 10s
    - match:
        severity: warning
      receiver: gitea-actions
```

## Gitea Token Secret

Managed via ESO PushSecrets:

```yaml
apiVersion: external-secrets.io/v1alpha1
kind: PushSecret
metadata:
  name: push-alertmanager-gitea-token
  namespace: monitoring
spec:
  secretStoreRefs:
    - name: vault-region1
      kind: ClusterSecretStore
  selector:
    secret:
      name: alertmanager-gitea-token
  data:
    - match:
        secretKey: token
        remoteRef:
          remoteKey: monitoring/alertmanager-gitea-token
          property: token
```

## Related

- [ADR-ZERO-HUMAN-INTERVENTION-OPS](../adrs/ADR-ZERO-HUMAN-INTERVENTION-OPS.md)
- [ADR-GITEA](../../gitea/docs/ADR-GITEA.md)
- [RUNBOOK-PLATFORM](../runbooks/RUNBOOK-PLATFORM.md)
