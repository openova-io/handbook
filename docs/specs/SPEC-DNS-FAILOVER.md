# SPEC: DNS Failover with k8gb

**Updated:** 2026-01-16

## Overview

DNS-based failover system using **k8gb** (Kubernetes Global Balancer) for cross-region load balancing and failover, integrated with **ExternalDNS** for DNS record management.

## Architecture

```mermaid
flowchart TB
    subgraph External["External DNS Provider"]
        CF[Cloudflare / Hetzner DNS]
    end

    subgraph Region1["Region 1"]
        subgraph K8s1["Kubernetes"]
            K8GB1[k8gb]
            EDNS1[ExternalDNS]
            GW1[Istio Gateway]
            SVC1[Services]
        end
    end

    subgraph Region2["Region 2"]
        subgraph K8s2["Kubernetes"]
            K8GB2[k8gb]
            EDNS2[ExternalDNS]
            GW2[Istio Gateway]
            SVC2[Services]
        end
    end

    K8GB1 <-->|"Health sync"| K8GB2
    K8GB1 -->|"Update DNS"| EDNS1
    K8GB2 -->|"Update DNS"| EDNS2
    EDNS1 -->|"Sync records"| CF
    EDNS2 -->|"Sync records"| CF
    CF -->|"Route traffic"| GW1
    CF -->|"Route traffic"| GW2
```

## Components

### k8gb (Kubernetes Global Balancer)

CNCF project for multi-cluster GSLB:

| Feature | Description |
|---------|-------------|
| Health-based routing | Routes only to healthy endpoints |
| Geo-based routing | Route by geography (optional) |
| Weighted routing | Distribute traffic by weight |
| Failover | Automatic DNS failover |

### ExternalDNS

Syncs Kubernetes resources to DNS providers:

| Feature | Description |
|---------|-------------|
| Ingress sync | Creates DNS from Ingress resources |
| Service sync | Creates DNS from LoadBalancer services |
| Provider support | Cloudflare, Hetzner, Route53, etc. |

## DNS Provider Options

| Provider | Availability | ExternalDNS Support |
|----------|--------------|---------------------|
| Cloudflare | Always | ✅ |
| Hetzner DNS | If Hetzner chosen | ✅ |
| AWS Route53 | If AWS chosen | ✅ |
| GCP Cloud DNS | If GCP chosen | ✅ |
| Azure DNS | If Azure chosen | ✅ |

## LoadBalancer Options

### Option 1: Cloud Provider LB (Recommended)

```mermaid
flowchart LR
    Client --> DNS[DNS]
    DNS --> LB1[Cloud LB Region 1]
    DNS --> LB2[Cloud LB Region 2]
    LB1 --> GW1[Istio Gateway]
    LB2 --> GW2[Istio Gateway]
```

- Cloud LB (Hetzner LB, OCI LB, etc.) in front of Istio Gateway
- k8gb manages DNS weights/health
- Cost: ~€5-10/mo per region

### Option 2: k8gb DNS-based LB (Free Alternative)

```mermaid
flowchart LR
    Client --> DNS[DNS]
    DNS -->|"Healthy IPs only"| Node1[Node 1]
    DNS -->|"Healthy IPs only"| Node2[Node 2]
    Node1 --> GW1[Istio Gateway<br/>hostNetwork]
    Node2 --> GW2[Istio Gateway<br/>hostNetwork]
```

- Istio Gateway uses `hostNetwork: true`
- k8gb health-checks Gateway endpoints
- k8gb updates DNS to only include healthy nodes
- Client connects directly to node IPs
- Cost: Free

### Option 3: Cilium L2 Mode

- Cilium provides LoadBalancer IP via ARP
- Works only within same L2 subnet
- Single region only
- Cost: Free

## k8gb Configuration

### Gslb Custom Resource

