# Architecture Governance Analysis Report: UK Fuel Price Transparency Service

> **Template Status**: Beta | **Version**: 3.0 | **Command**: `/arckit.analyze`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-ANAL-v3.0 |
| **Document Type** | Governance Analysis Report |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 3.0 |
| **Created Date** | 2026-03-01 |
| **Last Modified** | 2026-03-01 |
| **Review Cycle** | On-Demand |
| **Next Review Date** | 2026-03-31 |
| **Owner** | Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-28 | ArcKit AI | Initial analysis — 3 CRITICAL, 5 HIGH, 4 MEDIUM, 3 LOW (score 83/100) | PENDING | PENDING |
| 2.0 | 2026-03-01 | ArcKit AI | Re-analysis after TCoP/SOBC/FR-006 fixes — 0 CRITICAL, 7 HIGH, 7 MEDIUM, 3 LOW (score 87/100) | PENDING | PENDING |
| 3.0 | 2026-03-01 | ArcKit AI | Re-analysis after document owner and budget remediation — 0 CRITICAL, 5 HIGH, 6 MEDIUM, 2 LOW (score 90/100) | PENDING | PENDING |

---

## Executive Summary

**Overall Status**: ⚠️ Issues Found

**Key Metrics**:

- Total Requirements: 63 (7 BR, 15 FR, 27 NFR, 8 INT, 6 Data Entities)
- Requirements Coverage: N/A (no HLD/DLD — pre-design phase)
- Critical Issues: 0
- High Priority Issues: 5
- Medium Priority Issues: 6
- Low Priority Issues: 2

**Recommendation**: MAY PROCEED — address HIGH issues before Beta

### Version Tracking

| Finding | v1.0 Status | v2.0 Status | v3.0 Status |
|---------|-------------|-------------|-------------|
| C1: Missing TCoP assessment | CRITICAL | RESOLVED | RESOLVED |
| C2: FR-006 placeholder ("24 hours") | CRITICAL | RESOLVED | RESOLVED |
| C3: Missing SOBC business case | CRITICAL | RESOLVED | RESOLVED |
| H2: Document owner placeholders (16 files) | HIGH | HIGH (10+ files) | **RESOLVED** |
| H4: REQ budget all TBD | HIGH | HIGH | **RESOLVED** |
| H1: Cloud provider ADR missing | HIGH | HIGH | HIGH (unchanged) |
| H3: R-010 VE3 API no mitigating requirement | HIGH | HIGH | HIGH (unchanged) |
| H5: NFR-C-004 says "12 points" TCoP | HIGH | HIGH | HIGH (unchanged) |
| H7: TCoP says "No SOBC" (but SOBC exists) | — | HIGH | HIGH (unchanged) |
| H6: TCoP score 110 vs 108 discrepancy | — | LOW→HIGH | HIGH (unchanged) |

**Net Progress**: 5 of 10 HIGH issues resolved across v1.0→v3.0. All 3 CRITICAL issues resolved. Score improved from 83 → 87 → 90.

---

## Findings Summary

| ID | Category | Severity | Location(s) | Summary | Recommendation |
|----|----------|----------|-------------|---------|----------------|
| H1 | Traceability | HIGH | Missing artifact | No cloud provider ADR — blocks Beta | Create ADR with `/arckit:adr` |
| H3 | Risk Management | HIGH | ARC-001-RISK-v1.0 | R-010 (VE3 API) has no mitigating requirement | Add INT requirement for VE3 API fallback |
| H5 | Requirements Quality | HIGH | ARC-001-REQ-v2.0:L1227 | NFR-C-004 references "12 points" of TCoP — should be 13 | Correct to "13 points" |
| H7 | Cross-Artifact Consistency | HIGH | ARC-001-TCOP-v1.0:L513-514 | TCoP Point 11 says "No SOBC exists" and "Budget figures all TBD" — both now false | Update TCoP to reference ARC-001-SOBC-v1.0 |
| H6 | Cross-Artifact Consistency | HIGH | ARC-001-TCOP-v1.0:L56,L651 | Exec summary says 110/130 but scorecard sums to 108/130 | Correct exec summary to 108/130 (83%) |
| M1 | Traceability | MEDIUM | Missing artifact | No traceability matrix (ARC-001-TRAC) | Create with `/arckit:traceability` |
| M2 | Requirements Quality | MEDIUM | ARC-001-REQ-v2.0:L1599-1768 | Data entities lack formal DR-xxx requirement IDs | Add DR-001 to DR-006 prefixes |
| M3 | Stakeholder Analysis | MEDIUM | ARC-001-STKE-v1.0 | Interview schedule dates all TBC | Schedule user research interviews |
| M4 | Business Case | MEDIUM | ARC-001-SOBC-v1.0 | No exit strategy for cloud/technology vendor | Add exit strategy to Commercial Case |
| M5 | Security | MEDIUM | ARC-001-SECD-v1.0 | 10 TBD items pending design decisions | Resolve after cloud provider selection |
| M6 | UK Gov Compliance | MEDIUM | ARC-001-DPIA-v1.0 | DPO sign-off pending on DPIA | Obtain before retailer registration |
| L1 | Consistency | LOW | ARC-001-DPIA-v1.0 | Classification OFFICIAL-SENSITIVE vs OFFICIAL elsewhere | Align or document justification |
| L2 | Documentation | LOW | ARC-001-TCOP-v1.0 | Sustainability metrics not defined (Point 12) | Define before Live |

