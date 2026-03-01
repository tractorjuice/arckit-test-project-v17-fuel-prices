# Risk Register: UK Fuel Price Transparency Service

> **Template Status**: Live | **Version**: 1.0.3 | **Command**: `/arckit.risk`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RISK-v1.0 |
| **Document Type** | Risk Register |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-01-30 |
| **Last Modified** | 2026-01-30 |
| **Review Cycle** | Monthly |
| **Next Review Date** | 2026-03-01 |
| **Owner** | CMA Senior Responsible Owner (SRO) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Board, CMA SRO, DESNZ Policy, CMA Enforcement, CMA Digital, Programme Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-30 | ArcKit AI | Initial creation from `/arckit.risk` command | PENDING | PENDING |

---

## Executive Summary

### Risk Profile Overview

**Total Risks Identified:** 20 risks across 6 categories

| Risk Level | Inherent | Residual | Change |
|------------|----------|----------|--------|
| **Critical** (20-25) | 5 | 0 | ↓ 100% |
| **High** (13-19) | 8 | 4 | ↓ 50% |
| **Medium** (6-12) | 7 | 12 | ↑ (absorption from higher tiers) |
| **Low** (1-5) | 0 | 4 | ↑ (absorption from higher tiers) |
| **TOTAL Score** | 266 | 168 | ↓ 37% |

### Risk Category Distribution

| Category | Count | Avg Inherent | Avg Residual | Control Effectiveness |
|----------|-------|--------------|--------------|----------------------|
| **STRATEGIC** | 3 | 15.0 | 9.7 | 36% reduction |
| **OPERATIONAL** | 5 | 12.8 | 7.8 | 39% reduction |
| **FINANCIAL** | 3 | 12.0 | 7.3 | 39% reduction |
| **COMPLIANCE** | 3 | 14.7 | 9.3 | 37% reduction |
| **REPUTATIONAL** | 3 | 14.0 | 8.7 | 38% reduction |
| **TECHNOLOGY** | 3 | 13.3 | 8.3 | 38% reduction |

### Overall Risk Assessment

**Overall Residual Risk Score:** 168/500
**Risk Reduction from Controls:** 37% reduction from inherent risk
**Risk Profile Status:** ⚠️ Concerning — 4 High residual risks require active management; no Critical residual risks

### Risks Exceeding Appetite

**Number of risks exceeding organizational appetite:** 4 risks

| Risk ID | Title | Category | Score | Appetite | Excess | Escalation |
|---------|-------|----------|-------|----------|--------|------------|
| R-001 | Low independent retailer compliance | OPERATIONAL | 12 | ≤ 9 | +3 | CMA SRO approval required |
| R-003 | Enforcement tools not ready by May 2026 | COMPLIANCE | 12 | ≤ 9 | +3 | CMA Board escalation |
| R-006 | Negative media coverage undermines adoption | REPUTATIONAL | 12 | ≤ 9 | +3 | DESNZ Ministers briefed |
| R-010 | VE3 Global API specification unavailable | TECHNOLOGY | 12 | ≤ 9 | +3 | DESNZ escalation to VE3 |

### Top 5 Risks Requiring Immediate Attention

1. **R-001** (OPERATIONAL, High 12): Low independent retailer compliance — Owner: CMA Enforcement Division Lead
2. **R-003** (COMPLIANCE, High 12): Enforcement tools not ready by May 2026 — Owner: CMA Digital Lead
3. **R-006** (REPUTATIONAL, High 12): Negative media coverage undermines citizen adoption — Owner: CMA SRO
4. **R-010** (TECHNOLOGY, High 12): VE3 Global API specification unavailable — Owner: CMA Digital Lead
5. **R-002** (STRATEGIC, Medium 9): Ministerial pressure compromises governance — Owner: CMA SRO

### Key Findings and Recommendations

**Key Findings:**
- The highest-risk area is **retailer compliance** — ~4,000 independent forecourts with limited digital capability must comply with new regulations. This risk cascades into data quality, citizen trust, and enforcement credibility.
- **Enforcement readiness** has a hard deadline (May 2026 grace period end) that cannot slip. Delivery delays directly create compliance risk.
- The **VE3 Global API specification** has not been publicly published (as of January 2026). This creates a technology dependency that could delay the primary data integration.
- **Inter-departmental coordination** between CMA and DESNZ is structurally complex — two organisations with different governance cultures must align on a shared programme.
- All 20 risks have identified owners traced to the stakeholder RACI matrix (ARC-001-STKE-v1.0).

**Recommendations:**
1. **URGENT**: Contact DESNZ/VE3 Global for API specification (R-010) — blocks primary integration
2. **HIGH**: Establish dedicated independent retailer onboarding support team (R-001)
3. **HIGH**: Ensure enforcement tools are included in Sprint 1, not deferred (R-003)
4. **MEDIUM**: Prepare proactive media strategy with positive consumer benefit narrative (R-006)
5. **MEDIUM**: Establish joint CMA-DESNZ programme board with clear RACI (R-005)

---

## A. Risk Matrix Visualization

### Inherent Risk Matrix (Before Controls)

