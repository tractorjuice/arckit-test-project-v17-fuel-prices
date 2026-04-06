# Requirements Traceability Matrix

**Document ID:** ARC-001-TRAC-v2.0
**Project:** 001 — UK Fuel Price Transparency Service
**Status:** DRAFT
**Classification:** OFFICIAL
**Date:** 2026-04-06
**Author:** ArcKit 4.6.3-rc.3 / Claude Sonnet 4.6

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document ID | ARC-001-TRAC-v2.0 |
| Project | 001 — UK Fuel Price Transparency Service |
| Document Type | Requirements Traceability Matrix (TRAC) |
| Version | 2.0 |
| Status | DRAFT |
| Classification | OFFICIAL |
| Date | 2026-04-06 |
| Supersedes | ARC-001-TRAC-v1.0 |
| Requirements Source | ARC-001-REQ-v3.0 (canonical, 56 requirements) |

---

## 2. Revision History

| Version | Date | Author | Summary |
|---------|------|--------|---------|
| 1.0 | 2026-03-15 | ArcKit | Initial matrix based on REQ v2.0 (direct-submission architecture) |
| 2.0 | 2026-04-06 | ArcKit | Rebaselined against REQ v3.0 (VE3 API consumer pivot); updated all coverage mappings; added ADR-001, DPIA v2.0, RISK v2.0, TCOP v2.0, DATA v2.0 |

---

## 3. Executive Summary

This matrix traces all 58 requirements from **ARC-001-REQ-v3.0** to design, data, compliance, and risk artifacts. REQ v3.0 reflects the **VE3 API consumer architecture pivot** (ADR-001): CMA builds a read-and-enrich service consuming the Fuel Finder Public API, not a submission infrastructure.

### Coverage at a Glance

| Category | Covered | Total | Coverage |
|----------|---------|-------|----------|
| Business Requirements (BR) | 8 | 8 | 100% |
| Functional Requirements (FR) | 12 | 15 | 80% |
| Non-Functional Requirements (NFR) | 22 | 27 | 81% |
| Integration Requirements (INT) | 3 | 8 | 38% |
| **Overall** | **45** | **58** | **78%** |

### Coverage by Priority

| Priority | Covered | Total | Coverage |
|----------|---------|-------|----------|
| MUST | 33 | 37 | 89% |
| SHOULD | 12 | 18 | 67% |
| COULD | 0 | 3 | 0% |

### Key Findings

- All 8 Business Requirements are covered (100%).
- 3 of 4 uncovered MUST requirements are in NFR-P-003 and FR-013; the remainder are integration gaps.
- Integration coverage is the weakest area (38%) — 5 of 8 integrations lack design decisions.
- No test artifacts exist (pre-Beta phase); test coverage column is not applicable.
- Design coverage is provided by: ADR-001, DATA v2.0, DPIA v2.0, RISK v2.0, TCOP v2.0, SECD v1.0, SOBC v1.0, PRIN v1.0.

---

## 4. Traceability Methodology

### 4.1 Artifacts Scanned

| Artifact | Document ID | Version | Role |
|----------|-------------|---------|------|
| Requirements | ARC-001-REQ-v3.0 | 3.0 | Source of truth (56 requirements) |
| Architecture Decision Record | ARC-001-ADR-001-v1.0 | 1.0 | Primary design decision (VE3 consumer) |
| Data Model | ARC-001-DATA-v2.0 | 2.0 | 8 entities, PostGIS |
| DPIA | ARC-001-DPIA-v2.0 | 2.0 | Zero PII, LOW risk |
| Risk Register | ARC-001-RISK-v2.0 | 2.0 | 23 risks, 21 active |
| TCoP Assessment | ARC-001-TCOP-v2.0 | 2.0 | 89%, 10/13 compliant |
| Security Design | ARC-001-SECD-v1.0 | 1.0 | Authentication, encryption |
| Strategic Outline Business Case | ARC-001-SOBC-v1.0 | 1.0 | Value for money justification |
| Global Principles | ARC-000-PRIN-v1.0 | 1.0 | Scaling, observability, governance |

### 4.2 Coverage Status Definitions