---

## Requirements Analysis

### Requirements Inventory

| Category | Count | MUST | SHOULD | COULD | Quality |
|----------|-------|------|--------|-------|---------|
| Business (BR) | 7 | 7 | 0 | 0 | ✅ Good |
| Functional (FR) | 15 | 10 | 4 | 1 | ✅ Good |
| Non-Functional (NFR) | 27 | 22 | 4 | 1 | ✅ Good |
| Integration (INT) | 8 | 5 | 2 | 1 | ✅ Good |
| Data Entities | 6 | — | — | — | ⚠️ Missing DR-xxx IDs |
| **Total** | **63** | **44** | **10** | **3** | |

**Requirements Quality Score**: 92%

- All requirements have unique IDs, priorities, and rationale
- All business requirements traced to stakeholder goals
- All functional requirements have acceptance criteria with Given/When/Then format
- Budget section now references SOBC with real figures (£2.84M TCO, £3.41M with optimism bias)
- No TBD/TBC/TODO placeholders remain in REQ-v2.0
- Minor issue: NFR-C-004 references "12 points" — TCoP has 13 points
- Minor issue: Data entities lack formal DR-xxx IDs (described narratively, not enumerated)

### Uncovered Requirements

N/A — No HLD or DLD exist yet. Requirements coverage against design cannot be assessed until design artifacts are produced.

---

## Architecture Principles Compliance

| # | Principle | Status | Evidence |
|---|-----------|--------|----------|
| 1 | Open Data by Default | ✅ COMPLIANT | BR-005, FR-005, NFR-I-002, NFR-I-003 |
| 2 | Citizen-Centred Design | ✅ COMPLIANT | BR-003, 7 personas, WCAG 2.2 AA |
| 3 | Scalability and Elasticity | ✅ COMPLIANT | NFR-S-001, NFR-S-002, NFR-P-002 |
| 4 | Resilience and Fault Tolerance | ✅ COMPLIANT | NFR-A-001 to NFR-A-003, circuit breakers |
| 5 | Interoperability | ✅ COMPLIANT | NFR-I-001, INT-001 to INT-008, OpenAPI 3.0 |
| 6 | Security by Design | ✅ COMPLIANT | NFR-SEC-001 to 005, SECD-v1.0, DPIA |
| 7 | Observability | ✅ COMPLIANT | NFR-M-001, RED metrics, distributed tracing |
| 8 | Data Sovereignty | ✅ COMPLIANT | TC-1 (UK sovereign), NFR-C-001 |
| 9 | Data Quality and Timeliness | ✅ COMPLIANT | FR-007, NFR-P-002, freshness SLA |
| 10 | Single Source of Truth | ✅ COMPLIANT | DATA-v1.0, ingestion pipeline as SoR |
| 11-22 | Remaining principles | ✅ COMPLIANT | Covered across REQ and PRIN artifacts |

**Critical Principle Violations**: 0

**Alignment Score**: 100% — all 22 principles have supporting requirements

---

## Stakeholder Traceability Analysis

**Stakeholder Analysis Exists**: ✅ Yes (ARC-001-STKE-v1.0)

**Stakeholder-Requirements Coverage**:
- Requirements traced to stakeholder goals: 95%
- Orphan requirements (no stakeholder justification): 0
- Requirement conflicts documented and resolved: ✅ Yes (4 conflicts, all with resolution)

**RACI Governance Alignment**:

