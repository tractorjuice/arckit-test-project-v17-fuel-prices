# Risk Register: UK Fuel Price Transparency Service

> **Template Status**: Live | **Version**: 1.0.3 | **Command**: `/arckit.risk`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RISK-v2.0 |
| **Document Type** | Risk Register |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | ACTIVE |
| **Version** | 2.0 |
| **Created Date** | 2026-01-30 |
| **Last Modified** | 2026-04-06 |
| **Review Cycle** | Monthly |
| **Next Review Date** | 2026-05-06 |
| **Owner** | CMA Senior Responsible Owner (SRO) |
| **Reviewed By** | CMA SRO, SIRO/DPO |
| **Approved By** | PENDING |
| **Distribution** | CMA Board, CMA SRO, DESNZ Policy, CMA Enforcement, CMA Digital, Programme Board, VE3 Global (liaison) |
| **Supersedes** | ARC-001-RISK-v1.0 (2026-01-30) |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-30 | ArcKit AI | Initial creation from `/arckit.risk` command | PENDING | PENDING |
| 2.0 | 2026-04-06 | ArcKit AI | VE3 API architecture pivot update: R-010 and R-013 closed; R-001, R-003, R-004, R-012, R-014 updated for new architecture; R-021, R-022, R-023 added from DPIA v2.0 and vendor dependency analysis | PENDING | PENDING |

---

## Architecture Change Notice

> **IMPORTANT — ARCHITECTURE PIVOT (Jan–Apr 2026)**
>
> Between v1.0 (January 2026) and v2.0 (April 2026) the CMA service architecture changed materially. The original design assumed CMA would build and operate data ingestion infrastructure, receive submissions directly from ~8,500 fuel retailers, and store retailer contact data (PII) in a CMA-managed database.
>
> Under the revised architecture, the CMA **consumes** the VE3 Global Fuel Finder Public API. Key changes:
> - **VE3 Fuel Finder API is live** (went live early 2026, CMA has access)
> - **Organisation entity REMOVED** — CMA stores zero retailer PII (contact_name, email, phone managed by VE3 Global under DESNZ contract)
> - CMA syncs data from VE3 API every 15 minutes; enriches with PostGIS geospatial indexing
> - Data model reduced to 8 entities: Forecourt, CurrentPrice, PriceHistory, ComplianceRecord, EnforcementAction, AuditEvent, ApiSyncState, FuelType
> - **DPIA v2.0** (ARC-001-DPIA-v2.0) completed — residual risk LOW; no retailer PII in CMA DB
> - **Requirements v3.0** (ARC-001-REQ-v3.0) generated — 56 requirements reflecting VE3 API-consumer model
>
> Several v1.0 risks are now closed, several are reframed, and three new risks emerge from this architecture.

---

## Executive Summary

### Risk Profile Overview

**Total Risks in Register:** 23 (21 active, 2 closed)

| Risk Level | Inherent (active) | Residual (active) | Change |
|------------|-------------------|-------------------|--------|
| **Critical** (20-25) | 2 | 0 | ↓ 100% |
| **High** (13-19) | 4 | 0 | ↓ 100% |
| **Medium** (6-12) | 12 | 11 | ↓ 8% (absorption from higher tiers) |
| **Low** (1-5) | 3 | 10 | ↑ (absorption from higher tiers) |
| **TOTAL Active Score** | 228 | 115 | ↓ 50% |

**Closed Risks (not in totals above):** R-010 (VE3 API specification — now live), R-013 (DPIA — completed)

### Risk Category Distribution

| Category | Count (active) | Avg Inherent | Avg Residual | Control Effectiveness |
|----------|---------------|--------------|--------------|----------------------|
| **STRATEGIC** | 3 | 10.7 | 4.7 | 56% reduction |
| **OPERATIONAL** | 5 | 10.8 | 4.4 | 59% reduction |
| **FINANCIAL** | 3 | 8.7 | 3.0 | 66% reduction |
| **COMPLIANCE** | 2 | 14.0 | 8.0 | 43% reduction |
| **REPUTATIONAL** | 3 | 14.7 | 7.3 | 50% reduction |
| **TECHNOLOGY** | 5 | 8.8 | 4.4 | 50% reduction |

### Overall Risk Assessment

**Overall Residual Risk Score (active):** 115/525
**Risk Reduction from Controls:** 50% reduction from inherent risk
**Risk Profile Status:** MANAGEABLE — No High or Critical residual risks; two Medium risks (R-003, R-006) require active management near the May 2026 enforcement deadline

### Risks Exceeding Appetite

**Number of risks exceeding organizational appetite (active):** 3 risks

| Risk ID | Title | Category | Score | Appetite | Excess | Escalation |
|---------|-------|----------|-------|----------|--------|------------|
| R-003 | Enforcement tools not ready by May 2026 | COMPLIANCE | 12 | ≤ 6 | +6 | CMA Board — URGENT deadline |
| R-006 | Negative media coverage undermines adoption | REPUTATIONAL | 12 | ≤ 9 | +3 | DESNZ Ministers briefed |
| R-022 | CMA-VE3 data controller relationship not formalised | COMPLIANCE | 9 | ≤ 6 | +3 | CMA Legal / DESNZ escalation |

> **Note (vs v1.0):** R-001 no longer exceeds appetite (reduced from 12 to 9 following substantial registration progress). R-010 closed. R-013 closed. Three appetite exceedances remain; two require immediate action before May 2026.

### Top 5 Risks Requiring Immediate Attention

1. **R-003** (COMPLIANCE, Medium 12): Enforcement tools not ready by May 2026 — Owner: CMA Digital Lead — **URGENT: 4 weeks to enforcement deadline**
2. **R-006** (REPUTATIONAL, Medium 12): Negative media coverage undermines citizen adoption — Owner: CMA SRO
3. **R-001** (OPERATIONAL, Medium 9): Low independent retailer compliance — Owner: CMA Enforcement Lead — improving but not resolved
4. **R-022** (COMPLIANCE, Medium 9): CMA-VE3 data controller relationship not formalised — Owner: CMA Legal / SIRO
5. **R-021** (TECHNOLOGY, Medium 6): VE3 Global platform single point of failure — Owner: CMA Digital Lead

### Key Findings and Recommendations

**Key Findings:**
- **Architecture pivot has substantially improved the risk profile**: Removing direct retailer ingestion eliminates R-010 (VE3 API spec) and R-013 (DPIA), reduces R-001, R-004, and R-014 significantly, and shifts R-012 from a complex multi-retailer integration problem to a single CMA-to-VE3 API integration.
- **VE3 dependency is now the primary technology risk** (R-021): CMA has zero data without VE3. Caching mitigates outage risk, but a prolonged VE3 outage would render the citizen service stale. A 15-minute sync cycle provides reasonable data freshness but creates a single point of failure.
- **Enforcement deadline is imminent** (R-003): Grace period ends approximately May 2026. This is approximately 4 weeks away and is the highest-priority delivery risk.
- **Legal relationship with VE3 not formalised** (R-022): No data sharing or processing agreement yet governs the CMA-VE3-DESNZ relationship. ICO would expect this to be documented given VE3 holds retailer PII on DESNZ's behalf and supplies derived data to CMA.
- **Retailer registration substantially achieved**: The February 2026 deadline has passed and registration rates are strong. R-001 has improved from residual 12 to residual 9 but is not closed — ongoing compliance monitoring is required.
- **No Critical or High residual risks remain**: All active residual risks are Medium or Low — a significant improvement from v1.0's 4 High residual risks.

**Recommendations:**
1. **URGENT**: Finalise enforcement tools delivery — R-003 deadline is May 2026 (approx. 4 weeks)
2. **HIGH**: Formalise CMA-VE3 data sharing/controller agreement via DESNZ (R-022)
3. **HIGH**: Implement VE3 API resilience pattern — cache layer, stale-data TTL policy, fallback display (R-021)
4. **MEDIUM**: Continue independent retailer compliance monitoring post-registration (R-001)
5. **MEDIUM**: Activate proactive media strategy for service launch (R-006)

---

## A. Risk Matrix Visualization

### Inherent Risk Matrix (Before Controls) — Active Risks Only

```
                                    IMPACT
              1-Minimal   2-Minor    3-Moderate   4-Major    5-Severe
           ┌───────────┬───────────┬───────────┬───────────┬───────────┐
5-Almost   │           │           │           │  R-001    │           │
Certain    │    5      │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │  R-016    │  R-003    │  R-004    │
           │    4      │    8      │    16     │    16     │    20     │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 3-Possible│          │           │  R-009    │  R-002    │  R-006    │
K          │    3      │    6      │  R-011    │  R-007    │           │
E          │           │           │  R-018    │  R-008    │           │
L          │           │           │  R-022    │  R-017    │           │
I          │           │           │  R-021    │           │           │
H          ├───────────┼───────────┼───────────┼───────────┼───────────┤
O 2-Unlikely│          │  R-019    │  R-012    │  R-014    │           │
O          │    2      │    4      │    6      │    8      │    10     │
D          │           │           │  R-015    │  R-020    │           │
           │           │           │  R-023    │           │           │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
  1-Rare   │           │           │           │           │           │
           │    1      │    2      │    3      │    4      │    5      │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: Critical (20-25)  High (13-19)  Medium (6-12)  Low (1-5)
Note: R-005 (Inherent L3×I3=9) shown at 3-Possible/3-Moderate; not displayed above to avoid overcrowding
```

### Residual Risk Matrix (After Controls) — Active Risks Only