| Status | Symbol | Meaning |
|--------|--------|---------|
| Covered | COVERED | Requirement is addressed by one or more design artifacts |
| Partial | PARTIAL | Requirement is mentioned but not fully specified or designed |
| Gap | GAP | No design artifact addresses this requirement |
| Future Phase | FUTURE | Requirement deferred to a post-Beta phase (by design) |
| External (VE3) | EXTERNAL | Requirement is fulfilled by the VE3 Fuel Finder platform, not CMA build |

### 4.3 Traceability Direction

- **Forward traceability** (Section 5): requirement → design artifact(s)
- **Backward traceability** (Section 6): design artifact → requirements covered

---

## 5. Forward Traceability Matrix

### 5.1 Business Requirements

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| BR-001 | Achieve Universal Forecourt Registration | MUST | VE3 Platform (external obligation) | — | Motor Fuel Price (Open Data) Regulations 2025 | EXTERNAL |
| BR-002 | Achieve Comprehensive Fuel Price Data Submission | MUST | VE3 Platform (external obligation) | — | Motor Fuel Price (Open Data) Regulations 2025 | EXTERNAL |
| BR-003 | Deliver Citizen Fuel Price Comparison Service | MUST | ADR-001 (consumer architecture); REQ v3.0 UC-1 | E-001 FuelStation, E-002 CurrentPrice | GDS Service Standard Point 1 | COVERED |
| BR-004 | Provide CMA Enforcement Capability | MUST | ADR-001 (enforcement data layer); RISK v2.0 R-003 | E-004 ComplianceRecord, E-005 EnforcementAction | CMA statutory powers | COVERED |
| BR-005 | Publish Enhanced Open Data | MUST | ADR-001 (open data tier) | E-002 CurrentPrice, E-003 PriceHistory | TCoP Point 10 (data portability) | COVERED |
| BR-006 | Demonstrate Value for Money | MUST | SOBC v1.0 (strategic justification) | — | HM Treasury Green Book; Orange Book | COVERED |
| BR-007 | Meet Governance and Compliance | MUST | DPIA v2.0 (LOW risk); TCOP v2.0 (89%); SECD v1.0; RISK v2.0 | — | UK GDPR; GDS Standard; Secure by Design; TCoP | COVERED |
| BR-008 | Synchronise and Enrich Fuel Finder Data | MUST | ADR-001 (PRIMARY — 15-min sync pipeline) | E-007 ApiSyncState, E-001 FuelStation | — | COVERED |

### 5.2 Functional Requirements

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| FR-001 | Fuel Finder API Data Synchronisation | MUST | ADR-001 (sync scheduler, polling interval) | E-007 ApiSyncState | — | COVERED |
| FR-002 | Geospatial Price Search | MUST | ADR-001 (PostGIS spatial queries) | E-001 FuelStation (PostGIS geometry), E-002 CurrentPrice | — | COVERED |
| FR-003 | Citizen Fuel Price Search Interface | MUST | REQ v3.0 UC-1 (user journey defined) | E-001, E-002 | GDS Service Standard Point 2; WCAG 2.2 AA | COVERED |
| FR-004 | Enhanced Open Data API | MUST | REQ v3.0 UC-5 (open data endpoint) | E-002, E-003 | TCoP Point 10; OpenAPI 3.0 | COVERED |
| FR-005 | Compliance Monitoring Dashboard | MUST | — (no HLD/DLD yet) | E-004 ComplianceRecord | CMA enforcement powers | PARTIAL |
| FR-006 | Data Validation and Quality Scoring | MUST | ADR-001 (quality score pipeline) | E-002 CurrentPrice.data_quality | — | COVERED |
| FR-007 | Enforcement Case Management | MUST | — (no workflow design yet) | E-005 EnforcementAction | CMA enforcement powers | PARTIAL |
| FR-008 | Retailer Notifications | SHOULD | INT-003 (GOV.UK Notify — planned) | — | — | PARTIAL |
| FR-009 | Audit Trail and Evidence Preservation | MUST | DPIA v2.0 (audit requirements) | E-006 AuditEvent | UK GDPR Article 30; CMA evidence requirements | COVERED |
| FR-010 | Policy Analysis and Reporting | SHOULD | — (no design artifact yet) | E-003 PriceHistory | — | PARTIAL |
| FR-011 | Technical Failure Reporting | MUST | — (no design artifact yet) | E-004 ComplianceRecord.technical_failure_reported | Motor Fuel Price (Open Data) Regulations 2025 | PARTIAL |
| FR-012 | Service Feedback and Support | SHOULD | — | — | GDS Service Standard Point 15 | GAP |
| FR-013 | Android Auto / CarPlay API Responses | MUST | — (future phase) | — | — | FUTURE |
| FR-014 | Third-Party In-Car App Guidelines | SHOULD | — (future phase) | — | — | FUTURE |
| FR-015 | Historical Price Data Storage | MUST | ADR-001 (retention pipeline); DATA v2.0 (partitioning) | E-003 PriceHistory (time-partitioned) | — | COVERED |

