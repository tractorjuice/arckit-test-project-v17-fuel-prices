# Technology Code of Practice (TCoP) Review

> **Template Status**: Beta | **Version**: 2.16.0 | **Command**: `/arckit.tcop`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-TCOP-v2.0 |
| **Document Type** | Technology Code of Practice Review |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 2.0 |
| **Created Date** | 2026-04-06 |
| **Last Modified** | 2026-04-06 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-07-06 |
| **Owner** | Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, CDDO Spend Control, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-28 | ArcKit AI | Initial creation from `/arckit.tcop` command — Discovery/Alpha phase | PENDING | PENDING |
| 2.0 | 2026-04-06 | ArcKit AI | Updated for Beta phase — VE3 API consumer architecture pivot (ADR-001), REQ v3.0 (56 requirements), DATA v2.0 (8 entities, zero PII), DPIA v2.0 (LOW residual), RISK v2.0 (0 High/Critical), SOBC v1.0 created. Score improved from 108/130 (83%) to 116/130 (89%). | PENDING | PENDING |

## Document Purpose

This document assesses the UK Government Fuel Price Transparency Service ("Fuel Finder") against all 13 points of the Technology Code of Practice (TCoP). The TCoP is mandatory for UK Government technology projects and is used by the CDDO Digital Spend Control team to assess technology spending proposals. This assessment provides evidence of compliance for GDS Service Standard assessment (Point 12: "Meet the Service Standard") and CDDO spend control approval.

The project is currently approaching **Beta** phase, with an enforcement deadline of May 2026 and a GDS Beta assessment targeted for Q3 2026. This v2.0 review reflects a significant architecture pivot since v1.0: CMA now **consumes** the VE3 Global Fuel Finder API (contracted by DESNZ) rather than building its own ingestion infrastructure. This decision is formally documented in ADR-001 and is the single most consequential change to compliance posture across multiple TCoP points.

**Architecture Pivot Summary**: Under the VE3 API consumer model, the CMA Fuel Finder service acts as an orchestration and citizen-facing layer over the VE3 Fuel Finder API, which itself aggregates real-time pricing data from all ~8,500 UK fuel stations. Responsibilities annotated [VE3] vs [CMA] throughout requirements (ARC-001-REQ-v3.0).

**Source Documents Assessed**:

- ARC-000-PRIN-v1.0 — Enterprise Architecture Principles (22 principles)
- ARC-001-REQ-v3.0 — Business and Technical Requirements (56 requirements, VE3 API pivot)
- ARC-001-STKE-v1.0 — Stakeholder Drivers & Goals Analysis (12 stakeholder groups)
- ARC-001-RISK-v2.0 — Risk Register (23 risks, 21 active, 2 closed; 0 High/Critical residual)
- ARC-001-DATA-v2.0 — Data Model (8 entities, zero retailer PII, PostGIS geospatial indexing)
- ARC-001-DPIA-v2.0 — Data Protection Impact Assessment (LOW residual risk, zero retailer PII)
- ARC-001-SECD-v1.0 — Secure by Design Assessment (NCSC CAF — needs v2.0 update for VE3 architecture)
- ARC-001-SOBC-v1.0 — Strategic Outline Business Case (Green Book 5-case model, £3.6M ROM 3-year budget)
- ARC-001-ADR-001-v1.0 — Architecture Decision Record: VE3 API Consumer Architecture
- ARC-001-RSCH-v4.1 — Technology Research (updated with VE3 Fuel Finder API findings)
- ARC-001-AWRS-v2.0 — AWS Cloud Research (UK region, eu-west-2)
- ARC-001-AZRS-v2.0 — Azure Cloud Research (UK South/West regions)
- ARC-001-DIAG-001-v1.0 — Architecture Diagrams

---

## Executive Summary

**Overall TCoP Compliance**: ✅ Largely Compliant

**Score**: 116/130 (89%) — 10 Compliant, 3 Partially Compliant, 0 Non-Compliant

*Previous score (v1.0, Feb 2026): 108/130 (83%) — 8 Compliant, 5 Partially Compliant*

**Key Findings**:

- **Architecture pivot delivers TCoP benefits**: Consuming the DESNZ-contracted VE3 Fuel Finder API exemplifies TCoP Point 8 (Share, Reuse and Collaborate), eliminates significant build cost (ADR-001 TCO: £500K vs £1.5M over 3 years), and dramatically reduces the CMA's data processing attack surface (Point 7)
- **Critical governance gaps closed**: SOBC v1.0 now exists (previously the single most critical gap), ADR-001 formally documents the VE3 reuse decision, DPIA v2.0 achieves LOW residual risk with zero retailer PII in the CMA database, and RISK v2.0 has zero High/Critical residual risks (down from 4)
- **Cloud First resolved**: ADR-001 documents AWS eu-west-2 as primary cloud target; VE3 Global operates on UK cloud infrastructure under DESNZ contract — the previously HIGH gap on cloud provider selection is now substantially addressed
- **Privacy by Design exemplary**: DPIA v2.0 is a model outcome — Organisation entity removed entirely, zero retailer PII in CMA database, only indirect identifiers (CMA officer UUIDs, source IPs) in audit logs
- **Remaining gaps**: Security design document needs v2.0 update for VE3 architecture; sustainability metrics still not defined; GDS Beta self-assessment not yet prepared; procurement route (G-Cloud/DOS) not formally selected

**Critical Actions**:

1. Produce SECD v2.0 aligned to VE3 API consumer architecture and complete NCSC Cloud Security Principles assessment (Point 6)
2. Define sustainability metrics and carbon footprint baseline aligned with Greening Government ICT Strategy (Point 12)
3. Prepare GDS Service Standard self-assessment for Beta assessment panel Q3 2026 (Point 13)
4. Formally select procurement route (G-Cloud / DOS) and document exit strategy (Point 11)

---

## TCoP Point 1: Define User Needs

**Guidance**: Understand your users and their needs. Develop knowledge of your users and what that means for your technology project or programme.

**Reference**: https://www.gov.uk/guidance/define-user-needs

### Assessment

**Status**: ✅ Compliant

**Score**: 9/10 (unchanged from v1.0)

**Evidence**:

The project retains its comprehensive user needs documentation from ARC-001-REQ-v3.0 and ARC-001-STKE-v1.0. The architecture pivot to VE3 API consumption does not change user needs — it changes how needs are met.

- **7 user personas** defined with goals, pain points, and technical proficiency levels:
  - Sarah (Motorist/Citizen) — find cheapest fuel nearby
  - Raj (Independent Forecourt Owner) — comply with regulations with minimal effort
  - Claire (Supermarket IT Manager) — automate price submission via API
  - David (CMA Enforcement Officer) — monitor compliance, gather evidence
  - Emma (Third-Party Developer) — integrate fuel data into navigation app
  - Tom (DESNZ Policy Analyst) — analyse fuel price trends for ministerial briefings
  - Mike (Commuter Driver) — find fuel via Android Auto / Apple CarPlay while driving

- **7 use cases** (UC-1 through UC-7) with detailed main flows, alternative flows, exception flows, and business rules

- **REQ v3.0 update**: Requirements now distinguish [VE3] responsibilities (retailer data submission, real-time ingestion, feed normalisation) from [CMA] responsibilities (citizen search, enforcement monitoring, policy analytics). This distinction clarifies user journeys served by each layer