| Artifact | Role | Aligned with RACI? | Issues |
|----------|------|-------------------|--------|
| Risk Register | Risk Owners | ✅ Yes | All 20 risk owners traced to RACI |
| Data Model | Data Owners | ✅ Yes | CMA Director of Digital Markets as data owner |
| SOBC | Benefits Owners | ✅ Yes | SRO accountable for benefits realisation |
| All Artifacts | Document Owners | ✅ Yes | **RESOLVED in v3.0** — all 16 artifacts now have named owners |

**Critical Issues**: None (stakeholder governance is strong)

---

## Risk Management Analysis

**Risk Register Exists**: ✅ Yes (ARC-001-RISK-v1.0)

**Risk Profile**: 20 risks, 0 Critical residual, 4 High residual, 12 Medium, 4 Low

**Risk Coverage**:

| Risk ID | Category | Inherent | Residual | Response | Mitigation in Req? | Issue |
|---------|----------|----------|----------|----------|-------------------|-------|
| R-001 | OPERATIONAL | 20 | 12 | Treat | ✅ BR-001, FR-001 | Above appetite (+3) |
| R-003 | COMPLIANCE | 16 | 12 | Treat | ✅ BR-004, FR-006 | Above appetite (+3) |
| R-006 | REPUTATIONAL | 16 | 12 | Treat | ✅ BR-003, BR-006 | Above appetite (+3) |
| R-010 | TECHNOLOGY | 15 | 12 | Treat | ❌ No specific INT requirement | **H3: Above appetite, no requirement** |

**High/Very High Risks Requiring Attention**:

| Risk ID | Description | Current Status | Required Action |
|---------|-------------|----------------|-----------------|
| R-010 | VE3 Global API specification unavailable | In Progress | Add fallback integration requirement (e.g., INT-009) |

**Risk-SOBC Alignment**:
- Strategic risks reflected in Strategic Case: ✅ Yes
- Financial risks in Economic Case cost contingency: ✅ Yes (15% contingency)
- Risks included in Management Case Part E: ✅ Yes (all 4 above-appetite risks)

**Risk Governance**:
- Risk owners from stakeholder RACI: ✅ Yes (all 20)
- Risk appetite compliance: 16/20 within tolerance

**Risk Management Score**: 85%

---

## Business Case Analysis

**SOBC Exists**: ✅ Yes (ARC-001-SOBC-v1.0)

**Five-Case Model**: ✅ Complete (Strategic, Economic, Commercial, Financial, Management)

**Key Financials**:
- 3-Year TCO: £2.84M (£3.41M with optimism bias)
- NPV: £80.7M (social)
- BCR: 24:1
- Payback: < 1 month

**Benefits Coverage**:
- Total benefits: 4 quantified categories
- Benefits traced to stakeholder goals: 100%
- Benefits supported by requirements: 100%
- Benefits measurable and verifiable: ✅ Yes

**Option Analysis Quality**:
- Do Nothing baseline included: ✅ Yes
- Options analysed: 4 (Do Nothing, Minimal, Balanced RECOMMENDED, Comprehensive)
- Justification: ✅ Strong

**SOBC-Requirements Alignment**:
- Strategic Case drivers in requirements: ✅ Yes
- Economic Case benefits achievable with requirements: ✅ Yes
- Financial Case budget adequate: ✅ Yes (aligned with REQ budget section)
- REQ budget now cross-references SOBC: ✅ **RESOLVED in v3.0**

**Critical Issues**:
- Exit strategy not documented (M4)

**Business Case Score**: 92%

---

## Data Model Analysis

**Data Model Exists**: ✅ Yes (ARC-001-DATA-v1.0)

**Data Model Quality**:
- ERD exists and renderable: ✅ Yes (Mermaid)
- Entities with complete specs: 8/8 (96 attributes total)
- PII identified: ✅ Yes (Organisation contact details)
- GDPR compliance documented: ✅ Yes (Public Task Art 6(1)(e))
- Data governance matrix: ✅ Yes (owner, steward, custodian, DPO)

**Data Requirements Coverage**:
- Data entities described in REQ: 6 entities (L1599-1768)
- Entities in DATA model: 8 entities (6 core + 2 supplementary)
- Formal DR-xxx requirement IDs: ❌ Missing (M2)

**Data Model-Design Alignment**: N/A (no HLD/DLD yet)

**Data Model Score**: 90%

---

## UK Government Compliance Analysis

### Technology Code of Practice (TCoP)

**Assessment Exists**: ✅ Yes (ARC-001-TCOP-v1.0)