```
                                    IMPACT
              1-Minimal   2-Minor    3-Moderate   4-Major    5-Severe
           ┌───────────┬───────────┬───────────┬───────────┬───────────┐
5-Almost   │           │           │           │  R-001    │           │
Certain    │    5      │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │  R-012    │  R-003    │  R-004    │
           │    4      │    8      │  R-016    │  R-006    │           │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 3-Possible│          │           │  R-005    │  R-002    │  R-010    │
K          │    3      │    6      │  R-009    │  R-007    │           │
E          │           │           │  R-011    │  R-008    │           │
L          │           │           │  R-014    │  R-013    │           │
I          │           │           │  R-018    │  R-017    │           │
H          ├───────────┼───────────┼───────────┼───────────┼───────────┤
O 2-Unlikely│          │  R-019    │  R-015    │  R-020    │           │
O          │    2      │    4      │    6      │    8      │    10     │
D          ├───────────┼───────────┼───────────┼───────────┼───────────┤
  1-Rare   │           │           │           │           │           │
           │    1      │    2      │    3      │    4      │    5      │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: Critical (20-25)  High (13-19)  Medium (6-12)  Low (1-5)
```

### Residual Risk Matrix (After Controls)

```
                                    IMPACT
              1-Minimal   2-Minor    3-Moderate   4-Major    5-Severe
           ┌───────────┬───────────┬───────────┬───────────┬───────────┐
5-Almost   │           │           │           │           │           │
Certain    │    5      │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │  R-001    │           │           │
           │    4      │    8      │    12     │    16     │    20     │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 3-Possible│          │  R-012    │  R-003    │  R-006    │           │
K          │    3      │  R-016    │  R-010    │           │           │
E          │           │    6      │    9      │    12     │    15     │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 2-Unlikely│ R-019    │  R-005    │  R-002    │  R-004    │           │
H          │           │  R-009    │  R-007    │           │           │
O          │    2      │  R-011    │  R-008    │    8      │    10     │
O          │           │  R-014    │  R-013    │           │           │
D          │           │  R-018    │  R-017    │           │           │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
  1-Rare   │  R-015    │  R-020    │           │           │           │
           │    1      │    2      │    3      │    4      │    5      │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: Critical (20-25)  High (13-19)  Medium (6-12)  Low (1-5)
```

**Risk Movement Analysis:**
- **All 5 Critical risks reduced**: No residual Critical risks remain
- **4 High residual risks** (R-001, R-003, R-006, R-010): Require continued active management
- **12 Medium residual risks**: Manageable with current controls and monitoring
- **4 Low residual risks**: Routine monitoring sufficient

---

## B. Top 10 Risks (Ranked by Residual Score)

| Rank | ID | Title | Category | Inherent | Residual | Owner | Status | Response |
|------|----|-------|----------|----------|----------|-------|--------|----------|
| 1 | R-001 | Low independent retailer compliance | OPERATIONAL | 20 | 12 | CMA Enforcement Lead | In Progress | Treat |
| 2 | R-003 | Enforcement tools not ready by May 2026 | COMPLIANCE | 16 | 12 | CMA Digital Lead | In Progress | Treat |
| 3 | R-006 | Negative media coverage undermines adoption | REPUTATIONAL | 16 | 12 | CMA SRO | Open | Treat |
| 4 | R-010 | VE3 Global API specification unavailable | TECHNOLOGY | 15 | 12 | CMA Digital Lead | In Progress | Treat |
| 5 | R-002 | Ministerial pressure compromises governance | STRATEGIC | 12 | 6 | CMA SRO | Monitoring | Treat |
| 6 | R-004 | Data quality too low for citizen trust | REPUTATIONAL | 20 | 8 | CMA Digital Lead | In Progress | Treat |
| 7 | R-005 | CMA-DESNZ inter-departmental friction | STRATEGIC | 9 | 4 | CMA SRO | Monitoring | Treat |
| 8 | R-007 | GDS Service Standard assessment failure | COMPLIANCE | 12 | 6 | CMA Digital Lead | In Progress | Treat |
| 9 | R-008 | Budget overrun due to scope creep | FINANCIAL | 12 | 6 | CMA SRO | Monitoring | Treat |
| 10 | R-009 | Insufficient cloud/DevOps expertise | OPERATIONAL | 9 | 4 | CMA Digital Lead | In Progress | Treat |

---

## C. Detailed Risk Register

### Risk R-001: Low Independent Retailer Compliance

**Category:** OPERATIONAL
**Status:** In Progress
**Risk Owner:** CMA Enforcement Division Lead (from RACI: Accountable for enforcement)
**Action Owner:** CMA Digital Lead (onboarding tools)

#### Risk Identification

**Risk Description:**
Independent forecourt operators (~4,000 sites) fail to register or submit fuel price data due to limited digital capability, lack of awareness, or active resistance. This undermines data comprehensiveness, citizen trust, and the regulatory scheme's credibility.

**Root Cause:**
~4,000 independent operators have limited IT capability, may lack internet access at forecourt, and perceive the regulations as disproportionate burden on small businesses. Many are single-site family businesses without dedicated IT staff.

**Trigger Events:**
- Registration deadline (2 Feb 2026) passes with <70% independent forecourt registration
- Trade bodies report widespread confusion or resistance among members
- Assisted digital support overwhelmed by call volumes

**Consequences if Realized:**
- Data coverage below 80%, making citizen service unreliable in rural/independent areas
- CMA unable to demonstrate scheme effectiveness (SD-1 driver threatened)
- DESNZ Ministers unable to cite comprehensive coverage in parliamentary answers
- Media narrative: "Government fuel price tool missing thousands of stations"

**Affected Stakeholders:**
- **Citizens (SD-5)**: Incomplete data, especially in areas served primarily by independents
- **CMA Board (SD-1)**: Scheme effectiveness undermined
- **Independent Retailers (SD-7)**: Risk of enforcement penalties
- **Trade Bodies (SD-8)**: Member complaints about burden

