# UK Grants Research: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.6.4 | **Command**: `/arckit.grants`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GRNT-v1.0 |
| **Document Type** | UK Grants Research |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-04-07 |
| **Last Modified** | 2026-04-07 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-07-07 |
| **Owner** | CMA Digital Lead (Product Owner) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, HM Treasury, Programme Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-07 | ArcKit AI | Initial creation from `/arckit.grants` agent | PENDING | PENDING |

---

## Document Purpose

This document identifies and evaluates UK funding opportunities relevant to the UK Fuel Price Transparency Service ("Fuel Finder"). Each opportunity is scored for eligibility against the project profile. The project is a central government digital service led by the CMA and DESNZ, which significantly constrains eligibility for most external grant programmes (which typically target SMEs, charities, or academic institutions).

## Project Funding Profile

| Attribute | Value |
|-----------|-------|
| **Sector** | Government/Public Sector, Energy/Fuel, Consumer Protection, Open Data |
| **Organisation Type** | Central Government (CMA — statutory regulator; DESNZ — policy department) |
| **TRL Level** | TRL 7-8 (VE3 Global platform operational; CMA service in Alpha/Beta) |
| **Funding Sought** | £3.6M over 3 years (per SOBC ARC-001-SOBC-v1.0) |
| **Project Timeline** | 2026-2028 (enforcement grace period ends May 2026; Beta targeted Q3/Q4 2026) |
| **Key Objectives** | (1) Citizen fuel price comparison on GOV.UK; (2) CMA enforcement tools for retailer compliance; (3) Enhanced open data API with geospatial search and historical trends; (4) DESNZ policy analysis and market monitoring |

### Funding Context

The primary funding mechanism for this project is **HM Treasury departmental allocation** via the SOBC/OBC/FBC business case process. The SOBC (ARC-001-SOBC-v1.0) requests £3.6M over 3 years (ROM +/-30%) with a BCR of 24:1. External grant funding would be supplementary, targeting specific innovation components (geospatial analytics, open data innovation, regulatory technology) rather than the core service build.

**Key constraint**: As a central government body, CMA cannot lead most Innovate UK or UKRI grant applications. Eligible routes are limited to regulator-specific funds, cross-government innovation programmes, and partnership-based academic grants.

## Grant Opportunities

### 1. Regulators' Pioneer Fund (Round 5)

| Attribute | Detail |
|-----------|--------|
| **Funding Body** | DSIT (Department for Science, Innovation and Technology) |
| **Programme** | Regulators' Pioneer Fund |
| **Funding Range** | £50,000 - £1,000,000 per project |
| **Deadline** | Round 5 not yet announced (Round 4 ran Oct 2025 - Sep 2026; Round 5 subject to spending review and HMT approval) |
| **TRL Requirement** | No formal TRL requirement; focus on regulatory innovation |
| **Eligibility Score** | **High** |

**Eligibility Criteria:**

- Applicant must be a UK regulator or local authority — CMA qualifies as a statutory regulator
- Project must create a regulatory environment that fosters business innovation and investment
- 6-12 month project duration
- Must demonstrate innovation in regulatory approach

**Score Rationale:** The CMA is a statutory regulator, making this the strongest-fit funding programme. The Fuel Finder enforcement tools — real-time compliance monitoring, anomaly detection, automated non-compliance flagging — represent genuine regulatory innovation. The open data API enabling third-party innovation (navigation apps, price comparison services) directly supports business innovation. Round 4 awarded £5.5M across 16 projects. However, Round 5 has not been announced and is subject to spending review outcomes.

**Application Process:** Download application form from GOV.UK; submit to regulators.pioneerfund@dsit.gov.uk. Typically opens mid-year with 6-8 week application window.

**URL:** https://www.gov.uk/government/publications/regulators-pioneer-fund-round-4

---

### 2. ADR UK Research Grants (ESRC)

| Attribute | Detail |
|-----------|--------|
| **Funding Body** | ESRC / UKRI (via ADR UK programme) |
| **Programme** | Administrative Data Research UK — Policy Impact Research |
| **Funding Range** | Up to £950,000 per project (18-month awards) |
| **Deadline** | Rolling calls; current round projects start September 2026 |
| **TRL Requirement** | Research-focused (TRL 1-3 equivalent) |
| **Eligibility Score** | **Medium** |

