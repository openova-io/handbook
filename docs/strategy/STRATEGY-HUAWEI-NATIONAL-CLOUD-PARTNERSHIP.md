# OpenOva + Huawei National Cloud Partnership Strategy

> Date: 2026-01-22
> Status: Draft for Internal Review
> Context: Evaluation of Huawei National Cloud Services Catalog alignment

---

## Executive Summary

Huawei's National Cloud Services Catalog represents a traditional **integrator/MSP service model** with per-project, per-manday billing. OpenOva operates as an **ecosystem platform provider** (similar to Red Hat, SUSE, Ubuntu) with blueprints, subscriptions, and transformation partnerships.

**Key Insight**: These models are not mutually exclusive. Red Hat proves this daily - RHEL subscriptions + Red Hat Consulting coexist. OpenOva can absorb this opportunity without compromising its core identity by positioning as **"Platform + Professional Services"**.

---

## Part 1: Catalog Analysis - Service-by-Service Mapping

### Legend
| Symbol | Meaning |
|--------|---------|
| ✅ CORE | Already covered by OpenOva platform/blueprints |
| ⚡ ACCELERATED | PS work, but platform reduces effort 50-80% |
| 🔧 ADDON PS | Traditional PS work, minimal platform overlap |
| ❌ OUT OF SCOPE | Not aligned with OpenOva focus |

---

### 1. Tenant Landing Zone & Service Provision

| # | Service Item | OpenOva Fit | Analysis |
|---|--------------|-------------|----------|
| 1 | Direct Connect LLD | ⚡ ACCELERATED | Terraform modules exist, network architecture is defined |
| 1 | Direct Connect Implementation | ⚡ ACCELERATED | Infrastructure-as-Code execution |
| 2 | IAAS Landing Zone LLD | ✅ CORE | **Bootstrap Wizard does this automatically** |
| 2 | IAAS Landing Zone Implementation | ✅ CORE | **Terraform + Flux handles this** |
| 3 | IAAS Landing Zone (incremental) | ✅ CORE | Crossplane + Backstage catalog |
| 4 | CCE (Container) Provision LLD | ✅ CORE | **K8s is our core competency** |
| 4 | CCE Provision Implementation | ✅ CORE | Automated via bootstrap |
| 5 | DB Service Provision LLD | ✅ CORE | CNPG/MongoDB blueprints with best practices |
| 5 | DB Service Implementation | ✅ CORE | Operator-based, GitOps delivery |

**Summary**: Landing Zone is **90% OpenOva core**. What takes 20 mandays manually takes hours with the platform.

---

### 2. Tenant Migration Services

| # | Service Item | OpenOva Fit | Analysis |
|---|--------------|-------------|----------|
| 1 | VM Host Migration (package) | 🔧 ADDON PS | Lift-and-shift not our focus, but can execute |
| 1 | VM Host Migration (incremental) | 🔧 ADDON PS | Traditional migration work |
| 2 | Container Migration - small | ⚡ ACCELERATED | **Our sweet spot** - Harbor + GitOps pipelines |
| 2 | Container Migration - medium | ⚡ ACCELERATED | Automated with Flux + Gitea Actions |
| 2 | Container Migration - large | ⚡ ACCELERATED | Scale through automation |
| 3 | Storage Migration | 🔧 ADDON PS | Data migration requires hands-on work |
| 4 | DB Migration (homogeneous) | ⚡ ACCELERATED | CNPG migrations, Velero restore |
| 4 | DB Migration (incremental) | ⚡ ACCELERATED | Operator-assisted |

**Summary**: Container migrations are **70% platform-accelerated**. VM migrations are traditional PS.

---

### 3. Tenant O&M (Operations & Maintenance)

| # | Service Item | OpenOva Fit | Analysis |
|---|--------------|-------------|----------|
| 1 | O&M Consultation | ✅ CORE | **This IS our value proposition** - Day-2 excellence |
| 2 | O&M Plan & Design | ✅ CORE | Blueprints encode best practices |
| 2 | TAM Junior Engineer | ⚡ ACCELERATED | Platform reduces TAM overhead |
| 2 | TAM Senior Engineer | ⚡ ACCELERATED | Focus shifts from firefighting to optimization |

**Summary**: O&M is **100% aligned** - this is where OpenOva shines.

---