- **12 stakeholder groups** with drivers, goals, and measurable outcomes mapped to requirements (ARC-001-STKE-v1.0)

- **Digital inclusion** explicitly addressed: assisted digital channel for retailers with low digital confidence (BR-001, Persona Raj); progressive enhancement for core functionality without JavaScript (NFR-U-001)

**User Research Conducted**:

- [x] User personas created (7 personas in ARC-001-REQ-v3.0)
- [x] User journey mapping done (7 use cases with flows)
- [x] Accessibility needs identified (WCAG 2.2 AA, assisted digital)
- [x] Digital inclusion considerations documented (low-digital-confidence retailers, low-bandwidth connections)
- [x] VE3 vs CMA responsibility split clarified in REQ v3.0 user journey context
- [ ] User interviews completed — interviews planned but dates still TBC (ARC-001-STKE-v1.0)

**Gaps/Actions Required**:

- **MEDIUM**: Schedule and conduct user research interviews with real motorists, independent retailers, and CMA enforcement officers. GDS Beta assessment will examine user research evidence and requires demonstrated iteration based on real user feedback.

---

## TCoP Point 2: Make Things Accessible and Inclusive

**Guidance**: Make sure your technology, infrastructure and systems are accessible and inclusive for all users.

**Reference**: https://www.gov.uk/guidance/make-things-accessible

### Assessment

**Status**: ✅ Compliant

**Score**: 9/10 (unchanged from v1.0)

**Evidence**:

Accessibility requirements are unchanged and remain comprehensive. The VE3 API pivot means accessibility obligations are entirely concentrated in the CMA-owned citizen-facing layer and enforcement portal — both designed to GOV.UK Design System standards.

- **NFR-U-002**: WCAG 2.2 Level AA compliance mandated under Public Sector Bodies Accessibility Regulations 2018
- **NFR-U-001**: GOV.UK Design System mandated for all citizen-facing interfaces
- **NFR-U-003**: English mandatory; Welsh language support for citizen-facing pages (Welsh Language Act compliance)
- **Principle 2** (Citizen-Centred Design): WCAG 2.2 AA as minimum, support for low digital confidence, performance budgets for low-bandwidth connections
- The CMA Open Data API (distinct from VE3 raw API) adds geospatial search capabilities with an accessible list-view alternative for screen reader users

**Accessibility Standards**:

- [x] WCAG 2.2 Level AA compliance target set (NFR-U-002)
- [x] Assistive technology testing specified — NVDA, JAWS, VoiceOver (NFR-U-002)
- [x] Accessibility testing in CI/CD pipeline — axe-core automated testing (NFR-U-002)
- [x] Manual accessibility testing planned before each phase gate (NFR-U-002)
- [x] Map alternative: list view of results for screen reader users (ARC-001-REQ-v3.0)
- [ ] Accessibility audit completed — not yet (due before Public Beta)
- [ ] Accessibility statement published — not yet (required before Public Beta)

**Gaps/Actions Required**:

- **LOW**: Complete accessibility audit with specialist provider before Public Beta (already planned, not yet due)
- **LOW**: Publish accessibility statement before Public Beta

---

## TCoP Point 3: Be Open and Use Open Source

**Guidance**: Publish your code and use open source software to improve transparency, flexibility and accountability.

**Reference**: https://www.gov.uk/guidance/be-open-and-use-open-source

### Assessment

**Status**: ✅ Compliant

**Score**: 10/10 (unchanged from v1.0)

**Evidence**:

Open source and open data remain foundational to the Fuel Finder architecture. The VE3 pivot strengthens this: the CMA's own Open Data API enriches and re-publishes VE3 data under OGL v3.0 with geospatial capabilities beyond the raw VE3 feed, increasing the value of the open data layer.

- **NFR-I-002**: Source code must be published in a public repository unless a security exemption applies
- **TC-5**: "Source code MUST be open source unless a specific security exemption is granted"
- **Principle 1** (Open Data by Default): All fuel price data published as open data under Open Government Licence v3.0
- **BR-005**: Public API with OpenAPI specification, bulk download in open formats (CSV, JSON, GeoJSON)
- **DATA v2.0**: PostGIS geospatial enrichment adds value over raw VE3 data for third-party developers
- **ADR-001**: Decision rationale is openly documented in the project record

**Open Source Practices**:

- [x] Code publication planned in open repositories (TC-5, NFR-I-002)
- [x] Open source libraries to be used where appropriate (NFR-I-002)
- [x] Open data published under Open Government Licence v3.0 (BR-005)
- [x] VE3 API consumption decision openly documented (ADR-001)
- [x] OpenAPI specification for CMA Open Data API (NFR-I-001)
- [ ] Contribution guidelines published — not yet (appropriate for Beta)
- [ ] Open source licences reviewed for all dependencies — not yet (pre-development)

**Gaps/Actions Required**:

- **LOW**: Establish open source contribution guidelines before code is published
- **LOW**: Document open source licence review process for third-party dependencies

---

## TCoP Point 4: Make Use of Open Standards

**Guidance**: Build technology that uses open standards to ensure your technology works and communicates with other technology, and can easily be upgraded and expanded.

**Reference**: https://www.gov.uk/guidance/make-use-of-open-standards

### Assessment

**Status**: ✅ Compliant

**Score**: 10/10 (unchanged from v1.0)

**Evidence**:

Open standards are comprehensively specified in REQ v3.0. The VE3 API integration uses OAuth 2.0 client credentials — a mandated open standard — ensuring no proprietary coupling to the VE3 platform.

- **NFR-I-001** (API Standards): RESTful design, JSON request/response, OpenAPI 3.0 specification, RFC 7807 Problem Details for errors, cursor-based pagination, standard rate limiting headers
- **FR-003**: API versioning via URL path (/v1/, /v2/) with deprecation policy
- **FR-005**: Open Data API with GeoJSON for location-aware consumers
- **NFR-SEC-001**: OAuth 2.0 client credentials for VE3 API authentication and CMA API consumers
- **INT-006**: SAML 2.0 or OIDC for CMA corporate identity federation
- **NFR-U-003**: ISO 8601 dates in API responses, UK date format in UI
- **NFR-I-003**: Data export in CSV, JSON, GeoJSON — all open formats
- **DATA v2.0**: PostGIS for geospatial indexing (ISO SQL/MM spatial standard)

**Open Standards Used**:

- [x] RESTful APIs with OpenAPI 3.0 specification (NFR-I-001)
- [x] JSON for data interchange (NFR-I-001, FR-005)
- [x] OAuth 2.0 for VE3 API authentication and CMA consumer API (NFR-SEC-001)
- [x] SAML 2.0 / OIDC for identity federation (INT-006)
- [x] HTML5 via GOV.UK Design System (INT-004, NFR-U-001)
- [x] GeoJSON for geographic data (NFR-I-003)
- [x] RFC 7807 Problem Details for error responses (NFR-I-001)
- [x] ISO SQL/MM spatial standard via PostGIS (DATA v2.0)
- [x] Open standards documented in architecture (NFR-I-001, NFR-I-002)

**Gaps/Actions Required**:

- None identified. Open standards are well-specified and comprehensive.

---

## TCoP Point 5: Use Cloud First

**Guidance**: Consider using public cloud solutions first as stated in the Cloud First policy.

**Reference**: https://www.gov.uk/guidance/use-cloud-first

