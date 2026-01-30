# Stakeholder Drivers & Goals Analysis: UK Fuel Price Transparency Service

> **Template Status**: Live | **Version**: 1.0.3 | **Command**: `/arckit.stakeholders`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-STKE-v1.0 |
| **Document Type** | Stakeholder Drivers & Goals Analysis |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-01-30 |
| **Last Modified** | 2026-01-30 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-04-30 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Programme Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-30 | ArcKit AI | Initial creation from `/arckit.stakeholders` command | PENDING | PENDING |

---

## Executive Summary

### Purpose
This document identifies the key stakeholders of the UK Government Fuel Price Transparency Service ("Fuel Finder"), their underlying drivers, how those drivers manifest into measurable goals, and the outcomes that will demonstrate success. The service operates under the Motor Fuel Price (Open Data) Regulations 2025, requiring ~8,500 UK fuel stations to submit real-time pricing data for open publication.

### Key Findings
The stakeholder landscape is dominated by three forces: **regulatory enforcement** (CMA must demonstrate the open data scheme works), **citizen value** (motorists must find the service useful enough to change behaviour), and **retailer compliance** (fuel stations must submit data accurately and on time). The primary tension is between CMA's enforcement urgency and retailers' capacity to comply, particularly smaller independent operators. A secondary tension exists between rapid delivery (political pressure for visible results) and thorough governance (GDS Service Standard, Secure by Design).

### Critical Success Factors
- **Retailer onboarding**: All ~8,500 forecourts registered by 2 February 2026 and submitting accurate data before the enforcement grace period ends (early May 2026)
- **Data quality**: Published prices are accurate, timely, and comprehensive enough for citizens to make meaningful comparisons
- **Citizen adoption**: Motorists use the service and perceive it as trustworthy and useful
- **Regulatory credibility**: CMA can demonstrate the scheme is working and enforce non-compliance
- **GDS assessment pass**: Service meets all 14 points of the GDS Service Standard

### Stakeholder Alignment Score
**Overall Alignment**: **MEDIUM**

Most stakeholders share the goal of market transparency, but significant tensions exist around pace of delivery vs governance rigour, enforcement strictness vs retailer support, and data granularity vs retailer commercial sensitivity. These are manageable through phased delivery and clear communication.

---

## Stakeholder Identification

### Internal Stakeholders (Government)

| Stakeholder | Role/Department | Influence | Interest | Engagement Strategy |
|-------------|----------------|-----------|----------|---------------------|
| CMA Board / Chair | Competition and Markets Authority — statutory regulator | HIGH | HIGH | Steering committee, quarterly board updates |
| CMA Fuel Finder Programme SRO | Senior Responsible Owner for the programme | HIGH | HIGH | Weekly programme board, decision authority |
| CMA Digital & Data Team | Technology delivery arm within CMA | MEDIUM | HIGH | Daily standups, sprint reviews, architecture decisions |
| CMA Enforcement Division | Enforcement case officers | HIGH | HIGH | Requirements input, enforcement tool co-design |
| DESNZ Policy Team | Department for Energy Security & Net Zero — policy owner | HIGH | HIGH | Monthly policy alignment, regulatory change pipeline |
| DESNZ Ministers | Ministerial accountability for fuel policy | HIGH | MEDIUM | Briefings, parliamentary question support |
| GDS Assessors | Government Digital Service — service assessment | HIGH | MEDIUM | Phase gate assessments (Alpha, Beta, Live) |
| CDDO | Central Digital & Data Office — spend controls | HIGH | LOW | Spend control approvals, TCoP compliance |
| HM Treasury | Spending authority | HIGH | LOW | Business case approval, spending review alignment |
| Programme Delivery Team | Developers, designers, researchers, delivery managers | LOW | HIGH | Agile ceremonies, retrospectives |
| SIRO / Information Governance | Senior Information Risk Owner | HIGH | MEDIUM | Security and data governance sign-off |

### External Stakeholders

| Stakeholder | Organisation | Relationship | Influence | Interest |
|-------------|--------------|--------------|-----------|----------|
| Citizens / Motorists | UK public (~33M driving licence holders) | Primary beneficiary | LOW | HIGH |
| Motor Fuel Traders (large) | Supermarkets, major oil companies (BP, Shell, Esso) | Regulated data submitter | MEDIUM | HIGH |
| Motor Fuel Traders (independent) | ~4,000 independent forecourts | Regulated data submitter | LOW | HIGH |
| Fuel Retail Trade Bodies | Petrol Retailers Association (PRA), UK Petroleum Industry Association (UKPIA) | Industry representation | MEDIUM | HIGH |
| Third-Party Data Consumers | Price comparison apps, navigation providers, researchers | API consumers | LOW | HIGH |
| ICO | Information Commissioner's Office | Data protection regulator | HIGH | MEDIUM |
| NAO | National Audit Office | Value for money auditor | HIGH | LOW |
| PAC | Public Accounts Committee | Parliamentary oversight | HIGH | LOW |
| Media | National press, motoring journalists | Public narrative | MEDIUM | MEDIUM |

### Stakeholder Power-Interest Grid

```
                          INTEREST
              Low                         High
        ┌─────────────────────┬─────────────────────┐
        │                     │                     │
        │   KEEP SATISFIED    │   MANAGE CLOSELY    │
   High │                     │                     │
        │  • HM Treasury      │  • CMA Board/Chair  │
        │  • CDDO             │  • CMA SRO          │
        │  • NAO              │  • CMA Enforcement  │
        │  • PAC              │  • DESNZ Policy     │
        │  • SIRO             │  • DESNZ Ministers   │
 P      │  • GDS Assessors    │  • Trade Bodies     │
 O      │  • ICO              │                     │
 W      ├─────────────────────┼─────────────────────┤
 E      │                     │                     │
 R      │      MONITOR        │    KEEP INFORMED    │
        │                     │                     │
   Low  │                     │  • Citizens         │
        │                     │  • Large Retailers  │
        │                     │  • Independents     │
        │                     │  • Delivery Team    │
        │                     │  • 3rd Party APIs   │
        │                     │  • Media            │
        └─────────────────────┴─────────────────────┘
```

| Stakeholder | Power | Interest | Quadrant | Engagement Strategy |
|-------------|-------|----------|----------|---------------------|
| CMA Board / Chair | HIGH | HIGH | Manage Closely | Quarterly board update, monthly SRO report |
| CMA SRO | HIGH | HIGH | Manage Closely | Weekly programme board |
| CMA Enforcement | HIGH | HIGH | Manage Closely | Co-design enforcement tools, fortnightly sync |
| DESNZ Policy | HIGH | HIGH | Manage Closely | Monthly policy alignment meetings |
| DESNZ Ministers | HIGH | MEDIUM | Keep Satisfied | Briefing packs, parliamentary question support |
| GDS Assessors | HIGH | MEDIUM | Keep Satisfied | Phase gate assessments with pre-assessment check-ins |
| CDDO | HIGH | LOW | Keep Satisfied | Spend control submissions, TCoP evidence |
| HM Treasury | HIGH | LOW | Keep Satisfied | Business case updates at spending review |
| SIRO | HIGH | MEDIUM | Keep Satisfied | Security governance boards, DPIA review |
| ICO | HIGH | MEDIUM | Keep Satisfied | DPIA consultation, privacy notice review |
| NAO | HIGH | LOW | Keep Satisfied | Audit-ready documentation, VfM evidence |
| PAC | HIGH | LOW | Keep Satisfied | Briefing material if called to give evidence |
| Trade Bodies (PRA, UKPIA) | MEDIUM | HIGH | Manage Closely | Regular liaison, consultation on changes |
| Citizens / Motorists | LOW | HIGH | Keep Informed | GOV.UK service pages, media, user research panels |
| Large Retailers | MEDIUM | HIGH | Keep Informed | Onboarding support, technical documentation |
| Independent Retailers | LOW | HIGH | Keep Informed | Onboarding support, assisted digital, trade body cascade |
| Delivery Team | LOW | HIGH | Keep Informed | Agile ceremonies, architecture reviews |
| Third-Party Consumers | LOW | HIGH | Keep Informed | API documentation, developer portal |
| Media | MEDIUM | MEDIUM | Keep Informed | Press releases, transparency reports |