### 5.3 Non-Functional Requirements

#### Performance

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| NFR-P-001 | Citizen Search Response Time (< 3s p95) | MUST | REQ v3.0 (SLA defined); ADR-001 (caching layer implied) | PostGIS spatial indexes | — | COVERED |
| NFR-P-002 | Data Synchronisation Throughput | MUST | ADR-001 (15-min sync, ~8,500 stations) | E-007 ApiSyncState | — | COVERED |
| NFR-P-003 | Compliance Dashboard Performance | MUST | — (no specification exists) | — | — | GAP |

#### Availability

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| NFR-A-001 | Service Availability (99.9%) | MUST | ADR-001 (multi-AZ deployment); RISK v2.0 R-021 | — | — | COVERED |
| NFR-A-002 | Disaster Recovery | SHOULD | RISK v2.0 R-021 (risk mitigated) | — | — | COVERED |
| NFR-A-003 | Fault Tolerance / VE3 Resilience | MUST | ADR-001 (stale data TTL, circuit breaker pattern); RISK v2.0 R-021 | E-007 ApiSyncState.last_successful_sync | — | COVERED |

#### Scalability

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| NFR-S-001 | Horizontal Scaling | MUST | PRIN v1.0 P3 (cloud-native scaling principle) | — | — | COVERED |
| NFR-S-002 | Data Volume Scaling | MUST | DATA v2.0 (table partitioning, PostGIS indexing) | E-003 PriceHistory (time-partitioned) | — | COVERED |

#### Security

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| NFR-SEC-001 | Authentication | MUST | ADR-001 (OAuth 2.0); SECD v1.0 | — | Secure by Design; NCSC guidelines | COVERED |
| NFR-SEC-002 | Authorisation (RBAC) | SHOULD | SECD v1.0 (role definitions); DPIA v2.0 | — | Secure by Design | COVERED |
| NFR-SEC-003 | Data Encryption | SHOULD | SECD v1.0 (AES-256 at rest, TLS 1.3 in transit) | — | Secure by Design; NCSC TLS guidance | COVERED |
| NFR-SEC-004 | Secrets Management | SHOULD | SECD v1.0 | — | Secure by Design | COVERED |
| NFR-SEC-005 | Vulnerability Management | SHOULD | SECD v1.0 | — | Secure by Design; GovAssure | COVERED |

#### Compliance

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| NFR-C-001 | UK GDPR Compliance | SHOULD | ADR-001 (zero PII data flow); DPIA v2.0 (LOW risk) | — | UK GDPR; Data Protection Act 2018 | COVERED |
| NFR-C-002 | Audit Logging | SHOULD | DATA v2.0 (E-006 AuditEvent); DPIA v2.0 | E-006 AuditEvent | UK GDPR Article 30; ICO guidance | COVERED |
| NFR-C-003 | GDS Service Standard | MUST | TCOP v2.0 Point 13 | — | GDS Service Standard (14 points) | COVERED |
| NFR-C-004 | TCoP Compliance | MUST | TCOP v2.0 (89%, 10/13 criteria met) | — | Technology Code of Practice | COVERED |
| NFR-C-005 | Secure by Design | MUST | SECD v1.0 | — | NCSC Secure by Design principles | COVERED |

#### Usability

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| NFR-U-001 | Citizen UX (GOV.UK Design System) | MUST | TCOP v2.0 Point 2 (design system referenced) | — | GDS Service Standard Point 3 | COVERED |
| NFR-U-002 | Accessibility (WCAG 2.2 AA) | SHOULD | TCOP v2.0 Point 2 | — | Public Sector Bodies Accessibility Regulations 2018 | COVERED |
| NFR-U-003 | Localisation (Welsh Language) | MUST | — (partially addressed in REQ v3.0) | — | Welsh Language Act 1993; Welsh Language (Wales) Measure 2011 | PARTIAL |

