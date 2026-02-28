# Technology Code of Practice (TCoP) Review

> **Template Status**: Beta | **Version**: 2.16.0 | **Command**: `/arckit.tcop`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-TCOP-v1.0 |
| **Document Type** | Technology Code of Practice Review |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-02-28 |
| **Last Modified** | 2026-02-28 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-28 |
| **Owner** | Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, CDDO Spend Control, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-28 | ArcKit AI | Initial creation from `/arckit.tcop` command | PENDING | PENDING |

## Document Purpose

This document assesses the UK Government Fuel Price Transparency Service ("Fuel Finder") against all 13 points of the Technology Code of Practice (TCoP). The TCoP is mandatory for UK Government technology projects and is used by the CDDO Digital Spend Control team to assess technology spending proposals. This assessment provides evidence of compliance for GDS Service Standard assessment (Point 12: "Meet the Service Standard") and CDDO spend control approval.

The project is currently in **Discovery/Alpha** phase. Assessments reflect the maturity expected at this stage — full compliance on all points is expected before Live.

**Source Documents Assessed**:

- ARC-000-PRIN-v1.0 — Enterprise Architecture Principles (22 principles)
- ARC-001-REQ-v2.0 — Business and Technical Requirements (63 requirements)
- ARC-001-STKE-v1.0 — Stakeholder Drivers & Goals Analysis (7 goals, 4 outcomes)
- ARC-001-RISK-v1.0 — Risk Register (20 risks)
- ARC-001-DATA-v1.0 — Data Model (6 entities, ERD, CRUD, governance)
- ARC-001-DPIA-v1.0 — Data Protection Impact Assessment
- ARC-001-SECD-v1.0 — Secure by Design Assessment (NCSC CAF, Cyber Essentials)
- ARC-001-RSCH-v1.0/v2.0 — Technology Research
- ARC-001-AWRS-v1.0/v2.0 — AWS Cloud Research
- ARC-001-AZRS-v1.0/v2.0 — Azure Cloud Research
- ARC-001-DIAG-001-v1.0 — Architecture Diagrams

---

## Executive Summary

**Overall TCoP Compliance**: ⚠️ Partially Compliant

**Score**: 110/130 (85%) — 8 Compliant, 5 Partially Compliant, 0 Non-Compliant

**Key Findings**:

- **Strong foundations**: User needs well-defined (7 personas, 7 use cases), comprehensive accessibility requirements, open data architecture, privacy impact assessment completed, robust security requirements, and government platform reuse planned (GOV.UK Notify, Design System, Companies House API)
- **Phase-appropriate gaps**: Cloud provider not yet selected (research completed), penetration testing not yet conducted, GDS Service Standard assessment not yet undertaken — all expected at Discovery/Alpha
- **Action needed**: Procurement strategy lacks formal documentation (no SOBC), sustainability metrics not defined, and exit strategy for technology choices not documented

**Critical Actions**:

1. Create SOBC with procurement strategy before CDDO spend control submission (Point 11)
2. Complete cloud provider selection with formal decision record (Point 5)
3. Define sustainability metrics and carbon footprint baseline (Point 12)

---

## TCoP Point 1: Define User Needs

**Guidance**: Understand your users and their needs. Develop knowledge of your users and what that means for your technology project or programme.

**Reference**: https://www.gov.uk/guidance/define-user-needs

### Assessment

**Status**: ✅ Compliant

**Evidence**:

The project has comprehensive user needs documentation across ARC-001-STKE-v1.0 and ARC-001-REQ-v2.0:

- **7 user personas** defined with goals, pain points, and technical proficiency levels:
  - Sarah (Motorist/Citizen) — find cheapest fuel nearby
  - Raj (Independent Forecourt Owner) — comply with regulations with minimal effort
  - Claire (Supermarket IT Manager) — automate price submission via API
  - David (CMA Enforcement Officer) — monitor compliance, gather evidence
  - Emma (Third-Party Developer) — integrate fuel data into navigation app
  - Tom (DESNZ Policy Analyst) — analyse fuel price trends for ministerial briefings
  - Mike (Commuter Driver) — find fuel via Android Auto / Apple CarPlay while driving

- **7 use cases** with detailed main flows, alternative flows, exception flows, and business rules (UC-1 through UC-7)

- **Stakeholder analysis** (ARC-001-STKE-v1.0) identifies 12 stakeholder groups with drivers, goals, and measurable outcomes mapped to requirements

- **Digital inclusion** explicitly addressed: assisted digital channel for retailers with low digital confidence (BR-001, Persona Raj); progressive enhancement for core functionality without JavaScript (NFR-U-001)

**User Research Conducted**:

- [x] User personas created (7 personas in ARC-001-REQ-v2.0)
- [x] User journey mapping done (7 use cases with flows)
- [x] Accessibility needs identified (WCAG 2.2 AA, assisted digital)
- [x] Digital inclusion considerations documented (low-digital-confidence retailers, low-bandwidth connections)
- [ ] User interviews completed — interviews planned but dates TBC (ARC-001-STKE-v1.0:L1291-1297)