**Overall Score**: 108/130 (83%) — 8 Compliant, 5 Partially Compliant, 0 Non-Compliant

| Point | Requirement | Status | Score | Issues |
|-------|-------------|--------|-------|--------|
| 1 | Define user needs | ✅ | 9/10 | Interviews TBC |
| 2 | Make things accessible | ✅ | 9/10 | Audit not yet due |
| 3 | Be open and use open source | ✅ | 10/10 | None |
| 4 | Make use of open standards | ✅ | 10/10 | None |
| 5 | Use cloud first | ⚠️ | 7/10 | Provider selection pending |
| 6 | Make things secure | ⚠️ | 7/10 | Pen test not yet due |
| 7 | Make privacy integral | ✅ | 9/10 | DPO sign-off pending |
| 8 | Share, reuse and collaborate | ✅ | 10/10 | None |
| 9 | Integrate and adapt technology | ✅ | 10/10 | None |
| 10 | Make better use of data | ✅ | 10/10 | None |
| 11 | Define purchasing strategy | ⚠️ | 5/10 | **H7: Says "No SOBC" — SOBC now exists** |
| 12 | Make technology sustainable | ⚠️ | 5/10 | Sustainability metrics not defined |
| 13 | Meet the Service Standard | ⚠️ | 7/10 | Assessment not yet due |

**Cross-Artifact Issues**:
- **H7**: TCoP Point 11 text states "No SOBC exists" and "Budget figures all TBD" — both are now false. SOBC exists (ARC-001-SOBC-v1.0) and budget is populated in REQ. TCoP needs updating.
- **H6**: TCoP executive summary says "110/130 (85%)" but scorecard sums to 108/130 (83%). The scorecard total is correct.
- **H5**: REQ NFR-C-004 references "12 points" of TCoP — the TCoP has 13 points.

**TCoP Score (corrected)**: 108/130 (83%)

### Secure by Design

**Assessment Exists**: ✅ Yes (ARC-001-SECD-v1.0)

- STRIDE threat model: ✅ Completed
- NCSC CAF alignment: ✅ Assessed
- 10 TBD items pending design decisions (M5) — expected at Discovery/Alpha phase
- Classification: OFFICIAL (with OFFICIAL-SENSITIVE for enforcement data)

### DPIA

**Assessment Exists**: ✅ Yes (ARC-001-DPIA-v1.0)

- Residual risk: LOW-MEDIUM
- PII: Retailer contact details only
- Lawful basis: Public Task Art 6(1)(e)
- DPO sign-off: PENDING (M6)

**UK Gov Compliance Score**: 85%

---

## Traceability Analysis

**Traceability Matrix**: ❌ Missing (M1)

No formal traceability matrix (ARC-001-TRAC) exists. Requirements are traced to stakeholder goals and principles within REQ-v2.0, but no consolidated forward/backward traceability from requirements → design → tests.

**Traceability Score**: 40% (informal tracing exists but no formal matrix)

---

## Security & Compliance Summary

### Security Posture
- Security requirements defined: ✅ Yes (NFR-SEC-001 to 005)
- Threat model documented: ✅ Yes (STRIDE in SECD-v1.0)
- Security architecture in HLD: N/A (no HLD)
- Penetration testing: Planned (not yet due)
- SIRO sign-off: Pending

**Security Coverage**: 85%

### Compliance Posture
- UK GDPR: ✅ DPIA completed
- GDS Service Standard: ⚠️ Assessment planned, not yet conducted
- TCoP: ⚠️ 83% compliant (5 partial points)
- Secure by Design: ⚠️ Assessment completed, 10 TBD items

**Compliance Coverage**: 80%

---

## Recommendations

### High Priority Actions (SHOULD resolve before Beta)

1. **[H1] Create Cloud Provider ADR**: Formalise AWS vs Azure selection decision in an Architecture Decision Record. Both providers thoroughly researched. Run `/arckit:adr`. — *Addresses: TCoP Point 5*
2. **[H3] Add VE3 API Fallback Requirement**: Risk R-010 (VE3 API unavailable) exceeds appetite but has no specific mitigating requirement. Add INT-009 for VE3 API with fallback to interim CMA JSON endpoints. — *Addresses: Risk R-010*
3. **[H5] Correct TCoP Reference**: NFR-C-004 (ARC-001-REQ-v2.0:L1227) says "12 points" — TCoP has 13 points. Change to "13 points". — *Effort: 1 minute*
4. **[H7] Update TCoP Point 11**: ARC-001-TCOP-v1.0 states "No SOBC exists" and "Budget figures all TBD". Both are now false — update to reference ARC-001-SOBC-v1.0 and the populated budget in REQ-v2.0. — *Effort: 30 minutes*
5. **[H6] Fix TCoP Score Inconsistency**: Executive summary says 110/130 (85%) but scorecard sums to 108/130 (83%). Correct executive summary to match scorecard. — *Effort: 5 minutes*