```
                                    IMPACT
              1-Minimal   2-Minor    3-Moderate   4-Major    5-Severe
           ┌───────────┬───────────┬───────────┬───────────┬───────────┤
5-Almost   │           │           │           │           │           │
Certain    │    5      │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │           │           │           │
           │    4      │    8      │    12     │    16     │    20     │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 3-Possible│          │  R-016    │  R-001    │           │           │
K          │    3      │  R-017    │  R-003    │           │           │
E          │           │    6      │  R-006    │           │           │
L          │           │           │  R-022    │           │           │
I          │           │           │    9/12   │           │           │
H          ├───────────┼───────────┼───────────┼───────────┼───────────┤
O 2-Unlikely│ R-019    │  R-002    │           │  R-004    │           │
O          │  R-020    │  R-005    │    6      │    8      │    10     │
D          │  R-023    │  R-007    │           │           │           │
           │    2      │  R-008    │           │           │           │
           │           │  R-009    │           │           │           │
           │           │  R-011    │           │           │           │
           │           │  R-012    │           │           │           │
           │           │  R-014    │           │           │           │
           │           │  R-018    │           │           │           │
           │           │  R-021    │           │           │           │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
  1-Rare   │  R-015    │           │           │           │           │
           │    1      │    2      │    3      │    4      │    5      │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: Critical (20-25)  High (13-19)  Medium (6-12)  Low (1-5)
Residual placement: R-003 at L3×I4=12; R-006 at L3×I4=12; R-001 at L3×I3=9; R-022 at L3×I3=9
```

**Risk Movement Analysis (v1.0 → v2.0):**
- **0 Critical residual risks** (unchanged from v1.0 — no critical risks survived controls)
- **0 High residual risks** (↓ from 4 in v1.0): R-001 improved to Medium 9; R-010 closed; R-006 unchanged at 12 (still Medium)
- **11 Medium residual risks**: Stable overall; new R-021, R-022 added; R-004 improved from 8 to 6
- **10 Low residual risks**: Increased from 4 in v1.0 — reflects architecture simplification
- **2 Closed risks**: R-010 (VE3 API specification — now live), R-013 (DPIA — completed with LOW residual)

---

## B. Top 10 Risks (Ranked by Residual Score)

| Rank | ID | Title | Category | Inherent | Residual | Owner | Status | Response |
|------|----|-------|----------|----------|----------|-------|--------|----------|
| 1 | R-003 | Enforcement tools not ready by May 2026 | COMPLIANCE | 16 | 12 | CMA Digital Lead | **URGENT** | Treat |
| 2 | R-006 | Negative media coverage undermines adoption | REPUTATIONAL | 16 | 12 | CMA SRO | Open | Treat |
| 3 | R-001 | Low independent retailer compliance | OPERATIONAL | 20 | 9 | CMA Enforcement Lead | Improving | Treat |
| 4 | R-022 | CMA-VE3 data controller relationship not formalised | COMPLIANCE | 12 | 9 | SIRO / CMA Legal | **Open** | Treat |
| 5 | R-002 | Ministerial pressure compromises governance | STRATEGIC | 12 | 6 | CMA SRO | Monitoring | Treat |
| 6 | R-004 | Data quality too low for citizen trust | REPUTATIONAL | 16 | 6 | CMA Digital Lead | In Progress | Treat |
| 7 | R-007 | GDS Service Standard assessment failure | COMPLIANCE | 12 | 6 | CMA Digital Lead | In Progress | Treat |
| 8 | R-008 | Budget overrun due to scope creep | FINANCIAL | 12 | 6 | CMA SRO | Monitoring | Treat |
| 9 | R-016 | CDDO Digital Spend Control rejection | FINANCIAL | 12 | 6 | CMA SRO | Open | Treat |
| 10 | R-017 | Regulatory change mid-delivery | STRATEGIC | 12 | 6 | DESNZ Policy Lead | Monitoring | Tolerate |

---

## C. Detailed Risk Register

---

### Risk R-001: Low Independent Retailer Compliance

**Category:** OPERATIONAL
**Status:** Improving (substantially better than v1.0; not yet closed)
**Risk Owner:** CMA Enforcement Division Lead
**Action Owner:** CMA Digital Lead (compliance monitoring tools)

> **v2.0 Change:** Residual score reduced from **12 → 9**. Registration deadline (2 Feb 2026) has passed and independent forecourt registration is substantially achieved. The VE3 platform now handles retailer registration management — CMA monitors compliance via VE3 API data rather than direct submission tracking. Risk is no longer about registration but about ongoing submission frequency and data accuracy for the ~8,500 registered sites.

#### Risk Identification

**Risk Description:**
Independent forecourt operators continue to submit stale, inaccurate, or missing fuel price data despite having registered. Data quality and submission frequency from smaller independent operators remains variable, undermining data comprehensiveness and citizen trust. VE3 Global manages retailer registrations and API keys; CMA's enforcement exposure is now to ongoing non-compliance rather than registration failure.

**Root Cause:**
Registration substantially achieved but ongoing compliance requires continued effort from ~4,000 independent operators with limited digital capability. VE3 platform reduces the technical barrier but does not eliminate operational compliance risk.

**Trigger Events:**
- Data freshness analysis reveals ≥15% of independent forecourts are submitting data with staleness > 24 hours
- CMA compliance monitoring dashboard flags systemic non-submission by identifiable operator groups
- Trade body reports member confusion about submission frequency requirements post-grace period

**Consequences if Realized:**
- Data coverage degraded in rural/independent-heavy areas undermining citizen service quality
- CMA enforcement actions required at scale — resourcing risk
- Data quality below 80% freshness threshold triggers media interest

**Affected Stakeholders:**
- **Citizens (SD-5)**: Incomplete or stale data, especially in independent-heavy areas
- **CMA Enforcement (SD-2)**: Enforcement workload if compliance rates fall
- **Independent Retailers (SD-7)**: Risk of post-grace-period enforcement penalties
- **CMA Board (SD-1)**: Scheme effectiveness undermined if coverage rates fall

**Related Objectives:**
- Goal G-1 (Universal Registration): Substantially achieved — risk now about ongoing compliance
- Goal G-2 (Submission Compliance): Active risk — freshness and accuracy monitoring required
- Outcome O-1 (Comprehensive Transparency): Partially achieved; sustained compliance required

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 5 - Almost Certain | Historical precedent: sustained compliance harder than initial registration for low-capability operators |
| **Impact** | 4 - Major | ~4,000 independent sites = ~47% of all forecourts; poor compliance degrades citizen service |
| **Inherent Risk Score** | **20** (Critical) | 5 × 4 = 20 |

#### Current Controls and Mitigations

1. **VE3 platform manages retailer registration and API credentials**
   - Owner: VE3 Global (DESNZ contract)
   - Effectiveness: **Strong**
   - Evidence: VE3 Fuel Finder API live; retailer management delegated to VE3

2. **CMA compliance monitoring dashboard — flags non-submitting forecourts**
   - Owner: CMA Digital Team
   - Effectiveness: **Adequate**
   - Evidence: ARC-001-REQ-v3.0 NFR-C-001 through NFR-C-003; planned for MVP

3. **Enforcement grace period ended May 2026 — enforcement powers now active**
   - Owner: CMA Enforcement
   - Effectiveness: **Strong**
   - Evidence: Post-grace-period: enforcement credible deterrent

4. **Trade body partnership maintained (PRA, UKPIA)**
   - Owner: CMA Communications
   - Effectiveness: **Adequate**
   - Evidence: Ongoing communication channel for member guidance

**Overall Control Effectiveness:** Good (reduces from 20 to 9)

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | VE3 platform lowers barrier; most large chains fully compliant; risk concentrated in long-tail independents |
| **Impact** | 3 - Moderate | Impact reduced vs v1.0: VE3 handles registration, CMA monitors trends; CMA enforcement can act post-grace period |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Risk Response (4Ts Framework)

**Primary Response:** TREAT (Mitigate/Reduce)

**Rationale:** Risk reduced from High (12) to Medium (9) following registration achievement and VE3 platform delegation. Ongoing treatment via compliance monitoring tools and targeted enforcement.

#### Action Plan

1. **Operationalise compliance monitoring dashboard with automated alerting**
   - Owner: CMA Digital Lead
   - Due Date: 2026-04-30
   - Expected Impact: Real-time visibility of non-compliance by forecourt

2. **Define enforcement escalation threshold for post-grace-period non-compliance**
   - Owner: CMA Enforcement Lead
   - Due Date: 2026-05-07
   - Expected Impact: Clear trigger for enforcement action

3. **Monthly compliance rate reporting to CMA Board**
   - Owner: CMA SRO
   - Due Date: Ongoing from 2026-05-01
   - Expected Impact: Board visibility; sustained accountability

**Target Residual Risk:** 6 (Medium) — Likelihood 2, Impact 3 — achievable once enforcement establishes deterrent effect

---

### Risk R-002: Ministerial Pressure Compromises Governance

**Category:** STRATEGIC
**Status:** Monitoring
**Risk Owner:** CMA SRO
**Action Owner:** CMA Digital Lead

> **v2.0 Change:** No change to scores or controls. Monitoring status maintained.

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
- **GDS Assessors (SD-9)**: Failed assessment
- **Citizens (SD-5)**: Poor service quality

**Related Objectives:** G-7 (GDS assessment), G-3 (citizen service quality), O-4 (governance compliance)

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Fuel prices politically sensitive; ministerial attention is likely |
| **Impact** | 4 - Major | GDS assessment failure causes significant delay; security incident could be career-ending for SRO |
| **Inherent Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Current Controls

1. **CMA statutory independence from ministerial direction on enforcement** — Effectiveness: **Strong**
2. **Established GDS phase gate process with pre-assessment check-ins** — Effectiveness: **Adequate**
3. **Regular ministerial briefings showing progress within governance** — Effectiveness: **Adequate**

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
**Status:** URGENT
**Risk Owner:** CMA Digital Lead
**Action Owner:** CMA Digital Lead