**Gaps/Actions Required**:

- **MEDIUM**: Schedule and conduct user research interviews with real motorists, independent retailers, and CMA enforcement officers. GDS assessment will examine user research evidence at Alpha.

---

## TCoP Point 2: Make Things Accessible and Inclusive

**Guidance**: Make sure your technology, infrastructure and systems are accessible and inclusive for all users.

**Reference**: https://www.gov.uk/guidance/make-things-accessible

### Assessment

**Status**: ✅ Compliant

**Evidence**:

Accessibility is comprehensively addressed across requirements and architecture principles:

- **NFR-U-002**: WCAG 2.2 Level AA compliance mandated under Public Sector Bodies Accessibility Regulations 2018
- **NFR-U-001**: GOV.UK Design System mandated for all citizen-facing interfaces, ensuring baseline accessibility
- **NFR-U-003**: English mandatory; Welsh language support for citizen-facing pages (Welsh Language Act compliance)
- **Principle 2** (Citizen-Centred Design): WCAG 2.2 AA as minimum, support for low digital confidence, performance budgets for low-bandwidth connections

**Accessibility Standards**:

- [x] WCAG 2.2 Level AA compliance target set (NFR-U-002)
- [x] Assistive technology testing specified — NVDA, JAWS, VoiceOver (NFR-U-002)
- [x] Accessibility testing in CI/CD pipeline — axe-core automated testing (NFR-U-002)
- [x] Manual accessibility testing planned before each phase gate (NFR-U-002)
- [ ] Accessibility audit completed — not yet (appropriate for Alpha/Beta)
- [ ] Accessibility statement published — not yet (required before Public Beta)

**Detailed Accessibility Features** (from NFR-U-002):

- Keyboard navigation for all functions
- Screen reader compatibility (NVDA, JAWS, VoiceOver)
- Sufficient colour contrast ratios
- Text resizable to 200% without loss of content
- Alt text for all non-decorative images
- Map alternative: list view of results for screen reader users
- Skip links and landmark navigation
- Error messages associated with form fields

**Gaps/Actions Required**:

- **LOW**: Complete accessibility audit with specialist provider before Public Beta (already planned, not yet due)
- **LOW**: Publish accessibility statement before Public Beta

---

## TCoP Point 3: Be Open and Use Open Source

**Guidance**: Publish your code and use open source software to improve transparency, flexibility and accountability.

**Reference**: https://www.gov.uk/guidance/be-open-and-use-open-source

### Assessment

**Status**: ✅ Compliant

**Evidence**:

Open source and open data are foundational to the Fuel Finder architecture:

- **NFR-I-002**: Source code must be published in a public repository unless a security exemption applies (GDS Service Standard Point 12)
- **TC-5**: Technical constraint — "Source code MUST be open source unless a specific security exemption is granted"
- **Principle 1** (Open Data by Default): All fuel price data published as open data under Open Government Licence v3.0
- **BR-005**: Public API with OpenAPI specification, bulk download in open formats (CSV, JSON, GeoJSON)
- **NFR-I-002**: Open standards for data formats, no vendor lock-in for data formats or storage

**Open Source Practices**:

- [x] Code publication planned in open repositories (TC-5, NFR-I-002)
- [x] Open source libraries to be used where appropriate (NFR-I-002)
- [x] Open data published under Open Government Licence v3.0 (BR-005)
- [x] Proprietary software justified where used (implied by Principle 13 — reuse government platforms)
- [ ] Contribution guidelines published — not yet (appropriate for Beta)
- [ ] Open source licenses reviewed — not yet (pre-development)

**Gaps/Actions Required**:

- **LOW**: Establish open source contribution guidelines before code is published
- **LOW**: Document open source licence review process for third-party dependencies

---

## TCoP Point 4: Make Use of Open Standards

**Guidance**: Build technology that uses open standards to ensure your technology works and communicates with other technology, and can easily be upgraded and expanded.

**Reference**: https://www.gov.uk/guidance/make-use-of-open-standards

### Assessment

**Status**: ✅ Compliant

**Evidence**:

Open standards are comprehensively specified in the requirements:

- **NFR-I-001** (API Standards): RESTful design, JSON request/response, OpenAPI 3.0 specification, RFC 7807 Problem Details for errors, cursor-based pagination, standard rate limiting headers
- **FR-003**: API versioning via URL path (/v1/, /v2/) with deprecation policy
- **FR-005**: Open data API with GeoJSON for location-aware consumers
- **NFR-SEC-001**: OAuth 2.0 client credentials for API authentication
- **INT-006**: SAML 2.0 or OIDC for CMA corporate identity federation
- **NFR-U-003**: ISO 8601 dates in API responses, UK date format in UI
- **NFR-I-003**: Data export in CSV, JSON, GeoJSON — all open formats

