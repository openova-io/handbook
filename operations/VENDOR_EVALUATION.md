# Cloud Vendor Evaluation

**Purpose:** Evaluate cloud providers based on company reputation, size, financial stability, and suitability for Talent Mesh deployment with focus on Middle East (UAE/Oman) latency.

**Last Updated:** January 2026
**Status:** ✅ **DECISION FINALIZED - Contabo Selected**

---

## Decision Outcome

> **Final Decision:** Contabo VPS (India region) selected as primary infrastructure provider.

| Attribute | Selected Value |
|-----------|----------------|
| **Provider** | Contabo GmbH |
| **Region** | India (IN-MUM-1) for production, Germany (EU-DE-1) for development |
| **Instance Type** | VPS 10: 4 vCPU, 8GB RAM, 200GB SSD |
| **Node Count** | 3 nodes (all Control Plane + Worker) |
| **Total Resources** | 12 vCPU, 24GB RAM, 600GB SSD |
| **Monthly Cost** | €13.50 (~$15) |
| **Latency to UAE** | 40-60ms (acceptable for web applications) |

**Why Contabo:**
- Best $/GB RAM value ($0.54-0.62/GB)
- India data center provides lowest latency to ME among budget providers
- Official Terraform provider available
- 100% uptime track record (Q3-Q4 2025)
- Immediate provisioning (no capacity hunting)

**Fallback:** Hetzner Germany/Singapore if Contabo issues arise

See [ADR-014: Contabo VPS Infrastructure](../09-adrs/ADR-014-CONTABO-VPS-INFRASTRUCTURE.md) for full rationale.

---

## Evaluation Criteria

| Criteria | Weight | Description |
|----------|--------|-------------|
| **Cost Efficiency** | 30% | $/GB RAM, total monthly cost for 24GB cluster |
| **Middle East Latency** | 25% | Network latency to UAE/Oman |
| **Company Stability** | 20% | Revenue, years in business, market share |
| **Terraform Support** | 15% | Official provider maturity |
| **Reputation** | 10% | Uptime, support quality, community feedback |

---

## Vendor Profiles

### Tier 1: Budget Providers (Under $25/month for 24GB)

#### Hetzner Online GmbH (Germany)

| Attribute | Details |
|-----------|---------|
| **Founded** | 1997 (28 years) |
| **Headquarters** | Gunzenhausen, Germany |
| **Revenue** | €447M (2022) / ~$100-500M estimated |
| **Employees** | ~270-300 |
| **Market Share** | 2.86% in web hosting |
| **Customers** | 726,000+ companies |
| **Data Centers** | Nuremberg, Falkenstein (DE), Helsinki (FI), Ashburn, Hillsboro (US), Singapore |
| **Nearest to ME** | Germany (~80-100ms to UAE) or Singapore (~60-80ms) |
| **Terraform** | Official provider (mature) |

**Strengths:**
- 28 years in business - proven stability
- Owns data centers (not colocation)
- Best price/performance ratio
- Excellent uptime track record
- Nokia partnership (2025) for infrastructure

**Weaknesses:**
- No Middle East data center
- EU-focused, limited global presence
- Higher latency to UAE (~80-100ms from Germany)