---

## Stakeholder Drivers Analysis

### SD-1: CMA Board — Demonstrate Regulatory Effectiveness

**Stakeholder**: CMA Board and Chair

**Driver Category**: COMPLIANCE / STRATEGIC

**Driver Statement**: Demonstrate that the Motor Fuel Price (Open Data) Regulations 2025 are effective in improving fuel market transparency and competition, justifying the CMA's recommendation and the legislative effort invested.

**Context & Background**:
The CMA's 2023 road fuels market study recommended an open data scheme. The government legislated through the Motor Fuel Price (Open Data) Regulations 2025. The CMA now has enforcement powers and must demonstrate the scheme delivers its intended outcomes — fairer prices for consumers through transparency. Failure would undermine CMA credibility and future regulatory recommendations.

**Driver Intensity**: CRITICAL

**Enablers**:
- High retailer compliance rates (>95% of forecourts reporting)
- Measurable reduction in price dispersion or faster price drops at forecourts
- Positive media coverage and citizen adoption
- Robust enforcement tools to act against non-compliance

**Blockers**:
- Low retailer compliance, especially among independents
- Poor data quality undermining trust
- Technical failures causing service outages during high-profile periods
- Legal challenges to enforcement actions

**Related Stakeholders**: DESNZ Policy (co-owner of regulatory framework), Trade Bodies (compliance channel), Citizens (ultimate beneficiaries)

---

### SD-2: CMA Enforcement Division — Effective Enforcement Capability

**Stakeholder**: CMA Enforcement Division

**Driver Category**: OPERATIONAL / COMPLIANCE

**Driver Statement**: Have reliable tools and evidence to identify non-compliant retailers, assess the severity of non-compliance, and take proportionate enforcement action — from warnings through to penalties.

**Context & Background**:
The CMA published enforcement guidance in December 2025. An enforcement grace period runs until early May 2026, during which the focus is on support rather than penalties. After May 2026, the CMA needs operational capability to detect, investigate, and act on non-compliance. This requires robust audit trails, submission tracking, and compliance dashboards.

**Driver Intensity**: CRITICAL

**Enablers**:
- Immutable audit trail of all submissions (or missed submissions)
- Compliance dashboards showing submission rates, timeliness, coverage gaps
- Automated alerts for non-reporting forecourts
- Evidence export capability for formal enforcement cases
- Clear separation between operational and enforcement data access

**Blockers**:
- Incomplete audit trail undermining evidence admissibility
- Inability to distinguish "system failure" from "retailer non-compliance"
- Data retention gaps losing historical evidence
- Enforcement tools delivered late (after grace period ends)

**Related Stakeholders**: CMA Board (accountable for enforcement outcomes), Trade Bodies (first-line compliance channel), Independent Retailers (highest non-compliance risk)

---

### SD-3: DESNZ Policy Team — Deliver Ministerial Commitment

**Stakeholder**: DESNZ Policy Team

**Driver Category**: STRATEGIC / COMPLIANCE

**Driver Statement**: Deliver the fuel price transparency scheme as a working government service that fulfils the policy intent of the Motor Fuel Price (Open Data) Regulations 2025, on schedule and within governance frameworks.

**Context & Background**:
DESNZ owns the policy and the regulations. The 2 February 2026 registration deadline is set in legislation. Ministers are accountable to Parliament for the scheme's success. DESNZ needs the service to work so they can demonstrate policy delivery and respond to parliamentary questions with evidence.

**Driver Intensity**: CRITICAL

**Enablers**:
- On-time delivery aligned with regulatory milestones
- Clear reporting to ministers on scheme progress (registrations, submissions, coverage)
- Positive citizen feedback and media coverage
- Cross-government collaboration (CMA + DESNZ + GDS) working smoothly

**Blockers**:
- Delivery delays missing regulatory milestones
- Negative media coverage of scheme failures
- Parliamentary questions the minister cannot answer due to lack of data
- Inter-departmental friction between CMA and DESNZ

**Related Stakeholders**: DESNZ Ministers (accountable to Parliament), CMA Board (joint ownership), GDS Assessors (governance gate)

---

### SD-4: DESNZ Ministers — Political Accountability and Consumer Impact

**Stakeholder**: DESNZ Ministers

**Driver Category**: STRATEGIC / RISK

**Driver Statement**: Demonstrate visible progress on reducing fuel costs for constituents, avoid negative parliamentary or media scrutiny, and have clear answers to parliamentary questions about the scheme's effectiveness.

**Context & Background**:
Fuel prices are a high-visibility consumer issue. Ministers face parliamentary questions, media scrutiny, and constituent correspondence about fuel costs. The Fuel Finder is a tangible deliverable they can point to. They need it to work visibly and deliver measurable consumer benefit.

**Driver Intensity**: HIGH

**Enablers**:
- Headline metrics showing consumer benefit (e.g., "average savings of £X per year")
- High public awareness and adoption
- Positive media narrative
- Clear dashboard for ministerial briefings

**Blockers**:
- Service failures attracting negative headlines
- Lack of measurable consumer impact
- Slow rollout undermining credibility
- Retailer pushback attracting media sympathy

**Related Stakeholders**: DESNZ Policy (briefing support), CMA Board (enforcement credibility), Media (narrative shaping), Citizens (ultimate judges)

---

### SD-5: Citizens / Motorists — Find Cheapest Fuel Nearby

**Stakeholder**: UK Citizens and Motorists (~33 million driving licence holders)

**Driver Category**: CUSTOMER / FINANCIAL

**Driver Statement**: Easily find the cheapest fuel near their location or route, trust that the prices shown are accurate and current, and save money on fuel purchases.

**Context & Background**:
Motorists currently rely on ad-hoc information — word of mouth, brand loyalty, or existing comparison apps with incomplete data. The Fuel Finder promises comprehensive, accurate, regulated data from all forecourts. Citizens need the service to be simple, fast, mobile-friendly, and trustworthy.

**Driver Intensity**: HIGH

**Enablers**:
- Simple, fast, mobile-first interface
- Accurate, up-to-date prices (within hours of change)
- Geographic search (near me, along route)
- Trust signals (government branding, "updated X minutes ago")
- Comprehensive coverage (all forecourts, not just chains)

**Blockers**:
- Stale or inaccurate prices undermining trust
- Complex or slow interface
- Poor mobile experience
- Missing forecourts (especially local independents)
- No awareness the service exists

**Related Stakeholders**: Media (awareness channel), Trade Bodies (data accuracy), Third-Party Consumers (alternative access channels)

---

### SD-6: Large Motor Fuel Traders — Minimise Compliance Burden