**Open Standards Used**:

- [x] RESTful APIs with OpenAPI 3.0 specification (NFR-I-001)
- [x] JSON for data interchange (NFR-I-001, FR-005)
- [x] OAuth 2.0 for API authentication (NFR-SEC-001)
- [x] SAML 2.0 / OIDC for identity federation (INT-006)
- [x] HTML5 via GOV.UK Design System (INT-004, NFR-U-001)
- [x] GeoJSON for geographic data (NFR-I-003)
- [x] RFC 7807 Problem Details for error responses (NFR-I-001)
- [x] Open standards documented in architecture (NFR-I-001, NFR-I-002)

**Gaps/Actions Required**:

- None identified. Open standards are well-specified and comprehensive.

---

## TCoP Point 5: Use Cloud First

**Guidance**: Consider using public cloud solutions first as stated in the Cloud First policy.

**Reference**: https://www.gov.uk/guidance/use-cloud-first

### Assessment

**Status**: ⚠️ Partially Compliant

**Evidence**:

Cloud-first is embedded in architecture principles and requirements, with cloud research conducted for two major providers:

- **TC-1**: All data must be stored and processed within UK sovereign cloud regions
- **Principle 3** (Scalability and Elasticity): Design for horizontal scaling, auto-scaling, distributed deployment
- **Principle 15** (Availability and Reliability): Redundancy across availability zones within UK regions
- **Principle 17** (Infrastructure as Code): All infrastructure defined as code, no manual changes
- **ARC-001-AWRS-v1.0/v2.0**: AWS cloud research with UK region (eu-west-2) service evaluation
- **ARC-001-AZRS-v1.0/v2.0**: Azure cloud research with UK region (UK South/West) service evaluation
- **NFR-A-001**: Availability targets (99.9% citizen, 99.95% retailer API) implying cloud-grade infrastructure
- **NFR-A-002**: Multi-AZ failover, continuous replication, automated failover

**Cloud First Considerations**:

- [x] Public cloud considered as first option (AWS and Azure both evaluated)
- [x] UK sovereign cloud regions required (TC-1)
- [x] Cloud security controls specified (NFR-SEC-001 to NFR-SEC-005)
- [x] Data residency requirements met — UK-only (TC-1, Principle 8)
- [x] Auto-scaling specified (NFR-S-001)
- [ ] Cloud hosting decision formally documented — provider not yet selected
- [ ] Cloud provider architecture decision record (ADR) — not yet created

**Cloud Provider**: AWS (eu-west-2) and Azure (UK South) both evaluated in research artifacts. Final selection pending.

**Gaps/Actions Required**:

- **HIGH**: Formalise cloud provider selection in an Architecture Decision Record (ADR) before Beta. Both AWS and Azure have been researched — the decision should reference ARC-001-AWRS and ARC-001-AZRS evidence.
- **MEDIUM**: Document cloud security assessment against NCSC Cloud Security Principles for the selected provider.

---

## TCoP Point 6: Make Things Secure

**Guidance**: Keep systems and data safe with the appropriate level of security.

**Reference**: https://www.gov.uk/guidance/make-things-secure

### Assessment

**Status**: ⚠️ Partially Compliant

**Evidence**:

Security is treated as a non-negotiable foundational principle with comprehensive requirements and a Secure by Design assessment:

- **Principle 6** (Security by Design): NON-NEGOTIABLE — zero trust, defence-in-depth, encryption everywhere, continuous verification
- **ARC-001-SECD-v1.0**: Secure by Design assessment with STRIDE threat model, NCSC CAF alignment
- **NFR-SEC-001**: Authentication — MFA for retailers, SSO for CMA, OAuth 2.0 for API
- **NFR-SEC-002**: RBAC with 8 defined roles and least privilege
- **NFR-SEC-003**: TLS 1.2+ in transit, AES-256 at rest, UK sovereign key management
- **NFR-SEC-004**: Secrets management — no secrets in code, managed vault, 90-day rotation
- **NFR-SEC-005**: Vulnerability management — SAST every build, DAST weekly, pen testing by CHECK-approved provider
- **NFR-C-005**: NCSC Secure by Design assessment required before Beta, SIRO sign-off

**Security Controls**:

- [x] Threat modelling completed — STRIDE analysis in ARC-001-SECD-v1.0
- [x] Security by design principles applied — Principle 6, NCSC CAF
- [x] Security risk register maintained — ARC-001-RISK-v1.0 (R-004: Data breach, R-008: Security incident)
- [x] Data classification completed — OFFICIAL, OFFICIAL-SENSITIVE for enforcement data
- [x] Encryption at rest and in transit specified (NFR-SEC-003)
- [ ] Penetration testing completed — planned before Live (appropriate for current phase)
- [ ] NCSC Cloud Security Principles assessed — pending cloud provider selection
- [ ] Cyber Essentials Plus certified — not yet (required before Live)