> **v2.0 Change:** No change to scores. This risk is **escalating** as the May 2026 grace period end is now approximately 4 weeks away. Enforcement tools must be operational; any slip now directly threatens the regulatory scheme.

#### Risk Identification

**Risk Description:**
The enforcement tools (compliance dashboard, evidence export, enforcement case workflow, ComplianceRecord and EnforcementAction entity population) are not operational before the grace period ends in early May 2026. CMA cannot detect or act on non-compliance, destroying regulatory credibility.

**Root Cause:** Enforcement tools may be deprioritised in favour of citizen-facing features and retailer onboarding. The May 2026 deadline is fixed by legislation and cannot slip. VE3 API architecture change requires enforcement tools to consume VE3 data via the 15-minute sync rather than direct submission tracking — integration pattern has changed.

**Trigger Events:**
- Sprint velocity on enforcement features falls below plan
- VE3 API data quality issues delay ComplianceRecord population
- Legal review of evidence admissibility requirements raises new constraints
- Integration between CMA enforcement tools and VE3 ApiSyncState not completed

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
| **Likelihood** | 4 - Likely | Common pattern: enforcement features deprioritised; VE3 API architecture change adds integration complexity |
| **Impact** | 4 - Major | Regulatory scheme without enforcement is toothless; CMA credibility at stake |
| **Inherent Risk Score** | **16** (High) | 4 × 4 = 16 |

#### Current Controls

1. **Enforcement features included in MVP scope — not deferrable** — Effectiveness: **Adequate**
2. **CMA Enforcement co-designing ComplianceRecord and EnforcementAction entities (REQ v3.0)** — Effectiveness: **Strong**
3. **Weekly enforcement readiness milestone tracking** — Effectiveness: **Adequate**
4. **VE3 API live — removes blocker that existed in v1.0** — Effectiveness: **Strong**

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | VE3 API live removes key blocker; delivery risk remains due to proximity of deadline |
| **Impact** | 4 - Major | Impact unchanged — hard deadline means no recovery time |
| **Residual Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Risk Response (4Ts Framework)

**Primary Response:** TREAT — Treat as programme critical path item; enforce no-slip milestone

#### Action Plan

1. **Daily enforcement readiness stand-up from 2026-04-07**
   - Owner: CMA Digital Lead
   - Due Date: Ongoing until 2026-05-01
   - Expected Impact: Early warning if delivery is slipping

2. **Enforce feature-complete milestone for enforcement tools by 2026-04-20**
   - Owner: CMA Digital Lead
   - Due Date: 2026-04-20
   - Expected Impact: Two-week test buffer before grace period ends

3. **Conduct tabletop enforcement exercise with CMA Enforcement team**
   - Owner: CMA Enforcement Lead
   - Due Date: 2026-04-25
   - Expected Impact: Validate tool completeness and admissibility of evidence

4. **Obtain CMA legal sign-off on enforcement evidence trail (AuditEvent linkage)**
   - Owner: CMA Legal / SIRO
   - Due Date: 2026-04-22
   - Expected Impact: Legal admissibility confirmed before go-live

**Target Residual Risk:** 8 (Medium) — Likelihood 2, Impact 4 — if feature-complete milestone met

---

### Risk R-004: Data Quality Too Low for Citizen Trust

**Category:** REPUTATIONAL
**Status:** In Progress
**Risk Owner:** CMA Digital Lead
**Action Owner:** CMA Digital Team

> **v2.0 Change:** Residual score reduced from **8 → 6**. Architecture pivot means VE3 Global, not CMA, is responsible for retailer data ingestion and initial validation. CMA's quality role is now enrichment (PostGIS geospatial indexing, anomaly detection, freshness scoring) rather than raw ingestion validation. This significantly reduces the likelihood that CMA systems introduce data quality degradation, though VE3 pipeline quality is now a dependency (see R-021).

#### Risk Identification

**Risk Description:**
Published fuel prices are frequently inaccurate, stale, or geospatially incorrect, causing citizens to lose trust. Media reports "government fuel price tool shows wrong prices" or "nearest petrol station location is wrong."

**Root Cause (updated):** VE3 API data may carry quality issues upstream of CMA (retailer submission errors, VE3 ingestion errors). CMA enrichment layer (PostGIS, anomaly detection) may introduce geospatial errors if mapping data is outdated. Freshness indicator accuracy depends on 15-minute sync reliability.

**Trigger Events:**
- VE3 API returns price data with systematic outliers (e.g., £0.00 or £9.99 per litre)
- Geospatial enrichment maps forecourts to wrong postcode sector
- CMA-VE3 sync drops, serving stale data beyond acceptable TTL to citizens

**Consequences if Realized:**
- Citizens receive incorrect prices or directions; trust lost
- Media: "Government fuel tool shows wrong prices — is it broken?"
- CMA reputation damaged despite the error originating in VE3 pipeline

**Affected Stakeholders:**
- **Citizens (SD-5)**: Incorrect information causes poor decisions
- **CMA Board (SD-1)**: Reputational damage even if root cause is upstream
- **DESNZ Ministers (SD-4)**: Parliamentary embarrassment

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | VE3 pipeline quality not directly controllable by CMA; geospatial enrichment is complex |
| **Impact** | 4 - Major | Data quality failures undermine entire scheme purpose |
| **Inherent Risk Score** | **16** (High) | 4 × 4 = 16 |

#### Current Controls

1. **CMA anomaly detection layer — flags statistical outliers before publish** — Effectiveness: **Adequate**
2. **Data quality scoring per CurrentPrice entity (REQ v3.0 NFR-D-003)** — Effectiveness: **Adequate**
3. **Freshness indicator visible to citizen — transparent about data age** — Effectiveness: **Strong**
4. **VE3 API is live with established data pipeline** — Effectiveness: **Adequate**
5. **SLA expectation via DESNZ-VE3 contract for data quality** — Effectiveness: **Adequate**

**Overall Control Effectiveness:** Good (reduces from 16 to 6)

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Anomaly detection and VE3 contract quality standards reduce quality incidents |
| **Impact** | 3 - Moderate | Impact reduced from v1.0: CMA controls enrichment layer; freshness indicators set expectations |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

**Primary Response:** TREAT — CMA anomaly detection, freshness indicators, and quality scoring layer

---

### Risk R-005: CMA-DESNZ Inter-departmental Friction

**Category:** STRATEGIC
**Status:** Monitoring
**Risk Owner:** CMA SRO

> **v2.0 Change:** No change to scores. VE3 API architecture adds a third party (VE3 Global) to the inter-departmental relationship, slightly increasing coordination complexity, but DESNZ-VE3 contract management is DESNZ's responsibility.

**Risk Description:** CMA (enforcement body) and DESNZ (policy owner and VE3 contract holder) have different priorities, timelines, or views on implementation, causing delays or conflicting messaging. VE3 API architecture adds a further dimension: CMA may need DESNZ to raise service quality issues with VE3 on CMA's behalf.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Joint programme board and MoU established

**Primary Response:** TREAT — Joint CMA-DESNZ programme board; CMA escalation path for VE3 issues via DESNZ

---

### Risk R-006: Negative Media Coverage Undermines Citizen Adoption

**Category:** REPUTATIONAL
**Status:** Open
**Risk Owner:** CMA SRO
**Action Owner:** CMA Communications

> **v2.0 Change:** No change to scores. Risk profile unchanged; proactive media strategy must be activated ahead of service launch.

**Risk Description:** Trade body opposition, service launch issues, data quality problems, or VE3 platform outages generate negative media coverage that undermines public confidence and citizen adoption.

**Root Cause (updated):** Additional trigger point vs v1.0: VE3 platform downtime resulting in stale CMA data becoming visible to media.

**Inherent:** Likelihood 4 × Impact 4 = **16** (High)
**Residual:** Likelihood 3 × Impact 4 = **12** (Medium) — Proactive media strategy reduces likelihood; impact remains high for government service

**Primary Response:** TREAT — Proactive positive narrative; rapid response protocol; ministerial engagement

---

### Risk R-007: GDS Service Standard Assessment Failure

**Category:** COMPLIANCE
**Status:** In Progress
**Risk Owner:** CMA Digital Lead

> **v2.0 Change:** No change to scores. Architecture pivot (consumer model) may make some GDS points easier to meet (simpler data model, no complex submission infrastructure) but user research requirements are unchanged.

**Risk Description:** Service fails GDS assessment at Alpha or Beta phase, blocking progression.

**Inherent:** Likelihood 3 × Impact 4 = **12** (Medium)
**Residual:** Likelihood 2 × Impact 3 = **6** (Medium) — Pre-assessment check-ins and multidisciplinary team

**Primary Response:** TREAT — Pre-assessment GDS engagement; self-assessment at each sprint

---

### Risk R-008: Budget Overrun Due to Scope Creep

**Category:** FINANCIAL
**Status:** Monitoring
**Risk Owner:** CMA SRO

> **v2.0 Change:** No change to scores. VE3 API consumer model may reduce development costs (no ingestion infrastructure to build) but VE3 API integration development and PostGIS geospatial enrichment add complexity.

**Risk Description:** Programme costs exceed approved budget due to scope creep, unplanned VE3 API integration requirements, or cloud infrastructure cost overruns.

**Inherent:** Likelihood 3 × Impact 4 = **12** (Medium)
**Residual:** Likelihood 2 × Impact 3 = **6** (Medium) — Agile delivery; monthly FinOps reviews; VE3 consumer model reduces development scope

**Primary Response:** TREAT — Strict scope control; monthly FinOps reviews

---

### Risk R-009: Insufficient Cloud/DevOps Expertise

**Category:** OPERATIONAL
**Status:** In Progress
**Risk Owner:** CMA Digital Lead

