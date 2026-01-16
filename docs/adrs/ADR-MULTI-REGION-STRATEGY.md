# ADR: Multi-Region Strategy

**Status:** Accepted
**Date:** 2024-09-01
**Updated:** 2026-01-16

## Context

Enterprise deployments require multi-region capability for:
- Business Continuity Planning (BCP)
- Disaster Recovery (DR)
- Latency optimization for global users
- Regulatory compliance (data sovereignty)

## Decision

**Multi-region is mandatory from day 1** - minimum 2 independent clusters across regions.

### Architecture: Independent Clusters (NOT Stretched)

```
┌─────────────────────────────────────────────────────────────────────┐
│                     Multi-Region Architecture                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   Region 1 (Primary)              Region 2 (DR)                     │
│   ┌─────────────────┐            ┌─────────────────┐                │
│   │ Independent K8s │◄──────────►│ Independent K8s │                │
│   │ Cluster         │  WireGuard │ Cluster         │                │
│   │                 │  or native │                 │                │
│   │ Full stack      │  peering   │ Full stack      │                │
│   └─────────────────┘            └─────────────────┘                │
│          │                              │                           │
│          └──────────┬───────────────────┘                           │
│                     ▼                                               │
│              k8gb (GSLB)                                            │
│              DNS-based failover                                     │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

**Key Principles:**
- Each cluster survives independently during network partition
- No stretched clusters (avoids split-brain, reduces complexity)
- Async data replication between regions (eventual consistency)
- k8gb handles DNS-based global server load balancing

## Rationale

| Strategy | Complexity | Resilience | Selected |
|----------|------------|------------|----------|
| Single region | Low | Poor | ❌ |
| Stretched cluster | High | Risky (split-brain) | ❌ |
| **Independent clusters** | Medium | High | ✅ |

## Cross-Region Networking Options

| Option | Use Case | Notes |
|--------|----------|-------|
| WireGuard mesh | Different providers, secure overlay | Default |
| Native peering | Same provider (Hetzner vSwitch) | Lower latency |

## Data Replication Strategy

Each data service uses its own replication mechanism:

| Service | Replication Method | RPO |
|---------|-------------------|-----|
| CNPG (Postgres) | WAL streaming to standby | Near-zero |
| MongoDB | CDC via Debezium → Redpanda | Seconds |
| Redpanda | MirrorMaker2 | Seconds |
| Dragonfly | REPLICAOF command | Seconds |
| MinIO | Bucket replication | Minutes |
| Harbor | Registry replication | Minutes |
| Vault | ESO PushSecrets to both | Seconds |

## Global Load Balancing

k8gb provides:
- Health-based DNS routing
- Automatic failover when region is unhealthy
- Geo-based routing (optional)
- Integration with ExternalDNS

## Region Options

| Provider | Available Regions |
|----------|------------------|
| Hetzner Cloud | eu-central (Falkenstein), eu-west (Helsinki), us-east (Ashburn) |
| Huawei Cloud | eu-west (Paris), ap-southeast (Singapore), etc. |
| OCI | eu-frankfurt, eu-amsterdam, us-phoenix, etc. |

## Consequences

**Positive:**
- True disaster recovery capability
- Each region survives independently
- No split-brain scenarios
- Flexibility in provider selection

**Negative:**
- Increased infrastructure cost (2x clusters)
- Cross-region latency for data sync
- Operational complexity (manage 2 clusters)
- Eventual consistency trade-offs

## Related

- [SPEC-DNS-FAILOVER](../specs/SPEC-DNS-FAILOVER.md)
- [ADR-BOOTSTRAP-ARCHITECTURE](https://github.com/openova-io/bootstrap/docs/ADR-BOOTSTRAP-ARCHITECTURE.md)