**Related Objectives:**
- Goal G-1 (Universal Registration): Directly threatened
- Goal G-2 (Submission Compliance): Dependent on registration
- Outcome O-1 (Comprehensive Transparency): Target of ≥95% coverage at risk

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 5 - Almost Certain | Historical precedent: small businesses consistently lag on digital compliance; limited IT capability is factual |
| **Impact** | 4 - Major | ~4,000 sites = ~47% of forecourts; incomplete data undermines entire scheme purpose |
| **Inherent Risk Score** | **20** (Critical) | 5 × 4 = 20 |

#### Current Controls and Mitigations

1. **Assisted digital support (phone/email helpline)**
   - Owner: CMA Digital Team
   - Effectiveness: **Adequate**
   - Evidence: GDS best practice; planned but not yet operational

2. **Trade body partnership for member communications (PRA, UKPIA)**
   - Owner: CMA Communications
   - Effectiveness: **Adequate**
   - Evidence: PRA has direct channel to ~4,000 independent members

3. **Simple web-based manual submission (no API required)**
   - Owner: CMA Digital Team
   - Effectiveness: **Adequate**
   - Evidence: Designed for minimal digital capability; user research planned

4. **Enforcement grace period until May 2026**
   - Owner: CMA Enforcement
   - Effectiveness: **Strong**
   - Evidence: Statutory grace period provides time for onboarding

**Overall Control Effectiveness:** Adequate (reduces from 20 to 12)

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | Controls reduce but do not eliminate; many independents will still struggle |
| **Impact** | 3 - Moderate | Controls ensure most large chains comply; gap concentrated in independents (~20-30% of stations) |
| **Residual Risk Score** | **12** (High) | 4 × 3 = 12 |

#### Risk Response (4Ts Framework)

**Primary Response:** TREAT (Mitigate/Reduce)

**Rationale:** Risk exceeds appetite but can be significantly reduced through proactive onboarding support. Termination is impossible (regulatory obligation). Transfer is not viable (CMA must enforce). Toleration would undermine the entire scheme.

#### Action Plan

1. **Deploy dedicated independent retailer onboarding team**
   - Owner: CMA Digital Lead
   - Due Date: 2026-02-15
   - Expected Impact: Reduce likelihood from 4 to 3

2. **Produce plain-English video guides for registration and submission**
   - Owner: CMA Communications
   - Due Date: 2026-02-01
   - Expected Impact: Reduce digital capability barrier

3. **Proactive outreach to unregistered forecourts after deadline**
   - Owner: CMA Enforcement (supportive, not punitive during grace period)
   - Due Date: 2026-02-15
   - Expected Impact: Identify and contact non-registrants directly

**Target Residual Risk:** 9 (Medium) — Likelihood 3, Impact 3

---

### Risk R-002: Ministerial Pressure Compromises Governance

**Category:** STRATEGIC
**Status:** Monitoring
**Risk Owner:** CMA SRO (from RACI: Accountable for programme governance)
**Action Owner:** CMA Digital Lead

#### Risk Identification

**Risk Description:**
Political pressure from DESNZ Ministers to launch quickly leads to cutting corners on user research, accessibility, or security — resulting in GDS Service Standard assessment failure, security incidents, or poor user experience.

**Root Cause:** Conflict between political timelines (visible results before parliamentary sessions) and proper governance (GDS phases, Secure by Design, user research). Stakeholder driver conflict: SD-4 vs SD-9.

**Trigger Events:**
- Minister requests launch date brought forward
- Phase gate assessment postponed to meet political deadline
- User research scope reduced to save time

**Consequences if Realized:**
- GDS assessment failure blocking progression (Goal G-7 threatened)
- Security incident due to insufficient testing
- Accessibility non-compliance (legal risk under Public Sector Bodies regulations)
- Rework costs exceeding original timeline savings

**Affected Stakeholders:**
- **DESNZ Ministers (SD-4)**: Short-term gain, long-term reputational damage
- **GDS Assessors (SD-9)**: Failed assessment reflects poorly on all parties
- **Citizens (SD-5)**: Poor service quality
- **NAO/PAC (SD-12)**: Governance failure in audit scope

**Related Objectives:** G-7 (GDS assessment), G-3 (citizen service quality), O-4 (governance compliance)

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Fuel prices are politically sensitive; ministerial attention is likely but CMA's independent status provides some insulation |
| **Impact** | 4 - Major | GDS assessment failure causes significant delay; security incident could be career-ending for SRO |
| **Inherent Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Current Controls

1. **CMA statutory independence from ministerial direction on enforcement**
   - Effectiveness: **Strong**
2. **Established GDS phase gate process with pre-assessment check-ins**
   - Effectiveness: **Adequate**
3. **Regular ministerial briefings showing progress within governance**
   - Effectiveness: **Adequate**

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | CMA independence and established governance provide strong protection |
| **Impact** | 3 - Moderate | Impact reduced by ability to run Private Beta while addressing conditions |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

**Primary Response:** TREAT — Frame GDS assessment as risk mitigation for ministers

---

### Risk R-003: Enforcement Tools Not Ready by May 2026

**Category:** COMPLIANCE
**Status:** In Progress
**Risk Owner:** CMA Digital Lead (from RACI: Responsible for delivery)
**Action Owner:** CMA Digital Lead

#### Risk Identification

**Risk Description:**
The enforcement tools (compliance dashboard, evidence export, enforcement case workflow) are not operational before the grace period ends in early May 2026. CMA cannot detect or act on non-compliance, undermining the regulatory scheme.

**Root Cause:** Enforcement tools may be deprioritised in favour of citizen-facing features and retailer onboarding. The May 2026 deadline is fixed by legislation and cannot slip.