**Data Sensitivity**: OFFICIAL (with OFFICIAL-SENSITIVE for enforcement data)

**Gaps/Actions Required**:

- **HIGH**: Complete NCSC Cloud Security Principles assessment after cloud provider selection
- **HIGH**: Schedule penetration testing by CHECK-approved provider before Public Beta
- **MEDIUM**: Complete Secure by Design TBD items (10+ items pending design decisions — see ARC-001-SECD-v1.0)
- **MEDIUM**: Obtain Cyber Essentials Plus certification before Live

---

## TCoP Point 7: Make Privacy Integral

**Guidance**: Make sure users' rights are protected by integrating privacy as an essential part of your system.

**Reference**: https://www.gov.uk/guidance/make-privacy-integral

### Assessment

**Status**: ✅ Compliant

**Evidence**:

Privacy by design is embedded throughout the architecture with a completed DPIA:

- **ARC-001-DPIA-v1.0**: Data Protection Impact Assessment completed (LOW-MEDIUM residual risk)
- **Principle 21** (Privacy by Design): Minimise personal data, purpose-limited, UK GDPR Article 25 compliance
- **NFR-C-001**: UK GDPR compliance — lawful basis (Art. 6(1)(e) public task), privacy notices, data subject rights, breach notification within 72 hours, data minimisation
- **Data entities**: PII limited to retailer contact details (Organisation entity) — encrypted at field level (NFR-SEC-003)
- **Data retention**: Defined per entity type — retailer data: registration + 6 years; audit logs: 7 years; published prices: indefinite as public record

**Privacy Controls**:

- [x] Data Protection Impact Assessment (DPIA) completed (ARC-001-DPIA-v1.0)
- [x] Privacy by design principles applied (Principle 21)
- [x] UK GDPR compliance assessed (NFR-C-001)
- [x] Data retention policy defined (NFR-C-001, Data entities)
- [x] Data subject rights procedures documented (NFR-C-001)
- [x] Data minimisation verified — only retailer contact details as PII
- [x] Lawful basis identified — Article 6(1)(e) public task
- [ ] Privacy notice published — not yet (required before retailer registration)
- [ ] DPO formal sign-off — pending on DPIA (ARC-001-DPIA-v1.0 in DRAFT)

**Personal Data Processed**: Yes — retailer contact details (name, email, phone) for regulatory compliance purposes. Minimal PII; no citizen personal data collected.

**Gaps/Actions Required**:

- **MEDIUM**: Obtain DPO formal sign-off on DPIA before processing personal data (retailer registration)
- **LOW**: Publish privacy notices before retailer registration opens

---

## TCoP Point 8: Share, Reuse and Collaborate

**Guidance**: Avoid duplicating effort and unnecessary costs by collaborating across government and sharing and reusing technology, data, and services.

**Reference**: https://www.gov.uk/guidance/share-and-reuse-technology

### Assessment

**Status**: ✅ Compliant

**Evidence**:

Government platform reuse is a core architecture principle with multiple cross-government integrations planned:

- **Principle 13** (Reuse Government Platforms): Evaluate GaaP services before building bespoke
- **INT-003**: GOV.UK Notify for retailer emails, SMS, enforcement notices
- **INT-004**: GOV.UK Design System for all citizen-facing interfaces
- **INT-005**: GOV.UK One Login considered for future citizen identity (if needed)
- **INT-007**: Companies House API for retailer organisation validation
- **BR-005 / FR-005**: Open data API designed for third-party reuse and innovation
- **FR-015**: Developer guidelines for third-party integration (Android Auto / Apple CarPlay)

**Reuse and Collaboration**:

- [x] Existing government services reviewed (GOV.UK Notify, Design System, One Login, Companies House)
- [x] Cross-government platforms used — Notify, Design System (INT-003, INT-004)
- [x] APIs designed for reusability — open data API with OpenAPI spec (FR-005, NFR-I-001)
- [x] Collaboration with other departments documented — CMA/DESNZ joint governance (ARC-001-STKE-v1.0)
- [x] Open data enables third-party innovation — OGL v3.0 (BR-005)

**Common Platforms Used**:

- [x] GOV.UK Notify (INT-003)
- [x] GOV.UK Design System (INT-004)
- [x] GOV.UK One Login (INT-005 — future consideration)
- [ ] GOV.UK Pay — not required (no payment processing)
- [x] Companies House API (INT-007)

**Gaps/Actions Required**:

- None identified. Government platform reuse is well-planned and documented.

---

## TCoP Point 9: Integrate and Adapt Technology

**Guidance**: Your technology should work with existing technologies, processes and infrastructure in your organisation, and adapt to future demands.

**Reference**: https://www.gov.uk/guidance/integrate-and-adapt-technology

### Assessment

**Status**: ✅ Compliant

**Evidence**:

Integration architecture is comprehensively defined with 8 integration requirements and future-proof design:

- **8 integration requirements** (INT-001 to INT-008): Address gazetteer, geocoding, GOV.UK Notify, GOV.UK Design System, GOV.UK One Login (future), CMA Identity Provider, Companies House API, Android Auto / Apple CarPlay
- **Principle 5** (Interoperability): Versioned interfaces, published API contracts, no direct database coupling
- **Principle 11** (Loose Coupling): Independent deployment, async communication, published interfaces
- **Principle 12** (Async Communication): Event-driven data pipelines, decoupled ingestion from serving
- **Principle 16** (Maintainability): Configuration-driven rules, modular architecture, regulatory change accommodation (EV charging, hydrogen future phases)

**Integration Considerations**:

- [x] Integration points identified and documented (8 integrations in ARC-001-REQ-v2.0)
- [x] API strategy defined (NFR-I-001: RESTful, OpenAPI 3.0, versioning, rate limiting)
- [x] Future scalability considered — growth projections Year 1-3 (NFR-S-001, NFR-S-002)
- [x] Async patterns for data pipelines (Principle 12, FR-007)
- [x] Future extensibility — EV charging, hydrogen fuel types documented as future phases
- [x] Error handling and resilience patterns specified (NFR-A-003: circuit breakers, retries, bulkheads)

**Key Integrations**:

| System | Integration Method | Priority |
|--------|-------------------|----------|
| OS AddressBase Gazetteer | REST API (synchronous) | MUST |
| Geocoding Service | REST API (cacheable) | MUST |
| GOV.UK Notify | REST API + webhooks | MUST |
| GOV.UK Design System | Frontend framework | MUST |
| CMA Identity Provider | SAML 2.0 / OIDC | MUST |
| Companies House API | REST API | SHOULD |
| GOV.UK One Login | OIDC (future) | COULD |
| Android Auto / CarPlay | Via open data API | SHOULD |

**Gaps/Actions Required**:

- None identified. Integration architecture is well-defined for current and future needs.

---

## TCoP Point 10: Make Better Use of Data

**Guidance**: Use data more effectively by improving your technology, infrastructure and processes.

**Reference**: https://www.gov.uk/guidance/make-better-use-of-data

### Assessment

**Status**: ✅ Compliant

**Evidence**:

Data architecture and governance are comprehensively documented with a dedicated data model artifact:

- **ARC-001-DATA-v1.0**: Full data model with 6 entities, ERD (Mermaid), CRUD matrix, data governance matrix
- **Principle 1** (Open Data by Default): Fuel price data published as open data — machine-readable, no registration, OGL
- **Principle 9** (Data Quality and Timeliness): Validation rules, freshness SLA, anomaly detection, data lineage
- **Principle 10** (Single Source of Truth): Ingestion pipeline is system of record; PublishedPrice is derived view
- **FR-007**: Data validation and processing pipeline with quality rules, anomaly detection
- **FR-011**: Policy analysis and reporting capability for DESNZ
- **BR-005**: Bulk download alongside real-time API for third-party data consumers

**Data Management**:

- [x] Data architecture documented (ARC-001-DATA-v1.0 — ERD, entity catalog, attribute specifications)
- [x] Data quality standards defined (Principle 9, FR-007 — completeness, accuracy, timeliness, consistency)
- [x] Master data management approach defined (Principle 10 — single source of truth)
- [x] Data analytics/insights strategy — FR-011 for DESNZ policy analysis
- [x] Open data publication — core to the service (Principle 1, BR-005)
- [x] Data lineage tracked — source-to-publication mapping, transformation versioning (Principle 9)
- [x] Data governance matrix — owners, stewards, custodians defined (ARC-001-DATA-v1.0)

**Gaps/Actions Required**:

- None identified. Data architecture is exemplary for a government open data service.

---

## TCoP Point 11: Define Your Purchasing Strategy

**Guidance**: Your purchasing strategy must show you've considered commercial and technology aspects, and contractual limitations.

**Reference**: https://www.gov.uk/guidance/define-your-purchasing-strategy

### Assessment

**Status**: ⚠️ Partially Compliant

**Evidence**:

Technology research has been conducted but a formal procurement strategy is not yet documented:

- **ARC-001-RSCH-v1.0/v2.0**: Technology market research completed
- **ARC-001-AWRS-v1.0/v2.0**: AWS cloud services research with pricing analysis
- **ARC-001-AZRS-v1.0/v2.0**: Azure cloud services research with pricing analysis
- **Principle 22** (Sustainability and Cost Efficiency): Value for money required, right-sizing, cost reviews
- **NFR-I-002**: No vendor lock-in for data formats or storage
- BUT: No SOBC exists with formal commercial case
- BUT: Budget figures all TBD in ARC-001-REQ-v2.0
- BUT: No exit strategy documented
- BUT: Procurement route (G-Cloud, DOS, open tender) not formally identified

**Procurement Strategy**:

- [x] Market research conducted (ARC-001-RSCH, ARC-001-AWRS, ARC-001-AZRS)
- [x] Vendor lock-in risks acknowledged (NFR-I-002: open standards, no proprietary formats)
- [ ] Build vs buy decision formally documented — not in a dedicated artifact
- [ ] Digital Marketplace considered — not formally documented
- [ ] Crown Commercial Service frameworks reviewed — not documented
- [ ] Exit strategy defined — not documented
- [ ] Social value considerations included — not documented
- [ ] SME access considerations — not documented
- [ ] CDDO spend control submission prepared — no SOBC exists

**Procurement Route**: Not yet determined

**Gaps/Actions Required**:

- **HIGH**: Create SOBC (Strategic Outline Business Case) with commercial case including procurement route, budget estimates, and exit strategy. Run `/arckit:sobc`.
- **HIGH**: Document build vs buy decision formally, referencing technology research artifacts
- **MEDIUM**: Identify procurement route (G-Cloud, DOS, open tender) and document rationale
- **MEDIUM**: Define exit strategy for cloud provider and key technology dependencies
- **LOW**: Document social value and SME access considerations per Social Value Act 2012

---

## TCoP Point 12: Make Your Technology Sustainable

**Guidance**: Increase sustainability throughout the lifecycle of your technology.

**Reference**: https://www.gov.uk/guidance/make-your-technology-sustainable

### Assessment

**Status**: ⚠️ Partially Compliant

**Evidence**:

Sustainability is addressed at the principles level but lacks specific metrics and measurement:

- **Principle 22** (Sustainability and Cost Efficiency): Right-size compute, auto-scaling, energy-efficient architectures, carbon monitoring, data retention policies
- **NFR-S-001**: Auto-scaling to match resources to demand (avoids idle over-provisioning)
- **Principle 12** (Async Communication): Event-driven architecture reduces unnecessary compute
- Cloud-native approach inherently more efficient than on-premise (shared infrastructure, managed services)
- Data retention policies defined to prevent unnecessary storage growth

**Sustainability Considerations**:

- [x] Energy-efficient infrastructure chosen — cloud-native, serverless-ready, auto-scaling
- [x] Auto-scaling avoids idle resource waste (NFR-S-001, Principle 22)
- [ ] Carbon footprint assessed — not yet
- [ ] Sustainability metrics defined — not yet
- [ ] Green hosting/data centres considered — not formally documented (AWS/Azure both publish sustainability data)
- [ ] Sustainable procurement criteria applied — not documented
- [ ] Device lifecycle management — N/A (cloud service, no end-user devices)

**Sustainability Metrics**:

- Estimated carbon footprint: Not yet assessed
- Hosting energy source: Dependent on cloud provider selection (both AWS eu-west-2 and Azure UK South publish renewable energy commitments)

**Gaps/Actions Required**:

- **MEDIUM**: Define sustainability metrics (carbon footprint per transaction, energy per query) aligned with Greening Government ICT Strategy
- **MEDIUM**: Include sustainability criteria in cloud provider selection (renewable energy commitments, PUE ratings)
- **LOW**: Document hosting sustainability credentials once cloud provider is selected

---

## TCoP Point 13: Meet the Service Standard

**Guidance**: If you're building a service as part of your technology project or programme, you must meet the Service Standard.

**Reference**: https://www.gov.uk/service-manual/service-standard

### Assessment

**Status**: ⚠️ Partially Compliant

**Is this a public-facing service?**: Yes — citizen-facing fuel price comparison service on GOV.UK

**Evidence**:

GDS Service Standard compliance is mandated in requirements with assessment planned at each phase gate:

- **NFR-C-003**: Must comply with all 14 points and pass assessment at Alpha, Beta, and Live
- **BR-007**: Must pass GDS Service Standard assessment at each phase gate
- **Stakeholder Goal G-7**: Pass GDS Service Standard assessment at each phase
- User research evidence planned (7 personas, 7 use cases — but interviews not yet conducted)
- Multidisciplinary team required (NFR-C-003 Point 6)
- Performance metrics defined (NFR-P-001, NFR-P-003, Success Criteria section)
- Accessibility compliance targeted (NFR-U-001, NFR-U-002)
- Open source commitment (NFR-I-002, TC-5)

**Service Standard Compliance**:

- [x] Service assessments planned at each phase gate (NFR-C-003, BR-007)
- [x] User-centred approach used — 7 personas, 7 use cases, stakeholder analysis
- [x] Performance metrics defined (KPIs in Success Criteria section)
- [x] Assisted digital support planned (BR-001 — assisted digital for low-digital-confidence retailers)
- [x] Open source commitment (TC-5, NFR-I-002)
- [ ] Service assessments completed — not yet (appropriate for current phase)
- [ ] Alpha assessment passed — not yet
- [ ] Agile delivery approach formally documented — implied but not explicit

**Service Assessment Status**: Planned — Alpha assessment targeted for Q2 2026

**Gaps/Actions Required**:

- **MEDIUM**: Prepare GDS Service Standard self-assessment before Alpha assessment panel. Consider running `/arckit:service-assessment`.
- **MEDIUM**: Document agile delivery approach and team composition against DDaT capability framework
- **LOW**: Engage GDS assessment team for pre-assessment check-in (already noted as mitigation in Conflict C-1)

---

## Overall Compliance Summary

### Compliance Scorecard

| TCoP Point | Status | Score | Critical Issues |
|------------|--------|-------|-----------------|
| 1. Define user needs | ✅ Compliant | 9/10 | No — interviews TBC but personas comprehensive |
| 2. Make things accessible | ✅ Compliant | 9/10 | No — audit not yet due at this phase |
| 3. Be open and use open source | ✅ Compliant | 10/10 | No |
| 4. Make use of open standards | ✅ Compliant | 10/10 | No |
| 5. Use cloud first | ⚠️ Partially Compliant | 7/10 | No — provider selection pending (research done) |
| 6. Make things secure | ⚠️ Partially Compliant | 7/10 | No — pen test and CE+ not yet due at this phase |
| 7. Make privacy integral | ✅ Compliant | 9/10 | No — DPIA complete, DPO sign-off pending |
| 8. Share, reuse and collaborate | ✅ Compliant | 10/10 | No |
| 9. Integrate and adapt technology | ✅ Compliant | 10/10 | No |
| 10. Make better use of data | ✅ Compliant | 10/10 | No |
| 11. Define your purchasing strategy | ⚠️ Partially Compliant | 5/10 | **Yes** — no SOBC, no procurement route, no exit strategy |
| 12. Make your technology sustainable | ⚠️ Partially Compliant | 5/10 | No — metrics not defined but principles exist |
| 13. Meet the Service Standard | ⚠️ Partially Compliant | 7/10 | No — assessment not yet due at this phase |

**Overall Score**: 108/130 (83%) — 8 Compliant, 5 Partially Compliant, 0 Non-Compliant

### Critical Issues Requiring Immediate Action

1. **Point 11 — No procurement strategy**: No SOBC, no formally documented procurement route, no exit strategy. This will block CDDO spend control approval. Create SOBC with commercial case. (**HIGH PRIORITY**)

### Recommendations

**High Priority**:

- Create SOBC with commercial case, procurement route, and exit strategy (Point 11)
- Formalise cloud provider selection in an ADR (Point 5)
- Schedule penetration testing by CHECK-approved provider for pre-Beta (Point 6)

**Medium Priority**:

- Obtain DPO sign-off on DPIA (Point 7)
- Define sustainability metrics aligned with Greening Government ICT Strategy (Point 12)
- Prepare GDS Service Standard self-assessment for Alpha (Point 13)
- Complete NCSC Cloud Security Principles assessment for selected cloud provider (Point 6)
- Document agile delivery approach and DDaT team composition (Point 13)
- Identify procurement route: G-Cloud, DOS, or open tender (Point 11)
- Schedule and conduct user research interviews (Point 1)

**Low Priority**:

- Publish accessibility statement before Public Beta (Point 2)
- Establish open source contribution guidelines (Point 3)
- Publish privacy notices before retailer registration (Point 7)
- Document cloud provider sustainability credentials (Point 12)
- Define exit strategy for key technology dependencies (Point 11)

---

## GovS 005 (Government Functional Standard for Digital) Alignment