> **v2.0 Change:** No change to scores. PostGIS geospatial indexing adds a specialist skill requirement (spatial databases, coordinate system management) not present in v1.0. Partially offset by reduced ingestion infrastructure complexity.

**Risk Description:** CMA Digital team lacks sufficient cloud architecture, PostGIS geospatial, and DevOps expertise to build and operate the enrichment and caching service at required quality.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Contractor/consultancy support; PostGIS expertise procurement

**Primary Response:** TREAT — Augment team with specialist contractors including PostGIS/geospatial expertise

---

### Risk R-010: VE3 Global API Specification Unavailable — CLOSED

**Category:** TECHNOLOGY
**Status:** **CLOSED** (2026-04-06)
**Risk Owner:** CMA Digital Lead

> **CLOSED:** VE3 Fuel Finder API went live in early 2026. CMA has access to the API and documentation. The primary data integration blocker identified in v1.0 has been resolved. This risk is closed with **residual score 0**.

**Original Description (v1.0):** The Fuel Finder statutory API specification (VE3 Global aggregator) had not been publicly published as of January 2026.

**Closure Rationale:** VE3 Fuel Finder Public API is now live and accessible. CMA Digital team has obtained API credentials and documentation via DESNZ. Integration development is underway against the live API. The three action items from v1.0 action plan (contact DESNZ, build prototype, adapter pattern) have been executed.

**Original Inherent Score:** 15 (L3 × I5)
**Original Residual Score:** 12 (L3 × I4)
**Closed Residual Score:** 0

**Closure Date:** 2026-04-06
**Closed By:** CMA Digital Lead

---

### Risk R-011: Service Outage During High-Profile Period

**Category:** TECHNOLOGY
**Status:** Open
**Risk Owner:** CMA Digital Lead

> **v2.0 Change:** No change to scores. VE3 API dependency adds a second outage vector: VE3 downtime causes CMA to serve stale cached data. See also R-021 (VE3 platform single point of failure). R-011 focuses on CMA's own infrastructure outage; R-021 addresses the VE3 dependency.

**Risk Description:** The citizen-facing CMA service experiences an outage during a high-profile fuel price event (budget announcement, supply disruption, media spike), causing embarrassment and citizen frustration.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Auto-scaling, load testing, CDN caching; 15-minute VE3 sync with local cache provides partial resilience

**Primary Response:** TREAT — Load testing at 10x expected peak; CDN for static assets; graceful degradation to cached data

---

### Risk R-012: CMA-to-VE3 API Integration Issues

**Category:** OPERATIONAL
**Status:** In Progress
**Risk Owner:** CMA Digital Lead

> **v2.0 Change (Reframed):** In v1.0, this risk was "Retailer API Integration Issues for Large Chains" (Inherent L4×I3=12, Residual L3×I2=6). Under the new architecture, CMA no longer manages retailer API integrations — that responsibility belongs to VE3 Global. The risk is now the **CMA-to-VE3 API integration**: a single, well-documented, live API integration. This is substantially lower risk than multi-retailer integration management. Residual reduced from 6 to **4**.

**Risk Description:** CMA integration with the VE3 Fuel Finder Public API experiences technical difficulties (rate limiting, schema changes, authentication issues, API versioning breaks) that delay or degrade the 15-minute data sync cycle.

**Root Cause:** CMA depends on a single upstream API; any VE3 API schema change, rate limit policy change, or authentication issue directly affects CMA data freshness.

**Inherent:** Likelihood 2 × Impact 3 = **6** (Medium) — Single known API vs. multiple retailer APIs in v1.0
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Sandbox testing, adapter pattern, ApiSyncState monitoring, DESNZ escalation path for VE3 issues

**Primary Response:** TREAT — Adapter pattern isolating VE3 API details; ApiSyncState monitoring; DESNZ escalation path

---

### Risk R-013: DPIA Not Completed Before Personal Data Processing — CLOSED

**Category:** COMPLIANCE
**Status:** **CLOSED** (2026-04-06)
**Risk Owner:** SIRO / DPO

> **CLOSED:** DPIA v2.0 (ARC-001-DPIA-v2.0) completed with **LOW residual risk** across all 5 identified privacy risks. Critically, the VE3 API architecture pivot means CMA stores **zero retailer PII** (no contact_name, email, or phone in CMA database). Organisation entity removed from data model. ICO compliance risk substantially reduced. This risk is closed with **residual score 0**.

**Original Description (v1.0):** DPIA not completed before personal data (retailer contact details) is processed, creating ICO non-compliance risk.

**Closure Rationale:** DPIA v2.0 completed. Architecture pivot eliminates PII storage from CMA systems entirely. All five DPIA risks carry LOW residual. No processing of personal data in CMA systems requiring ongoing DPIA risk management at this score level.

**Original Inherent Score:** 12 (L3 × I4)
**Original Residual Score:** 6 (L2 × I3)
**Closed Residual Score:** 0

**Closure Date:** 2026-04-06
**Closed By:** SIRO / DPO

---

### Risk R-014: Security Breach or Vulnerability Exploitation

**Category:** TECHNOLOGY
**Status:** Open
**Risk Owner:** SIRO

> **v2.0 Change:** Residual score reduced from **4 → 4** (impact reduced but unchanged numerically). Key change: CMA no longer holds retailer PII (no contact_name, email, phone). Breach impact is substantially reduced — a CMA security breach would expose enforcement records and audit logs but not personal data of ~8,500 retailers. ICO notification risk remains but harm-to-individuals risk is much lower. Inherent score adjusted downward from original: L3×I3=9 maintained but rationale updated.

**Risk Description:** Security vulnerability is exploited, compromising enforcement records, ComplianceRecord data, AuditEvent logs, or service availability. No retailer PII is at risk (VE3 holds this). Government service breach attracts media and ICO scrutiny.

**Updated Root Cause:** CMA systems hold enforcement-sensitive data (EnforcementAction records, CMA officer audit trail) but zero retailer PII. Breach impact is lower than in v1.0 architecture.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Secure by Design (ARC-001-SECU-v1.0), penetration testing, encryption at rest/in transit, zero PII reduces breach harm

**Primary Response:** TREAT — Mandatory Secure by Design assessment; penetration testing before Live

---

### Risk R-015: Benefits Not Measurable or Not Materialising

**Category:** FINANCIAL
**Status:** Open
**Risk Owner:** CMA SRO

> **v2.0 Change:** No change to scores.

**Risk Description:** Consumer benefit from fuel price transparency is difficult to measure or does not materialise at projected levels, undermining NAO/PAC value-for-money assessment.

**Inherent:** Likelihood 2 × Impact 3 = **6** (Medium)
**Residual:** Likelihood 1 × Impact 1 = **1** (Low) — Benefits framework defined early; economic analysis capability planned; VE3 API delivers comprehensive data coverage

**Primary Response:** TREAT — Define benefits measurement framework in SOBC

---

### Risk R-016: CDDO Digital Spend Control Rejection

**Category:** FINANCIAL
**Status:** Open
**Risk Owner:** CMA SRO

> **v2.0 Change:** No change to scores. VE3 API consumer model may simplify CDDO case (lower procurement cost, no bespoke ingestion infrastructure) but spend control still required.

**Risk Description:** CDDO rejects digital spend control submission, delaying procurement and delivery.

**Inherent:** Likelihood 4 × Impact 3 = **12** (Medium)
**Residual:** Likelihood 3 × Impact 2 = **6** (Medium) — Early CDDO engagement; TCoP compliance documented (ARC-001-TCOP-v1.0)

**Primary Response:** TREAT — Early CDDO engagement; strong TCoP evidence; VE3 consumer model demonstrates cost efficiency

---

### Risk R-017: Regulatory Change Mid-Delivery

**Category:** STRATEGIC
**Status:** Monitoring
**Risk Owner:** DESNZ Policy Lead

> **v2.0 Change:** No change to scores. VE3 API consumer model increases exposure to regulatory change: if regulations expand (e.g., new fuel types, EV charging), VE3 must update their API before CMA can consume new data.

**Risk Description:** Motor Fuel Price Regulations are amended mid-delivery (new fuel types, changed submission frequency, expanded scope), requiring CMA to wait for VE3 API updates before consuming new data types.

**Inherent:** Likelihood 3 × Impact 4 = **12** (Medium)
**Residual:** Likelihood 2 × Impact 3 = **6** (Medium) — Modular architecture; VE3 API versioning; DESNZ-VE3 contract requires regulatory change support

**Primary Response:** TOLERATE — Architecture designed for change; regulatory change requires VE3 API update (DESNZ contract obligation)

---

### Risk R-018: Assisted Digital Channels Overwhelmed

**Category:** OPERATIONAL
**Status:** Monitoring (reducing)
**Risk Owner:** CMA Digital Lead

> **v2.0 Change:** No change to scores. Registration surge has passed; support volumes expected to reduce. Ongoing supported digital need remains for compliance queries.

**Risk Description:** Phone and email support channels experience ongoing demand from independent retailers with compliance queries and data submission questions post-registration period.

**Inherent:** Likelihood 3 × Impact 3 = **9** (Medium)
**Residual:** Likelihood 2 × Impact 2 = **4** (Low) — Registration surge passed; FAQs and self-service now live; VE3 handles registration queries directly

**Primary Response:** TREAT — VE3 platform handles registration; CMA support focused on enforcement and compliance queries

---

### Risk R-019: FOI Requests Reveal Sensitive Programme Information

**Category:** OPERATIONAL
**Status:** Monitoring
**Risk Owner:** CMA SRO

> **v2.0 Change:** No change to scores. VE3 contract details (£3M DESNZ spend) may attract FOI interest.