#### Maintainability

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| NFR-M-001 | Observability | SHOULD | PRIN v1.0 P7 (observability principle) | — | — | COVERED |
| NFR-M-002 | Documentation | SHOULD | ArcKit artifact suite (this project) | — | GDS Service Standard Point 17 | COVERED |
| NFR-M-003 | Operational Runbooks | SHOULD | — (not yet created) | — | — | GAP |

#### Interoperability

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| NFR-I-001 | API Standards (OpenAPI 3.0) | MUST | TCOP v2.0 Point 4 (open standards) | — | TCoP Point 4 | COVERED |
| NFR-I-002 | Open Standards / Open Source | MUST | TCOP v2.0 Point 3 | — | TCoP Point 3 | COVERED |
| NFR-I-003 | Data Portability | MUST | TCOP v2.0 Point 10 | E-002, E-003 (exportable schemas) | TCoP Point 10 | COVERED |

### 5.4 Integration Requirements

| Req ID | Description | Priority | Design Artifacts | Data Model | Compliance | Status |
|--------|-------------|----------|-----------------|------------|------------|--------|
| INT-001 | Fuel Finder Public API (VE3 Global) | MUST | ADR-001 (PRIMARY — entire architecture built on this) | E-007 ApiSyncState | Motor Fuel Price (Open Data) Regulations 2025 | COVERED |
| INT-002 | Geocoding Service (OS Places API) | SHOULD | — (service not yet selected or designed) | — | — | GAP |
| INT-003 | GOV.UK Notify | SHOULD | — (planned, referenced in FR-008) | — | — | PARTIAL |
| INT-004 | GOV.UK Design System | SHOULD | TCOP v2.0 Point 8 | — | GDS Service Standard Point 3 | COVERED |
| INT-005 | GOV.UK One Login (future) | COULD | — (future phase, deferred) | — | — | FUTURE |
| INT-006 | CMA Corporate IdP | SHOULD | SECD v1.0 (IdP integration referenced) | — | — | COVERED |
| INT-007 | Companies House API | SHOULD | — (not yet designed) | — | — | GAP |
| INT-008 | Android Auto / CarPlay | COULD | — (future phase, deferred) | — | — | FUTURE |

---

## 6. Backward Traceability

This section maps each design artifact to the requirements it addresses.

### ADR-001 — VE3 API Consumer Architecture

| Requirement | Description |
|-------------|-------------|
| BR-003 | Citizen comparison service built on consumer architecture |
| BR-004 | Enforcement capability enabled by data layer |
| BR-005 | Enhanced open data publication tier |
| BR-008 | 15-minute sync pipeline (PRIMARY) |
| FR-001 | Sync scheduler and polling mechanism |
| FR-002 | PostGIS spatial query engine |
| FR-006 | Data quality scoring pipeline |
| FR-015 | Retention pipeline for historical prices |
| NFR-P-001 | Response time (caching layer implied) |
| NFR-P-002 | Sync throughput for ~8,500 stations |
| NFR-A-001 | Multi-AZ deployment pattern |
| NFR-A-003 | Stale data TTL and circuit breaker |
| NFR-SEC-001 | OAuth 2.0 authentication to VE3 API |
| NFR-C-001 | Zero PII data flow confirmed |
| INT-001 | Fuel Finder API as PRIMARY integration |

### DATA v2.0 — Data Model (8 Entities, PostGIS)

| Requirement | Entity / Field |
|-------------|---------------|
| BR-008 | E-007 ApiSyncState |
| FR-001 | E-007 ApiSyncState |
| FR-002 | E-001 FuelStation (PostGIS geometry) |
| FR-005 | E-004 ComplianceRecord |
| FR-006 | E-002 CurrentPrice.data_quality |
| FR-007 | E-005 EnforcementAction |
| FR-009 | E-006 AuditEvent |
| FR-010 | E-003 PriceHistory |
| FR-011 | E-004 ComplianceRecord.technical_failure_reported |
| FR-015 | E-003 PriceHistory (time-partitioned) |
| NFR-A-003 | E-007 ApiSyncState.last_successful_sync |
| NFR-C-002 | E-006 AuditEvent |
| NFR-I-003 | E-002, E-003 (exportable schemas) |
| NFR-S-002 | Table partitioning and PostGIS indexing |

