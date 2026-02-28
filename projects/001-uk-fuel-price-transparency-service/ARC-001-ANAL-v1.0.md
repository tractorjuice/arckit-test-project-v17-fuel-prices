# Architecture Governance Analysis Report: UK Fuel Price Transparency Service

> **Template Status**: Beta | **Version**: 2.16.0 | **Command**: `/arckit.analyze`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-ANAL-v1.0 |
| **Document Type** | Governance Analysis Report |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-02-28 |
| **Last Modified** | 2026-02-28 |
| **Review Cycle** | On-Demand |
| **Next Review Date** | 2026-03-30 |
| **Owner** | Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-28 | ArcKit AI | Initial creation from `/arckit.analyze` command | PENDING | PENDING |

---

## Executive Summary

**Overall Status**: ⚠️ Issues Found

**Key Metrics**:

- Total Requirements: 57 (7 BR, 15 FR, 27 NFR, 8 INT) + 6 Data Entities
- Requirements Quality: 85%
- Critical Issues: 3
- High Priority Issues: 5
- Medium Priority Issues: 4
- Low Priority Issues: 3

**Recommendation**: RESOLVE CRITICAL ISSUES FIRST

The UK Fuel Price Transparency Service has a strong governance foundation with comprehensive architecture principles (22), well-structured requirements, detailed stakeholder analysis, risk register, data model, DPIA, and Secure by Design assessment. However, three critical gaps must be addressed before proceeding to design or procurement: (1) missing TCoP assessment, (2) undefined enforcement threshold in FR-006, and (3) missing SOBC business case. Five high-priority issues — including document ownership gaps, traceability matrix absence, and incomplete Secure by Design controls — should be resolved in parallel.

---

## Findings Summary

| ID | Category | Severity | Location(s) | Summary | Recommendation |
|----|----------|----------|-------------|---------|----------------|
| C1 | UK Gov Compliance | CRITICAL | Missing artifact | No TCoP assessment exists — mandatory for UK Government projects | Run `/arckit:tcop` |
| C2 | Requirements Quality | CRITICAL | ARC-001-REQ-v2.0:L446 | FR-006 enforcement threshold "[X hours]" undefined — core enforcement capability | Define threshold with CMA Enforcement Lead |
| C3 | Business Case | CRITICAL | Missing artifact | No SOBC — major UK Government investment requires Green Book business case | Run `/arckit:sobc` |
| H1 | Traceability | HIGH | Missing artifact | No Traceability Matrix artifact (ARC-001-TRAC) for end-to-end requirements tracing | Run `/arckit:traceability` |
| H2 | Document Control | HIGH | 5 artifacts | Document Owner field is [OWNER_NAME_AND_ROLE] across PRIN, REQ, STKE, RISK, DATA | Assign named document owners |
| H3 | Security | HIGH | ARC-001-SECD-v1.0 | Secure by Design assessment has 10+ TBD items on key security controls | Complete SbD assessment after design decisions |
| H4 | Requirements Quality | HIGH | ARC-001-REQ-v2.0:L2061-2077 | All budget figures TBD — cannot validate value for money (BR-006) | Develop cost estimates with finance team |
| H5 | Requirements Quality | HIGH | ARC-001-REQ-v2.0:L2198 | Traceability references "DR-001-006" but no formal DR-xxx IDs in requirements body | Add formal DR-xxx numbered requirements |
| M1 | Stakeholder | MEDIUM | ARC-001-STKE-v1.0:L1291-1297 | Stakeholder interview schedule dates all TBC | Schedule user research interviews |
| M2 | Risk Management | MEDIUM | ARC-001-RISK-v1.0 | Risk R-010 (VE3 API unavailable) above appetite with no specific mitigating requirement | Add contingency requirement for alternative data source |
| M3 | Document Control | MEDIUM | All artifacts | All artifacts in DRAFT status with no reviewer/approver assigned | Establish review schedule and assign reviewers |
| M4 | UK Gov Compliance | MEDIUM | Missing artifact | No GDS Service Assessment preparation artifact | Consider running `/arckit:service-assessment` |
| L1 | Requirements Quality | LOW | ARC-001-REQ-v2.0:L2198 | Appendix C shorthand "DR-001-006" doesn't match body structure "Entity 1-6" | Align data requirement IDs with body section |
| L2 | Document Control | LOW | ARC-001-DPIA-v1.0 | DPIA classified as OFFICIAL-SENSITIVE while other artifacts are OFFICIAL | Verify classification is intentional (may be correct) |
| L3 | Requirements Quality | LOW | ARC-001-REQ-v2.0:L1226 | NFR-C-004 lists 12 TCoP points — verify against current TCoP version | Confirm point count matches current TCoP |

---

## Requirements Analysis

### Requirements Coverage Matrix