**Risk Description:** FOI requests reveal sensitive programme information (costs, vendor contract details, enforcement case volumes) used by media or opposition to criticise the programme.

**Inherent:** Likelihood 2 × Impact 2 = **4** (Low)
**Residual:** Likelihood 2 × Impact 1 = **2** (Low) — FOI-ready documentation; transparency by default; VE3 contract details in DESNZ ownership

**Primary Response:** TOLERATE — Transparency by default reduces FOI risk

---

### Risk R-020: NAO Audit Identifies Governance Weaknesses

**Category:** OPERATIONAL
**Status:** Monitoring
**Risk Owner:** CMA SRO

> **v2.0 Change:** No change to scores. DPIA v2.0 completion and updated requirements (REQ v3.0) strengthen audit readiness.

**Risk Description:** NAO post-launch audit identifies governance weaknesses, inadequate cost tracking, or poor benefits realisation.

**Inherent:** Likelihood 2 × Impact 4 = **8** (Medium)
**Residual:** Likelihood 1 × Impact 2 = **2** (Low) — Audit-ready documentation; benefits tracking; governance framework; DPIA v2.0 complete

**Primary Response:** TREAT — Maintain audit-ready documentation; version-controlled artifact trail (ArcKit)

---

### Risk R-021: VE3 Global Platform Single Point of Failure

**Category:** TECHNOLOGY
**Status:** Open
**Risk Owner:** CMA Digital Lead
**Action Owner:** CMA Digital Lead / DESNZ Policy Lead

#### Risk Identification

**Risk Description:**
The CMA Fuel Price Transparency Service has zero independent data source. All price data is consumed from the VE3 Fuel Finder Public API on a 15-minute sync cycle. If VE3 Global experiences a prolonged platform outage, CMA has no alternative data feed and will progressively serve stale data until the outage is resolved. Unlike v1.0 architecture where CMA had direct retailer relationships as a fallback, the VE3 consumer model creates a single external dependency with no bypass.

**Root Cause:**
Architecture pivot to VE3 API consumer model eliminates CMA's direct data ingestion capability. CMA has no contractual right to demand VE3 uptime guarantees — that SLA exists between DESNZ and VE3. CMA is a downstream consumer of that contract.

**Trigger Events:**
- VE3 API returns errors or empty responses for more than 30 consecutive minutes
- VE3 Global experiences infrastructure outage (cloud provider, network, application layer)
- VE3 API authentication/access token issues prevent CMA sync
- VE3 platform changes API schema without notice, breaking CMA integration

**Consequences if Realized:**
- CMA serves progressively stale data to citizens — trust erodes
- If VE3 outage exceeds 24 hours, published prices may differ materially from pump prices
- CMA has no ability to self-recover — entirely dependent on VE3 resolution
- DESNZ must escalate VE3 support on CMA's behalf (indirect recovery path)
- Reputational risk: media reports "government fuel price service offline"

**Affected Stakeholders:**
- **Citizens (SD-5)**: Stale or absent price information; poor user experience
- **CMA Board (SD-1)**: Service reliability undermined; regulatory tool non-functional during outage
- **DESNZ Ministers (SD-4)**: Political exposure if service down during high-profile fuel price event
- **VE3 Global (new stakeholder)**: Reputation and contract performance at risk

**Related Objectives:**
- Objective O-1 (Comprehensive Transparency): Directly threatened during any VE3 outage
- NFR ARC-001-REQ-v3.0 NFR-R-001 through NFR-R-003: Resilience requirements

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | VE3 is a production API (live since early 2026) but any SaaS platform has occasional outages; CMA has no fallback |
| **Impact** | 4 - Major | Complete data dependency: outage = zero fresh data; prolonged outage undermines scheme |
| **Inherent Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Current Controls and Mitigations

1. **15-minute sync with local CMA cache — serves cached data during short outages**
   - Owner: CMA Digital Team
   - Effectiveness: **Adequate**
   - Evidence: ApiSyncState entity tracks last successful sync; freshness TTL controls display

2. **Staleness indicator shown to citizens when data age exceeds threshold**
   - Owner: CMA Digital Team
   - Effectiveness: **Adequate**
   - Evidence: Freshness transparency reduces harm from stale data

3. **DESNZ escalation path to VE3 Global via contract**
   - Owner: DESNZ Policy Lead
   - Effectiveness: **Adequate**
   - Evidence: DESNZ holds the VE3 contract; contractual SLA enforceable

4. **VE3 API status monitoring with automated alerting (PagerDuty/equivalent)**
   - Owner: CMA Digital Team
   - Effectiveness: **Adequate**
   - Evidence: Planned per ARC-001-REQ-v3.0 NFR-R-002

**Overall Control Effectiveness:** Adequate (reduces from 12 to 6)

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Cache mitigates short outages; VE3 production stability expected; DESNZ contract provides pressure |
| **Impact** | 3 - Moderate | Prolonged outage (> 4 hours) cannot be self-resolved; impact reduced by staleness transparency |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response (4Ts Framework)

**Primary Response:** TREAT (Mitigate/Reduce)

**Rationale:** Cannot terminate dependency on VE3 (it is the statutory data source under the CMA Fuel Finder scheme). Cannot transfer (no alternative data source exists). Cannot fully tolerate — outage affects citizens. Must treat via caching, monitoring, and DESNZ contract escalation.

#### Action Plan

1. **Define and implement cache TTL policy — specify staleness thresholds for citizen-facing display**
   - Owner: CMA Digital Lead
   - Due Date: 2026-04-30
   - Expected Impact: Clear policy for when to show staleness warning; reduce harm from short outages

2. **Implement VE3 API health monitoring with 5-minute checks and automated alerting**
   - Owner: CMA Digital Team
   - Due Date: 2026-04-30
   - Expected Impact: Rapid detection of VE3 outages; DESNZ notified within 15 minutes

3. **Formalise VE3 outage escalation procedure with DESNZ (SLA visibility)**
   - Owner: DESNZ Policy Lead / CMA SRO
   - Due Date: 2026-05-15
   - Expected Impact: CMA has documented escalation path and expected VE3 recovery SLA

4. **Review VE3 API versioning policy — agree change notification period with DESNZ**
   - Owner: CMA Digital Lead / DESNZ Policy Lead
   - Due Date: 2026-05-15
   - Expected Impact: Schema changes cannot break CMA integration without notice

**Target Residual Risk:** 4 (Low) — Likelihood 2, Impact 2 — achievable once cache TTL policy and monitoring are operational

---

### Risk R-022: CMA-VE3 Data Controller Relationship Not Formalised

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** SIRO / CMA Legal
**Action Owner:** DESNZ Policy Lead (contract holder) / CMA Legal

#### Risk Identification

**Risk Description:**
No data sharing agreement, data processing agreement, or contractual instrument formally governs the CMA-VE3 Global data relationship. VE3 Global holds retailer PII (contact_name, email, phone) under a DESNZ contract. CMA consumes derived (non-PII) data from VE3 but the legal basis for this consumption, the accountability structure for data quality, and the responsibilities in the event of a VE3 data breach are not documented. The ICO would expect a formal data sharing framework to be in place given the public sector nature of both parties and the regulatory context.

**Root Cause:**
Architecture pivot happened rapidly — the VE3 API consumer model emerged from the architecture pivot in early 2026. Legal frameworks typically lag architectural decisions. DESNZ holds the primary VE3 contract; CMA is a downstream consumer outside that contract. No trilateral agreement (CMA-DESNZ-VE3) yet exists.

**Trigger Events:**
- ICO audit or enquiry raises question about legal basis for CMA consuming VE3 data
- VE3 data quality incident raises question about who is accountable to affected parties
- DESNZ-VE3 contract change affects CMA's API access without CMA notification
- Parliamentary question asks CMA to describe data governance with VE3

**Consequences if Realized:**
- ICO enforcement action against CMA for processing data without adequate legal framework
- CMA unable to demonstrate accountability to ICO — reputational and regulatory damage
- VE3 contract change (DESNZ decision) inadvertently terminates CMA data access
- In event of VE3 breach: legal uncertainty about CMA notification obligations

**Affected Stakeholders:**
- **ICO (SD-10)**: Regulatory oversight body — expects documented legal framework
- **CMA Board (SD-1)**: Regulatory accountability; CMA cannot be seen to breach data law
- **DESNZ Policy (SD-3)**: Contract holder; must facilitate CMA-VE3 legal relationship
- **VE3 Global (new stakeholder)**: Contractual clarity protects VE3 as well as CMA

**Related Objectives:**
- Outcome O-4 (Governance Compliance): Legal framework is core governance requirement
- NFR ARC-001-REQ-v3.0 NFR-C-004, NFR-C-005: Compliance and audit requirements
- ARC-001-DPIA-v2.0: DPIA identified data sharing framework as a required control (DPIA-002)

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | No agreement currently exists; architecture pivot has outpaced legal formalisation |
| **Impact** | 3 - Moderate | ICO enforcement or CMA/DESNZ relationship disruption; no immediate citizen harm (no PII in CMA DB) |
| **Inherent Risk Score** | **12** (Medium) | 4 × 3 = 12 |

#### Current Controls and Mitigations

1. **DPIA v2.0 (ARC-001-DPIA-v2.0) identifies and records the gap — DPIA-002 control item**
   - Owner: SIRO / DPO
   - Effectiveness: **Partial**
   - Evidence: DPIA completed; gap documented; agreement not yet in place

2. **DESNZ engagement underway — CMA legal team has raised requirement**
   - Owner: CMA Legal / DESNZ Policy Lead
   - Effectiveness: **Partial**
   - Evidence: Early engagement; no signed instrument yet