### Assessment

**Status**: ✅ Compliant

**Score**: 9/10 (improved from 7/10 ⚠️ Partially Compliant in v1.0)

**Evidence**:

The architecture pivot formally resolves the critical gap from v1.0 (no cloud provider ADR). ADR-001 documents the VE3 API consumer architecture decision and identifies AWS eu-west-2 as the primary cloud target for the CMA's own infrastructure. VE3 Global itself operates on UK cloud infrastructure under the DESNZ contract — confirmed in RSCH v4.1.

- **ADR-001**: Formally documents the VE3 API consumer architecture with cost comparison (£500K vs £1.5M TCO over 3 years). AWS eu-west-2 identified as primary cloud for CMA-owned compute
- **TC-1**: All CMA-held data stored and processed within UK sovereign cloud regions (eu-west-2 primary, UK South/West secondary consideration)
- **Principle 3** (Scalability and Elasticity): Horizontal scaling, auto-scaling, distributed deployment across availability zones
- **Principle 15** (Availability and Reliability): Multi-AZ redundancy within UK regions
- **Principle 17** (Infrastructure as Code): All infrastructure defined as code, no manual changes
- **ARC-001-AWRS-v2.0**: AWS cloud research with detailed eu-west-2 service evaluation and pricing
- **ARC-001-AZRS-v2.0**: Azure cloud research with UK South/West evaluation (kept as contingency)
- **VE3 infrastructure**: Confirmed operating on UK cloud under DESNZ contract (RSCH v4.1)
- Consuming VE3 API reduces CMA's cloud footprint significantly — no ingestion worker farms or raw feed storage required

**Cloud First Considerations**:

- [x] Public cloud considered as first option — AWS and Azure both evaluated
- [x] UK sovereign cloud regions required and met (TC-1, ADR-001)
- [x] Cloud security controls specified (NFR-SEC-001 to NFR-SEC-005)
- [x] Data residency requirements met — UK-only (TC-1, Principle 8)
- [x] Auto-scaling specified (NFR-S-001)
- [x] VE3 API consumer architecture formally documented in ADR-001
- [x] AWS eu-west-2 identified as primary cloud in ADR-001 and RSCH v4.1
- [x] VE3 platform confirmed on UK cloud infrastructure (RSCH v4.1)
- [ ] Separate CMA infrastructure ADR (distinct from VE3 API decision) — not yet created as standalone document

**Gaps/Actions Required**:

- **MEDIUM**: Create a dedicated CMA Infrastructure ADR (separate from ADR-001) formally selecting AWS eu-west-2 as the CMA deployment target for the citizen search layer, enforcement portal, and Open Data API. Reference AWRS v2.0 and AZRS v2.0 as evidence base.
- **LOW**: Document NCSC Cloud Security Principles assessment for AWS eu-west-2 once infrastructure ADR is finalised.

---

## TCoP Point 6: Make Things Secure

**Guidance**: Keep systems and data safe with the appropriate level of security.

**Reference**: https://www.gov.uk/guidance/make-things-secure

### Assessment

**Status**: ⚠️ Partially Compliant

**Score**: 7/10 (unchanged from v1.0, but gap nature changed)

**Evidence**:

Security requirements and principles remain strong. The architecture pivot to VE3 API consumption has **reduced** the attack surface materially (no retailer data ingestion layer, no direct feed processing, zero retailer PII in CMA database). However, SECD v1.0 reflects the old ingestion architecture and needs updating; operational security activities remain pending at this phase.

- **Principle 6** (Security by Design): NON-NEGOTIABLE — zero trust, defence-in-depth, encryption everywhere, continuous verification
- **ARC-001-SECD-v1.0**: Secure by Design assessment with STRIDE threat model, NCSC CAF alignment — but written for old architecture (needs v2.0)
- **NFR-SEC-001**: Authentication — OAuth 2.0 client credentials for VE3 API, MFA for CMA enforcement portal, SSO for CMA staff
- **NFR-SEC-002**: RBAC with defined roles and least privilege (enforcement officers, policy analysts, system admins)
- **NFR-SEC-003**: TLS 1.3 in transit, AES-256 at rest, UK sovereign key management
- **NFR-SEC-004**: Secrets management — no secrets in code, managed vault, 90-day rotation for VE3 API credentials
- **NFR-SEC-005**: Vulnerability management — SAST every build, DAST weekly, pen testing by CHECK-approved provider
- **NFR-C-005**: NCSC Secure by Design assessment required before Beta, SIRO sign-off
- **DPIA v2.0**: Zero retailer PII in CMA database — dramatically reduced data breach impact and attack motivation
- **RISK v2.0**: Data breach risk residual reduced (Organisation entity removed means no PII to breach)

**Attack Surface Changes (VE3 Pivot)**:

- VE3 API handles all retailer data submission — CMA no longer processes retailer portal submissions
- CMA OAuth 2.0 token for VE3 API is the new critical secret (90-day rotation, managed vault)
- Reduced to: citizen search, enforcement monitoring, Open Data API, CMA staff portal
- No direct database writes from external parties; all data flows through VE3 API

**Security Controls**:

- [x] Threat modelling completed — STRIDE analysis in ARC-001-SECD-v1.0 (needs v2.0 update)
- [x] Security by design principles applied — Principle 6, NCSC CAF
- [x] Security risk register maintained — ARC-001-RISK-v2.0 (data breach risk residual reduced)
- [x] Data classification maintained — OFFICIAL, OFFICIAL-SENSITIVE for enforcement data
- [x] Encryption at rest and in transit specified (NFR-SEC-003)
- [x] VE3 API credential management specified (NFR-SEC-004)
- [x] Zero PII in CMA database reduces breach impact (DPIA v2.0, DATA v2.0)
- [ ] SECD v2.0 for VE3 architecture — SECD v1.0 reflects old ingestion model
- [ ] Penetration testing completed — planned before Live (phase-appropriate)
- [ ] NCSC Cloud Security Principles assessed — pending CMA infrastructure ADR finalisation
- [ ] Cyber Essentials Plus certified — not yet (required before Live)

**Gaps/Actions Required**:

- **HIGH**: Produce SECD v2.0 aligned to VE3 API consumer architecture — update STRIDE threat model for new attack surface (VE3 API token compromise, stale data exploitation, enforcement data exfiltration)
- **HIGH**: Schedule penetration testing by CHECK-approved provider before Public Beta
- **MEDIUM**: Complete NCSC Cloud Security Principles assessment for AWS eu-west-2 once infrastructure ADR finalised
- **MEDIUM**: Obtain Cyber Essentials Plus certification before Live
- **LOW**: Document VE3 API SLA and security controls provided by DESNZ/VE3 contract (third-party security assurance)

---

## TCoP Point 7: Make Privacy Integral

**Guidance**: Make sure users' rights are protected by integrating privacy as an essential part of your system.

**Reference**: https://www.gov.uk/guidance/make-privacy-integral

### Assessment

**Status**: ✅ Compliant

**Score**: 10/10 (improved from 9/10 in v1.0)

**Evidence**:

This is the standout compliance improvement in v2.0. The architecture pivot eliminates retailer PII from the CMA database entirely, achieving exemplary Privacy by Design. DPIA v2.0 scores LOW residual risk — the optimal outcome.