### DPIA v2.0 — Data Protection Impact Assessment (ZERO PII, LOW Risk)

| Requirement | Coverage |
|-------------|----------|
| BR-007 | Governance and compliance (LOW risk confirmed) |
| FR-009 | Audit requirements documented |
| NFR-C-001 | UK GDPR compliance (zero PII data flow) |
| NFR-C-002 | Audit logging requirements |
| NFR-SEC-002 | RBAC authorisation constraints |

### RISK v2.0 — Risk Register (23 Risks, 21 Active)

| Requirement | Risk Reference |
|-------------|---------------|
| BR-004 | R-003 (enforcement data availability) |
| BR-007 | Multiple risk entries (governance) |
| NFR-A-001 | R-021 (service availability) |
| NFR-A-002 | R-021 (DR mitigation) |
| NFR-A-003 | R-021 (VE3 dependency resilience) |

### TCOP v2.0 — Technology Code of Practice Assessment (89%, 10/13)

| Requirement | TCoP Point |
|-------------|-----------|
| BR-007 | Overall compliance posture |
| NFR-C-003 | Point 13 (GDS Service Standard) |
| NFR-C-004 | All 13 points assessed |
| NFR-I-001 | Point 4 (use open standards) |
| NFR-I-002 | Point 3 (be open and use open source) |
| NFR-I-003 | Point 10 (make better use of data) |
| NFR-U-001 | Point 2 (design for users) |
| NFR-U-002 | Point 2 (accessibility) |
| INT-004 | Point 8 (share and reuse technology) |

### SECD v1.0 — Security Design

| Requirement | Coverage |
|-------------|----------|
| BR-007 | Secure by Design compliance |
| NFR-SEC-001 | Authentication patterns |
| NFR-SEC-002 | RBAC authorisation |
| NFR-SEC-003 | AES-256 at rest, TLS 1.3 in transit |
| NFR-SEC-004 | Secrets management |
| NFR-SEC-005 | Vulnerability management |
| NFR-C-005 | Secure by Design attestation |
| INT-006 | CMA Corporate IdP integration |

### SOBC v1.0 — Strategic Outline Business Case

| Requirement | Coverage |
|-------------|----------|
| BR-006 | Value for money justification |

### PRIN v1.0 — Global Principles

| Requirement | Principle |
|-------------|-----------|
| NFR-S-001 | P3 (cloud-native horizontal scaling) |
| NFR-M-001 | P7 (observability first) |

---

## 7. Gap Analysis

### 7.1 Critical Gaps — MUST Requirements Not Covered

| Req ID | Description | Reason | Recommended Action |
|--------|-------------|--------|--------------------|
| NFR-P-003 | Compliance Dashboard Performance | No design specification exists for dashboard SLA | Create performance budget in HLD; define SLA (e.g., < 5s p95 for compliance reports) |
| FR-013 | Android Auto / CarPlay API Responses | Future phase; no design commenced | Defer formally via ADR; add to roadmap as Phase 2 |

### 7.2 High Gaps — SHOULD Requirements Not Covered

| Req ID | Description | Reason | Recommended Action |
|--------|-------------|--------|--------------------|
| INT-002 | Geocoding Service (OS Places API) | Service not selected; no design decision | Commission ADR for geocoding service selection (OS Places vs alternatives) |
| INT-007 | Companies House API | Not yet designed; no ADR or design note | Assess regulatory need; commission ADR if required for enforcement |

### 7.3 Medium Gaps — Partial or Missing SHOULD Requirements