### 4. DB/Bigdata Consultant Services (Senior Engineer)

| # | Service Item | OpenOva Fit | Analysis |
|---|--------------|-------------|----------|
| 1-2 | DB Homogeneous Migration Consult | ⚡ ACCELERATED | Platform knowledge reduces discovery |
| 3-4 | DB Heterogeneous Migration Consult | 🔧 ADDON PS | Complex transformation work |
| 5 | Bigdata Migration Consult - small | 🔧 ADDON PS | Outside core focus |
| 5 | Bigdata Migration Consult - large | ❌ OUT OF SCOPE | Requires dedicated Bigdata practice |
| 6 | Bigdata IAAS Provision | 🔧 ADDON PS | Huawei MRS/DWS specific |

**Summary**: DB consultation is **partially accelerated**. Bigdata is **edge case**.

---

### 5. Expert Migration Services (Senior Engineer)

| # | Service Item | OpenOva Fit | Analysis |
|---|--------------|-------------|----------|
| 1 | VM Host Migration | 🔧 ADDON PS | Same as standard |
| 2 | Expert Container Migration | ✅ CORE | **Refactoring + tuning is our expertise** |
| 3 | Expert Storage Migration | 🔧 ADDON PS | Data migration work |
| 4 | DB Heterogeneous Migration | 🔧 ADDON PS | Complex transformation |
| 5 | Bigdata Migration | 🔧 ADDON PS | Outside core |

**Summary**: Expert container work with **refactoring and tuning** is OpenOva's wheelhouse.

---

### 6. Security Services

| # | Service Item | OpenOva Fit | Analysis |
|---|--------------|-------------|----------|
| 1 | Tenant Environment Scan | ⚡ ACCELERATED | Trivy + Kyverno + Harbor scanning built-in |
| 1 | Application Layer Scan | ⚡ ACCELERATED | Coraza WAF, security observability |
| 2 | SOC Team (5x8, 7x24) | 🔧 ADDON PS | Requires dedicated SOC practice or partnership |

**Summary**: Security **tooling is built-in**. SOC team is a staffing model.

---

## Part 2: The Model Alignment Framework

### The Perceived Conflict

| Huawei Catalog Model | OpenOva Model |
|---------------------|---------------|
| Project-based | Subscription-based |
| Per-manday billing | Platform + support licensing |
| Integrator mindset | Ecosystem mindset |
| Bespoke delivery | Blueprint-driven delivery |
| Labor-intensive | Automation-first |

### The Resolution: Red Hat Pattern

Red Hat solves the same tension with a **three-tier offering**:

```
┌─────────────────────────────────────────────────────────────┐
│  TIER 1: PLATFORM SUBSCRIPTION                              │
│  - RHEL, OpenShift subscriptions                            │
│  - Updates, security patches, certified ecosystem           │
│  - "The foundation"                                         │
├─────────────────────────────────────────────────────────────┤
│  TIER 2: PREMIUM SUPPORT                                    │
│  - TAM (Technical Account Manager)                          │
│  - Priority support, architecture reviews                   │
│  - "Confidence as a service"                                │
├─────────────────────────────────────────────────────────────┤
│  TIER 3: PROFESSIONAL SERVICES                              │
│  - Red Hat Consulting                                       │
│  - Migration, implementation, custom development            │
│  - "Boutique deep technical work"                           │
└─────────────────────────────────────────────────────────────┘
```

**OpenOva can adopt the same pattern:**

```
┌─────────────────────────────────────────────────────────────┐
│  TIER 1: OPENOVA PLATFORM                                   │
│  - Bootstrap Wizard + Blueprints                            │
│  - GitOps infrastructure, certified components              │
│  - Recurring subscription per cluster                       │
├─────────────────────────────────────────────────────────────┤
│  TIER 2: OPENOVA ASSURANCE                                  │
│  - TAM service, SLA guarantees                              │
│  - Upgrade planning, health reviews                         │
│  - "We own the pager"                                       │
├─────────────────────────────────────────────────────────────┤
│  TIER 3: OPENOVA PROFESSIONAL SERVICES                      │
│  - Migration engagements                                    │
│  - Platform extensions, custom blueprints                   │
│  - Per-project/manday billing (Huawei catalog compatible)   │
└─────────────────────────────────────────────────────────────┘
```

---

## Part 3: Service Category Mapping