**Sources:** [Hetzner](https://www.hetzner.com), [Tracxn](https://tracxn.com/d/companies/hetzner/), [Enlyft](https://enlyft.com/tech/products/hetzner)

---

#### Contabo GmbH (Germany)

| Attribute | Details |
|-----------|---------|
| **Founded** | 2003 (22 years, as Giga-International, renamed 2013) |
| **Headquarters** | Munich, Germany |
| **Revenue** | ~$35-36M (2025) |
| **Employees** | ~200-300 |
| **Market Share** | Smaller niche player |
| **Data Centers** | Germany, UK, USA (3), Singapore, Japan, Australia, **India** |
| **Nearest to ME** | **India (~40-60ms to UAE)** - Best budget option |
| **Terraform** | Official provider |

**Strengths:**
- Cheapest $/GB RAM ($0.54-0.62)
- India data center (lowest latency to ME among budget providers)
- 100% uptime Q3-Q4 2025 (HOSTtest verified)
- Lean operations = sustainable low prices
- Official Terraform provider

**Weaknesses:**
- Smaller company, lower revenue
- Mixed support reviews (slower response times)
- Prices increased in 2025
- Less mature than Hetzner

**Awards:** Cloud VPS 30 - #1 best-performing VPS (2025 rankings)

**Sources:** [Contabo](https://contabo.com), [PitchBook](https://pitchbook.com/profiles/company/433096-75), [CompWorth](https://compworth.com/company/contabo-gmbh)

---

#### Netcup GmbH (Germany)

| Attribute | Details |
|-----------|---------|
| **Founded** | 2003 (22 years) |
| **Headquarters** | Karlsruhe, Germany |
| **Revenue** | Not publicly disclosed |
| **Employees** | ~100-150 estimated |
| **Data Centers** | Nuremberg (DE), Vienna (AT), Amsterdam (NL), Manassas (US) |
| **Nearest to ME** | Germany (~80-100ms to UAE) |
| **Terraform** | **No official provider** |

**Strengths:**
- Excellent value (256GB SSD included)
- AMD EPYC 9634 (latest gen) + DDR5 ECC
- Unmetered traffic
- ARM servers available

**Weaknesses:**
- **No Terraform provider** (deal-breaker for IaC)
- ARM servers often sold out
- 99.6% SLA (vs 99.9% elsewhere)
- Throttling controversy (2025)

**Sources:** [Netcup](https://www.netcup.com), [VPSBenchmarks](https://www.vpsbenchmarks.com/hosters/netcup)

---

#### Hostinger (Lithuania/Global)

| Attribute | Details |
|-----------|---------|
| **Founded** | 2004 (21 years) |
| **Headquarters** | Kaunas, Lithuania |
| **Revenue** | ~$100M+ estimated |
| **Employees** | 1,000+ |
| **Data Centers** | North America, Europe, Asia, South America |
| **Nearest to ME** | Europe or Asia (~70-100ms to UAE) |
| **Terraform** | Official provider |

**Strengths:**
- Large company, well-funded
- Global presence
- 100GB NVMe included
- Official Terraform provider

**Weaknesses:**
- Only 2 vCPU for 8GB RAM tier
- 8TB traffic (vs 20-32TB elsewhere)
- Less specialized in cloud/VPS

**Sources:** [Hostinger](https://www.hostinger.com), [Terraform Registry](https://registry.terraform.io/providers/hostinger/hostinger/latest)

---

### Tier 2: Mid-Range Providers ($50-150/month)

#### Vultr (USA)

| Attribute | Details |
|-----------|---------|
| **Founded** | 2014 (11 years) |
| **Headquarters** | New Jersey, USA |
| **Revenue** | ~$100M+ estimated |
| **Employees** | ~100-200 |
| **Data Centers** | **32 locations in 19 countries** |
| **Nearest to ME** | Mumbai, India (~40-60ms to UAE) |
| **Terraform** | Official provider (mature) |

**Strengths:**
- Best global coverage (32 DCs)
- Mumbai DC for Middle East
- NVMe storage standard
- Mature Terraform provider

**Weaknesses:**
- More expensive than Hetzner/Contabo
- 4GB RAM max at $20/month tier

**Sources:** [Vultr](https://www.vultr.com), [Vultr Locations](https://www.vultr.com/features/datacenter-regions/)

---

#### DigitalOcean (USA)

| Attribute | Details |
|-----------|---------|
| **Founded** | 2011 (14 years) |
| **Headquarters** | New York, USA |
| **Revenue** | ~$700M (2024) |
| **Employees** | ~1,200 |
| **Market Share** | Significant in developer market |
| **Data Centers** | 14 locations globally |
| **Nearest to ME** | Bangalore, India (~50-70ms to UAE) |
| **Terraform** | Official provider (excellent) |

**Strengths:**
- Public company (financially transparent)
- Excellent documentation
- Developer-friendly
- Mature ecosystem

**Weaknesses:**
- More expensive ($5/GB RAM)
- No Middle East DC

**Sources:** [DigitalOcean](https://www.digitalocean.com), [DO Docs](https://docs.digitalocean.com)

---

#### Linode/Akamai (USA)

| Attribute | Details |
|-----------|---------|
| **Founded** | 2003 (22 years), acquired by Akamai 2022 |
| **Headquarters** | Philadelphia, USA (now part of Akamai) |
| **Parent Revenue** | ~$3.8B (Akamai) |
| **Data Centers** | 11 locations globally |
| **Nearest to ME** | Mumbai, India (~40-60ms to UAE) |
| **Terraform** | Official provider |

**Strengths:**
- Backed by Akamai (huge company)
- 99.99% uptime SLA
- Mumbai DC for Middle East
- Good bandwidth pricing

**Weaknesses:**
- Expensive for specs
- Akamai integration ongoing

**Sources:** [Linode](https://www.linode.com), [Akamai](https://www.akamai.com)

---

### Tier 3: Hyperscalers with Middle East Presence

#### AWS (USA)

| Attribute | Details |
|-----------|---------|
| **Middle East DC** | **Bahrain (me-south-1)** - ~10-20ms to UAE |
| **Cost** | ~$263/month for 24GB |
| **Terraform** | Official (excellent) |

#### Microsoft Azure (USA)

| Attribute | Details |
|-----------|---------|
| **Middle East DC** | **UAE North (Dubai), UAE Central (Abu Dhabi)** - ~5-15ms |
| **Cost** | ~$282/month for 24GB |
| **Terraform** | Official (excellent) |

#### Google Cloud (USA)

| Attribute | Details |
|-----------|---------|
| **Middle East DC** | **Doha, Qatar (me-central1)** - ~20-40ms to UAE |
| **Cost** | ~$284/month for 24GB |
| **Terraform** | Official (excellent) |

#### Oracle Cloud (USA)

| Attribute | Details |
|-----------|---------|
| **Middle East DC** | **UAE (Abu Dhabi)** - ~5-15ms |
| **Cost** | ~$96/month for 24GB (paid) / **$0 Always Free** |
| **Terraform** | Official |
| **Note** | Capacity issues in UAE region |

#### Alibaba Cloud (China)

| Attribute | Details |
|-----------|---------|
| **Middle East DC** | **Dubai** - ~5-15ms to UAE |
| **Cost** | ~$299/month for 24GB |
| **Terraform** | Official |
| **Free Credits** | $300-450 for 12 months (highest) |

---

## Latency Comparison to UAE/Oman

| Rank | Provider | Nearest DC | Est. Latency to UAE | Cost/mo |
|------|----------|------------|---------------------|---------|
| 1 | **Azure** | UAE (Dubai/Abu Dhabi) | **5-15ms** | ~$282 |
| 2 | **Oracle** | UAE (Abu Dhabi) | **5-15ms** | ~$96 / $0 |
| 3 | **Alibaba** | Dubai | **5-15ms** | ~$299 |
| 4 | **AWS** | Bahrain | **10-20ms** | ~$263 |
| 5 | **GCP** | Qatar (Doha) | **20-40ms** | ~$284 |
| 6 | **Contabo** | India | **40-60ms** | **~$15** |
| 7 | **Vultr** | Mumbai | **40-60ms** | ~$105 |
| 8 | **Linode** | Mumbai | **40-60ms** | ~$179 |
| 9 | **DigitalOcean** | Bangalore | **50-70ms** | ~$95 |
| 10 | **Hetzner** | Singapore | **60-80ms** | **~$21** |
| 11 | **Hetzner** | Germany | **80-100ms** | **~$21** |

---

## Vendor Stability Score

| Provider | Years | Revenue | Employees | Terraform | **Stability Score** |
|----------|-------|---------|-----------|-----------|---------------------|
| **AWS** | 19 | $90B+ | 1.5M+ | Excellent | **10/10** |
| **Azure** | 14 | $80B+ | 220K+ | Excellent | **10/10** |
| **GCP** | 16 | $40B+ | 180K+ | Excellent | **10/10** |
| **DigitalOcean** | 14 | $700M | 1,200 | Excellent | **9/10** |
| **Linode/Akamai** | 22 | $3.8B (parent) | 9,500 | Good | **9/10** |
| **Hetzner** | 28 | €447M | 300 | Good | **8/10** |
| **Vultr** | 11 | $100M+ | 200 | Good | **7/10** |
| **Contabo** | 22 | $36M | 300 | Good | **7/10** |
| **Oracle Cloud** | 8 | $14B+ (cloud) | 160K | Good | **9/10** |
| **Alibaba Cloud** | 15 | $13B+ | 250K+ | Good | **9/10** |
| **Netcup** | 22 | N/A | 150 | **None** | **5/10** |

---

## Final Recommendation Matrix

### For Talent Mesh (24GB RAM, Middle East Focus)

| Priority | Best Choice | Latency | Cost | Trade-off | Status |
|----------|-------------|---------|------|-----------|--------|
| **Lowest Cost** | Contabo 3x VPS 10 | 40-60ms | **$15/mo** | Smaller company | ✅ **SELECTED** |
| **Best Balance** | Hetzner 3x CAX21 | 60-80ms | **$21/mo** | Higher latency | 📋 Fallback |
| **Best Latency (Budget)** | Contabo India | **40-60ms** | **$15/mo** | Best budget + latency combo | ✅ **SELECTED** |
| **Best Latency (Premium)** | Oracle UAE | **5-15ms** | $96/mo | 5x cost of Contabo | ❌ Not selected |
| **Zero Cost** | Oracle Always Free | **5-15ms** | **$0** | Capacity hunting | ❌ **DEPRECATED** |

### Selected Strategy

**Primary: ✅ Contabo India (3x VPS 10)**
- €13.50/month (~$15)
- 40-60ms to UAE (acceptable for web apps)
- Official Terraform provider
- 100% uptime track record (Q3-Q4 2025)
- **Instance specs:** 4 vCPU, 8GB RAM, 200GB SSD per node
- **Total cluster:** 12 vCPU, 24GB RAM, 600GB SSD

**Fallback: 📋 Hetzner Germany/Singapore (3x CAX21)**
- ~$21/month
- 60-80ms to UAE
- More mature/stable company
- Better Terraform provider maturity
- Use if Contabo issues arise

**Deprecated: ❌ Oracle Cloud Always Free**
- Abandoned due to severe ARM capacity issues
- Weeks of "out of capacity" errors
- Abu Dhabi region lock-in with no capacity
- Not viable for reliable infrastructure

---

## Sources

### Company Information
- [Hetzner Tracxn Profile](https://tracxn.com/d/companies/hetzner/)
- [Contabo PitchBook Profile](https://pitchbook.com/profiles/company/433096-75)
- [Contabo About Us](https://contabo.com/en/about-us/)
- [DigitalOcean Investor Relations](https://investors.digitalocean.com/)

### Data Center Locations
- [Hetzner Locations](https://docs.hetzner.com/cloud/general/locations/)
- [Contabo Locations](https://contabo.com/en/locations/)
- [Vultr Datacenter Regions](https://www.vultr.com/features/datacenter-regions/)
- [OVHcloud Global Infrastructure](https://www.ovhcloud.com/en/about-us/global-infrastructure/)

### Middle East Infrastructure
- [UAE Data Centers - Piwik PRO](https://piwik.pro/blog/uae-data-centers/)
- [Data Center Map - UAE](https://www.datacentermap.com/united-arab-emirates/)
- [PWC - Middle East Data Centers](https://www.pwc.com/m1/en/media-centre/articles/unlocking-the-data-centre-opportunity-in-the-middle-east.html)

### Benchmarks & Reviews
- [VPSBenchmarks](https://www.vpsbenchmarks.com/)
- [HOSTtest Uptime Reports](https://www.hosttest.co.uk/)

### Related Documentation
- [ADR-014: Contabo VPS Infrastructure](../09-adrs/ADR-014-CONTABO-VPS-INFRASTRUCTURE.md)
- [Infrastructure Setup Guide](./INFRASTRUCTURE_SETUP.md)
- [Infrastructure Agreements](./INFRASTRUCTURE_AGREEMENTS.md)
- [Cloud Provider Cost Comparison](./CLOUD_PROVIDER_COST_COMPARISON.md)

---

*Note: Latency estimates are approximate and may vary based on routing, time of day, and network conditions. Always test actual latency before committing to a provider.*

---

*Document Version: 2.0*
*Last Updated: 2026-01-06*
*Status: Decision Finalized*
