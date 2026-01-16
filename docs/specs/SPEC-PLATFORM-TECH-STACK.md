# SPEC: Platform Technology Stack

## Overview

Technology choices for the OpenOva kubernetes platform.

## Infrastructure Summary

| Category | Technology | Purpose |
|----------|------------|---------|
| Orchestration | K3s | Lightweight Kubernetes |
| CNI | Cilium | eBPF networking with Hubble |
| Service Mesh | Istio (Ambient) | Sidecar-less traffic management |
| GitOps | Flux | Continuous delivery |
| TLS | cert-manager | Automated certificates |
| Registry | ghcr.io | Container images |
| Security Scanning | Trivy | CI/CD vulnerability scanning |
| DB Operators | CNPG + MongoDB | Database management |
| Cache | Dragonfly | Redis-compatible |
| Events | Redpanda | Kafka-compatible streaming |
| Objects | MinIO | S3-compatible storage |
| Email | Stalwart | Self-hosted JMAP/IMAP/SMTP |
| Backup | Velero + R2 | Kubernetes backup |
| Logging | Grafana Loki | Log aggregation |
| Tracing | Grafana Tempo | Distributed tracing |
| Metrics | Mimir | Prometheus-compatible |
| Collector | Grafana Alloy | Unified telemetry |

## Kubernetes Cluster (K3s on Contabo VPS)

### Cluster Architecture

| Node | Resources | Role |
|------|-----------|------|
| Node 1 | 4 vCPU, 8GB RAM, 200GB SSD | K3s Server + etcd + Worker |
| Node 2 | 4 vCPU, 8GB RAM, 200GB SSD | K3s Server + etcd + Worker |
| Node 3 | 4 vCPU, 8GB RAM, 200GB SSD | K3s Server + etcd + Worker |
| **Total** | 12 vCPU, 24GB RAM, 600GB SSD | HA quorum |
| **Cost** | €13.50/month (~$15) | |

### Disabled K3s Components

| Component | Reason |
|-----------|--------|
| traefik | Istio handles ingress |
| servicelb | DNS-based failover |
| local-storage | App-level replication |
| flannel | Cilium CNI |
| network-policy | Cilium policies |

## Service Mesh (Istio Ambient)

### Why Ambient Mode?

- No sidecar containers (saves ~50MB per pod)
- Simplified debugging
- Faster pod startup
- Same mTLS and traffic management

### Components

| Component | Deployment | Purpose |
|-----------|------------|---------|
| ztunnel | DaemonSet | L4 proxy, mTLS |
| Ingress Gateway | DaemonSet | External traffic |

## Observability Stack (Grafana LGTM)

| Component | Role | Memory |
|-----------|------|--------|
| **L**oki | Log aggregation | ~500MB |
| **G**rafana | Visualization | ~200MB |
| **T**empo | Distributed tracing | ~300MB |
| **M**imir | Metrics storage | ~500MB |
| Alloy | Unified collector | ~400MB x3 |
| ztunnel | L4 mesh metrics | ~100MB x3 |
| **Total** | | ~3GB |

## High Availability Summary

| Component | HA Strategy |
|-----------|-------------|
| K3s Control Plane | 3-node etcd quorum |
| Load Balancing | DNS-based failover |
| PostgreSQL | CNPG operator (auto-failover) |
| MongoDB | 3-node replica set |
| Dragonfly | 3 replicas StatefulSet |
| Redpanda | 3 brokers with Raft |
| MinIO | Erasure coding |

## Related

- [ADR-REPOSITORY-STRUCTURE](../adrs/ADR-REPOSITORY-STRUCTURE.md)
- [BLUEPRINT-NAMESPACE](../blueprints/BLUEPRINT-NAMESPACE.md)