**Eligibility Criteria:**

- Lead applicant must be a UK research organisation eligible for ESRC funding (university or approved research institute)
- Government department can be a data partner and co-investigator but cannot lead
- Project must demonstrate policy impact potential using administrative data
- Part of £168M UKRI investment in ADR UK (2026-2031)

**Score Rationale:** The Fuel Finder dataset — ~8,500 forecourt prices updated in real-time — is a rich administrative dataset with clear policy relevance. DESNZ policy analysis (market competitiveness, geographic pricing patterns, fuel poverty indicators) aligns well with ADR UK's mission to use administrative data for policy impact. However, CMA/DESNZ cannot lead the application; they would need an academic partner (e.g., economics department studying market transparency effects). Funding would support the research/analysis component, not the core service build.

**Application Process:** ESRC standard application via Je-S or the new UKRI funding service. CMA/DESNZ would need to partner with an eligible academic institution.

**URL:** https://www.adruk.org/news-publications/funding-opportunities-1/

---

### 3. Geospatial Commission Innovation Programme

| Attribute | Detail |
|-----------|--------|
| **Funding Body** | Geospatial Commission (now part of GDS/DSIT) |
| **Programme** | Location Data Innovation Competition |
| **Funding Range** | £50,000 - £750,000 per project (£1.5M total pot in recent rounds) |
| **Deadline** | No current open round; previous rounds partnered with Innovate UK |
| **TRL Requirement** | TRL 4-7 (proof of concept to demonstration) |
| **Eligibility Score** | **Medium** |

**Eligibility Criteria:**

- Typically requires UK registered business or research organisation to lead
- Government departments can participate as challenge sponsors or data partners
- Project must use location data to improve public services or drive innovation
- Focus on geospatial innovation with demonstrable public benefit

**Score Rationale:** The Fuel Finder service has a strong geospatial component: PostGIS-indexed forecourt locations, proximity search by coordinates, route-based fuel price lookup, and geographic market analysis. The Geospatial Commission's mission to unlock the value of location data aligns directly. However, CMA would likely need to act as challenge sponsor rather than lead applicant, and no current competition is open. The Geospatial Commission's absorption into GDS may affect future programme structure.

**Application Process:** Via Innovate UK Innovation Funding Service when competitions are open. CMA could propose a challenge or partner with a geospatial SME.

**URL:** https://www.gov.uk/government/news/15-million-geospatial-competition-open-to-improve-public-services

---

### 4. Spark — Technology Innovation Marketplace (DPS)

| Attribute | Detail |
|-----------|--------|
| **Funding Body** | Crown Commercial Service / DSIT |
| **Programme** | Spark Dynamic Purchasing System (RM6094) |
| **Funding Range** | Variable — procurement route, not a grant; individual call-offs typically £50,000 - £500,000 |
| **Deadline** | Open continuously until 15 February 2029 |
| **TRL Requirement** | Proven but innovative technology (TRL 6-9) |
| **Eligibility Score** | **Medium** |

**Eligibility Criteria:**

- Any central government or wider public sector body can use Spark as a buyer
- Suppliers must be on the Spark DPS (new suppliers can join at any time)
- Technology must be innovative (AI, data analytics, IoT, geospatial, etc.)
- Four filters: subject area, delivery method, geography, security level

**Score Rationale:** Spark is not a grant but a procurement mechanism that enables government departments to buy innovative technology. CMA could use Spark to procure specific innovative components: anomaly detection algorithms for price manipulation, geospatial analytics for market analysis, or AI-driven compliance monitoring. This is a realistic route for funding innovation within the project without requiring a traditional grant application. The DPS is open until 2029.

**Application Process:** CMA procurement team raises a further competition on the Spark DPS, specifying the challenge. Suppliers on the DPS bid for the work.

**URL:** https://www.crowncommercial.gov.uk/agreements/RM6094

---

### 5. Innovate UK FAIR Data and AI Benchmarks Competition