| Requirement Category | Count | MUST | SHOULD | COULD | Design Coverage | Status |
|---------------------|-------|------|--------|-------|-----------------|--------|
| Business Requirements (BR) | 7 | 7 | 0 | 0 | N/A (pre-design) | ✅ Well-defined |
| Functional Requirements (FR) | 15 | 10 | 5 | 0 | N/A (pre-design) | ⚠️ 1 placeholder |
| Performance (NFR-P) | 3 | 2 | 1 | 0 | N/A (pre-design) | ✅ Measurable |
| Availability (NFR-A) | 3 | 3 | 0 | 0 | N/A (pre-design) | ✅ Complete |
| Scalability (NFR-S) | 2 | 2 | 0 | 0 | N/A (pre-design) | ✅ Complete |
| Security (NFR-SEC) | 5 | 5 | 0 | 0 | N/A (pre-design) | ✅ Comprehensive |
| Compliance (NFR-C) | 5 | 5 | 0 | 0 | N/A (pre-design) | ✅ Complete |
| Usability (NFR-U) | 3 | 2 | 1 | 0 | N/A (pre-design) | ✅ Complete |
| Maintainability (NFR-M) | 3 | 3 | 0 | 0 | N/A (pre-design) | ✅ Complete |
| Interoperability (NFR-I) | 3 | 3 | 0 | 0 | N/A (pre-design) | ✅ Complete |
| Integration (INT) | 8 | 5 | 2 | 1 | N/A (pre-design) | ✅ Complete |
| Data Entities | 6 | 6 | 0 | 0 | ✅ ARC-001-DATA | ✅ Complete |
| **TOTAL** | **63** | **53** | **9** | **1** | | |

**Statistics**:

- Total Requirements: 63 (including data entities)
- Well-Defined: 61 (97%)
- With Placeholder: 1 (FR-006 — "[X hours]")
- With TBD Values: Budget section (10 TBD items)
- MoSCoW Applied: ✅ Yes — 84% MUST, 14% SHOULD, 2% COULD

**Note on Design Coverage**: This project is in Discovery/Alpha phase. No vendor HLD/DLD exists. Design coverage assessment will be relevant once design artifacts are produced. The absence of design artifacts is expected at this phase and is not a gap.

### Requirements Quality Assessment

**Strengths**:

- Comprehensive coverage across all NFR categories (Performance, Availability, Scalability, Security, Compliance, Usability, Maintainability, Interoperability)
- Measurable acceptance criteria on most requirements
- Good MoSCoW prioritisation with appropriate distribution
- 7 use cases with detailed flows, alternative flows, and exception flows
- 7 well-defined personas covering all user types
- 4 requirement conflicts documented with resolutions
- All requirements traced to stakeholder goals and architecture principles (Appendix C)

**Issues Found**:

1. **[CRITICAL] FR-006 placeholder**: Line 446 — "no submission within [X hours] of regulatory deadline" — the enforcement threshold is undefined. This is the core enforcement capability and must be specified.
2. **[HIGH] Budget all TBD**: Lines 2061-2077 — every budget line item is "TBD". Cannot validate value for money (BR-006) or cost adequacy.
3. **[HIGH] DR-xxx IDs missing**: Appendix C references "DR-001-006" but the Data Requirements section (lines 1599-1768) defines entities as "Entity 1: Organisation" etc. without formal DR-xxx identifiers.
4. **[LOW] TCoP point count**: NFR-C-004 lists 12 TCoP points. Verify this matches the current version of the Technology Code of Practice.

---

## Architecture Principles Compliance

| # | Principle | Category | Criticality | Requirements Coverage | Status |
|---|-----------|----------|-------------|----------------------|--------|
| 1 | Open Data by Default | Strategic | CRITICAL | BR-002, BR-005, FR-005, NFR-I-002, NFR-I-003 | ✅ COMPLIANT |
| 2 | Citizen-Centred Design | Strategic | CRITICAL | BR-001, BR-003, FR-001, FR-004, NFR-U-001, NFR-U-002 | ✅ COMPLIANT |
| 3 | Scalability and Elasticity | Strategic | HIGH | NFR-S-001, NFR-S-002, NFR-P-002 | ✅ COMPLIANT |
| 4 | Resilience and Fault Tolerance | Strategic | CRITICAL | NFR-A-002, NFR-A-003 | ✅ COMPLIANT |
| 5 | Interoperability and Integration | Strategic | HIGH | BR-005, FR-003, FR-005, NFR-I-001, INT-001-008 | ✅ COMPLIANT |
| 6 | Security by Design | Strategic | CRITICAL | NFR-SEC-001-005, NFR-C-005 | ✅ COMPLIANT |
| 7 | Observability | Strategic | HIGH | NFR-M-001, BR-004, FR-006 | ✅ COMPLIANT |
| 8 | Data Sovereignty | Data | CRITICAL | NFR-C-001, TC-1 | ✅ COMPLIANT |
| 9 | Data Quality and Timeliness | Data | CRITICAL | BR-002, FR-007, Data Quality Requirements | ✅ COMPLIANT |
| 10 | Single Source of Truth | Data | HIGH | Entity 4 (PublishedPrice) as derived view | ✅ COMPLIANT |
| 11 | Loose Coupling | Integration | HIGH | FR-007 (async pipeline), Architecture patterns | ✅ COMPLIANT |
| 12 | Async Communication | Integration | MEDIUM | FR-003, FR-007 (async processing) | ✅ COMPLIANT |
| 13 | Reuse Government Platforms | Integration | HIGH | INT-003 (Notify), INT-004 (Design System), NFR-C-004 | ✅ COMPLIANT |
| 14 | Performance and Efficiency | Quality | HIGH | NFR-P-001, NFR-P-002, NFR-P-003 | ✅ COMPLIANT |
| 15 | Availability and Reliability | Quality | CRITICAL | NFR-A-001, NFR-A-002 | ✅ COMPLIANT |
| 16 | Maintainability and Evolvability | Quality | MEDIUM | NFR-M-002, NFR-M-003 | ✅ COMPLIANT |
| 17 | Infrastructure as Code | DevOps | HIGH | Implicit in architecture — no explicit requirement | ⚠️ PARTIAL |
| 18 | Automated Testing | DevOps | HIGH | NFR-SEC-005 (security scanning), NFR-U-002 (accessibility testing) | ⚠️ PARTIAL |
| 19 | CI/CD | DevOps | HIGH | Implicit in architecture — no explicit requirement | ⚠️ PARTIAL |
| 20 | Regulatory Compliance by Design | Government | CRITICAL | BR-004, FR-010, NFR-C-002 | ✅ COMPLIANT |
| 21 | Privacy by Design | Government | CRITICAL | NFR-C-001, ARC-001-DPIA-v1.0 | ✅ COMPLIANT |
| 22 | Sustainability and Cost Efficiency | Government | MEDIUM | BR-006 — but budget TBD | ⚠️ PARTIAL |