### How to Respond to Each Catalog Category

| Catalog Category | OpenOva Response | Commercial Model |
|-----------------|------------------|------------------|
| Landing Zone & Provision | **Platform-included** | Subscription (Tier 1) |
| Container Migration | **Accelerated PS** | Fixed-price project (Tier 3) |
| VM Migration | **Standard PS** | Time & Materials (Tier 3) |
| O&M Consultation | **Platform-included + TAM** | Subscription + TAM (Tier 1+2) |
| TAM Services | **Premium Support** | Monthly retainer (Tier 2) |
| DB Migration (homogeneous) | **Accelerated PS** | Fixed-price project (Tier 3) |
| DB Migration (heterogeneous) | **Standard PS** | Time & Materials (Tier 3) |
| Bigdata Services | **Partner/Subcontract** | Pass-through or decline |
| Security Scanning | **Platform-included** | Subscription (Tier 1) |
| SOC Services | **Partner/Subcontract** | Pass-through to MSSP partner |

---

## Part 4: Value Proposition to Huawei

### What OpenOva Brings That Integrators Don't

| Capability | Traditional Integrator | OpenOva |
|-----------|----------------------|---------|
| Landing Zone | 20 mandays manual setup | 4 hours with Bootstrap Wizard |
| Container Migration | Custom scripts per project | Repeatable GitOps pipelines |
| O&M Documentation | Bespoke per customer | Standardized runbooks in blueprints |
| Upgrades | Risky, manual, project-based | Safe, automated, continuous |
| Knowledge Transfer | Walks out the door | Encoded in blueprints |
| Scalability | Linear with headcount | Platform leverage |

### The "Acceleration Factor" Argument

For services where OpenOva accelerates delivery:

```
Traditional Model:
  Landing Zone LLD:        25 mandays
  Landing Zone Impl:       10 mandays
  Container Migration:     22 mandays (small)
  O&M Setup:              20 mandays
  ─────────────────────────────────────
  Total:                   77 mandays

OpenOva-Accelerated Model:
  Landing Zone:            2 mandays (platform setup + customization)
  Container Migration:     8 mandays (GitOps pipeline setup + execution)
  O&M Setup:              0 mandays (included in platform)
  Platform Subscription:   Annual fee
  ─────────────────────────────────────
  Total PS:                10 mandays + subscription

Customer gets: Faster delivery, repeatable foundation, ongoing support
OpenOva gets: Recurring revenue, higher margin, customer stickiness
Huawei gets: Differentiated offering, higher win rate, customer success
```

---

## Part 5: Communication Plan for Huawei

### Phase 1: Internal Alignment (Pre-Meeting)

**Objective**: Ensure Huawei National Cloud team understands OpenOva's differentiation

**Key Messages**:
1. "We are a platform company that also delivers professional services, not an integrator that has a platform."
2. "Our platform ACCELERATES the catalog services - same outcomes, faster delivery, lower risk."
3. "We bring intellectual property (blueprints) that creates customer stickiness for Huawei Cloud."

**Deliverable**: One-page positioning document showing catalog mapping

### Phase 2: Joint Value Proposition Design

**Objective**: Co-create a joint offering that leverages both parties

**Proposal Structure**:

```
┌──────────────────────────────────────────────────────────────┐
│  HUAWEI + OPENOVA JOINT OFFERING                             │
│                                                              │
│  "Cloud-Native Transformation Accelerator"                   │
│                                                              │
│  ┌────────────────┐    ┌────────────────┐                   │
│  │ HUAWEI CLOUD   │    │ OPENOVA        │                   │
│  │ - Infrastructure│    │ - Platform     │                   │
│  │ - CCE / RDS    │    │ - Blueprints   │                   │
│  │ - Sales & GTM  │    │ - Support      │                   │
│  │ - Relationship │    │ - PS Delivery  │                   │
│  └────────────────┘    └────────────────┘                   │
│                                                              │
│  Packages:                                                   │
│  - Foundation: Platform + 40hrs PS                          │
│  - Professional: Platform + TAM + 80hrs PS                  │
│  - Enterprise: Platform + TAM + Unlimited PS credits        │
└──────────────────────────────────────────────────────────────┘
```

### Phase 3: Catalog Response Document

**Format**: Excel/table showing how OpenOva addresses each line item