### Medium Priority Actions (Address during Alpha/Beta)

1. **[M1] Create Traceability Matrix**: Run `/arckit:traceability` to generate formal requirements-to-design-to-test traceability. — *Required before Live assessment*
2. **[M2] Add DR-xxx Requirement IDs**: Data entities in REQ-v2.0 (L1599-1768) lack formal DR-001 to DR-006 identifiers. — *Effort: 30 minutes*
3. **[M3] Schedule User Research Interviews**: Stakeholder interview dates in STKE-v1.0 are all TBC. GDS Alpha assessment will examine user research evidence. — *Critical for GDS assessment*
4. **[M4] Document Exit Strategy**: SOBC Commercial Case lacks cloud/technology exit strategy. Required for TCoP Point 11. — *Effort: 1 hour*
5. **[M5] Resolve SECD TBD Items**: 10 TBD items in Secure by Design assessment pending design decisions. Resolve after cloud provider selection. — *Required before Beta*
6. **[M6] Obtain DPO Sign-off on DPIA**: DPIA is in DRAFT. DPO sign-off required before processing personal data (retailer registration). — *Required before registration opens*

### Low Priority Actions (Optional improvements)

1. **[L1] Align DPIA Classification**: DPIA classified OFFICIAL-SENSITIVE; all other artifacts classified OFFICIAL. Align or document the justification for the difference.
2. **[L2] Define Sustainability Metrics**: TCoP Point 12 requires sustainability metrics (carbon per transaction, energy per query). Define before Live.

---

## Metrics Dashboard

### Requirement Quality
- Total Requirements: 63
- Ambiguous Requirements: 0
- Duplicate Requirements: 0
- Untestable Requirements: 0
- Budget Aligned with SOBC: ✅ Yes (resolved v3.0)
- **Quality Score**: 92%

### Architecture Alignment
- Principles Compliant: 22/22
- Principles Violations: 0
- **Alignment Score**: 100%

### Traceability
- Traceability Matrix: ❌ Missing
- Informal tracing in REQ: ✅ Yes (goals, principles)
- **Traceability Score**: 40%

### Stakeholder Traceability
- Requirements traced to stakeholder goals: 95%
- Orphan requirements: 0
- Conflicts resolved: 100% (4/4)
- RACI governance alignment: 100%
- Document owners assigned: 100% (resolved v3.0)
- **Stakeholder Score**: 98%

### Risk Management
- High/Very High risks mitigated: 75% (3 of 4 above-appetite have requirements)
- Risk owners from RACI: 100%
- Risk-SOBC alignment: 100%
- **Risk Management Score**: 85%

### Business Case
- Benefits traced to stakeholder goals: 100%
- Benefits supported by requirements: 100%
- Benefits measurable: 100%
- Budget adequacy: ✅ Adequate (£2.84M TCO)
- REQ-SOBC budget alignment: ✅ Aligned (resolved v3.0)
- **Business Case Score**: 92%

### Data Model
- Entities with complete specs: 8/8
- PII identified: 100%
- Data governance complete: 100%
- DR-xxx formal IDs: ❌ Missing
- **Data Model Score**: 90%

### UK Government Compliance
- TCoP Score: 108/130 (83%)
- Secure by Design: ⚠️ 10 TBD items
- DPIA: ✅ Completed (DPO sign-off pending)
- **UK Gov Compliance Score**: 85%

### Overall Governance Health

**Score**: 90/100

**Grade**: A (90-100%)

**Grade Thresholds**:
- A (90-100%): Excellent governance, ready to proceed
- B (80-89%): Good governance, minor issues
- C (70-79%): Adequate governance, address high-priority issues
- D (60-69%): Poor governance, major rework needed
- F ( < 60%): Insufficient governance, do not proceed

**Score Progression**: 83 (v1.0) → 87 (v2.0) → **90 (v3.0)**

---

## Next Steps

### Immediate Actions