```yaml
apiVersion: k8gb.absa.oss/v1beta1
kind: Gslb
metadata:
  name: app-gslb
  namespace: app
spec:
  ingress:
    ingressClassName: istio
    rules:
      - host: app.example.com
        http:
          paths:
            - path: /
              pathType: Prefix
              backend:
                service:
                  name: app-service
                  port:
                    number: 80
  strategy:
    type: roundRobin  # or failover, geoip
    splitBrainThresholdSeconds: 300
    dnsTtlSeconds: 30
```

### Strategy Options

| Strategy | Description | Use Case |
|----------|-------------|----------|
| `roundRobin` | Even distribution | Active-Active |
| `failover` | Primary/Secondary | Active-Passive |
| `geoip` | Geographic routing | Latency optimization |

## Health Checking

k8gb performs health checks on Gslb endpoints:

```mermaid
sequenceDiagram
    participant K8GB1 as k8gb Region 1
    participant K8GB2 as k8gb Region 2
    participant DNS as DNS Provider

    loop Every 5s
        K8GB1->>K8GB1: Check local endpoints
        K8GB2->>K8GB2: Check local endpoints
        K8GB1->>K8GB2: Share health status
        K8GB2->>K8GB1: Share health status
    end

    alt Region 2 unhealthy
        K8GB1->>DNS: Update: only Region 1 IPs
    else Both healthy
        K8GB1->>DNS: Update: both region IPs
    end
```

## TTL Configuration

| Setting | Value | Purpose |
|---------|-------|---------|
| DNS TTL | 30s | Balance caching vs failover |
| Health check interval | 5s | Detect failures quickly |
| Split-brain threshold | 300s | Prevent flapping |

**Failover time:** 30-60 seconds (DNS TTL + propagation)

## ExternalDNS Configuration

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: external-dns
spec:
  template:
    spec:
      containers:
        - name: external-dns
          image: registry.k8s.io/external-dns/external-dns:latest
          args:
            - --source=ingress
            - --source=service
            - --source=crd
            - --crd-source-apiversion=k8gb.absa.oss/v1beta1
            - --crd-source-kind=Gslb
            - --provider=cloudflare  # or hetzner, aws, gcp, azure
            - --policy=sync
            - --txt-owner-id=openova-cluster-1
```

## Monitoring

### Grafana Dashboard

k8gb exposes metrics for monitoring:

| Metric | Description |
|--------|-------------|
| `k8gb_gslb_healthy_records` | Healthy endpoint count |
| `k8gb_gslb_status` | GSLB status (0=unhealthy, 1=healthy) |
| `k8gb_infoblox_*` | DNS provider metrics |

### Alerts

| Alert | Condition | Severity |
|-------|-----------|----------|
| GslbEndpointDown | healthy_records < expected | Warning |
| GslbAllEndpointsDown | healthy_records = 0 | Critical |
| DNSSyncFailed | sync errors > 0 | Warning |

## Multi-Region Failover Flow

```mermaid
sequenceDiagram
    participant C as Client
    participant DNS as Cloudflare DNS
    participant R1 as Region 1
    participant R2 as Region 2
    participant K8GB as k8gb

    C->>DNS: Resolve app.example.com
    DNS->>C: [R1-IP, R2-IP] (both healthy)
    C->>R1: Request

    Note over R1: Region 1 fails

    K8GB->>K8GB: Detect R1 unhealthy
    K8GB->>DNS: Remove R1-IP

    C->>DNS: Resolve app.example.com
    DNS->>C: [R2-IP] (only healthy)
    C->>R2: Request (failover complete)
```

## Related

- [ADR-MULTI-REGION-STRATEGY](../adrs/ADR-MULTI-REGION-STRATEGY.md)
- [SPEC-PLATFORM-TECH-STACK](./SPEC-PLATFORM-TECH-STACK.md)
- [RUNBOOK-DNS-FAILOVER](../runbooks/RUNBOOK-DNS-FAILOVER.md)