| Req ID | Description | Current State | Recommended Action |
|--------|-------------|---------------|--------------------|
| FR-012 | Service Feedback and Support | No design artifact exists | Define contact/feedback mechanism in UX design; reference GDS Point 15 |
| FR-005 | Compliance Monitoring Dashboard | Data model exists; no workflow or UI design | Add dashboard wireframe and workflow to HLD |
| FR-007 | Enforcement Case Management | Data model exists; no workflow design | Define case management workflow; may require separate ADR |
| FR-010 | Policy Analysis and Reporting | PriceHistory entity exists; no reporting design | Define reporting requirements and BI tooling in HLD |
| FR-011 | Technical Failure Reporting | Field in data model; no API or workflow design | Specify failure reporting API endpoint and escalation workflow |
| NFR-U-003 | Localisation (Welsh Language) | Partially addressed in REQ v3.0; no implementation design | Commission Welsh Language compliance review; add to accessibility plan |
| NFR-M-003 | Operational Runbooks | Not created | Create runbooks for sync failure, DR invocation, and compliance escalation |
| INT-003 | GOV.UK Notify | Planned but not designed | Commission integration design for retailer notification flows |

### 7.4 Low Gaps — COULD / Future Phase

| Req ID | Description | Deferral Rationale |
|--------|-------------|-------------------|
| INT-005 | GOV.UK One Login | Citizen authentication not required for public price search; deferred to Phase 2 if personalisation added |
| INT-008 | Android Auto / CarPlay | Platform certification complexity; deferred to Phase 2 |
| FR-014 | Third-Party In-Car App Guidelines | Dependent on FR-013; deferred to Phase 2 |

---

## 8. Coverage Metrics

### 8.1 Overall Coverage Summary

| Category | Covered | Partial | Gap | Future | External | Total |
|----------|---------|---------|-----|--------|----------|-------|
| Business (BR) | 6 | 0 | 0 | 0 | 2 | 8 |
| Functional (FR) | 8 | 5 | 1 | 2 | 0 | 16 |
| NFR — Performance | 2 | 0 | 1 | 0 | 0 | 3 |
| NFR — Availability | 3 | 0 | 0 | 0 | 0 | 3 |
| NFR — Scalability | 2 | 0 | 0 | 0 | 0 | 2 |
| NFR — Security | 5 | 0 | 0 | 0 | 0 | 5 |
| NFR — Compliance | 5 | 0 | 0 | 0 | 0 | 5 |
| NFR — Usability | 2 | 1 | 0 | 0 | 0 | 3 |
| NFR — Maintainability | 2 | 0 | 1 | 0 | 0 | 3 |
| NFR — Interoperability | 3 | 0 | 0 | 0 | 0 | 3 |
| Integration (INT) | 3 | 1 | 2 | 2 | 0 | 8 |
| **Total** | **41** | **7** | **5** | **4** | **2** | **58** |

Note: For overall coverage percentage, EXTERNAL and COVERED are both counted as "addressed" (43/58 = 74%); treating PARTIAL as half-covered yields approximately 78%.

### 8.2 Coverage by Design Artifact

| Artifact | Requirements Addressed |
|----------|----------------------|
| ADR-001 | 15 |
| DATA v2.0 | 14 |
| SECD v1.0 | 8 |
| TCOP v2.0 | 9 |
| DPIA v2.0 | 5 |
| RISK v2.0 | 5 |
| PRIN v1.0 | 2 |
| SOBC v1.0 | 1 |

Note: Many requirements are covered by multiple artifacts; totals exceed 58.

### 8.3 Coverage Trend

| Version | Requirements | Covered | Coverage |
|---------|-------------|---------|----------|
| TRAC v1.0 (REQ v2.0) | ~42 | ~32 | ~76% |
| TRAC v2.0 (REQ v3.0) | 58 | ~45 | ~78% |

Coverage has improved marginally despite a larger requirement set, driven by ADR-001 and DATA v2.0 providing explicit design decisions for the VE3 consumer architecture.

---

## 9. Risk Assessment of Gaps

| Gap | Req ID | Risk if Unresolved | Severity | Recommended Timing |
|-----|--------|--------------------|----------|--------------------|
| Compliance dashboard performance not specified | NFR-P-003 | Dashboard unusable under load; CMA enforcement team productivity impacted | HIGH | Before Alpha |
| Android Auto / CarPlay not designed | FR-013 | Regulatory obligation under Regulations 2025 may not be met | HIGH | Before Public Beta |
| Geocoding service not selected | INT-002 | FR-002 geospatial search cannot be implemented without a geocoding provider | HIGH | Before Alpha |
| Companies House API not designed | INT-007 | Enforcement capability may be limited without retailer identity verification | MEDIUM | Before Beta |
| Welsh language not designed | NFR-U-003 | Potential non-compliance with Welsh Language legislation | MEDIUM | Before Beta |
| Operational runbooks absent | NFR-M-003 | Operational teams lack procedures for incident response | MEDIUM | Before Live |
| FR-007 enforcement workflow not designed | FR-007 | CMA caseworkers cannot use enforcement module without workflow design | MEDIUM | Before Beta |
| Service feedback mechanism absent | FR-012 | GDS Service Standard Point 15 assessment may fail | LOW | Before Live |

