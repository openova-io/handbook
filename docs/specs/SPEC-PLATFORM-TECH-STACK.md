# SPEC: Platform Technology Stack

**Updated:** 2026-01-16

## Overview

Technology stack for the OpenOva Kubernetes platform. Components are categorized as **Mandatory** (always installed) or **User Choice** (options available).

## Architecture Overview

```mermaid
flowchart TB
    subgraph External["External Services"]
        DNS[DNS Provider]
        Git[Git Provider]
        Archival[Archival S3]
    end

    subgraph Region1["Region 1"]
        subgraph K8s1["Kubernetes Cluster"]
            Istio1[Istio Gateway]
            Apps1[Applications]
            Data1[Data Services]
        end
        Vault1[Vault]
        Harbor1[Harbor]
        MinIO1[MinIO]
    end

    subgraph Region2["Region 2"]
        subgraph K8s2["Kubernetes Cluster"]
            Istio2[Istio Gateway]
            Apps2[Applications]
            Data2[Data Services]
        end
        Vault2[Vault]
        Harbor2[Harbor]
        MinIO2[MinIO]
    end

    DNS --> Istio1
    DNS --> Istio2
    Harbor1 <-->|"Replicate"| Harbor2
    MinIO1 -->|"Tier to"| Archival
    MinIO2 -->|"Tier to"| Archival
    Vault1 <-->|"PushSecrets"| Vault2
```

## Mandatory Components

### Infrastructure & Provisioning

| Component | Purpose | Notes |
|-----------|---------|-------|
| Terraform | Bootstrap IaC | Initial cluster provisioning only |
| Crossplane | Day-2 IaC | Cloud resource provisioning post-bootstrap |

### Networking

| Component | Purpose | Notes |
|-----------|---------|-------|
| Cilium | CNI with eBPF | Network policies, Hubble observability |
| Istio | Service mesh | User selects mode (Ambient/Waypoint/Sidecar) |
| Coraza | WAF | OWASP CRS, integrated with Istio |
| ExternalDNS | DNS sync | Syncs K8s resources to DNS provider |
| k8gb | GSLB | Cross-region DNS-based load balancing |

### Istio Mode Options

```mermaid
flowchart LR
    subgraph Ambient["Ambient Mode"]
        Z1[ztunnel]
    end
    subgraph Waypoint["Ambient + Waypoint"]
        Z2[ztunnel]
        W[Waypoint Proxy]
    end
    subgraph Sidecar["Sidecar Mode"]
        E[Envoy Sidecar]
    end

    Ambient -->|"L4 only"| L4[mTLS]
    Waypoint -->|"L4 + L7"| L7[Full Traffic Mgmt]
    Sidecar -->|"L4 + L7"| L7Full[Full + Per-Pod Traces]
```

| Mode | L4 mTLS | L7 Traffic | OTel Traces | Resources |
|------|---------|------------|-------------|-----------|
| Ambient | ✅ | ❌ | ⚠️ Limited | Low |
| Ambient + Waypoint | ✅ | ✅ | ✅ | Medium |
| Sidecar | ✅ | ✅ | ✅ | High |

### GitOps & IDP

| Component | Purpose | Notes |
|-----------|---------|-------|
| Flux | GitOps engine | ArgoCD as future option |
| Backstage | Developer portal | Service catalog, templates |

### Security

| Component | Purpose | Notes |
|-----------|---------|-------|
| cert-manager | TLS certificates | Let's Encrypt integration |
| External Secrets (ESO) | Secrets operator | Manages secrets lifecycle |
| Vault | Secrets backend | One per cluster, synced via PushSecrets |
| Kyverno | Policy engine | Auto-generate PDBs, NetworkPolicies |
| Trivy | Security scanning | CI/CD + Harbor + Runtime |

### Scaling

| Component | Purpose | Notes |
|-----------|---------|-------|
| VPA | Vertical autoscaling | Right-sizing pods |
| KEDA | Horizontal autoscaling | Event-driven, scale-to-zero |

### Observability

| Component | Purpose | Notes |
|-----------|---------|-------|
| Grafana Alloy | Telemetry collector | Unified metrics/logs/traces |
| Loki | Log aggregation | Query via LogQL |
| Mimir | Metrics storage | Prometheus-compatible |
| Tempo | Distributed tracing | OpenTelemetry native |
| Grafana | Visualization | Dashboards and alerting |

### Storage & Registry

| Component | Purpose | Notes |
|-----------|---------|-------|
| Harbor | Container registry | Trivy scanning, cross-region replication |
| MinIO | Object storage | Tiered to archival S3 |
| Velero | Backup/restore | Backs up to archival S3 |

## User Choice Options

### Cloud Provider