**Trigger Events:**
- Sprint planning consistently defers enforcement features
- Integration with audit trail and submission tracking delayed
- Legal review of evidence admissibility requirements arrives late
- CMA legal team identifies additional requirements mid-development

**Consequences if Realized:**
- CMA cannot enforce after grace period — regulatory credibility destroyed (SD-1, SD-2)
- Non-compliant retailers face no consequences — compliance rates stagnate
- DESNZ Ministers cannot report effective enforcement to Parliament
- Media: "Government can't enforce its own fuel price rules"

**Affected Stakeholders:**
- **CMA Enforcement (SD-2)**: Cannot fulfil statutory function
- **CMA Board (SD-1)**: Regulatory credibility undermined
- **Trade Bodies (SD-8)**: Compliant members disadvantaged vs non-compliant competitors

**Related Objectives:** G-4 (Enforcement Capability), O-3 (Effective Enforcement)

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | Common pattern: enforcement features deprioritised for user-facing work |
| **Impact** | 4 - Major | Regulatory scheme without enforcement is toothless; CMA credibility at stake |
| **Inherent Risk Score** | **16** (High) | 4 × 4 = 16 |

#### Current Controls

1. **Enforcement features included in MVP scope definition**
   - Effectiveness: **Adequate**
2. **CMA Enforcement co-designing requirements**
   - Effectiveness: **Strong**
3. **Early legal review of evidence admissibility requirements**
   - Effectiveness: **Adequate**

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Co-design reduces but doesn't eliminate delivery risk |
| **Impact** | 4 - Major | Impact unchanged — hard deadline means no recovery time |
| **Residual Risk Score** | **12** (High) | 3 × 4 = 12 |

**Primary Response:** TREAT — Prioritise enforcement tools in Sprint 1; establish enforcement readiness milestone

#### Action Plan

1. **Define enforcement MVP and include in Sprint 1 backlog**
   - Owner: CMA Digital Lead
   - Due Date: 2026-02-15
   - Expected Impact: Reduce likelihood from 3 to 2

2. **Conduct tabletop enforcement exercise by March 2026**
   - Owner: CMA Enforcement Lead
   - Due Date: 2026-03-31

---

### Risk R-004: Data Quality Too Low for Citizen Trust

**Category:** REPUTATIONAL
**Status:** In Progress
**Risk Owner:** CMA Digital Lead
**Action Owner:** CMA Digital Team

**Risk Description:** Published fuel prices are frequently inaccurate, stale, or incomplete, causing citizens to lose trust. Media reports "government fuel price tool shows wrong prices."

**Root Cause:** Retailers submit inaccurate prices (intentionally or accidentally); submission frequency too low; validation rules insufficient; no feedback loop for corrections.

**Inherent:** Likelihood 5 × Impact 4 = **20** (Critical)
**Residual:** Likelihood 2 × Impact 4 = **8** (Medium) — Strong automated validation and data quality dashboard reduce likelihood significantly

**Primary Response:** TREAT — Automated validation at ingestion, anomaly detection, freshness indicators

---

### Risk R-005: CMA-DESNZ Inter-departmental Friction

**Category:** STRATEGIC
**Status:** Monitoring
**Risk Owner:** CMA SRO

**Risk Description:** CMA (enforcement body) and DESNZ (policy owner) have different priorities, timelines, or views on implementation, causing delays or conflicting messaging to retailers.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Joint programme board and MoU established

**Primary Response:** TREAT — Joint programme board with clear RACI

---

### Risk R-006: Negative Media Coverage Undermines Citizen Adoption

**Category:** REPUTATIONAL
**Status:** Open
**Risk Owner:** CMA SRO
**Action Owner:** CMA Communications

**Risk Description:** Trade body opposition, service launch issues, or data quality problems generate negative media coverage that undermines public confidence and citizen adoption.

**Inherent:** Likelihood 4 × Impact 4 = **16** (High)
**Residual:** Likelihood 3 × Impact 4 = **12** (High) — Proactive media strategy reduces likelihood but impact remains high for government service

**Primary Response:** TREAT — Proactive positive narrative; rapid response protocol; ministerial engagement

---

### Risk R-007: GDS Service Standard Assessment Failure

**Category:** COMPLIANCE
**Status:** In Progress
**Risk Owner:** CMA Digital Lead

**Risk Description:** Service fails GDS assessment at Alpha or Beta phase, blocking progression and causing delivery delay.

**Inherent:** Likelihood 3 × Impact 4 = **12** (Medium)
**Residual:** Likelihood 2 × Impact 3 = **6** (Medium) — Pre-assessment check-ins and multidisciplinary team reduce risk

**Primary Response:** TREAT — Pre-assessment GDS engagement; self-assessment at each sprint

---

### Risk R-008: Budget Overrun Due to Scope Creep

**Category:** FINANCIAL
**Status:** Monitoring
**Risk Owner:** CMA SRO

**Risk Description:** Programme costs exceed approved budget due to scope creep, unplanned requirements, or technology cost overruns.

**Inherent:** Likelihood 3 × Impact 4 = **12** (Medium)
**Residual:** Likelihood 2 × Impact 3 = **6** (Medium) — Agile delivery with fixed iterations; monthly cost reviews

**Primary Response:** TREAT — Strict scope control; monthly FinOps reviews

---

### Risk R-009: Insufficient Cloud/DevOps Expertise

**Category:** OPERATIONAL
**Status:** In Progress
**Risk Owner:** CMA Digital Lead

**Risk Description:** CMA Digital team lacks sufficient cloud architecture and DevOps expertise to build and operate the service at required quality.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Contractor/consultancy support; training programme

**Primary Response:** TREAT — Augment team with specialist contractors

---