3. **VE3 data does not include PII visible to CMA — reduces immediate UK GDPR exposure**
   - Owner: CMA Data Model (architecture control)
   - Effectiveness: **Adequate**
   - Evidence: Organisation entity removed from CMA data model; zero retailer PII in CMA DB

**Overall Control Effectiveness:** Partial (reduces from 12 to 9 — gap remains open)

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Agreement not in place; DESNZ engagement underway but not concluded |
| **Impact** | 3 - Moderate | Impact mitigated by zero PII in CMA systems; legal gap remains a compliance risk |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Risk Response (4Ts Framework)

**Primary Response:** TREAT (Resolve/Mitigate)

**Rationale:** Compliance risk that should be eliminated by establishing a formal agreement. Cannot be tolerated indefinitely — ICO would view absence of legal framework as a control deficiency. Cannot be transferred. Must be treated by formalising the CMA-DESNZ-VE3 data relationship.

#### Action Plan

1. **Draft Data Sharing Agreement (DSA) between CMA and DESNZ covering VE3 data consumption**
   - Owner: CMA Legal / DESNZ Legal
   - Due Date: 2026-04-30
   - Expected Impact: Legal framework in place before service go-live

2. **Request VE3 Global to provide DESNZ with processing terms applicable to CMA downstream access**
   - Owner: DESNZ Policy Lead
   - Due Date: 2026-04-30
   - Expected Impact: VE3 accountability for data quality and breach notification formalised

3. **DPO sign-off on completed data sharing instrument**
   - Owner: SIRO / DPO
   - Due Date: 2026-05-07
   - Expected Impact: ICO-defensible legal framework in place

4. **Document in ICO-accessible record (Article 30 register update)**
   - Owner: DPO
   - Due Date: 2026-05-07
   - Expected Impact: GDPR Article 30 processing record updated to reflect VE3 consumer model

**Target Residual Risk:** 4 (Low) — Likelihood 2, Impact 2 — achievable once DSA signed

---

### Risk R-023: Audit Trail Function Creep

**Category:** TECHNOLOGY
**Status:** Open
**Risk Owner:** SIRO / DPO
**Action Owner:** CMA Digital Lead

#### Risk Identification

**Risk Description:**
The AuditEvent entity logs CMA officer UUID, action type, source IP, and enforcement outcomes for regulatory accountability purposes. There is a risk that this audit data is repurposed — by CMA management or third parties — for employee performance monitoring beyond its stated regulatory accountability purpose. This would constitute unlawful secondary processing under UK GDPR Article 5(1)(b) (purpose limitation). The risk was identified in ARC-001-DPIA-v2.0 as DPIA-004.

**Root Cause:**
Audit logs combining officer identity (UUID), action type, timestamp, and source IP create a detailed activity record of individual CMA officers. If access controls are insufficiently granular, HR functions or line managers could query this data for performance review. The technical capability to do so exists even if policy prohibits it.

**Trigger Events:**
- Line manager or HR requests AuditEvent data for individual officer performance review
- CMA IT team grants audit log access to personnel without explicit need-to-know
- AuditEvent data included in regular reporting without purpose limitation safeguards
- Data subject access request (DSAR) reveals officer audit trail to wrong party

**Consequences if Realized:**
- UK GDPR breach — unlawful secondary processing of officer personal data
- ICO investigation and potential enforcement action
- CMA officers lose trust in audit trail system — affect willingness to log enforcement actions accurately
- Union or employment law dispute

**Affected Stakeholders:**
- **CMA Officers** (data subjects): Privacy rights potentially violated
- **ICO (SD-10)**: Regulatory authority — would investigate purpose limitation breach
- **CMA Board (SD-1)**: Governance failure — reputational and legal risk
- **SIRO / DPO**: Accountability for UK GDPR compliance

**Related Objectives:**
- Principle P-21 (Privacy by Design — ARC-000-PRIN-v1.0): AuditEvent design must embed purpose limitation
- ARC-001-DPIA-v2.0 DPIA-004: This risk identified and documented in DPIA

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Requires deliberate or negligent misuse of audit system; policy and technical controls planned |
| **Impact** | 2 - Minor | Individual CMA officer privacy; limited third-party harm; ICO would likely issue guidance not penalty for first occurrence |
| **Inherent Risk Score** | **4** (Low) | 2 × 2 = 4 |

#### Current Controls and Mitigations

1. **Role-Based Access Control (RBAC) — AuditEvent access restricted to SIRO/DPO and designated audit function only**
   - Owner: CMA Digital Lead
   - Effectiveness: **Strong**
   - Evidence: ARC-001-REQ-v3.0 NFR-SEC-003; planned for MVP

2. **Purpose limitation notice embedded in audit log access UI**
   - Owner: CMA Digital Lead
   - Effectiveness: **Adequate**
   - Evidence: Technical design pattern — access screen displays purpose limitation statement

3. **DPO oversight — quarterly review of AuditEvent access logs**
   - Owner: SIRO / DPO
   - Effectiveness: **Adequate**
   - Evidence: DPIA-004 control requirement; planned for governance calendar

4. **Data minimisation — AuditEvent uses officer UUID not name; resolution only via HR lookup with DPO approval**
   - Owner: CMA Digital Lead / SIRO
   - Effectiveness: **Strong**
   - Evidence: Architecture design; UUID-based audit reduces casual identification

**Overall Control Effectiveness:** Good (reduces from 4 to 2)

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 1 - Rare | RBAC, UUID pseudonymisation, and DPO oversight collectively make misuse very unlikely |
| **Impact** | 2 - Minor | Impact unchanged — limited to individual officer privacy and ICO scrutiny |
| **Residual Risk Score** | **2** (Low) | 1 × 2 = 2 |

#### Risk Response (4Ts Framework)

**Primary Response:** TREAT (Residual low — tolerate with controls maintained)

**Rationale:** Risk is low after controls and consistent with DPIA v2.0 findings (all DPIA residual risks LOW). Maintain RBAC, DPO oversight, and purpose limitation notice. No further treatment investment required beyond controls in place.

#### Action Plan

1. **Implement RBAC with AuditEvent access restricted to audit function role**
   - Owner: CMA Digital Lead
   - Due Date: 2026-04-30
   - Expected Impact: Technical enforcement of purpose limitation

2. **Schedule quarterly DPO audit of AuditEvent access log**
   - Owner: SIRO / DPO
   - Due Date: First review 2026-07-01
   - Expected Impact: Ongoing assurance that access is within defined purpose

**Target Residual Risk:** 2 (Low) — Already achieved once RBAC implemented

---

## D. Risk Category Analysis

### STRATEGIC Risks

**Total:** 3 (R-002, R-005, R-017)
**Average Inherent Score:** 11.0 (Medium)
**Average Residual Score:** 5.3 (Low-Medium)
**Control Effectiveness:** 52% reduction

**Key Themes:** Political pressure vs governance rigour; inter-departmental coordination (now includes VE3 dimension); regulatory change and its impact on VE3 API
**Category Risk Profile:** ACCEPTABLE — Good control effectiveness; CMA independence provides structural protection; VE3 adds coordination complexity but DESNZ contract manages this

### OPERATIONAL Risks

**Total:** 5 (R-001, R-009, R-012, R-018, R-019, R-020)
**Average Inherent Score:** 9.0 (Medium)
**Average Residual Score:** 3.5 (Low)
**Control Effectiveness:** 61% reduction

> Note: v1.0 listed 6 operational risks but R-020 is correctly categorised as OPERATIONAL (NAO audit). R-019 is also OPERATIONAL. Count remains 6 for this category.

**Key Themes:** Ongoing retailer compliance monitoring; CMA-to-VE3 API integration (simplified from retailer-multi-API); FOI and audit readiness
**Category Risk Profile:** ACCEPTABLE — Significant improvement from v1.0; VE3 platform delegation substantially reduces operational burden. R-001 remains above appetite but improving.

### FINANCIAL Risks

**Total:** 3 (R-008, R-015, R-016)
**Average Inherent Score:** 10.0 (Medium)
**Average Residual Score:** 4.3 (Low)
**Control Effectiveness:** 57% reduction

**Key Themes:** Scope creep; benefits measurement; spend control approval
**Category Risk Profile:** ACCEPTABLE — Strong financial controls; VE3 consumer model reduces infrastructure costs; data procurement cost remains £0

### COMPLIANCE Risks

**Total:** 2 active (R-003, R-007) + R-022 reclassified as COMPLIANCE
**Including R-022:** 3 active risks

**R-013 CLOSED** — DPIA completed; removed from active compliance risk count.

**Average Inherent Score (3 active):** 13.3 (High)
**Average Residual Score (3 active):** 9.0 (Medium)
**Control Effectiveness:** 32% reduction

**Key Themes:** Enforcement readiness deadline (May 2026 — 4 weeks); GDS assessment; CMA-VE3 legal framework
**Category Risk Profile:** CONCERNING — R-003 (enforcement tools) has immovable deadline 4 weeks away; R-022 (data sharing agreement) is an open compliance gap requiring urgent resolution

### REPUTATIONAL Risks

**Total:** 3 (R-004, R-006, R-011)
**Average Inherent Score:** 13.7 (High)
**Average Residual Score:** 7.3 (Medium)
**Control Effectiveness:** 47% reduction

**Key Themes:** Data quality (now VE3-sourced); media coverage; service outage visibility
**Category Risk Profile:** MANAGEABLE — R-004 improved from 8 to 6 following VE3 architecture; R-006 unchanged at 12; prevention remains critical

### TECHNOLOGY Risks

**Total:** 5 active (R-009, R-011, R-012, R-014, R-021) — R-010 CLOSED

**Average Inherent Score (5 active):** 9.0 (Medium)
**Average Residual Score (5 active):** 4.4 (Low)
**Control Effectiveness:** 51% reduction