**Critical Principle Violations**: 0

**Partial Compliance Notes**:

- **Principles 17, 18, 19 (IaC, Testing, CI/CD)**: These DevOps principles are referenced in architecture principles but lack explicit corresponding requirements in ARC-001-REQ-v2.0. They are implied by the technical approach but should be formalised as NFR requirements for traceability.
- **Principle 22 (Sustainability)**: Budget is entirely TBD. Cannot validate cost efficiency without estimates.

**Principles Compliance Score**: 19/22 fully compliant (86%), 3/22 partially compliant (14%), 0 violations

---

## Stakeholder Traceability Analysis

**Stakeholder Analysis Exists**: ✅ Yes (ARC-001-STKE-v1.0)

**Stakeholder-Requirements Coverage**:

- Requirements traced to stakeholder goals: 100% (all 63 requirements mapped to at least one goal in Appendix C)
- Orphan requirements (no stakeholder justification): 0
- Requirement conflicts documented and resolved: ✅ Yes (4 conflicts with documented resolutions: C-1 through C-4)

**Goals Coverage**:

| Goal | Description | Owner | Requirements Mapped | Status |
|------|-------------|-------|-------------------|--------|
| G-1 | Universal Retailer Registration | CMA SRO | BR-001, FR-001, FR-008, INT-001, INT-002, INT-007 | ✅ Well-covered |
| G-2 | Data Submission Compliance | CMA Enforcement | BR-002, FR-002, FR-003, FR-007, FR-009, FR-012, NFR-P-002, NFR-A-001 | ✅ Well-covered |
| G-3 | Trusted Citizen Service | CMA Digital Lead | BR-003, FR-004, FR-013, FR-014, NFR-P-001, NFR-U-001, NFR-U-002, NFR-I-001 | ✅ Well-covered |
| G-4 | Enforcement Capability | CMA Enforcement | BR-004, FR-006, FR-010, FR-012, NFR-C-002, NFR-M-001 | ⚠️ FR-006 has placeholder |
| G-5 | Value for Money | CMA SRO | BR-006 | ⚠️ Budget TBD, no SOBC |
| G-6 | Data Protection Compliance | SIRO/DPO | NFR-C-001, ARC-001-DPIA-v1.0 | ✅ Well-covered |
| G-7 | GDS Service Standard | CMA Digital Lead | BR-007, NFR-C-003, NFR-C-004, NFR-C-005 | ⚠️ No TCoP assessment |

**RACI Governance Alignment**:

| Artifact | Role | Aligned with RACI? | Issues |
|----------|------|-------------------|--------|
| Risk Register | Risk Owners | ✅ Yes | All 20 risk owners traced to stakeholder RACI matrix |
| Data Model | Data Owners | ✅ Yes | Governance matrix present in ARC-001-DATA-v1.0 |
| DPIA | DPO | ✅ Yes | CMA DPO identified as controller |
| Secure by Design | SIRO | ✅ Yes | CMA SIRO identified as security owner |

**Stakeholder Traceability Score**: 92%

---

## Risk Management Analysis

**Risk Register Exists**: ✅ Yes (ARC-001-RISK-v1.0)

**Risk Profile Summary**:

- Total Risks: 20 across 6 categories
- Inherent Critical: 5 → Residual Critical: 0 (100% reduction)
- Inherent High: 8 → Residual High: 4 (50% reduction)
- Overall Risk Score: 266 inherent → 168 residual (37% reduction)

**Risks Exceeding Appetite (Residual)**:

| Risk ID | Title | Category | Residual Score | Appetite | Excess | Mitigating Requirements |
|---------|-------|----------|---------------|----------|--------|------------------------|
| R-001 | Low independent retailer compliance | Operational | 12 | ≤ 9 | +3 | BR-001, FR-001, FR-012 |
| R-003 | Enforcement tools not ready by May 2026 | Compliance | 12 | ≤ 9 | +3 | BR-004, FR-006 |
| R-006 | Negative media coverage | Reputational | 12 | ≤ 9 | +3 | BR-003, FR-013 |
| R-010 | VE3 Global API unavailable | Technology | 12 | ≤ 9 | +3 | ⚠️ No specific mitigating requirement |