| Catalog Item | OpenOva Delivery Method | Effort Reduction | Commercial Model |
|--------------|------------------------|------------------|------------------|
| Landing Zone LLD | Bootstrap Wizard | 90% | Platform subscription |
| CCE Provision | Terraform + Flux | 80% | Platform subscription |
| Container Migration | GitOps pipelines | 60% | Fixed-price PS |
| TAM Service | Included in Premium | - | Support subscription |
| ... | ... | ... | ... |

### Phase 4: Pilot Proposal

**Objective**: Prove the model with a real customer

**Proposal**:
- Select 1 customer with migration project in pipeline
- OpenOva delivers using platform (Huawei observes)
- Track actual effort vs catalog estimates
- Use results to refine joint pricing model

---

## Part 6: Business Model Design

### Option A: Pure Platform + PS (Recommended)

```
Revenue Streams:
├── Platform Subscription (per cluster/year)
│   └── Includes: Bootstrap, Blueprints, Updates, Basic Support
│
├── Premium Support (per cluster/year)
│   └── Includes: TAM, SLA, Priority Support, Health Reviews
│
└── Professional Services (per project)
    └── Pricing: Fixed-price or T&M, depends on scope
```

**Huawei Role**: Reseller with margin, or referral partner with commission

### Option B: Managed Service Provider

```
Revenue Streams:
├── Managed Platform Fee (per cluster/month)
│   └── Includes: All Tier 1 + Tier 2 + ongoing operations
│
└── Professional Services (per project)
    └── Includes: Migrations, Extensions, Custom Work
```

**Huawei Role**: Primary customer relationship, OpenOva as subcontractor

### Option C: Hybrid - Recommended for Huawei

```
Revenue Split Model:
├── Platform Subscription → OpenOva (recurring)
├── Huawei Cloud Spend → Huawei (consumption)
├── Professional Services → Split (60% OpenOva / 40% Huawei referral)
```

**Joint GTM**: Huawei sells "OpenOva-powered Cloud Native Package"

---

## Part 7: What NOT to Do

### Anti-Patterns to Avoid

| Don't | Why | Instead |
|-------|-----|---------|
| Compete on manday rates | Race to bottom, no differentiation | Compete on outcome speed and quality |
| Unbundle platform into services | Destroys recurring revenue model | Platform is the foundation, PS is additive |
| Promise everything in catalog | Overcommit, underdeliver | Focus on core competencies, partner for rest |
| Position as "cheaper" | Commoditizes the offering | Position as "faster and safer" |
| Hide the platform | Loses differentiation | Platform is the hero, not the secret |

### Services to Decline or Partner

| Service | Recommendation |
|---------|----------------|
| Bigdata Migration (large) | Partner with Bigdata specialist |
| SOC 7x24 Services | Partner with MSSP |
| VM-only migrations (no containers) | Accept but deprioritize |
| Custom Huawei service integration | Case-by-case evaluation |

---

## Part 8: Sample Pitch Narrative

### For Huawei Internal Team

> "OpenOva isn't competing with your services catalog - we're accelerating it. Every line item in that catalog that involves Kubernetes, containers, or cloud-native infrastructure becomes faster and more reliable with our platform.
>
> Think of us like Red Hat. They don't just sell Linux - they sell confidence. We don't just deploy Kubernetes - we own the operational outcomes. When your customer has a 3am incident, they call us, not you.
>
> Here's the commercial model: Huawei sells cloud infrastructure, OpenOva sells the platform subscription. Professional services are joint-delivered. Customer gets faster time-to-value, Huawei gets differentiation, OpenOva gets recurring revenue."

### For End Customer

> "National Cloud gives you the infrastructure. OpenOva gives you the operations. Together, we deliver a complete cloud-native transformation - not just migration, but ongoing excellence.
>
> Our platform includes everything you need: GitOps delivery, observability, security, disaster recovery - all pre-integrated and battle-tested. Your team focuses on applications, we focus on the platform underneath.
>
> The difference? Traditional integrators deploy and leave. We deploy and stay. Our blueprints keep your platform current, our support keeps it running, our upgrades keep it safe."

---

## Part 9: Action Items

### Immediate (This Week)

1. [ ] Create one-page positioning document for Huawei meeting
2. [ ] Map all catalog items to OpenOva response (detailed spreadsheet)
3. [ ] Identify 2-3 pilot customer candidates