- **ARC-001-DPIA-v2.0**: Data Protection Impact Assessment — LOW residual risk (down from LOW-MEDIUM in v1.0)
- **ARC-001-DATA-v2.0**: Organisation entity removed entirely — zero retailer PII in CMA database. Only 8 entities: StationProfile, FuelPrice, PriceHistory, EnforcementAlert, AuditLog, DataQualityScore, GeospatialIndex, ApiSyncStatus
- **Principle 21** (Privacy by Design): Minimise personal data, purpose-limited, UK GDPR Article 25 compliance
- **NFR-C-001**: UK GDPR compliance — lawful basis (Art. 6(1)(e) public task), data subject rights, breach notification within 72 hours, data minimisation
- **Personal data scope** (v2.0): Only indirect identifiers remain — CMA officer UUIDs in EnforcementAlert and AuditLog (pseudonymous, not directly identifying to external parties), source IP addresses in AuditLog (ephemeral)
- **Retailer contact data**: Now held exclusively by VE3 / DESNZ under their own GDPR lawful basis. CMA is not joint controller for this data
- **Data retention**: Defined per entity — StationProfile (indefinite public record), FuelPrice (indefinite public record), EnforcementAlert (retention + 6 years), AuditLog (7 years)

**Privacy by Design Achievement (v2.0)**:

The removal of the Organisation entity is a material privacy improvement with direct regulatory significance:

| Aspect | v1.0 | v2.0 |
|--------|------|------|
| Retailer PII in CMA database | Yes (name, email, phone) | No — held by VE3/DESNZ only |
| DPIA residual risk | LOW-MEDIUM | LOW |
| Data breach PII exposure | Retailer contact details | None (pseudonymous CMA officer UUIDs only) |
| CMA GDPR controller scope | Retailer data + public fuel data | Public fuel data only |
| DPA Subject Access Requests | Potentially from retailers | Not applicable to fuel pricing data |

**Privacy Controls**:

- [x] DPIA v2.0 completed with LOW residual risk (ARC-001-DPIA-v2.0)
- [x] Privacy by design principles applied — Organisation entity removed (Principle 21)
- [x] UK GDPR compliance assessed (NFR-C-001)
- [x] Data retention policy defined per entity (DATA v2.0)
- [x] Data subject rights procedures documented (NFR-C-001)
- [x] Data minimisation exemplary — zero retailer PII (DATA v2.0)
- [x] Lawful basis identified — Article 6(1)(e) public task
- [x] No joint controllership with VE3/DESNZ for retailer data
- [ ] Privacy notice published — not yet (required before service go-live)
- [ ] DPO formal sign-off on DPIA v2.0 — pending (DPIA v2.0 in DRAFT)

**Gaps/Actions Required**:

- **LOW**: Obtain DPO formal sign-off on DPIA v2.0 (LOW risk rating expected to expedite sign-off)
- **LOW**: Publish privacy notice before service go-live (covers CMA officer audit log data)

---

## TCoP Point 8: Share, Reuse and Collaborate

**Guidance**: Avoid duplicating effort and unnecessary costs by collaborating across government and sharing and reusing technology, data, and services.

**Reference**: https://www.gov.uk/guidance/share-and-reuse-technology

### Assessment

**Status**: ✅ Compliant

**Score**: 10/10 (improved from 10/10, additional evidence added)

**Evidence**:

The VE3 API consumer architecture is a textbook demonstration of TCoP Point 8. The decision to consume the existing DESNZ-contracted VE3 Fuel Finder API — rather than build CMA's own data ingestion infrastructure — is the defining reuse act of this programme.

- **ADR-001**: Formally documents the reuse decision with TCO comparison (£500K CMA cost consuming VE3 vs £1.5M to build equivalent ingestion capability). Government reuse rationale explicitly referenced
- **ARC-001-SOBC-v1.0**: Commercial case in the Green Book 5-case model — Strategic case explicitly cites VE3 API reuse as a factor achieving government efficiency
- **GOVR v2.0 (Government Reuse Assessment)**: Completed — VE3 Fuel Finder API identified as the primary government platform for reuse
- **Principle 13** (Reuse Government Platforms): Evaluate GaaP services before building bespoke — ADR-001 is the formal evidence of this evaluation
- **INT-003**: GOV.UK Notify for enforcement notices and alerts
- **INT-004**: GOV.UK Design System for all citizen-facing interfaces
- **INT-005**: GOV.UK One Login for future citizen identity (if required)
- **INT-007**: Companies House API for organisation validation (retained for enforcement context)
- **BR-005 / FR-005**: CMA Open Data API adds geospatial search value over raw VE3 API, designed for third-party reuse and innovation under OGL v3.0
- **FR-015**: Developer guidelines for third-party integration (Android Auto / Apple CarPlay via open data API)
- CMA analytics layer adds government value over VE3 data: policy analysis tools for DESNZ, enforcement intelligence for CMA — neither duplicated from VE3

**Reuse and Collaboration**:

- [x] VE3 Fuel Finder API consumed — primary reuse of DESNZ-contracted platform (ADR-001)
- [x] Build vs buy formally documented — ADR-001 with TCO comparison
- [x] GOV.UK Notify, Design System, Companies House API all planned (INT-003/004/007)
- [x] APIs designed for reusability — CMA Open Data API with OpenAPI spec (FR-005, NFR-I-001)
- [x] Collaboration with DESNZ — VE3 contract coordination (ARC-001-STKE-v1.0)
- [x] Open data enables third-party innovation — OGL v3.0 (BR-005)
- [x] GOVR v2.0 completed — government reuse assessment documented

**Common Platforms Used**:

- [x] VE3 Fuel Finder API (DESNZ-contracted) — primary data source
- [x] GOV.UK Notify (INT-003)
- [x] GOV.UK Design System (INT-004)
- [x] GOV.UK One Login (INT-005 — future consideration)
- [ ] GOV.UK Pay — not required (no payment processing)
- [x] Companies House API (INT-007 — enforcement context)

**Gaps/Actions Required**:

- None identified. The VE3 API reuse decision, combined with GOV.UK platform adoption and open data publication, makes this the highest-evidence TCoP Point in the portfolio.

---

## TCoP Point 9: Integrate and Adapt Technology

**Guidance**: Your technology should work with existing technologies, processes and infrastructure in your organisation, and adapt to future demands.

**Reference**: https://www.gov.uk/guidance/integrate-and-adapt-technology

### Assessment

**Status**: ✅ Compliant

**Score**: 10/10 (unchanged from v1.0, VE3 API integration evidence added)

**Evidence**:

Integration architecture is comprehensively defined with the VE3 API as the new primary integration point, plus an adapter pattern that ensures the CMA service is not permanently coupled to any single data provider.

- **INT-001 (VE3 API)**: OAuth 2.0 client credentials, 15-minute polling sync with stale data TTL fallback for resilience (REQ v3.0)
- **Adapter pattern**: VE3ApiAdapter interface in architecture allows swap to alternative data source if VE3 contract ends — documented in ADR-001 as an explicit exit strategy consideration
- **INT-002**: OS AddressBase Gazetteer for address validation and geocoding
- **INT-003**: GOV.UK Notify for enforcement notices
- **INT-004**: GOV.UK Design System for citizen interfaces
- **INT-005**: GOV.UK One Login (future)
- **INT-006**: CMA Identity Provider (SAML 2.0 / OIDC)
- **INT-007**: Companies House API for enforcement context
- **PostGIS geospatial enrichment** (DATA v2.0): Adds spatial indexing to VE3 station data enabling radial search, proximity ranking, and geographic filtering beyond raw VE3 API capabilities
- **Principle 5** (Interoperability): Versioned interfaces, published API contracts, no direct database coupling
- **Principle 11** (Loose Coupling): Independent deployment, async communication where appropriate
- **Principle 12** (Async Communication): 15-minute sync background job decouples CMA read layer from VE3 API availability
- **Stale data resilience**: TTL-based fallback serves cached prices during VE3 API outages (NFR-A-003)