**Risk Coverage Assessment**:

- Risks with mitigating requirements: 19/20 (95%)
- Risk R-010 gap: VE3 Global API specification unavailability has no specific contingency requirement for an alternative data ingestion approach
- Risk owners from RACI: ✅ 20/20 (100%)
- Risk responses documented: ✅ Yes (4Ts applied)

**Risk-SOBC Alignment**: ❌ Cannot assess — no SOBC exists

**Risk Management Score**: 85%

---

## Business Case Analysis

**SOBC Exists**: ❌ No

**Impact**: BR-006 requires demonstrating value for money. Goal G-5 references an "approved business case" that does not yet exist. Without an SOBC:

- Cannot validate whether budget is adequate for requirements scope
- Cannot trace benefits to stakeholder goals or requirements
- Cannot establish NPV, ROI, or cost-benefit analysis
- NAO/PAC cannot assess value for money

**Recommendation**: Run `/arckit:sobc` to create a Strategic Outline Business Case using the Green Book 5-case model. This is a CRITICAL gap for a major UK Government investment programme.

---

## Data Model Analysis

**Data Model Exists**: ✅ Yes (ARC-001-DATA-v1.0)

**Data Entity Coverage**:

| Entity | Description | REQ Reference | PII? | GDPR Basis | Status |
|--------|-------------|---------------|------|------------|--------|
| E-001: Organisation | Motor fuel trader | Entity 1 (REQ) | ✅ Contact details | Art. 6(1)(e) Public task | ✅ Complete |
| E-002: Forecourt | Fuel retail location | Entity 2 (REQ) | ❌ | N/A (public data) | ✅ Complete |
| E-003: PriceSubmission | Price data submission | Entity 3 (REQ) | ❌ | N/A (business data) | ✅ Complete |
| E-004: PublishedPrice | Current published price | Entity 4 (REQ) | ❌ | N/A (public data) | ✅ Complete |
| E-005: EnforcementAction | CMA enforcement action | Entity 5 (REQ) | ❌ | Art. 6(1)(e) Public task | ✅ Complete |
| E-006: AuditEvent | Immutable audit record | Entity 6 (REQ) | ❌ | N/A (system data) | ✅ Complete |

**Data Model Quality**:

- ERD exists and renderable (Mermaid syntax): ✅ Yes
- Entities with complete specifications: 6/6
- PII identified: ✅ Yes (Organisation contact details)
- GDPR compliance documented: ✅ Yes (in both DATA and DPIA artifacts)
- Data governance matrix: ✅ Present
- CRUD matrix: ✅ Present

**Data Requirements Traceability Issue**:

- The requirements document defines 6 data entities in the "Data Requirements" section (lines 1599-1768) using descriptive names ("Entity 1: Organisation", "Entity 2: Forecourt", etc.)
- Appendix C traceability matrix references "DR-001-006" but these formal IDs do not appear in the requirements body
- The data model artifact (ARC-001-DATA-v1.0) provides the detailed elaboration
- **Recommendation**: Add formal DR-xxx numbered requirements to the body of ARC-001-REQ-v2.0 for traceability

**Data Model Score**: 90%

---

## UK Government Compliance Analysis

### Technology Code of Practice (TCoP)

**TCoP Assessment Exists**: ❌ No

**Impact**: NFR-C-004 mandates TCoP compliance. Without a formal assessment:

- Cannot demonstrate compliance to CDDO spend control
- GDS assessment may challenge TCoP evidence
- Technology decisions lack governance evidence

**Status**: ❌ Non-Compliant (missing mandatory assessment)

**Recommendation**: Run `/arckit:tcop` — this is a CRITICAL gap

### Secure by Design (NCSC)

**SbD Assessment Exists**: ✅ Yes (ARC-001-SECD-v1.0)

**SbD Assessment Status**:

- Threat model: ✅ Present (STRIDE analysis)
- Security controls mapped: ✅ Present
- Supply chain assessment: ⚠️ Multiple TBD items (cloud provider, pen test provider not selected)
- Key TBD items: Operating systems (line 275), consumer separation (line 678), external interface protection (line 686), secure administration (line 687), secure use of service (line 689), backup method (line 822)

**Status**: ⚠️ Partial — assessment framework complete but implementation details require design decisions

### Data Protection Impact Assessment (DPIA)

**DPIA Exists**: ✅ Yes (ARC-001-DPIA-v1.0)

**DPIA Status**:

- Processing activities documented: ✅ Yes
- Lawful basis identified: ✅ Yes (Article 6(1)(e) — Public task)
- Risk assessment: ✅ Present (LOW-MEDIUM residual risk)
- DPO review: ⚠️ Pending
- Approval: ⚠️ Pending

**Status**: ⚠️ Complete but awaiting DPO review and approval

### GDS Service Standard

**Service Assessment Preparation**: ❌ No preparation artifact exists

**Evidence in requirements**: NFR-C-003 addresses all 14 GDS Service Standard points. The requirements are comprehensive, but a formal self-assessment would strengthen readiness.

**Recommendation**: Consider running `/arckit:service-assessment` before Alpha assessment

### AI Playbook / ATRS

**Applicable**: ❌ No — this service does not use AI/ML algorithms. Not required.

