# Company Capabilities Reference

**This file is an empty template.** Fill it in with your company's actual capabilities before running the rfp-shredder skill. The skill maps mandatory RFP requirements against this file, so the more accurate and specific it is, the better the Go/No-Go recommendation.

Update this file whenever your product, certifications, deployment options, or constraints change. Stale capabilities lead to wrong Go/No-Go calls.

---

## Company Overview

| Attribute | Detail |
|---|---|
| Company Name | _Your company name_ |
| Founded | _Year_ |
| Headquarters | _City, Country_ |
| Employees | _Approximate headcount_ |
| Industry Focus | _Sectors and verticals you sell into_ |
| Primary Buyers | _ICP: who buys from you_ |
| ARR / Revenue | _Optional, useful for ICP fit questions_ |
| Funding | _Stage if relevant_ |

---

## Product

_Brief description of your core product/platform._

### Core Modules / Capabilities

| Module | Description |
|---|---|
| _Module 1_ | _What it does_ |
| _Module 2_ | _What it does_ |

### Key Capabilities

- _Capability 1_
- _Capability 2_
- _Capability 3_

---

## Deployment Model

| Attribute | Detail |
|---|---|
| Deployment | _SaaS / On-prem / Hybrid / Private cloud_ |
| Cloud Provider | _AWS / Azure / GCP / Other_ |
| On-Premises | _Offered? Yes/No. If no, this is usually a deal-breaker for on-prem-mandatory RFPs._ |
| Data Residency | _Regions supported (US, UK, EU, APAC, etc.)_ |
| Environments | _Production, Staging, Sandbox, etc._ |

**CONSTRAINT EXAMPLE:** If you are SaaS-only and an RFP mandates on-premises hosting, flag as NON-COMPLIANT. Adjust this section to match your deployment reality.

---

## Integrations

### Pre-Built Connectors

| System Type | Supported Platforms |
|---|---|
| _Category 1_ | _Platforms_ |
| _Category 2_ | _Platforms_ |

### API & Custom Integration

- _API style (REST, GraphQL, webhooks)_
- _Rate limits_
- _Bulk data ingestion details_

---

## Security & Compliance Certifications

| Certification / Standard | Status |
|---|---|
| SOC 2 Type II | _Current / In progress / Not held_ |
| ISO 27001 | _Status_ |
| ISO 27701 (Privacy) | _Status_ |
| PCI DSS | _Status / Not applicable_ |
| HIPAA | _Status / Not applicable_ |
| GDPR | _Compliant? DPA available?_ |
| CCPA | _Status_ |
| FedRAMP | _Status / Not applicable_ |
| Industry-specific (e.g. APRA CPS 234, FCA, DORA) | _Status_ |

### Security Controls

- _Encryption at rest_
- _Encryption in transit_
- _Key management_
- _Penetration testing cadence_
- _Vulnerability management SLAs_
- _Incident response_
- _Business continuity (RPO/RTO)_
- _Access controls (MFA, SSO, RBAC)_

---

## Implementation & Onboarding

| Attribute | Detail |
|---|---|
| Typical timeline | _Weeks/months range_ |
| Methodology | _Phased approach_ |
| Professional services | _Team size and expertise_ |
| Customer success | _CSM model_ |
| Training | _Approach_ |
| Data migration | _Supported? With what tooling?_ |

---

## Support

| Tier | Coverage |
|---|---|
| Standard | _Hours, channels, SLAs_ |
| Premium | _Hours, channels, SLAs_ |
| Enterprise | _Hours, channels, SLAs_ |

---

## Customers & References

| Client | Type | Region | Use Case |
|---|---|---|---|
| _Reference 1_ | _Sector_ | _Region_ | _Use case_ |
| _Reference 2_ | _Sector_ | _Region_ | _Use case_ |

_Aggregate metrics: total clients, awards, analyst recognition._

---

## Constraints & Known Limitations

**This is the most important section for Go/No-Go decisions.** List everything you cannot do, will not do, or only do with significant effort. The skill uses this section to flag NON-COMPLIANT items, which often become deal-breakers.

| Constraint | Detail |
|---|---|
| _Constraint 1_ | _Why this is a hard limit_ |
| _Constraint 2_ | _Why this is a hard limit_ |

Examples of common constraints to consider documenting:
- Deployment model limits (SaaS-only, no on-prem)
- Certifications not held (e.g. FedRAMP, PCI DSS, HIPAA)
- Geographic limits (data residency, sales territory)
- Language support
- Scale ceilings (max users, max transactions)
- Industry verticals you do not serve
- Pricing floors (minimum ACV, minimum contract term)
- Customization limits (e.g. "we do not white-label")