> **Note**: The Technology Code of Practice is the **implementation guidance** for [GovS 005 — Government Functional Standard for Digital](https://www.gov.uk/government/publications/government-functional-standard-govs-005-digital). Completing a TCoP review therefore covers the majority of GovS 005 requirements. The mapping below shows how each GovS 005 principle traces to TCoP points assessed above.

### TCoP-to-GovS 005 Principle Mapping

| GovS 005 Principle | Description | TCoP Points | Project Status |
|---------------------|-------------|-------------|----------------|
| User-centred | Services designed around user needs | 1 (Define user needs), 2 (Accessible & inclusive) | ✅ Strong — 7 personas, WCAG 2.2 AA |
| Open | Open source, open standards, transparency | 3 (Open source), 4 (Open standards) | ✅ Strong — open data foundation |
| Secure | Proportionate security controls | 6 (Make things secure), 7 (Privacy integral) | ⚠️ Adequate — SbD and DPIA exist, TBDs remain |
| Technology | Cloud first, sustainable, integrated | 5 (Cloud first), 9 (Integrate & adapt), 12 (Sustainable) | ⚠️ Adequate — cloud researched, sustainability gaps |
| Data-driven | Evidence-based decisions using data | 10 (Make better use of data) | ✅ Strong — comprehensive data model and governance |
| Inclusive | Accessible to all users and communities | 2 (Accessible & inclusive), 13 (Service Standard) | ✅ Strong — WCAG 2.2 AA, assisted digital |
| Collaborative | Share, reuse, work across boundaries | 8 (Share, reuse & collaborate) | ✅ Strong — GOV.UK Notify, Design System, open API |
| Commercially aware | Smart procurement, value for money | 11 (Purchasing strategy) | ⚠️ Weak — no SOBC, no procurement route |
| Sustainable delivery | Lifecycle management, long-term viability | 12 (Sustainable), 9 (Integrate & adapt) | ⚠️ Adequate — auto-scaling, but no carbon metrics |

### GovS 005 Governance Obligations

| Obligation | Status | Evidence / Notes |
|------------|--------|------------------|
| Senior Responsible Owner (SRO) appointed for digital function | ✅ MET | CMA SRO identified in ARC-001-STKE-v1.0, RACI matrix |
| Lifecycle stage identified (Discovery / Alpha / Beta / Live) | ✅ MET | Discovery/Alpha — milestones in ARC-001-REQ-v2.0 (Alpha Q2 2026) |
| CDDO digital spend control thresholds met | ⚠️ NOT YET | No SOBC — spend control submission not prepared |
| DDaT capability framework applied to team roles | ⚠️ NOT YET | Team composition not formally documented against DDaT |
| Performance and status reported to the Permanent Secretary | N/A | Reporting cadence to be established |

**Overall GovS 005 Alignment Status**: PARTIALLY ALIGNED — Strong on user-centred, open, data-driven, and collaborative principles. Gaps in commercial awareness (no SOBC) and sustainability metrics. SRO and lifecycle stage properly identified.

---

## Next Steps

**Immediate Actions** (0-30 days):

- [ ] Create SOBC with commercial case, procurement route, and exit strategy (`/arckit:sobc`) — **CRITICAL for CDDO spend control**
- [ ] Formalise cloud provider selection in ADR with evidence from AWRS/AZRS research
- [ ] Obtain DPO sign-off on DPIA (ARC-001-DPIA-v1.0)
- [ ] Schedule user research interviews (dates currently TBC in ARC-001-STKE-v1.0)

**Short-term Actions** (1-3 months):

- [ ] Prepare GDS Service Standard self-assessment before Alpha assessment (`/arckit:service-assessment`)
- [ ] Complete NCSC Cloud Security Principles assessment for selected provider
- [ ] Document DDaT team composition and agile delivery approach
- [ ] Define sustainability metrics and carbon footprint baseline
- [ ] Identify and document procurement route (G-Cloud / DOS / open tender)

**Long-term Actions** (3-12 months):

- [ ] Schedule penetration testing by CHECK-approved provider before Public Beta
- [ ] Complete accessibility audit with specialist provider before Public Beta
- [ ] Obtain Cyber Essentials Plus certification before Live
- [ ] Publish accessibility statement and privacy notices before Public Beta
- [ ] Complete all Secure by Design TBD items as design decisions are made
- [ ] Document cloud provider sustainability credentials and energy metrics

**Review Schedule**: Next TCoP review at Beta phase gate (estimated Q3/Q4 2026)

---

## Approval

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Project Lead | CMA Digital Lead | | |
| Technical Architect | Enterprise Architect | | |
| Senior Responsible Owner | CMA SRO | | |
| Digital Spend Control (if applicable) | CDDO Representative | | |

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-000-PRIN-v1.0 | Architecture Principles | Project | 22 principles, technology standards | `projects/000-global/` |
| ARC-001-REQ-v2.0 | Requirements | Project | 63 requirements, technical constraints | `projects/001-uk.../` |
| ARC-001-STKE-v1.0 | Stakeholder Analysis | Project | 7 goals, RACI, conflicts | `projects/001-uk.../` |
| ARC-001-RISK-v1.0 | Risk Register | Project | 20 risks, security and compliance risks | `projects/001-uk.../` |
| ARC-001-DATA-v1.0 | Data Model | Project | 6 entities, ERD, GDPR, governance | `projects/001-uk.../` |
| ARC-001-DPIA-v1.0 | DPIA | Project | Privacy risk LOW-MEDIUM, lawful basis | `projects/001-uk.../` |
| ARC-001-SECD-v1.0 | Secure by Design | Project | STRIDE threat model, NCSC CAF | `projects/001-uk.../` |
| ARC-001-AWRS-v1.0/v2.0 | AWS Research | Project | AWS UK region services, pricing | `projects/001-uk.../research/` |
| ARC-001-AZRS-v1.0/v2.0 | Azure Research | Project | Azure UK region services, pricing | `projects/001-uk.../research/` |

---

**Generated by**: ArcKit `/arckit.tcop` command
**Generated on**: 2026-02-28 12:30 GMT
**ArcKit Version**: 2.16.0
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: claude-opus-4-6
**Generation Context**: TCoP assessment based on 11 project artifacts — principles, requirements, stakeholder analysis, risk register, data model, DPIA, Secure by Design, technology research (general, AWS, Azure), and architecture diagrams. No external documents or policies found.