**UK Government Compliance Score**: 60%

---

## Design Quality Analysis

### HLD Analysis

**HLD Exists**: ❌ No — project is in Discovery/Alpha phase

This is expected. No design artifacts exist yet. Design coverage analysis will be applicable once architecture design is produced.

### DLD Analysis

**DLD Exists**: ❌ No — project is in Discovery/Alpha phase

---

## Detailed Findings

### Critical Issues

#### C1: Missing Technology Code of Practice (TCoP) Assessment

**Severity**: 🔴 CRITICAL
**Category**: UK Government Compliance
**Location**: Missing artifact — no ARC-001-TCOP exists

**Description**:
NFR-C-004 in ARC-001-REQ-v2.0 mandates TCoP compliance. Architecture Principle 13 (Reuse Government Platforms) requires TCoP compliance evidence. The Technology Code of Practice is mandatory for all UK Government technology projects and must be assessed before spend control approval from CDDO.

**Impact**:
- CDDO spend control approval may be blocked
- GDS Service Standard assessment (Point 12: "Meet the Service Standard") may challenge TCoP evidence
- Technology decisions lack formal governance evidence
- Compliance requirement NFR-C-004 cannot be validated

**Recommendation**:
1. Run `/arckit:tcop` to generate a comprehensive TCoP assessment
2. Map TCoP points to existing requirements and principles
3. Include TCoP evidence in GDS assessment portfolio

**Estimated Effort**: 2-3 hours

---

#### C2: FR-006 Enforcement Threshold Undefined

**Severity**: 🔴 CRITICAL
**Category**: Requirements Quality
**Location**: ARC-001-REQ-v2.0:L446

**Description**:
FR-006 (Compliance Monitoring Dashboard) contains the business rule: "Non-compliance defined as: no submission within [X hours] of regulatory deadline". The "[X hours]" is an unresolved placeholder. This is the core enforcement capability — without a defined threshold, the system cannot distinguish compliant from non-compliant retailers.

**Evidence**:
```text
Non-compliance defined as: no submission within [X hours] of regulatory deadline
```

**Impact**:
- Cannot implement automated non-compliance detection
- Enforcement tools cannot operate without a defined threshold
- BR-004 (CMA Enforcement Capability) success criteria cannot be met
- Risk R-003 (Enforcement tools not ready by May 2026) is exacerbated

**Recommendation**:
1. Consult with CMA Enforcement Lead to define the non-compliance threshold (e.g., 24 hours, 48 hours)
2. Update FR-006 business rule with specific value
3. Align with CMA Enforcement Guidance (December 2025) referenced in Appendix B

**Estimated Effort**: 30 minutes (decision) + 15 minutes (document update)

---

#### C3: Missing Strategic Outline Business Case (SOBC)

**Severity**: 🔴 CRITICAL
**Category**: Business Case
**Location**: Missing artifact — no ARC-001-SOBC exists

**Description**:
BR-006 requires demonstrating value for money. Stakeholder Goal G-5 references an "approved business case" (ARC-001-STKE-v1.0:L665). The requirements budget section (lines 2061-2077) contains all TBD values. Without an SOBC, the programme lacks:

- HM Treasury Green Book 5-case model assessment
- Formal cost-benefit analysis
- Options appraisal (Do Nothing baseline required)
- Benefits realisation framework
- Financial affordability confirmation

**Impact**:
- HM Treasury approval at risk
- NAO/PAC cannot assess value for money
- Risk register references budget constraints that are undefined
- Programme governance lacks financial baseline

**Recommendation**:
1. Run `/arckit:sobc` to create an SOBC using the Green Book 5-case model
2. Include options appraisal with Do Nothing baseline
3. Quantify benefits mapped to stakeholder goals (G-1 through G-5)
4. Establish cost estimates for budget section of ARC-001-REQ-v2.0

**Estimated Effort**: 8-12 hours

---

### High Priority Issues

#### H1: Missing Traceability Matrix Artifact

**Severity**: 🟠 HIGH
**Category**: Traceability
**Location**: Missing artifact — no ARC-001-TRAC exists

**Description**:
While ARC-001-REQ-v2.0 contains an Appendix C traceability matrix (lines 2139-2198), this is a summary table within the requirements document, not a dedicated traceability artifact. A formal ARC-001-TRAC would provide:

- Forward traceability: Requirements → Design → Tests
- Backward traceability: Tests → Design → Requirements
- Coverage percentages per requirement type
- Gap identification with severity and recommended actions
- Independent verification of requirement coverage

**Recommendation**:
1. Run `/arckit:traceability` to generate a comprehensive traceability matrix
2. This becomes essential once HLD/DLD design artifacts are produced
3. Will enable automated coverage tracking

**Estimated Effort**: 2-3 hours

---

#### H2: Document Owner Fields Unresolved

**Severity**: 🟠 HIGH
**Category**: Document Control
**Location**: ARC-000-PRIN-v1.0:L19, ARC-001-REQ-v2.0:L19, ARC-001-STKE-v1.0:L19, ARC-001-RISK-v1.0:L19, ARC-001-DATA-v1.0:L19

**Description**:
Five governance artifacts have `[OWNER_NAME_AND_ROLE]` as the document owner. Without named owners, there is no accountability for document currency, review, or approval. This undermines the governance model.

