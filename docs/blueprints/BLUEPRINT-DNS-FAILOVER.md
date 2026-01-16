# BLUEPRINT: DNS Failover Deployment

## Overview

Kubernetes manifests for the DNS-based failover system.

## Health Orchestrator Deployment

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dns-failover
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: health-orchestrator
  namespace: dns-failover
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: health-orchestrator
rules:
  - apiGroups: [""]
    resources: ["configmaps"]
    verbs: ["get", "patch", "update"]
  - apiGroups: [""]
    resources: ["nodes"]
    verbs: ["list", "watch"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: health-orchestrator
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: health-orchestrator
subjects:
  - kind: ServiceAccount
    name: health-orchestrator
    namespace: dns-failover
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: health-orchestrator-config
  namespace: dns-failover
data:
  config.yaml: |
    nodes:
      - name: node-1
        ip: "${NODE_1_IP}"
        health_endpoint: "http://${NODE_1_IP}:15021/healthz/ready"
      - name: node-2
        ip: "${NODE_2_IP}"
        health_endpoint: "http://${NODE_2_IP}:15021/healthz/ready"
      - name: node-3
        ip: "${NODE_3_IP}"
        health_endpoint: "http://${NODE_3_IP}:15021/healthz/ready"

    tenants:
      - name: <tenant>
        domains:
          - api.<tenant>.io
          - app.<tenant>.io
        hosts_key: "<tenant>.hosts"

    health_check:
      interval_seconds: 5
      timeout_seconds: 2
      failure_threshold: 2
      success_threshold: 1

    coredns:
      configmap_name: "coredns-custom"
      configmap_namespace: "kube-system"
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: health-orchestrator
  namespace: dns-failover
spec:
  replicas: 1
  selector:
    matchLabels:
      app: health-orchestrator
  template:
    metadata:
      labels:
        app: health-orchestrator
    spec:
      serviceAccountName: health-orchestrator
      containers:
        - name: health-orchestrator
          image: ghcr.io/openova-io/health-orchestrator:latest
          ports:
            - containerPort: 8080
          resources:
            requests:
              memory: "16Mi"
              cpu: "10m"
            limits:
              memory: "32Mi"
              cpu: "100m"
          env:
            - name: RUST_LOG
              value: "info"
          volumeMounts:
            - name: config
              mountPath: /etc/health-orchestrator
          livenessProbe:
            httpGet:
              path: /health
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 10
          readinessProbe:
            httpGet:
              path: /health
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 5
      volumes:
        - name: config
          configMap:
            name: health-orchestrator-config
```

## CoreDNS Custom Configuration

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: coredns-custom
  namespace: kube-system
data:
  <tenant>.hosts: |
    # Managed by Health Orchestrator
    # Updated dynamically
```

## Alert Rules

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: dns-failover-alerts
  namespace: monitoring
spec:
  groups:
    - name: dns-failover
      rules:
        - alert: LowHealthyNodes
          expr: health_orchestrator_healthy_nodes < 2
          for: 1m
          labels:
            severity: warning
          annotations:
            summary: "Only {{ $value }} healthy nodes"

        - alert: AllNodesDown
          expr: health_orchestrator_healthy_nodes == 0
          for: 30s
          labels:
            severity: critical
          annotations:
            summary: "No healthy nodes available"
```

## Related

- [SPEC-DNS-FAILOVER](../specs/SPEC-DNS-FAILOVER.md)
- [RUNBOOK-DNS-FAILOVER](../runbooks/RUNBOOK-DNS-FAILOVER.md)