**Key Integration Architecture**:

| System | Integration Method | Owner | Priority |
|--------|-------------------|-------|----------|
| VE3 Fuel Finder API | OAuth 2.0 REST, 15-min polling | DESNZ/VE3 | MUST |
| OS AddressBase Gazetteer | REST API (synchronous) | Ordnance Survey | MUST |
| GOV.UK Notify | REST API + webhooks | GDS | MUST |
| GOV.UK Design System | Frontend framework | GDS | MUST |
| CMA Identity Provider | SAML 2.0 / OIDC | CMA | MUST |
| Companies House API | REST API | Companies House | SHOULD |
| GOV.UK One Login | OIDC (future) | GDS | COULD |
| Android Auto / CarPlay | Via CMA Open Data API | Third-party | SHOULD |

**Integration Considerations**:

- [x] VE3 API integration specified — OAuth 2.0, 15-min polling, TTL resilience (REQ v3.0)
- [x] Adapter pattern documented — enables future API source swap (ADR-001)
- [x] All integration points identified and documented (REQ v3.0)
- [x] API strategy defined (NFR-I-001: RESTful, OpenAPI 3.0, versioning, rate limiting)
- [x] Stale data resilience — cached fallback during VE3 outages (NFR-A-003)
- [x] Future extensibility — EV charging, hydrogen fuel types as future phases
- [x] PostGIS spatial enrichment adds geospatial integration capability (DATA v2.0)

**Gaps/Actions Required**:

- None identified. Integration architecture is well-defined and VE3 adapter pattern provides future-proofing.

---

## TCoP Point 10: Make Better Use of Data

**Guidance**: Use data more effectively by improving your technology, infrastructure and processes.

**Reference**: https://www.gov.uk/guidance/make-better-use-of-data

### Assessment

**Status**: ✅ Compliant

**Score**: 10/10 (improved — DATA v2.0 evidence significantly stronger than v1.0)

**Evidence**:

DATA v2.0 represents a substantially improved data architecture over v1.0, with PostGIS geospatial indexing, a comprehensive governance matrix, anomaly detection, data quality scoring, and historical price storage. The VE3 API pivot means the CMA's data layer is purpose-built for value-add: enrichment, analysis, and open publication rather than raw ingestion.

- **ARC-001-DATA-v2.0**: 8 entities, 78 attributes, ERD (Mermaid), CRUD matrix, data governance matrix, PostGIS geospatial indexing
- **8 entities**: StationProfile, FuelPrice, PriceHistory, EnforcementAlert, AuditLog, DataQualityScore, GeospatialIndex, ApiSyncStatus
- **Zero retailer PII** in CMA database — data is entirely fuel pricing and enforcement data (public interest)
- **Principle 1** (Open Data by Default): Fuel price data published as open data under OGL v3.0
- **Principle 9** (Data Quality and Timeliness): Validation rules, freshness SLA (15-minute sync from VE3), anomaly detection, data lineage
- **Principle 10** (Single Source of Truth): VE3 API is the system of record for real-time prices; CMA database is the enriched, queryable view
- **FR-007**: Data validation, quality scoring, and anomaly detection pipeline
- **FR-011**: Policy analysis and reporting capability for DESNZ ministerial briefings
- **DataQualityScore entity**: Persists quality metrics per station per sync cycle — enables trend analysis of data quality
- **ApiSyncStatus entity**: Full audit trail of each VE3 API sync cycle for data lineage
- **PriceHistory entity**: Historical pricing for trend analysis — CMA adds longitudinal value over point-in-time VE3 API

**Data Value-Add Over Raw VE3 API**:

| Capability | VE3 API (raw) | CMA Open Data API |
|-----------|--------------|------------------|
| Real-time prices | Yes | Yes (15-min lag) |
| Geospatial radial search | No | Yes (PostGIS) |
| Historical price trends | No | Yes (PriceHistory entity) |
| Data quality scoring | No | Yes (DataQualityScore entity) |
| Enforcement context | No | Yes (EnforcementAlert entity) |
| OGL open licence | No | Yes |
| Bulk download (CSV/GeoJSON) | No | Yes |

**Data Management**:

- [x] Data architecture documented (ARC-001-DATA-v2.0 — ERD, entity catalogue, attribute specifications)
- [x] Data quality standards defined (Principle 9, FR-007 — completeness, accuracy, timeliness, consistency)
- [x] DataQualityScore entity persists per-station quality metrics (DATA v2.0)
- [x] Data lineage tracked — ApiSyncStatus logs every VE3 sync cycle (DATA v2.0)
- [x] Open data publication — core to the service (Principle 1, BR-005)
- [x] Historical pricing storage — PriceHistory entity for trend analysis (DATA v2.0)
- [x] Data governance matrix — owners, stewards, custodians defined (ARC-001-DATA-v2.0)
- [x] PostGIS geospatial indexing — value-add enrichment for citizen search (DATA v2.0)

**Gaps/Actions Required**:

- None identified. Data architecture is exemplary for a government open data service.

---

## TCoP Point 11: Define Your Purchasing Strategy

**Guidance**: Your purchasing strategy must show you've considered commercial and technology aspects, and contractual limitations.

**Reference**: https://www.gov.uk/guidance/define-your-purchasing-strategy

### Assessment

**Status**: ✅ Compliant

**Score**: 8/10 (improved from 5/10 ⚠️ Partially Compliant in v1.0)

**Evidence**:

The critical gap from v1.0 (no SOBC) is now closed. SOBC v1.0 provides a complete Green Book 5-case model with ROM budget, commercial case, and management case. ADR-001 provides a formal build vs buy comparison. The VE3 API data is available to CMA at £0 additional cost (DESNZ contract cost not borne by CMA), which significantly strengthens the commercial case.

- **ARC-001-SOBC-v1.0**: Green Book 5-case model — Strategic, Economic, Commercial, Financial, Management cases. ROM budget £3.6M over 3 years (CMA-funded). Includes option appraisal, benefits realisation approach
- **ADR-001**: Build vs buy analysis with TCO comparison — VE3 API consumer (£500K CMA cost) vs build own ingestion (£1.5M TCO). Saving: £1M over 3 years
- **VE3 API data cost**: £0 to CMA — data acquisition cost borne by DESNZ under existing VE3 contract
- **GOVR v2.0**: Government Reuse Assessment completed — VE3 API identified, evaluated, and selected
- **ARC-001-RSCH-v4.1**: Technology research updated with VE3 API commercial terms and capabilities
- **Principle 22** (Sustainability and Cost Efficiency): Value for money, right-sizing, cost reviews
- **NFR-I-002**: No vendor lock-in for data formats — adapter pattern ensures exit path from VE3

**Procurement Strategy**:

- [x] SOBC created with Green Book 5-case model (ARC-001-SOBC-v1.0)
- [x] ROM budget documented — £3.6M over 3 years (SOBC v1.0)
- [x] Build vs buy formally documented with TCO comparison (ADR-001)
- [x] VE3 API reuse decision — £0 data cost to CMA (ADR-001)
- [x] Vendor lock-in risks addressed — adapter pattern, open standards (NFR-I-002, ADR-001)
- [x] Market research conducted (RSCH v4.1, AWRS v2.0, AZRS v2.0)
- [ ] Procurement route formally selected — G-Cloud vs DOS vs open tender not yet documented
- [ ] Crown Commercial Service frameworks reviewed and documented
- [ ] Exit strategy fully documented — adapter pattern noted in ADR-001 but not a standalone exit strategy document
- [ ] Social value considerations documented (Social Value Act 2012)
- [ ] SME access considerations documented

**Gaps/Actions Required**:

- **MEDIUM**: Formally select and document procurement route for CMA infrastructure components — G-Cloud 14 or Digital Outcomes and Specialists 6 (DOS6) most likely; document rationale
- **MEDIUM**: Produce standalone exit strategy document covering VE3 API dependency, cloud provider, and key software components
- **LOW**: Document social value and SME access considerations per Social Value Act 2012

---

## TCoP Point 12: Make Your Technology Sustainable

**Guidance**: Increase sustainability throughout the lifecycle of your technology.

**Reference**: https://www.gov.uk/guidance/make-your-technology-sustainable

### Assessment

**Status**: ⚠️ Partially Compliant

**Score**: 6/10 (slight improvement from 5/10 in v1.0)

**Evidence**:

Sustainability principles are in place and the VE3 API pivot materially reduces the CMA's cloud infrastructure footprint (no ingestion worker farms, smaller database, reduced compute). However, carbon metrics remain undefined and sustainability criteria for cloud provider selection are not documented.

- **Principle 22** (Sustainability and Cost Efficiency): Right-size compute, auto-scaling, energy-efficient architectures, carbon monitoring, data retention policies
- **NFR-S-001**: Auto-scaling to match resources to demand — avoids idle over-provisioning
- **Principle 12** (Async Communication): 15-minute batch sync more energy-efficient than continuous streaming
- **VE3 API consumption reduces CMA footprint**: No retailer submission portal to host, no feed processing worker pool, smaller CMA database (8 entities, ~8,500 station records vs full ingestion pipeline)
- **AWS eu-west-2 sustainability**: AWS publishes Scope 1, 2, 3 emissions data; UK region powered by renewable energy under Power Purchase Agreements — documented in AWRS v2.0
- Data retention policies prevent unnecessary storage growth (DATA v2.0 entity-level retention rules)
- Serverless-ready architecture (Lambda, managed services) further reduces idle compute

**Sustainability Improvements (VE3 Pivot)**:

| Component | Old Architecture | VE3 Consumer Architecture |
|-----------|-----------------|--------------------------|
| Retailer submission portal | Hosted by CMA | Hosted by VE3/DESNZ |
| Feed ingestion workers | CMA-managed | VE3-managed |
| Raw price data storage | CMA database | Not stored by CMA |
| CMA database size | Larger (all entities incl. retailer PII) | Smaller (8 entities, no PII) |
| Overall CMA cloud footprint | Medium | Reduced |

**Sustainability Considerations**:

- [x] Energy-efficient infrastructure — cloud-native, serverless-ready, auto-scaling (NFR-S-001)
- [x] Auto-scaling avoids idle resource waste (Principle 22)
- [x] 15-min batch sync more efficient than continuous streaming (Principle 12)
- [x] VE3 API consumption reduces CMA infrastructure footprint
- [x] AWS eu-west-2 renewable energy credentials available (AWRS v2.0)
- [ ] Carbon footprint quantified — not yet assessed
- [ ] Sustainability metrics defined (transactions per kWh, carbon per query) — not yet
- [ ] Greening Government ICT Strategy alignment formally documented — not yet
- [ ] Sustainable procurement criteria applied — not documented
- [ ] Device lifecycle management — N/A (cloud service, no end-user devices)

**Gaps/Actions Required**:

- **MEDIUM**: Define sustainability metrics — carbon footprint per transaction, energy per API query, aligned with Greening Government ICT Strategy 2021
- **MEDIUM**: Include sustainability and renewable energy criteria formally in CMA infrastructure ADR — reference AWS eu-west-2 renewable energy commitments
- **LOW**: Document hosting sustainability credentials once CMA infrastructure ADR is finalised (AWS eu-west-2 sustainability data available in AWRS v2.0)

---

## TCoP Point 13: Meet the Service Standard

**Guidance**: If you're building a service as part of your technology project or programme, you must meet the Service Standard.

**Reference**: https://www.gov.uk/service-manual/service-standard

### Assessment

**Status**: ⚠️ Partially Compliant

**Score**: 8/10 (improved from 7/10 in v1.0)

**Is this a public-facing service?**: Yes — citizen-facing fuel price comparison service on GOV.UK

**Evidence**:

GDS Service Standard compliance is mandated in requirements. The project is now approaching Beta with a GDS Beta assessment targeted Q3 2026. All prerequisite evidence artefacts exist (requirements, risk, data model, DPIA, SOBC, ADR), but the GDS self-assessment document itself has not yet been prepared.

- **NFR-C-003**: Must comply with all 14 Service Standard points and pass assessment at Alpha, Beta, and Live
- **BR-007**: Must pass GDS Service Standard assessment at each phase gate
- **Stakeholder Goal G-7**: Pass GDS Service Standard assessment at each phase
- **7 personas, 7 use cases** — user research evidence base strong (interviews still needed)
- **Accessibility**: WCAG 2.2 AA, assistive technology, inclusive design (NFR-U-001, NFR-U-002)
- **SOBC v1.0**: Commercial case and cost justification available for GDS scrutiny
- **ADR-001**: Architecture decision evidence for GDS technical assessors
- **Open source commitment**: TC-5, NFR-I-002
- **DPIA v2.0**: Privacy and data governance evidence
- **RISK v2.0**: Risk management evidence (0 High/Critical residual)
- **Performance metrics**: KPIs and success criteria defined (NFR-P-001, NFR-P-003)

**Service Standard Point Coverage** (pre-assessment readiness):

| Service Standard Point | Evidence Available | Gap |
|----------------------|-------------------|-----|
| 1. Understand users and their needs | 7 personas, 7 use cases, STKE v1.0 | User interviews still needed |
| 2. Solve a whole problem for users | UC-1 to UC-7 end-to-end | Prototype not yet built |
| 3. Provide a joined-up experience | GOV.UK Design System, One Login (future) | No prototype |
| 4. Make the service simple to use | GOV.UK Design System, content strategy | Design not yet validated |
| 5. Make sure everyone can use the service | WCAG 2.2 AA, assisted digital | Audit not yet done |
| 6. Have a multidisciplinary team | Required (NFR-C-003) | Team not formally documented |
| 7. Use agile ways of working | Implied, milestones defined | Agile approach not formally documented |
| 8. Iterate based on feedback | Planned — user research TBC | No iteration yet |
| 9. Create a secure service | SECD v1.0, RISK v2.0, DPIA v2.0 | SECD v2.0 needed |
| 10. Define what success looks like | KPIs in success criteria | Agreed with stakeholders? |
| 11. Choose the right tools and technology | ADR-001, AWRS v2.0, AZRS v2.0 | Infrastructure ADR pending |
| 12. Make the codebase public | TC-5, NFR-I-002 | Code not yet written |
| 13. Use and contribute to open standards | NFR-I-001, open standards throughout | Strong |
| 14. Operate a reliable service | NFR-A-001 to NFR-A-003, RISK v2.0 | Operations model not documented |