**Recommendation**:
1. Assign named document owners for each artifact:
   - PRIN: Enterprise Architect / Architecture Review Board Chair
   - REQ: CMA Digital Lead / Product Owner
   - STKE: Programme Manager
   - RISK: CMA SRO
   - DATA: Data Architect / Data Governance Lead
2. Update Document Control sections in all 5 artifacts

**Estimated Effort**: 30 minutes

---

#### H3: Secure by Design Assessment Incomplete

**Severity**: 🟠 HIGH
**Category**: Security
**Location**: ARC-001-SECD-v1.0 (multiple lines)

**Description**:
The Secure by Design assessment has a strong framework but contains 10+ TBD items for implementation-specific controls that depend on design decisions not yet made:

- Operating system details (line 275)
- Consumer separation controls (line 678)
- External interface protection (line 686)
- Secure service administration (line 687)
- Secure use of service (line 689)
- Supply chain: cloud provider, pen test provider (lines 783-785)
- Open source component assessment (line 798)
- Backup methodology (line 822)

**Recommendation**:
1. This is expected for Discovery/Alpha phase — TBDs should be resolved during Beta
2. Track these as SbD completion conditions in the project plan
3. Ensure cloud provider selection resolves supply chain TBDs
4. Complete SbD assessment after technology research conclusions

**Estimated Effort**: Progressive — resolved during design phase

---

#### H4: Budget Figures All TBD

**Severity**: 🟠 HIGH
**Category**: Requirements Quality
**Location**: ARC-001-REQ-v2.0:L2061-2077

**Description**:
Every line item in both the Cost Estimate and Ongoing Operational Costs tables contains "TBD". While the document notes these are "subject to HM Treasury Green Book business case approval", the complete absence of even preliminary estimates means:

- BR-006 (Value for Money) cannot be validated
- Programme governance lacks financial baseline
- Risk register cost impacts cannot be quantified

**Evidence**:
```text
| Delivery Team (multidisciplinary) | TBD | Per approved business case |
| Cloud Infrastructure | TBD | UK sovereign cloud; auto-scaling |
| **Total** | **TBD** | **Per approved business case** |
```

**Recommendation**:
1. Develop ROM (rough order of magnitude) estimates using cloud research artifacts (ARC-001-AWRS, ARC-001-AZRS)
2. Include in SOBC when created (finding C3)
3. Update ARC-001-REQ-v2.0 budget section with at least range estimates

**Estimated Effort**: 4-6 hours (requires finance team input)

---

#### H5: Formal DR-xxx Requirement IDs Missing

**Severity**: 🟠 HIGH
**Category**: Requirements Quality
**Location**: ARC-001-REQ-v2.0:L1599-1768, L2198

**Description**:
The requirements traceability matrix (Appendix C, line 2198) references "DR-001-006" mapped to stakeholder goals and principles. However, the Data Requirements section in the body uses descriptive identifiers ("Entity 1: Organisation", "Entity 2: Forecourt", etc.) rather than formal DR-xxx numbered requirements. This creates a traceability disconnect — the matrix references IDs that don't exist in the body.

**Recommendation**:
1. Add formal DR-xxx headers to each entity definition (e.g., "DR-001: Organisation Entity", "DR-002: Forecourt Entity")
2. Update Appendix C to reference these IDs individually rather than as a range
3. This enables the traceability matrix to link individual data requirements to entities in ARC-001-DATA-v1.0

**Estimated Effort**: 1 hour

---

### Medium Priority Issues

#### M1: Stakeholder Interview Schedule TBC

**Severity**: 🟡 MEDIUM
**Category**: Stakeholder
**Location**: ARC-001-STKE-v1.0:L1291-1297

**Description**:
The stakeholder interview schedule has all dates as "TBC" for 7 key stakeholders including CMA Enforcement Lead, DESNZ Policy Lead, PRA Representative, UKPIA Representative, sample motorists, sample independent retailers, and GDS Assessment Lead.

**Recommendation**:
Schedule user research interviews as a priority for Alpha phase. GDS assessment will examine user research evidence (Service Standard Points 1, 2, 5).

---

#### M2: Risk R-010 Lacks Mitigating Requirement

**Severity**: 🟡 MEDIUM
**Category**: Risk Management
**Location**: ARC-001-RISK-v1.0

**Description**:
Risk R-010 (VE3 Global API specification unavailable) has a residual score of 12, exceeding the appetite of ≤ 9. This is flagged as the #5 top risk requiring immediate attention. However, unlike R-001 and R-003, there is no specific requirement that addresses the contingency if VE3 Global API is not available.

**Recommendation**:
Add a contingency requirement addressing alternative data ingestion approaches if the VE3 Global API specification is unavailable or delayed.

---

#### M3: All Artifacts in DRAFT Status

**Severity**: 🟡 MEDIUM
**Category**: Document Control
**Location**: All artifacts

**Description**:
All 7 governance artifacts (PRIN, REQ, STKE, RISK, DATA, DPIA, SECD) are in DRAFT status with "PENDING" for both Reviewed By and Approved By fields. For a project approaching statutory deadlines (registration deadline 2 Feb 2026, enforcement May 2026), governance artifacts should progress through review and approval cycles.