**Key Themes:** VE3 single point of failure (new); CMA infrastructure resilience; security posture (lower risk with no PII); PostGIS expertise
**Category Risk Profile:** MANAGEABLE — R-010 (VE3 API spec) closed; R-021 (VE3 dependency) is the new primary technology risk; no High technology residual risks remain

---

## E. Risk Ownership Matrix

| Stakeholder | Role | Owned Risks (active) | Medium | Low | Total Residual Score |
|-------------|------|----------------------|--------|-----|----------------------|
| CMA SRO | Programme SRO | R-002, R-005, R-006, R-008, R-015, R-019, R-020 | 2 | 5 | 29 |
| CMA Digital Lead | Technology Delivery | R-003, R-004, R-009, R-011, R-012, R-018, R-021 | 3 | 4 | 38 |
| CMA Enforcement Lead | Enforcement | R-001 | 1 | 0 | 9 |
| SIRO / DPO | Information Governance | R-014, R-022, R-023 | 1 | 2 | 15 |
| DESNZ Policy Lead | Policy | R-017 | 1 | 0 | 6 |
| CMA Communications | Comms | R-007, R-016 | 2 | 0 | 12 |

**Risk Concentration Analysis:**
- **CMA Digital Lead owns 7 risks totalling 38 points** — Highest concentration. Appropriate given technology pivot; consider delegating R-018 to operations lead once registration surge has fully subsided.
- **CMA SRO owns 7 risks totalling 29 points** — Appropriate for programme-level strategic and financial risks.
- **SIRO/DPO risk ownership increased** (from 2 to 3 risks): R-022 (data controller relationship) and R-023 (audit function creep) are new; appropriate for information governance owner.
- **VE3 Global** (new stakeholder): Not a risk owner in CMA register but is an action owner for R-021 and R-022 activities. DESNZ acts as intermediary.

---

## F. 4Ts Response Framework Summary

| Response | Count (active) | % | Total Residual Score | Key Examples |
|----------|---------------|---|----------------------|--------------|
| **TOLERATE** | 2 | 10% | 8 | R-017 (regulatory change), R-019 (FOI) |
| **TREAT** | 19 | 90% | 107 | R-001, R-003, R-004, R-006, R-021, R-022, and 13 others |
| **TRANSFER** | 0 | 0% | 0 | No transfer opportunities; VE3 dependency cannot be insured |
| **TERMINATE** | 0 | 0% | 0 | All programme activities essential to regulatory mandate |
| **TOTAL (active)** | 21 | 100% | 115 | |

**Key Insights:**
- **90% of risks require active treatment** — Consistent with v1.0; regulatory urgency drives this profile
- **No transfer opportunities** — VE3 dependency is statutory; no commercial insurance available for government data service failures
- **Only 10% tolerated** — Two low-probability risks with manageable impact; unchanged from v1.0
- **No terminated activities** — All programme activities remain essential
- **Risk score reduction: 37% (v1.0) → 50% (v2.0)** — Architecture pivot has significantly improved the risk profile

---

## G. Risk Appetite Compliance

**Organizational Risk Appetite for UK Government Digital Service:**

| Category | Appetite Level | Threshold | Description |
|----------|---------------|-----------|-------------|
| STRATEGIC | Medium | ≤ 9 | Willing to accept medium strategic risks for regulatory delivery |
| OPERATIONAL | Medium | ≤ 9 | Moderate tolerance for operational challenges during new service launch |
| FINANCIAL | Medium | ≤ 9 | Moderate tolerance given public money accountability |
| COMPLIANCE | Low | ≤ 6 | Low tolerance for compliance breaches (regulatory body must lead by example) |
| REPUTATIONAL | Medium | ≤ 9 | Moderate tolerance given political context but high visibility |
| TECHNOLOGY | Medium | ≤ 9 | Moderate tolerance for technology challenges with controls |

**Compliance Summary (v2.0):**

| Category | Appetite | Risks Within | Risks Exceeding | Action Required |
|----------|----------|--------------|-----------------|-----------------|
| STRATEGIC | ≤ 9 | 3 (100%) | 0 (0%) | COMPLIANT |
| OPERATIONAL | ≤ 9 | 5 (100%)* | 0 (0%)* | COMPLIANT (R-001 reduced from 12 to 9 — within appetite) |
| FINANCIAL | ≤ 9 | 3 (100%) | 0 (0%) | COMPLIANT |
| COMPLIANCE | ≤ 6 | 1 (33%) | 2 (67%) | BREACH: R-003 (12), R-022 (9) — escalation required |
| REPUTATIONAL | ≤ 9 | 2 (67%) | 1 (33%) | BREACH: R-006 (12) — SRO monitoring |
| TECHNOLOGY | ≤ 9 | 5 (100%) | 0 (0%) | COMPLIANT (R-010 closed; R-021 at 6 — within appetite) |

*Note: R-001 at residual 9 is exactly at the OPERATIONAL appetite threshold of ≤ 9 — within appetite.

**Overall Appetite Compliance (v2.0):** 2 of 6 categories have at least one risk exceeding appetite (improved from 4 of 6 in v1.0)

**v1.0 → v2.0 Compliance Improvement:**
- OPERATIONAL: Previously 1 breach (R-001 at 12) → Now compliant (R-001 at 9)
- TECHNOLOGY: Previously 2 breaches (R-010 at 12, R-011 at 4) → Now compliant (R-010 closed, R-011 within appetite)
- COMPLIANCE: Previously 2 breaches → Now 2 breaches but different: R-013 closed (resolved); R-022 (new) added

---

## H. Prioritized Action Plan

### Priority 1: URGENT (This Week — deadline-driven)

| # | Action | Risk(s) | Owner | Due Date | Status |
|---|--------|---------|-------|----------|--------|
| 1 | Achieve feature-complete milestone for enforcement tools | R-003 | CMA Digital Lead | 2026-04-20 | In Progress |
| 2 | Conduct tabletop enforcement exercise with CMA Enforcement | R-003 | CMA Enforcement Lead | 2026-04-25 | Not Started |
| 3 | Obtain CMA legal sign-off on enforcement evidence trail | R-003 | CMA Legal / SIRO | 2026-04-22 | Not Started |
| 4 | Draft Data Sharing Agreement: CMA-DESNZ covering VE3 data | R-022 | CMA Legal / DESNZ Legal | 2026-04-30 | Not Started |

### Priority 2: HIGH (This Month)

| # | Action | Risk(s) | Owner | Due Date | Status |
|---|--------|---------|-------|----------|--------|
| 5 | Implement VE3 cache TTL policy and staleness indicator | R-021 | CMA Digital Lead | 2026-04-30 | In Progress |
| 6 | Implement VE3 API health monitoring with automated alerting | R-021 | CMA Digital Team | 2026-04-30 | Not Started |
| 7 | Implement RBAC for AuditEvent access | R-023 | CMA Digital Lead | 2026-04-30 | Not Started |
| 8 | Operationalise compliance monitoring dashboard | R-001 | CMA Digital Lead | 2026-04-30 | In Progress |
| 9 | Activate proactive media strategy ahead of launch | R-006 | CMA Communications | 2026-04-30 | Not Started |

### Priority 3: HIGH (Next 6 Weeks)

| # | Action | Risk(s) | Owner | Due Date | Status |
|---|--------|---------|-------|----------|--------|
| 10 | VE3 DSA: DPO sign-off and ICO Article 30 update | R-022 | SIRO / DPO | 2026-05-07 | Blocked on #4 |
| 11 | Define enforcement escalation threshold post-grace period | R-001 | CMA Enforcement Lead | 2026-05-07 | Not Started |
| 12 | Formalise VE3 outage escalation procedure with DESNZ | R-021 | DESNZ Policy Lead / CMA SRO | 2026-05-15 | Not Started |
| 13 | Agree VE3 API versioning change notification period | R-021 | CMA Digital Lead / DESNZ | 2026-05-15 | Not Started |

### Priority 4: MEDIUM (This Quarter)

| # | Action | Risk(s) | Owner | Due Date | Status |
|---|--------|---------|-------|----------|--------|
| 14 | Conduct GDS pre-assessment check-in | R-007 | CMA Digital Lead | 2026-05-31 | Not Started |
| 15 | Load test at 10x expected peak | R-011 | CMA Digital Team | 2026-05-31 | Not Started |
| 16 | Penetration testing engagement | R-014 | SIRO | 2026-05-31 | Not Started |
| 17 | Monthly compliance rate reporting to CMA Board | R-001 | CMA SRO | 2026-05-01 onwards | Planned |
| 18 | Schedule quarterly DPO audit of AuditEvent access | R-023 | SIRO / DPO | 2026-07-01 | Planned |

---

## I. Integration with SOBC

### SOBC Strategic Case (Part A)

- **R-001** (independent retailer compliance — improved): Registration substantially achieved demonstrates scheme momentum; ongoing compliance monitoring validates enforcement investment
- **R-003** (enforcement readiness — URGENT): Demonstrates urgency of enforcement tools as a programme critical path item; failure would negate the entire regulatory scheme
- **R-021** (VE3 dependency): Confirms strategic case for maintaining DESNZ-VE3 contract quality standards; CMA is downstream dependent
- **R-022** (data controller relationship): Confirms need for formal CMA-DESNZ-VE3 data sharing framework as a governance prerequisite

### SOBC Economic Case (Part B)

- **R-008** (budget overrun): Apply HM Treasury optimism bias (20-25% for digital services); VE3 consumer model reduces infrastructure costs vs original architecture
- **Data cost profile**: VE3 API access £0 (included in DESNZ-VE3 contract); CMA infrastructure costs focused on enrichment and citizen-facing service only
- **Architecture pivot saving**: Elimination of retailer submission infrastructure represents material cost reduction; quantify for SOBC economic case
- **Risk contingency**: Concentrate contingency on enforcement tool delivery (R-003) and VE3 legal framework (R-022); data procurement remains £0