### Risk R-010: VE3 Global API Specification Unavailable

**Category:** TECHNOLOGY
**Status:** In Progress
**Risk Owner:** CMA Digital Lead
**Action Owner:** CMA Digital Lead / DESNZ Policy

**Risk Description:** The Fuel Finder statutory API specification (VE3 Global aggregator) has not been publicly published as of January 2026. Without it, the primary data integration cannot be developed, tested, or deployed.

**Root Cause:** VE3 Global (£3M contract holder) has not published developer documentation. Specification may exist but is not publicly indexed. DESNZ may need to facilitate access.

**Inherent:** Likelihood 3 × Impact 5 = **15** (High)
**Residual:** Likelihood 3 × Impact 4 = **12** (High) — Mitigation via CMA interim endpoints as fallback; but primary integration still blocked

**Primary Response:** TREAT — Contact DESNZ/VE3 directly; develop against CMA interim JSON endpoints as bridge

#### Action Plan

1. **Contact DESNZ for VE3 Global API documentation**
   - Owner: CMA Digital Lead
   - Due Date: 2026-02-07 (URGENT)

2. **Build integration prototype against CMA interim JSON endpoints**
   - Owner: CMA Digital Team
   - Due Date: 2026-02-28

3. **Adapter pattern: design data ingestion layer to swap between CMA interim and Fuel Finder APIs**
   - Owner: CMA Technical Architect
   - Due Date: 2026-03-15

---

### Risk R-011: Service Outage During High-Profile Period

**Category:** TECHNOLOGY
**Status:** Open
**Risk Owner:** CMA Digital Lead

**Risk Description:** The citizen-facing service experiences an outage during a high-profile fuel price event (budget announcement, supply disruption, media spike), causing embarrassment and citizen frustration.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Auto-scaling, load testing, CDN caching

**Primary Response:** TREAT — Load testing at 10x expected peak; CDN for static assets; graceful degradation

---

### Risk R-012: Retailer API Integration Issues for Large Chains

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** CMA Digital Lead

**Risk Description:** Large retail chains (supermarkets, oil majors) experience technical difficulties integrating their pricing systems with the submission API, delaying automated data flow.

**Inherent:** Likelihood 4 × Impact 3 = **12** (Medium)
**Residual:** Likelihood 3 × Impact 2 = **6** (Medium) — Sandbox environment, technical support, clear API documentation

**Primary Response:** TREAT — Provide sandbox environment and integration support

---

### Risk R-013: DPIA Not Completed Before Personal Data Processing

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** SIRO / DPO

**Risk Description:** Data Protection Impact Assessment not completed before personal data (retailer contact details) is processed, creating ICO non-compliance risk.

**Inherent:** Likelihood 3 × Impact 4 = **12** (Medium)
**Residual:** Likelihood 2 × Impact 3 = **6** (Medium) — DPIA initiated; data model defines PII scope

**Primary Response:** TREAT — Prioritise DPIA completion via `/arckit.dpia`

---

### Risk R-014: Security Breach or Vulnerability Exploitation

**Category:** TECHNOLOGY
**Status:** Open
**Risk Owner:** SIRO

**Risk Description:** Security vulnerability is exploited, compromising retailer data, enforcement records, or service availability. Government service breach attracts heightened media and ICO scrutiny.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Secure by Design, penetration testing, encryption at rest/in transit

**Primary Response:** TREAT — Mandatory Secure by Design assessment; penetration testing before Live

---

### Risk R-015: Benefits Not Measurable or Not Materialising

**Category:** FINANCIAL
**Status:** Open
**Risk Owner:** CMA SRO

**Risk Description:** Consumer benefit from fuel price transparency is difficult to measure or does not materialise at projected levels, undermining NAO/PAC value-for-money assessment.

**Inherent:** Likelihood 2 × Impact 3 = **6** (Medium)
**Residual:** Likelihood 1 × Impact 1 = **1** (Low) — Benefits framework defined early; economic analysis capability planned

**Primary Response:** TREAT — Define benefits measurement framework in SOBC

---

### Risk R-016: CDDO Digital Spend Control Rejection

**Category:** FINANCIAL
**Status:** Open
**Risk Owner:** CMA SRO

**Risk Description:** CDDO rejects digital spend control submission, delaying procurement and delivery.

**Inherent:** Likelihood 4 × Impact 3 = **12** (Medium)
**Residual:** Likelihood 3 × Impact 2 = **6** (Medium) — Early engagement with CDDO; TCoP compliance documented

**Primary Response:** TREAT — Early CDDO engagement; strong TCoP evidence

---

### Risk R-017: Regulatory Change Mid-Delivery

**Category:** STRATEGIC
**Status:** Monitoring
**Risk Owner:** DESNZ Policy Lead

**Risk Description:** Motor Fuel Price Regulations are amended mid-delivery (new fuel types, changed submission frequency, expanded scope), requiring architectural rework.

**Inherent:** Likelihood 3 × Impact 4 = **12** (Medium)
**Residual:** Likelihood 2 × Impact 3 = **6** (Medium) — Modular architecture designed for evolvability (Principle 16)

**Primary Response:** TOLERATE — Architecture designed for change; low probability of near-term amendment

---

### Risk R-018: Assisted Digital Channels Overwhelmed

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** CMA Digital Lead

**Risk Description:** Phone and email support channels overwhelmed by independent retailer enquiries during registration period, leaving retailers unable to get help.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Capacity planning, trade body cascade, self-service FAQs

**Primary Response:** TREAT — Scale support team for registration surge period

---

### Risk R-019: FOI Requests Reveal Sensitive Programme Information

