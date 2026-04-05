# Project Requirements: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.6.3-rc.1 | **Command**: `/arckit.requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-REQ-v3.0 |
| **Document Type** | Business and Technical Requirements |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 3.0 |
| **Created Date** | 2026-04-05 |
| **Last Modified** | 2026-04-05 |
| **Review Cycle** | Monthly |
| **Next Review Date** | 2026-05-05 |
| **Owner** | CMA Digital Lead (Product Owner) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-30 | ArcKit AI | Initial creation from `/arckit.requirements` command | [PENDING] | [PENDING] |
| 2.0 | 2026-01-30 | ArcKit AI | Added in-car platform use case (UC-7), personas (Mike), functional requirements (FR-014, FR-015), integration requirements (INT-008) for Android Auto / Apple CarPlay | [PENDING] | [PENDING] |
| 3.0 | 2026-04-05 | ArcKit AI | Major revision: architecture pivot to consume VE3 Global Fuel Finder API (now production-live); restructured FR/INT requirements to distinguish VE3 Global platform capabilities from CMA-built services; added data synchronisation and enrichment requirements; updated timeline for current project state (registration deadline passed, approaching enforcement grace period end May 2026); aligned budget with SOBC; incorporated findings from research v4.1, gov code search reports, landscape analysis, and cloud platform research | [PENDING] | [PENDING] |

## Document Purpose

This document defines the comprehensive business, functional, non-functional, integration, and data requirements for the UK Government Fuel Price Transparency Service ("Fuel Finder"). It serves as the authoritative requirements baseline for architecture design, vendor evaluation, development, and acceptance testing. Requirements are traced to stakeholder goals (ARC-001-STKE-v1.0) and architecture principles (ARC-000-PRIN-v1.0).

**v3.0 Architecture Context**: The Fuel Finder statutory platform — operated by VE3 Global Ltd under DESNZ contract — went live in early 2026. It provides REST API endpoints for retailer price submission and public data access. The CMA's digital service now **consumes** this platform's Public API rather than building the data ingestion infrastructure from scratch. This fundamentally restructures the integration architecture. Requirements in this document distinguish between capabilities delivered by the VE3 Global platform (marked **[VE3]**) and those requiring CMA development (marked **[CMA]**).

---

## Executive Summary

### Business Context

The Competition and Markets Authority (CMA) recommended an open data scheme for UK fuel prices following its 2023 road fuels market study. The Motor Fuel Price (Open Data) Regulations 2025 (SI 2025/1356) mandate that approximately 8,500 UK fuel forecourts submit real-time pricing data. The Fuel Finder platform, operated by VE3 Global Ltd under DESNZ contract, handles retailer registration and price submission. The CMA's digital service ingests data from the Fuel Finder Public API and provides: a citizen-facing price comparison service, compliance monitoring tools, enforcement case management, and an enhanced open data API.

The service is jointly owned by the CMA (enforcement and digital delivery) and the Department for Energy Security and Net Zero (DESNZ — policy and regulation). It must comply with the GDS Service Standard, Technology Code of Practice, UK GDPR, Secure by Design, and HM Treasury governance frameworks.

**Regulatory timeline update (as of April 2026)**:
- Forecourt registration deadline (2 February 2026): **PASSED** — registration substantially complete
- Enforcement grace period: ends **early May 2026** — enforcement tools MUST be operational
- GDS Beta assessment: targeted **Q3 2026**
- Public Beta launch: targeted **Q3/Q4 2026**

### Objectives

- **O1**: Provide citizens with a simple, accessible tool to find and compare fuel prices near them, leveraging comprehensive data from the Fuel Finder API
- **O2**: Equip CMA with enforcement tools to detect, investigate, and act on retailer non-compliance using data from the Fuel Finder platform
- **O3**: Publish enriched fuel price data as an enhanced open data API with geospatial search, historical trends, and analytics
- **O4**: Enable DESNZ policy analysis through aggregated fuel price trends, geographic patterns, and market competitiveness reporting
- **O5**: Meet all UK Government governance requirements (GDS Service Standard, TCoP, Secure by Design, UK GDPR)

### Expected Outcomes

Traced to stakeholder outcomes (ARC-001-STKE-v1.0):

- **O-1**: ≥ 95% of UK forecourts publishing accurate, current prices within 12 months of launch
- **O-2**: 1 million monthly unique users within 12 months; ≥ 80% user satisfaction
- **O-3**: CMA enforcement capability operational by May 2026; < 24h non-compliance detection
- **O-4**: All mandatory governance gates passed (GDS, Secure by Design, DPIA, TCoP)

### Project Scope

**In Scope (CMA Service — to be built)**:
- Citizen-facing fuel price comparison service on GOV.UK
- Data synchronisation from Fuel Finder Public API (VE3 Global)
- Data enrichment: geospatial indexing, staleness detection, anomaly flagging
- Enhanced open data API for third-party consumers (geospatial search, historical data, bulk download)
- CMA compliance monitoring dashboard and enforcement case management
- DESNZ policy analysis and reporting tools
- Operational dashboards and alerting
- Integration with GOV.UK Notify for enforcement communications

**In Scope (VE3 Global Platform — already operational)**:
- Retailer registration and account management (via GOV.UK One Login)
- Fuel price data submission (REST API for automated, web form for manual)
- Data validation at point of submission
- Primary Fuel Finder Public API and Price Submission API

**Out of Scope**:
- EV charging point pricing (future phase)
- Hydrogen fuel pricing (future phase)
- Fuel quality or availability data
- Direct price regulation or price-cap mechanisms
- Retailer financial systems or POS integration beyond the VE3 Global platform
- Official Fuel Finder mobile app (Phase 1 relies on third-party apps consuming the open API; official companion app for Android Auto / Apple CarPlay is a COULD_HAVE for future phases)
- Building a separate price submission infrastructure (handled by VE3 Global)

---

## Stakeholders

Detailed stakeholder analysis in ARC-001-STKE-v1.0. Summary for requirements context:

| Stakeholder | Role | Organisation | Involvement Level |
|-------------|------|--------------|-------------------|
| CMA SRO | Senior Responsible Owner | CMA | Decision maker, programme accountability |
| CMA Digital Lead | Product and technology delivery | CMA | Requirements definition, architecture |
| CMA Enforcement Lead | Enforcement case management | CMA | Enforcement tool requirements |
| DESNZ Policy Lead | Policy owner, regulatory framework | DESNZ | Regulatory requirements, ministerial briefing |
| GDS Assessment Lead | Service Standard assessment | GDS | Governance gate assessments |
| SIRO | Information risk ownership | CMA | Security and data governance sign-off |
| DPO | Data protection | CMA | DPIA, UK GDPR compliance |
| PRA Representative | Independent retailer trade body | PRA | Retailer usability, compliance burden |
| Citizen User Researchers | User needs validation | CMA Digital | User acceptance, accessibility |
| VE3 Global | Fuel Finder platform operator | VE3 Global / DESNZ | API specification, data availability, SLA |

---

## Business Requirements

### BR-001: Achieve Universal Forecourt Registration **[VE3]**

**Description**: All UK motor fuel traders MUST register their forecourts on the Fuel Finder platform, capturing the information required under the Motor Fuel Price (Open Data) Regulations 2025.

**Rationale**: Registration is the statutory prerequisite for price data submission. Without universal registration, the open data scheme cannot deliver comprehensive market transparency. (Supports Stakeholder Goal G-1, Driver SD-1, SD-3)

**Delivery**: VE3 Global platform (registration via GOV.UK One Login). CMA monitors registration completeness via API data.

**Success Criteria**:
- ≥ 97% of known UK forecourts registered — **substantially achieved** as of April 2026
- Registration process completable within 15 minutes per forecourt
- Assisted digital channel available for retailers unable to self-serve

**Priority**: MUST_HAVE

**Stakeholder**: CMA SRO (G-1), DESNZ Policy (SD-3)

**Principle Alignment**: Principle 2 (Citizen-Centred Design), Principle 13 (Reuse Government Platforms)

---

### BR-002: Achieve Comprehensive Fuel Price Data Submission **[VE3]**

**Description**: Registered forecourts MUST submit current fuel prices for all fuel types they sell via the Fuel Finder Price Submission API or web form, meeting the data quality and timeliness requirements defined in the regulations.

**Rationale**: Comprehensive, timely, accurate price data is the core value proposition. Without it, citizens cannot make informed decisions and CMA cannot analyse market behaviour. (Supports Goal G-2, Drivers SD-1, SD-2, SD-5)

**Delivery**: VE3 Global platform handles price submission. CMA monitors compliance using data from the Public API.

**Success Criteria**:
- ≥ 90% of registered forecourts submitting current prices by end of enforcement grace period (May 2026)
- ≥ 95% compliance within 6 months after grace period
- Data freshness: prices published within 30 minutes of any change (statutory requirement per VE3 API specification)
- Submission rejection rate < 5%

**Priority**: MUST_HAVE

**Stakeholder**: CMA Board (SD-1), CMA Enforcement (SD-2), Citizens (SD-5)

**Principle Alignment**: Principle 1 (Open Data by Default), Principle 9 (Data Quality and Timeliness)

---

### BR-003: Deliver Citizen Fuel Price Comparison Service **[CMA]**

**Description**: The CMA service MUST provide citizens with a simple, accessible, mobile-friendly service to find and compare fuel prices near their location or along a route, using data sourced from the Fuel Finder Public API.

**Rationale**: Citizens are the ultimate beneficiaries. The service must be useful enough to drive adoption and demonstrate consumer benefit. Ministers need a visible, tangible deliverable. (Supports Goal G-3, Outcomes O-1, O-2, Drivers SD-4, SD-5)

**Success Criteria**:
- ≥ 80% user satisfaction (GOV.UK satisfaction survey)
- ≥ 95% task completion rate (find fuel price near me)
- WCAG 2.2 AA compliance
- Page load time p95 < 3 seconds on mobile
- Pass GDS Service Standard assessment at Beta and Live

**Priority**: MUST_HAVE

**Stakeholder**: Citizens (SD-5), DESNZ Ministers (SD-4), GDS Assessors (SD-9)

**Principle Alignment**: Principle 2 (Citizen-Centred Design), Principle 14 (Performance and Efficiency)

---

### BR-004: Provide CMA Enforcement Capability **[CMA]**

**Description**: The CMA service MUST provide enforcement officers with tools to monitor retailer compliance, detect non-compliance, and gather evidence for enforcement actions, using data from the Fuel Finder Public API.

**Rationale**: The regulations grant CMA enforcement powers. Without effective tools, the scheme lacks teeth and compliance will decline. The enforcement grace period ends in early May 2026, so tools must be operational by that date. (Supports Goal G-4, Outcome O-3, Drivers SD-1, SD-2)

**Success Criteria**:
- Enforcement tools operational before grace period ends (May 2026)
- Non-compliance detection within 24 hours of missed submission
- Compliance dashboard showing real-time submission rates, coverage, and timeliness
- Evidence export capability validated by CMA legal team
- Audit trail tamper-evident and admissible

**Priority**: MUST_HAVE

**Stakeholder**: CMA Enforcement (SD-2), CMA Board (SD-1)

**Principle Alignment**: Principle 20 (Regulatory Compliance by Design), Principle 7 (Observability)

---

### BR-005: Publish Enhanced Open Data for Third-Party Innovation **[CMA]**

**Description**: The CMA service MUST publish enriched fuel price data through an enhanced public API and bulk download, licensed under the Open Government Licence, providing value-added capabilities beyond the raw Fuel Finder API (geospatial search, historical trends, quality indicators).

**Rationale**: Third-party consumers amplify the service's reach — citizens may access fuel prices through navigation apps, comparison sites, or news articles rather than directly through GOV.UK. The CMA's enhanced API adds geospatial search and historical data that the VE3 Global API does not provide. (Supports Outcome O-2, Driver SD-11)

**Success Criteria**:
- Public API with OpenAPI specification published
- Geospatial search by coordinates and radius
- Historical price data queryable by date range
- Bulk download available in open formats (CSV, JSON, GeoJSON)
- API developer portal with documentation and sandbox
- ≥ 10 third-party integrations within 12 months of API launch
- Open Government Licence applied to all published data
- API developer guidelines include Android Auto / Apple CarPlay integration patterns

**Priority**: MUST_HAVE

**Stakeholder**: Third-Party Consumers (SD-11), CMA Board (SD-1)

**Principle Alignment**: Principle 1 (Open Data by Default), Principle 5 (Interoperability)

---

### BR-006: Demonstrate Value for Money **[CMA]**

**Description**: The programme MUST deliver within approved budget (£3.6M over 3 years per SOBC) and demonstrate measurable consumer benefit within 12 months of launch.