**Stakeholder**: Supermarkets (Tesco, Sainsbury's, Asda, Morrisons), Major Oil Companies (BP, Shell, Esso)

**Driver Category**: OPERATIONAL / COMPLIANCE

**Driver Statement**: Comply with the Motor Fuel Price (Open Data) Regulations 2025 with minimal disruption to existing operations, using automated integration with existing pricing and POS systems.

**Context & Background**:
Large retailers operate hundreds of sites with centralised pricing systems. They have IT departments capable of API integration. Their primary concern is the operational burden — they want to connect once via API and automate ongoing submissions. They also have commercial sensitivity concerns about competitors seeing their pricing strategy in real time.

**Driver Intensity**: MEDIUM

**Enablers**:
- Well-documented API with clear specifications
- Test environment for integration development
- Bulk submission capability (all sites in one call)
- Clear data schema with no ambiguity
- Reasonable update frequency requirements

**Blockers**:
- Poorly documented or unstable API
- Unreasonable update frequency requirements
- Ambiguous data schema causing rejection
- No test environment for integration
- Excessive manual processes

**Related Stakeholders**: Trade Bodies (UKPIA representing majors), CMA Enforcement (compliance monitoring), Independent Retailers (different compliance challenges)

---

### SD-7: Independent Motor Fuel Traders — Avoid Disproportionate Burden

**Stakeholder**: ~4,000 independent forecourts (single-site operators, small chains)

**Driver Category**: COMPLIANCE / RISK / PERSONAL

**Driver Statement**: Comply with the regulations without disproportionate cost or complexity, given limited IT capability and staff. Avoid enforcement penalties during the transition period.

**Context & Background**:
Independent operators often lack IT departments, may not have automated pricing systems, and may have limited digital skills. The regulations apply equally to a single-site family business and a supermarket chain with 500 sites. These operators fear enforcement penalties and resent what they perceive as administrative burden on small businesses. Many rely on trade body guidance.

**Driver Intensity**: HIGH

**Enablers**:
- Simple web-based manual submission interface
- Clear, plain-English guidance (not technical jargon)
- Extended support during onboarding
- Assisted digital channel (phone/email support)
- Reasonable update frequency (not requiring constant attention)
- Grace period used genuinely for support, not early enforcement

**Blockers**:
- Complex registration or submission process
- Technical jargon in guidance documents
- Lack of phone/email support
- Perceived unfairness (same rules as large chains)
- Penalties during grace period

**Related Stakeholders**: PRA (trade body representing independents), CMA Enforcement (proportionate enforcement), GDS (accessibility and assisted digital)

---

### SD-8: Trade Bodies (PRA, UKPIA) — Protect Member Interests

**Stakeholder**: Petrol Retailers Association (PRA), UK Petroleum Industry Association (UKPIA)

**Driver Category**: STRATEGIC / OPERATIONAL

**Driver Statement**: Ensure the regulatory scheme is workable for their members, the compliance burden is proportionate, and their members' commercial interests are not unfairly disadvantaged by data transparency.

**Context & Background**:
Trade bodies were consulted during the regulatory development process. They represent their members' collective interests and act as an intermediary between government and industry. They need to demonstrate value to members by securing reasonable terms and providing compliance support.

**Driver Intensity**: HIGH

**Enablers**:
- Early consultation on technical specifications and data schemas
- Clear regulatory guidance they can cascade to members
- Proportionate enforcement approach (warnings before penalties)
- Industry-friendly submission processes
- Regular liaison meetings with CMA/DESNZ

**Blockers**:
- Changes imposed without consultation
- Disproportionate enforcement against smaller members
- Unreasonable data requirements beyond statutory minimum
- Lack of communication channels to CMA

**Related Stakeholders**: All retailers (represented parties), CMA Enforcement (enforcement approach), DESNZ Policy (regulatory framework)

---

### SD-9: GDS Assessors — Service Meets the Standard

**Stakeholder**: GDS Service Assessment Team

**Driver Category**: COMPLIANCE / OPERATIONAL

**Driver Statement**: The Fuel Finder service meets all 14 points of the GDS Service Standard, demonstrating user-centred design, accessibility, technical quality, and operational readiness at each phase gate.

**Context & Background**:
All government digital services must pass GDS Service Standard assessment at Alpha, Beta, and Live phases. Failure to pass means the service cannot proceed to the next phase. GDS assessors evaluate against 14 points covering user needs, accessibility, technology choices, operations, and continuous improvement.

**Driver Intensity**: HIGH

**Enablers**:
- User research evidence at each phase
- Accessibility audit results (WCAG 2.2 AA)
- Multidisciplinary team with user researchers, designers, developers
- Technology choices aligned with TCoP
- Open source code and open standards
- Performance data and analytics

**Blockers**:
- Insufficient user research evidence
- Accessibility failures
- Technology decisions that don't follow TCoP
- Lack of multidisciplinary team
- No performance metrics or analytics

**Related Stakeholders**: Delivery Team (produces the evidence), CDDO (spend controls linked to assessment), CMA SRO (accountable for passing)

---

### SD-10: ICO — Data Protection Compliance

**Stakeholder**: Information Commissioner's Office

**Driver Category**: COMPLIANCE

**Driver Statement**: Ensure the Fuel Finder service processes personal data lawfully, fairly, and transparently under UK GDPR, with a completed DPIA and appropriate privacy safeguards.

**Context & Background**:
The service processes limited personal data (retailer contact details, operator names). While not a high-risk processing operation, government services are under heightened scrutiny. The ICO expects to see a DPIA, clear lawful basis, privacy notices, and data subject rights processes.

**Driver Intensity**: MEDIUM

**Enablers**:
- DPIA completed and shared with ICO
- Clear lawful basis documented (public task)
- Privacy notices published before data collection
- Data minimisation demonstrably applied
- Data subject rights procedures operational

**Blockers**:
- DPIA not completed before go-live
- Unclear lawful basis
- Scope creep collecting additional personal data
- Data retained beyond stated purposes

**Related Stakeholders**: SIRO (internal governance), DESNZ DPO (data protection officer), Retailers (data subjects for contact details)

---

### SD-11: Third-Party Data Consumers — Reliable API Access

**Stakeholder**: Price comparison apps, navigation providers, academic researchers, journalists

**Driver Category**: OPERATIONAL / STRATEGIC

**Driver Statement**: Access comprehensive, accurate, real-time UK fuel pricing data through a reliable, well-documented API to build products and conduct analysis.

**Context & Background**:
Third-party consumers amplify the service's reach — a motorist may find fuel prices through their favourite navigation app rather than the government website. These consumers need stable APIs, clear documentation, reasonable rate limits, and advance notice of changes.

**Driver Intensity**: MEDIUM

**Enablers**:
- Well-documented public API with OpenAPI specification
- Developer portal with sandbox environment
- Reasonable rate limits with clear documentation
- Advance notice of API changes (deprecation policy)
- Bulk download option for researchers

**Blockers**:
- Undocumented or frequently changing API
- Unreasonable rate limits
- No sandbox or test environment
- Breaking changes without notice
- Data licensing uncertainty

**Related Stakeholders**: Citizens (reached through third-party apps), CMA Board (wider ecosystem amplifies impact), GDS (open data principles)

---

### SD-12: NAO / PAC — Value for Money and Governance

**Stakeholder**: National Audit Office, Public Accounts Committee

**Driver Category**: FINANCIAL / RISK

**Driver Statement**: Ensure public money is spent wisely, the programme demonstrates value for money, governance is sound, and lessons are learned from delivery.

**Context & Background**:
NAO audits government spending and reports to PAC. High-profile digital programmes that overspend or underdeliver attract scrutiny. The Fuel Finder must demonstrate proportionate spending, clear benefits realisation, and sound governance. NAO typically examines programmes 1-2 years after launch.

**Driver Intensity**: MEDIUM

**Enablers**:
- Clear business case with quantified benefits
- Robust cost tracking and benefits realisation
- Agile delivery with regular value demonstration
- Sound governance with clear decision trails
- Transparent reporting of costs and outcomes

**Blockers**:
- Cost overruns without clear justification
- Benefits not measured or not materialising
- Poor governance documentation
- Lack of lessons learned process
- Avoidable failures that waste public money

**Related Stakeholders**: HM Treasury (business case), CMA SRO (governance), CDDO (spend controls)

---

## Driver-to-Goal Mapping

### Goal G-1: Achieve Universal Retailer Registration

**Derived From Drivers**: SD-1, SD-3, SD-6, SD-7, SD-8

**Goal Owner**: CMA SRO

**Goal Statement**: All ~8,500 UK fuel forecourts registered on the Fuel Finder service by the statutory deadline of 2 February 2026.

**Why This Matters**: Registration is the prerequisite for data submission. Without universal registration, the open data scheme is incomplete and CMA cannot demonstrate regulatory effectiveness. DESNZ cannot report to ministers that the scheme is on track.

**Success Metrics**:
- **Primary Metric**: Percentage of known forecourts registered
- **Secondary Metrics**:
  - Registration rate per week (velocity)
  - Registrations by retailer type (chain vs independent)
  - Support requests received and resolved

**Baseline**: 0 forecourts registered (pre-launch)

**Target**: ≥97% of known forecourts registered by 2 February 2026 (allowing for closures, disputed sites)

**Measurement Method**: Count of registered forecourts vs BEIS/DESNZ forecourt register, updated daily

**Dependencies**:
- Accurate master list of UK forecourts
- Registration service operational and performant
- Retailer communications sent via trade bodies and direct mail
- Assisted digital support available for independents

**Risks to Achievement**:
- Independent retailers unaware of obligation
- Registration process too complex for small operators
- Master forecourt list inaccurate or incomplete

---

### Goal G-2: Achieve High-Quality Data Submission Compliance

**Derived From Drivers**: SD-1, SD-2, SD-5, SD-6, SD-7, SD-9

**Goal Owner**: CMA Enforcement Division (monitoring), CMA SRO (accountable)

**Goal Statement**: ≥90% of registered forecourts submitting accurate fuel price data within the required timeframe, rising to ≥95% within 6 months of the enforcement grace period ending.

**Why This Matters**: The scheme's value depends on comprehensive, accurate data. Incomplete data undermines citizen trust and CMA's ability to analyse the market. This goal satisfies the CMA's effectiveness driver, citizens' need for accurate data, and GDS's service quality expectations.

**Success Metrics**:
- **Primary Metric**: Percentage of registered forecourts with a current (within-SLA) price submission
- **Secondary Metrics**:
  - Data freshness (median time from price change to publication)
  - Submission rejection rate (data quality failures)
  - Coverage by fuel type (petrol, diesel)
  - Geographic coverage (no significant regional gaps)

**Baseline**: 0% (pre-launch)

**Target**: ≥90% by end of grace period (May 2026); ≥95% by November 2026

**Measurement Method**: Automated compliance dashboard comparing registered forecourts vs forecourts with current submissions, measured daily

**Dependencies**:
- Registration target (G-1) substantially met
- Submission API reliable and performant
- Manual submission interface available for non-API retailers
- Clear guidance on submission frequency and data requirements

**Risks to Achievement**:
- Independent retailers submit sporadically
- API integration issues for large chains delay automated submission
- Ambiguous data requirements cause high rejection rates
- Retailers submit but with stale or inaccurate prices

---

### Goal G-3: Deliver a Trusted Citizen-Facing Service

**Derived From Drivers**: SD-4, SD-5, SD-9, SD-11

**Goal Owner**: CMA Digital & Data Team Lead

**Goal Statement**: Launch a citizen-facing fuel price comparison service on GOV.UK that passes GDS Service Standard assessment and achieves a user satisfaction score of ≥80% by Public Beta.

**Why This Matters**: Citizens are the ultimate beneficiaries. Ministers need to point to a visible, trusted service. GDS assessment is a mandatory governance gate. Third-party consumers need a reliable API to amplify reach.

**Success Metrics**:
- **Primary Metric**: GDS Service Standard assessment result (pass/not pass)
- **Secondary Metrics**:
  - User satisfaction score (GOV.UK satisfaction survey)
  - Task completion rate (user can find fuel price near them)
  - Accessibility audit result (WCAG 2.2 AA compliance)
  - Page load time (p95 < 3 seconds on mobile)
  - Monthly unique users

**Baseline**: No service exists

**Target**: Pass Beta assessment; ≥80% user satisfaction; ≥95% task completion; WCAG 2.2 AA compliant

**Measurement Method**: GDS assessment panel; GOV.UK analytics; accessibility audit; user research sessions

**Dependencies**:
- Data submission compliance (G-2) providing sufficient data to be useful
- User research conducted with motorists
- GOV.UK Design System used for interface
- Performance tested on low-bandwidth mobile connections

**Risks to Achievement**:
- Insufficient data makes the service unhelpful
- GDS assessment identifies significant issues
- Accessibility audit reveals fundamental problems
- Low awareness means low uptake

---

### Goal G-4: Establish Effective Enforcement Capability

**Derived From Drivers**: SD-1, SD-2, SD-3

**Goal Owner**: CMA Enforcement Division Lead

**Goal Statement**: Operational enforcement tools and processes ready before the grace period ends (early May 2026), with capability to detect, investigate, and act on non-compliance.

**Why This Matters**: Without enforcement capability, the regulatory scheme lacks teeth. CMA's credibility depends on being able to act. The grace period provides a window to build tools while focusing on retailer support.

**Success Metrics**:
- **Primary Metric**: Enforcement tools operational by May 2026
- **Secondary Metrics**:
  - Compliance dashboard accuracy (correctly identifies non-reporting forecourts)
  - Time to detect non-compliance (target: <24 hours)
  - Evidence export capability tested and validated
  - Enforcement case workflow operational

**Baseline**: No enforcement tools exist

**Target**: Full enforcement capability operational by May 2026

**Measurement Method**: Enforcement readiness review; tabletop exercise with mock non-compliance scenarios; legal review of evidence chain

**Dependencies**:
- Audit trail architecture in place (ARC-000-PRIN Principle 20)
- Tamper-evident storage for submission records
- Compliance dashboards built and tested
- Legal review of evidence admissibility requirements

**Risks to Achievement**:
- Architecture decisions delay audit trail implementation
- Legal requirements for evidence not understood until late
- Enforcement tools deprioritised in favour of citizen features
- Grace period shortened or extended, changing timeline

---

### Goal G-5: Demonstrate Value for Money

**Derived From Drivers**: SD-4, SD-12

**Goal Owner**: CMA SRO

**Goal Statement**: Deliver the Fuel Finder programme within approved budget (per Green Book business case) and demonstrate measurable consumer benefit within 12 months of launch.

**Why This Matters**: Public money accountability is non-negotiable. NAO and PAC will examine whether the programme delivered its promised benefits. Ministers need to justify the investment to Parliament.

**Success Metrics**:
- **Primary Metric**: Programme spend vs approved budget
- **Secondary Metrics**:
  - Estimated consumer savings (based on price transparency effect)
  - Cost per forecourt per year (operational cost / number of forecourts)
  - Benefits realisation vs business case projections

**Baseline**: Approved business case budget and projected benefits

**Target**: Deliver within ±10% of approved budget; measurable consumer benefit evidence within 12 months

**Measurement Method**: Monthly financial reporting; economic analysis of price data trends; benefits realisation tracker

**Dependencies**:
- Approved business case with clear benefits model
- Regular cost tracking and reporting
- Economic analysis capability to measure price transparency effects

**Risks to Achievement**:
- Scope creep increasing costs
- Benefits difficult to isolate from other market factors
- Technology cost overruns
- Delays increasing programme overhead costs

---

### Goal G-6: Ensure Data Protection Compliance

**Derived From Drivers**: SD-10, SD-3

**Goal Owner**: SIRO / DPO

**Goal Statement**: Complete DPIA before personal data processing begins, achieve full UK GDPR compliance, and maintain ongoing ICO readiness.

**Why This Matters**: Legal obligation under UK GDPR Article 35. Government services face heightened scrutiny from ICO. Non-compliance could result in enforcement action and reputational damage.

**Success Metrics**:
- **Primary Metric**: DPIA completed and signed off before go-live
- **Secondary Metrics**:
  - Privacy notices published
  - Data subject rights processes operational
  - ICO consultation completed (if required)
  - No data breaches or ICO complaints

**Baseline**: No DPIA exists

**Target**: DPIA complete before Private Beta; zero ICO enforcement actions

**Measurement Method**: DPIA document review; ICO correspondence tracking; data breach log

**Dependencies**:
- Data model defined (what personal data is processed)
- Lawful basis agreed with legal team
- Privacy notices drafted and reviewed
- Data subject rights processes designed

**Risks to Achievement**:
- DPIA identifies risks requiring significant architectural change
- ICO consultation required, adding time
- Scope creep introduces additional personal data processing

---

### Goal G-7: Pass GDS Service Standard Assessment at Each Phase

**Derived From Drivers**: SD-9, SD-3, SD-4

**Goal Owner**: CMA Digital & Data Team Lead

**Goal Statement**: Pass GDS Service Standard assessment at Alpha, Private Beta, Public Beta, and Live phases without conditions that block progression.

**Why This Matters**: GDS assessment is mandatory for government digital services. Failure to pass blocks progression to the next phase and causes delivery delays. Passing demonstrates that the service is well-designed, accessible, and operationally ready.

**Success Metrics**:
- **Primary Metric**: Assessment outcome at each phase (pass / pass with conditions / not pass)
- **Secondary Metrics**:
  - Number of assessment points met vs not met
  - Conditions from previous assessment addressed

**Baseline**: No assessment conducted

**Target**: Pass at each phase gate

**Measurement Method**: GDS assessment panel outcome; self-assessment against 14 points

**Dependencies**:
- User research evidence
- Multidisciplinary team in place
- Accessibility audit completed
- Analytics and performance monitoring operational
- Open source and open standards demonstrated

**Risks to Achievement**:
- Insufficient user research evidence
- Team lacks required roles (e.g., no user researcher)
- Accessibility issues not addressed
- Technology choices not aligned with TCoP

---

## Goal-to-Outcome Mapping

### Outcome O-1: Comprehensive Fuel Market Transparency

**Supported Goals**: G-1, G-2, G-3

**Outcome Statement**: ≥95% of UK fuel forecourts with accurate, current prices published and accessible to citizens and third-party consumers within 12 months of launch.

**Measurement Details**:
- **KPI**: Forecourt coverage rate (% of known forecourts with current published prices)
- **Current Value**: 0%
- **Target Value**: ≥95%
- **Measurement Frequency**: Daily
- **Data Source**: Compliance monitoring dashboard
- **Report Owner**: CMA Digital & Data Team

**Business Value**:
- **Financial Impact**: Estimated £Xm annual consumer savings from better-informed purchasing decisions (to be quantified in SOBC)
- **Strategic Impact**: UK becomes international exemplar for fuel market transparency
- **Operational Impact**: CMA market monitoring capability established
- **Customer Impact**: Citizens can reliably find cheapest fuel in their area

**Timeline**:
- **Phase 1 (Months 1-3)**: ≥50% coverage (large chains onboarded)
- **Phase 2 (Months 4-6)**: ≥80% coverage (majority of independents)
- **Phase 3 (Months 7-12)**: ≥95% coverage (near-universal)
- **Sustainment (Year 2+)**: Maintain ≥95%, automate enforcement for remainder

**Stakeholder Benefits**:
- **CMA Board**: Evidence of scheme effectiveness for annual report
- **DESNZ Ministers**: Headline metric for parliamentary answers
- **Citizens**: Comprehensive price data enabling informed choices
- **Trade Bodies**: Level playing field — all competitors visible

**Leading Indicators**:
- Registration rate trending toward target
- Automated (API) submissions increasing weekly
- Submission rejection rate decreasing

**Lagging Indicators**:
- Sustained ≥95% coverage over 3 consecutive months
- Independent academic analysis confirming data comprehensiveness

---

### Outcome O-2: Measurable Consumer Benefit

**Supported Goals**: G-3, G-5

**Outcome Statement**: Evidence of consumer benefit from fuel price transparency — measured through service adoption, user satisfaction, and economic analysis of price convergence.

**Measurement Details**:
- **KPI**: Monthly unique users of the service (direct + via third-party apps)
- **Current Value**: 0
- **Target Value**: 1 million monthly unique users within 12 months
- **Measurement Frequency**: Monthly
- **Data Source**: GOV.UK analytics; API usage metrics
- **Report Owner**: CMA Digital & Data Team

**Business Value**:
- **Financial Impact**: Consumer savings from informed fuel purchasing
- **Strategic Impact**: Demonstrates government intervention improves market outcomes
- **Customer Impact**: User satisfaction ≥80%, task completion ≥95%

**Timeline**:
- **Phase 1 (Months 1-3)**: 100,000 monthly users; media launch coverage
- **Phase 2 (Months 4-6)**: 500,000 monthly users; third-party app integrations live
- **Phase 3 (Months 7-12)**: 1,000,000 monthly users; first economic analysis
- **Sustainment (Year 2+)**: Sustained adoption; annual consumer benefit report

**Stakeholder Benefits**:
- **Citizens**: Demonstrable savings on fuel costs
- **DESNZ Ministers**: Tangible constituent benefit to cite
- **NAO/PAC**: Evidence the investment delivered value
- **CMA Board**: Proof the regulatory recommendation worked

**Leading Indicators**:
- User research participants report they would use the service
- Media coverage generates awareness spikes
- Third-party developers requesting API access

**Lagging Indicators**:
- Sustained monthly user numbers
- Economic analysis showing price convergence in transparent markets
- User satisfaction survey results

---

### Outcome O-3: Effective Regulatory Enforcement

**Supported Goals**: G-2, G-4

**Outcome Statement**: CMA can detect non-compliant retailers within 24 hours, has admissible evidence for enforcement, and achieves ≥95% compliance after enforcement capability is operational.

**Measurement Details**:
- **KPI**: Time to detect non-compliance (hours)
- **Current Value**: Not measurable (no system)
- **Target Value**: <24 hours detection; enforcement tools operational by May 2026
- **Measurement Frequency**: Daily (automated)
- **Data Source**: Compliance monitoring system
- **Report Owner**: CMA Enforcement Division

**Business Value**:
- **Strategic Impact**: Credible enforcement deters non-compliance
- **Operational Impact**: Automated detection reduces manual monitoring
- **Customer Impact**: Comprehensive data due to high compliance

**Timeline**:
- **Phase 1 (Months 1-3)**: Compliance dashboard operational; grace period support focus
- **Phase 2 (Months 4-6)**: Enforcement tools tested; first formal notices after grace period
- **Phase 3 (Months 7-12)**: Full enforcement operational; compliance ≥95%
- **Sustainment (Year 2+)**: Routine enforcement; annual compliance report

**Stakeholder Benefits**:
- **CMA Enforcement**: Effective tools; defensible evidence chain
- **CMA Board**: Credible enforcement capability
- **Trade Bodies**: Fair enforcement — no compliant member unfairly penalised
- **Citizens**: High compliance means comprehensive data

**Leading Indicators**:
- Compliance dashboard accurately identifies test non-compliance scenarios
- Evidence export validated by CMA legal team
- Enforcement tabletop exercise completed successfully

**Lagging Indicators**:
- Sustained ≥95% compliance rate
- Successful enforcement actions (where needed) upheld
- Reduction in non-compliance over time

---

### Outcome O-4: Governance and Assurance Compliance

**Supported Goals**: G-5, G-6, G-7

**Outcome Statement**: The service passes all mandatory governance gates (GDS assessment, Secure by Design, DPIA, TCoP, spend control) and maintains audit-ready documentation.

**Measurement Details**:
- **KPI**: Governance gates passed vs required
- **Current Value**: 0 gates passed
- **Target Value**: All mandatory gates passed at each phase
- **Measurement Frequency**: Per phase gate
- **Data Source**: Assessment outcomes; governance tracker
- **Report Owner**: CMA SRO

**Business Value**:
- **Strategic Impact**: Demonstrates proper governance of public investment
- **Financial Impact**: Avoids rework costs from governance failures
- **Operational Impact**: Sound architecture reduces technical debt

**Timeline**:
- **Phase 1 (Alpha)**: GDS Alpha assessment pass; DPIA complete
- **Phase 2 (Beta)**: GDS Beta assessment pass; Secure by Design assessment; TCoP review
- **Phase 3 (Live)**: GDS Live assessment pass; SIRO sign-off; full operational readiness
- **Sustainment**: Annual reassessment; continuous compliance monitoring

**Stakeholder Benefits**:
- **GDS Assessors**: Well-evidenced assessment
- **CDDO**: TCoP compliance demonstrated
- **NAO/PAC**: Sound governance if audited
- **ICO**: Data protection compliance assured
- **SIRO**: Information risk managed

**Leading Indicators**:
- Self-assessment scores improving at each phase
- No blocking conditions from previous assessments unresolved
- All required roles filled in delivery team

**Lagging Indicators**:
- Pass at each phase gate
- Zero ICO enforcement actions
- Positive NAO assessment (if audited)

---

## Complete Traceability Matrix

### Stakeholder → Driver → Goal → Outcome

| Stakeholder | Driver ID | Driver Summary | Goal ID | Goal Summary | Outcome ID | Outcome Summary |
|-------------|-----------|----------------|---------|--------------|------------|-----------------|
| CMA Board | SD-1 | Demonstrate regulatory effectiveness | G-1 | Universal registration | O-1 | Comprehensive transparency |
| CMA Board | SD-1 | Demonstrate regulatory effectiveness | G-2 | Data submission compliance | O-1 | Comprehensive transparency |
| CMA Board | SD-1 | Demonstrate regulatory effectiveness | G-4 | Enforcement capability | O-3 | Effective enforcement |
| CMA Enforcement | SD-2 | Effective enforcement tools | G-4 | Enforcement capability | O-3 | Effective enforcement |
| CMA Enforcement | SD-2 | Effective enforcement tools | G-2 | Submission compliance | O-1 | Comprehensive transparency |
| DESNZ Policy | SD-3 | Deliver ministerial commitment | G-1 | Universal registration | O-1 | Comprehensive transparency |
| DESNZ Policy | SD-3 | Deliver ministerial commitment | G-7 | GDS assessment pass | O-4 | Governance compliance |
| DESNZ Policy | SD-3 | Deliver ministerial commitment | G-6 | Data protection compliance | O-4 | Governance compliance |
| DESNZ Ministers | SD-4 | Political accountability | G-3 | Trusted citizen service | O-2 | Consumer benefit |
| DESNZ Ministers | SD-4 | Political accountability | G-5 | Value for money | O-2 | Consumer benefit |
| Citizens | SD-5 | Find cheapest fuel | G-3 | Trusted citizen service | O-2 | Consumer benefit |
| Citizens | SD-5 | Find cheapest fuel | G-2 | Submission compliance | O-1 | Comprehensive transparency |
| Large Retailers | SD-6 | Minimise compliance burden | G-1 | Universal registration | O-1 | Comprehensive transparency |
| Large Retailers | SD-6 | Minimise compliance burden | G-2 | Submission compliance | O-1 | Comprehensive transparency |
| Independents | SD-7 | Avoid disproportionate burden | G-1 | Universal registration | O-1 | Comprehensive transparency |
| Independents | SD-7 | Avoid disproportionate burden | G-2 | Submission compliance | O-1 | Comprehensive transparency |
| Trade Bodies | SD-8 | Protect member interests | G-1 | Universal registration | O-1 | Comprehensive transparency |
| Trade Bodies | SD-8 | Protect member interests | G-2 | Submission compliance | O-3 | Effective enforcement |
| GDS Assessors | SD-9 | Service meets standard | G-7 | GDS assessment pass | O-4 | Governance compliance |
| GDS Assessors | SD-9 | Service meets standard | G-3 | Trusted citizen service | O-2 | Consumer benefit |
| ICO | SD-10 | Data protection compliance | G-6 | Data protection | O-4 | Governance compliance |
| Third Parties | SD-11 | Reliable API access | G-3 | Trusted citizen service | O-2 | Consumer benefit |
| NAO / PAC | SD-12 | Value for money | G-5 | VfM demonstration | O-4 | Governance compliance |

### Conflict Analysis

**Competing Drivers**:

- **Conflict 1**: **Speed vs Governance** — DESNZ Ministers (SD-4) want rapid, visible delivery to meet political timelines. GDS Assessors (SD-9) require thorough user research and phased delivery. Attempting to skip governance creates assessment failure risk.
  - **Resolution Strategy**: Commit to GDS phases but compress timescales within each phase. Front-load user research. Conduct pre-assessment check-ins with GDS to identify issues early. Communicate phased delivery as evidence of responsible governance, not delay.

- **Conflict 2**: **Enforcement Rigour vs Retailer Support** — CMA Enforcement (SD-2) needs effective tools to act against non-compliance. Independent Retailers (SD-7) and Trade Bodies (SD-8) want a supportive onboarding approach with no penalties during transition. Too-aggressive enforcement alienates retailers and creates media backlash. Too-lenient enforcement undermines the scheme.
  - **Resolution Strategy**: Respect the legislative grace period (until May 2026). Use the grace period for genuine support — onboarding assistance, technical help, compliance reminders. After the grace period, escalate proportionately: automated reminders → formal warnings → penalties. Publish the enforcement approach transparently so retailers know what to expect.

- **Conflict 3**: **Data Granularity vs Commercial Sensitivity** — Citizens (SD-5) and CMA (SD-1) want comprehensive, granular, real-time data. Large Retailers (SD-6) have concerns about competitors seeing pricing strategy in real time.
  - **Resolution Strategy**: The regulations define the required data scope — stick to statutory requirements. Data is already displayed on forecourt price boards, so digital publication doesn't reveal additional information. Frame as levelling the playing field. Consider reasonable time-delay (e.g., 30-minute buffer) if legally permissible and aligned with user needs.

**Synergies**:

- **Synergy 1**: CMA Board (SD-1) and Citizens (SD-5) share the fundamental goal of market transparency — comprehensive, accurate data serves both enforcement and consumer value simultaneously.

- **Synergy 2**: Large Retailers (SD-6) wanting API integration and Third-Party Consumers (SD-11) wanting API access both drive investment in a well-documented, reliable API — a single capability satisfies both stakeholders.

- **Synergy 3**: GDS assessment requirements (SD-9) and Citizen needs (SD-5) are aligned — meeting the Service Standard inherently means building a service that works for users, is accessible, and performs well.

- **Synergy 4**: DESNZ Ministers (SD-4) and NAO/PAC (SD-12) both benefit from clear benefits realisation — investing in measurement capability serves both political accountability and financial audit readiness.

---

## Communication & Engagement Plan

### CMA Board / Chair

**Primary Message**: The programme is on track to deliver a functioning open data scheme with measurable market transparency outcomes and credible enforcement capability.

**Key Talking Points**:
- Registration and submission rates vs targets
- Enforcement readiness timeline
- Early evidence of market impact

**Communication Frequency**: Quarterly (formal board paper); monthly (SRO update)

**Preferred Channel**: Board paper with executive summary; oral briefing from SRO

**Success Story**: "95% of forecourts now submitting data, and early analysis shows price convergence in competitive areas"

---

### DESNZ Ministers

**Primary Message**: The Fuel Finder is delivering visible consumer benefit, the scheme is on track, and here are the headline metrics you can use in parliamentary answers.

**Key Talking Points**:
- Headline coverage and usage statistics
- Consumer benefit narrative (savings, trust, comprehensiveness)
- Responses to anticipated parliamentary questions

**Communication Frequency**: Monthly (briefing note); ad hoc (PQ support)

**Preferred Channel**: Ministerial briefing note (1 page); PQ response drafts

**Success Story**: "Over 1 million motorists used Fuel Finder last month, with 95% of UK forecourts now publishing real-time prices"

---

### Independent Retailers

**Primary Message**: We are here to help you comply. The process is simple, support is available, and the grace period gives you time to get set up.

**Key Talking Points**:
- Step-by-step registration guide in plain English
- Phone and email support available
- Grace period means no penalties while you're getting started
- Simple web form for manual price submission

**Communication Frequency**: Weekly during onboarding period; monthly after stabilisation

**Preferred Channel**: Trade body newsletters (PRA); direct email; GOV.UK guidance pages; phone helpline

**Success Story**: "Single-site operator registers and submits first price in under 10 minutes with no IT skills needed"

---

### Trade Bodies (PRA, UKPIA)

**Primary Message**: We value your input, the scheme is designed to be workable for your members, and we will consult on any changes.

**Key Talking Points**:
- Technical specifications shared for member review
- Enforcement approach is proportionate (warnings before penalties)
- Regular liaison meetings to raise member concerns
- Support materials available for cascade to members

**Communication Frequency**: Fortnightly during onboarding; monthly after stabilisation

**Preferred Channel**: Liaison meetings; email; shared documentation portal

**Success Story**: "Trade body feedback on API specification incorporated, reducing member integration effort by 40%"

---

### Third-Party Data Consumers

**Primary Message**: High-quality, well-documented open data is available via API and bulk download, and we welcome third-party innovation.

**Key Talking Points**:
- API documentation and sandbox available
- Open Government Licence — free to use commercially
- Rate limits and fair use policy published
- Change notification process for API updates

**Communication Frequency**: Monthly developer newsletter; as-needed for breaking changes

**Preferred Channel**: Developer portal; GitHub discussions; email newsletter

**Success Story**: "Major navigation app integrates Fuel Finder data, reaching 5 million additional users"

---

## Change Impact Assessment

### Impact on Stakeholders

| Stakeholder | Current State | Future State | Change Magnitude | Resistance Risk | Mitigation Strategy |
|-------------|---------------|--------------|------------------|-----------------|---------------------|
| Citizens | No comprehensive fuel price comparison | Single government service with all forecourt prices | LOW (opt-in) | LOW | Awareness campaign; simple design |
| Large Retailers | No mandatory reporting | Automated API submission of all prices | MEDIUM | LOW | API integration; technical support |
| Independents | No mandatory reporting | Manual or semi-automated price submission | HIGH | HIGH | Assisted digital; plain English guides; grace period |
| CMA Enforcement | No fuel price enforcement tools | New compliance monitoring and enforcement capability | HIGH | LOW | Co-design approach; training |
| Trade Bodies | Represent members on voluntary basis | Active intermediary for regulatory compliance | MEDIUM | MEDIUM | Consultation; liaison role formalised |
| Third Parties | Partial/commercial fuel price data | Comprehensive free open data | LOW (beneficial) | LOW | Good documentation; stable API |

### Change Readiness

**Champions** (Enthusiastic supporters):
- **CMA Digital & Data Team** — Building the service; intrinsically motivated by mission
- **DESNZ Policy Team** — Delivering their policy commitment
- **Third-Party Consumers** — Free access to comprehensive data
- **Citizens** — Direct financial benefit

**Fence-sitters** (Neutral, need convincing):
- **Large Retailers** — Will comply but want minimal burden; convince through good API design and technical support
- **Trade Bodies** — Supportive in principle but vigilant about member interests; convince through genuine consultation

**Resisters** (Opposed or skeptical):
- **Independent Retailers** — Perceive burden without proportionate benefit to them personally; address through simplicity, support, and emphasising that transparency helps them compete with supermarkets
- **Some NAO/PAC members** — Skeptical of government digital delivery; address through robust governance and transparent cost reporting

---

## Risk Register (Stakeholder-Related)

### Risk R-1: Low Independent Retailer Compliance

**Related Stakeholders**: Independent Retailers (SD-7), Trade Bodies (SD-8), CMA Enforcement (SD-2)

**Risk Description**: Independent forecourt operators fail to register or submit data due to limited digital capability, lack of awareness, or active resistance, undermining data comprehensiveness.

**Impact on Goals**: G-1 (registration), G-2 (submission compliance), O-1 (market transparency)

**Probability**: HIGH

**Impact**: HIGH

**Mitigation Strategy**:
- Partner with PRA for member communications
- Provide simple web-based submission (no API required)
- Offer phone and email assisted digital support
- Use grace period for proactive outreach to non-registered forecourts
- Provide multilingual guidance where needed

**Contingency Plan**: If compliance remains low after grace period, CMA issues formal warnings with clear escalation timeline. Consider whether simplified mobile app submission would improve compliance.

---

### Risk R-2: Ministerial or Parliamentary Pressure Compromises Governance

**Related Stakeholders**: DESNZ Ministers (SD-4), GDS Assessors (SD-9)

**Risk Description**: Political pressure to launch quickly leads to cutting corners on user research, accessibility, or security — resulting in GDS assessment failure or security incidents.

**Impact on Goals**: G-7 (GDS assessment), G-3 (citizen service quality)

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**:
- Establish clear phase gate expectations with ministerial team from outset
- Provide regular progress updates demonstrating momentum within governance
- Frame GDS assessment as risk mitigation, not bureaucracy
- Pre-assessment check-ins to catch issues early

**Contingency Plan**: If assessment fails, present clear remediation plan with timeline. Private Beta can run while addressing conditions.

---

### Risk R-3: Trade Body Opposition Generates Negative Media

**Related Stakeholders**: Trade Bodies (SD-8), Media, DESNZ Ministers (SD-4)

**Risk Description**: Trade bodies publicly oppose the scheme's data requirements or enforcement approach, generating negative media coverage that undermines public confidence and creates political pressure.

**Impact on Goals**: G-1 (registration), O-2 (consumer benefit through adoption)

**Probability**: MEDIUM

**Impact**: MEDIUM

**Mitigation Strategy**:
- Genuine consultation on technical specifications before publication
- Proportionate enforcement approach with published guidance
- Regular liaison meetings showing responsiveness to feedback
- Proactive positive media narrative about consumer benefit

**Contingency Plan**: If negative coverage emerges, respond with evidence of consultation, proportionality, and consumer benefit. Minister-level engagement with trade body leadership.

---

### Risk R-4: Data Quality Too Low for Citizen Trust

**Related Stakeholders**: Citizens (SD-5), CMA Board (SD-1), Media

**Risk Description**: Published prices are frequently inaccurate, stale, or incomplete, causing citizens to lose trust and abandon the service. Media reports "government fuel price tool shows wrong prices."

**Impact on Goals**: G-2 (compliance), G-3 (citizen service), O-2 (consumer benefit)

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**:
- Automated data quality validation at ingestion (plausible price ranges, required fields)
- Clear "last updated" timestamps displayed to users
- Anomaly detection for suspicious submissions
- Data quality dashboard visible to operations team
- Retailer feedback mechanism for price corrections

**Contingency Plan**: If quality issues emerge, display data confidence indicators. Temporarily suppress forecourts with known data quality issues rather than showing wrong prices. Engage enforcement for persistent offenders.

---

### Risk R-5: CMA-DESNZ Inter-departmental Friction

**Related Stakeholders**: CMA Board (SD-1), DESNZ Policy (SD-3), DESNZ Ministers (SD-4)

**Risk Description**: CMA (enforcement body) and DESNZ (policy owner) have different priorities, timelines, or views on the scheme's implementation, causing delays or conflicting messaging to retailers.

**Impact on Goals**: G-1 (registration), G-4 (enforcement), G-5 (VfM)

**Probability**: MEDIUM

**Impact**: MEDIUM

**Mitigation Strategy**:
- Joint programme board with CMA and DESNZ senior representation
- Single published view of requirements and timelines
- MoU or working agreement defining responsibilities
- Regular senior sponsor meetings (CMA + DESNZ)

**Contingency Plan**: Escalate to respective Permanent Secretaries if joint governance fails. Involve Cabinet Office if inter-departmental alignment proves intractable.

---

## Governance & Decision Rights

### Decision Authority Matrix (RACI)

| Decision Type | Responsible | Accountable | Consulted | Informed |
|---------------|-------------|-------------|-----------|----------|
| Programme budget approval | CMA Finance | CMA SRO | HM Treasury, CDDO | DESNZ, NAO |
| Regulatory requirements interpretation | CMA Legal | DESNZ Policy Lead | CMA Enforcement | Trade Bodies, Retailers |
| Technology architecture | CMA Technical Architect | CMA Digital Lead | GDS, CDDO | CMA SRO, DESNZ |
| Data schema and API design | CMA Digital Lead | CMA SRO | Trade Bodies, Large Retailers, Third Parties | GDS Assessors |
| Enforcement approach and timing | CMA Enforcement Lead | CMA Board | DESNZ Ministers, Trade Bodies | Retailers, Media |
| User-facing design decisions | User Research Lead / Designer | CMA Digital Lead | Citizens (via research), GDS | CMA SRO, DESNZ |
| Go/No-go for phase transitions | CMA SRO | CMA Board | GDS Assessors, SIRO, DESNZ | All stakeholders |
| Data protection decisions | DPO | SIRO | ICO (if consulted), CMA Legal | CMA SRO, DESNZ |
| Security risk acceptance | SIRO | CMA Accounting Officer | CMA Security, NCSC | CMA Board |

### Escalation Path

1. **Level 1**: Delivery Manager / Product Owner — day-to-day delivery decisions, sprint priorities, minor scope adjustments
2. **Level 2**: CMA Digital Lead / Programme Manager — cross-team dependencies, technical trade-offs, resource allocation
3. **Level 3**: CMA SRO — programme-level scope, timeline, or budget changes; inter-departmental issues
4. **Level 4**: CMA Board / DESNZ Permanent Secretary — strategic direction, major conflicts, ministerial concerns
5. **Level 5**: Cabinet Office — inter-departmental alignment failures (last resort)

---

## Validation & Sign-off

### Stakeholder Review

| Stakeholder | Review Date | Comments | Status |
|-------------|-------------|----------|--------|
| CMA SRO | PENDING | | PENDING |
| DESNZ Policy Lead | PENDING | | PENDING |
| CMA Enforcement Lead | PENDING | | PENDING |
| CMA Digital Lead | PENDING | | PENDING |
| PRA Representative | PENDING | | PENDING |
| UKPIA Representative | PENDING | | PENDING |

### Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Programme SRO | | | |
| DESNZ Policy Owner | | | |
| Enterprise Architect | | | |

---

## Appendices

### Appendix A: Stakeholder Interview Plan

The following stakeholder interviews should be conducted to validate and refine this analysis:

| Stakeholder | Proposed Date | Topics | Interviewer |
|-------------|---------------|--------|-------------|
| CMA Enforcement Lead | TBC | Enforcement tools, evidence requirements, grace period approach | Programme Manager |
| DESNZ Policy Lead | TBC | Regulatory milestones, ministerial priorities, policy evolution | Programme Manager |
| PRA Representative | TBC | Independent retailer challenges, compliance support needs | User Researcher |
| UKPIA Representative | TBC | Large retailer API requirements, commercial sensitivity | User Researcher |
| Sample motorists (6-8) | TBC | Price comparison needs, trust factors, digital capability | User Researcher |
| Sample independent retailer (3-5) | TBC | Digital capability, compliance burden, support needs | User Researcher |
| GDS Assessment Lead | TBC | Assessment expectations, common issues, pre-assessment support | Delivery Manager |

### Appendix B: Regulatory Timeline

| Date | Milestone | Impact |
|------|-----------|--------|
| 2025-12-18 | CMA enforcement guidance published | Enforcement approach defined |
| 2026-02-02 | Forecourt registration deadline | All forecourts must be registered |
| 2026-05 (early) | Enforcement grace period ends | CMA may begin formal enforcement |
| 2026-Q2 | Expected Alpha assessment | GDS phase gate |
| 2026-Q3 | Expected Beta assessment | GDS phase gate |
| 2027-Q1 | Expected Live assessment | GDS phase gate |
| 2027-Q2 | NAO potential audit window | First post-launch audit opportunity |

### Appendix C: References

- ARC-000-PRIN-v1.0 — Enterprise Architecture Principles
- Motor Fuel Price (Open Data) Regulations 2025
- CMA Fuel Finder Enforcement Guidance (December 2025)
- GDS Service Standard (14 points)
- Technology Code of Practice (TCoP)
- GOV.UK Guidance: Fuel Finder (https://www.gov.uk/guidance/fuel-finder)

---

**Generated by**: ArcKit `/arckit.stakeholders` command
**Generated on**: 2026-01-30
**ArcKit Version**: 1.0.3
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: Claude Opus 4.5