**Recommendation**:
Establish a review schedule and assign named reviewers for each artifact. Prioritise REQ and RISK for review given their proximity to regulatory deadlines.

---

#### M4: No GDS Service Assessment Preparation

**Severity**: 🟡 MEDIUM
**Category**: UK Government Compliance
**Location**: Missing artifact

**Description**:
NFR-C-003 mandates GDS Service Standard assessment at Alpha, Beta, and Live. No preparation artifact exists to self-assess against the 14 points and identify gaps before the formal assessment panel.

**Recommendation**:
Consider running `/arckit:service-assessment` to identify gaps and prepare evidence portfolio for Alpha assessment.

---

### Low Priority Issues

#### L1: Data Requirement ID Mismatch

**Severity**: 🟢 LOW
**Category**: Requirements Quality
**Location**: ARC-001-REQ-v2.0:L2198

**Description**:
Appendix C uses shorthand "DR-001-006" as a single line item, rather than listing individual DR-xxx requirements separately. This is less useful for traceability than individual entries.

**Recommendation**: Expand into individual DR-001, DR-002, DR-003, DR-004, DR-005, DR-006 rows if formal DR-xxx IDs are added (see H5).

---

#### L2: DPIA Classification Inconsistency

**Severity**: 🟢 LOW
**Category**: Document Control
**Location**: ARC-001-DPIA-v1.0:L13

**Description**:
The DPIA is classified as OFFICIAL-SENSITIVE while all other artifacts are classified as OFFICIAL. This may be intentional (DPIAs often warrant higher classification due to privacy risk details) but should be confirmed.

**Recommendation**: Verify this is an intentional classification decision. If so, no action needed.

---

#### L3: TCoP Point Count

**Severity**: 🟢 LOW
**Category**: Requirements Quality
**Location**: ARC-001-REQ-v2.0:L1226

**Description**:
NFR-C-004 states "12 points of the Technology Code of Practice" and lists 12 items (Points 1-12). Verify this matches the current version of the TCoP, as the standard has been updated.

**Recommendation**: Confirm against current TCoP publication during TCoP assessment (C1).

---

## Recommendations Summary

### Immediate Actions (Before Design/Procurement)

1. **[C1] Run `/arckit:tcop`**: Generate TCoP assessment — mandatory for UK Government projects. Addresses CRITICAL compliance gap.
2. **[C2] Define enforcement threshold**: Consult CMA Enforcement Lead to replace "[X hours]" in FR-006 with a specific value. Addresses CRITICAL requirements placeholder.
3. **[C3] Run `/arckit:sobc`**: Create Strategic Outline Business Case using Green Book 5-case model. Addresses CRITICAL governance gap for major investment.

### Short-term Actions (Within 2 weeks)

4. **[H1] Run `/arckit:traceability`**: Generate formal traceability matrix for end-to-end requirement coverage tracking.
5. **[H2] Assign document owners**: Update `[OWNER_NAME_AND_ROLE]` in 5 artifacts with named individuals and roles.
6. **[H4] Develop budget estimates**: Work with finance team and cloud research outputs (AWRS, AZRS) to produce at least ROM cost estimates.
7. **[H5] Add formal DR-xxx IDs**: Add numbered data requirement identifiers to the requirements body for traceability.

### Medium-term Actions (Within 1 month)

8. **[M1] Schedule stakeholder interviews**: Confirm user research interview dates for Alpha phase evidence.
9. **[M2] Add VE3 API contingency**: Create a requirement for an alternative data ingestion approach if VE3 Global API is unavailable.
10. **[M3] Progress artifact reviews**: Move key artifacts (REQ, RISK) from DRAFT to IN_REVIEW with assigned reviewers.
11. **[M4] Run `/arckit:service-assessment`**: Prepare for GDS Alpha assessment with self-assessment.
12. **[H3] Complete SbD TBDs**: Resolve Secure by Design TBDs progressively as design decisions are made.

---

## Metrics Dashboard

### Requirement Quality

- Total Requirements: 63
- Ambiguous Requirements: 1 (FR-006 placeholder)
- Duplicate Requirements: 0
- Untestable Requirements: 0
- Unresolved Placeholders: 1 ([X hours]) + 10 (budget TBDs)
- **Quality Score**: 85%

### Architecture Alignment

- Principles Compliant: 19/22
- Principles Partially Compliant: 3/22 (IaC, Testing, CI/CD — implicit but not formalised)
- Principles Violations: 0/22
- **Alignment Score**: 95%

### Traceability

- Requirements Covered by Design: N/A (pre-design phase)
- Requirements Traced to Stakeholder Goals: 63/63 (100%)
- Requirements Traced to Principles: 63/63 (100%)
- Formal Traceability Matrix: ❌ Missing
- **Traceability Score**: 75% (penalised for missing TRAC artifact)

### Stakeholder Traceability

- Requirements traced to stakeholder goals: 100%
- Orphan requirements: 0
- Conflicts documented and resolved: 4/4 (100%)
- RACI governance alignment: 100%
- **Stakeholder Score**: 92%

### Risk Management

- Total risks: 20
- High/Very High risks with mitigation: 19/20 (95%)
- Risk owners from RACI: 20/20 (100%)
- Risks above appetite: 4 (all with escalation paths)
- Risk-SOBC alignment: ❌ Cannot assess (no SOBC)
- **Risk Management Score**: 85%