**Rationale**: Public money accountability is non-negotiable. NAO and PAC will examine whether the programme delivered value. HM Treasury Green Book requires benefits realisation tracking. (Supports Goal G-5, Outcome O-4, Drivers SD-4, SD-12)

**Success Criteria**:
- Programme spend within ±10% of approved budget (£3.6M ROM ±30%)
- Benefits realisation tracker operational from launch
- Economic analysis of price transparency effect commissioned within 6 months
- Annual value for money report published

**Priority**: MUST_HAVE

**Stakeholder**: HM Treasury, NAO/PAC (SD-12), DESNZ Ministers (SD-4)

**Principle Alignment**: Principle 22 (Sustainability and Cost Efficiency)

---

### BR-007: Meet All Governance and Compliance Requirements **[CMA]**

**Description**: The service MUST pass all mandatory UK Government governance gates: GDS Service Standard assessment, Technology Code of Practice compliance, Secure by Design assessment, DPIA completion, and spend control approval.

**Rationale**: Governance compliance is mandatory for government digital services. Failure blocks progression through delivery phases. (Supports Goal G-7, Outcome O-4, Drivers SD-3, SD-9, SD-10)

**Success Criteria**:
- GDS Service Standard assessment passed at Alpha, Beta, and Live
- DPIA completed before personal data processing begins (ARC-001-DPIA-v1.0 complete)
- Secure by Design assessment completed before Beta (ARC-001-SECD-v1.0 complete)
- TCoP compliance evidence documented (ARC-001-TCOP-v1.0 complete)
- CDDO spend control approval obtained

**Priority**: MUST_HAVE

**Stakeholder**: GDS Assessors (SD-9), ICO (SD-10), CDDO, SIRO

**Principle Alignment**: Principles 6, 8, 13, 20, 21

---

### BR-008: Synchronise and Enrich Fuel Finder Data **[CMA]**

**Description**: The CMA service MUST maintain a synchronised, enriched local copy of Fuel Finder data from the VE3 Global Public API, adding geospatial indexing, data quality scoring, staleness detection, anomaly flagging, and historical price storage.

**Rationale**: The VE3 Global API provides raw current data but does not offer geospatial search by coordinates, historical price trends, data quality indicators, or anomaly detection. The CMA service must enrich the data to serve citizen search, compliance monitoring, and policy analysis use cases. Local caching also insulates the CMA service from VE3 API availability issues. (Supports Goals G-2, G-3, G-4)

**Success Criteria**:
- Data synchronisation from Fuel Finder API within 15 minutes of VE3 API data refresh
- All ~8,500 forecourts indexed with geospatial coordinates (PostGIS or equivalent)
- Historical price data retained indefinitely for trend analysis
- Data quality score computed for each forecourt (freshness, completeness, anomaly flag)
- Service continues to serve last-known data during VE3 API outages

**Priority**: MUST_HAVE

**Stakeholder**: CMA Digital Lead, Citizens (SD-5), CMA Enforcement (SD-2), DESNZ Policy (SD-3)

**Principle Alignment**: Principle 4 (Resilience), Principle 9 (Data Quality and Timeliness)

---

## Functional Requirements

### User Personas

#### Persona 1: Sarah — Motorist
- **Role**: Car-owning citizen, commutes 30 miles daily
- **Goals**: Find the cheapest fuel near her home, workplace, or along her route; save money on weekly fill-ups
- **Pain Points**: No single trusted source for all forecourt prices; existing apps have incomplete coverage; unsure if displayed prices are current
- **Technical Proficiency**: Medium (smartphone-competent, uses GOV.UK occasionally)

#### Persona 2: Raj — Independent Forecourt Owner
- **Role**: Owner-operator of a single independent petrol station
- **Goals**: Comply with regulations with minimal effort; avoid penalties; maintain competitiveness
- **Pain Points**: Limited IT capability; no automated pricing system; worried about compliance burden; unclear on regulatory requirements
- **Technical Proficiency**: Low (uses email and basic web browsing; no API capability)
- **Interaction**: Submits prices via VE3 Global web form; monitored for compliance by CMA service

#### Persona 3: Claire — Supermarket Fuel Chain IT Manager
- **Role**: IT manager responsible for fuel pricing systems across 400+ sites
- **Goals**: Automate price submission via API integration; minimise manual processes; ensure data accuracy across all sites
- **Pain Points**: Needs clear API specification; wants test environment; concerned about system reliability and error handling
- **Technical Proficiency**: High (API integration, automated systems, CI/CD)
- **Interaction**: Submits prices via VE3 Global Price Submission API; monitored for compliance by CMA service

#### Persona 4: David — CMA Enforcement Officer
- **Role**: CMA case officer responsible for monitoring retailer compliance
- **Goals**: Identify non-compliant retailers quickly; gather admissible evidence; escalate proportionately
- **Pain Points**: No existing tools for fuel price compliance; needs real-time visibility; evidence must be legally defensible
- **Technical Proficiency**: Medium (uses internal case management systems; needs intuitive dashboards)

#### Persona 5: Emma — Third-Party Developer
- **Role**: Developer at a navigation app company
- **Goals**: Integrate comprehensive UK fuel prices into the app; provide real-time data to users
- **Pain Points**: Current data sources are incomplete or expensive; needs reliable API with good documentation
- **Technical Proficiency**: High (API consumer, mobile app development)

#### Persona 6: Tom — DESNZ Policy Analyst
- **Role**: Policy analyst responsible for fuel market monitoring
- **Goals**: Analyse fuel price trends, geographic patterns, and market competitiveness; support ministerial briefings
- **Pain Points**: No comprehensive dataset for policy analysis; relies on ad-hoc data collection
- **Technical Proficiency**: Medium (spreadsheets, basic data analysis; not a developer)

#### Persona 7: Mike — Commuter Driver Using In-Car Systems
- **Role**: Daily commuter, uses Android Auto or Apple CarPlay in his car
- **Goals**: Find cheapest fuel along his route without taking his eyes off the road; get fuel price alerts while driving; have the fuel station appear as a navigation destination automatically
- **Pain Points**: Can't safely browse web while driving; existing fuel apps don't integrate with car dashboard; wants voice-activated price search; needs simplified UI for glance-and-go in-car display
- **Technical Proficiency**: Medium (uses smartphone daily, comfortable with in-car tech, uses voice assistants)

---

### Use Cases

#### UC-1: Citizen Finds Cheapest Fuel Nearby **[CMA]**

**Actor**: Sarah (Motorist)

**Preconditions**:
- CMA service has synchronised current fuel price data from Fuel Finder API
- Citizen has a web browser (mobile or desktop)

**Main Flow**:
1. Citizen navigates to the Fuel Finder service on GOV.UK
2. System prompts for location (postcode, place name, or "use my location")
3. Citizen enters their postcode or allows geolocation
4. System performs geospatial search against locally indexed data (PostGIS)
5. System displays nearby forecourts with current prices, sorted by price (cheapest first)
6. Citizen can filter by fuel type (E10 unleaded, E5 super unleaded, B7 diesel, SDV premium diesel)
7. Citizen selects a forecourt to see details (address, opening hours, all fuel prices, last updated)
8. System displays directions link (opens in maps application)

**Postconditions**:
- Citizen has identified cheapest fuel option near them
- Page view recorded in analytics

**Alternative Flows**:
- **Alt 3a**: If geolocation denied, system prompts for manual postcode entry
- **Alt 5a**: If no forecourts within default radius, system expands search area and notifies citizen
- **Alt 5b**: If data for a forecourt is stale ( > 24h), system displays "Last updated" warning

**Exception Flows**:
- **Ex 1**: If service unavailable, display GOV.UK standard error page with "try again later" message
- **Ex 2**: If VE3 API sync is delayed, serve cached data with staleness indicator

**Business Rules**:
- Default search radius: 5 miles (configurable)
- Results capped at 20 forecourts per page
- Prices display in pence per litre (PPL) to 1 decimal place (source data is 3 decimal places in GBP)
- "Last updated" timestamp displayed for each forecourt
- Fuel types displayed using consumer-friendly names (Unleaded, Super Unleaded, Diesel, Premium Diesel)

**Priority**: CRITICAL

---

#### UC-2: Independent Retailer Submits Fuel Prices (Manual) **[VE3]**

**Actor**: Raj (Independent Forecourt Owner)

**Preconditions**:
- Retailer has registered on the Fuel Finder platform via GOV.UK One Login
- Retailer is authenticated

**Main Flow**:
1. Retailer logs in to the Fuel Finder service via GOV.UK One Login
2. System displays their registered forecourt(s) (VE3 Global platform)
3. Retailer selects a forecourt to update
4. System displays current published prices and a form for new prices
5. Retailer enters new price(s) for **changed** fuel types only (unchanged prices must not be resubmitted)
6. System validates prices (within plausible range, correct format)
7. Retailer confirms submission
8. System acknowledges receipt with confirmation and timestamp
9. System processes submission asynchronously and publishes updated price within 30 minutes

**Postconditions**:
- Fuel prices updated in the VE3 Global system
- CMA service detects update on next API sync cycle
- Audit trail entry created on VE3 platform

**Business Rules**:
- Prices entered in pence per litre to 1 decimal place
- Only changed prices submitted (VE3 API constraint: unchanged prices must not be resent)
- Submission timestamp recorded in UTC
- Previous prices retained in history

**Priority**: CRITICAL

**Note**: This use case is delivered by VE3 Global's platform. CMA service monitors submission compliance via the Public API.

---

#### UC-3: Large Retailer Submits Prices via API **[VE3]**

**Actor**: Claire (Supermarket IT Manager)

**Preconditions**:
- Retailer organisation registered with API credentials via GOV.UK One Login
- OAuth 2.0 client credentials obtained (client_id + client_secret)
- API integration developed and tested in VE3 sandbox environment

**Main Flow**:
1. Retailer system authenticates via OAuth 2.0 client credentials grant at the VE3 OAuth endpoint with client_id, client_secret, and scope `fuelfinder.write`
2. Bearer credential returned (3600s lifetime)
3. Retailer system calls the Price Submission API endpoint with changed prices only
4. System returns submission acknowledgement
5. Retailer system polls transaction endpoint for status (accepted/rejected)
6. If errors detected, system provides rejection reason

**Postconditions**:
- Prices updated for submitted forecourts on VE3 platform
- CMA service detects updates on next API sync cycle

**Business Rules**:
- Sequential processing: must not send next request until previous response received (429 if violated)
- Changed prices only — unchanged prices must not be resent by changing timestamp
- OAuth 2.0 client credentials grant; separate credentials per environment
- Rate limit: 30 RPM per client, 1 concurrent request
- Test credentials invalid in production and vice versa

**Priority**: CRITICAL

**Note**: This use case is delivered by VE3 Global's platform.

---

#### UC-4: CMA Enforcement Officer Monitors Compliance **[CMA]**

**Actor**: David (CMA Enforcement Officer)

**Preconditions**:
- Officer authenticated with CMA enforcement role (via CMA corporate IdP)
- Compliance monitoring dashboard operational
- CMA service has synchronised data from Fuel Finder API