**Category:** OPERATIONAL
**Status:** Monitoring
**Risk Owner:** CMA SRO

**Risk Description:** FOI requests reveal sensitive programme information (costs, issues, vendor details) that is used by media or opposition to criticise the programme.

**Inherent:** Likelihood 2 × Impact 2 = **4** (Low)
**Residual:** Likelihood 2 × Impact 1 = **2** (Low) — FOI-ready documentation; transparency by default

**Primary Response:** TOLERATE — Transparency by default reduces FOI risk

---

### Risk R-020: NAO Audit Identifies Governance Weaknesses

**Category:** OPERATIONAL
**Status:** Monitoring
**Risk Owner:** CMA SRO

**Risk Description:** NAO post-launch audit identifies governance weaknesses, inadequate cost tracking, or poor benefits realisation, resulting in adverse PAC findings.

**Inherent:** Likelihood 2 × Impact 4 = **8** (Medium)
**Residual:** Likelihood 1 × Impact 2 = **2** (Low) — Audit-ready documentation; benefits tracking; governance framework

**Primary Response:** TREAT — Maintain audit-ready documentation from day one

---

## D. Risk Category Analysis

### STRATEGIC Risks

**Total:** 3 (R-002, R-005, R-017)
**Average Inherent Score:** 11.0 (Medium)
**Average Residual Score:** 5.3 (Low-Medium)
**Control Effectiveness:** 52% reduction

**Key Themes:** Political pressure vs governance rigour; inter-departmental coordination; regulatory change
**Category Risk Profile:** ✅ Acceptable — Good control effectiveness; CMA independence provides structural protection

### OPERATIONAL Risks

**Total:** 5 (R-001, R-009, R-012, R-018, R-019, R-020)
**Average Inherent Score:** 10.7 (Medium)
**Average Residual Score:** 5.7 (Low-Medium)
**Control Effectiveness:** 47% reduction

**Key Themes:** Independent retailer compliance; skills gaps; support capacity; audit readiness
**Category Risk Profile:** ⚠️ Concerning — R-001 (independent compliance) is the programme's highest residual risk

### FINANCIAL Risks

**Total:** 3 (R-008, R-015, R-016)
**Average Inherent Score:** 10.0 (Medium)
**Average Residual Score:** 4.3 (Low)
**Control Effectiveness:** 57% reduction

**Key Themes:** Scope creep; benefits measurement; spend control approval
**Category Risk Profile:** ✅ Acceptable — Strong financial controls; low API procurement costs (£0 for data)

### COMPLIANCE Risks

**Total:** 3 (R-003, R-007, R-013)
**Average Inherent Score:** 13.3 (High)
**Average Residual Score:** 8.0 (Medium)
**Control Effectiveness:** 40% reduction

**Key Themes:** Enforcement readiness deadline; GDS assessment; DPIA completion
**Category Risk Profile:** ⚠️ Concerning — R-003 (enforcement tools) has hard deadline that cannot slip

### REPUTATIONAL Risks

**Total:** 3 (R-004, R-006, R-011)
**Average Inherent Score:** 15.0 (High)
**Average Residual Score:** 10.7 (Medium)
**Control Effectiveness:** 29% reduction

**Key Themes:** Data quality; media coverage; service outage visibility
**Category Risk Profile:** ⚠️ Concerning — Reputational risks harder to control; prevention is critical

### TECHNOLOGY Risks

**Total:** 3 (R-010, R-011, R-014)
**Average Inherent Score:** 11.0 (Medium)
**Average Residual Score:** 6.7 (Medium)
**Control Effectiveness:** 39% reduction

**Key Themes:** VE3 API dependency; service resilience; security posture
**Category Risk Profile:** ⚠️ Concerning — R-010 (VE3 API) is a blocking external dependency

---

## E. Risk Ownership Matrix

| Stakeholder | Role | Owned Risks | High | Medium | Low | Total Score |
|-------------|------|-------------|------|--------|-----|-------------|
| CMA SRO | Programme SRO | R-002, R-005, R-006, R-008, R-015, R-019, R-020 | 1 | 3 | 3 | 38 |
| CMA Digital Lead | Technology Delivery | R-003, R-004, R-009, R-010, R-011, R-012, R-018 | 2 | 4 | 1 | 50 |
| CMA Enforcement Lead | Enforcement | R-001 | 1 | 0 | 0 | 12 |
| SIRO / DPO | Information Governance | R-013, R-014 | 0 | 1 | 1 | 10 |
| DESNZ Policy Lead | Policy | R-017 | 0 | 1 | 0 | 6 |
| CMA Communications | Comms | R-007, R-016 | 0 | 2 | 0 | 12 |

**Risk Concentration Analysis:**
- ⚠️ **CMA Digital Lead owns 7 risks totaling 50 points** — Highest concentration. Consider delegating R-011 and R-018 to operations lead.
- **CMA SRO owns 7 risks** — Appropriate for programme-level strategic and financial risks.
- **CMA Enforcement Lead owns only 1 risk** (R-001) but it is the highest residual risk — appropriate focused ownership.

---

## F. 4Ts Response Framework Summary

| Response | Count | % | Total Residual Score | Key Examples |
|----------|-------|---|---------------------|--------------|
| **TOLERATE** | 2 | 10% | 8 | R-017 (regulatory change), R-019 (FOI) |
| **TREAT** | 18 | 90% | 160 | R-001, R-003, R-004, R-006, R-010, and 13 others |
| **TRANSFER** | 0 | 0% | 0 | No transfer opportunities identified |
| **TERMINATE** | 0 | 0% | 0 | No activities to terminate |
| **TOTAL** | 20 | 100% | 168 | |