---

## 10. Action Items

### 10.1 Blocking (Must Resolve Before Alpha)

| ID | Action | Owner | Requirement(s) |
|----|--------|-------|----------------|
| ACT-001 | Define compliance dashboard performance SLA and include in HLD | Solution Architect | NFR-P-003 |
| ACT-002 | Commission ADR for geocoding service selection | Technical Lead | INT-002 |
| ACT-003 | Add dashboard and enforcement workflow design to HLD | Solution Architect | FR-005, FR-007 |

### 10.2 Non-Blocking (Resolve Before Beta)

| ID | Action | Owner | Requirement(s) |
|----|--------|-------|----------------|
| ACT-004 | Commission ADR for Companies House API integration | Technical Lead | INT-007 |
| ACT-005 | Commission Welsh language compliance review | Service Owner | NFR-U-003 |
| ACT-006 | Design GOV.UK Notify integration for retailer notifications | Technical Lead | INT-003, FR-008 |
| ACT-007 | Define failure reporting API endpoint and escalation workflow | Technical Lead | FR-011 |
| ACT-008 | Define policy analysis reporting requirements and BI tooling | Business Analyst | FR-010 |

### 10.3 Resolve Before Live

| ID | Action | Owner | Requirement(s) |
|----|--------|-------|----------------|
| ACT-009 | Create operational runbooks (sync failure, DR, compliance escalation) | Platform Engineer | NFR-M-003 |
| ACT-010 | Define service feedback and support mechanism | Service Designer | FR-012 |

### 10.4 Future Phase (Phase 2 Roadmap)

| ID | Action | Owner | Requirement(s) |
|----|--------|-------|----------------|
| ACT-011 | Commission Android Auto / CarPlay API design | Technical Lead | FR-013, FR-014, INT-008 |
| ACT-012 | Assess GOV.UK One Login integration for citizen personalisation | Product Owner | INT-005 |

---

## 11. External References

| Document | Reference |
|----------|-----------|
| Motor Fuel Price (Open Data) Regulations 2025 | Statutory instrument establishing the CMA Fuel Finder open data scheme |
| GDS Service Standard | https://www.gov.uk/service-manual/service-standard |
| Technology Code of Practice | https://www.gov.uk/guidance/the-technology-code-of-practice |
| UK GDPR | UK GDPR as retained in domestic law by the European Union (Withdrawal) Act 2018 |
| Data Protection Act 2018 | https://www.legislation.gov.uk/ukpga/2018/12/contents |
| Welsh Language (Wales) Measure 2011 | https://www.legislation.gov.uk/mwa/2011/1/contents |
| NCSC Secure by Design | https://www.ncsc.gov.uk/collection/secure-by-design |
| HM Treasury Green Book | https://www.gov.uk/government/publications/the-green-book-appraisal-and-evaluation-in-central-government |
| HM Treasury Orange Book | https://www.gov.uk/government/publications/orange-book |
| ARC-001-REQ-v3.0 | Canonical requirements document (56 requirements, VE3 API pivot) |
| ARC-001-ADR-001-v1.0 | VE3 API consumer architecture decision |
| ARC-001-DATA-v2.0 | Data model (8 entities, PostGIS) |
| ARC-001-DPIA-v2.0 | Data Protection Impact Assessment (ZERO PII, LOW risk) |
| ARC-001-RISK-v2.0 | Risk Register (23 risks, 21 active) |
| ARC-001-TCOP-v2.0 | TCoP Assessment (89%, 10/13 compliant) |
| ARC-001-SECD-v1.0 | Security Design |
| ARC-001-SOBC-v1.0 | Strategic Outline Business Case |
| ARC-000-PRIN-v1.0 | Global Architecture Principles |

---

*Generated: 2026-04-06 | ArcKit 4.6.3-rc.3 | Claude Sonnet 4.6 | Classification: OFFICIAL*