**Service Standard Compliance**:

- [x] Service assessments planned at each phase gate (NFR-C-003, BR-007)
- [x] User-centred approach — 7 personas, 7 use cases, 12 stakeholder groups
- [x] Performance metrics defined (KPIs, Success Criteria section)
- [x] Assisted digital support planned (BR-001)
- [x] Open source commitment (TC-5, NFR-I-002)
- [x] Beta assessment targeted Q3 2026
- [x] All prerequisite evidence artefacts exist (SOBC, ADR, RISK, DPIA, DATA)
- [ ] GDS Service Standard self-assessment document not yet prepared
- [ ] Alpha assessment not yet passed (Alpha targeted Q2 2026)
- [ ] Agile delivery approach formally documented — implied but not explicit
- [ ] DDaT team composition documented

**Gaps/Actions Required**:

- **MEDIUM**: Prepare GDS Service Standard self-assessment before Beta assessment panel. Run `/arckit:service-assessment`. All evidence artefacts now exist — this is an assembly and self-assessment task.
- **MEDIUM**: Document agile delivery approach and DDaT team composition against DDaT Profession Capability Framework
- **LOW**: Engage GDS assessment team for pre-assessment check-in (mitigates assessment risk, noted in RISK v2.0)

---

## Overall Compliance Summary

### Compliance Scorecard

| TCoP Point | Status | Score | v1.0 Score | Change | Critical Issues |
|------------|--------|-------|-----------|--------|-----------------|
| 1. Define user needs | ✅ Compliant | 9/10 | 9/10 | — | No — interviews TBC but personas comprehensive |
| 2. Make things accessible | ✅ Compliant | 9/10 | 9/10 | — | No — audit not yet due at this phase |
| 3. Be open and use open source | ✅ Compliant | 10/10 | 10/10 | — | No |
| 4. Make use of open standards | ✅ Compliant | 10/10 | 10/10 | — | No |
| 5. Use cloud first | ✅ Compliant | 9/10 | 7/10 | ▲ +2 | No — ADR-001 resolves prior gap |
| 6. Make things secure | ⚠️ Partially Compliant | 7/10 | 7/10 | — | No — pen test and CE+ phase-appropriate; SECD v2.0 needed |
| 7. Make privacy integral | ✅ Compliant | 10/10 | 9/10 | ▲ +1 | No — DPIA v2.0 LOW risk, zero retailer PII |
| 8. Share, reuse and collaborate | ✅ Compliant | 10/10 | 10/10 | — | No |
| 9. Integrate and adapt technology | ✅ Compliant | 10/10 | 10/10 | — | No |
| 10. Make better use of data | ✅ Compliant | 10/10 | 10/10 | — | No |
| 11. Define purchasing strategy | ✅ Compliant | 8/10 | 5/10 | ▲ +3 | No — SOBC created, route not yet selected |
| 12. Make technology sustainable | ⚠️ Partially Compliant | 6/10 | 5/10 | ▲ +1 | No — metrics not yet defined |
| 13. Meet the Service Standard | ⚠️ Partially Compliant | 8/10 | 7/10 | ▲ +1 | No — Beta assessment Q3 2026, self-assessment not yet prepared |
| **Total** | | **116/130** | **108/130** | **▲ +8** | |

**Overall Score**: 116/130 (89%) — 10 Compliant, 3 Partially Compliant, 0 Non-Compliant
*(v1.0: 108/130, 83%, 8 Compliant, 5 Partially Compliant)*

### Critical Issues Requiring Immediate Action

No critical blockers remain. All previously HIGH-priority gaps are resolved or substantially mitigated:

| Previous Critical Issue | Resolution in v2.0 |
|------------------------|-------------------|
| No SOBC | SOBC v1.0 created (Green Book 5-case, £3.6M ROM) |
| Cloud provider not selected / no ADR | ADR-001 documents VE3 API consumer + AWS eu-west-2 identified |
| Procurement route not documented | SOBC v1.0 exists; route selection still needed (MEDIUM priority) |
| DPIA residual risk LOW-MEDIUM | DPIA v2.0 LOW risk; zero retailer PII in CMA database |

### Recommendations

**High Priority** (before Beta assessment):

- Produce SECD v2.0 aligned to VE3 API consumer architecture — STRIDE threat model needs updating for new attack surface (Point 6)
- Conduct user research interviews and demonstrate iteration based on findings — required for GDS Beta assessment (Point 1)
- Prepare GDS Service Standard self-assessment document for Beta panel Q3 2026 (Point 13)

**Medium Priority** (before Public Beta):

- Create CMA Infrastructure ADR (separate from ADR-001) formally selecting AWS eu-west-2 (Point 5)
- Formally select procurement route: G-Cloud 14 or DOS6 (Point 11)
- Obtain DPO sign-off on DPIA v2.0 (Point 7)
- Define sustainability metrics aligned with Greening Government ICT Strategy 2021 (Point 12)
- Document DDaT team composition and agile delivery approach (Point 13)
- Complete NCSC Cloud Security Principles assessment for AWS eu-west-2 (Point 6)
- Document VE3 API third-party security assurance from DESNZ contract (Point 6)

**Low Priority** (before Live):

- Schedule penetration testing by CHECK-approved provider (Point 6)
- Complete accessibility audit with specialist provider (Point 2)
- Obtain Cyber Essentials Plus certification (Point 6)
- Publish accessibility statement and privacy notice (Points 2, 7)
- Produce standalone exit strategy document for VE3 API and cloud provider (Point 11)
- Document social value and SME access considerations (Point 11)
- Document cloud provider sustainability credentials (Point 12)

---

## GovS 005 (Government Functional Standard for Digital) Alignment