| Attribute | Detail |
|-----------|--------|
| **Funding Body** | Innovate UK / UKRI |
| **Programme** | Frontier AI Benchmarking Datasets |
| **Funding Range** | £500,000 - £750,000 per project (£4.5M total pot) |
| **Deadline** | Opens 21 April 2026; Closes 27 May 2026 |
| **TRL Requirement** | TRL 4-7 |
| **Eligibility Score** | **Low** |

**Eligibility Criteria:**

- Lead applicant must be a UK registered business or Research Technology Organisation (RTO)
- Collaborative projects required
- Focus on creating, curating, annotating and exploiting FAIR-data and benchmarks for AI
- Must demonstrate commercial or societal impact

**Score Rationale:** The Fuel Finder's comprehensive open dataset (8,500 forecourts, real-time prices, historical trends, geospatial data) could serve as a FAIR-data benchmark for AI applications in consumer markets or regulatory technology. However, CMA cannot lead the application — a business or RTO partner would need to lead with CMA as data provider. The competition focus on AI benchmarking datasets is tangential to the project's core mission. The timing (opens 21 April 2026) is relevant but the fit is loose.

**Application Process:** Via Innovation Funding Service (apply-for-innovation-funding.service.gov.uk). CMA would need to find a lead applicant partner.

**URL:** https://apply-for-innovation-funding.service.gov.uk/competition/2424/overview/e618b7a8-ab7f-45f3-a098-57c01b334fcd

---

### 6. DSIT Cross-Government Digital Transformation Fund

| Attribute | Detail |
|-----------|--------|
| **Funding Body** | DSIT / GDS |
| **Programme** | Cross-Government Digital Transformation |
| **Funding Range** | Up to £80M total (2025-26); individual department allocations vary |
| **Deadline** | Internal government allocation — not a competitive grant |
| **TRL Requirement** | Not applicable (operational transformation) |
| **Eligibility Score** | **Medium** |

**Eligibility Criteria:**

- Central government departments and arm's-length bodies eligible
- Must support transformation of government corporate functions or services
- Aligned with GDS Blueprint for Modern Digital Government
- Subject to CDDO spend control approval

**Score Rationale:** CMA is eligible as a government body. The Fuel Finder service aligns with the GDS roadmap for modern digital government — it delivers open data, API-first architecture, GOV.UK integration, and cross-department collaboration (CMA/DESNZ). However, this is an internal allocation rather than a competitive grant, and the £80M is spread across all government departments. CMA would need to make a case through departmental spending processes rather than an external application.

**Application Process:** Internal government process via CDDO/GDS. CMA finance team would engage through normal departmental channels.

**URL:** https://gds.blog.gov.uk/2026/01/20/our-roadmap-for-modern-digital-government/

---

### 7. ODI Stimulus Fund / Data Sharing Grants

| Attribute | Detail |
|-----------|--------|
| **Funding Body** | Open Data Institute (ODI), funded by Innovate UK |
| **Programme** | ODI R&D Programme / Stimulus Fund |
| **Funding Range** | £15,000 - £20,000 per project |
| **Deadline** | Periodic calls; no current open round identified |
| **TRL Requirement** | Research/early-stage (TRL 2-4) |
| **Eligibility Score** | **Low** |

**Eligibility Criteria:**

- UK-based organisations working on ethical and trustworthy data sharing
- Projects must explore how data can be shared in more ethical and trustworthy ways
- Part of ODI's £8M R&D programme funded by Innovate UK
- Short-duration projects (typically 3-6 months)

**Score Rationale:** The Fuel Finder's open data approach — publishing enriched fuel price data under the Open Government Licence — aligns philosophically with ODI's mission. However, the funding amounts (£15-20K) are insignificant relative to the project's £3.6M budget. The value would be primarily in thought leadership and ecosystem engagement rather than material funding. CMA could benefit from ODI's expertise in open data standards and governance frameworks rather than their grants.

**Application Process:** Via ODI website when calls are open.

**URL:** https://theodi.org/

---

### 8. Energy Smart Data Scheme (Policy Alignment)

