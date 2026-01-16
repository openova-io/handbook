# RUNBOOK: DNS Failover Operations

## Overview

Operational procedures for the DNS-based failover system.

## Health Checks

### Check Health Orchestrator Status

```bash
# Pod status
kubectl get pods -n dns-failover

# Logs
kubectl logs -l app=health-orchestrator -n dns-failover --tail=100

# Health endpoint
kubectl exec -it deploy/health-orchestrator -n dns-failover -- curl localhost:8080/health

# Current healthy nodes
kubectl exec -it deploy/health-orchestrator -n dns-failover -- curl localhost:8080/status
```

### Check CoreDNS Status

```bash
# CoreDNS pods
kubectl get pods -n kube-system -l k8s-app=kube-dns

# Hosts file content
kubectl get configmap coredns-custom -n kube-system -o yaml

# DNS resolution test
kubectl run -it --rm dns-test --image=busybox --restart=Never -- nslookup api.<tenant>.io
```

## Troubleshooting

### Node Not Being Added to DNS

1. Check health endpoint directly:
   ```bash
   curl -s http://<node-ip>:15021/healthz/ready
   ```

2. Check Health Orchestrator logs:
   ```bash
   kubectl logs -l app=health-orchestrator -n dns-failover | grep <node-ip>
   ```

3. Verify ConfigMap is being updated:
   ```bash
   kubectl get configmap coredns-custom -n kube-system -o jsonpath='{.data}'
   ```

### DNS Not Resolving

1. Check CoreDNS logs:
   ```bash
   kubectl logs -l k8s-app=kube-dns -n kube-system --tail=50
   ```

2. Check hosts file is loaded:
   ```bash
   kubectl exec -it coredns-<pod> -n kube-system -- cat /etc/coredns/<tenant>.hosts
   ```

3. Verify Corefile includes hosts:
   ```bash
   kubectl get configmap coredns -n kube-system -o yaml
   ```

### High Failover Latency

1. Check TTL settings:
   - DNS A record: 30s
   - CoreDNS cache: 30s
   - Browser cache: ~60s

2. Reduce check interval if needed:
   ```bash
   kubectl patch configmap health-orchestrator-config -n dns-failover --type merge \
     -p '{"data":{"config.yaml":"health_check:\n  interval_seconds: 3"}}'
   ```

## Adding New Tenant

1. Update health orchestrator config:
   ```bash
   kubectl edit configmap health-orchestrator-config -n dns-failover
   ```

   Add tenant:
   ```yaml
   tenants:
     - name: new-tenant
       domains:
         - api.new-tenant.io
         - app.new-tenant.io
       hosts_key: "new-tenant.hosts"
   ```

2. Update CoreDNS Corefile to include new hosts file

3. Restart Health Orchestrator:
   ```bash
   kubectl rollout restart deployment/health-orchestrator -n dns-failover
   ```

## Recovery Procedures

### Health Orchestrator Down

1. Check pod status:
   ```bash
   kubectl describe pod -l app=health-orchestrator -n dns-failover
   ```

2. If CrashLoopBackOff, check logs:
   ```bash
   kubectl logs -l app=health-orchestrator -n dns-failover --previous
   ```

3. Force restart:
   ```bash
   kubectl delete pod -l app=health-orchestrator -n dns-failover
   ```

4. If persistent issue, fall back to static hosts:
   ```bash
   kubectl patch configmap coredns-custom -n kube-system --type merge \
     -p '{"data":{"<tenant>.hosts":"<node1-ip> api.<tenant>.io app.<tenant>.io\n<node2-ip> api.<tenant>.io app.<tenant>.io"}}'
   ```

## Metrics and Alerts

### Key Metrics

| Metric | Query | Threshold |
|--------|-------|-----------|
| Healthy nodes | `health_orchestrator_healthy_nodes` | <2 = warning |
| Check duration | `health_orchestrator_check_duration_seconds` | >10s = warning |
| DNS updates | `health_orchestrator_dns_updates_total` | Spike = investigate |

### Silence Alerts During Maintenance

```bash
# Create silence
curl -X POST http://alertmanager.monitoring:9093/api/v2/silences \
  -H "Content-Type: application/json" \
  -d '{
    "matchers": [{"name": "alertname", "value": "LowHealthyNodes", "isRegex": false}],
    "startsAt": "'$(date -u +%Y-%m-%dT%H:%M:%SZ)'",
    "endsAt": "'$(date -u -d "+1 hour" +%Y-%m-%dT%H:%M:%SZ)'",
    "comment": "Planned maintenance"
  }'
```

## Related

- [SPEC-DNS-FAILOVER](../specs/SPEC-DNS-FAILOVER.md)
- [BLUEPRINT-DNS-FAILOVER](../blueprints/BLUEPRINT-DNS-FAILOVER.md)