### Short-term (Next 2 Weeks)

4. [ ] Draft joint value proposition with Huawei team
5. [ ] Define pricing model for packages (Foundation/Professional/Enterprise)
6. [ ] Identify partner/subcontractor for Bigdata and SOC services

### Medium-term (Next Month)

7. [ ] Execute pilot with first customer
8. [ ] Refine commercial model based on pilot learnings
9. [ ] Develop joint marketing materials

---

## Appendix A: Full Catalog Mapping Table

| # | Category | Service | Mandays | OpenOva Fit | Effort Reduction | Commercial Model |
|---|----------|---------|---------|-------------|------------------|------------------|
| 1 | Connection | DC LLD | 7 | ⚡ | 50% | PS |
| 1 | Connection | DC Impl | 4 | ⚡ | 50% | PS |
| 2 | Landing Zone | IAAS LLD (start) | 25 | ✅ | 90% | Platform |
| 2 | Landing Zone | IAAS LLD (incr) | 2.5 | ✅ | 90% | Platform |
| 3 | Landing Zone | IAAS Impl (start) | 10 | ✅ | 90% | Platform |
| 3 | Landing Zone | IAAS Impl (incr) | 1 | ✅ | 90% | Platform |
| 4 | Container | CCE LLD | 10 | ✅ | 80% | Platform |
| 4 | Container | CCE Impl | 2 | ✅ | 80% | Platform |
| 5 | DB | DB LLD | 3 | ✅ | 70% | Platform |
| 5 | DB | DB Impl | 1 | ✅ | 70% | Platform |
| 1 | Migration | VM (start) | 12 | 🔧 | 0% | PS T&M |
| 1 | Migration | VM (incr) | 0.5 | 🔧 | 0% | PS T&M |
| 2 | Migration | Container (S) | 22 | ⚡ | 60% | PS Fixed |
| 2 | Migration | Container (M) | 40 | ⚡ | 60% | PS Fixed |
| 2 | Migration | Container (L) | 50 | ⚡ | 60% | PS Fixed |
| 3 | Migration | Storage (start) | 12 | 🔧 | 20% | PS T&M |
| 4 | Migration | DB Homo (start) | 12 | ⚡ | 40% | PS Fixed |
| 4 | Migration | DB Homo (incr) | 4/3 | ⚡ | 40% | PS Fixed |
| 1 | O&M | Consultation | 20 | ✅ | 80% | Platform |
| 2 | O&M | Plan & Design | TBD | ✅ | 80% | Platform |
| 2 | O&M | TAM Junior | 12/mo | ⚡ | 50% | Support Sub |
| 2 | O&M | TAM Senior | 12/mo | ⚡ | 50% | Support Sub |
| 1-4 | Consult | DB Consult | varies | ⚡ | 30% | PS |
| 5-6 | Consult | Bigdata | varies | 🔧 | 0% | Partner |
| 2 | Expert | Container | 30-80 | ✅ | 50% | PS Fixed |
| 4 | Expert | DB Hetero | 40+ | 🔧 | 20% | PS T&M |
| 5 | Expert | Bigdata | 100+ | ❌ | - | Partner |
| 1 | Security | Scan | TBD | ✅ | 90% | Platform |
| 2 | Security | SOC | annual | 🔧 | - | Partner |

---

## Appendix B: Competitive Positioning

### Against Traditional Integrators

| Dimension | Traditional Integrator | OpenOva |
|-----------|----------------------|---------|
| Delivery Model | Project-based, bespoke | Platform + PS |
| Knowledge Retention | In consultants' heads | In blueprints (customer asset) |
| Upgrade Path | New project each time | Continuous delivery |
| Support Model | "Call us for next project" | Subscription support |
| Scalability | Linear with headcount | Platform leverage |
| Differentiation | "We know Huawei Cloud" | "We own operational outcomes" |

### Against Platform Vendors

| Dimension | Platform-Only Vendor | OpenOva |
|-----------|---------------------|---------|
| Implementation | "Here's the software" | Platform + PS delivery |
| Migration Support | DIY or find partner | Included in offering |
| Localization | Generic | Huawei Cloud optimized |
| Go-to-Market | Direct | Joint with Huawei |

---

*Document prepared for internal strategy discussion. Update after Huawei alignment meeting.*
