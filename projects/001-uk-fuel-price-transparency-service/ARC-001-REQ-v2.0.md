# Project Requirements: UK Fuel Price Transparency Service

> **Template Status**: Live | **Version**: 1.0.3 | **Command**: `/arckit.requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-REQ-v2.0 |
| **Document Type** | Business and Technical Requirements |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 2.0 |
| **Created Date** | 2026-01-30 |
| **Last Modified** | 2026-01-30 |
| **Review Cycle** | Monthly |
| **Next Review Date** | 2026-03-01 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-30 | ArcKit AI | Initial creation from `/arckit.requirements` command | [PENDING] | [PENDING] |
| 2.0 | 2026-01-30 | ArcKit AI | Added in-car platform use case (UC-7), personas (Mike), functional requirements (FR-014, FR-015), integration requirements (INT-008) for Android Auto / Apple CarPlay | [PENDING] | [PENDING] |

## Document Purpose

This document defines the comprehensive business, functional, non-functional, integration, and data requirements for the UK Government Fuel Price Transparency Service ("Fuel Finder"). It serves as the authoritative requirements baseline for architecture design, vendor evaluation, development, and acceptance testing. Requirements are traced to stakeholder goals (ARC-001-STKE-v1.0) and architecture principles (ARC-000-PRIN-v1.0).

---

## Executive Summary

### Business Context

The Competition and Markets Authority (CMA) recommended an open data scheme for UK fuel prices following its 2023 road fuels market study. The Motor Fuel Price (Open Data) Regulations 2025 mandate that approximately 8,500 UK fuel forecourts submit real-time pricing data. The Fuel Finder service ingests, validates, and publishes this data as open data for citizens, competition analysis, and third-party innovation.

The service is jointly owned by the CMA (enforcement and digital delivery) and the Department for Energy Security and Net Zero (DESNZ — policy and regulation). It must comply with the GDS Service Standard, Technology Code of Practice, UK GDPR, Secure by Design, and HM Treasury governance frameworks.

The regulatory timeline is fixed: forecourt registration deadline is 2 February 2026, with an enforcement grace period ending in early May 2026. This creates an immovable delivery constraint.

### Objectives

- **O1**: Establish a comprehensive, accurate, real-time register of UK fuel prices from all ~8,500 forecourts
- **O2**: Publish fuel price data as open data accessible to citizens and third parties without registration or payment
- **O3**: Provide citizens with a simple, accessible tool to find and compare fuel prices near them
- **O4**: Equip CMA with enforcement tools to detect, investigate, and act on retailer non-compliance
- **O5**: Meet all UK Government governance requirements (GDS Service Standard, TCoP, Secure by Design, UK GDPR)

### Expected Outcomes

Traced to stakeholder outcomes (ARC-001-STKE-v1.0):

- **O-1**: ≥95% of UK forecourts publishing accurate, current prices within 12 months of launch
- **O-2**: 1 million monthly unique users within 12 months; ≥80% user satisfaction
- **O-3**: CMA enforcement capability operational by May 2026; <24h non-compliance detection
- **O-4**: All mandatory governance gates passed (GDS, Secure by Design, DPIA, TCoP)

### Project Scope

**In Scope**:
- Retailer registration and account management
- Fuel price data submission (API and manual web form)
- Data validation, processing, and publication pipeline
- Citizen-facing fuel price comparison service on GOV.UK
- Open data API for third-party consumers
- CMA compliance monitoring and enforcement tools
- Operational dashboards and alerting
- Integration with GOV.UK Notify for retailer communications

**Out of Scope**:
- EV charging point pricing (future phase)
- Hydrogen fuel pricing (future phase)
- Fuel quality or availability data
- Direct price regulation or price-cap mechanisms
- Retailer financial systems or POS integration beyond data submission
- Official Fuel Finder mobile app (Phase 1 relies on third-party apps consuming the open API; official companion app for Android Auto / Apple CarPlay is a COULD_HAVE for future phases)

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

---

## Business Requirements

### BR-001: Establish Universal Forecourt Registration

**Description**: The system MUST enable all UK motor fuel traders to register their forecourts on the Fuel Finder service, capturing the information required under the Motor Fuel Price (Open Data) Regulations 2025.

**Rationale**: Registration is the statutory prerequisite for price data submission. Without universal registration, the open data scheme cannot deliver comprehensive market transparency. (Supports Stakeholder Goal G-1, Driver SD-1, SD-3)

**Success Criteria**:
- ≥97% of known UK forecourts registered by 2 February 2026
- Registration process completable within 15 minutes per forecourt
- Assisted digital channel available for retailers unable to self-serve

**Priority**: MUST_HAVE

**Stakeholder**: CMA SRO (G-1), DESNZ Policy (SD-3)

**Principle Alignment**: Principle 2 (Citizen-Centred Design), Principle 13 (Reuse Government Platforms)

---

### BR-002: Achieve Comprehensive Fuel Price Data Submission

**Description**: The system MUST enable registered forecourts to submit current fuel prices for all fuel types they sell, meeting the data quality and timeliness requirements defined in the regulations.

**Rationale**: Comprehensive, timely, accurate price data is the core value proposition. Without it, citizens cannot make informed decisions and CMA cannot analyse market behaviour. (Supports Goal G-2, Drivers SD-1, SD-2, SD-5)

**Success Criteria**:
- ≥90% of registered forecourts submitting current prices by end of enforcement grace period (May 2026)
- ≥95% compliance within 6 months after grace period
- Data freshness: median time from price change to publication ≤30 minutes for API submitters
- Submission rejection rate <5% (indicating clear data schema)

**Priority**: MUST_HAVE

**Stakeholder**: CMA Board (SD-1), CMA Enforcement (SD-2), Citizens (SD-5)

**Principle Alignment**: Principle 1 (Open Data by Default), Principle 9 (Data Quality and Timeliness)

---

### BR-003: Deliver Citizen Fuel Price Comparison Service

**Description**: The system MUST provide citizens with a simple, accessible, mobile-friendly service to find and compare fuel prices near their location or along a route.

**Rationale**: Citizens are the ultimate beneficiaries. The service must be useful enough to drive adoption and demonstrate consumer benefit. Ministers need a visible, tangible deliverable. (Supports Goal G-3, Outcomes O-1, O-2, Drivers SD-4, SD-5)

**Success Criteria**:
- ≥80% user satisfaction (GOV.UK satisfaction survey)
- ≥95% task completion rate (find fuel price near me)
- WCAG 2.2 AA compliance
- Page load time p95 <3 seconds on mobile
- Pass GDS Service Standard assessment at Beta and Live

**Priority**: MUST_HAVE

**Stakeholder**: Citizens (SD-5), DESNZ Ministers (SD-4), GDS Assessors (SD-9)

**Principle Alignment**: Principle 2 (Citizen-Centred Design), Principle 14 (Performance and Efficiency)

---

### BR-004: Provide CMA Enforcement Capability

**Description**: The system MUST provide CMA enforcement officers with tools to monitor retailer compliance, detect non-compliance, and gather evidence for enforcement actions.

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

### BR-005: Publish Open Data for Third-Party Innovation

**Description**: The system MUST publish fuel price data as open data through a public API and bulk download, licensed under the Open Government Licence, enabling third-party applications, researchers, and journalists to access the data.

**Rationale**: Third-party consumers amplify the service's reach — citizens may access fuel prices through navigation apps, comparison sites, or news articles rather than directly through GOV.UK. Open data is also a statutory requirement. (Supports Outcome O-2, Driver SD-11)

**Success Criteria**:
- Public API with OpenAPI specification published
- Bulk download available in open format (CSV, JSON)
- API developer portal with documentation and sandbox
- ≥10 third-party integrations within 12 months of API launch
- Open Government Licence applied to all published data
- API developer guidelines include Android Auto / Apple CarPlay integration patterns

**Priority**: MUST_HAVE

**Stakeholder**: Third-Party Consumers (SD-11), CMA Board (SD-1)

**Principle Alignment**: Principle 1 (Open Data by Default), Principle 5 (Interoperability)

---

### BR-006: Demonstrate Value for Money

**Description**: The programme MUST deliver within approved budget and demonstrate measurable consumer benefit within 12 months of launch.

**Rationale**: Public money accountability is non-negotiable. NAO and PAC will examine whether the programme delivered value. HM Treasury Green Book requires benefits realisation tracking. (Supports Goal G-5, Outcome O-4, Drivers SD-4, SD-12)

**Success Criteria**:
- Programme spend within ±10% of approved budget
- Benefits realisation tracker operational from launch
- Economic analysis of price transparency effect commissioned within 6 months
- Annual value for money report published

**Priority**: MUST_HAVE

**Stakeholder**: HM Treasury, NAO/PAC (SD-12), DESNZ Ministers (SD-4)

**Principle Alignment**: Principle 22 (Sustainability and Cost Efficiency)

---

### BR-007: Meet All Governance and Compliance Requirements

**Description**: The service MUST pass all mandatory UK Government governance gates: GDS Service Standard assessment, Technology Code of Practice compliance, Secure by Design assessment, DPIA completion, and spend control approval.

**Rationale**: Governance compliance is mandatory for government digital services. Failure blocks progression through delivery phases. (Supports Goal G-7, Outcome O-4, Drivers SD-3, SD-9, SD-10)

**Success Criteria**:
- GDS Service Standard assessment passed at Alpha, Beta, and Live
- DPIA completed before personal data processing begins
- Secure by Design assessment completed before Beta
- TCoP compliance evidence documented
- CDDO spend control approval obtained

**Priority**: MUST_HAVE

**Stakeholder**: GDS Assessors (SD-9), ICO (SD-10), CDDO, SIRO

**Principle Alignment**: Principles 6, 8, 13, 20, 21

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

#### Persona 3: Claire — Supermarket Fuel Chain IT Manager
- **Role**: IT manager responsible for fuel pricing systems across 400+ sites
- **Goals**: Automate price submission via API integration; minimise manual processes; ensure data accuracy across all sites
- **Pain Points**: Needs clear API specification; wants test environment; concerned about system reliability and error handling
- **Technical Proficiency**: High (API integration, automated systems, CI/CD)

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

#### UC-1: Citizen Finds Cheapest Fuel Nearby

**Actor**: Sarah (Motorist)

**Preconditions**:
- Fuel price data is published and current
- Citizen has a web browser (mobile or desktop)

**Main Flow**:
1. Citizen navigates to the Fuel Finder service on GOV.UK
2. System prompts for location (postcode, place name, or "use my location")
3. Citizen enters their postcode or allows geolocation
4. System displays nearby forecourts with current prices, sorted by price (cheapest first)
5. Citizen can filter by fuel type (petrol, diesel) and distance
6. Citizen selects a forecourt to see details (address, opening hours, all fuel prices)
7. System displays directions link (opens in maps application)

**Postconditions**:
- Citizen has identified cheapest fuel option near them
- Page view recorded in analytics

**Alternative Flows**:
- **Alt 3a**: If geolocation denied, system prompts for manual postcode entry
- **Alt 4a**: If no forecourts within default radius, system expands search area and notifies citizen
- **Alt 4b**: If data for a forecourt is stale (>24h), system displays "Last updated" warning

**Exception Flows**:
- **Ex 1**: If service unavailable, display GOV.UK standard error page with "try again later" message

**Business Rules**:
- Default search radius: 5 miles (configurable)
- Results capped at 20 forecourts per page
- Prices display in pence per litre (PPL) to 1 decimal place
- "Last updated" timestamp displayed for each forecourt

**Priority**: CRITICAL

---

#### UC-2: Independent Retailer Submits Fuel Prices (Manual)

**Actor**: Raj (Independent Forecourt Owner)

**Preconditions**:
- Retailer has registered their forecourt
- Retailer is authenticated

**Main Flow**:
1. Retailer logs in to the Fuel Finder service
2. System displays their registered forecourt(s)
3. Retailer selects a forecourt to update
4. System displays current published prices and a form for new prices
5. Retailer enters new price(s) for each fuel type
6. System validates prices (within plausible range, correct format)
7. Retailer confirms submission
8. System acknowledges receipt with confirmation number and timestamp
9. System processes submission asynchronously and publishes updated price

**Postconditions**:
- Fuel prices updated in the system
- Audit trail entry created
- Published data updated within freshness SLA

**Alternative Flows**:
- **Alt 5a**: If retailer enters price outside plausible range (e.g., <80p or >300p), system displays warning but allows override with confirmation
- **Alt 6a**: If validation fails (missing required fields), system highlights errors inline

**Exception Flows**:
- **Ex 1**: If system unavailable during submission, display error with "report technical issue" link and record attempted submission for compliance purposes

**Business Rules**:
- Prices entered in pence per litre to 1 decimal place
- All fuel types currently sold at the forecourt must be updated
- Submission timestamp recorded in UTC
- Previous prices retained in history (not overwritten)

**Priority**: CRITICAL

---

#### UC-3: Large Retailer Submits Prices via API

**Actor**: Claire (Supermarket IT Manager)

**Preconditions**:
- Retailer organisation registered with API credentials
- API integration developed and tested in sandbox

**Main Flow**:
1. Retailer system calls the price submission API endpoint
2. System authenticates the request (API key + OAuth 2.0 client credentials)
3. System validates the payload (JSON schema, required fields, plausible ranges)
4. System returns synchronous acknowledgement with submission ID
5. System processes submission asynchronously (validation, enrichment, publication)
6. If errors detected during async processing, system sends notification via callback URL or GOV.UK Notify

**Postconditions**:
- Prices updated for all submitted forecourts
- Audit trail entry per forecourt per submission
- API response logged

**Alternative Flows**:
- **Alt 3a**: If schema validation fails, return 400 with detailed error messages per field
- **Alt 3b**: If rate limit exceeded, return 429 with Retry-After header

**Exception Flows**:
- **Ex 1**: If system unavailable, return 503 with Retry-After header; retailer retries per documented backoff strategy

**Business Rules**:
- Bulk submission: up to 1,000 forecourts per API call
- Rate limit: 60 requests per minute per organisation
- Idempotent submission: duplicate submissions (same forecourt, same timestamp) are accepted but not re-processed
- API versioning: URL path versioning (e.g., /v1/submissions)

**Priority**: CRITICAL

---

#### UC-4: CMA Enforcement Officer Monitors Compliance

**Actor**: David (CMA Enforcement Officer)

**Preconditions**:
- Officer authenticated with CMA enforcement role
- Compliance monitoring dashboard operational

**Main Flow**:
1. Officer logs in to the enforcement dashboard
2. System displays compliance overview: total registered forecourts, % currently compliant, % non-reporting
3. Officer filters by region, retailer type, or non-compliance duration
4. System displays list of non-compliant forecourts with last submission date and contact details
5. Officer selects a forecourt to view submission history
6. System displays full audit trail: all submissions, timestamps, data quality issues
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
- Non-compliance defined as: no submission within [X hours] of regulatory deadline
- Enforcement actions follow published CMA enforcement guidance escalation path
- Enforcement data access restricted to authorised CMA staff only

**Priority**: CRITICAL

---

#### UC-5: Third-Party Developer Integrates Open Data API

**Actor**: Emma (Third-Party Developer)

**Preconditions**:
- Open data API published with documentation
- No registration required for read-only access

**Main Flow**:
1. Developer discovers API documentation on developer portal
2. Developer reads OpenAPI specification and authentication requirements (none for public data)
3. Developer tests queries against sandbox/production API
4. Developer integrates API into their application
5. System serves fuel price data in JSON format with appropriate caching headers
6. Developer's application displays fuel prices to end users

**Postconditions**:
- Third-party application consuming live fuel price data
- API usage metrics recorded

**Business Rules**:
- No authentication required for open data read access
- Rate limit: 300 requests per minute per IP (adjustable)
- Data licensed under Open Government Licence v3.0
- API responses include Cache-Control headers for appropriate client-side caching
- Bulk download available as alternative to high-frequency API polling

**Priority**: HIGH

---

#### UC-6: Retailer Registers a Forecourt

**Actor**: Raj or Claire (Retailer)

**Preconditions**:
- Retailer has Companies House or HMRC reference for their organisation
- Retailer knows their forecourt address and fuel types

**Main Flow**:
1. Retailer navigates to Fuel Finder registration page on GOV.UK
2. System presents registration form (organisation details, forecourt details)
3. Retailer enters organisation details (company name, Companies House number, contact details)
4. Retailer enters forecourt details (address, fuel types sold, operating hours)
5. System validates address against OS AddressBase or similar gazetteer
6. System geocodes the forecourt location
7. System sends verification email/SMS to contact
8. Retailer confirms verification
9. System creates account and issues credentials (web login; API key if requested)

**Postconditions**:
- Forecourt registered in the system
- Retailer account active
- Forecourt appears on map (without prices until first submission)

**Alternative Flows**:
- **Alt 3a**: If organisation already registered, system links new forecourt to existing organisation
- **Alt 5a**: If address not found in gazetteer, allow manual entry with map pin placement

**Business Rules**:
- One organisation can register multiple forecourts
- Each forecourt must have a unique address
- At least one fuel type must be specified
- Contact details required for compliance communications

**Priority**: CRITICAL

---

#### UC-7: Driver Finds Cheapest Fuel via Android Auto / Apple CarPlay

**Actor**: Mike (Commuter Driver)

**Preconditions**:
- Fuel price data is published and current
- Driver has Android Auto or Apple CarPlay connected in their vehicle
- Fuel Finder companion app installed on smartphone (or third-party app consuming the open API)

**Main Flow**:
1. Driver activates voice assistant ("Hey Google, find cheap petrol nearby" or "Hey Siri, find cheap fuel near me")
2. App queries the Fuel Finder open data API with current GPS coordinates
3. System returns nearby forecourts sorted by cheapest price with distance
4. Results displayed on vehicle head unit in simplified card format (station name, price, distance)
5. Driver selects a forecourt by voice or single tap on head unit
6. App launches turn-by-turn navigation to selected forecourt via native maps integration
7. Driver arrives at forecourt with cheapest fuel

**Postconditions**:
- Driver navigated to cheapest fuel option with minimal distraction
- API query recorded in analytics

**Alternative Flows**:
- **Alt 1a**: If no connected car system, driver uses smartphone app directly (falls back to standard mobile experience)
- **Alt 2a**: If voice recognition fails, driver uses tap interface on head unit display
- **Alt 4a**: If all nearby forecourts have stale data (>24h), results show "Last updated" warning

**Exception Flows**:
- **Ex 1**: If API unavailable, app displays cached results with "Prices may be outdated" warning
- **Ex 2**: If GPS unavailable, prompt driver to enter destination postcode via voice

**Business Rules**:
- In-car display limited to top 5 nearest/cheapest results (driver distraction guidelines)
- Voice interaction must complete within 10 seconds
- No text input permitted while vehicle is in motion (comply with driver distraction regulations)
- Results must be readable at a glance (large fonts, high contrast, minimal detail)

**Priority**: SHOULD_HAVE (first phase via third-party apps; COULD_HAVE for official companion app)

---

### Functional Requirements Detail

#### FR-001: Forecourt Registration

**Description**: The system MUST allow motor fuel traders to register their forecourts, capturing organisation details, forecourt location, fuel types, and contact information.

**Relates To**: BR-001, UC-6

**Acceptance Criteria**:
- [ ] Given a retailer with valid organisation details, when they complete the registration form, then their forecourt is registered and they receive confirmation
- [ ] Given a retailer with multiple forecourts, when they register a second forecourt, then it is linked to their existing organisation account
- [ ] Given an invalid address, when the system cannot match to gazetteer, then the retailer can manually place a pin on a map
- [ ] Given the registration deadline has passed, when a new retailer registers, then the system records late registration for enforcement awareness

**Data Requirements**:
- **Inputs**: Organisation name, Companies House number, contact name, email, phone, forecourt address, fuel types, operating hours
- **Outputs**: Account credentials, forecourt ID, registration confirmation
- **Validations**: Valid email format, valid postcode, Companies House number format, at least one fuel type selected

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: Address gazetteer integration (INT-001), geocoding service (INT-002)

---

#### FR-002: Manual Price Submission (Web Form)

**Description**: The system MUST provide a web-based form for retailers to manually submit current fuel prices for their forecourt(s).

**Relates To**: BR-002, UC-2

**Acceptance Criteria**:
- [ ] Given an authenticated retailer, when they enter valid prices and submit, then prices are recorded with timestamp and confirmation is displayed
- [ ] Given a price outside plausible range (configurable: default <80p or >300p per litre), when the retailer submits, then a warning is displayed but submission is allowed after confirmation
- [ ] Given a retailer with multiple forecourts, when they log in, then they can select which forecourt to update
- [ ] Given required fuel types, when any are missing from submission, then the system highlights missing prices and requests completion

**Data Requirements**:
- **Inputs**: Forecourt ID, fuel type, price (pence per litre, 1 decimal place)
- **Outputs**: Submission confirmation, submission ID, updated published price
- **Validations**: Numeric price, within plausible range, all required fuel types present

**Priority**: MUST_HAVE

**Complexity**: LOW

**Dependencies**: FR-001 (registration), FR-007 (data validation pipeline)

---

#### FR-003: API Price Submission

**Description**: The system MUST provide a versioned RESTful API for automated fuel price submission, supporting bulk updates for retailers with multiple forecourts.

**Relates To**: BR-002, UC-3

**Acceptance Criteria**:
- [ ] Given valid API credentials and a correctly formatted JSON payload, when the retailer calls POST /v1/submissions, then the system returns 202 Accepted with a submission ID
- [ ] Given a payload with up to 1,000 forecourt price updates, when submitted in a single API call, then all are processed
- [ ] Given an invalid payload (schema error), when submitted, then the system returns 400 with field-level error details
- [ ] Given rate limit exceeded (>60 req/min), when submitted, then the system returns 429 with Retry-After header
- [ ] Given duplicate submission (same forecourt + timestamp), when submitted, then the system returns 200 OK (idempotent) without re-processing

**Data Requirements**:
- **Inputs**: JSON array of {forecourt_id, fuel_type, price_ppl, effective_time}
- **Outputs**: Submission ID, per-forecourt status (accepted/rejected with reason)
- **Validations**: JSON schema validation, forecourt ownership verification, price plausibility

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: FR-001 (registration), FR-007 (data validation), NFR-SEC-1 (API authentication)

---

#### FR-004: Citizen Fuel Price Search

**Description**: The system MUST allow citizens to search for fuel prices by location (postcode, place name, or geolocation) and display results sorted by price.

**Relates To**: BR-003, UC-1

**Acceptance Criteria**:
- [ ] Given a valid postcode, when the citizen searches, then nearby forecourts are displayed sorted by cheapest price first
- [ ] Given browser geolocation permission granted, when the citizen clicks "use my location", then results show nearest forecourts
- [ ] Given fuel type filter selected (petrol or diesel), when applied, then only that fuel type's prices are displayed and sorted
- [ ] Given a forecourt with stale data (>24h since last update), when displayed, then a visible "Last updated: X hours ago" warning is shown
- [ ] Given no forecourts within 5 miles, when the citizen searches, then the system expands to 10 miles and informs the citizen

**Data Requirements**:
- **Inputs**: Location (postcode, coordinates, or place name), fuel type filter, distance filter
- **Outputs**: List of forecourts with: name, address, distance, fuel prices, last updated timestamp
- **Validations**: Valid postcode format, coordinates within UK bounding box

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-007 (published data available), INT-002 (geocoding)

---

#### FR-005: Open Data API (Read)

**Description**: The system MUST provide a public read-only API for third-party consumers to query fuel price data, with no authentication required.

**Relates To**: BR-005, UC-5

**Acceptance Criteria**:
- [ ] Given any client (no authentication), when calling GET /v1/prices with location parameters, then fuel price data is returned in JSON
- [ ] Given a request for bulk data, when calling GET /v1/prices/bulk, then a complete dataset is returned (or download link provided)
- [ ] Given more than 300 requests per minute from a single IP, when rate limited, then the system returns 429 with Retry-After header and documentation link
- [ ] Given API versioning, when a new version is released, then the previous version remains available for at least 6 months (deprecation policy)
- [ ] Given an in-car application requesting simplified results, when querying with format=carplay or format=auto, then a navigation-optimised response is returned

**Data Requirements**:
- **Inputs**: Query parameters (latitude, longitude, radius, fuel_type, format)
- **Outputs**: JSON array of forecourt objects with prices, location, metadata; appropriate Cache-Control headers
- **Validations**: Parameters within valid ranges; radius ≤50 miles

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-007 (data processing pipeline), NFR-I-1 (API standards)

---

#### FR-006: Compliance Monitoring Dashboard

**Description**: The system MUST provide CMA enforcement officers with a dashboard showing real-time retailer compliance status, including submission rates, timeliness, coverage gaps, and non-compliant forecourt identification.

**Relates To**: BR-004, UC-4

**Acceptance Criteria**:
- [ ] Given an authenticated enforcement officer, when accessing the dashboard, then headline compliance metrics are displayed: total registered, % compliant, % non-reporting, trend over time
- [ ] Given filtering by region or retailer type, when applied, then metrics and forecourt lists update accordingly
- [ ] Given a non-compliant forecourt, when selected, then full submission history and contact details are displayed
- [ ] Given an enforcement action is initiated, when the officer triggers a warning, then GOV.UK Notify sends the appropriate template to the retailer
- [ ] Given a request for export, when the officer clicks "Export CSV", then compliance data is downloaded for offline analysis

**Data Requirements**:
- **Inputs**: Enforcement officer authentication, filter criteria
- **Outputs**: Compliance metrics, forecourt lists, submission histories, enforcement action records
- **Validations**: Role-based access (enforcement role required)

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: FR-001 (registration data), FR-007 (submission data), NFR-SEC-2 (authorisation), INT-003 (GOV.UK Notify)

---

#### FR-007: Data Validation and Processing Pipeline

**Description**: The system MUST validate, enrich, and process all fuel price submissions asynchronously, applying quality rules before publication.

**Relates To**: BR-002, BR-005

**Acceptance Criteria**:
- [ ] Given a valid submission, when processed, then the price is published within the freshness SLA (≤15 minutes for API submissions, ≤30 minutes for manual)
- [ ] Given a submission with a price outside plausible range, when validated, then the submission is flagged but published with a quality indicator
- [ ] Given an anomalous price change (>20% change in 24 hours), when detected, then an alert is generated for operations review
- [ ] Given a submission for a closed forecourt, when processed, then the submission is rejected with appropriate error
- [ ] Given pipeline failure, when a submission cannot be processed, then it is queued for retry and an alert is raised

**Data Requirements**:
- **Inputs**: Raw submission data
- **Outputs**: Validated, enriched, published price data; quality metrics; anomaly alerts
- **Validations**: Price plausibility (configurable range), required fields, forecourt status check, duplicate detection

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: FR-001 (forecourt registry), messaging infrastructure

---

#### FR-008: Retailer Account Management

**Description**: The system MUST allow retailers to manage their account, update forecourt details, add/remove forecourts, and manage API credentials.

**Relates To**: BR-001, BR-002

**Acceptance Criteria**:
- [ ] Given an authenticated retailer, when they update forecourt details (hours, fuel types), then changes are reflected in published data
- [ ] Given a retailer adding a new forecourt, when registration is completed, then the new forecourt appears in their account
- [ ] Given a retailer requesting API credentials, when approved, then client ID and secret are generated and displayed once
- [ ] Given a retailer needing to rotate API credentials, when they regenerate, then old credentials are revoked after a grace period (24 hours)

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001, NFR-SEC-1

---

#### FR-009: Retailer Notifications

**Description**: The system SHOULD send automated notifications to retailers for compliance reminders, submission confirmations, and account-related events via GOV.UK Notify.

**Relates To**: BR-002, BR-004

**Acceptance Criteria**:
- [ ] Given a forecourt with no submission for [X] hours, when the reminder threshold is reached, then an automated email/SMS reminder is sent
- [ ] Given a successful price submission, when processed, then an optional confirmation notification is sent (configurable by retailer)
- [ ] Given an enforcement action, when initiated by CMA, then the appropriate notification template is sent to the retailer's registered contact

**Priority**: SHOULD_HAVE

**Complexity**: LOW

**Dependencies**: INT-003 (GOV.UK Notify)

---

#### FR-010: Audit Trail and Evidence Preservation

**Description**: The system MUST maintain an immutable, tamper-evident audit trail of all retailer submissions, enforcement actions, and administrative changes for CMA enforcement purposes.

**Relates To**: BR-004

**Acceptance Criteria**:
- [ ] Given any price submission (API or manual), when received, then the complete submission is recorded with: timestamp (UTC, millisecond), source IP/channel, payload, submitter identity, and submission ID
- [ ] Given an enforcement officer requesting evidence for a forecourt, when queried, then the complete submission history is returned with cryptographic integrity verification
- [ ] Given an attempt to modify an audit record, when detected, then the system prevents modification and logs the attempt as a security event
- [ ] Given audit data older than the retention period, when retention policy executes, then data is archived (not deleted) to tamper-evident long-term storage

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: NFR-C-2 (audit logging), NFR-SEC-3 (encryption)

---

#### FR-011: Policy Analysis and Reporting

**Description**: The system SHOULD provide DESNZ policy analysts with tools to analyse fuel price trends, geographic patterns, and market competitiveness.

**Relates To**: BR-006

**Acceptance Criteria**:
- [ ] Given authenticated DESNZ analyst access, when querying historical price data, then aggregate reports are available (average prices by region, fuel type, time period)
- [ ] Given a request for ministerial briefing data, when generated, then headline metrics are exportable (coverage rate, average prices, price trends)
- [ ] Given data export request, when executed, then data is available in CSV and JSON formats

**Priority**: SHOULD_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-007 (processed data), data warehouse/analytics capability

---

#### FR-012: Technical Failure Reporting

**Description**: The system MUST provide a mechanism for retailers to report that they are unable to submit prices due to technical failure (their own or the service's), to distinguish genuine non-compliance from technical issues.

**Relates To**: BR-002, BR-004

**Acceptance Criteria**:
- [ ] Given a retailer experiencing technical issues, when they report a failure via web form or phone, then the forecourt is flagged as "technical failure" rather than "non-compliant"
- [ ] Given a technical failure report, when CMA reviews compliance, then the forecourt is excluded from non-compliance metrics for the reported period
- [ ] Given the technical failure is resolved, when the retailer resumes submissions, then normal compliance monitoring resumes

**Priority**: MUST_HAVE

**Complexity**: LOW

**Dependencies**: FR-006 (compliance dashboard), FR-009 (notifications)

---

#### FR-013: Service Feedback and Support

**Description**: The system SHOULD provide feedback mechanisms for both citizens and retailers, and support channels for retailers needing compliance help.

**Relates To**: BR-003, BR-001

**Acceptance Criteria**:
- [ ] Given a citizen using the service, when they click "Report a problem" or "Give feedback", then they can submit feedback via standard GOV.UK feedback component
- [ ] Given a retailer needing help, when they access the support section, then plain-English guidance, FAQs, and contact details (phone/email) are available
- [ ] Given feedback submitted, when aggregated, then analytics are available for service improvement

**Priority**: SHOULD_HAVE

**Complexity**: LOW

**Dependencies**: GOV.UK Design System components

---

#### FR-014: Android Auto and Apple CarPlay Compatible API Responses

**Description**: The open data API (FR-005) MUST return responses in a format optimised for consumption by Android Auto and Apple CarPlay applications, including simplified result sets and navigation-ready coordinates.

**Relates To**: BR-003, BR-005, UC-7

**Acceptance Criteria**:
- [ ] Given an API query with `format=carplay` or `format=auto` parameter, when results are returned, then the response includes a simplified schema with: station_name, brand, fuel_type, price_ppl, distance_miles, latitude, longitude, and navigation_uri (geo: URI for native maps)
- [ ] Given in-car display constraints, when results are requested, then the API supports a `limit` parameter (default 5 for in-car use) to restrict result count
- [ ] Given the need for rapid response on mobile networks, when queried from an in-car app, then API response time is <300ms (p95) for nearby search
- [ ] Given voice-activated search, when a natural language location query is received (e.g., "petrol near me"), then the API accepts lat/lng coordinates as primary location input

**Data Requirements**:
- **Inputs**: Latitude, longitude, fuel_type (optional), limit (optional, default 5), format (optional: standard, carplay, auto)
- **Outputs**: Simplified JSON array with navigation-ready data including `geo:` URI scheme coordinates
- **Validations**: GPS coordinates within UK bounding box; limit 1-20

**Priority**: SHOULD_HAVE

**Complexity**: LOW (extension of existing FR-005 open data API)

**Dependencies**: FR-005 (Open Data API)

---

#### FR-015: Third-Party In-Car App Integration Guidelines

**Description**: The service SHOULD publish developer guidelines and best practices for building Android Auto and Apple CarPlay compatible applications that consume the Fuel Finder open data API, including UX patterns for driver safety.

**Relates To**: BR-005, UC-7

**Acceptance Criteria**:
- [ ] Given a third-party developer building an in-car app, when they access the developer portal, then guidelines for Android Auto and Apple CarPlay integration are available
- [ ] Given driver safety requirements, when guidelines are published, then they include: maximum results displayed, font size recommendations, voice interaction patterns, and prohibited interactions while driving
- [ ] Given Apple CarPlay and Android Auto platform review requirements, when documented, then the guidelines reference platform-specific template requirements (e.g., CarPlay List Template, Android Auto Place List Template)

**Priority**: SHOULD_HAVE

**Complexity**: LOW (documentation, not code)

**Dependencies**: FR-005, developer portal (NFR-M-002)

---

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-001: Citizen Search Response Time

**Requirement**: Citizen-facing fuel price search MUST return results within:
- Page load time: <3 seconds (p95) on mobile 3G connections
- API response time for open data queries: <500ms (p95)
- API response time for open data queries: <200ms (p50)

**Measurement Method**: Real user monitoring (RUM) and synthetic monitoring; APM tooling

**Load Conditions**:
- Normal load: 100 concurrent citizen searches
- Peak load: 10,000 concurrent citizen searches (media event / fuel crisis)
- Data volume: ~8,500 forecourts, ~25,000 price records (multiple fuel types per forecourt)

**Priority**: MUST_HAVE

**Relates To**: BR-003, Goal G-3

**Principle Alignment**: Principle 14 (Performance and Efficiency)

---

#### NFR-P-002: Data Ingestion Throughput

**Requirement**: The data ingestion pipeline MUST process:
- Sustained: 100 submissions per minute (normal operations)
- Peak: 5,000 submissions per minute (all large chains submitting simultaneously)
- End-to-end processing time: ≤15 minutes from API submission to published data (p95)

**Measurement Method**: Pipeline metrics; data freshness SLI

**Priority**: MUST_HAVE

**Relates To**: BR-002, Goal G-2

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

**Requirement**: The Fuel Finder service MUST achieve:
- Citizen-facing service: 99.9% availability (≤43.8 minutes unplanned downtime per month)
- Retailer submission API: 99.95% availability (≤21.9 minutes unplanned downtime per month)
- CMA enforcement dashboard: 99.5% availability (≤3.6 hours unplanned downtime per month)

**Maintenance Windows**: Planned maintenance permitted Sundays 02:00–06:00 UTC with 7 days' notice to retailers

**Priority**: MUST_HAVE

**Relates To**: BR-002, BR-003, Goal G-2

**Principle Alignment**: Principle 15 (Availability and Reliability)

---

#### NFR-A-002: Disaster Recovery

**RPO (Recovery Point Objective)**: Maximum 15 minutes of data loss for submission data; zero data loss for audit trail

**RTO (Recovery Time Objective)**: Service restored within 4 hours of disaster declaration

**Backup Requirements**:
- Backup frequency: Continuous replication for submission database; hourly snapshots for analytics
- Backup retention: 30 days for operational backups; indefinite for audit trail archives
- Geographic backup location: Secondary UK availability zone (separate from primary)

**Failover Requirements**:
- Automatic failover to secondary availability zone: YES
- Failover time: <15 minutes for automated failover

**Priority**: MUST_HAVE

**Relates To**: Principle 4 (Resilience and Fault Tolerance)

---

#### NFR-A-003: Fault Tolerance

**Requirement**: The system MUST gracefully degrade when components fail:
- If data processing pipeline fails: citizen service continues to serve last-known prices with staleness indicators
- If citizen search is degraded: retailer submission continues unaffected (bulkhead isolation)
- If GOV.UK Notify is unavailable: notifications are queued and retried; submissions are not blocked

**Resilience Patterns Required**:
- [ ] Circuit breaker for all external dependencies (geocoding, Notify, address lookup)
- [ ] Retry with exponential backoff (max 3 retries, 1s/2s/4s)
- [ ] Timeout on all network calls (default: 5 seconds)
- [ ] Bulkhead isolation between ingestion and serving tiers
- [ ] Graceful degradation with staleness indicators

**Priority**: MUST_HAVE

**Relates To**: Principle 4 (Resilience and Fault Tolerance)

---

### Scalability Requirements

#### NFR-S-001: Horizontal Scaling

**Requirement**: All stateless components MUST support horizontal scaling without code changes

**Growth Projections**:
- Year 1: 8,500 forecourts, 1M monthly citizen users, 10 third-party integrations
- Year 2: 9,000 forecourts (new builds), 3M monthly citizen users, 50 third-party integrations; Android Auto / Apple CarPlay app integrations emerging
- Year 3: 10,000 forecourts (potentially including EV charging), 5M monthly users, 100+ third-party integrations; significant in-car app usage driving API traffic growth

**Scaling Triggers**: Auto-scale based on CPU utilisation (>70%), request queue depth, and response latency

**Priority**: MUST_HAVE

**Relates To**: Principle 3 (Scalability and Elasticity)

---

#### NFR-S-002: Data Volume Scaling

**Requirement**: The system MUST handle data growth for:
- Price submissions: ~150,000 per day (Year 1) growing to ~300,000 per day (Year 3)
- Historical price data: ~55M records per year, retained indefinitely for public record
- Audit data: ~200M events per year, retained for 7+ years

**Data Archival Strategy**: Hot storage for current + 90 days; warm storage for 90 days to 2 years; cold archival beyond 2 years. All tiers queryable.

**Priority**: MUST_HAVE

---

### Security Requirements

#### NFR-SEC-001: Authentication

**Requirement**: All user access MUST be authenticated using industry-standard protocols:
- **Retailers**: Username/password with mandatory MFA for all account access
- **CMA Staff**: Integrated with CMA corporate identity provider (SSO)
- **API Consumers (submission)**: OAuth 2.0 client credentials grant
- **Citizens (read-only)**: No authentication required for public data access
- **Third-Party API (read-only)**: No authentication required; rate limiting by IP

**Session Management**:
- Session timeout: 30 minutes of inactivity (retailer and CMA interfaces)
- Absolute session timeout: 8 hours
- Re-authentication required for: credential rotation, enforcement actions

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 6 (Security by Design)

---

#### NFR-SEC-002: Authorisation

**Requirement**: Role-based access control (RBAC) with least privilege:

| Role | Permissions |
|------|------------|
| Citizen | Read published fuel prices (no authentication) |
| Retailer User | Submit prices for own forecourts; manage own account |
| Retailer Admin | All retailer user permissions + manage organisation, API credentials |
| CMA Operations | View dashboards, data quality metrics |
| CMA Enforcement | All operations + compliance monitoring, enforcement actions, audit trail access |
| CMA Admin | All enforcement + user management, system configuration |
| DESNZ Analyst | Read published and aggregate data; export reports |
| System Service | Inter-service communication; data processing |

**Privilege Elevation**: Enforcement actions require MFA re-authentication; admin actions require approval workflow

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 6 (Security by Design)

---

#### NFR-SEC-003: Data Encryption

**Requirement**:
- Data in transit: TLS 1.2+ (prefer 1.3) for all communications
- Data at rest: AES-256 or equivalent for all data stores
- Key management: Managed key service within UK sovereign cloud

**Encryption Scope**:
- [ ] Database encryption at rest (all databases)
- [ ] Backup encryption (all backups)
- [ ] File storage encryption (all object storage)
- [ ] Application-level field encryption for PII (retailer contact details)
- [ ] Audit trail integrity (cryptographic hashing for tamper evidence)

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 6 (Security by Design)

---

#### NFR-SEC-004: Secrets Management

**Requirement**: No secrets (API keys, passwords, certificates, database credentials) stored in code, configuration files, or environment variables at rest

**Secrets Management**: All secrets stored in a managed secrets service, injected at runtime

**Secrets Rotation**: Automatic rotation every 90 days for service credentials; retailer API credentials rotatable on demand

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
- [ ] DPIA completed before processing personal data (retailer contact details)
- [ ] Lawful basis documented: public task under Article 6(1)(e) — performance of a task in the public interest
- [ ] Privacy notices published at point of data collection (retailer registration)
- [ ] Data subject rights processes operational (access, rectification, erasure where lawful)
- [ ] Data breach notification within 72 hours to ICO
- [ ] Data minimisation verified — only personal data necessary for regulatory purpose

**Data Residency**: All data MUST be stored and processed within UK sovereign territory

**Data Retention**:
- Published fuel price data: Retained indefinitely as public record
- Retailer contact details: Duration of registration plus 6 years
- Audit logs: 7 years minimum
- Application logs: 90 days

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 8 (Data Sovereignty), Principle 21 (Privacy by Design), Goal G-6, Driver SD-10

---

#### NFR-C-002: Audit Logging

**Requirement**: Comprehensive, tamper-evident audit trail for compliance and CMA enforcement

**Audit Log Contents** (for all data submissions and enforcement actions):
- **Who**: User/service identity (authenticated principal)
- **What**: Action performed (submission, query, enforcement action, account change)
- **When**: Timestamp (UTC, millisecond precision)
- **Where**: System component, API endpoint, IP address
- **Why**: Context (submission ID, transaction ID, enforcement case reference)
- **Result**: Success/failure with error details

**Log Retention**: 7 years for enforcement-related audit logs (immutable storage)

**Log Integrity**: Tamper-evident logging — cryptographic chain hashing or append-only storage with integrity verification

**Priority**: MUST_HAVE

**Relates To**: Principle 20 (Regulatory Compliance by Design), FR-010

---

#### NFR-C-003: GDS Service Standard Compliance

**Requirement**: The service MUST comply with all 14 points of the GDS Service Standard and pass assessment at Alpha, Beta, and Live phases

**Key Evidence Requirements**:
- Point 1: User research evidence with real users at each phase
- Point 2: Solve a whole problem for users
- Point 3: Provide a joined-up experience across channels
- Point 5: Make sure everyone can use the service (accessibility)
- Point 6: Have a multidisciplinary team
- Point 9: Create a secure service (Secure by Design)
- Point 10: Define what success looks like and publish performance data
- Point 12: Make new source code open
- Point 14: Operate a reliable service

**Priority**: MUST_HAVE

**Relates To**: Goal G-7, Driver SD-9

---

#### NFR-C-004: Technology Code of Practice (TCoP)

**Requirement**: All technology decisions MUST comply with the 12 points of the Technology Code of Practice

**Key Compliance Areas**:
- [ ] Define user needs (Point 1)
- [ ] Make things accessible and inclusive (Point 2)
- [ ] Be open and use open source (Point 3)
- [ ] Make use of open standards (Point 4)
- [ ] Use cloud first (Point 5)
- [ ] Make things secure (Point 6)
- [ ] Make privacy integral (Point 7)
- [ ] Share, reuse, and collaborate (Point 8)
- [ ] Integrate and adapt technology (Point 9)
- [ ] Make better use of data (Point 10)
- [ ] Define your purchasing strategy (Point 11)
- [ ] Meet the Service Standard (Point 12)

**Priority**: MUST_HAVE

**Relates To**: Principle 13 (Reuse Government Platforms)

---

#### NFR-C-005: Secure by Design

**Requirement**: The service MUST complete an NCSC Secure by Design assessment before entering Beta phase

**Requirements**:
- [ ] Threat model completed for all components
- [ ] Security controls mapped to identified threats
- [ ] Penetration test conducted by CHECK-approved provider
- [ ] SIRO sign-off on residual risk
- [ ] Incident response plan documented and tested

**Priority**: MUST_HAVE (NON-NEGOTIABLE)

**Relates To**: Principle 6 (Security by Design)

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

**User Onboarding**: No onboarding required — single-purpose, self-explanatory interface following GOV.UK patterns

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

**Relates To**: BR-003, BR-007

---

#### NFR-U-003: Localisation

**Requirement**: The service MUST support English. Welsh language support SHOULD be available for citizen-facing pages.

**Localisation Scope**:
- [ ] English (primary, mandatory)
- [ ] Welsh (citizen-facing pages, to comply with Welsh Language Act where applicable)
- [ ] Pence per litre formatting (UK convention)
- [ ] UK date format (DD/MM/YYYY) in user interfaces
- [ ] ISO 8601 dates in API responses

**Priority**: English: MUST_HAVE; Welsh: SHOULD_HAVE

---

### Maintainability and Supportability Requirements

#### NFR-M-001: Observability

**Requirement**: Comprehensive instrumentation for monitoring, troubleshooting, and capacity planning

**Telemetry Requirements**:
- **Logging**: Structured JSON logs with correlation IDs, centralised aggregation
- **Metrics**: Request rate, error rate, duration (RED); data freshness; submission volumes; compliance rates
- **Tracing**: Distributed tracing across ingestion pipeline components
- **Dashboards**: Real-time operational dashboards for: service health, data freshness, submission volumes, compliance rates, API usage
- **Alerts**: SLO-based alerting with runbooks; data freshness breach alerts; security event alerts

**Business Metrics Dashboard**:
- Forecourt registration rate
- Submission compliance rate (% of forecourts with current data)
- Data freshness (median and p95)
- Citizen usage (unique users, searches, satisfaction)
- API consumer usage (requests, top consumers)

**Priority**: MUST_HAVE

**Relates To**: Principle 7 (Observability and Operational Excellence)

---

#### NFR-M-002: Documentation

**Requirement**: Comprehensive documentation for operators, developers, and retailers

**Documentation Types**:
- [ ] Architecture documentation (system context, component diagrams)
- [ ] API documentation (OpenAPI 3.0 specification for all APIs)
- [ ] Retailer guidance (plain English, step-by-step)
- [ ] Operational runbooks (deployment, rollback, incident response, DR)
- [ ] Developer onboarding guide
- [ ] Third-party API developer portal

**Documentation Currency**: Updated within 5 working days of code changes

**Priority**: MUST_HAVE

---

#### NFR-M-003: Operational Runbooks

**Requirement**: Runbooks for all common operational scenarios

**Runbook Coverage**:
- [ ] Deployment and rollback procedures
- [ ] Data pipeline failure and recovery
- [ ] Citizen service degradation response
- [ ] Retailer submission API incident
- [ ] Security incident response
- [ ] Disaster recovery procedure
- [ ] Capacity scaling (manual and automated)
- [ ] Data quality issue investigation

**Priority**: MUST_HAVE

---

### Portability and Interoperability Requirements

#### NFR-I-001: API Standards

**Requirement**: All APIs MUST follow open standards

**API Design Principles**:
- RESTful design with standard HTTP methods
- JSON request/response format
- Versioning via URL path (/v1/, /v2/)
- OpenAPI 3.0 specification published for all APIs
- Consistent error response format (RFC 7807 Problem Details)
- Pagination for list endpoints (cursor-based preferred)
- Rate limiting with standard headers (X-RateLimit-*, Retry-After)

**Priority**: MUST_HAVE

**Relates To**: Principle 5 (Interoperability and Integration)

---

#### NFR-I-002: Open Standards and Open Source

**Requirement**: The service MUST use open standards and make new source code open (GDS Service Standard Point 12; TCoP Point 3/4)

**Requirements**:
- Source code published in a public repository (unless security exemption applies)
- Open data published under Open Government Licence v3.0
- Open standards for data formats (JSON, CSV)
- No vendor lock-in for data formats or storage
- Infrastructure defined as code using open-source tooling where practical

**Priority**: MUST_HAVE

**Relates To**: Principle 1 (Open Data by Default), NFR-C-003, NFR-C-004

---

#### NFR-I-003: Data Portability

**Requirement**: Fuel price data MUST be exportable in open formats

**Export Formats**: CSV, JSON (GeoJSON for location-aware consumers)

**Export Scope**: Complete dataset (bulk download), filtered by date range, region, fuel type

**Import Capability**: Not applicable (data flows inward from retailers only)

**Priority**: MUST_HAVE

---

---

## Integration Requirements

### External System Integrations

#### INT-001: Address Gazetteer (OS AddressBase or Equivalent)

**Purpose**: Validate and standardise forecourt addresses during registration; resolve postcodes to coordinates

**Integration Type**: Real-time API (query on registration)

**Data Exchanged**:
- **From Fuel Finder to Gazetteer**: Postcode or address string
- **From Gazetteer to Fuel Finder**: Standardised address, UPRN, coordinates (latitude/longitude)

**Integration Pattern**: Request/response (synchronous)

**Authentication**: API key or OAuth 2.0 (per provider)

**Error Handling**: If gazetteer unavailable, allow manual address entry with map pin; retry for background geocoding

**SLA**: <2 seconds response time; 99.9% availability

**Owner**: CMA Digital Team

**Priority**: MUST_HAVE

---

#### INT-002: Geocoding Service

**Purpose**: Convert postcodes and place names to coordinates for proximity search; calculate distances

**Integration Type**: Real-time API

**Data Exchanged**:
- **From Fuel Finder**: Postcode, place name, or address
- **From Service**: Latitude, longitude, formatted address

**Integration Pattern**: Request/response; results cacheable

**Error Handling**: Circuit breaker; fallback to cached postcode-to-coordinate lookup table

**SLA**: <500ms response time; 99.9% availability

**Priority**: MUST_HAVE

---

#### INT-003: GOV.UK Notify

**Purpose**: Send emails and SMS to retailers for compliance reminders, submission confirmations, enforcement notices, and account notifications

**Integration Type**: Real-time API (per notification); batch for bulk reminders

**Data Exchanged**:
- **From Fuel Finder to Notify**: Notification type, recipient details, template parameters
- **From Notify to Fuel Finder**: Delivery status callbacks

**Integration Pattern**: Request/response for send; webhook for delivery status

**Authentication**: API key (GOV.UK Notify standard)

**Error Handling**: Retry with exponential backoff; dead letter queue for persistently failed notifications; alert operations

**SLA**: Per GOV.UK Notify published SLA

**Owner**: GDS (GOV.UK Notify team)

**Priority**: MUST_HAVE

---

#### INT-004: GOV.UK Design System and Frontend

**Purpose**: Citizen-facing service hosted on GOV.UK using GOV.UK Design System components for consistent, accessible UI

**Integration Type**: Frontend framework integration (GOV.UK Frontend, Nunjucks templates or equivalent)

**Data Exchanged**: N/A (UI framework, not data integration)

**Priority**: MUST_HAVE

**Relates To**: NFR-U-001, NFR-C-003

---

#### INT-005: GOV.UK One Login (Future Consideration)

**Purpose**: Citizen identity verification if future features require authenticated citizen access (e.g., saved preferences, alerts)

**Integration Type**: OIDC/OAuth 2.0

**Note**: Not required for initial launch (citizen access is anonymous). Included for architectural awareness.

**Priority**: COULD_HAVE (future phase)

---

#### INT-006: CMA Corporate Identity Provider

**Purpose**: Single sign-on for CMA staff accessing enforcement dashboard and administration tools

**Integration Type**: SAML 2.0 or OIDC federation with CMA identity provider

**Data Exchanged**:
- **From CMA IdP to Fuel Finder**: Authenticated identity, role claims, group membership
- **From Fuel Finder to CMA IdP**: Authentication request, logout

**Authentication**: SAML 2.0 or OIDC (per CMA IT standard)

**Priority**: MUST_HAVE

---

#### INT-007: Companies House API

**Purpose**: Validate retailer organisation details during registration (company name, registration number, status)

**Integration Type**: Real-time API (query during registration)

**Data Exchanged**:
- **From Fuel Finder**: Company number
- **From Companies House**: Company name, status, registered address

**Error Handling**: If unavailable, allow manual entry with deferred verification

**Priority**: SHOULD_HAVE

---

#### INT-008: Android Auto and Apple CarPlay Platform Compatibility

**Purpose**: Ensure the open data API and any official companion app are compatible with Android Auto and Apple CarPlay platform requirements for fuel/navigation category apps

**Integration Type**: Platform API compliance (Google and Apple platform SDKs)

**Data Exchanged**:
- **From Fuel Finder API to In-Car App**: Simplified fuel price results with navigation-ready coordinates
- **From In-Car App to Vehicle**: Display templates (list cards, navigation intents)
- **From Vehicle to In-Car App**: User selections, voice commands

**Integration Pattern**: The Fuel Finder service does not directly integrate with Android Auto/Apple CarPlay. Instead, the open data API (FR-005) is consumed by third-party apps that implement the platform SDKs. The service's role is to ensure API responses are optimised for in-car consumption.

**Authentication**: No authentication required (open data API)

**Error Handling**: In-car apps should cache recent results; display graceful offline message if API unavailable

**SLA**: API response <300ms (p95) to support responsive in-car experience

**Owner**: Third-party developers (CMA publishes guidelines per FR-015)

**Priority**: SHOULD_HAVE

---

---

## Data Requirements

### Data Entities

#### Entity 1: Organisation

**Description**: A motor fuel trader (company or sole trader) that operates one or more forecourts

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| organisation_id | UUID | Yes | Unique identifier | Primary key |
| name | String(255) | Yes | Organisation name | Not null |
| companies_house_number | String(8) | No | Companies House registration | Format validated |
| contact_name | String(255) | Yes | Primary contact name | PII — encrypted |
| contact_email | String(255) | Yes | Primary contact email | PII — encrypted, format validated |
| contact_phone | String(20) | Yes | Primary contact phone | PII — encrypted |
| registration_date | Timestamp | Yes | When the organisation registered | Indexed |
| status | Enum | Yes | Account status | ['active', 'suspended', 'deregistered'] |
| created_at | Timestamp | Yes | Record creation | Indexed |
| updated_at | Timestamp | Yes | Last update | Indexed |

**Relationships**: One-to-many with Forecourt

**Data Volume**: ~3,000 organisations (Year 1)

**Data Classification**: OFFICIAL (contains PII — contact details)

**Data Retention**: Duration of registration + 6 years

---

#### Entity 2: Forecourt

**Description**: A physical fuel retail location (petrol station / filling station)

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| forecourt_id | UUID | Yes | Unique identifier | Primary key |
| organisation_id | UUID | Yes | Owning organisation | Foreign key |
| name | String(255) | Yes | Forecourt display name | Not null |
| address_line_1 | String(255) | Yes | Street address | Not null |
| address_line_2 | String(255) | No | Additional address | |
| town | String(100) | Yes | Town/city | Not null |
| postcode | String(10) | Yes | UK postcode | Format validated, indexed |
| latitude | Decimal(10,7) | Yes | WGS84 latitude | Range: 49.0–61.0 |
| longitude | Decimal(10,7) | Yes | WGS84 longitude | Range: -8.0–2.0 |
| uprn | String(12) | No | Unique Property Reference Number | |
| fuel_types | Array[Enum] | Yes | Fuel types sold | ['unleaded', 'super_unleaded', 'diesel', 'premium_diesel'] |
| opening_hours | JSON | No | Operating hours | Structured JSON |
| status | Enum | Yes | Forecourt status | ['active', 'closed', 'suspended'] |
| registration_date | Timestamp | Yes | When registered | Indexed |
| created_at | Timestamp | Yes | Record creation | Indexed |
| updated_at | Timestamp | Yes | Last update | Indexed |

**Relationships**: Many-to-one with Organisation; One-to-many with PriceSubmission

**Data Volume**: ~8,500 forecourts (Year 1), ~10,000 (Year 3)

**Access Patterns**: Geographic queries (lat/lng + radius); postcode lookup; organisation lookup; status filtering

**Data Classification**: OFFICIAL — PUBLIC (addresses and locations are public; published as open data)

**Data Retention**: Indefinite (public record)

---

#### Entity 3: PriceSubmission

**Description**: A fuel price data submission from a retailer for a specific forecourt

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| submission_id | UUID | Yes | Unique submission identifier | Primary key |
| forecourt_id | UUID | Yes | Which forecourt | Foreign key, indexed |
| submitted_by | UUID | Yes | User/API client | Foreign key |
| submission_channel | Enum | Yes | How submitted | ['web', 'api'] |
| submitted_at | Timestamp | Yes | When received (UTC, ms) | Indexed |
| effective_time | Timestamp | No | When price took effect | |
| prices | JSON | Yes | Array of {fuel_type, price_ppl} | Schema validated |
| validation_status | Enum | Yes | Processing result | ['valid', 'warning', 'rejected'] |
| validation_messages | JSON | No | Validation details | |
| processed_at | Timestamp | No | When processing completed | |
| published_at | Timestamp | No | When published to open data | |
| source_ip | String(45) | Yes | Submitter IP address | Audit field |
| request_id | UUID | Yes | Correlation ID | Indexed |

**Relationships**: Many-to-one with Forecourt

**Data Volume**: ~150,000 per day (Year 1), growing to ~300,000 per day (Year 3); ~55M per year

**Access Patterns**: By forecourt (latest + history); by time range; by validation status; aggregate compliance queries

**Data Classification**: OFFICIAL — PUBLIC (prices are published as open data; submission metadata is OFFICIAL)

**Data Retention**: Indefinite for published prices; 7 years for full submission audit trail

---

#### Entity 4: PublishedPrice

**Description**: The current published fuel price for a forecourt (derived from PriceSubmission, optimised for query)

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| forecourt_id | UUID | Yes | Which forecourt | Primary key (composite) |
| fuel_type | Enum | Yes | Fuel type | Primary key (composite) |
| price_ppl | Decimal(5,1) | Yes | Price in pence per litre | Range: 50.0–500.0 |
| last_updated | Timestamp | Yes | When price was last updated | Indexed |
| submission_id | UUID | Yes | Source submission | Foreign key |
| data_quality | Enum | Yes | Quality indicator | ['good', 'stale', 'warning'] |

**Access Patterns**: Geographic proximity query (lat/lng + radius + fuel_type); bulk export; freshness monitoring

**Data Classification**: OFFICIAL — PUBLIC

**Data Retention**: Current record replaced on each update; historical data in PriceSubmission entity

---

#### Entity 5: EnforcementAction

**Description**: A CMA enforcement action against a non-compliant retailer

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| action_id | UUID | Yes | Unique identifier | Primary key |
| forecourt_id | UUID | Yes | Target forecourt | Foreign key |
| organisation_id | UUID | Yes | Target organisation | Foreign key |
| action_type | Enum | Yes | Type of action | ['reminder', 'warning', 'formal_notice', 'penalty'] |
| initiated_by | UUID | Yes | CMA officer | Foreign key |
| initiated_at | Timestamp | Yes | When action initiated | Indexed |
| reason | Text | Yes | Reason for action | Not null |
| evidence_refs | Array[UUID] | Yes | Linked submission IDs | |
| status | Enum | Yes | Action status | ['pending', 'sent', 'acknowledged', 'resolved', 'escalated'] |
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
| event_type | Enum | Yes | Type of event | ['submission', 'login', 'account_change', 'enforcement_action', 'config_change', 'data_export'] |
| actor_id | UUID | Yes | Who performed the action | Indexed |
| actor_type | Enum | Yes | Type of actor | ['retailer', 'cma_staff', 'system', 'api_client'] |
| timestamp | Timestamp | Yes | When it occurred (UTC, ms) | Indexed, not null |
| resource_type | String(100) | Yes | What was affected | |
| resource_id | UUID | Yes | Specific resource | Indexed |
| action | String(100) | Yes | What was done | |
| result | Enum | Yes | Outcome | ['success', 'failure', 'warning'] |
| details | JSON | No | Additional context | |
| source_ip | String(45) | Yes | Source IP address | |
| integrity_hash | String(64) | Yes | SHA-256 chain hash | Tamper evidence |

**Data Classification**: OFFICIAL — SENSITIVE

**Data Retention**: 7 years (immutable, append-only storage)

---

### Data Quality Requirements

**Data Accuracy**: Fuel prices validated against configurable plausible range (default: 50.0–500.0 PPL). Prices outside range accepted with warning flag. Anomaly detection for >20% price change within 24 hours.

**Data Completeness**: All fuel types listed for a forecourt must have prices submitted. Missing fuel type prices generate compliance warning.

**Data Consistency**: Forecourt must exist and be 'active' for submissions to be accepted. Organisation must be 'active' for any associated forecourt submission.

**Data Timeliness**: Target freshness SLA: ≤30 minutes from submission to publication. Stale threshold: >24 hours since last update triggers staleness indicator in published data and compliance monitoring alert.

**Data Lineage**: Every published price traces to a specific PriceSubmission, which traces to a specific submitter, channel, and timestamp. Full chain preserved in audit events.

---

### Data Migration Requirements

**Migration Scope**: No legacy system migration required — this is a new service. Initial data load required for:
- Forecourt master list: Import known forecourt locations from BEIS/DESNZ register or equivalent authoritative source
- Geographic data: OS postcode-to-coordinate mapping for search functionality

**Migration Strategy**: Phased — seed forecourt register before registration deadline; retailers verify and update during registration.

**Data Validation**: Cross-reference imported forecourt list against retailer registrations; flag discrepancies for investigation.

---

## Constraints and Assumptions

### Technical Constraints

**TC-1**: All data MUST be stored and processed within UK sovereign cloud regions (Principle 8: Data Sovereignty)

**TC-2**: The citizen-facing service MUST be hosted on GOV.UK infrastructure or integrate with the GOV.UK domain

**TC-3**: All citizen-facing pages MUST use the GOV.UK Design System

**TC-4**: The service MUST operate at OFFICIAL classification (no SECRET or TOP SECRET data)

**TC-5**: Source code MUST be open source unless a specific security exemption is granted (GDS Service Standard Point 12)

---

### Business Constraints

**BC-1**: Forecourt registration deadline is 2 February 2026 — this is set in legislation and cannot move

**BC-2**: CMA enforcement grace period ends early May 2026 — enforcement tools must be operational by this date

**BC-3**: Programme budget is defined in the approved business case (specific figures subject to Green Book assessment)

**BC-4**: The service must pass GDS Service Standard assessment at each phase gate before progressing

**BC-5**: Cross-departmental governance: CMA delivers the digital service; DESNZ owns the policy and regulations; both must agree on scope changes

---

### Assumptions

**A-1**: BEIS/DESNZ maintains an authoritative list of UK fuel forecourts that can be used to seed the forecourt register

**A-2**: GOV.UK Notify has sufficient capacity for the notification volumes required (~50,000 emails/month during onboarding)

**A-3**: Large retail chains (supermarkets, oil companies) have IT capability to integrate via API within 3 months of API specification publication

**A-4**: Independent retailers have at minimum a smartphone with web browser capability for manual price submission

**A-5**: The Motor Fuel Price (Open Data) Regulations 2025 will not be significantly amended during initial delivery

**A-6**: CMA and DESNZ will maintain joint governance arrangements and resolve inter-departmental disagreements through the programme board

**Validation Plan**: Assumptions A-1, A-3, and A-4 to be validated during Discovery/Alpha through user research and data audit. A-2 validated through GOV.UK Notify capacity planning engagement.

---

## Success Criteria and KPIs

### Business Success Metrics

| Metric | Baseline | Target | Timeline | Measurement Method |
|--------|----------|--------|----------|-------------------|
| Forecourt registration rate | 0 | ≥97% of known forecourts | By 2 Feb 2026 | Registration count vs forecourt master list |
| Submission compliance rate | 0% | ≥90% (grace period end); ≥95% (6 months later) | May 2026 / Nov 2026 | Compliance dashboard |
| Monthly unique citizen users | 0 | 1,000,000 | 12 months post-launch | GOV.UK analytics |
| User satisfaction | N/A | ≥80% | Public Beta onwards | GOV.UK satisfaction survey |
| Third-party API integrations | 0 | ≥10 | 12 months post-API launch | API consumer registration |
| Programme spend vs budget | Approved budget | Within ±10% | Ongoing | Financial reporting |

### Technical Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Citizen search availability | 99.9% | Uptime monitoring |
| Retailer submission API availability | 99.95% | Uptime monitoring |
| Citizen search response time (p95) | <3 seconds | RUM / synthetic monitoring |
| Open data API response time (p95) | <500ms | APM tooling |
| Data freshness (p95) | ≤30 minutes submission-to-publication | Pipeline metrics |
| Error rate (citizen search) | <0.1% | Log aggregation |
| Non-compliance detection time | <24 hours | Compliance monitoring |
| Deployment frequency | ≥Weekly | CI/CD metrics |
| Mean time to recovery (MTTR) | <1 hour | Incident tracking |

### User Adoption Metrics

| Metric | Target | Timeline | Measurement Method |
|--------|--------|----------|-------------------|
| Citizen monthly active users | 1,000,000 | 12 months | GOV.UK analytics |
| Task completion rate (find fuel price) | ≥95% | Public Beta | User research |
| Accessibility audit pass | WCAG 2.2 AA | Each phase gate | Automated + manual audit |
| Retailer satisfaction with submission process | ≥70% | 6 months post-launch | Survey |
| GDS Service Standard assessment | Pass | Each phase gate | GDS assessment panel |

---

## Dependencies and Risks

### Dependencies

| Dependency | Description | Owner | Target Date | Status | Impact if Delayed |
|------------|-------------|-------|-------------|--------|-------------------|
| Forecourt master list | Authoritative list of UK forecourts from BEIS/DESNZ | DESNZ | Jan 2026 | At Risk | HIGH — cannot measure registration completeness |
| GOV.UK Notify capacity | Confirm Notify can handle onboarding email volumes | GDS Notify team | Jan 2026 | On Track | MEDIUM — alternative notification needed |
| CMA Identity Provider | SAML/OIDC federation for CMA staff SSO | CMA IT | Feb 2026 | On Track | MEDIUM — fallback to standalone auth |
| GDS pre-assessment | Early engagement with GDS assessment team | GDS | Feb 2026 | On Track | MEDIUM — assessment risk |
| OS AddressBase licence | Licence for address gazetteer data | CMA Procurement | Jan 2026 | On Track | HIGH — address validation degraded |
| CMA Legal guidance | Evidence admissibility requirements for enforcement | CMA Legal | Mar 2026 | On Track | HIGH — audit trail design affected |

### Risks

| Risk ID | Description | Probability | Impact | Mitigation Strategy | Owner |
|---------|-------------|-------------|--------|---------------------|-------|
| R-1 | Low independent retailer registration and compliance | HIGH | HIGH | PRA partnership, assisted digital, grace period support | CMA SRO |
| R-2 | Data quality too low for citizen trust | MEDIUM | HIGH | Automated validation, anomaly detection, staleness indicators | CMA Digital Lead |
| R-3 | Political pressure compromises governance | MEDIUM | HIGH | Clear phase gates, ministerial briefing on governance value | CMA SRO |
| R-4 | GDS Service Standard assessment failure | MEDIUM | HIGH | Pre-assessment check-ins, user research investment | CMA Digital Lead |
| R-5 | Trade body opposition generates negative media | MEDIUM | MEDIUM | Genuine consultation, proportionate enforcement, proactive comms | CMA Comms |
| R-6 | API integration delays for large retailers | MEDIUM | MEDIUM | Early API spec publication, sandbox environment, technical support | CMA Digital Lead |
| R-7 | Inter-departmental friction (CMA-DESNZ) | MEDIUM | MEDIUM | Joint programme board, MoU, escalation path | CMA SRO |
| R-8 | Security incident or data breach | LOW | CRITICAL | Secure by Design, pen testing, incident response plan, SIRO review | SIRO |

---

## Requirement Conflicts & Resolutions

### Conflict C-1: Delivery Speed vs Governance Rigour

**Conflicting Requirements**:
- **BR-004**: Enforcement tools operational by May 2026 (fixed regulatory deadline)
- **BR-007 / NFR-C-003**: Must pass GDS Service Standard assessment at each phase gate

**Stakeholders Involved**:
- **DESNZ Ministers (SD-4)**: Want rapid, visible delivery to meet political timelines
- **GDS Assessors (SD-9)**: Require thorough user research and phased delivery evidence

**Nature of Conflict**: Compressed delivery timelines may not allow sufficient user research cycles and governance evidence for GDS assessment. Attempting to skip governance creates assessment failure risk.

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Prioritize speed, defer governance | Meet May 2026 deadline | Risk GDS failure; rework | Ministers satisfied short-term; governance gap |
| **Option 2**: Prioritize governance, extend timeline | Strong GDS evidence | Miss enforcement deadline | GDS satisfied; ministers frustrated |
| **Option 3**: Compress phases, front-load research | Balance both; tight delivery | Team intensity; risk of thin evidence | Both partially satisfied |

**Resolution Strategy**: COMPROMISE (Option 3)

**Decision**: Compress delivery phases but invest heavily in user research from day one. Conduct pre-assessment check-ins with GDS to identify issues early. Accept that Private Beta may run with enforcement tools in basic form, with full capability by May 2026.

**Decision Authority**: CMA SRO (per RACI matrix in ARC-001-STKE-v1.0)

**Impact on Requirements**:
- BR-004 unchanged (May 2026 deadline)
- BR-007 unchanged (must pass assessment)
- Added: user research sprint at start of each phase

**Stakeholder Management**:
- **Ministers**: Communicate phased delivery as responsible governance, not delay. Provide weekly progress metrics.
- **GDS**: Early engagement; pre-assessment check-ins to surface issues before formal panel.

---

### Conflict C-2: Enforcement Rigour vs Retailer Support

**Conflicting Requirements**:
- **FR-006**: Compliance dashboard with automated non-compliance detection (<24h)
- **FR-012**: Technical failure reporting mechanism (distinguishing can't from won't)

**Stakeholders Involved**:
- **CMA Enforcement (SD-2)**: Needs effective detection and evidence for enforcement
- **Independent Retailers (SD-7) / Trade Bodies (SD-8)**: Want supportive approach, proportionate enforcement

**Nature of Conflict**: Aggressive automated enforcement could penalise retailers experiencing genuine technical difficulties. Too-lenient thresholds undermine the scheme.

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Strict automated enforcement | Strong deterrent; high compliance | Unfair to struggling retailers; media backlash | CMA satisfied; retailers alienated |
| **Option 2**: Supportive only, no automation | Good retailer relations | Low compliance; scheme fails | Retailers satisfied; CMA frustrated |
| **Option 3**: Phased escalation with self-service failure reporting | Proportionate; fair; auditable | More complex to build | Both satisfied |

**Resolution Strategy**: PHASE (Option 3)

**Decision**: Build both automated detection (FR-006) and self-service failure reporting (FR-012). During grace period, focus on support. After grace period, escalate proportionately: automated reminders → formal warnings → penalties. Genuine technical failures excluded from non-compliance counts.

**Decision Authority**: CMA Enforcement Lead (per RACI; enforcement approach decisions)

**Impact on Requirements**:
- FR-006 unchanged
- FR-012 confirmed as MUST_HAVE (not SHOULD_HAVE)
- FR-009 (notifications) confirmed as SHOULD_HAVE for compliance reminders

**Stakeholder Management**:
- **Trade Bodies**: Published enforcement approach; regular liaison meetings.
- **CMA Enforcement**: Clear escalation path documented; discretion preserved for edge cases.

---

### Conflict C-3: Data Granularity vs Retailer Commercial Sensitivity

**Conflicting Requirements**:
- **BR-005 / FR-005**: Publish comprehensive real-time fuel price data as open data
- **Implicit retailer concern**: Competitors can see pricing strategy in real time

**Stakeholders Involved**:
- **Citizens (SD-5) / CMA (SD-1)**: Want comprehensive, real-time data
- **Large Retailers (SD-6)**: Concerned about competitive intelligence

**Nature of Conflict**: Real-time publication of all prices enables competitor monitoring. However, prices are already displayed on forecourt price boards and the regulations mandate publication.

**Resolution Strategy**: PRIORITIZE (regulatory requirement takes precedence)

**Decision**: Publish data as required by the Motor Fuel Price (Open Data) Regulations 2025. The regulations define the data scope — the service implements statutory requirements, not additional data. Prices are already publicly visible on forecourt price boards; digital publication does not reveal new information.

**Decision Authority**: DESNZ Policy Lead (regulatory interpretation)

**Impact on Requirements**: No changes — BR-005 and FR-005 stand as written.

**Stakeholder Management**:
- **Large Retailers**: Frame as levelling the playing field. Small independents gain the same visibility that large chains already have through competitive intelligence tools. Regular trade body liaison.

---

### Conflict C-4: Driver Safety vs Feature Richness

**Conflicting Requirements**:
- **FR-014**: Provide optimised in-car API responses with navigation-ready data
- **NFR-U-001**: GOV.UK Design System for citizen-facing service (doesn't apply to in-car platforms)

**Stakeholders Involved**:
- **Citizens/Motorists (SD-5)**: Want in-car fuel search while driving
- **GDS Assessors (SD-9)**: GOV.UK Design System applies to government services

**Nature of Conflict**: Android Auto and Apple CarPlay have their own strict UX guidelines that differ from GOV.UK Design System. A government-built in-car app would need to follow platform guidelines (Google/Apple), not GOV.UK patterns.

**Resolution Strategy**: PHASE

**Decision**: Phase 1 — rely on third-party apps consuming the open data API (no GOV.UK Design System conflict, as third-party apps follow their own UX). Phase 2 (future) — if an official companion app is built, it would follow Android Auto / Apple CarPlay platform guidelines per Google/Apple requirements, with GOV.UK branding where platform permits. GDS assessment would focus on the web service, not the in-car app.

**Decision Authority**: CMA Digital Lead (per RACI; technology architecture decisions)

**Impact on Requirements**: FR-014 and FR-015 are SHOULD_HAVE, not MUST_HAVE. Third-party implementation removes the design system conflict for Phase 1.

---

## Timeline and Milestones

### High-Level Milestones

| Milestone | Description | Target Date | Dependencies |
|-----------|-------------|-------------|--------------|
| Requirements Approval | Stakeholder sign-off on this document | 2026-02-14 | This document |
| Forecourt Registration Deadline | Statutory deadline — all forecourts registered | 2026-02-02 | Registration service operational (FR-001) |
| Alpha Assessment | GDS Service Standard Alpha assessment | 2026-Q2 | User research, prototype |
| Enforcement Grace Period End | CMA may begin formal enforcement | 2026-05 (early) | Enforcement tools operational (FR-006, FR-010) |
| Private Beta | Service available to limited users | 2026-Q3 | Alpha assessment pass |
| Public Beta | Service available to all citizens | 2026-Q3/Q4 | Private Beta assessment pass |
| Live Assessment | GDS Service Standard Live assessment | 2027-Q1 | Public Beta stable, all metrics met |
| First Annual Review | Benefits realisation, NAO readiness | 2027-Q2 | 12 months of live data |

---

## Budget

Budget figures subject to HM Treasury Green Book business case approval. Structure:

### Cost Estimate

| Category | Estimated Cost | Notes |
|----------|----------------|-------|
| Delivery Team (multidisciplinary) | TBD | Per approved business case |
| Cloud Infrastructure | TBD | UK sovereign cloud; auto-scaling |
| GOV.UK Notify | Included | Government shared platform (no additional cost) |
| Address Gazetteer Licence | TBD | OS AddressBase or equivalent |
| Penetration Testing | TBD | CHECK-approved provider; pre-Beta and pre-Live |
| Accessibility Audit | TBD | Manual audit by specialist provider |
| **Total** | **TBD** | **Per approved business case** |

### Ongoing Operational Costs

| Category | Annual Cost | Notes |
|----------|-------------|-------|
| Cloud Infrastructure | TBD | Auto-scaling; pay-per-use |
| Support Team | TBD | 2nd/3rd line support; on-call |
| Address Gazetteer Licence | TBD | Annual renewal |
| Penetration Testing | TBD | Annual re-test |
| **Total** | **TBD/year** | |

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
| Android Auto | Google's in-car platform that projects compatible smartphone apps onto a vehicle's head unit display, enabling voice-controlled and simplified interactions while driving |
| Apple CarPlay | Apple's in-car platform that integrates iPhone apps with a vehicle's built-in display, providing a driver-safe interface with Siri voice control |
| CMA | Competition and Markets Authority — UK competition regulator and Fuel Finder enforcement body |
| DESNZ | Department for Energy Security and Net Zero — policy owner for fuel market regulation |
| Forecourt | A physical fuel retail location (petrol station / filling station) |
| GDS | Government Digital Service — service assessment and standards body |
| Motor Fuel Trader (MFT) | A business operating one or more forecourts that sells motor fuel to the public |
| OGL | Open Government Licence — standard UK Government open data licence |
| PPL | Pence per litre — standard UK unit for fuel pricing |
| TCoP | Technology Code of Practice — mandatory for UK Government technology |
| UPRN | Unique Property Reference Number — OS address identifier |
| WCAG | Web Content Accessibility Guidelines |

### Appendix B: Reference Documents

- ARC-000-PRIN-v1.0 — Enterprise Architecture Principles
- ARC-001-STKE-v1.0 — Stakeholder Drivers & Goals Analysis
- Motor Fuel Price (Open Data) Regulations 2025
- CMA Fuel Finder Enforcement Guidance (December 2025)
- GDS Service Standard (14 points)
- Technology Code of Practice (TCoP)
- GOV.UK Guidance: Fuel Finder (https://www.gov.uk/guidance/fuel-finder)
- GOV.UK Publications: Fuel Finder Enforcement Guidance (https://www.gov.uk/government/publications/fuel-finder-enforcement-guidance)

### Appendix C: Requirements Traceability Matrix

| Req ID | Requirement | Stakeholder Goal | Principle | Priority |
|--------|-------------|-----------------|-----------|----------|
| BR-001 | Universal registration | G-1 | P2, P13 | MUST |
| BR-002 | Data submission compliance | G-2 | P1, P9 | MUST |
| BR-003 | Citizen price comparison | G-3 | P2, P14 | MUST |
| BR-004 | CMA enforcement capability | G-4 | P20, P7 | MUST |
| BR-005 | Open data publication | O-2 | P1, P5 | MUST |
| BR-006 | Value for money | G-5 | P22 | MUST |
| BR-007 | Governance compliance | G-7 | P6, P8, P13, P20, P21 | MUST |
| FR-001 | Forecourt registration | G-1 | P2 | MUST |
| FR-002 | Manual price submission | G-2 | P2 | MUST |
| FR-003 | API price submission | G-2 | P5 | MUST |
| FR-004 | Citizen fuel price search | G-3 | P2, P14 | MUST |
| FR-005 | Open data API | O-2 | P1, P5 | MUST |
| FR-006 | Compliance dashboard | G-4 | P20, P7 | MUST |
| FR-007 | Data validation pipeline | G-2 | P9 | MUST |
| FR-008 | Retailer account management | G-1 | P2 | MUST |
| FR-009 | Retailer notifications | G-2, G-4 | P13 | SHOULD |
| FR-010 | Audit trail | G-4 | P20 | MUST |
| FR-011 | Policy analysis | G-5 | P7 | SHOULD |
| FR-012 | Technical failure reporting | G-2, G-4 | P20 | MUST |
| FR-013 | Feedback and support | G-3 | P2 | SHOULD |
| FR-014 | In-car API responses | G-3 | P5, P14 | SHOULD |
| FR-015 | In-car dev guidelines | O-2 | P1, P5 | SHOULD |
| NFR-P-001 | Citizen search performance | G-3 | P14 | MUST |
| NFR-P-002 | Ingestion throughput | G-2 | P3, P9 | MUST |
| NFR-P-003 | Dashboard performance | G-4 | P14 | SHOULD |
| NFR-A-001 | Service availability | G-2, G-3 | P15 | MUST |
| NFR-A-002 | Disaster recovery | G-2 | P4, P15 | MUST |
| NFR-A-003 | Fault tolerance | G-2, G-3 | P4 | MUST |
| NFR-S-001 | Horizontal scaling | G-3 | P3 | MUST |
| NFR-S-002 | Data volume scaling | G-2 | P3 | MUST |
| NFR-SEC-001 | Authentication | G-7 | P6 | MUST |
| NFR-SEC-002 | Authorisation | G-7 | P6 | MUST |
| NFR-SEC-003 | Encryption | G-7 | P6 | MUST |
| NFR-SEC-004 | Secrets management | G-7 | P6 | MUST |
| NFR-SEC-005 | Vulnerability management | G-7 | P6 | MUST |
| NFR-C-001 | UK GDPR compliance | G-6 | P8, P21 | MUST |
| NFR-C-002 | Audit logging | G-4 | P20 | MUST |
| NFR-C-003 | GDS Service Standard | G-7 | P2 | MUST |
| NFR-C-004 | TCoP compliance | G-7 | P13 | MUST |
| NFR-C-005 | Secure by Design | G-7 | P6 | MUST |
| NFR-U-001 | Citizen UX | G-3 | P2 | MUST |
| NFR-U-002 | Accessibility | G-3 | P2 | MUST |
| NFR-U-003 | Localisation | G-3 | P2 | EN: MUST; CY: SHOULD |
| NFR-M-001 | Observability | G-2, G-4 | P7 | MUST |
| NFR-M-002 | Documentation | G-7 | P16 | MUST |
| NFR-M-003 | Runbooks | G-7 | P7 | MUST |
| NFR-I-001 | API standards | G-3 | P5 | MUST |
| NFR-I-002 | Open standards | G-7 | P1, P5 | MUST |
| NFR-I-003 | Data portability | O-2 | P1 | MUST |
| INT-001 | Address gazetteer | G-1 | P5 | MUST |
| INT-002 | Geocoding service | G-1, G-3 | P5 | MUST |
| INT-003 | GOV.UK Notify | G-2, G-4 | P13 | MUST |
| INT-004 | GOV.UK Design System | G-3 | P2, P13 | MUST |
| INT-005 | GOV.UK One Login | Future | P13 | COULD |
| INT-006 | CMA Identity Provider | G-4 | P6 | MUST |
| INT-007 | Companies House API | G-1 | P5 | SHOULD |
| INT-008 | Android Auto / CarPlay | G-3, O-2 | P5 | SHOULD |
| DR-001–006 | Data entities (6 defined) | G-1, G-2, G-4 | P8, P9, P10 | MUST |

---

**Generated by**: ArcKit `/arckit.requirements` command
**Generated on**: 2026-01-30 23:30 GMT
**ArcKit Version**: 1.0.3
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: claude-opus-4-5-20251101
**Generation Context**: Requirements v2.0 — added Android Auto / Apple CarPlay in-car use case (UC-7), user persona (Mike), functional requirements (FR-014, FR-015), and integration requirement (INT-008). Source documents: ARC-000-PRIN-v1.0, ARC-001-STKE-v1.0, ARC-001-DATA-v1.0, ARC-001-RSCH-v1.0.