| Attribute | Detail |
|-----------|--------|
| **Funding Body** | DESNZ / DSIT |
| **Programme** | Smart Data Scheme — Energy Sector |
| **Funding Range** | Not a grant; government-funded policy programme |
| **Deadline** | Consultation planned 2026; regulations targeted 2027/28 |
| **TRL Requirement** | Not applicable (policy/regulatory framework) |
| **Eligibility Score** | **Low** (not a grant, but strategic alignment opportunity) |

**Eligibility Criteria:**

- Not a competitive grant — government policy programme
- Fuel Finder is itself a smart data scheme under the Motor Fuel Price Regulations
- Energy Smart Data Scheme targets electricity/gas but creates policy precedent

**Score Rationale:** This is not a funding opportunity per se, but represents strategic alignment. The Fuel Finder is effectively an early exemplar of a government smart data scheme. The Government published its Smart Data Strategy in April 2026, and the Energy Smart Data Scheme (for electricity/gas) is working toward a minimum viable product in late 2026. CMA/DESNZ could position the Fuel Finder as a pathfinder project, potentially unlocking shared infrastructure investment or cross-scheme efficiencies. The strategic value is in policy alignment and shared platform costs rather than direct grant funding.

**Application Process:** Engagement via DESNZ policy channels. No application required — this is about cross-programme coordination.

**URL:** https://www.gov.uk/government/calls-for-evidence/developing-an-energy-smart-data-scheme/developing-an-energy-smart-data-scheme-call-for-evidence-html

---

## Summary Comparison

| Grant | Funder | Amount | Deadline | Eligibility | TRL | Score |
|-------|--------|--------|----------|-------------|-----|-------|
| Regulators' Pioneer Fund (R5) | DSIT | £50K - £1M | Round 5 TBC (expected H2 2026) | Regulators and local authorities | N/A | **High** |
| ADR UK Research Grants | ESRC/UKRI | Up to £950K | Rolling; Sep 2026 start | Academic-led with govt data partner | TRL 1-3 | **Medium** |
| Geospatial Commission Innovation | Geospatial Commission/GDS | £50K - £750K | No current round | Business/RTO-led; govt as sponsor | TRL 4-7 | **Medium** |
| Spark DPS | CCS/DSIT | £50K - £500K (procurement) | Open to Feb 2029 | Any public sector buyer | TRL 6-9 | **Medium** |
| Innovate UK FAIR Data | Innovate UK | £500K - £750K | 21 Apr - 27 May 2026 | Business/RTO-led collaborative | TRL 4-7 | **Low** |
| DSIT Digital Transformation | DSIT/GDS | Variable (£80M total) | Internal allocation | Central government | N/A | **Medium** |
| ODI Stimulus Fund | ODI/Innovate UK | £15K - £20K | Periodic calls | UK-based data orgs | TRL 2-4 | **Low** |
| Energy Smart Data Scheme | DESNZ/DSIT | N/A (policy alignment) | Consultation 2026 | Cross-programme coordination | N/A | **Low** |

## Recommended Funding Strategy

### Top Recommendations

1. **Regulators' Pioneer Fund (Round 5)** — Strongest fit. CMA should prepare an application targeting the enforcement innovation components: real-time compliance monitoring, anomaly detection, and automated non-compliance workflows. The open data API enabling third-party innovation strengthens the case for fostering business innovation. CMA should monitor DSIT announcements for Round 5 opening (likely H2 2026, subject to spending review) and begin drafting the application now using Round 4 guidance.

2. **Spark DPS for Innovation Procurement** — Most immediately actionable. CMA can use Spark to procure innovative technology components today, without waiting for grant rounds. Recommended focus areas: (a) geospatial analytics for market analysis, (b) anomaly detection algorithms for price manipulation, (c) data visualisation for compliance dashboards. This is a procurement route rather than a grant, but achieves the same outcome of accessing innovative solutions.

3. **ADR UK Academic Partnership** — Best route for the research/analytics dimension. CMA/DESNZ should approach an economics or data science department at a Russell Group university to co-develop a research proposal examining the market transparency effects of the Fuel Finder data. This would fund sophisticated policy analysis (fuel poverty indicators, geographic competition patterns, price transmission analysis) while the core service build continues through departmental funding.