### SOBC Management Case (Part E)

- Full risk register (v2.0) included — 21 active risks, 2 closed risks
- Top 10 risks with mitigation plans — all Medium or below at residual; no High or Critical residual risks
- Risk ownership matrix demonstrates clear accountability across CMA SRO, CMA Digital Lead, SIRO, and DESNZ
- Architecture pivot documented — risk profile improved from v1.0 (37% reduction → 50% reduction)

### SOBC Recommendation

- Risk profile is **MANAGEABLE and improving** — architecture pivot reduced residual risk score by 50%; no High or Critical residual risks remain (improved from 4 High residual risks in v1.0)
- **Three appetite exceedances** require resolution: R-003 (enforcement tools — imminent deadline), R-006 (media — treatment underway), R-022 (data controller relationship — new gap)
- Key risks are **time-bound** (May 2026 enforcement deadline) — next 4 weeks are critical delivery period

---

## J. Monitoring and Review Framework

### Review Schedule

| Risk Level | Review Frequency | Reviewed By | Escalated To |
|------------|------------------|-------------|--------------|
| **URGENT (R-003)** | Daily | CMA Digital Lead | CMA SRO / Programme Board |
| **Medium (6-12)** | Weekly | Risk Owner | CMA SRO |
| **Low (1-5)** | Monthly | Action Owner | Risk Owner |

### Key Risk Indicators (KRIs)

**Leading Indicators (v2.0 — updated for new architecture):**
- Independent forecourt data freshness rate (below 80% with freshness < 24h → R-001 escalation)
- Sprint velocity on enforcement features (behind plan → R-003 escalation — currently URGENT)
- VE3 API sync failure rate (more than 2 failed syncs per day → R-021 escalation)
- VE3 API response time (median latency > 2s → R-021 investigation)
- CMA-VE3 DSA completion status (unsigned by 2026-04-30 → R-022 SRO escalation)
- Media sentiment analysis (negative fuel price coverage → R-006 escalation)

**Lagging Indicators:**
- Data coverage rate (freshness) at launch (below 90% → R-001 and R-004 escalation)
- VE3 API outage duration (exceeds 4 hours → R-021 materialised; invoke DESNZ escalation)
- GDS assessment result (condition applied → R-007 escalation)
- Enforcement tool availability on grace period end date (not available → R-003 materialised)
- ICO enquiry received re: CMA-VE3 legal framework (before DSA signed → R-022 materialised)

### Escalation Criteria

1. Any active risk increases by 3+ points
2. Any new High or Critical risk identified
3. Any risk exceeds appetite with no approved mitigation plan
4. Any mitigation action on Priority 1 or Priority 2 delayed more than 5 working days
5. R-003 enforcement tools not feature-complete by 2026-04-20
6. VE3 API outage exceeds 4 hours
7. R-022 DSA not signed by 2026-05-07 (CMA Board notification required)

### Reporting Requirements

- **Daily**: R-003 enforcement tool delivery status to CMA Digital Lead and CMA SRO
- **Weekly**: Medium risks (R-001, R-003, R-006, R-021, R-022) to Programme Board
- **Monthly**: Full risk register to CMA SRO; compliance rate reporting (post-grace period)
- **Quarterly**: Risk appetite compliance to CMA Board and Audit Committee; DPO audit of AuditEvent access (R-023)
- **Next Review Date**: 2026-05-06

**Risk Register Owner:** CMA SRO (Programme Senior Responsible Owner)

---

## K. Orange Book Compliance Checklist

- **A. Governance and Leadership**: Risk owners assigned from senior stakeholders (RACI matrix in ARC-001-STKE-v1.0); VE3 Global added as new stakeholder with DESNZ as contract intermediary; escalation paths defined; risk appetite set and compliance assessed
- **B. Integration**: Risks linked to stakeholder goals (G-1 through G-7) and outcomes (O-1 through O-4); architecture pivot documented and integrated; feeds into SOBC Management Case; DPIA v2.0 cross-referenced
- **C. Collaboration and Best Information**: Risks sourced from DPIA v2.0 (R-023), architecture pivot analysis (R-021, R-022), requirements v3.0 (NFR linkages), stakeholder concerns (SD-1 through SD-12); VE3 API live status verified
- **D. Risk Management Processes**: 5×5 assessment methodology; 4Ts framework; inherent and residual tracking; systematic identification across 6 categories; risk closure process applied to R-010 and R-013
- **E. Continual Improvement**: Monthly review schedule; KRIs updated for VE3 architecture; escalation criteria updated; version-controlled register (v1.0 → v2.0 demonstrates improvement tracking)

---

## Appendix A: Stakeholder-Risk Linkage

| Stakeholder | Driver (ARC-001-STKE-v1.0) | Risk ID | Risk Title | Residual |
|-------------|----------------------------|---------|------------|----------|
| CMA Board | SD-1: Regulatory effectiveness | R-001, R-003, R-004, R-021 | Compliance, enforcement, data quality, VE3 dependency | 9, 12, 6, 6 |
| CMA Enforcement | SD-2: Enforcement capability | R-001, R-003 | Ongoing compliance, enforcement tools | 9, 12 |
| DESNZ Policy | SD-3: Deliver commitment | R-002, R-005, R-017, R-022 | Governance, friction, reg change, VE3 legal | 6, 4, 6, 9 |
| DESNZ Ministers | SD-4: Political accountability | R-002, R-006, R-015, R-021 | Governance, media, benefits, VE3 outage | 6, 12, 1, 6 |
| Citizens | SD-5: Find cheapest fuel | R-004, R-006, R-011, R-021 | Data quality, media, outage, VE3 dependency | 6, 12, 4, 6 |
| Large Retailers | SD-6: Minimise burden | R-012 | CMA-VE3 API integration issues | 4 |
| Independents | SD-7: Avoid disproportionate burden | R-001, R-018 | Ongoing compliance, support | 9, 4 |
| Trade Bodies | SD-8: Protect members | R-001, R-006 | Ongoing compliance, media | 9, 12 |
| GDS Assessors | SD-9: Service meets standard | R-007, R-002 | GDS failure, governance shortcuts | 6, 6 |
| ICO | SD-10: Data protection | R-014, R-022, R-023 | Security, VE3 legal, audit function creep | 4, 9, 2 |
| Third Parties / VE3 | SD-11: Reliable API | R-021, R-011 | VE3 dependency, CMA outage | 6, 4 |
| NAO/PAC | SD-12: Value for money | R-008, R-015, R-020 | Budget, benefits, audit | 6, 1, 2 |

---

## Appendix B: Closed Risk Summary

| Risk ID | Title | Original Inherent | Original Residual | Closure Date | Closure Reason |
|---------|-------|-------------------|-------------------|--------------|----------------|
| R-010 | VE3 Global API specification unavailable | 15 (L3×I5) | 12 (L3×I4) | 2026-04-06 | VE3 Fuel Finder API went live early 2026; CMA has access and integration is underway |
| R-013 | DPIA not completed before personal data processing | 12 (L3×I4) | 6 (L2×I3) | 2026-04-06 | DPIA v2.0 completed (ARC-001-DPIA-v2.0); all 5 DPIA risks LOW; CMA stores zero retailer PII |

---

## Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| **Risk Register Owner** | CMA SRO | | |
| **CMA Enforcement Lead** | | | |
| **CMA Digital Lead** | | | |
| **SIRO / DPO** | | | |
| **DESNZ Policy Lead** | | | |

---

## Next Steps

1. **Immediate Actions** (This Week — enforcement deadline driven):
   - [ ] Daily enforcement readiness stand-up — R-003 (URGENT)
   - [ ] Initiate CMA-DESNZ Data Sharing Agreement drafting — R-022
   - [ ] Implement VE3 API health monitoring — R-021
   - [ ] Brief CMA SRO on updated risk profile (3 appetite exceedances; 2 closed risks)

2. **Short-term Actions** (By End April 2026):
   - [ ] Enforcement tools feature-complete milestone — R-003 (2026-04-20)
   - [ ] Enforce tabletop exercise with CMA Enforcement — R-003 (2026-04-25)
   - [ ] VE3 cache TTL policy and staleness indicator operational — R-021
   - [ ] RBAC implementation for AuditEvent access — R-023
   - [ ] Compliance monitoring dashboard operational — R-001
   - [ ] Proactive media strategy activated — R-006

3. **Medium-term Actions** (May 2026):
   - [ ] DSA signed and DPO sign-off obtained — R-022 (2026-05-07)
   - [ ] Enforcement grace period ends — R-003 enforcement operational
   - [ ] Post-grace-period compliance monitoring begins — R-001
   - [ ] VE3 outage escalation procedure agreed with DESNZ — R-021

4. **Ongoing Actions** (Quarterly):
   - [ ] Full risk register review — next review 2026-05-06
   - [ ] Risk appetite compliance report to CMA Board
   - [ ] DPO quarterly audit of AuditEvent access — first review 2026-07-01 (R-023)

---

**END OF RISK REGISTER**

---

*This risk register follows HM Treasury Orange Book (2023) principles and integrates with ArcKit's stakeholder-driven architecture governance framework. v2.0 reflects the VE3 API architecture pivot (Jan–Apr 2026): two risks closed, five risks updated, three new risks added.*

*For questions or updates, contact: CMA SRO (Programme Senior Responsible Owner)*

---

**Generated by**: ArcKit `/arckit.risk` command
**Generated on**: 2026-04-06
**ArcKit Version**: 4.6.3-rc.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: Claude Opus 4.6
**Supersedes**: ARC-001-RISK-v1.0 (2026-01-30)