| Provider | Status | Crossplane Provider |
|----------|--------|---------------------|
| Hetzner Cloud | ✅ Available | hcloud |
| Huawei Cloud | 🔜 Coming | huaweicloud |
| Oracle Cloud (OCI) | 🔜 Coming | oci |
| AWS | 🔜 Coming | aws |
| GCP | 🔜 Coming | gcp |
| Azure | 🔜 Coming | azure |

### Regions

| Option | Description |
|--------|-------------|
| 1 region | Allowed (no DR) |
| 2+ regions | Recommended (multi-region DR) |

### LoadBalancer

| Option | How It Works | Cost |
|--------|--------------|------|
| Cloud Provider LB | Native LB (Hetzner LB, etc.) | ~€5-10/mo |
| k8gb DNS-based LB | Istio Gateway + k8gb health-checks | Free |
| Cilium L2 Mode | ARP-based (same subnet only) | Free |

### DNS Provider

| Provider | Availability | Cost |
|----------|--------------|------|
| Cloudflare | Always | Free |
| Hetzner DNS | If Hetzner chosen | Free |
| AWS Route53 | If AWS chosen | ~$0.50/zone |
| GCP Cloud DNS | If GCP chosen | ~$0.20/zone |
| Azure DNS | If Azure chosen | ~$0.50/zone |

### Secrets Backend

| Option | Type | Notes |
|--------|------|-------|
| Vault self-hosted | Self-hosted | One per cluster, ESO PushSecrets sync |
| HCP Vault | Managed | HashiCorp Cloud Platform |
| Infisical | Managed | Developer-friendly |
| AWS Secrets Manager | Managed | If AWS chosen |
| GCP Secret Manager | Managed | If GCP chosen |
| Azure Key Vault | Managed | If Azure chosen |

### Archival S3 Storage

Used for backup and MinIO tiering:

| Provider | Availability |
|----------|--------------|
| Cloudflare R2 | Always |
| AWS S3 | If AWS chosen |
| GCP GCS | If GCP chosen |
| Azure Blob | If Azure chosen |
| OCI Object Storage | If OCI chosen |
| Huawei OBS | If Huawei chosen |

### WAF Options

| Option | Type | Notes |
|--------|------|-------|
| Coraza | Self-hosted | Free, OWASP CRS |
| Cloudflare WAF | External | Pro tier ($20/mo) |
| AWS WAF | External | If AWS chosen |
| Both (layered) | Hybrid | Defense in depth |

### Git Provider

| Provider | Type |
|----------|------|
| GitHub | SaaS |
| GitLab SaaS | SaaS |
| GitLab Self-Hosted | Self-hosted |

## À La Carte Data Services

| Component | Purpose | DR Strategy |
|-----------|---------|-------------|
| CNPG | PostgreSQL operator | WAL streaming |
| MongoDB | Document database | CDC via Debezium → Redpanda |
| Redpanda | Event streaming | MirrorMaker2 |
| Dragonfly | Redis-compatible cache | REPLICAOF |

## À La Carte Communication

| Component | Purpose |
|-----------|---------|
| Stalwart | Email server (JMAP/IMAP/SMTP) |
| STUNner | WebRTC gateway |

## Multi-Region Data Flow

```mermaid
flowchart TB
    subgraph Region1["Region 1 (Primary)"]
        PG1[CNPG Primary]
        MG1[MongoDB Primary]
        RP1[Redpanda]
        DF1[Dragonfly Primary]
    end

    subgraph Region2["Region 2 (DR)"]
        PG2[CNPG Standby]
        MG2[MongoDB Standby]
        RP2[Redpanda]
        DF2[Dragonfly Replica]
    end

    PG1 -->|"WAL Streaming"| PG2
    MG1 -->|"Debezium CDC"| RP1
    RP1 -->|"MirrorMaker2"| RP2
    RP2 -->|"Sink Connector"| MG2
    DF1 -->|"REPLICAOF"| DF2
```

## Resource Estimates (Per Region)

| Category | Components | Estimated Resources |
|----------|------------|---------------------|
| Core Platform | Istio, Cilium, Flux, ESO, Kyverno | ~2GB RAM |
| Observability | Grafana Stack + Alloy | ~3GB RAM |
| Storage | Harbor, MinIO, Velero | ~4GB RAM |
| Security | Vault, cert-manager, Trivy | ~1GB RAM |
| IDP | Backstage | ~1GB RAM |
| **Minimum Total** | | ~11GB RAM |

**Recommended minimum:** 3 nodes × 8GB RAM = 24GB per region

## Related

- [ADR-PLATFORM-ENGINEERING-TOOLS](../adrs/ADR-PLATFORM-ENGINEERING-TOOLS.md)
- [ADR-MULTI-REGION-STRATEGY](../adrs/ADR-MULTI-REGION-STRATEGY.md)
- [ADR-OPERATIONAL-RESILIENCE](../adrs/ADR-OPERATIONAL-RESILIENCE.md)