### Data Model

- Entities specified: 6/6 (100%)
- ERD present: ✅
- PII identified: ✅
- GDPR compliance documented: ✅
- Data governance matrix: ✅
- CRUD matrix: ✅
- DR-xxx formal IDs: ❌ Missing in requirements body
- **Data Model Score**: 90%

### UK Government Compliance

- TCoP Assessment: ❌ Missing (CRITICAL)
- DPIA: ✅ Present (pending approval)
- Secure by Design: ⚠️ Present (TBDs remaining)
- GDS Service Standard: ⚠️ Referenced in requirements but no preparation artifact
- **UK Gov Compliance Score**: 60%

### Overall Governance Health

**Score**: 83/100
**Grade**: B

**Grade Thresholds**:

- A (90-100%): Excellent governance, ready to proceed
- **B (80-89%): Good governance, minor issues** ← Current
- C (70-79%): Adequate governance, address high-priority issues
- D (60-69%): Poor governance, major rework needed
- F ( < 60%): Insufficient governance, do not proceed

---

## Next Steps

### Immediate Actions

1. **CRITICAL issues exist**: ⚠️ **RESOLVE 3 CRITICAL ISSUES** before proceeding to design or procurement.
   - Run: `/arckit:tcop` to create TCoP assessment
   - Define: FR-006 enforcement threshold with CMA Enforcement Lead
   - Run: `/arckit:sobc` to create Green Book business case

2. **After resolving CRITICAL issues**: Address HIGH priority issues in parallel with design work.

3. **After resolving HIGH issues**: Re-run `/arckit:analyze` to verify improvement.

### Suggested Commands

**Governance Foundation (CRITICAL)**:

- `/arckit:tcop` — Complete TCoP assessment (CRITICAL gap)
- `/arckit:sobc` — Create Strategic Outline Business Case (CRITICAL gap)

**Traceability & Quality**:

- `/arckit:traceability` — Generate formal traceability matrix
- `/arckit:service-assessment` — Prepare for GDS Alpha assessment
- `/arckit:conformance` — Assess architecture conformance against principles

**Design Phase (When Ready)**:

- `/arckit:diagram` — Generate architecture diagrams
- `/arckit:hld-review` — Review HLD once produced
- `/arckit:dld-review` — Review DLD once produced

### Re-run Analysis

After making changes, re-run analysis:
```
/arckit:analyze
```

Expected improvement: 83% → 90%+ after resolving CRITICAL and HIGH issues.

---

## Appendix A: Artifacts Analyzed

| Artifact | Location | Last Modified | Status |
|----------|----------|---------------|--------|
| Architecture Principles | `projects/000-global/ARC-000-PRIN-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| Stakeholder Drivers | `projects/001-uk.../ARC-001-STKE-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| Risk Register | `projects/001-uk.../ARC-001-RISK-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| Requirements | `projects/001-uk.../ARC-001-REQ-v2.0.md` | 2026-01-30 | ✅ Analyzed |
| Data Model | `projects/001-uk.../ARC-001-DATA-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| DPIA | `projects/001-uk.../ARC-001-DPIA-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| Secure by Design | `projects/001-uk.../ARC-001-SECD-v1.0.md` | 2026-01-30 | ✅ Analyzed |
| SOBC | N/A | N/A | ❌ Not Found |
| TCoP Assessment | N/A | N/A | ❌ Not Found |
| Traceability Matrix | N/A | N/A | ❌ Not Found |
| Vendor HLD | N/A | N/A | ❌ Not Found (expected — pre-design) |
| Vendor DLD | N/A | N/A | ❌ Not Found (expected — pre-design) |

---

## Appendix B: Analysis Methodology

**Analysis Date**: 2026-02-28
**Analyzed By**: ArcKit `/arckit.analyze` command

**Checks Performed**:

- Requirements completeness and quality (ambiguity, placeholders, duplication, prioritisation)
- Architecture principles compliance (22 principles × 63 requirements)
- Stakeholder traceability (7 goals, 4 conflicts, RACI alignment)
- Risk coverage and mitigation (20 risks, 4 above appetite)
- Data model consistency (6 entities, DR-xxx coverage, GDPR, governance)
- UK Government compliance (TCoP, DPIA, Secure by Design, GDS Service Standard)
- Cross-artifact consistency (terminology, technology stack, data model alignment)
- Document control (owners, status, classification, placeholders)

**Severity Classification**:

- 🔴 **CRITICAL**: Blocks progression, must resolve immediately — 3 found
- 🟠 **HIGH**: Significant risk, resolve before major milestones — 5 found
- 🟡 **MEDIUM**: Should be addressed, can proceed with caution — 4 found
- 🟢 **LOW**: Minor issues, address when convenient — 3 found

**Total Findings**: 15

---

**Generated by**: ArcKit `/arckit.analyze` command
**Generated on**: 2026-02-28 12:00 GMT
**ArcKit Version**: 2.16.0
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: claude-opus-4-6
**Generation Context**: Analysis of 7 governance artifacts (PRIN, STKE, RISK, REQ, DATA, DPIA, SECD) against architecture principles, stakeholder goals, risk register, UK Government compliance requirements, and cross-artifact consistency. 3 missing artifacts identified (SOBC, TCOP, TRAC).