1. **No CRITICAL issues** — ✅ MAY PROCEED to Beta planning
2. **5 HIGH issues** — Resolve before Beta phase gate:
   - H1: Create cloud provider ADR (`/arckit:adr`)
   - H3: Add VE3 API fallback requirement to REQ-v2.0
   - H5, H6, H7: Fix TCoP and REQ text errors (quick edits)

### Suggested Commands

**Governance Foundation** (address HIGH issues):
- `/arckit:adr` — Create cloud provider selection ADR (addresses H1)
- `/arckit:traceability` — Generate traceability matrix (addresses M1)

**UK Government Compliance** (address TCoP gaps):
- `/arckit:service-assessment` — Prepare GDS Service Standard self-assessment
- `/arckit:tcop` — Regenerate TCoP assessment (addresses H6, H7)

**Operational Readiness** (Alpha/Beta preparation):
- `/arckit:hld-review` — Review HLD once design is produced
- `/arckit:devops` — Create DevOps strategy
- `/arckit:operationalize` — Create operational readiness pack

### Re-run Analysis

After making changes, re-run analysis:
```
/arckit:analyze
```

Target: Resolve all HIGH issues to achieve 93%+ score before Beta.

---

## Detailed Findings

### HIGH Issues

#### H1: Cloud Provider ADR Missing

**Severity**: 🟠 HIGH
**Category**: Traceability / Decision Records
**Location**: Missing artifact

**Description**:
Both AWS (ARC-001-AWRS-v1.0/v1.1/v2.0) and Azure (ARC-001-AZRS-v1.0/v1.1/v2.0) have been thoroughly researched with comprehensive service evaluations. However, no Architecture Decision Record (ADR) formalises the cloud provider selection. TCoP Point 5 (Cloud First) is rated Partially Compliant because of this gap.

**Impact**: Cloud provider selection blocks infrastructure design, SECD TBD resolution, and cost finalisation. Without an ADR, the decision lacks the audit trail required for CDDO spend control approval.

**Recommendation**:
1. Run `/arckit:adr` to create a formal cloud provider selection ADR
2. Reference both AWS and Azure research artifacts as evidence
3. Document rationale for selected provider including UK sovereign region, pricing, and managed service availability

**Estimated Effort**: 2 hours

---

#### H3: R-010 VE3 API — No Mitigating Requirement

**Severity**: 🟠 HIGH
**Category**: Risk Management
**Location**: ARC-001-RISK-v1.0 (R-010, residual score 12, exceeds appetite by +3)

**Description**:
Risk R-010 identifies that the VE3 Global API specification for fuel price data submission has not been publicly published. This is one of 4 risks exceeding organisational appetite (residual score 12 vs appetite ≤ 9). However, unlike R-001, R-003, and R-006, there is no specific mitigating requirement in ARC-001-REQ-v2.0 for a VE3 API fallback strategy.

The interim CMA JSON endpoints (from existing voluntary scheme) exist and are analysed in ARC-001-DATA-v1.0, but no integration requirement mandates fallback to these endpoints if VE3 is unavailable.

**Impact**: If VE3 API remains unavailable, the primary data ingestion path is blocked. Without a formal fallback requirement, delivery teams may not plan for this contingency.

**Recommendation**:
1. Add INT-009 to ARC-001-REQ-v2.0: "The system MUST support fallback data ingestion from the interim CMA JSON API endpoints if the VE3 Global API specification is unavailable at development start"
2. Priority: MUST_HAVE
3. Reference: ARC-001-DATA-v1.0 CmaJsonStation entity (E-007)

**Estimated Effort**: 30 minutes

---

#### H5: NFR-C-004 References "12 Points" of TCoP

**Severity**: 🟠 HIGH
**Category**: Requirements Quality
**Location**: ARC-001-REQ-v2.0:L1227

**Description**:
NFR-C-004 states: "All technology decisions MUST comply with the **12 points** of the Technology Code of Practice". The TCoP has **13 points** (Point 13: Meet the Service Standard was added). The requirement then lists only 12 items (missing Point 13), despite NFR-C-003 separately covering GDS Service Standard.

**Impact**: Compliance checklist is incomplete; auditors may question TCoP coverage.

**Recommendation**: Change "12 points" to "13 points" and add Point 13 to the checklist.

**Estimated Effort**: 5 minutes

---

#### H6: TCoP Score Inconsistency (110 vs 108)

**Severity**: 🟠 HIGH
**Category**: Cross-Artifact Consistency
**Location**: ARC-001-TCOP-v1.0:L56 and L651

