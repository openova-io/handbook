# BLUEPRINT: LLM Gateway Deployment

## Overview

Kubernetes manifests for the LLM Gateway platform service.

## Deployment

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: platform-services
  labels:
    istio.io/dataplane-mode: ambient
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: llm-gateway-config
  namespace: platform-services
data:
  LLM_BACKEND: "cli"
  LLM_POOL_SIZE: "2"
  LLM_KEEP_ALIVE_INTERVAL: "300"
  LLM_REQUEST_TIMEOUT: "60"
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: llm-gateway
  namespace: platform-services
spec:
  replicas: 1
  selector:
    matchLabels:
      app: llm-gateway
  template:
    metadata:
      labels:
        app: llm-gateway
    spec:
      containers:
        - name: llm-gateway
          image: ghcr.io/openova-io/llm-gateway:latest
          ports:
            - containerPort: 5005
          envFrom:
            - configMapRef:
                name: llm-gateway-config
          resources:
            requests:
              memory: "512Mi"
              cpu: "250m"
            limits:
              memory: "1Gi"
              cpu: "500m"
          livenessProbe:
            httpGet:
              path: /health
              port: 5005
            initialDelaySeconds: 30
            periodSeconds: 10
          readinessProbe:
            httpGet:
              path: /health
              port: 5005
            initialDelaySeconds: 10
            periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: llm-gateway
  namespace: platform-services
spec:
  selector:
    app: llm-gateway
  ports:
    - port: 5005
      targetPort: 5005
```

## Service Monitor

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: llm-gateway
  namespace: monitoring
spec:
  selector:
    matchLabels:
      app: llm-gateway
  namespaceSelector:
    matchNames:
      - platform-services
  endpoints:
    - port: http
      path: /metrics
      interval: 30s
```

## Tenant Access

Tenants access via internal service URL:

```
http://llm-gateway.platform-services.svc.cluster.local:5005/v1/chat/completions
```

## Related

- [SPEC-LLM-GATEWAY](../specs/SPEC-LLM-GATEWAY.md)