**Main Flow**:
1. Officer logs in to the enforcement dashboard
2. System displays compliance overview: total registered forecourts, % currently compliant, % non-reporting, trend over time
3. Officer filters by region, retailer type, or non-compliance duration
4. System displays list of non-compliant forecourts with last submission date and contact details
5. Officer selects a forecourt to view submission history (from CMA's locally stored sync data)
6. System displays full compliance timeline: all detected submissions, timestamps, data quality issues, gaps
7. Officer initiates enforcement action (warning letter, formal notice) via integrated workflow
8. System records enforcement action and sends notification via GOV.UK Notify

**Postconditions**:
- Enforcement action recorded in case management
- Retailer notified
- Audit trail updated

**Alternative Flows**:
- **Alt 3a**: Officer exports compliance data to CSV for analysis
- **Alt 7a**: Officer marks forecourt as "under investigation" (restricts visibility to enforcement team)

**Business Rules**:
- Non-compliance defined as: no price update detected from Fuel Finder API within 24 hours of regulatory deadline
- Enforcement actions follow published CMA enforcement guidance escalation path
- Enforcement data access restricted to authorised CMA staff only

**Priority**: CRITICAL

---

#### UC-5: Third-Party Developer Integrates Enhanced Open Data API **[CMA]**

**Actor**: Emma (Third-Party Developer)

**Preconditions**:
- CMA enhanced open data API published with documentation
- No registration required for read-only access

**Main Flow**:
1. Developer discovers API documentation on CMA developer portal
2. Developer reads OpenAPI specification and notes no authentication required
3. Developer tests geospatial queries against the API (search by coordinates + radius)
4. Developer integrates API into their application
5. System serves enriched fuel price data in JSON/GeoJSON format with caching headers
6. Developer's application displays fuel prices with quality indicators and last-updated timestamps

**Postconditions**:
- Third-party application consuming live enriched fuel price data
- API usage metrics recorded

**Business Rules**:
- No authentication required for open data read access
- Rate limit: 300 requests per minute per IP (adjustable)
- Data licensed under Open Government Licence v3.0
- API responses include Cache-Control headers for appropriate client-side caching
- Bulk download available as alternative to high-frequency API polling
- Geospatial search, historical price queries, and quality indicators not available from VE3 API — unique CMA value-add

**Priority**: HIGH

---

#### UC-6: Retailer Registers a Forecourt **[VE3]**

**Actor**: Raj or Claire (Retailer)

**Preconditions**:
- Retailer has GOV.UK One Login account
- Retailer knows their forecourt address and fuel types

**Main Flow**:
1. Retailer navigates to Fuel Finder registration page on GOV.UK
2. Retailer authenticates via GOV.UK One Login
3. System presents registration form (organisation details, forecourt details)
4. Retailer enters organisation details (company name, Companies House number, contact details)
5. Retailer enters forecourt details (address, fuel types sold, operating hours)
6. System validates address and geocodes the forecourt location
7. System creates forecourt record with unique ID in format `GB-NNNNN`
8. System issues API credentials if requested (OAuth 2.0 client credentials)

**Postconditions**:
- Forecourt registered on VE3 Global platform
- Forecourt appears in Fuel Finder API data (detected by CMA service on next sync)

**Business Rules**:
- One organisation can register multiple forecourts
- Each forecourt assigned a unique `GB-NNNNN` identifier
- At least one fuel type must be specified
- Contact details required for compliance communications
- Registration deadline was 2 February 2026 (statutory)

**Priority**: CRITICAL

**Note**: This use case is delivered by VE3 Global's platform. CMA service detects new registrations via API sync.

---

#### UC-7: Driver Finds Cheapest Fuel via Android Auto / Apple CarPlay **[Third-Party + CMA API]**

**Actor**: Mike (Commuter Driver)

**Preconditions**:
- CMA enhanced API has current fuel price data
- Driver has Android Auto or Apple CarPlay connected in their vehicle
- Third-party app consuming the CMA enhanced API installed on smartphone

**Main Flow**:
1. Driver activates voice assistant ("Hey Google, find cheap petrol nearby" or "Hey Siri, find cheap fuel near me")
2. App queries the CMA enhanced open data API with current GPS coordinates and `format=auto` parameter
3. System returns nearby forecourts sorted by cheapest price with distance and navigation-ready coordinates
4. Results displayed on vehicle head unit in simplified card format (station name, price, distance)
5. Driver selects a forecourt by voice or single tap on head unit
6. App launches turn-by-turn navigation to selected forecourt via native maps integration
7. Driver arrives at forecourt with cheapest fuel

**Postconditions**:
- Driver navigated to cheapest fuel option with minimal distraction
- API query recorded in analytics

**Alternative Flows**:
- **Alt 1a**: If no connected car system, driver uses smartphone app directly
- **Alt 2a**: If voice recognition fails, driver uses tap interface on head unit display
- **Alt 4a**: If all nearby forecourts have stale data ( > 24h), results show "Last updated" warning

**Exception Flows**:
- **Ex 1**: If CMA API unavailable, app displays cached results with "Prices may be outdated" warning
- **Ex 2**: If GPS unavailable, prompt driver to enter destination postcode via voice

**Business Rules**:
- In-car display limited to top 5 nearest/cheapest results (driver distraction guidelines)
- Voice interaction must complete within 10 seconds
- No text input permitted while vehicle is in motion
- Results must be readable at a glance (large fonts, high contrast, minimal detail)

**Priority**: SHOULD_HAVE (first phase via third-party apps consuming CMA enhanced API)

---

#### UC-8: CMA Service Synchronises Data from Fuel Finder API **[CMA]**

**Actor**: System (automated)

**Preconditions**:
- CMA service has valid OAuth 2.0 credentials for Fuel Finder Public API
- PostgreSQL + PostGIS database operational

**Main Flow**:
1. Scheduled sync job triggers (every 15 minutes)
2. System authenticates via OAuth 2.0 client credentials grant at the VE3 OAuth endpoint with scope `fuelfinder.read`
3. System calls `GET /api/v1/pfs/fuel-prices` with `effective-start-timestamp` for incremental sync
4. System paginates through results (up to 80 batches)
5. For each forecourt price update: validate, enrich with geospatial index, compute data quality score, detect anomalies
6. System updates local PostGIS database with enriched data
7. System updates historical price table (append-only)
8. System updates compliance metrics (forecourt last-seen timestamp, gap detection)
9. Sync completion logged with metrics (records processed, errors, duration)

**Postconditions**:
- Local database reflects current state of Fuel Finder data
- Historical prices appended
- Compliance metrics updated
- Any anomalies flagged for review

**Alternative Flows**:
- **Alt 3a**: If Fuel Finder API returns 429, system waits per Retry-After header and retries (max 3 retries, exponential backoff)
- **Alt 3b**: If Fuel Finder API returns 5xx, system logs error, serves stale data, and retries on next cycle

**Exception Flows**:
- **Ex 1**: If API unavailable for > 1 hour, alert operations team; citizen service continues with cached data plus staleness indicator

**Business Rules**:
- Sync frequency: every 15 minutes (aligned with VE3 recommended price caching)
- Full sync (all stations): daily at 03:00 UTC
- Incremental sync: every 15 minutes using `effective-start-timestamp`
- Rate limit compliance: stay within 30 RPM per client
- Station metadata sync: every 1 hour (aligned with VE3 caching recommendation)

**Priority**: CRITICAL

---

### Functional Requirements Detail

#### FR-001: Fuel Finder API Data Synchronisation **[CMA]**

**Description**: The CMA service MUST synchronise fuel price and station data from the VE3 Global Fuel Finder Public API on a regular schedule, maintaining a locally enriched copy for all downstream services.

**Relates To**: BR-008, UC-8

**Acceptance Criteria**:
- [ ] Given valid OAuth 2.0 credentials (scope: `fuelfinder.read`), when the sync job runs, then all current price data is retrieved and stored locally
- [ ] Given the incremental sync parameter (`effective-start-timestamp`), when used, then only changed records since last sync are retrieved (reducing API load)
- [ ] Given the VE3 API returns paginated results (up to 80 batches), when syncing, then all pages are consumed completely
- [ ] Given a VE3 API outage, when sync fails, then the system logs the failure, alerts operations, and serves cached data with staleness indicators
- [ ] Given rate limit constraints (30 RPM, 1 concurrent request), when syncing, then the system respects all limits and handles 429 responses with Retry-After backoff

**Data Requirements**:
- **Inputs**: VE3 API responses (station metadata, fuel prices, timestamps)
- **Outputs**: Enriched local database records with geospatial index, quality scores, anomaly flags
- **Validations**: Price plausibility (50.0–500.0 PPL), required fields present, coordinates within UK bounding box

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: INT-001 (Fuel Finder API), PostGIS database infrastructure

---

#### FR-002: Geospatial Price Search **[CMA]**

**Description**: The CMA service MUST provide geospatial fuel price search by coordinates and radius, enabling citizen location-based queries and third-party app integration.

**Relates To**: BR-003, BR-005, UC-1

**Acceptance Criteria**:
- [ ] Given a valid postcode, when the citizen searches, then nearby forecourts are returned sorted by cheapest price, with distance calculated from PostGIS spatial query
- [ ] Given GPS coordinates and radius, when an API consumer queries, then forecourts within the radius are returned with distance in miles
- [ ] Given fuel type filter (E10, E5, B7, SDV), when applied, then only that fuel type's prices are displayed and sorted
- [ ] Given a forecourt with stale data ( > 24h since last update), when displayed, then a visible "Last updated: X hours ago" warning is shown
- [ ] Given no forecourts within 5 miles, when searched, then the system expands to 10 miles and informs the user

**Data Requirements**:
- **Inputs**: Location (postcode, coordinates, or place name), fuel type filter, distance filter
- **Outputs**: List of forecourts with: name, brand, address, distance, fuel prices (PPL), last updated timestamp, data quality indicator
- **Validations**: Valid postcode format, coordinates within UK bounding box (lat 49.0–61.0, lng -8.0–2.0)

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001 (synced data), PostGIS geospatial index, INT-002 (geocoding for postcode lookup)

---

#### FR-003: Citizen Fuel Price Search Interface **[CMA]**

**Description**: The CMA service MUST provide a citizen-facing web interface on GOV.UK for searching and comparing fuel prices, using the GOV.UK Design System.

**Relates To**: BR-003, UC-1

**Acceptance Criteria**:
- [ ] Given a citizen on the GOV.UK service, when they enter a postcode or allow geolocation, then nearby forecourts are displayed sorted by cheapest price
- [ ] Given browser geolocation permission, when granted, then results show nearest forecourts
- [ ] Given fuel type filter selected, when applied, then only that fuel type's prices are displayed
- [ ] Given a forecourt selected, when clicked, then full details displayed (address, all prices, opening hours, last updated, directions link)
- [ ] Given the service running on mobile 3G, when loaded, then page renders within 3 seconds (p95)

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-002 (geospatial search), INT-002 (geocoding), INT-004 (GOV.UK Design System)

---

#### FR-004: Enhanced Open Data API **[CMA]**

**Description**: The CMA service MUST provide an enhanced public read-only API with geospatial search, historical price queries, data quality indicators, and bulk download — capabilities not available from the VE3 Global API directly.

**Relates To**: BR-005, UC-5

**Acceptance Criteria**:
- [ ] Given any client (no authentication), when calling GET /v1/prices with latitude, longitude, and radius, then geospatially-filtered fuel price data is returned in JSON
- [ ] Given a request for historical prices, when calling GET /v1/prices/history with forecourt_id and date range, then historical price records are returned
- [ ] Given a request for bulk data, when calling GET /v1/prices/bulk, then a complete dataset is returned in CSV, JSON, or GeoJSON
- [ ] Given more than 300 requests per minute from a single IP, when rate limited, then the system returns 429 with Retry-After header
- [ ] Given an in-car application, when querying with `format=auto`, then a navigation-optimised response is returned with `geo:` URI coordinates
- [ ] Given API versioning, when a new version is released, then the previous version remains available for at least 6 months

**Data Requirements**:
- **Inputs**: Query parameters (latitude, longitude, radius, fuel_type, format, date_from, date_to, forecourt_id)
- **Outputs**: JSON/GeoJSON array of forecourt objects with prices, location, quality indicators, last_updated; appropriate Cache-Control headers
- **Validations**: Parameters within valid ranges; radius ≤ 50 miles

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001 (synced data), FR-002 (geospatial index), NFR-I-001 (API standards)

---

#### FR-005: Compliance Monitoring Dashboard **[CMA]**

**Description**: The CMA service MUST provide enforcement officers with a dashboard showing retailer compliance status derived from Fuel Finder API data, including submission rates, timeliness, coverage gaps, and non-compliant forecourt identification.

**Relates To**: BR-004, UC-4

**Acceptance Criteria**:
- [ ] Given an authenticated enforcement officer, when accessing the dashboard, then headline compliance metrics are displayed: total registered, % compliant, % non-reporting, trend over time
- [ ] Given filtering by region or retailer type, when applied, then metrics and forecourt lists update accordingly
- [ ] Given a non-compliant forecourt (no price update detected > 24h), when selected, then full compliance timeline and contact details are displayed
- [ ] Given an enforcement action initiated, when the officer triggers a warning, then GOV.UK Notify sends the appropriate template to the retailer
- [ ] Given a request for export, when the officer clicks "Export CSV", then compliance data is downloaded for offline analysis

**Data Requirements**:
- **Inputs**: Enforcement officer authentication, filter criteria
- **Outputs**: Compliance metrics, forecourt lists, compliance timelines, enforcement action records
- **Validations**: Role-based access (enforcement role required)

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: FR-001 (synced data), NFR-SEC-002 (authorisation), INT-003 (GOV.UK Notify)

---

#### FR-006: Data Validation and Quality Scoring **[CMA]**

**Description**: The CMA service MUST validate, enrich, and score all fuel price data received from the Fuel Finder API, applying quality rules and anomaly detection before serving to downstream consumers.

**Relates To**: BR-008

**Acceptance Criteria**:
- [ ] Given a synced price record, when processed, then a data quality score is computed (good/stale/warning) based on freshness and plausibility
- [ ] Given a price outside plausible range ( < 50p or > 500p per litre), when validated, then the record is flagged with a quality warning
- [ ] Given an anomalous price change ( > 20% change within 24 hours), when detected, then an alert is generated for operations review
- [ ] Given a forecourt with no price update for > 24 hours, when detected, then it is flagged as "stale" in citizen-facing results and "non-reporting" in compliance dashboard
- [ ] Given processing pipeline failure, when a sync batch cannot be processed, then it is queued for retry and an alert is raised

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001 (synced data), messaging infrastructure

---

#### FR-007: Enforcement Case Management **[CMA]**

**Description**: The CMA service MUST provide enforcement officers with workflow tools to initiate, track, and manage enforcement actions against non-compliant retailers.

**Relates To**: BR-004, UC-4

**Acceptance Criteria**:
- [ ] Given a non-compliant forecourt identified, when an officer initiates enforcement action, then the action is recorded with: type (reminder/warning/formal_notice/penalty), reason, evidence references, timestamp
- [ ] Given an enforcement action initiated, when triggered, then GOV.UK Notify sends the appropriate notification template to the retailer's registered contact
- [ ] Given an enforcement case, when the officer views it, then the full evidence chain is displayed: compliance timeline, missed submissions, previous actions, retailer responses
- [ ] Given an enforcement action resolved, when the officer closes it, then the resolution is recorded and compliance monitoring resumes

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: FR-005 (compliance dashboard), INT-003 (GOV.UK Notify), FR-009 (audit trail)

---

#### FR-008: Retailer Notifications **[CMA]**

**Description**: The CMA service SHOULD send automated notifications to retailers for compliance reminders and enforcement notices via GOV.UK Notify.

**Relates To**: BR-004

**Acceptance Criteria**:
- [ ] Given a forecourt with no price update detected for 24 hours, when the reminder threshold is reached, then an automated email reminder is sent via GOV.UK Notify
- [ ] Given an enforcement action, when initiated by CMA, then the appropriate notification template is sent to the retailer's registered contact
- [ ] Given a batch of compliance reminders, when triggered, then bulk notifications are sent within GOV.UK Notify capacity limits

**Priority**: SHOULD_HAVE

**Complexity**: LOW

**Dependencies**: INT-003 (GOV.UK Notify), FR-005 (compliance data)

---

#### FR-009: Audit Trail and Evidence Preservation **[CMA]**

**Description**: The CMA service MUST maintain an immutable, tamper-evident audit trail of all enforcement actions, compliance assessments, data sync events, and administrative changes for CMA enforcement purposes.

**Relates To**: BR-004

**Acceptance Criteria**:
- [ ] Given any enforcement action, when recorded, then the complete action is logged with: timestamp (UTC, ms), officer identity, action type, evidence references, and outcome
- [ ] Given an enforcement officer requesting evidence for a forecourt, when queried, then the complete compliance timeline is returned with cryptographic integrity verification
- [ ] Given an attempt to modify an audit record, when detected, then the system prevents modification and logs the attempt as a security event
- [ ] Given audit data older than the retention period, when retention policy executes, then data is archived (not deleted) to tamper-evident long-term storage

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: NFR-C-002 (audit logging), NFR-SEC-003 (encryption)

---

#### FR-010: Policy Analysis and Reporting **[CMA]**

**Description**: The CMA service SHOULD provide DESNZ policy analysts with tools to analyse fuel price trends, geographic patterns, and market competitiveness using historical data.

**Relates To**: BR-006

**Acceptance Criteria**:
- [ ] Given authenticated DESNZ analyst access, when querying historical price data, then aggregate reports are available (average prices by region, fuel type, time period)
- [ ] Given a request for ministerial briefing data, when generated, then headline metrics are exportable (coverage rate, average prices, price trends)
- [ ] Given data export request, when executed, then data is available in CSV and JSON formats

**Priority**: SHOULD_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001 (synced + historical data), data warehouse/analytics capability

---

#### FR-011: Technical Failure Reporting **[CMA]**

**Description**: The CMA service MUST provide a mechanism for retailers to report that they are unable to submit prices due to technical failure, to distinguish genuine non-compliance from technical issues.

**Relates To**: BR-004

**Acceptance Criteria**:
- [ ] Given a retailer experiencing technical issues, when they report a failure via web form or phone, then the forecourt is flagged as "technical failure" rather than "non-compliant"
- [ ] Given a technical failure report, when CMA reviews compliance, then the forecourt is excluded from non-compliance metrics for the reported period
- [ ] Given the technical failure is resolved, when the retailer resumes submissions, then normal compliance monitoring resumes

**Priority**: MUST_HAVE

**Complexity**: LOW

**Dependencies**: FR-005 (compliance dashboard)

---

#### FR-012: Service Feedback and Support **[CMA]**

**Description**: The CMA service SHOULD provide feedback mechanisms for citizens and support channels for retailers needing compliance help.

**Relates To**: BR-003

**Acceptance Criteria**:
- [ ] Given a citizen using the service, when they click "Report a problem" or "Give feedback", then they can submit feedback via standard GOV.UK feedback component
- [ ] Given a retailer needing help, when they access the support section, then plain-English guidance, FAQs, and contact details are available
- [ ] Given feedback submitted, when aggregated, then analytics are available for service improvement

**Priority**: SHOULD_HAVE

**Complexity**: LOW

**Dependencies**: GOV.UK Design System components

---

#### FR-013: Android Auto and Apple CarPlay Compatible API Responses **[CMA]**

**Description**: The enhanced open data API (FR-004) MUST return responses in a format optimised for consumption by Android Auto and Apple CarPlay applications, including simplified result sets and navigation-ready coordinates.

**Relates To**: BR-005, UC-7

**Acceptance Criteria**:
- [ ] Given an API query with `format=auto` parameter, when results are returned, then the response includes a simplified schema with: station_name, brand, fuel_type, price_ppl, distance_miles, latitude, longitude, and navigation_uri (`geo:` URI for native maps)
- [ ] Given in-car display constraints, when results are requested, then the API supports a `limit` parameter (default 5 for in-car use) to restrict result count
- [ ] Given the need for rapid response on mobile networks, when queried from an in-car app, then API response time is < 300ms (p95) for nearby search
- [ ] Given voice-activated search, when a natural language location query is received, then the API accepts lat/lng coordinates as primary location input

**Priority**: SHOULD_HAVE

**Complexity**: LOW (extension of FR-004)

**Dependencies**: FR-004 (Enhanced Open Data API)

---

#### FR-014: Third-Party In-Car App Integration Guidelines **[CMA]**

**Description**: The service SHOULD publish developer guidelines for building Android Auto and Apple CarPlay compatible applications that consume the CMA enhanced API.

**Relates To**: BR-005, UC-7

**Acceptance Criteria**:
- [ ] Given a third-party developer, when they access the developer portal, then in-car integration guidelines are available
- [ ] Given driver safety requirements, when guidelines are published, then they include: maximum results displayed, font size recommendations, voice interaction patterns, prohibited interactions while driving
- [ ] Given platform review requirements, when documented, then guidelines reference CarPlay List Template and Android Auto Place List Template requirements

**Priority**: SHOULD_HAVE

**Complexity**: LOW (documentation)

**Dependencies**: FR-004, developer portal (NFR-M-002)

---

#### FR-015: Historical Price Data Storage and Query **[CMA]**

**Description**: The CMA service MUST retain all historical fuel price data received from the Fuel Finder API and provide query capabilities for trend analysis, policy reporting, and evidence preservation.

**Relates To**: BR-008, FR-010

**Acceptance Criteria**:
- [ ] Given each price data sync from VE3 API, when processed, then all price records are appended to the historical price table (never overwritten)
- [ ] Given a query for historical prices by forecourt, when requested, then all price records for the specified date range are returned chronologically
- [ ] Given a query for aggregate trends, when requested by region or fuel type, then average, min, max, and median prices are computed for the specified period
- [ ] Given historical data growing at ~55M records per year, when stored, then the system handles the volume with appropriate partitioning and archival

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001 (data sync), database infrastructure with partitioning

---

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-001: Citizen Search Response Time

**Requirement**: Citizen-facing fuel price search MUST return results within:
- Page load time: < 3 seconds (p95) on mobile 3G connections
- CMA enhanced API response time for geospatial queries: < 500ms (p95)
- CMA enhanced API response time for geospatial queries: < 200ms (p50)

**Measurement Method**: Real user monitoring (RUM) and synthetic monitoring; APM tooling

**Load Conditions**:
- Normal load: 100 concurrent citizen searches
- Peak load: 10,000 concurrent citizen searches (media event / fuel crisis)
- Data volume: ~8,500 forecourts, ~25,000 price records (multiple fuel types per forecourt)

**Priority**: MUST_HAVE

**Relates To**: BR-003, Goal G-3

**Principle Alignment**: Principle 14 (Performance and Efficiency)

---

#### NFR-P-002: Data Synchronisation Throughput

**Requirement**: The data synchronisation pipeline MUST process:
- Full sync (all ~8,500 stations): completed within 30 minutes
- Incremental sync: completed within 5 minutes per cycle
- End-to-end latency: ≤ 20 minutes from VE3 API data refresh to availability in CMA service
- Respect VE3 API rate limits: ≤ 30 RPM, 1 concurrent request

**Measurement Method**: Pipeline metrics; data freshness SLI

**Priority**: MUST_HAVE

**Relates To**: BR-008, Goal G-2

**Principle Alignment**: Principle 3 (Scalability and Elasticity), Principle 9 (Data Quality and Timeliness)

---

#### NFR-P-003: Compliance Dashboard Performance

**Requirement**: CMA enforcement dashboard MUST:
- Load compliance overview within 5 seconds
- Filter and refresh results within 3 seconds
- Support 20 concurrent enforcement users
- Export up to 10,000 records to CSV within 30 seconds

**Priority**: SHOULD_HAVE

**Relates To**: BR-004, Goal G-4

---

### Availability and Resilience Requirements

#### NFR-A-001: Service Availability

**Requirement**: The CMA service MUST achieve:
- Citizen-facing service: 99.9% availability (≤ 43.8 minutes unplanned downtime per month)
- CMA enhanced open data API: 99.9% availability
- CMA enforcement dashboard: 99.5% availability (≤ 3.6 hours unplanned downtime per month)

**Note**: VE3 Global Fuel Finder API availability is governed by the DESNZ-VE3 contract and is outside CMA's SLA scope. CMA service must be resilient to VE3 API outages.

**Maintenance Windows**: Planned maintenance permitted Sundays 02:00–06:00 UTC with 7 days' notice

**Priority**: MUST_HAVE

**Relates To**: BR-003, Goal G-3

**Principle Alignment**: Principle 15 (Availability and Reliability)

---

#### NFR-A-002: Disaster Recovery

**RPO (Recovery Point Objective)**: Maximum 15 minutes of data loss for enriched data; zero data loss for audit trail and enforcement records

**RTO (Recovery Time Objective)**: Service restored within 4 hours of disaster declaration

**Backup Requirements**:
- Backup frequency: Continuous replication for operational database; hourly snapshots for analytics
- Backup retention: 30 days for operational backups; indefinite for audit trail archives
- Geographic backup location: Secondary UK availability zone (separate from primary)

**Failover Requirements**:
- Automatic failover to secondary availability zone: YES
- Failover time: < 15 minutes for automated failover

**Priority**: MUST_HAVE

---

#### NFR-A-003: Fault Tolerance and VE3 API Resilience

**Requirement**: The CMA service MUST gracefully degrade when components fail:
- If VE3 Fuel Finder API is unavailable: citizen service continues to serve last-known cached prices with staleness indicators; compliance monitoring pauses detection timers
- If data processing pipeline fails: citizen service continues to serve last-known prices with staleness indicators
- If citizen search is degraded: enforcement dashboard continues unaffected (bulkhead isolation)
- If GOV.UK Notify is unavailable: notifications are queued and retried; enforcement actions are not blocked

**Resilience Patterns Required**:
- [ ] Circuit breaker for all external dependencies (VE3 API, geocoding, Notify, address lookup)
- [ ] Retry with exponential backoff for VE3 API (max 3 retries, respect Retry-After header)
- [ ] Timeout on all network calls (default: 5 seconds; VE3 API: 20 seconds per developer guidance)
- [ ] Bulkhead isolation between data sync, citizen serving, and enforcement tiers
- [ ] Graceful degradation with staleness indicators when serving cached data

**Priority**: MUST_HAVE

**Relates To**: Principle 4 (Resilience and Fault Tolerance)

---

### Scalability Requirements

#### NFR-S-001: Horizontal Scaling

**Requirement**: All stateless components MUST support horizontal scaling without code changes

**Growth Projections**:
- Year 1: 8,500 forecourts, 1M monthly citizen users, 10 third-party API integrations
- Year 2: 9,000 forecourts (new builds), 3M monthly citizen users, 50 third-party integrations; in-car app integrations emerging
- Year 3: 10,000 forecourts (potentially including EV charging), 5M monthly users, 100+ third-party integrations; significant in-car usage driving API traffic

**Scaling Triggers**: Auto-scale based on CPU utilisation ( > 70%), request queue depth, and response latency

**Priority**: MUST_HAVE

**Relates To**: Principle 3 (Scalability and Elasticity)

---

#### NFR-S-002: Data Volume Scaling

**Requirement**: The CMA service MUST handle data growth for:
- Synced price data: ~150,000 records per day (Year 1) growing to ~300,000 per day (Year 3)
- Historical price data: ~55M records per year, retained indefinitely for public record and enforcement evidence
- Audit data: ~50M events per year, retained for 7+ years
- Compliance metrics: aggregated daily, retained indefinitely

**Data Archival Strategy**: Hot storage for current + 90 days; warm storage for 90 days to 2 years; cold archival beyond 2 years. All tiers queryable.

**Priority**: MUST_HAVE

---

### Security Requirements

#### NFR-SEC-001: Authentication

**Requirement**: All user access to CMA-built services MUST be authenticated:
- **CMA Staff**: Integrated with CMA corporate identity provider (SSO via SAML 2.0 or OIDC)
- **DESNZ Analysts**: Federated identity or delegated access via CMA IdP
- **Citizens (read-only)**: No authentication required for public data access
- **Third-Party API (read-only)**: No authentication required; rate limiting by IP
- **CMA Service to VE3 API**: OAuth 2.0 client credentials (client_id + client_secret + scope `fuelfinder.read`)

**Note**: Retailer authentication is handled by VE3 Global platform via GOV.UK One Login. CMA service does not authenticate retailers.

**Session Management**:
- Session timeout: 30 minutes of inactivity (CMA and DESNZ interfaces)
- Absolute session timeout: 8 hours
- Re-authentication required for: enforcement actions

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 6 (Security by Design)

---

#### NFR-SEC-002: Authorisation

**Requirement**: Role-based access control (RBAC) with least privilege for CMA-built services:

| Role | Permissions |
|------|------------|
| Citizen | Read published fuel prices via web or API (no authentication) |
| CMA Operations | View operational dashboards, data quality metrics |
| CMA Enforcement | All operations + compliance monitoring, enforcement actions, audit trail access |
| CMA Admin | All enforcement + user management, system configuration |
| DESNZ Analyst | Read published and aggregate data; export reports |
| System Service | Inter-service communication; data sync with VE3 API |

**Privilege Elevation**: Enforcement actions require MFA re-authentication; admin actions require approval workflow

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 6 (Security by Design)

---

#### NFR-SEC-003: Data Encryption

**Requirement**:
- Data in transit: TLS 1.2+ (prefer 1.3) for all communications including VE3 API calls
- Data at rest: AES-256 or equivalent for all data stores
- Key management: Managed key service within UK sovereign cloud

**Encryption Scope**:
- [ ] Database encryption at rest (all databases including PostGIS)
- [ ] Backup encryption (all backups)
- [ ] File storage encryption (all object storage)
- [ ] Audit trail integrity (cryptographic hashing for tamper evidence)
- [ ] VE3 API credentials encrypted at rest in secrets manager

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 6 (Security by Design)

---

#### NFR-SEC-004: Secrets Management

**Requirement**: No secrets stored in code, configuration files, or environment variables at rest

**Secrets Scope**:
- VE3 API OAuth 2.0 client credentials (client_id, client_secret)
- CMA IdP federation certificates
- Database connection credentials
- GOV.UK Notify API keys
- Address gazetteer API keys

**Secrets Management**: All secrets stored in a managed secrets service (AWS Secrets Manager or equivalent), injected at runtime

**Secrets Rotation**: Automatic rotation every 90 days for service credentials; VE3 API credentials rotated per VE3 guidance; immediate rotation if compromise suspected (per VE3 developer guidelines)

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

---

#### NFR-SEC-005: Vulnerability Management

**Requirement**:
- Dependency scanning in CI/CD pipeline: no critical or high vulnerabilities in production
- Static application security testing (SAST): every build
- Dynamic application security testing (DAST): weekly in staging, pre-release in production
- Penetration testing: annually by NCSC CHECK-approved provider; additionally before Live assessment

**Remediation SLA**:
- Critical vulnerabilities: 24 hours
- High vulnerabilities: 7 days
- Medium vulnerabilities: 30 days
- Low vulnerabilities: 90 days

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 6 (Security by Design)

---

### Compliance and Regulatory Requirements

#### NFR-C-001: UK GDPR and Data Protection Act 2018

**Applicable Regulations**: UK GDPR, Data Protection Act 2018

**Compliance Requirements**:
- [ ] DPIA completed (ARC-001-DPIA-v1.0 — complete)
- [ ] Lawful basis documented: public task under Article 6(1)(e)
- [ ] Privacy notices published at point of data collection
- [ ] Data subject rights processes operational (access, rectification, erasure where lawful)
- [ ] Data breach notification within 72 hours to ICO
- [ ] Data minimisation verified — CMA service stores only data necessary for its functions

**Data Residency**: All data MUST be stored and processed within UK sovereign territory

**Data Retention**:
- Published fuel price data (synced from VE3): Retained indefinitely as public record
- Historical price data: Retained indefinitely for trend analysis and enforcement evidence
- Enforcement records: 7 years minimum
- Audit logs: 7 years minimum
- Application logs: 90 days

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 8 (Data Sovereignty), Principle 21 (Privacy by Design), Goal G-6, Driver SD-10

---

#### NFR-C-002: Audit Logging

**Requirement**: Comprehensive, tamper-evident audit trail for CMA enforcement purposes

**Audit Log Contents** (for all enforcement actions, data sync events, and admin operations):
- **Who**: User/service identity (authenticated principal)
- **What**: Action performed (enforcement action, data export, compliance assessment, config change)
- **When**: Timestamp (UTC, millisecond precision)
- **Where**: System component, API endpoint, IP address
- **Why**: Context (enforcement case reference, sync batch ID)
- **Result**: Success/failure with error details

**Log Retention**: 7 years for enforcement-related audit logs (immutable storage)

**Log Integrity**: Tamper-evident logging — cryptographic chain hashing or append-only storage with integrity verification

**Priority**: MUST_HAVE

**Relates To**: Principle 20 (Regulatory Compliance by Design), FR-009

---

#### NFR-C-003: GDS Service Standard Compliance

**Requirement**: The CMA citizen-facing service MUST comply with all 14 points of the GDS Service Standard and pass assessment at Alpha, Beta, and Live phases

**Key Evidence Requirements**:
- Point 1: User research evidence with real motorists at each phase
- Point 2: Solve a whole problem for users (find cheapest fuel nearby)
- Point 3: Joined-up experience across channels
- Point 5: Make sure everyone can use the service (WCAG 2.2 AA)
- Point 6: Multidisciplinary team
- Point 9: Create a secure service (Secure by Design — ARC-001-SECD-v1.0)
- Point 10: Define success and publish performance data
- Point 12: Make new source code open
- Point 14: Operate a reliable service

**Priority**: MUST_HAVE

**Relates To**: Goal G-7, Driver SD-9

---

#### NFR-C-004: Technology Code of Practice (TCoP)

**Requirement**: All technology decisions MUST comply with the Technology Code of Practice (assessed in ARC-001-TCOP-v1.0)

**Priority**: MUST_HAVE

---

#### NFR-C-005: Secure by Design

**Requirement**: The service MUST complete an NCSC Secure by Design assessment before entering Beta phase (ARC-001-SECD-v1.0 — complete)

**Requirements**:
- [ ] Threat model completed for all components
- [ ] Security controls mapped to identified threats
- [ ] Penetration test conducted by CHECK-approved provider
- [ ] SIRO sign-off on residual risk
- [ ] Incident response plan documented and tested

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

---

### Usability Requirements

#### NFR-U-001: Citizen User Experience

**Requirement**: The citizen-facing service MUST use the GOV.UK Design System and be usable by citizens with low digital confidence

**UX Standards**:
- GOV.UK Design System components and patterns
- WCAG 2.2 Level AA compliance (legal requirement)
- Mobile-first responsive design
- Browser support: Chrome, Firefox, Safari, Edge — last 2 major versions
- Progressive enhancement: core functionality works without JavaScript

**Priority**: MUST_HAVE

**Relates To**: BR-003, Principle 2 (Citizen-Centred Design)

---

#### NFR-U-002: Accessibility

**Requirement**: WCAG 2.2 Level AA compliance (mandatory under Public Sector Bodies Accessibility Regulations 2018)

**Accessibility Features**:
- [ ] Keyboard navigation for all functions
- [ ] Screen reader compatibility (NVDA, JAWS, VoiceOver)
- [ ] Sufficient colour contrast ratios
- [ ] Text resizable to 200% without loss of content
- [ ] Alt text for all non-decorative images
- [ ] Map alternative: list view of results for screen reader users
- [ ] Skip links and landmark navigation
- [ ] Error messages associated with form fields

**Testing**: Automated accessibility testing (axe-core) in CI/CD + manual testing with assistive technologies before each phase gate

**Priority**: MUST_HAVE

---

#### NFR-U-003: Localisation

**Requirement**: The CMA service MUST support English. Welsh language support SHOULD be available for citizen-facing pages.

**Localisation Scope**:
- [ ] English (primary, mandatory)
- [ ] Welsh (citizen-facing pages, to comply with Welsh Language Act where applicable)
- [ ] Pence per litre formatting (UK convention — display to 1 decimal place; source data in 3 decimal places in GBP)
- [ ] UK date format (DD/MM/YYYY) in user interfaces
- [ ] ISO 8601 dates in API responses

**Priority**: English: MUST_HAVE; Welsh: SHOULD_HAVE

---

### Maintainability and Supportability Requirements

#### NFR-M-001: Observability

**Requirement**: Comprehensive instrumentation for monitoring, troubleshooting, and capacity planning

**Telemetry Requirements**:
- **Logging**: Structured JSON logs with correlation IDs, centralised aggregation
- **Metrics**: Request rate, error rate, duration (RED); data freshness SLI; sync success rate; compliance rates
- **Tracing**: Distributed tracing across data sync and serving components
- **Dashboards**: Real-time operational dashboards for: service health, VE3 API sync status, data freshness, citizen API usage, compliance rates
- **Alerts**: SLO-based alerting with runbooks; VE3 API sync failure alerts; data freshness breach alerts; security event alerts

**Business Metrics Dashboard**:
- Forecourt coverage rate (synced from VE3 data)
- Data freshness (median and p95 time since last price update per forecourt)
- Citizen usage (unique users, searches, satisfaction)
- Enhanced API consumer usage (requests, top consumers, geospatial query patterns)
- Compliance rate (% of forecourts with current data)

**Priority**: MUST_HAVE

**Relates To**: Principle 7 (Observability and Operational Excellence)

---

#### NFR-M-002: Documentation

**Requirement**: Comprehensive documentation for operators, developers, and third-party API consumers

**Documentation Types**:
- [ ] Architecture documentation (system context, component diagrams)
- [ ] Enhanced API documentation (OpenAPI 3.0 specification)
- [ ] Operational runbooks (deployment, rollback, incident response, DR, VE3 API sync failure)
- [ ] Developer onboarding guide
- [ ] Third-party API developer portal with in-car integration guidelines

**Documentation Currency**: Updated within 5 working days of code changes

**Priority**: MUST_HAVE

---

#### NFR-M-003: Operational Runbooks

**Requirement**: Runbooks for all common operational scenarios

**Runbook Coverage**:
- [ ] Deployment and rollback procedures
- [ ] VE3 API sync failure: diagnosis, manual recovery, cache management
- [ ] Citizen service degradation response
- [ ] Enhanced API incident management
- [ ] Security incident response
- [ ] Disaster recovery procedure
- [ ] Capacity scaling (manual and automated)
- [ ] Data quality issue investigation

**Priority**: MUST_HAVE

---

### Portability and Interoperability Requirements

#### NFR-I-001: API Standards

**Requirement**: All CMA-built APIs MUST follow open standards

**API Design Principles**:
- RESTful design with standard HTTP methods
- JSON request/response format (GeoJSON for spatial data)
- Versioning via URL path (/v1/, /v2/)
- OpenAPI 3.0 specification published for all APIs
- Consistent error response format (RFC 7807 Problem Details)
- Pagination for list endpoints (cursor-based preferred)
- Rate limiting with standard headers (X-RateLimit-*, Retry-After)

**Priority**: MUST_HAVE

**Relates To**: Principle 5 (Interoperability and Integration)

---

#### NFR-I-002: Open Standards and Open Source

**Requirement**: The CMA service MUST use open standards and make new source code open (GDS Service Standard Point 12; TCoP Point 3/4)

**Requirements**:
- Source code published in a public repository (unless security exemption applies)
- Open data published under Open Government Licence v3.0
- Open standards for data formats (JSON, GeoJSON, CSV)
- No vendor lock-in for data formats or storage
- Infrastructure defined as code using open-source tooling where practical

**Priority**: MUST_HAVE

---

#### NFR-I-003: Data Portability

**Requirement**: Fuel price data MUST be exportable in open formats

**Export Formats**: CSV, JSON, GeoJSON (for location-aware consumers)

**Export Scope**: Complete dataset (bulk download), filtered by date range, region, fuel type

**Priority**: MUST_HAVE

---

---

## Integration Requirements

### External System Integrations

#### INT-001: Fuel Finder Public API (VE3 Global) **[CRITICAL]**

**Purpose**: Primary data source — synchronise all fuel price and station data from the statutory Fuel Finder platform operated by VE3 Global under DESNZ contract

**Integration Type**: Scheduled REST API polling (every 15 minutes incremental; daily full sync)

**API Details** (from developer.fuel-finder.service.gov.uk):

| Aspect | Detail |
|--------|--------|
| Base URL | `https://api.fuelfinder.service.gov.uk/v1/` |
| Authentication | OAuth 2.0 client credentials grant via VE3 OAuth endpoint |
| Credential Lifetime | 3600 seconds (Bearer) |
| Rate Limit | 30 RPM per client, 1 concurrent request |
| Environments | Test (sandbox) + Production with separate credentials |

**Endpoints Consumed**:

| Endpoint | Purpose | Frequency |
|----------|---------|-----------|
| `GET /api/v1/pfs` | Station metadata (address, brand, amenities, hours) | Every 1 hour |
| `GET /api/v1/pfs/fuel-prices` | Current prices by fuel type with timestamps | Every 15 minutes |

**Data Exchanged**:
- **From VE3 API to CMA Service**: Station metadata (node_id `GB-NNNNN`, trading_name, brand_name, location, fuel_types, amenities, opening_times); Price data (price in GBP to 3 decimal places, fuel_type [E10/E5/B7/SDV], price_last_updated, price_change_effective_timestamp)
- **Pagination**: Batch-number parameter (up to 80 batches)
- **Incremental Sync**: `effective-start-timestamp` parameter for delta updates

**Error Handling**: Circuit breaker; exponential backoff on 429/5xx; serve cached data during outages; alert operations if unavailable > 1 hour

**SLA**: CMA service must tolerate VE3 API outages of up to 4 hours without citizen-facing degradation (serve cached data)

**Owner**: VE3 Global / DESNZ (API provider); CMA Digital (integration consumer)

**Priority**: MUST_HAVE (CRITICAL — entire service depends on this integration)

---

#### INT-002: Geocoding Service (OS Places API)

**Purpose**: Convert postcodes and place names to coordinates for citizen proximity search

**Integration Type**: Real-time API (on citizen search request)

**Authentication**: PSGA (Public Sector Geospatial Agreement) — free for central government

**Data Exchanged**:
- **From CMA Service**: Postcode, place name, or address
- **From OS Places API**: Latitude, longitude, formatted address, UPRN

**Rate Limits**: 50 RPM (development), 600 RPM (production) per VE3 developer guidance

**Error Handling**: Circuit breaker; fallback to cached postcode-to-coordinate lookup table

**SLA**: < 500ms response time; 99.9% availability

**Priority**: MUST_HAVE

---

#### INT-003: GOV.UK Notify

**Purpose**: Send emails and SMS for compliance reminders, enforcement notices, and operational alerts

**Integration Type**: REST API

**Authentication**: API key (GOV.UK Notify standard)

**Error Handling**: Retry with exponential backoff; dead letter queue for persistently failed notifications

**Priority**: MUST_HAVE

---

#### INT-004: GOV.UK Design System and Frontend

**Purpose**: Citizen-facing service using GOV.UK Design System for consistent, accessible UI

**Integration Type**: Frontend framework integration

**Priority**: MUST_HAVE

---

#### INT-005: GOV.UK One Login (Future Consideration)

**Purpose**: Citizen identity verification if future features require authenticated citizen access (e.g., saved preferences, price alerts)

**Note**: VE3 Global platform already uses GOV.UK One Login for retailer authentication. CMA citizen service does not currently require authentication. Included for architectural awareness.

**Priority**: COULD_HAVE (future phase)

---

#### INT-006: CMA Corporate Identity Provider

**Purpose**: Single sign-on for CMA staff accessing enforcement dashboard and administration tools

**Integration Type**: SAML 2.0 or OIDC federation with CMA identity provider

**Data Exchanged**:
- **From CMA IdP to CMA Service**: Authenticated identity, role claims, group membership
- **From CMA Service to CMA IdP**: Authentication request, logout

**Priority**: MUST_HAVE

---

#### INT-007: Companies House API

**Purpose**: Cross-reference retailer organisation details for enforcement investigations (company status, registered address)

**Integration Type**: Real-time API (on-demand during enforcement investigation)

**Rate Limits**: Strict limits — use cached or mocked responses to avoid quota exhaustion (per VE3 developer guidance)

**Priority**: SHOULD_HAVE

---

#### INT-008: Android Auto and Apple CarPlay Platform Compatibility

**Purpose**: Ensure the CMA enhanced API is compatible with in-car platform requirements

**Integration Pattern**: CMA service provides the API; third-party apps implement platform SDKs. CMA publishes guidelines per FR-014.

**Priority**: SHOULD_HAVE

---

---

## Data Requirements

### Data Entities

#### Entity 1: Forecourt (synced from VE3 API)

**Description**: A physical fuel retail location synced from the Fuel Finder Public API

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| forecourt_id | String(8) | Yes | VE3 node_id (e.g., `GB-12345`) | Primary key |
| trading_name | String(255) | Yes | Forecourt display name | From VE3 API |
| brand_name | String(255) | No | Brand (Shell, BP, etc.) | From VE3 API |
| address | JSON | Yes | Location object from VE3 | Structured JSON |
| latitude | Decimal(10,7) | Yes | WGS84 latitude | Range: 49.0–61.0 |
| longitude | Decimal(10,7) | Yes | WGS84 longitude | Range: -8.0–2.0 |
| geom | Geometry(Point, 4326) | Yes | PostGIS point for spatial queries | Indexed (GiST) |
| fuel_types | Array[Enum] | Yes | Fuel types sold | [E10, E5, B7, SDV] |
| amenities | Array[String] | No | Forecourt amenities | From VE3 API |
| opening_times | JSON | No | Operating hours | From VE3 API |
| last_synced_at | Timestamp | Yes | When last synced from VE3 | Indexed |
| created_at | Timestamp | Yes | Record creation in CMA database | Indexed |
| updated_at | Timestamp | Yes | Last update | Indexed |

**Relationships**: One-to-many with CurrentPrice; One-to-many with PriceHistory

**Data Volume**: ~8,500 forecourts (Year 1), ~10,000 (Year 3)

**Access Patterns**: Geographic queries (PostGIS ST_DWithin); forecourt_id lookup; brand filtering

**Data Classification**: OFFICIAL — PUBLIC (published as open data)

**Data Retention**: Indefinite (public record)

---

#### Entity 2: CurrentPrice

**Description**: The current published fuel price for a forecourt, synced from VE3 API and enriched with quality scoring

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| forecourt_id | String(8) | Yes | VE3 node_id | FK, composite PK |
| fuel_type | Enum | Yes | Fuel type code | [E10, E5, B7, SDV], composite PK |
| price_gbp | Decimal(6,3) | Yes | Price in GBP per litre (3dp) | From VE3 API |
| price_ppl | Decimal(5,1) | Yes | Price in pence per litre (1dp) | Computed: price_gbp x 100 |
| price_last_updated | Timestamp | Yes | When price was last changed at forecourt | From VE3 API |
| price_change_effective | Timestamp | No | When price change took effect | From VE3 API |
| synced_at | Timestamp | Yes | When synced from VE3 API | Indexed |
| data_quality | Enum | Yes | Quality indicator | [good, stale, warning, anomaly] |
| anomaly_flag | Boolean | No | Price anomaly detected | Default false |

**Access Patterns**: Geographic proximity query (via Forecourt.geom + JOIN); bulk export; freshness monitoring

**Data Classification**: OFFICIAL — PUBLIC

**Data Retention**: Current record replaced on each sync; historical data in PriceHistory

---

#### Entity 3: PriceHistory

**Description**: Append-only historical record of all fuel prices observed from the VE3 API

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| id | BIGSERIAL | Yes | Auto-increment ID | Primary key |
| forecourt_id | String(8) | Yes | VE3 node_id | Indexed |
| fuel_type | Enum | Yes | Fuel type code | [E10, E5, B7, SDV] |
| price_gbp | Decimal(6,3) | Yes | Price in GBP per litre | |
| price_last_updated | Timestamp | Yes | When price changed (from VE3) | Indexed |
| observed_at | Timestamp | Yes | When CMA service observed this price | Indexed |

**Data Volume**: ~55M records per year

**Access Patterns**: By forecourt + date range; aggregate queries (avg price by region/fuel type/period)

**Data Classification**: OFFICIAL — PUBLIC

**Data Retention**: Indefinite (public record, partitioned by month)

---

#### Entity 4: ComplianceRecord

**Description**: CMA-computed compliance status for each forecourt, derived from price submission patterns observed via the API

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| forecourt_id | String(8) | Yes | VE3 node_id | Primary key |
| compliance_status | Enum | Yes | Current compliance state | [compliant, non_reporting, stale, technical_failure, under_investigation] |
| last_price_observed | Timestamp | No | When last price update was detected | |
| non_reporting_since | Timestamp | No | When non-reporting status began | |
| technical_failure_reported | Boolean | No | Retailer reported tech failure | Default false |
| failure_report_date | Timestamp | No | When failure was reported | |
| updated_at | Timestamp | Yes | Last compliance assessment | Indexed |

**Data Classification**: OFFICIAL

**Data Retention**: Duration of forecourt registration + 7 years

---

#### Entity 5: EnforcementAction

**Description**: A CMA enforcement action against a non-compliant retailer

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| action_id | UUID | Yes | Unique identifier | Primary key |
| forecourt_id | String(8) | Yes | Target forecourt | FK |
| action_type | Enum | Yes | Type of action | [reminder, warning, formal_notice, penalty] |
| initiated_by | UUID | Yes | CMA officer | FK to CMA user |
| initiated_at | Timestamp | Yes | When action initiated | Indexed |
| reason | Text | Yes | Reason for action | Not null |
| evidence_summary | JSON | Yes | Compliance timeline snapshot | |
| status | Enum | Yes | Action status | [pending, sent, acknowledged, resolved, escalated] |
| notification_id | UUID | No | GOV.UK Notify reference | |
| resolved_at | Timestamp | No | When resolved | |
| notes | Text | No | Officer notes | |

**Data Classification**: OFFICIAL — SENSITIVE

**Data Retention**: 7 years minimum (CMA legal requirements)

---

#### Entity 6: AuditEvent

**Description**: Immutable record of significant system events for compliance and forensics

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| event_id | UUID | Yes | Unique identifier | Primary key |
| event_type | Enum | Yes | Type of event | [enforcement_action, data_export, config_change, sync_event, login, compliance_assessment] |
| actor_id | UUID | Yes | Who performed the action | Indexed |
| actor_type | Enum | Yes | Type of actor | [cma_staff, desnz_staff, system] |
| timestamp | Timestamp | Yes | When it occurred (UTC, ms) | Indexed, not null |
| resource_type | String(100) | Yes | What was affected | |
| resource_id | String(100) | Yes | Specific resource | Indexed |
| action | String(100) | Yes | What was done | |
| result | Enum | Yes | Outcome | [success, failure, warning] |
| details | JSON | No | Additional context | |
| source_ip | String(45) | No | Source IP address | |
| integrity_hash | String(64) | Yes | SHA-256 chain hash | Tamper evidence |

**Data Classification**: OFFICIAL — SENSITIVE

**Data Retention**: 7 years (immutable, append-only storage)

---

#### Entity 7: ApiSyncState

**Description**: Tracks the state of data synchronisation from the VE3 Fuel Finder API

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| sync_id | UUID | Yes | Unique sync batch ID | Primary key |
| sync_type | Enum | Yes | Type of sync | [full, incremental] |
| started_at | Timestamp | Yes | When sync started | Indexed |
| completed_at | Timestamp | No | When sync completed | |
| status | Enum | Yes | Sync status | [running, completed, failed, partial] |
| records_processed | Integer | No | Number of records processed | |
| records_updated | Integer | No | Number of records with changes | |
| errors | JSON | No | Error details if any | |
| last_effective_timestamp | Timestamp | No | Timestamp used for next incremental sync | |

**Data Classification**: OFFICIAL

**Data Retention**: 90 days (operational data)

---

### Data Quality Requirements

**Data Accuracy**: Fuel prices validated against plausible range (50.0–500.0 PPL). Prices from VE3 API are in GBP to 3 decimal places; CMA converts to PPL for display. Anomaly detection for > 20% price change within 24 hours.

**Data Completeness**: All fuel types listed for a forecourt in VE3 API should have current prices. Missing fuel type prices generate staleness warning.

**Data Consistency**: Forecourt must exist in synced data for compliance monitoring. Cross-reference VE3 station data with OS Places data for address validation.

**Data Timeliness**: CMA service freshness target: ≤ 20 minutes from VE3 API data refresh to availability in citizen search. Stale threshold: > 24 hours since last price update triggers staleness indicator in citizen-facing results and non-reporting flag in compliance dashboard.

**Data Lineage**: Every published price traces to a specific VE3 API sync batch (via ApiSyncState), which traces to VE3 API response timestamps.

---

### Data Migration Requirements

**Migration Scope**: No legacy system migration required — new service consuming existing VE3 API. Initial data load required for:
- Full station and price sync from VE3 Fuel Finder API (bootstrap)
- Geographic reference data: OS postcode-to-coordinate mapping for search fallback

**Migration Strategy**: Full API sync on first deployment; incremental from then on.

---

## Constraints and Assumptions

### Technical Constraints

**TC-1**: All CMA data MUST be stored and processed within UK sovereign cloud regions (Principle 8: Data Sovereignty)

**TC-2**: The citizen-facing service MUST be hosted on GOV.UK infrastructure or integrate with the GOV.UK domain

**TC-3**: All citizen-facing pages MUST use the GOV.UK Design System

**TC-4**: The CMA service MUST operate at OFFICIAL classification

**TC-5**: Source code MUST be open source unless a specific security exemption is granted (GDS Service Standard Point 12)

**TC-6**: CMA service is dependent on VE3 Global Fuel Finder API for all fuel price data — no alternative statutory data source exists

**TC-7**: VE3 API rate limit of 30 RPM per client constrains sync frequency and must be respected

---

### Business Constraints

**BC-1**: Forecourt registration deadline was 2 February 2026 — **PASSED**

**BC-2**: CMA enforcement grace period ends early May 2026 — enforcement tools must be operational by this date

**BC-3**: Programme budget: £3.6M over 3 years (ROM ±30%) per SOBC (ARC-001-SOBC-v1.0)

**BC-4**: The service must pass GDS Service Standard assessment at each phase gate before progressing

**BC-5**: Cross-departmental governance: CMA delivers the digital service; DESNZ owns the policy, regulations, and VE3 Global platform contract

**BC-6**: VE3 Global API specification and availability are governed by the DESNZ-VE3 contract, outside CMA's direct control

---

### Assumptions

**A-1**: VE3 Global Fuel Finder API remains available and performant throughout CMA service operation — **VALIDATED** (API is live as of Q1 2026)

**A-2**: GOV.UK Notify has sufficient capacity for enforcement notification volumes (~10,000 emails/month steady state)

**A-3**: VE3 API rate limits (30 RPM) are sufficient for CMA's sync requirements — validated through sync design analysis

**A-4**: VE3 API data format and endpoints remain stable; versioned at `/v1/` with deprecation policy

**A-5**: The Motor Fuel Price (Open Data) Regulations 2025 (SI 2025/1356) will not be significantly amended during initial delivery

**A-6**: CMA and DESNZ will maintain joint governance arrangements; DESNZ manages VE3 Global contract on behalf of both organisations

**A-7**: PostGIS geospatial queries can serve citizen search at required latency ( < 500ms for proximity query across 8,500 forecourts) — to be validated in Alpha

**Validation Plan**: A-3 and A-7 to be validated during Alpha through load testing and performance benchmarking.

---

## Success Criteria and KPIs

### Business Success Metrics

| Metric | Baseline | Target | Timeline | Measurement Method |
|--------|----------|--------|----------|-------------------|
| Forecourt data coverage | 0 | ≥ 95% of known forecourts with current data | 12 months post-launch | CMA compliance dashboard |
| Monthly unique citizen users | 0 | 1,000,000 | 12 months post-launch | GOV.UK analytics |
| User satisfaction | N/A | ≥ 80% | Public Beta onwards | GOV.UK satisfaction survey |
| Third-party enhanced API integrations | 0 | ≥ 10 | 12 months post-API launch | API consumer metrics |
| Programme spend vs budget | £3.6M (ROM) | Within ±10% | Ongoing | Financial reporting |

### Technical Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Citizen search availability | 99.9% | Uptime monitoring |
| Enhanced API availability | 99.9% | Uptime monitoring |
| Citizen search response time (p95) | < 3 seconds | RUM / synthetic monitoring |
| Enhanced API response time (p95) | < 500ms | APM tooling |
| VE3 API sync freshness (p95) | ≤ 20 minutes | Pipeline metrics |
| Error rate (citizen search) | < 0.1% | Log aggregation |
| Non-compliance detection time | < 24 hours | Compliance monitoring |
| Deployment frequency | ≥ Weekly | CI/CD metrics |
| Mean time to recovery (MTTR) | < 1 hour | Incident tracking |

### User Adoption Metrics

| Metric | Target | Timeline | Measurement Method |
|--------|--------|----------|-------------------|
| Citizen monthly active users | 1,000,000 | 12 months | GOV.UK analytics |
| Task completion rate (find fuel price) | ≥ 95% | Public Beta | User research |
| Accessibility audit pass | WCAG 2.2 AA | Each phase gate | Automated + manual audit |
| GDS Service Standard assessment | Pass | Each phase gate | GDS assessment panel |

---

## Dependencies and Risks

### Dependencies

| Dependency | Description | Owner | Target Date | Status | Impact if Delayed |
|------------|-------------|-------|-------------|--------|-------------------|
| VE3 Fuel Finder API | Production API availability and stability | VE3 Global / DESNZ | Live (achieved) | **Available** | CRITICAL — no data source |
| VE3 API documentation | Complete endpoint documentation and test environment | VE3 Global / DESNZ | Live (achieved) | **Available** | HIGH — integration delay |
| OS Places API access | PSGA licence for geocoding | CMA Procurement | Q2 2026 | On Track | HIGH — address resolution degraded |
| GOV.UK Notify capacity | Confirm Notify handles enforcement notification volumes | GDS Notify team | Q2 2026 | On Track | MEDIUM — alternative notification needed |
| CMA Identity Provider | SAML/OIDC federation for CMA staff SSO | CMA IT | Q2 2026 | On Track | MEDIUM — fallback to standalone auth |
| CMA Legal guidance | Evidence admissibility requirements for enforcement records | CMA Legal | Q2 2026 | On Track | HIGH — audit trail design affected |
| AWS cloud account | UK sovereign region setup with security controls | CMA IT / CDDO | Q2 2026 | On Track | HIGH — no deployment target |

### Risks

| Risk ID | Description | Probability | Impact | Mitigation Strategy | Owner |
|---------|-------------|-------------|--------|---------------------|-------|
| R-1 | VE3 Global API unavailability or degradation | MEDIUM | CRITICAL | Circuit breaker, cached data serving, SLA monitoring, escalation to DESNZ | CMA Digital Lead |
| R-2 | VE3 API rate limits insufficient for CMA sync needs | LOW | HIGH | Incremental sync design, negotiate higher limits via DESNZ, local caching | CMA Digital Lead |
| R-3 | Data quality from VE3 API insufficient for citizen trust | MEDIUM | HIGH | Client-side validation, anomaly detection, staleness indicators, quality scoring | CMA Digital Lead |
| R-4 | Enforcement tools not ready by May 2026 grace period end | MEDIUM | HIGH | Prioritise enforcement features in Sprint 1; MVP compliance dashboard first | CMA Digital Lead |
| R-5 | Low independent retailer compliance on VE3 platform | HIGH | HIGH | PRA partnership, assisted digital (VE3/DESNZ responsibility), CMA enforcement tools | CMA Enforcement Lead |
| R-6 | GDS Service Standard assessment failure | MEDIUM | HIGH | Pre-assessment check-ins, user research investment | CMA Digital Lead |
| R-7 | Political pressure compromises governance | MEDIUM | HIGH | Clear phase gates, ministerial briefing on governance value | CMA SRO |
| R-8 | Security incident or data breach | LOW | CRITICAL | Secure by Design, pen testing, incident response plan, SIRO review | SIRO |

---

## Requirement Conflicts & Resolutions

### Conflict C-1: Delivery Speed vs Governance Rigour

**Conflicting Requirements**:
- **BR-004**: Enforcement tools operational by May 2026 (fixed regulatory deadline)
- **BR-007 / NFR-C-003**: Must pass GDS Service Standard assessment at each phase gate

**Stakeholders Involved**:
- **DESNZ Ministers (SD-4)**: Want rapid, visible delivery
- **GDS Assessors (SD-9)**: Require thorough user research and phased delivery evidence

**Nature of Conflict**: Compressed delivery timelines may not allow sufficient user research cycles for GDS assessment.

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Prioritize speed | Meet May deadline | Risk GDS failure | Ministers satisfied short-term |
| **Option 2**: Prioritize governance | Strong evidence | Miss enforcement deadline | GDS satisfied; ministers frustrated |
| **Option 3**: Compress phases, front-load research | Balance both | Team intensity | Both partially satisfied |

**Resolution Strategy**: COMPROMISE (Option 3)

**Decision**: Compress delivery phases but invest heavily in user research from day one. MVP enforcement dashboard operational by May 2026; full capability iterates post-Beta.

**Decision Authority**: CMA SRO

---

### Conflict C-2: Enforcement Rigour vs Retailer Support

**Conflicting Requirements**:
- **FR-005**: Compliance dashboard with automated non-compliance detection ( < 24h)
- **FR-011**: Technical failure reporting mechanism

**Stakeholders Involved**:
- **CMA Enforcement (SD-2)**: Needs effective detection and evidence
- **Independent Retailers (SD-7) / Trade Bodies (SD-8)**: Want supportive, proportionate approach

**Nature of Conflict**: Aggressive automated enforcement could penalise retailers experiencing genuine technical difficulties.

**Resolution Strategy**: PHASE

**Decision**: Build both automated detection (FR-005) and self-service failure reporting (FR-011). During grace period: support focus. After grace period: proportionate escalation (reminders to warnings to penalties). Technical failures excluded from non-compliance counts.

**Decision Authority**: CMA Enforcement Lead

---

### Conflict C-3: Data Granularity vs Retailer Commercial Sensitivity

**Conflicting Requirements**:
- **BR-005 / FR-004**: Publish comprehensive real-time fuel price data as open data
- **Implicit retailer concern**: Competitors can see pricing strategy in real time

**Resolution Strategy**: PRIORITIZE (regulatory requirement takes precedence)

**Decision**: Publish data as required by the Motor Fuel Price (Open Data) Regulations 2025. Prices are already publicly visible on forecourt price boards; digital publication does not reveal new information. Data published under OGL v3.0 per VE3 API terms.

**Decision Authority**: DESNZ Policy Lead

---

### Conflict C-4: Driver Safety vs Feature Richness (In-Car)

**Conflicting Requirements**:
- **FR-013**: Provide optimised in-car API responses
- **NFR-U-001**: GOV.UK Design System for citizen-facing service

**Resolution Strategy**: PHASE

**Decision**: Phase 1 — rely on third-party apps consuming the CMA enhanced API (no GOV.UK Design System conflict). Phase 2 (future) — official companion app follows platform-specific guidelines.

**Decision Authority**: CMA Digital Lead

---

### Conflict C-5: VE3 API Dependency vs Service Resilience

**Conflicting Requirements**:
- **BR-008**: Synchronise data from VE3 API (creates external dependency)
- **NFR-A-001**: 99.9% availability for citizen-facing service

**Stakeholders Involved**:
- **CMA Digital (technology)**: Need resilient architecture despite external dependency
- **DESNZ (contract owner)**: VE3 API SLA governed by separate contract

**Nature of Conflict**: CMA service availability depends on an API managed by a third party (VE3 Global) under a contract CMA does not control. VE3 API outages could cascade to citizen-facing degradation.

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Real-time passthrough | Always fresh data | Cascading failures | Citizens affected by every VE3 outage |
| **Option 2**: Local cache with staleness tolerance | Resilient to outages | May serve stale data | Citizens get data even during VE3 outages |
| **Option 3**: Multi-source fallback | Maximum resilience | Complex; multiple integrations | Expensive to maintain |

**Resolution Strategy**: COMPROMISE (Option 2)

**Decision**: Maintain a locally cached and enriched copy (PostGIS database). Sync every 15 minutes. During VE3 outages, serve cached data with staleness indicators. Alert operations if VE3 unavailable > 1 hour. CMA requests DESNZ include minimum API SLA in VE3 contract.

**Decision Authority**: CMA Digital Lead

**Impact on Requirements**: FR-001 designed with resilience; NFR-A-003 explicitly addresses VE3 outages.

---

## Timeline and Milestones

### High-Level Milestones

| Milestone | Description | Target Date | Dependencies | Status |
|-----------|-------------|-------------|--------------|--------|
| Requirements v3.0 Approval | Stakeholder sign-off on this document | 2026-04-18 | This document | IN PROGRESS |
| Forecourt Registration Deadline | Statutory deadline — all forecourts registered | 2026-02-02 | VE3 Global platform | **COMPLETE** |
| Enforcement Grace Period End | CMA may begin formal enforcement | Early May 2026 | Enforcement tools operational (FR-005, FR-007) | AT RISK |
| Alpha Assessment | GDS Service Standard Alpha assessment | 2026-Q2 | User research, prototype | ON TRACK |
| Private Beta | Service available to limited users | 2026-Q3 | Alpha assessment pass | ON TRACK |
| Public Beta | Service available to all citizens | 2026-Q3/Q4 | Private Beta assessment pass | ON TRACK |
| Live Assessment | GDS Service Standard Live assessment | 2027-Q1 | Public Beta stable, all metrics met | PLANNED |
| First Annual Review | Benefits realisation, NAO readiness | 2027-Q2 | 12 months of live data | PLANNED |

---

## Budget

Budget figures are derived from the Strategic Outline Business Case (ARC-001-SOBC-v1.0). All figures are Rough Order of Magnitude (ROM ±30%) in 2026 prices, excluding VAT.

### Capital Expenditure (Year 1 Delivery)

| Category | Estimated Cost | Notes |
|----------|----------------|-------|
| Delivery Team (multidisciplinary, 12 months) | £1.20M | 10-person team |
| Cloud Infrastructure Setup (AWS eu-west-2) | £0.10M | UK sovereign cloud |
| Third-party Licences (initial) | £0.05M | OS Places API under PSGA (free); PostGIS (open source) |
| Security Testing (pen test + accessibility audit) | £0.08M | CHECK-approved provider |
| GOV.UK Platforms (Notify, Design System) | Included | Government shared platforms (integration effort only) |
| Contingency (15%) | £0.21M | VE3 API integration complexity, scope clarification |
| **Total CapEx** | **£1.64M** | |

### Ongoing Operational Costs (from Year 2)

| Category | Annual Cost | Notes |
|----------|-------------|-------|
| Cloud Hosting (AWS) | £0.15M | Auto-scaling; pay-per-use; PostGIS on RDS |
| Support Team (2nd/3rd line, 3 FTE) | £0.25M | On-call included |
| Third-party Licences (annual) | £0.03M | Monitoring tools, security scanning |
| Security Testing (annual) | £0.03M | Annual pen test and re-audit |
| Platform Maintenance | £0.10M | Patching, updates, VE3 API version updates |
| **Total OpEx** | **~£0.56M/year** | |

### 3-Year Total Cost of Ownership

| | Year 1 | Year 2 | Year 3 | 3-Year Total |
|---|--------|--------|--------|--------------|
| CapEx | £1.64M | — | — | £1.64M |
| OpEx | £0.06M | £0.56M | £0.58M | £1.20M |
| **Total** | **£1.70M** | **£0.56M** | **£0.58M** | **£2.84M** |

*With HM Treasury optimism bias (+20%): £3.41M. See ARC-001-SOBC-v1.0 for full breakdown.*

---

## Approval

### Requirements Review

| Reviewer | Role | Status | Date | Comments |
|----------|------|--------|------|----------|
| [CMA SRO] | Programme SRO | [ ] Approved | | |
| [CMA Digital Lead] | Product/Technology Lead | [ ] Approved | | |
| [CMA Enforcement Lead] | Enforcement Requirements | [ ] Approved | | |
| [DESNZ Policy Lead] | Policy/Regulatory | [ ] Approved | | |
| [Enterprise Architect] | Architecture Alignment | [ ] Approved | | |
| [SIRO] | Security/Information Risk | [ ] Approved | | |
| [DPO] | Data Protection | [ ] Approved | | |

### Sign-Off

By signing below, stakeholders confirm that requirements are complete, understood, and approved to proceed to design phase.

| Stakeholder | Signature | Date |
|-------------|-----------|------|
| CMA SRO | _________ | |
| DESNZ Policy Lead | _________ | |
| Enterprise Architect | _________ | |

---

## Appendices

### Appendix A: Glossary

| Term | Definition |
|------|-----------|
| Android Auto | Google's in-car platform that projects compatible smartphone apps onto a vehicle's head unit display |
| Apple CarPlay | Apple's in-car platform that integrates iPhone apps with a vehicle's built-in display |
| B7 | Standard diesel fuel type (7% biodiesel) — VE3 API code |
| CMA | Competition and Markets Authority — UK competition regulator and Fuel Finder enforcement body |
| DESNZ | Department for Energy Security and Net Zero — policy owner for fuel market regulation |
| E10 | Standard unleaded petrol (10% ethanol) — VE3 API code |
| E5 | Super unleaded petrol (5% ethanol) — VE3 API code |
| Forecourt | A physical fuel retail location (petrol station / filling station) |
| GDS | Government Digital Service — service assessment and standards body |
| GeoJSON | Open standard format for encoding geographic data structures in JSON |
| Motor Fuel Trader (MFT) | A business operating one or more forecourts that sells motor fuel to the public |
| OGL | Open Government Licence — standard UK Government open data licence |
| PostGIS | Open-source geospatial extension for PostgreSQL database |
| PPL | Pence per litre — standard UK unit for fuel pricing display |
| PSGA | Public Sector Geospatial Agreement — provides free access to OS data for UK government |
| SDV | Premium diesel (super diesel variant) — VE3 API code |
| TCoP | Technology Code of Practice — mandatory for UK Government technology |
| UPRN | Unique Property Reference Number — OS address identifier |
| VE3 Global | Technology company operating the Fuel Finder API platform under DESNZ contract |
| WCAG | Web Content Accessibility Guidelines |

### Appendix B: Reference Documents

- ARC-000-PRIN-v1.0 — Enterprise Architecture Principles
- ARC-001-STKE-v1.0 — Stakeholder Drivers & Goals Analysis
- ARC-001-RISK-v1.0 — Risk Register
- ARC-001-SOBC-v1.0 — Strategic Outline Business Case
- ARC-001-DPIA-v1.0 — Data Protection Impact Assessment
- ARC-001-SECD-v1.0 — Secure by Design Assessment
- ARC-001-TCOP-v1.0 — Technology Code of Practice Review
- ARC-001-RSCH-v4.1 — Technology and Service Research (includes Fuel Finder API specification)
- Motor Fuel Price (Open Data) Regulations 2025 (SI 2025/1356)
- CMA Fuel Finder Enforcement Guidance (December 2025)
- GDS Service Standard (14 points)
- Technology Code of Practice (TCoP)
- VE3 Global Fuel Finder Developer Portal (developer.fuel-finder.service.gov.uk)

### Appendix C: Requirements Traceability Matrix

| Req ID | Requirement | Delivery | Stakeholder Goal | Principle | Priority |
|--------|-------------|----------|-----------------|-----------|----------|
| BR-001 | Universal registration | VE3 | G-1 | P2, P13 | MUST |
| BR-002 | Data submission compliance | VE3 | G-2 | P1, P9 | MUST |
| BR-003 | Citizen price comparison | CMA | G-3 | P2, P14 | MUST |
| BR-004 | CMA enforcement capability | CMA | G-4 | P20, P7 | MUST |
| BR-005 | Enhanced open data | CMA | O-2 | P1, P5 | MUST |
| BR-006 | Value for money | CMA | G-5 | P22 | MUST |
| BR-007 | Governance compliance | CMA | G-7 | P6, P8, P13, P20, P21 | MUST |
| BR-008 | Data sync and enrichment | CMA | G-2, G-3, G-4 | P4, P9 | MUST |
| FR-001 | API data synchronisation | CMA | G-2, G-3 | P5, P9 | MUST |
| FR-002 | Geospatial price search | CMA | G-3 | P2, P14 | MUST |
| FR-003 | Citizen search interface | CMA | G-3 | P2 | MUST |
| FR-004 | Enhanced open data API | CMA | O-2 | P1, P5 | MUST |
| FR-005 | Compliance dashboard | CMA | G-4 | P20, P7 | MUST |
| FR-006 | Data validation and quality | CMA | G-2 | P9 | MUST |
| FR-007 | Enforcement case mgmt | CMA | G-4 | P20 | MUST |
| FR-008 | Retailer notifications | CMA | G-2, G-4 | P13 | SHOULD |
| FR-009 | Audit trail | CMA | G-4 | P20 | MUST |
| FR-010 | Policy analysis | CMA | G-5 | P7 | SHOULD |
| FR-011 | Technical failure reporting | CMA | G-2, G-4 | P20 | MUST |
| FR-012 | Feedback and support | CMA | G-3 | P2 | SHOULD |
| FR-013 | In-car API responses | CMA | G-3 | P5, P14 | SHOULD |
| FR-014 | In-car dev guidelines | CMA | O-2 | P1, P5 | SHOULD |
| FR-015 | Historical price storage | CMA | G-2, G-4 | P9 | MUST |
| NFR-P-001 | Citizen search performance | CMA | G-3 | P14 | MUST |
| NFR-P-002 | Sync throughput | CMA | G-2 | P3, P9 | MUST |
| NFR-P-003 | Dashboard performance | CMA | G-4 | P14 | SHOULD |
| NFR-A-001 | Service availability | CMA | G-2, G-3 | P15 | MUST |
| NFR-A-002 | Disaster recovery | CMA | G-2 | P4, P15 | MUST |
| NFR-A-003 | Fault tolerance + VE3 resilience | CMA | G-2, G-3 | P4 | MUST |
| NFR-S-001 | Horizontal scaling | CMA | G-3 | P3 | MUST |
| NFR-S-002 | Data volume scaling | CMA | G-2 | P3 | MUST |
| NFR-SEC-001 | Authentication | CMA | G-7 | P6 | MUST |
| NFR-SEC-002 | Authorisation | CMA | G-7 | P6 | MUST |
| NFR-SEC-003 | Encryption | CMA | G-7 | P6 | MUST |
| NFR-SEC-004 | Secrets management | CMA | G-7 | P6 | MUST |
| NFR-SEC-005 | Vulnerability management | CMA | G-7 | P6 | MUST |
| NFR-C-001 | UK GDPR compliance | CMA | G-6 | P8, P21 | MUST |
| NFR-C-002 | Audit logging | CMA | G-4 | P20 | MUST |
| NFR-C-003 | GDS Service Standard | CMA | G-7 | P2 | MUST |
| NFR-C-004 | TCoP compliance | CMA | G-7 | P13 | MUST |
| NFR-C-005 | Secure by Design | CMA | G-7 | P6 | MUST |
| NFR-U-001 | Citizen UX | CMA | G-3 | P2 | MUST |
| NFR-U-002 | Accessibility | CMA | G-3 | P2 | MUST |
| NFR-U-003 | Localisation | CMA | G-3 | P2 | EN: MUST; CY: SHOULD |
| NFR-M-001 | Observability | CMA | G-2, G-4 | P7 | MUST |
| NFR-M-002 | Documentation | CMA | G-7 | P16 | MUST |
| NFR-M-003 | Runbooks | CMA | G-7 | P7 | MUST |
| NFR-I-001 | API standards | CMA | G-3 | P5 | MUST |
| NFR-I-002 | Open standards | CMA | G-7 | P1, P5 | MUST |
| NFR-I-003 | Data portability | CMA | O-2 | P1 | MUST |
| INT-001 | Fuel Finder API (VE3) | CMA to VE3 | G-2, G-3, G-4 | P5 | MUST |
| INT-002 | OS Places geocoding | CMA to OS | G-3 | P5 | MUST |
| INT-003 | GOV.UK Notify | CMA to GDS | G-4 | P13 | MUST |
| INT-004 | GOV.UK Design System | CMA | G-3 | P2, P13 | MUST |
| INT-005 | GOV.UK One Login | Future | Future | P13 | COULD |
| INT-006 | CMA Identity Provider | CMA to CMA IT | G-4 | P6 | MUST |
| INT-007 | Companies House API | CMA to CH | G-4 | P5 | SHOULD |
| INT-008 | Android Auto / CarPlay | 3rd Party | G-3, O-2 | P5 | SHOULD |

---

**Generated by**: ArcKit `/arckit:requirements` command
**Generated on**: 2026-04-05 09:15 GMT
**ArcKit Version**: 4.6.3-rc.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: claude-opus-4-6
**Generation Context**: Requirements v3.0 — major revision incorporating live Fuel Finder API (VE3 Global), restructured integration architecture, data synchronisation requirements, and findings from ARC-001-RSCH-v4.1, ARC-001-STKE-v1.0, ARC-000-PRIN-v1.0, ARC-001-RISK-v1.0, ARC-001-SOBC-v1.0, ARC-001-PLAN-v2.0.