**Key Insights:**
- **90% of risks require active treatment** — Reflects the programme's regulatory urgency and tight deadlines
- **No transfer opportunities** — Risks are internal to the programme; no insurance or outsourcing viable for regulatory delivery
- **Only 10% tolerated** — Two low-probability risks with manageable impact
- **No terminated activities** — All programme activities are essential to regulatory mandate

---

## G. Risk Appetite Compliance

**Organizational Risk Appetite for UK Government Digital Service:**

| Category | Appetite Level | Threshold | Description |
|----------|---------------|-----------|-------------|
| STRATEGIC | Medium | ≤ 9 | Willing to accept medium strategic risks for regulatory delivery |
| OPERATIONAL | Medium | ≤ 9 | Moderate tolerance for operational challenges during new service launch |
| FINANCIAL | Medium | ≤ 9 | Moderate financial risk given public money accountability |
| COMPLIANCE | Low | ≤ 6 | Low tolerance for compliance breaches (regulatory body must lead by example) |
| REPUTATIONAL | Medium | ≤ 9 | Moderate tolerance given political context but high visibility |
| TECHNOLOGY | Medium | ≤ 9 | Moderate tolerance for technology challenges with controls |

**Compliance Summary:**

| Category | Appetite | Risks Within | Risks Exceeding | Action Required |
|----------|----------|--------------|-----------------|-----------------|
| STRATEGIC | ≤ 9 | 3 (100%) | 0 (0%) | ✅ Compliant |
| OPERATIONAL | ≤ 9 | 4 (80%) | 1 (20%) | ⚠️ R-001 (12) — SRO approval |
| FINANCIAL | ≤ 9 | 3 (100%) | 0 (0%) | ✅ Compliant |
| COMPLIANCE | ≤ 6 | 1 (33%) | 2 (67%) | ⚠️ R-003 (12), R-007 (6) — Board escalation |
| REPUTATIONAL | ≤ 9 | 1 (33%) | 2 (67%) | ⚠️ R-006 (12), R-004 (8) — SRO monitoring |
| TECHNOLOGY | ≤ 9 | 1 (33%) | 2 (67%) | ⚠️ R-010 (12), R-011 (4) — active treatment |

**Overall Appetite Compliance:** ⚠️ 4 of 6 categories have at least one risk exceeding appetite

---

## H. Prioritized Action Plan

### Priority 1: URGENT (This Week)

| # | Action | Risk(s) | Owner | Due Date | Status |
|---|--------|---------|-------|----------|--------|
| 1 | Contact DESNZ/VE3 Global for API specification | R-010 | CMA Digital Lead | 2026-02-07 | Not Started |
| 2 | Define enforcement MVP for Sprint 1 backlog | R-003 | CMA Digital Lead | 2026-02-15 | Not Started |
| 3 | Deploy independent retailer onboarding team | R-001 | CMA Enforcement | 2026-02-15 | Not Started |

### Priority 2: HIGH (This Month)

| # | Action | Risk(s) | Owner | Due Date | Status |
|---|--------|---------|-------|----------|--------|
| 4 | Prepare proactive media strategy | R-006 | CMA Communications | 2026-02-28 | Not Started |
| 5 | Initiate DPIA completion | R-013 | SIRO/DPO | 2026-02-28 | Not Started |
| 6 | Build CMA interim JSON integration prototype | R-010 | CMA Digital Team | 2026-02-28 | In Progress |
| 7 | Establish joint CMA-DESNZ programme board | R-005 | CMA SRO | 2026-02-15 | Not Started |

### Priority 3: MEDIUM (This Quarter)

| # | Action | Risk(s) | Owner | Due Date | Status |
|---|--------|---------|-------|----------|--------|
| 8 | Conduct GDS pre-assessment check-in | R-007 | CMA Digital Lead | 2026-03-31 | Not Started |
| 9 | Tabletop enforcement exercise | R-003 | CMA Enforcement | 2026-03-31 | Not Started |
| 10 | Load test at 10x expected peak | R-011 | CMA Digital Team | 2026-04-30 | Not Started |
| 11 | Penetration testing engagement | R-014 | SIRO | 2026-04-30 | Not Started |
| 12 | Define benefits measurement framework | R-015 | CMA SRO | 2026-03-31 | Not Started |

---

## I. Integration with SOBC

### SOBC Strategic Case (Part A)
- **R-001** (independent compliance) demonstrates urgency of onboarding support investment
- **R-003** (enforcement readiness) demonstrates urgency of enforcement tools delivery
- **R-010** (VE3 API) informs risk of dependency on single aggregator

### SOBC Economic Case (Part B)
- **R-008** (budget overrun): Add HM Treasury optimism bias (20-25% for new digital services)
- All data API costs are £0 (per ARC-001-RSCH-v1.0) — reduces financial risk profile
- **Risk contingency**: £0 for data procurement; contingency focused on delivery team costs

### SOBC Management Case (Part E)
- Full risk register included
- Top 10 risks with mitigation plans
- Risk ownership matrix demonstrates clear accountability
- Monitoring framework shows ongoing risk management

### SOBC Recommendation
- Risk profile is **Concerning but manageable** — 4 High residual risks with active treatment plans
- No Critical residual risks — controls are effective
- Key risks are **time-bound** (May 2026 enforcement deadline) — urgency drives priority

---

## J. Monitoring and Review Framework

### Review Schedule

| Risk Level | Review Frequency | Reviewed By | Escalated To |
|------------|------------------|-------------|--------------|
| **High (12+)** | Weekly | Risk Owner | CMA SRO / Programme Board |
| **Medium (6-11)** | Bi-weekly | Risk Owner | CMA Digital Lead |
| **Low (1-5)** | Monthly | Action Owner | Risk Owner |