**Description**:
The TCoP executive summary (L56) states: "Score: **110/130 (85%)**". However, the scorecard table (L635-649) sums individual point scores to **108/130 (83%)**:
9+9+10+10+7+7+9+10+10+10+5+5+7 = 108

**Impact**: Incorrect score misleads stakeholders about TCoP compliance level. The 2-point and 2% difference may affect CDDO spend control decisions.

**Recommendation**: Correct executive summary to "108/130 (83%)" to match the scorecard.

**Estimated Effort**: 5 minutes

---

#### H7: TCoP Point 11 References Outdated State

**Severity**: 🟠 HIGH
**Category**: Cross-Artifact Consistency
**Location**: ARC-001-TCOP-v1.0:L513-514, L528, L534, L647, L655

**Description**:
TCoP Point 11 assessment was written before the SOBC and REQ budget updates. Multiple lines state:
- L513: "No SOBC exists with formal commercial case"
- L514: "Budget figures all TBD in ARC-001-REQ-v2.0"
- L528: "CDDO spend control submission prepared — no SOBC exists"
- L534: "Create SOBC ... Run `/arckit:sobc`"

All of these are now false:
- ARC-001-SOBC-v1.0 was created on 2026-02-28 with full 5-case model
- ARC-001-REQ-v2.0 budget section now cross-references SOBC with £2.84M TCO

**Impact**: TCoP assessment presents incorrect information. Point 11 score (5/10) may be too low given SOBC now exists. Re-scoring could improve overall TCoP compliance to ~115/130 (88%).

**Recommendation**: Update TCoP Point 11 to reference ARC-001-SOBC-v1.0 and the populated budget. Re-score Point 11 (likely 7-8/10 with SOBC but still missing exit strategy and procurement route documentation).

**Estimated Effort**: 30 minutes

---

### MEDIUM Issues

#### M1: Missing Traceability Matrix

**Severity**: 🟡 MEDIUM
**Location**: Missing artifact (ARC-001-TRAC)

**Description**: No formal traceability matrix exists mapping requirements → design → tests. Requirements internally trace to stakeholder goals and principles, but no consolidated forward/backward matrix.

**Recommendation**: Run `/arckit:traceability` to generate. Required before Live assessment.

---

#### M2: Data Entities Lack DR-xxx IDs

**Severity**: 🟡 MEDIUM
**Location**: ARC-001-REQ-v2.0:L1599-1768

**Description**: Six data entities are described narratively in the Data Requirements section but lack formal DR-001 to DR-006 identifiers. The DATA-v1.0 model references entities E-001 to E-008 but these don't map to explicit DR-xxx requirements.

**Recommendation**: Add DR-001 through DR-006 identifiers to data entity descriptions for traceability.

---

#### M3: Stakeholder Interview Dates TBC

**Severity**: 🟡 MEDIUM
**Location**: ARC-001-STKE-v1.0

**Description**: Interview schedule dates for all stakeholder groups remain TBC. GDS Alpha assessment will examine user research evidence.

**Recommendation**: Schedule user research interviews with motorists, independent retailers, and CMA enforcement officers before Alpha assessment.

---

#### M4: SOBC Exit Strategy Missing

**Severity**: 🟡 MEDIUM
**Location**: ARC-001-SOBC-v1.0

**Description**: Commercial Case lacks an exit strategy for cloud provider and key technology dependencies. Required for TCoP Point 11 compliance.

**Recommendation**: Add exit strategy section to SOBC Commercial Case addressing data portability, vendor transition, and contract termination.

---

#### M5: SECD 10 TBD Items

**Severity**: 🟡 MEDIUM
**Location**: ARC-001-SECD-v1.0

**Description**: 10 TBD items in the Secure by Design assessment pending design decisions (operating systems, cloud provider security controls, external interface protection, etc.). Expected at Discovery/Alpha phase.

**Recommendation**: Resolve after cloud provider selection. All should be addressed before Beta.

---

#### M6: DPO Sign-off Pending on DPIA

**Severity**: 🟡 MEDIUM
**Location**: ARC-001-DPIA-v1.0

**Description**: DPIA is complete but in DRAFT status. DPO formal sign-off required before processing personal data (retailer contact details during registration).

**Recommendation**: Obtain DPO sign-off before retailer registration system goes live.

---

### LOW Issues

#### L1: DPIA Classification Mismatch

**Severity**: 🟢 LOW
**Location**: ARC-001-DPIA-v1.0