### Application Timeline

| Date | Action | Grant |
|------|--------|-------|
| April 2026 | Begin drafting RPF Round 5 application | Regulators' Pioneer Fund |
| April 2026 | Identify academic partner for ADR UK | ADR UK Research Grants |
| May 2026 | Initiate Spark DPS call-off for innovation procurement | Spark DPS |
| H2 2026 | Submit RPF Round 5 application (when announced) | Regulators' Pioneer Fund |
| Q3 2026 | Submit ADR UK research proposal with academic partner | ADR UK Research Grants |
| Ongoing | Monitor Geospatial Commission competitions | Geospatial Innovation |

### Complementary Funding

The recommended strategy layers three funding mechanisms:

- **Departmental allocation** (£3.6M via SOBC) — core service build and operation
- **Regulators' Pioneer Fund** (up to £1M) — enforcement innovation components
- **ADR UK** (up to £950K via academic partner) — policy analysis and research
- **Spark DPS** (variable) — procurement of specific innovative technology

These are complementary, not competing: each targets a different aspect of the project with different eligibility requirements and timelines.

### Total Potential Funding

| Source | Amount | Probability | Expected Value |
|--------|--------|-------------|----------------|
| HM Treasury (SOBC) | £3.6M | High (statutory obligation) | £3.6M |
| Regulators' Pioneer Fund R5 | Up to £1M | Medium (R5 not yet confirmed) | £300K - £500K |
| ADR UK Research | Up to £950K | Medium (requires academic partner) | £200K - £500K |
| Spark DPS innovation | £100K - £300K | High (procurement route, not grant) | £100K - £300K |
| **Total supplementary** | **Up to £2.25M** | — | **£600K - £1.3M** |

## Risks and Considerations

| Risk | Impact | Mitigation |
|------|--------|------------|
| Regulators' Pioneer Fund Round 5 not announced or cancelled due to spending review | Loss of best-fit funding opportunity (up to £1M) | Monitor DSIT announcements; prepare application in advance using Round 4 template; engage DSIT early to signal interest |
| Academic partnership for ADR UK takes too long to establish | Miss September 2026 project start window | Begin partner outreach immediately; DESNZ policy team likely has existing academic relationships |
| Spark DPS call-off procurement timelines slow | Innovation components delayed | Start procurement process in parallel with core build; define clear challenge briefs |
| Grant reporting obligations divert team from delivery | Team capacity stretched across delivery and grant compliance | Ring-fence grant management as a specific role; ensure grant scope is clearly bounded |
| Central government ineligibility for most innovation grants | Limited pool of accessible funding | Focus on regulator-specific and procurement routes; use academic partnerships for UKRI access |
| Co-funding requirements | Some grants may require matched funding from CMA | Ensure SOBC budget has contingency for matched funding; co-funding may come from existing programme budget |

## Spawned Knowledge

The following standalone knowledge files were created or updated from this research:

### Tech Notes

- `tech-notes/regulators-pioneer-fund.md` — Created
- `tech-notes/energy-smart-data-scheme.md` — Created

## External References

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| FFDF | Fuel Finder for drivers_ Factsheet - GOV.UK.pdf | Factsheet | 001-uk-fuel-price-transparency-service/external/ | GOV.UK factsheet on the Fuel Finder scheme for motorists |
| UFP | UpdatedFuelPrice-1775466000049.csv | Data Sample | 001-uk-fuel-price-transparency-service/external/ | Sample VE3 Global fuel price data CSV export |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| *No external document citations used in this artifact — all grant data sourced from live web research* | — | — | — | — |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| Fuel Finder for drivers_ Factsheet - GOV.UK.pdf | 001-uk-fuel-price-transparency-service/external/ | Factsheet covers citizen-facing scheme information; no grant-relevant content |
| UpdatedFuelPrice-1775466000049.csv | 001-uk-fuel-price-transparency-service/external/ | Raw data sample; no grant-relevant content |

---

**Generated by**: ArcKit `/arckit.grants` command
**Generated on**: 2026-04-07
**ArcKit Version**: 4.6.4
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: Claude Opus 4.6 (1M context)