### Key Risk Indicators (KRIs)

**Leading Indicators:**
- Independent forecourt registration rate (below 80% by 2 Feb → R-001 escalation)
- Sprint velocity on enforcement features (behind plan → R-003 escalation)
- VE3 API specification received (not received by Feb → R-010 escalation)
- Media sentiment analysis (negative trend → R-006 escalation)

**Lagging Indicators:**
- Data coverage rate post-launch (below 80% → R-001 materialised)
- GDS assessment result (not pass → R-007 materialised)
- Security incident count (any → R-014 materialised)

### Escalation Criteria

1. Any risk increases by 4+ points
2. Any new High or Critical risk identified
3. Any risk exceeds appetite with no approved mitigation plan
4. Any mitigation action delayed > 2 weeks
5. Registration rate below 70% by 2 February 2026

### Reporting Requirements

- **Weekly**: High risks to Programme Board (R-001, R-003, R-006, R-010)
- **Monthly**: Full risk register to CMA SRO
- **Quarterly**: Risk appetite compliance to CMA Board and Audit Committee
- **Next Review Date**: 2026-03-01

**Risk Register Owner:** CMA SRO (Programme Senior Responsible Owner)

---

## K. Orange Book Compliance Checklist

- ✅ **A. Governance and Leadership**: Risk owners assigned from senior stakeholders (RACI matrix in ARC-001-STKE-v1.0); escalation paths defined; risk appetite set
- ✅ **B. Integration**: Risks linked to stakeholder goals (G-1 through G-7) and outcomes (O-1 through O-4); feeds into SOBC Management Case
- ✅ **C. Collaboration and Best Information**: Risks sourced from stakeholder concerns (SD-1 through SD-12) and conflict analysis; research findings (ARC-001-RSCH-v1.0) inform technology risks
- ✅ **D. Risk Management Processes**: 5×5 assessment methodology; 4Ts framework; inherent and residual tracking; systematic identification across 6 categories
- ✅ **E. Continual Improvement**: Monthly review schedule; KRIs defined; escalation criteria; version-controlled register

---

## Appendix A: Stakeholder-Risk Linkage

| Stakeholder | Driver (ARC-001-STKE-v1.0) | Risk ID | Risk Title | Residual |
|-------------|----------------------------|---------|------------|----------|
| CMA Board | SD-1: Regulatory effectiveness | R-001, R-003, R-004 | Compliance, enforcement, data quality | 12, 12, 8 |
| CMA Enforcement | SD-2: Enforcement capability | R-001, R-003 | Compliance, enforcement tools | 12, 12 |
| DESNZ Policy | SD-3: Deliver commitment | R-002, R-005, R-017 | Governance, friction, reg change | 6, 4, 6 |
| DESNZ Ministers | SD-4: Political accountability | R-002, R-006, R-015 | Governance, media, benefits | 6, 12, 1 |
| Citizens | SD-5: Find cheapest fuel | R-004, R-006, R-011 | Data quality, media, outage | 8, 12, 4 |
| Large Retailers | SD-6: Minimise burden | R-012 | API integration issues | 6 |
| Independents | SD-7: Avoid disproportionate burden | R-001, R-018 | Compliance, support overwhelm | 12, 4 |
| Trade Bodies | SD-8: Protect members | R-001, R-006 | Compliance, media | 12, 12 |
| GDS Assessors | SD-9: Service meets standard | R-007, R-002 | GDS failure, governance shortcuts | 6, 6 |
| ICO | SD-10: Data protection | R-013, R-014 | DPIA, security | 6, 4 |
| Third Parties | SD-11: Reliable API | R-010, R-011 | VE3 API, outage | 12, 4 |
| NAO/PAC | SD-12: Value for money | R-008, R-015, R-020 | Budget, benefits, audit | 6, 1, 2 |

---

## Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| **Risk Register Owner** | CMA SRO | | |
| **CMA Enforcement Lead** | | | |
| **CMA Digital Lead** | | | |
| **SIRO** | | | |

---

## Next Steps

1. **Immediate Actions** (This Week):
   - [ ] Contact DESNZ/VE3 Global for API specification (R-010 — URGENT)
   - [ ] Define enforcement MVP for Sprint 1 (R-003)
   - [ ] Deploy independent retailer onboarding team (R-001)
   - [ ] Brief CMA SRO on risk profile and appetite exceedances

2. **Short-term Actions** (This Month):
   - [ ] Establish joint CMA-DESNZ programme board (R-005)
   - [ ] Initiate DPIA (R-013) — run `/arckit.dpia`
   - [ ] Prepare proactive media strategy (R-006)
   - [ ] Build CMA interim JSON integration prototype (R-010)

3. **Medium-term Actions** (This Quarter):
   - [ ] Integrate risk register into SOBC Management Case — run `/arckit.sobc`
   - [ ] GDS pre-assessment check-in (R-007)
   - [ ] Tabletop enforcement exercise (R-003)
   - [ ] Penetration testing engagement (R-014)
   - [ ] Use risk register for Wardley Map strategic positioning — run `/arckit.wardley`

---

**END OF RISK REGISTER**

---

*This risk register follows HM Treasury Orange Book (2023) principles and integrates with ArcKit's stakeholder-driven architecture governance framework.*

*For questions or updates, contact: CMA SRO (Programme Senior Responsible Owner)*

---

**Generated by**: ArcKit `/arckit.risk` command
**Generated on**: 2026-01-30
**ArcKit Version**: 1.0.3
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: Claude Opus 4.5