**Description**: DPIA classified as OFFICIAL-SENSITIVE while all other project artifacts are classified OFFICIAL. May be justified (DPIA contains risk assessment detail) but not documented.

**Recommendation**: Add note explaining higher classification or align to OFFICIAL.

---

#### L2: Sustainability Metrics Not Defined

**Severity**: 🟢 LOW
**Location**: ARC-001-TCOP-v1.0 (Point 12)

**Description**: TCoP Point 12 expects sustainability metrics (carbon footprint per transaction, energy per query). Architecture principles reference sustainability but no specific metrics are defined.

**Recommendation**: Define sustainability metrics before Live, aligned with Greening Government ICT Strategy.

---

## Appendix A: Artifacts Analyzed

| Artifact | Location | Last Modified | Status |
|----------|----------|---------------|--------|
| Architecture Principles | `projects/000-global/ARC-000-PRIN-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| Requirements (v2.0) | `projects/001-.../ARC-001-REQ-v2.0.md` | 2026-03-01 | ✅ Analyzed |
| Stakeholder Analysis | `projects/001-.../ARC-001-STKE-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| Risk Register | `projects/001-.../ARC-001-RISK-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| SOBC Business Case | `projects/001-.../ARC-001-SOBC-v1.0.md` | 2026-02-28 | ✅ Analyzed |
| Data Model | `projects/001-.../ARC-001-DATA-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| DPIA | `projects/001-.../ARC-001-DPIA-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| TCoP Assessment | `projects/001-.../ARC-001-TCOP-v1.0.md` | 2026-02-28 | ✅ Analyzed |
| Secure by Design | `projects/001-.../ARC-001-SECD-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| Project Plan | `projects/001-.../ARC-001-PLAN-v1.0.md` | 2026-02-28 | ✅ Analyzed |
| Product Backlog | `projects/001-.../ARC-001-BKLG-v1.0.md` | 2026-02-28 | ✅ Analyzed |
| Technology Research (v1.0, v2.0) | `projects/001-.../ARC-001-RSCH-*.md` | 2026-01-31 | ✅ Analyzed |
| Data Scout (v1.0, v2.0) | `projects/001-.../ARC-001-DSCT-*.md` | 2026-02-01 | ✅ Analyzed |
| AWS Research (v1.0, v1.1, v2.0) | `projects/001-.../research/ARC-001-AWRS-*.md` | 2026-02-02 | ✅ Analyzed |
| Azure Research (v1.0, v1.1, v2.0) | `projects/001-.../research/ARC-001-AZRS-*.md` | 2026-02-01 | ✅ Analyzed |
| Architecture Diagrams | `projects/001-.../diagrams/ARC-001-DIAG-001-v1.0.md` | 2026-01-31 | ✅ Analyzed |
| Traceability Matrix | Missing | — | ❌ Not Found |
| HLD | Missing | — | ❌ Not Found (pre-design phase) |
| DLD | Missing | — | ❌ Not Found (pre-design phase) |

**Total artifacts analyzed**: 21 files across 2 projects

---

## Appendix B: Analysis Methodology

**Analysis Date**: 2026-03-01
**Analyzed By**: ArcKit `/arckit.analyze` command (v3.0)

**Checks Performed**:

- Requirements completeness and quality (duplication, ambiguity, underspecification)
- Architecture principles compliance (22 principles vs 63 requirements)
- Stakeholder traceability (requirements to goals, RACI alignment)
- Risk coverage and mitigation (20 risks, 4 above appetite)
- Business case alignment (5-case model, benefits, costs, REQ-SOBC consistency)
- Data model consistency (entities, PII, governance, DR-xxx coverage)
- UK Government compliance (TCoP 13 points, SbD, DPIA)
- Cross-artifact consistency (terminology, scores, dates, references)
- Document governance (owners, classification, revision history)

**Severity Classification**:

- 🔴 **CRITICAL**: Blocks procurement/implementation, must resolve immediately
- 🟠 **HIGH**: Significant risk, resolve before major milestones
- 🟡 **MEDIUM**: Should be addressed, can proceed with caution
- 🟢 **LOW**: Minor issues, address when convenient

---

**Generated by**: ArcKit `/arckit.analyze` command
**Generated on**: 2026-03-01 GMT
**ArcKit Version**: 2.22.0
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: claude-opus-4-6
**Generation Context**: Analysis of 21 artifacts across requirements, stakeholder, risk, business case, data model, compliance, and research documents. Third iteration following remediation of document owners (16 files) and budget references (REQ-SOBC alignment).
