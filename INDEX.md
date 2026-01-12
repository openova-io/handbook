# Documentation Index

> **Complete index of all documentation across openova-io and talentmesh-io organizations**
> 
> Last updated: 2026-01-10

---

# PART 1: talentmesh-io (Product Application)

> AI-powered talent assessment platform documentation

## Summary

| Category | Document Count |
|----------|----------------|
| Business | 3 |
| Requirements | 4 |
| Architecture | 4 |
| API Specs | 1 |
| Data Model | 4 |
| Technical | 7 |
| UI/UX | 2 |
| Operations | 2 |
| ADRs | 9 |
| **Total** | **36** |

---

## Business

| Document | Description |
|----------|-------------|
| [BUSINESS_CASE.md](https://github.com/talentmesh-io/handbook/blob/main/business/BUSINESS_CASE.md) | Business case and value proposition |
| [PRODUCT_VISION.md](https://github.com/talentmesh-io/handbook/blob/main/business/PRODUCT_VISION.md) | Product vision and strategy |
| [STAKEHOLDER_PERSONAS.md](https://github.com/talentmesh-io/handbook/blob/main/business/STAKEHOLDER_PERSONAS.md) | User personas and stakeholders |

## Requirements

| Document | Description |
|----------|-------------|
| [FUNCTIONAL_REQUIREMENTS.md](https://github.com/talentmesh-io/handbook/blob/main/requirements/FUNCTIONAL_REQUIREMENTS.md) | Functional requirements specification |
| [NON_FUNCTIONAL_REQUIREMENTS.md](https://github.com/talentmesh-io/handbook/blob/main/requirements/NON_FUNCTIONAL_REQUIREMENTS.md) | Non-functional requirements (performance, security, etc.) |
| [USER_STORIES.md](https://github.com/talentmesh-io/handbook/blob/main/requirements/USER_STORIES.md) | User stories by persona |
| [USE_CASES.md](https://github.com/talentmesh-io/handbook/blob/main/requirements/USE_CASES.md) | Detailed use cases |

## Architecture

| Document | Description |
|----------|-------------|
| [SYSTEM_OVERVIEW.md](https://github.com/talentmesh-io/handbook/blob/main/architecture/SYSTEM_OVERVIEW.md) | High-level system architecture |
| [DATA_ARCHITECTURE.md](https://github.com/talentmesh-io/handbook/blob/main/architecture/DATA_ARCHITECTURE.md) | Data architecture and storage design |
| [INTEGRATION_PATTERNS.md](https://github.com/talentmesh-io/handbook/blob/main/architecture/INTEGRATION_PATTERNS.md) | Service integration patterns |
| [MICROSERVICES_CATALOG.md](https://github.com/talentmesh-io/handbook/blob/main/architecture/MICROSERVICES_CATALOG.md) | Catalog of all microservices |

## API Specs

| Document | Description |
|----------|-------------|
| [API_OVERVIEW.md](https://github.com/talentmesh-io/handbook/blob/main/api-specs/API_OVERVIEW.md) | API overview and conventions |

## Data Model

| Document | Description |
|----------|-------------|
| [DOMAIN_MODEL.md](https://github.com/talentmesh-io/handbook/blob/main/data-model/DOMAIN_MODEL.md) | Domain model and entities |
| [ENTITY_RELATIONSHIP.md](https://github.com/talentmesh-io/handbook/blob/main/data-model/ENTITY_RELATIONSHIP.md) | Entity relationship diagrams |
| [DOCUMENT_SCHEMAS.md](https://github.com/talentmesh-io/handbook/blob/main/data-model/DOCUMENT_SCHEMAS.md) | MongoDB document schemas |
| [EVENT_SCHEMAS.md](https://github.com/talentmesh-io/handbook/blob/main/data-model/EVENT_SCHEMAS.md) | Event/message schemas |

## Technical Specifications

| Document | Description |
|----------|-------------|
| [TECH_STACK.md](https://github.com/talentmesh-io/handbook/blob/main/technical/TECH_STACK.md) | Product technology stack |
| [AI_ML_SPECIFICATIONS.md](https://github.com/talentmesh-io/handbook/blob/main/technical/AI_ML_SPECIFICATIONS.md) | AI/ML model specifications |
| [CLAUDE_WRAPPER_SPEC.md](https://github.com/talentmesh-io/handbook/blob/main/technical/CLAUDE_WRAPPER_SPEC.md) | Claude CLI wrapper specification |
| [WEBRTC_MESH_SPEC.md](https://github.com/talentmesh-io/handbook/blob/main/technical/WEBRTC_MESH_SPEC.md) | WebRTC mesh architecture |
| [SCORING_SERVICE_SPEC.md](https://github.com/talentmesh-io/handbook/blob/main/technical/SCORING_SERVICE_SPEC.md) | Scoring service specification |
| [MATCHING_ALGORITHM_SPEC.md](https://github.com/talentmesh-io/handbook/blob/main/technical/MATCHING_ALGORITHM_SPEC.md) | Candidate-job matching algorithm |
| [VERIFICATION_SYSTEM_SPEC.md](https://github.com/talentmesh-io/handbook/blob/main/technical/VERIFICATION_SYSTEM_SPEC.md) | Credential verification system |

## UI/UX

| Document | Description |
|----------|-------------|
| [USER_FLOWS.md](https://github.com/talentmesh-io/handbook/blob/main/ui-ux/USER_FLOWS.md) | User flow diagrams |
| [WIREFRAMES.md](https://github.com/talentmesh-io/handbook/blob/main/ui-ux/WIREFRAMES.md) | UI wireframes |

## Operations

| Document | Description |
|----------|-------------|
| [DEPLOYMENT_GUIDE.md](https://github.com/talentmesh-io/handbook/blob/main/operations/DEPLOYMENT_GUIDE.md) | Product deployment guide |
| [ROADMAP.md](https://github.com/talentmesh-io/handbook/blob/main/operations/ROADMAP.md) | Product roadmap |

## ADRs (Architecture Decision Records)

| ADR | Title | Description |
|-----|-------|-------------|
| [ADR-002](https://github.com/talentmesh-io/handbook/blob/main/adrs/ADR-002-polyglot-database-strategy.md) | Polyglot Database Strategy | PostgreSQL + MongoDB approach |
| [ADR-003](https://github.com/talentmesh-io/handbook/blob/main/adrs/ADR-003-claude-cli-wrapper.md) | Claude CLI Wrapper | LLM integration design |
| [ADR-005](https://github.com/talentmesh-io/handbook/blob/main/adrs/ADR-005-whisper-cpp-stt.md) | Whisper.cpp STT | Speech-to-text engine |
| [ADR-006](https://github.com/talentmesh-io/handbook/blob/main/adrs/ADR-006-LINKEDIN-ONLY-AUTH.md) | LinkedIn Only Auth | Authentication strategy |
| [ADR-007](https://github.com/talentmesh-io/handbook/blob/main/adrs/ADR-007-event-driven-architecture.md) | Event-Driven Architecture | Async messaging patterns |
| [ADR-009](https://github.com/talentmesh-io/handbook/blob/main/adrs/ADR-009-CLAUDE-CLI-WRAPPER.md) | Claude CLI Wrapper (Updated) | Refined LLM wrapper |
| [ADR-010](https://github.com/talentmesh-io/handbook/blob/main/adrs/ADR-010-WEBRTC-DIRECT-ASSESSMENT.md) | WebRTC Direct Assessment | Real-time video architecture |
| [ADR-015](https://github.com/talentmesh-io/handbook/blob/main/adrs/ADR-015-piper-tts.md) | Piper TTS | Text-to-speech engine |
| [ADR-033](https://github.com/talentmesh-io/handbook/blob/main/adrs/ADR-033-DATABASE-CICD-MIGRATIONS.md) | Database CI/CD Migrations | Database deployment strategy |

---

# PART 2: openova-io (Cloud Platform)

> Kubernetes platform infrastructure documentation

## Summary

| Repository | Document Count |
|------------|----------------|
| handbook | 14 |
| terraform | 3 |
| flux | 2 |
| grafana | 5 |
| external-secrets | 3 |
| kyverno | 2 |
| istio | 1 |
| cilium | 1 |
| cnpg | 1 |
| mongodb | 1 |
| dragonfly | 1 |
| redpanda | 1 |
| minio | 1 |
| velero | 1 |
| cert-manager | 1 |
| keda | 1 |
| stalwart | 1 |
| **Total** | **40** |

---

## handbook (Central Platform Docs)

### Architecture

| Document | Description |
|----------|-------------|
| [DEPLOYMENT_ARCHITECTURE.md](https://github.com/openova-io/handbook/blob/main/architecture/DEPLOYMENT_ARCHITECTURE.md) | K8s deployment patterns |

### Operations

| Document | Description |
|----------|-------------|
| [INFRASTRUCTURE_AGREEMENTS.md](https://github.com/openova-io/handbook/blob/main/operations/INFRASTRUCTURE_AGREEMENTS.md) | Provider SLAs and agreements |
| [VENDOR_EVALUATION.md](https://github.com/openova-io/handbook/blob/main/operations/VENDOR_EVALUATION.md) | Cloud provider evaluation |

### Runbooks

| Document | Description |
|----------|-------------|
| [RUNBOOK.md](https://github.com/openova-io/handbook/blob/main/runbooks/RUNBOOK.md) | Incident response runbook |

### Security

| Document | Description |
|----------|-------------|
| [SECURITY_ARCHITECTURE.md](https://github.com/openova-io/handbook/blob/main/security/SECURITY_ARCHITECTURE.md) | Platform security architecture |

### Technical

| Document | Description |
|----------|-------------|
| [PLATFORM_TECH_STACK.md](https://github.com/openova-io/handbook/blob/main/technical/PLATFORM_TECH_STACK.md) | Platform technology stack |
| [DNS_FAILOVER_SPEC.md](https://github.com/openova-io/handbook/blob/main/technical/DNS_FAILOVER_SPEC.md) | DNS-based failover spec |

### ADRs (Platform-Wide)

| ADR | Title | Description |
|-----|-------|-------------|
| [ADR-001](https://github.com/openova-io/handbook/blob/main/adrs/ADR-001-microservices-architecture.md) | Microservices Architecture | Platform service patterns |
| [ADR-018](https://github.com/openova-io/handbook/blob/main/adrs/ADR-018-IMAGE-REGISTRY-NO-HARBOR.md) | Image Registry (No Harbor) | Direct ghcr.io pulls |
| [ADR-019](https://github.com/openova-io/handbook/blob/main/adrs/ADR-019-TRIVY-CICD-SCANNING.md) | Trivy CI/CD Scanning | Security scanning |
| [ADR-034](https://github.com/openova-io/handbook/blob/main/adrs/ADR-034-OPERATIONAL-RESILIENCE.md) | Operational Resilience | Circuit breakers, SLOs |
| [ADR-035](https://github.com/openova-io/handbook/blob/main/adrs/ADR-035-PROGRESSIVE-DELIVERY.md) | Progressive Delivery | Canary, feature flags |
| [ADR-036](https://github.com/openova-io/handbook/blob/main/adrs/ADR-036-MULTI-REGION-STRATEGY.md) | Multi-Region Strategy | Cross-region deployment |
| [ADR-037](https://github.com/openova-io/handbook/blob/main/adrs/ADR-037-ZERO-HUMAN-INTERVENTION-OPS.md) | Zero Human Intervention | Fully automated ops |
| [ADR-038](https://github.com/openova-io/handbook/blob/main/adrs/ADR-038-PLATFORM-ENGINEERING-TOOLS.md) | Platform Engineering Tools | Crossplane, Backstage |
| [ADR-040](https://github.com/openova-io/handbook/blob/main/adrs/ADR-040-REPOSITORY-STRUCTURE.md) | Repository Structure | Multi-product repos |
| [ADR-043](https://github.com/openova-io/handbook/blob/main/adrs/ADR-043-AIRGAP-COMPLIANCE.md) | Air-Gap Compliance | Regulated environments |

---

## terraform (Infrastructure as Code)

| Document | Description |
|----------|-------------|
| [ADR-014-CONTABO-VPS-INFRASTRUCTURE.md](https://github.com/openova-io/terraform/blob/main/docs/ADR-014-CONTABO-VPS-INFRASTRUCTURE.md) | Contabo VPS decision |
| [CLOUD_PROVIDER_COST_COMPARISON.md](https://github.com/openova-io/terraform/blob/main/docs/CLOUD_PROVIDER_COST_COMPARISON.md) | Provider cost analysis |
| [INFRASTRUCTURE_SETUP.md](https://github.com/openova-io/terraform/blob/main/docs/INFRASTRUCTURE_SETUP.md) | Setup guide |

## flux (GitOps)

| Document | Description |
|----------|-------------|
| [ADR-016-FLUX-GITOPS.md](https://github.com/openova-io/flux/blob/main/docs/ADR-016-FLUX-GITOPS.md) | Flux GitOps decision |
| [ADR-041-GITOPS-RELEASE-MANAGEMENT.md](https://github.com/openova-io/flux/blob/main/docs/ADR-041-GITOPS-RELEASE-MANAGEMENT.md) | Release management |

## grafana (Observability)

| Document | Description |
|----------|-------------|
| [OBSERVABILITY_STACK.md](https://github.com/openova-io/grafana/blob/main/docs/OBSERVABILITY_STACK.md) | Complete LGTM stack |
| [ADR-020-LOGGING-GRAFANA-LOKI.md](https://github.com/openova-io/grafana/blob/main/docs/ADR-020-LOGGING-GRAFANA-LOKI.md) | Loki logging |
| [ADR-024-DISTRIBUTED-TRACING-GRAFANA-TEMPO.md](https://github.com/openova-io/grafana/blob/main/docs/ADR-024-DISTRIBUTED-TRACING-GRAFANA-TEMPO.md) | Tempo tracing |
| [ADR-028-UNIFIED-OBSERVABILITY-GRAFANA-ALLOY.md](https://github.com/openova-io/grafana/blob/main/docs/ADR-028-UNIFIED-OBSERVABILITY-GRAFANA-ALLOY.md) | Alloy collector |
| [ADR-029-METRICS-MIMIR-OTEL.md](https://github.com/openova-io/grafana/blob/main/docs/ADR-029-METRICS-MIMIR-OTEL.md) | Mimir + OTel |

## external-secrets (Secrets Management)

| Document | Description |
|----------|-------------|
| [SECRETS_MANAGEMENT.md](https://github.com/openova-io/external-secrets/blob/main/docs/SECRETS_MANAGEMENT.md) | Secrets management guide |
| [ADR-013-SECRETS-SOPS-ESO.md](https://github.com/openova-io/external-secrets/blob/main/docs/ADR-013-SECRETS-SOPS-ESO.md) | SOPS + ESO |
| [ADR-039-SECRETS-MANAGEMENT-INFISICAL.md](https://github.com/openova-io/external-secrets/blob/main/docs/ADR-039-SECRETS-MANAGEMENT-INFISICAL.md) | Infisical |

## kyverno (Policy Engine)

| Document | Description |
|----------|-------------|
| [ADR-031-POD-SECURITY-NETWORK-POLICIES.md](https://github.com/openova-io/kyverno/blob/main/docs/ADR-031-POD-SECURITY-NETWORK-POLICIES.md) | Pod security |
| [ADR-032-KYVERNO-POLICY-ENGINE.md](https://github.com/openova-io/kyverno/blob/main/docs/ADR-032-KYVERNO-POLICY-ENGINE.md) | Kyverno engine |

## istio (Service Mesh)

| Document | Description |
|----------|-------------|
| [ADR-008-REMOVE-KONG-USE-ISTIO.md](https://github.com/openova-io/istio/blob/main/docs/ADR-008-REMOVE-KONG-USE-ISTIO.md) | Istio as API gateway |

## cilium (CNI)

| Document | Description |
|----------|-------------|
| [ADR-025-CNI-CILIUM-EBPF.md](https://github.com/openova-io/cilium/blob/main/docs/ADR-025-CNI-CILIUM-EBPF.md) | Cilium with eBPF |

## cnpg (PostgreSQL)

| Document | Description |
|----------|-------------|
| [ADR-021-DATABASE-OPERATORS-CNPG-MONGODB.md](https://github.com/openova-io/cnpg/blob/main/docs/ADR-021-DATABASE-OPERATORS-CNPG-MONGODB.md) | CloudNativePG operator |

## mongodb (MongoDB)

| Document | Description |
|----------|-------------|
| [ADR-021-DATABASE-OPERATORS-CNPG-MONGODB.md](https://github.com/openova-io/mongodb/blob/main/docs/ADR-021-DATABASE-OPERATORS-CNPG-MONGODB.md) | MongoDB operator |

## dragonfly (Cache)

| Document | Description |
|----------|-------------|
| [ADR-027-CACHING-DRAGONFLY.md](https://github.com/openova-io/dragonfly/blob/main/docs/ADR-027-CACHING-DRAGONFLY.md) | Dragonfly cache |

## redpanda (Event Streaming)

| Document | Description |
|----------|-------------|
| [ADR-026-EVENT-STREAMING-REDPANDA.md](https://github.com/openova-io/redpanda/blob/main/docs/ADR-026-EVENT-STREAMING-REDPANDA.md) | Redpanda streaming |

## minio (Object Storage)

| Document | Description |
|----------|-------------|
| [ADR-012-MINIO-BLOCK-STORAGE.md](https://github.com/openova-io/minio/blob/main/docs/ADR-012-MINIO-BLOCK-STORAGE.md) | MinIO storage |

## velero (Backup)

| Document | Description |
|----------|-------------|
| [ADR-023-BACKUP-CLOUDFLARE-R2.md](https://github.com/openova-io/velero/blob/main/docs/ADR-023-BACKUP-CLOUDFLARE-R2.md) | Velero + R2 |

## cert-manager (TLS)

| Document | Description |
|----------|-------------|
| [ADR-017-CERT-MANAGER-HTTP01.md](https://github.com/openova-io/cert-manager/blob/main/docs/ADR-017-CERT-MANAGER-HTTP01.md) | cert-manager |

## keda (Autoscaling)

| Document | Description |
|----------|-------------|
| [ADR-030-K8S-WORKLOAD-MANAGEMENT.md](https://github.com/openova-io/keda/blob/main/docs/ADR-030-K8S-WORKLOAD-MANAGEMENT.md) | KEDA autoscaling |

## stalwart (Email)

| Document | Description |
|----------|-------------|
| [ADR-022-EMAIL-PLATFORM-STALWART.md](https://github.com/openova-io/stalwart/blob/main/docs/ADR-022-EMAIL-PLATFORM-STALWART.md) | Stalwart email |

---

# Appendix: Complete ADR Index (39 Total)

## talentmesh-io ADRs (9)

| # | ADR | Repository | Title |
|---|-----|------------|-------|
| 1 | ADR-002 | handbook | Polyglot Database Strategy |
| 2 | ADR-003 | handbook | Claude CLI Wrapper |
| 3 | ADR-005 | handbook | Whisper.cpp STT |
| 4 | ADR-006 | handbook | LinkedIn Only Auth |
| 5 | ADR-007 | handbook | Event-Driven Architecture |
| 6 | ADR-009 | handbook | Claude CLI Wrapper (Updated) |
| 7 | ADR-010 | handbook | WebRTC Direct Assessment |
| 8 | ADR-015 | handbook | Piper TTS |
| 9 | ADR-033 | handbook | Database CI/CD Migrations |

## openova-io ADRs (30)

| # | ADR | Repository | Title |
|---|-----|------------|-------|
| 1 | ADR-001 | handbook | Microservices Architecture |
| 2 | ADR-008 | istio | Remove Kong, Use Istio |
| 3 | ADR-012 | minio | MinIO Block Storage |
| 4 | ADR-013 | external-secrets | Secrets SOPS ESO |
| 5 | ADR-014 | terraform | Contabo VPS Infrastructure |
| 6 | ADR-016 | flux | Flux GitOps |
| 7 | ADR-017 | cert-manager | Cert-Manager HTTP01 |
| 8 | ADR-018 | handbook | Image Registry No Harbor |
| 9 | ADR-019 | handbook | Trivy CI/CD Scanning |
| 10 | ADR-020 | grafana | Logging Grafana Loki |
| 11 | ADR-021 | cnpg, mongodb | Database Operators |
| 12 | ADR-022 | stalwart | Email Platform Stalwart |
| 13 | ADR-023 | velero | Backup Cloudflare R2 |
| 14 | ADR-024 | grafana | Distributed Tracing Tempo |
| 15 | ADR-025 | cilium | CNI Cilium eBPF |
| 16 | ADR-026 | redpanda | Event Streaming Redpanda |
| 17 | ADR-027 | dragonfly | Caching Dragonfly |
| 18 | ADR-028 | grafana | Unified Observability Alloy |
| 19 | ADR-029 | grafana | Metrics Mimir OTel |
| 20 | ADR-030 | keda | K8s Workload Management |
| 21 | ADR-031 | kyverno | Pod Security Network Policies |
| 22 | ADR-032 | kyverno | Kyverno Policy Engine |
| 23 | ADR-034 | handbook | Operational Resilience |
| 24 | ADR-035 | handbook | Progressive Delivery |
| 25 | ADR-036 | handbook | Multi-Region Strategy |
| 26 | ADR-037 | handbook | Zero Human Intervention Ops |
| 27 | ADR-038 | handbook | Platform Engineering Tools |
| 28 | ADR-039 | external-secrets | Secrets Management Infisical |
| 29 | ADR-040 | handbook | Repository Structure |
| 30 | ADR-041 | flux | GitOps Release Management |
| 31 | ADR-043 | handbook | Air-Gap Compliance |

---

*Generated: 2026-01-10 | Total Documents: 76 (unique) | Total ADRs: 39*