> **Note**: The Technology Code of Practice is the **implementation guidance** for [GovS 005 — Government Functional Standard for Digital](https://www.gov.uk/government/publications/government-functional-standard-govs-005-digital). Completing a TCoP review covers the majority of GovS 005 requirements. The mapping below shows how each GovS 005 principle traces to TCoP points assessed above.

### TCoP-to-GovS 005 Principle Mapping

| GovS 005 Principle | Description | TCoP Points | Project Status v2.0 |
|---------------------|-------------|-------------|---------------------|
| User-centred | Services designed around user needs | 1 (Define user needs), 2 (Accessible & inclusive) | ✅ Strong — 7 personas, WCAG 2.2 AA; interviews still needed |
| Open | Open source, open standards, transparency | 3 (Open source), 4 (Open standards) | ✅ Strong — open data, OGL v3.0, ADR-001 published |
| Secure | Proportionate security controls | 6 (Make things secure), 7 (Privacy integral) | ✅ Improving — DPIA v2.0 LOW risk, SECD v2.0 needed |
| Technology | Cloud first, sustainable, integrated | 5 (Cloud first), 9 (Integrate & adapt), 12 (Sustainable) | ✅ Improved — ADR-001 resolves cloud gap; sustainability metrics still absent |
| Data-driven | Evidence-based decisions using data | 10 (Make better use of data) | ✅ Strong — DATA v2.0, PostGIS, historical pricing, open data |
| Inclusive | Accessible to all users and communities | 2 (Accessible & inclusive), 13 (Service Standard) | ✅ Strong — WCAG 2.2 AA, assisted digital; Beta assessment pending |
| Collaborative | Share, reuse, work across boundaries | 8 (Share, reuse & collaborate) | ✅ Exemplary — VE3 API reuse, GOV.UK Notify, Design System, open API |
| Commercially aware | Smart procurement, value for money | 11 (Purchasing strategy) | ✅ Improved — SOBC v1.0, ADR-001 TCO analysis; procurement route pending |
| Sustainable delivery | Lifecycle management, long-term viability | 12 (Sustainable), 9 (Integrate & adapt) | ⚠️ Adequate — reduced footprint via VE3 pivot; carbon metrics not defined |

### GovS 005 Governance Obligations

| Obligation | Status | Evidence / Notes |
|------------|--------|------------------|
| Senior Responsible Owner (SRO) appointed | ✅ MET | CMA SRO identified in ARC-001-STKE-v1.0, RACI matrix |
| Lifecycle stage identified (approaching Beta) | ✅ MET | Beta — enforcement deadline May 2026, GDS Beta assessment Q3 2026 |
| CDDO digital spend control — SOBC submitted | ⚠️ IN PROGRESS | SOBC v1.0 exists; CDDO submission preparation required |
| DDaT capability framework applied to team roles | ⚠️ NOT YET | Team composition not formally documented against DDaT Profession Capability Framework |
| Performance reporting to Permanent Secretary | ⚠️ TO BE ESTABLISHED | Reporting cadence not yet defined; performance metrics in REQ v3.0 |
| Architecture Decision Records maintained | ✅ MET | ADR-001 (VE3 API consumer architecture) — further ADRs needed |

**Overall GovS 005 Alignment Status**: SUBSTANTIALLY ALIGNED — Strong on user-centred, open, data-driven, collaborative, and commercial principles. VE3 API pivot improves commercial and reuse standing materially. Gaps: sustainability metrics, DDaT team documentation, CDDO spend control submission.

---

## Next Steps

**Immediate Actions** (0-30 days — before enforcement deadline May 2026):

- [ ] Produce SECD v2.0 aligned to VE3 API consumer architecture — update STRIDE threat model for new attack surface (`/arckit:secure`) — **required for Beta**
- [ ] Schedule and conduct user research interviews with motorists, retailers, and CMA enforcement officers — **required for GDS Beta assessment**
- [ ] Prepare CDDO spend control submission using SOBC v1.0 as basis — **required for budget approval**
- [ ] Obtain DPO formal sign-off on DPIA v2.0 — LOW risk rating should expedite this

**Short-term Actions** (1-3 months — before GDS Beta assessment Q3 2026):

- [ ] Prepare GDS Service Standard self-assessment for Beta panel (`/arckit:service-assessment`)
- [ ] Create CMA Infrastructure ADR formally selecting AWS eu-west-2 (`/arckit:adr`)
- [ ] Formally select procurement route (G-Cloud 14 / DOS6) and document rationale
- [ ] Define sustainability metrics aligned with Greening Government ICT Strategy 2021 (Point 12)
- [ ] Document DDaT team composition and agile delivery approach
- [ ] Complete NCSC Cloud Security Principles assessment for AWS eu-west-2
- [ ] Document VE3 API third-party security assurance from DESNZ contract

**Long-term Actions** (3-12 months — before Public Beta / Live):

- [ ] Schedule penetration testing by CHECK-approved provider
- [ ] Complete accessibility audit with specialist provider before Public Beta
- [ ] Obtain Cyber Essentials Plus certification before Live
- [ ] Publish accessibility statement and privacy notice before Public Beta
- [ ] Produce standalone exit strategy document (VE3 API and cloud provider)
- [ ] Document sustainability credentials once CMA infrastructure ADR finalised
- [ ] Document social value and SME access considerations

**Review Schedule**: Next TCoP review at Live phase gate (estimated Q1/Q2 2027). Interim review if significant architecture changes occur (new ADRs, regulatory changes).

---

## Approval

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Project Lead | CMA Digital Lead | | |
| Technical Architect | Enterprise Architect | | |
| Senior Responsible Owner | CMA SRO | | |
| Data Protection Officer | CMA DPO | | |
| Digital Spend Control (if applicable) | CDDO Representative | | |

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-000-PRIN-v1.0 | Architecture Principles | Project | 22 principles, technology standards | `projects/000-global/` |
| ARC-001-REQ-v3.0 | Requirements | Project | 56 requirements, VE3 vs CMA distinctions, technical constraints | `projects/001-uk.../` |
| ARC-001-STKE-v1.0 | Stakeholder Analysis | Project | 12 stakeholder groups, 7 goals, RACI, conflicts | `projects/001-uk.../` |
| ARC-001-RISK-v2.0 | Risk Register | Project | 23 risks (21 active), 0 High/Critical residual | `projects/001-uk.../` |
| ARC-001-DATA-v2.0 | Data Model | Project | 8 entities, zero PII, PostGIS, 78 attributes, governance | `projects/001-uk.../` |
| ARC-001-DPIA-v2.0 | DPIA | Project | LOW residual risk, zero retailer PII, lawful basis | `projects/001-uk.../` |
| ARC-001-SECD-v1.0 | Secure by Design | Project | STRIDE threat model, NCSC CAF (needs v2.0 update) | `projects/001-uk.../` |
| ARC-001-SOBC-v1.0 | Strategic Outline Business Case | Project | Green Book 5-case, £3.6M ROM 3-year, VE3 reuse case | `projects/001-uk.../` |
| ARC-001-ADR-001-v1.0 | Architecture Decision Record | Project | VE3 API consumer architecture, TCO comparison £500K vs £1.5M | `projects/001-uk.../` |
| ARC-001-RSCH-v4.1 | Technology Research | Project | VE3 Fuel Finder API findings, vendor profiles | `projects/001-uk.../research/` |
| ARC-001-AWRS-v2.0 | AWS Cloud Research | Project | AWS eu-west-2 services, pricing, sustainability | `projects/001-uk.../research/` |
| ARC-001-AZRS-v2.0 | Azure Cloud Research | Project | Azure UK South/West services, pricing | `projects/001-uk.../research/` |
| ARC-001-DIAG-001-v1.0 | Architecture Diagrams | Project | C4 context and container diagrams | `projects/001-uk.../` |

---

**Generated by**: ArcKit `/arckit.tcop` command
**Generated on**: 2026-04-06 09:00 GMT
**ArcKit Version**: 4.6.3-rc.3
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: Claude Opus 4.6
**Generation Context**: TCoP v2.0 assessment based on 13 project artifacts — VE3 API consumer architecture pivot (ADR-001), REQ v3.0 (56 requirements), DATA v2.0 (8 entities, zero PII, PostGIS), DPIA v2.0 (LOW residual), RISK v2.0 (0 High/Critical), SOBC v1.0 (Green Book 5-case), architecture principles, stakeholder analysis, security design (v1.0), technology research v4.1, AWS/Azure cloud research v2.0, and architecture diagrams. Score improved from 108/130 (83%) to 116/130 (89%).
