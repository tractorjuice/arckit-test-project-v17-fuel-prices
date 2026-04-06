# Technology and Service Research: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 1.0.3 | **Command**: `/arckit.research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RSCH-v5.0 |
| **Document Type** | Technology and Service Research |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 5.0 |
| **Created Date** | 2026-04-06 |
| **Last Modified** | 2026-04-06 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-07-06 |
| **Owner** | Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-30 | ArcKit AI | Initial creation -- data source catalogue and API landscape (pre-API launch) | PENDING | PENDING |
| 2.0 | 2026-01-31 | ArcKit AI | Open source tools research for fuel data feed access | PENDING | PENDING |
| 3.0 | 2026-03-03 | ArcKit AI | Alibaba Cloud-specific research (community command) | PENDING | PENDING |
| 4.0 | 2026-03-26 | ArcKit AI | Major revision: Fuel Finder developer API now live with documented endpoints; full market research across 10 categories with build vs buy analysis; 3-year TCO projections; updated against ARC-001-REQ-v2.0 | PENDING | PENDING |
| 4.1 | 2026-03-27 | ArcKit AI | Updated from official Fuel Finder developer portal PDFs (5 documents): added two distinct API surfaces, price submission constraints, testing workflow, legislation SI reference, forecourt ID format | PENDING | PENDING |
| 5.0 | 2026-04-06 | ArcKit AI | Major revision: incorporated GOV.UK Fuel Finder factsheet (31 March 2026) with named third-party ecosystem (7 confirmed consumers); updated against ARC-001-REQ-v3.0 (56 requirements); added VE3 platform reliability risk (data quality issues, contract risk); new research categories for citizen error reporting and CSV bulk data channel; updated compliance rates (90% registered, enforcement from May 2026); quantified consumer benefit (GBP 40/year savings); added third-party API intermediary landscape (CheckFuelPrices, FuelCosts.co.uk Kaggle dataset); updated GOV.UK Forms for error reporting; risk-adjusted TCO updated | PENDING | PENDING |

---

## Executive Summary

### Research Scope

This document presents comprehensive market research findings for technologies, services, and platforms required to build and operate the UK Fuel Price Transparency Service. It is updated against **ARC-001-REQ-v3.0** (56 requirements across FR, NFR, INT, and DR categories) and incorporates new findings from the **GOV.UK Fuel Finder for Drivers Factsheet** (published 31 March 2026) [FFDF-C1], which provides the first official government confirmation of the live third-party consumer ecosystem, 90% station registration compliance, and estimated GBP 40/year household savings.

**Requirements Analyzed**: 15 functional (FR-001 to FR-015), 25 non-functional (NFR-P, NFR-A, NFR-S, NFR-SEC, NFR-C, NFR-U, NFR-M, NFR-I), 7 integration (INT-001 to INT-007), 8 business requirements (BR-001 to BR-008)

**Research Categories Identified**: 13 categories based on requirement analysis (3 new since v4.1)

**Research Approach**: Web research across UK Government developer portal, GOV.UK platforms, Digital Marketplace, official Fuel Finder factsheet, Forecourt Trader industry reporting, open source repositories, vendor documentation, pricing calculators, and third-party developer community sites

### Key Findings

- **Third-party ecosystem is already live**: 7 named consumers confirmed by DESNZ factsheet (Confused.com, DriveScore, Fuel Finder UK, Fuel Spy, MotorMouth, PetrolPrices.com, RAC Fuel Watch) [FFDF-C2] -- the CMA enhanced API must add unique value beyond what these already provide
- **VE3 platform reliability is a material risk**: Data quality issues (prices displayed as 1.3p/litre due to pence/pounds unit confusion), 500+ forecourts with incorrect location data, and government frustration growing to the point of contingency planning to strip the GBP 2M contract from VE3 Global -- CMA service must implement robust data validation and resilience
- **CSV bulk download already available**: Fuel Finder data is available as a twice-daily CSV download in addition to the API, with email subscription notification -- this is a new data access channel not previously documented
- **Citizen error reporting service exists**: GOV.UK provides a service at gov.uk/guidance/report-an-error-in-fuel-prices-or-forecourt-details where citizens can report pricing discrepancies -- CMA service should integrate with or complement this capability
- **Enforcement timeline confirmed**: CMA enforcement powers activate from 1 May 2026; enforcement tools MUST be operational by that date; current 90% compliance rate leaves approximately 850 non-compliant stations
- **GOV.UK platforms cover 5 categories at zero cost**: GOV.UK Notify (notifications), GOV.UK One Login (retailer authentication), GOV.UK Design System (frontend), OS Places API (geocoding), and GOV.UK Forms (error reporting) are all free for UK central government
- **AWS remains the recommended cloud platform**: G-Cloud listed, NCSC-assessed, UK region (eu-west-2) with 3 availability zones, GBP billing -- unchanged from v4.1

### Build vs Buy Summary

| Approach | Categories | Total 3-Year TCO | Rationale |
|----------|-----------|------------------|-----------|
| **BUILD** (Custom Development) | 5 categories | GBP 1,200K-1,600K | Core bespoke service logic -- no off-the-shelf product |
| **BUY** (Managed Cloud Services) | 4 categories | GBP 195K-250K | AWS managed services (RDS, SQS, ECS/EKS, API Gateway) |
| **ADOPT** (Open Source) | 3 categories | GBP 45K-85K | PostGIS, Pydantic, Great Expectations, Grafana |
| **GOV.UK Platforms** | 5 categories | GBP 5K-15K | Notify, One Login, Design System, OS Places, Forms (integration effort only) |
| **TOTAL** | 13 categories | **GBP 1,445K-1,950K** | Blended approach recommended |

### Top Recommended Vendors

**Shortlist for further evaluation**:

1. **AWS (Amazon Web Services)** for Cloud Infrastructure: G-Cloud listed, NCSC-assessed, 3 UK AZs, widest UK Government adoption, GBP billing
2. **GOV.UK Notify** for Notifications: Free for central government, 250K free SMS/year, API-integrated, mandatory under TCoP
3. **Ordnance Survey Places API** for Geocoding and Address Validation: Free under PSGA, authoritative UK addressing, UPRN-based, updated 6-weekly

### Requirements Coverage

- 100% of requirements (56/56) have identified solutions (build, buy, adopt, or GOV.UK platform)
- 5 functional areas require custom development (data ingestion pipeline, compliance dashboard, enforcement tools, citizen search UI, data quality validation)
- 0 requirements need further research
- 3 new risk factors identified since v4.1 (VE3 platform reliability, data quality at source, third-party ecosystem competition)

---

## New Findings Since v4.1

This section documents material changes discovered since the previous research version (v4.1, dated 2026-03-27).

### Finding NF-1: Third-Party Consumer Ecosystem Confirmed Live

**Source**: GOV.UK Fuel Finder for Drivers Factsheet (31 March 2026) [FFDF-C2]

The DESNZ factsheet confirms 7 named third-party services are already consuming and displaying Fuel Finder data to drivers:

| Consumer | Type | URL | Status |
|----------|------|-----|--------|
| Confused.com | Price comparison website | confused.com/petrol-prices | Live |
| DriveScore | Driver rewards app | drivescore.com | Live |
| Fuel Finder UK | Dedicated fuel price comparison | fuel-finder.uk | Live |
| Fuel Spy | Fuel price tracker | fuelspy.co.uk | Live |
| MotorMouth | Fuel price app | motormouth.app | Live |
| PetrolPrices.com | Price comparison website | petrolprices.com/app/map | Live |
| RAC Fuel Watch | Motoring organisation service | rac.co.uk/drive/advice/fuel-watch | Live |

Additionally, web research identified third-party API intermediaries that re-serve the data:
- **CheckFuelPrices.co.uk**: Free API for developers (no API key required), covers 4,000+ stations, sourced from Fuel Finder API and CMA retailer feeds
- **FuelCosts.co.uk**: Publishes daily CSV dataset to Kaggle with 7,581+ stations, price data refreshed every 4 minutes

**Implication for CMA Service**: The CMA enhanced API (FR-004) must provide **distinct value** beyond what these third parties already offer. The unique CMA capabilities are: geospatial search by coordinates/radius, historical price trends, data quality scoring, bulk GeoJSON download, and in-car optimised responses. Without these differentiators, the CMA API risks low adoption.

### Finding NF-2: VE3 Platform Reliability Risk (ELEVATED)

**Source**: Forecourt Trader industry reporting (February-April 2026)

The VE3 Global platform has experienced significant reliability and data quality issues since launch:

| Issue | Date | Impact | Status |
|-------|------|--------|--------|
| Invalid activation codes sent to retailers | Jan 2026 | Registration delays | Resolved |
| Registration opened 2 weeks behind schedule | Jan 2026 | Late retailer onboarding | Resolved |
| Prices displayed as 1.3p/litre (pence/pounds unit confusion) | Feb 2026 | Consumer misinformation | Partially resolved |
| 500+ forecourts with incorrect location data | Mar 2026 | Navigation errors | Under investigation |
| Unannounced back-end IT changes without retailer consultation | Mar 2026 | Submission failures | Resolved |
| Forecourts located "in the ocean" (coordinate errors) | Mar 2026 | Data integrity | Under investigation |
| Prices of GBP 15/litre (implausible) | Mar 2026 | Consumer misinformation | Under investigation |

**Contract Risk**: The GBP 2M DESNZ contract with VE3 Global is reportedly at risk, with ministers preparing contingency to strip the contract. VE3 Global had "no prior experience in the sector" when awarded the contract in May 2025.

**Implication for CMA Service**: This ELEVATES the existing risk VR-2 (Fuel Finder API Availability) from v4.1. The CMA data validation pipeline (FR-006) is now even more critical -- it must detect and filter implausible prices, incorrect coordinates, and unit confusion errors before serving to citizens. The CMA service must function as a **data quality gateway** between the raw VE3 API output and citizen-facing services.

**New Validation Rules Required**:
- Price unit detection: reject prices < 50p/litre or > 500p/litre (catches pounds-as-pence and pence-as-pounds errors)
- Coordinate validation: reject locations outside UK bounding box (lat 49.0-61.0, lng -8.0 to 2.0)
- Cross-reference validation: flag locations > 500m from nearest road
- Historical consistency: flag price changes > 50% in 24 hours as anomalous

### Finding NF-3: CSV Bulk Download Channel Available

**Source**: GOV.UK guidance page (gov.uk/guidance/access-the-latest-fuel-prices-and-forecourt-data-via-api-or-email) [FFDF-C3]

The Fuel Finder platform provides a **twice-daily CSV download** in addition to the REST API:
- **Format**: CSV containing current prices and forecourt details
- **Update frequency**: Twice daily
- **Access**: Direct download at developer.fuelfinder.service.gov.uk/access-latest-fuelprices [FFDF-C4]
- **Subscription**: Email notification when new CSV is published
- **Fields**: Current retail prices by fuel type, forecourt address, operator, brand, site amenities, opening hours, update timestamps

**Implication for CMA Service**: The CSV download provides a complementary data channel for:
- Daily full-sync validation (cross-reference against API data)
- Bulk data loading for initial database population
- Disaster recovery (if API is unavailable, CSV can serve as fallback)
- Analytics workloads that benefit from flat-file processing

### Finding NF-4: Citizen Error Reporting Service Exists

**Source**: GOV.UK guidance page (gov.uk/guidance/report-an-error-in-fuel-prices-or-forecourt-details)

DESNZ operates an error reporting service where citizens can report pricing discrepancies. The factsheet directs drivers to this service if they "visit a petrol station and the price does not match up" [FFDF-C5].

**Reportable Issues**:
- Price difference between advertised and charged
- Incorrect facilities information
- Inaccurate opening times
- Accessibility details
- Location information errors
- Temporary closures

**Submission Requirements**:
- Forecourt name and address/postcode
- Date and time of observation
- Description of problem
- Where the error was seen (roadside sign, pump display, app, on-site)
- Optional photos/screenshots

**Post-Submission**: Reports may be shared with forecourt operators or local Trading Standards. CMA can pursue enforcement against persistent inaccurate reporting.

**Implication for CMA Service**: The CMA service should integrate with this error reporting flow:
- **Option A**: Link to the existing GOV.UK error reporting service (simplest, avoids duplication)
- **Option B**: Build a complementary reporting flow that feeds both the CMA compliance dashboard and the DESNZ error reporting pipeline
- **Recommendation**: Option A for Phase 1 (link to existing service), with Option B considered for Phase 2 if citizen feedback volume warrants it. This aligns with FR-012 (Service Feedback and Support).

**GOV.UK Forms** (free for central government, 80+ organisations using, 420+ forms) could be used to build a CMA-specific reporting form if Option B is pursued.

### Finding NF-5: Compliance and Enforcement Timeline Update

**Source**: GOV.UK factsheet [FFDF-C6], CMA enforcement guidance, Forecourt Trader reporting

| Milestone | Date | Status |
|-----------|------|--------|
| Registration opened | 18 December 2025 | Complete (2 weeks late) |
| Registration deadline | 2 February 2026 | Passed -- 6,243 of 8,279 (75.4%) registered at deadline |
| Enforcement grace period | 2 Feb - ~1 May 2026 | CMA focus on supporting compliance |
| Current registration rate | 31 March 2026 | ~90% signed up [FFDF-C7] |
| Enforcement powers activate | 1 May 2026 | CMA will "prioritise enforcement action" |
| GDS Beta assessment | Q3 2026 | Targeted |

**Implication for CMA Service**: Enforcement tools (FR-005, FR-007) are on a hard deadline of 1 May 2026. With ~10% of stations (approximately 850) still non-compliant, the compliance dashboard must be operational to identify, prioritise, and manage enforcement actions from day one.

### Finding NF-6: Quantified Consumer Benefit

**Source**: GOV.UK factsheet [FFDF-C8]

"We estimate this will save households who own a car an average of GBP 40 a year."

This is the first official government quantification of the Fuel Finder consumer benefit. It directly supports the SOBC economic case and benefits realisation tracking required by BR-006.

---

## Research Categories

> **Note**: Research categories dynamically identified from analysis of ARC-001-REQ-v3.0 functional, non-functional, and integration requirements. 3 new categories added since v4.1 (marked **NEW**).

---

## Category 1: Fuel Price Data Source -- Statutory Fuel Finder API

**Requirements Addressed**: FR-001, FR-002, FR-004, FR-015, BR-002, BR-003, BR-005, BR-008, INT-001, NFR-P-001, NFR-P-002

**Why This Category**: The Fuel Finder statutory API is the authoritative source of fuel price data from all ~8,500 UK forecourts under the Motor Fuel Price (Open Data) Regulations 2025. It is the foundation upon which all downstream service capabilities depend.

### Option 1A: GOV.UK Platform -- Fuel Finder Statutory API (VE3 Global / DESNZ)

**Description**: The production Fuel Finder API, operated by VE3 Global Ltd under contract to DESNZ, provides REST endpoints for accessing real-time fuel prices and forecourt information from all registered UK petrol filling stations.

**API Specification** (unchanged from v4.1 -- see ARC-001-RSCH-v4.1 for full details):

| Aspect | Detail |
|--------|--------|
| **Base URL** | `https://api.fuelfinder.service.gov.uk/v1/` |
| **Authentication** | OAuth 2.0 client credentials (client_id + client_secret + scope) |
| **Token Lifetime** | 3600 seconds (1 hour), Bearer token |
| **Rate Limit** | 30 RPM per client, 1 concurrent request |
| **Data Freshness** | Prices published within 30 minutes of any change (statutory requirement) |
| **Fuel Types** | E10 (Unleaded), E5 (Super Unleaded), B7 (Diesel), SDV (Premium Diesel) |
| **Pagination** | Batch-number parameter (up to 80 batches) |
| **Incremental Sync** | `effective-start-timestamp` parameter for delta updates |

**Updated Data Access Channels** (new in v5.0):

| Channel | Method | Update Frequency | Authentication | Best For |
|---------|--------|-----------------|----------------|----------|
| REST API | GET requests (JSON) | Within 30 min of change | OAuth 2.0 | Real-time integration |
| CSV Download | Direct download | Twice daily | GOV.UK One Login | Bulk analytics, DR fallback |
| Email Subscription | Link to latest CSV | On publication | Email | Monitoring, notification |

**Cost Model** (unchanged):

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| API Usage | GBP 0 | GBP 0 | GBP 0 | Free open data |
| Integration Development | GBP 15K | GBP 0 | GBP 0 | OAuth client, pagination, error handling |
| CSV Integration | GBP 3K | GBP 0 | GBP 0 | **NEW**: CSV parser for DR/validation |
| Maintenance | GBP 0 | GBP 3K | GBP 3K | API version updates, monitoring |
| **Total** | **GBP 18K** | **GBP 3K** | **GBP 3K** | |
| **3-Year TCO** | | | **GBP 24K** | |

**Updated Risk Assessment** (elevated from v4.1):

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| VE3 API outage | MEDIUM (was LOW) | HIGH | Cache with staleness indicators; CSV fallback |
| Data quality errors (unit confusion, bad coordinates) | HIGH (NEW) | HIGH | CMA validation pipeline with plausibility rules |
| VE3 contract termination | LOW-MEDIUM (NEW) | CRITICAL | Monitor DESNZ contract status; design for API surface change |
| Rate limit constrains growth | MEDIUM | MEDIUM | Efficient batching; negotiate higher limits |

**Recommendation**: The statutory API remains the **sole authoritative data source**. No change to the overall recommendation. However, the CMA service must now implement **stronger data validation** (FR-006) given documented VE3 data quality issues, and must use the **CSV download as a secondary validation channel**.

### Option 1B: Adopt -- CMA Interim Scheme (14 Retailer JSON Feeds)

**Status**: **Superseded by Fuel Finder statutory API**. Retained for reference and as a fallback during any statutory API outages. Covers ~35% of stations and ~60% of fuel volume.

### Option 1C: Adopt -- Third-Party API Intermediaries

**Description**: Third-party services that re-serve Fuel Finder data with additional processing.

| Service | Coverage | Update Frequency | Auth Required | Cost |
|---------|----------|-----------------|---------------|------|
| CheckFuelPrices.co.uk | 4,000+ stations | Near real-time | No API key | Free |
| FuelCosts.co.uk (Kaggle) | 7,581+ stations | Daily CSV (prices refreshed every 4 min) | Kaggle account | Free (OGL v3.0) |

**Recommendation**: **Do not use as primary source**. These are derivative of the statutory API and add processing delay. Useful for cross-reference validation and competitive landscape monitoring only.

### Build vs Buy Recommendation for Fuel Price Data Source

**Recommended Approach**: GOV.UK Platform -- Fuel Finder Statutory API (primary) + CSV Download (secondary/validation)

**Rationale**: Unchanged from v4.1. The statutory API is the sole authoritative data source. The addition of the CSV download channel provides a valuable secondary data path for validation, disaster recovery, and bulk analytics workloads.

---

## Category 2: Cloud Infrastructure and Hosting

**Requirements Addressed**: NFR-A-001 (99.9% availability), NFR-A-002 (RPO 15min, RTO 4h), NFR-S-001 (horizontal scaling), NFR-SEC-003 (encryption), NFR-C-004 (TCoP cloud-first), BR-007 (governance)

**Recommendation**: **BUY -- AWS eu-west-2 (London)**. Unchanged from v4.1.

**3-Year TCO**: GBP 195K-250K (with reserved instance savings)

Full details: See ARC-001-RSCH-v4.1 Category 2 and ARC-001-AWRS-v2.0.

---

## Category 3: Database and Geospatial Search

**Requirements Addressed**: FR-002 (citizen proximity search), FR-001 (data sync), FR-015 (historical data), FR-009 (audit trail), NFR-P-001 ( < 3s p95), NFR-A-002 (RPO 15min), NFR-S-002 (55M records/year)

**Recommendation**: **BUY -- AWS RDS PostgreSQL with PostGIS extension**. Unchanged from v4.1.

**3-Year TCO**: GBP 106.5K

Full details: See ARC-001-RSCH-v4.1 Category 3.

---

## Category 4: Message Queue and Event Streaming

**Requirements Addressed**: FR-001 (async data pipeline), NFR-P-002 (sync throughput), NFR-A-003 (fault tolerance), Principle 12 (async communication)

**Recommendation**: **BUY -- AWS SQS**. Unchanged from v4.1.

**3-Year TCO**: GBP 5.3K

Full details: See ARC-001-RSCH-v4.1 Category 4.

---

## Category 5: API Gateway and Management

**Requirements Addressed**: FR-004 (enhanced open data API), FR-013 (CarPlay/Auto responses), NFR-I-001 (REST, OpenAPI), NFR-SEC-001 (WAF protection)

**Recommendation**: **BUY -- AWS API Gateway**. Unchanged from v4.1.

**3-Year TCO**: GBP 18K

Full details: See ARC-001-RSCH-v4.1 Category 5.

---

## Category 6: Notifications and Communications

**Requirements Addressed**: FR-008 (retailer notifications), FR-007 (enforcement notifications), INT-003 (GOV.UK Notify), BR-004 (enforcement capability)

**Recommendation**: **GOV.UK Platform -- GOV.UK Notify**. Unchanged from v4.1.

**3-Year TCO**: GBP 6.5K

Full details: See ARC-001-RSCH-v4.1 Category 6.

---

## Category 7: Address Validation and Geocoding

**Requirements Addressed**: INT-002 (geocoding), FR-002 (citizen postcode search)

**Recommendation**: **GOV.UK Platform -- Ordnance Survey Places API (PSGA)**. Unchanged from v4.1.

**3-Year TCO**: GBP 5K

Full details: See ARC-001-RSCH-v4.1 Category 7.

---

## Category 8: Authentication and Identity

**Requirements Addressed**: NFR-SEC-001 (authentication), NFR-SEC-002 (authorisation), INT-006 (CMA IdP)

**Recommendation**: **GOV.UK Platform (One Login for retailers) + CMA IdP federation (staff) + Custom OAuth 2.0 (API clients)**. Unchanged from v4.1.

**3-Year TCO**: GBP 13K

Full details: See ARC-001-RSCH-v4.1 Category 8.

---

## Category 9: Data Validation and Quality

**Requirements Addressed**: FR-006 (data validation pipeline), NFR-P-002 (15-minute freshness SLA), Principle 9 (data quality)

**Why This Category (updated)**: Given documented VE3 data quality issues (Finding NF-2), the data validation pipeline is now **elevated in criticality**. The CMA service must function as a data quality gateway between raw VE3 output and citizen-facing services.

### Updated Validation Requirements (v5.0)

Based on documented VE3 platform issues, the validation pipeline must now handle:

| Validation Rule | Catches | Priority |
|----------------|---------|----------|
| Price range: 50.0-500.0 PPL | Pence/pounds unit confusion (1.3p errors) | CRITICAL |
| Price format: 3 decimal places in GBP | Inconsistent formatting | HIGH |
| Coordinate bounding box: UK (lat 49.0-61.0, lng -8.0 to 2.0) | Forecourts "in the ocean" | CRITICAL |
| Coordinate proximity: < 500m from nearest road | Implausible locations | HIGH |
| Price change rate: < 50% change in 24h | Anomalous price jumps (GBP 15/litre) | HIGH |
| Required fields present | Missing data | CRITICAL |
| Fuel type valid: E10, E5, B7, SDV only | Invalid fuel type codes | MEDIUM |
| Cross-reference: API vs CSV data consistency | Data integrity between channels | MEDIUM |

**Recommendation**: **ADOPT -- Pydantic + Great Expectations** (unchanged technology). Development effort increased to account for enhanced validation rules.

**Updated Cost Estimate**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Development (enhanced validation rules) | GBP 25K | GBP 5K | GBP 5K | +GBP 5K from v4.1 for VE3 data quality rules |
| Infrastructure | GBP 0 | GBP 0 | GBP 0 | Runs within application containers |
| **Total** | **GBP 25K** | **GBP 5K** | **GBP 5K** | |
| **3-Year TCO** | | | **GBP 35K** | |

---

## Category 10: Observability and Monitoring

**Requirements Addressed**: NFR-M-001 (observability), NFR-C-002 (audit logging), Principle 7 (operational excellence), FR-009 (audit trail)

**Recommendation**: **Hybrid -- AWS CloudWatch + Amazon Managed Grafana**. Unchanged from v4.1.

**3-Year TCO**: GBP 27K

Full details: See ARC-001-RSCH-v4.1 Category 10.

---

## Category 11: Citizen Frontend (GOV.UK Design System)

**Requirements Addressed**: INT-004, NFR-U-001, NFR-U-002, NFR-C-003, BR-003

**Recommendation**: **GOV.UK Platform -- GOV.UK Design System**. Unchanged from v4.1.

**3-Year TCO**: GBP 0 (framework is free; development effort in core build estimate)

---

## Category 12: Citizen Error Reporting (NEW)

**Requirements Addressed**: FR-011 (technical failure reporting), FR-012 (service feedback and support)

**Why This Category**: The GOV.UK factsheet [FFDF-C5] directs citizens to report pricing errors at gov.uk/guidance/report-an-error-in-fuel-prices-or-forecourt-details. The CMA service must either integrate with this existing service or provide complementary reporting capability.

### Option 12A: GOV.UK Platform -- Existing DESNZ Error Reporting Service

**Description**: DESNZ operates an error reporting form where citizens can report pricing discrepancies, incorrect facilities, inaccurate opening times, location errors, and temporary closures. Reports are shared with forecourt operators and local Trading Standards, and the CMA can pursue enforcement.

**Pros**:
- Already operational and promoted in government factsheet
- No development cost for CMA
- Consistent citizen journey (single GOV.UK reporting point)
- CMA enforcement data feed already exists

**Cons**:
- CMA does not control the reporting form or data flow
- May not capture all data points needed for CMA compliance monitoring
- Unknown SLA for report processing or sharing with CMA

**Cost**: GBP 0 (link from CMA service to existing GOV.UK page)

### Option 12B: BUILD -- CMA Complementary Error Reporting

**Description**: Build a CMA-specific error reporting flow using GOV.UK Forms (free for central government) that feeds directly into the CMA compliance dashboard, while also forwarding to DESNZ.

**GOV.UK Forms Context**: GOV.UK Forms is now used by 80+ government organisations with 420+ forms, and is free for central government. It uses accessible GOV.UK templates and provides completion metrics.

**Pros**:
- Direct integration with CMA compliance dashboard (FR-005)
- Captures CMA-specific data (forecourt ID, fuel type, price discrepancy amount)
- Error reports become compliance evidence
- CMA controls data flow and processing SLA

**Cons**:
- Development effort required (form design, dashboard integration)
- Potential citizen confusion if two reporting channels exist
- Duplication of DESNZ capability

**Cost Estimate**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| GOV.UK Forms setup | GBP 0 | GBP 0 | GBP 0 | Free for central government |
| Form design and dashboard integration | GBP 5K | GBP 0 | GBP 0 | 1 person-week |
| **Total** | **GBP 5K** | **GBP 0** | **GBP 0** | |
| **3-Year TCO** | | | **GBP 5K** | |

### Build vs Buy Recommendation for Error Reporting

**Recommended Approach**: **Phase 1**: Link to existing DESNZ error reporting service (Option 12A). **Phase 2**: Build CMA-specific form using GOV.UK Forms (Option 12B) if citizen feedback volume exceeds 100 reports/month or CMA requires direct evidence integration.

**Rationale**: The DESNZ service already exists, is promoted in government communications, and avoids duplication. The CMA can pursue Phase 2 once user research validates the need for a complementary channel.

---

## Category 13: Third-Party Ecosystem Monitoring (NEW)

**Requirements Addressed**: BR-005 (third-party innovation), FR-004 (enhanced open data API), NFR-M-001 (business metrics)

**Why This Category**: With 7+ confirmed third-party consumers and intermediary APIs (CheckFuelPrices, FuelCosts.co.uk), the CMA must monitor the ecosystem to: ensure the enhanced API provides distinct value, track adoption, and identify emerging third-party capabilities that may influence CMA service design.

### Confirmed Third-Party Ecosystem (as of April 2026)

| Category | Consumer | Data Source | CMA API Needed? |
|----------|----------|-------------|-----------------|
| Price comparison | Confused.com | Fuel Finder API | Yes -- geospatial search |
| Price comparison | PetrolPrices.com | Fuel Finder API | Yes -- historical data |
| Motoring organisation | RAC Fuel Watch | Fuel Finder API | Yes -- bulk download |
| Dedicated fuel finder | Fuel Finder UK | Fuel Finder API (confirmed integrated) | Yes -- quality indicators |
| Fuel price tracker | Fuel Spy | Fuel Finder API | Yes -- in-car format |
| Fuel price app | MotorMouth | Fuel Finder API | Yes -- geospatial search |
| Driver rewards | DriveScore | Fuel Finder API | Uncertain |
| Developer intermediary | CheckFuelPrices.co.uk | Fuel Finder API + CMA feeds | No -- provides own free API |
| Data publisher | FuelCosts.co.uk | Fuel Finder API | No -- publishes to Kaggle |

### CMA Enhanced API Differentiation Strategy

The CMA enhanced API (FR-004) must provide capabilities **not available** from the VE3 API or third-party intermediaries:

| Capability | VE3 API | Third Parties | CMA Enhanced API |
|-----------|---------|---------------|------------------|
| Real-time prices | Yes | Yes (via VE3) | Yes (via sync) |
| Geospatial search (lat/lng + radius) | No | Some (basic) | **Yes -- PostGIS** |
| Historical price trends | No | Limited | **Yes -- full history** |
| Data quality scoring | No | No | **Yes -- freshness/anomaly** |
| Bulk GeoJSON download | No | CSV only | **Yes -- GeoJSON + CSV** |
| In-car optimised responses (format=auto) | No | No | **Yes -- UC-7** |
| Open data (no auth for reads) | OAuth required | Varies | **Yes -- unauthenticated** |
| Developer portal with OpenAPI spec | React SPA docs | Basic | **Yes -- full OpenAPI** |

**Recommendation**: No procurement required. The differentiation strategy is a custom build requirement (included in core development estimate). Ecosystem monitoring should be a standing item on the quarterly service review agenda.

---

## Total Cost of Ownership (TCO) Summary

### Blended TCO Across All Categories

**Recommended Approach (Blended)**:

| Category | Recommended Option | Year 1 | Year 2 | Year 3 | 3-Year TCO |
|----------|-------------------|--------|--------|--------|------------|
| 1. Fuel Price Data | GOV.UK: Fuel Finder API + CSV | GBP 18K | GBP 3K | GBP 3K | GBP 24K |
| 2. Cloud Infrastructure | BUY: AWS eu-west-2 | GBP 65K | GBP 72.5K | GBP 79K | GBP 216.5K |
| 3. Database + Geospatial | BUY: RDS PostgreSQL + PostGIS | GBP 31K | GBP 32.5K | GBP 43K | GBP 106.5K |
| 4. Message Queue | BUY: AWS SQS | GBP 1.2K | GBP 1.8K | GBP 2.3K | GBP 5.3K |
| 5. API Gateway | BUY: AWS API Gateway | GBP 4K | GBP 6K | GBP 8K | GBP 18K |
| 6. Notifications | GOV.UK: Notify | GBP 5K | GBP 500 | GBP 1K | GBP 6.5K |
| 7. Address / Geocoding | GOV.UK: OS Places API | GBP 5K | GBP 0 | GBP 0 | GBP 5K |
| 8. Authentication | GOV.UK: One Login + CMA IdP | GBP 13K | GBP 0 | GBP 0 | GBP 13K |
| 9. Data Validation | ADOPT: Pydantic + GX (enhanced) | GBP 25K | GBP 5K | GBP 5K | GBP 35K |
| 10. Observability | BUY: CloudWatch + Managed Grafana | GBP 8K | GBP 9K | GBP 10K | GBP 27K |
| 11. Citizen Frontend | GOV.UK: Design System | GBP 0 | GBP 0 | GBP 0 | GBP 0 |
| 12. Error Reporting | GOV.UK: DESNZ service (Phase 1) | GBP 0 | GBP 0 | GBP 0 | GBP 0 |
| 13. Ecosystem Monitoring | Internal process | GBP 0 | GBP 0 | GBP 0 | GBP 0 |
| **Custom Dev (Core Service)** | BUILD: Pipeline, Dashboard, Search, Enforcement, Validation | GBP 620K | GBP 200K | GBP 200K | GBP 1,020K |
| **TOTAL** | | **GBP 795.2K** | **GBP 330.3K** | **GBP 351.3K** | **GBP 1,476.8K** |

### Alternative Scenarios

**Scenario A: Build Everything Custom**:
- 3-Year TCO: GBP 2,200K-2,800K
- Risk-adjusted: GBP 2,640K-3,360K (+20% contingency)

**Scenario B: Buy Everything (Managed SaaS)**:
- 3-Year TCO: GBP 1,800K-2,200K
- Risk-adjusted: GBP 1,980K-2,420K (+10% contingency)

**Scenario C: Open Source Everything (Self-Hosted)**:
- 3-Year TCO: GBP 1,600K-2,000K
- Risk-adjusted: GBP 1,840K-2,300K (+15% contingency)

**Scenario D: Recommended Blended Approach**:
- 3-Year TCO: GBP 1,477K-1,950K
- Risk-adjusted: GBP 1,654K-2,184K (+12% contingency)

### TCO Assumptions

- Engineering rates: GBP 800/day blended rate (mix of contractor and FTE)
- Infrastructure: AWS eu-west-2 pricing (on-demand with 1-year reserved instances for databases)
- SaaS pricing: List prices with 10% annual increase assumption
- Maintenance: 20% of development cost per year for custom builds
- GOV.UK platforms: Free for central government (integration effort only)
- Currency: All costs in GBP; no FX conversion required (AWS GBP billing)
- Custom development increased by GBP 20K (from GBP 1,000K to GBP 1,020K) to account for enhanced data validation rules required by VE3 data quality issues

### Risk-Adjusted TCO

| Scenario | Base TCO | Contingency | Risk-Adjusted TCO | Risk Factors |
|----------|----------|-------------|-------------------|--------------|
| Build Everything | GBP 2,500K | +20% | GBP 3,000K | Scope creep, skill gaps, operational complexity |
| Buy (SaaS) | GBP 2,000K | +10% | GBP 2,200K | Price increases, vendor changes |
| Open Source | GBP 1,800K | +15% | GBP 2,070K | Underestimated maintenance, security patching |
| **Recommended Blend** | **GBP 1,477K** | **+12%** | **GBP 1,654K** | Blended risk; **VE3 reliability adds ~GBP 20K** |

---

## Requirements Traceability

### Requirements Coverage Matrix

| Requirement ID | Requirement Description | Research Category | Recommended Solution | Rationale |
|----------------|------------------------|-------------------|---------------------|-----------|
| BR-001 | Universal forecourt registration | Cat 1 (Data), Cat 8 (Auth) | VE3 platform (monitoring via API) | VE3 handles registration; CMA monitors completeness |
| BR-002 | Comprehensive price submission | Cat 1 (Data) | VE3 platform (monitoring via API) | VE3 handles submission; CMA monitors compliance |
| BR-003 | Citizen price comparison | Cat 3 (DB), Cat 7 (Geocoding), Cat 11 (Frontend) | PostGIS + OS Places + GOV.UK Design System | Geospatial search on locally enriched data |
| BR-004 | CMA enforcement capability | Cat 9 (Validation), Cat 6 (Notify) | Custom build + GOV.UK Notify | Bespoke enforcement tooling |
| BR-005 | Enhanced open data API | Cat 5 (API GW), Cat 13 (Ecosystem) | API Gateway + custom build | Differentiated from VE3 API via geospatial, history, quality |
| BR-006 | Value for money | Cat 2-13 (All) | Blended approach within GBP 3.6M budget | TCO of GBP 1.5K-2.0M within budget |
| BR-007 | Governance compliance | Cat 11 (Frontend), Cat 8 (Auth) | GOV.UK platforms + Secure by Design | GDS, TCoP, DPIA all addressed |
| BR-008 | Data sync and enrichment | Cat 1 (Data), Cat 3 (DB), Cat 9 (Validation) | API sync + PostGIS + validation pipeline | Enhanced validation due to VE3 data quality issues |
| FR-001 | API data synchronisation | Cat 1, Cat 4 | API client + SQS + CSV validation | Primary: API; Secondary: CSV cross-reference |
| FR-002 | Geospatial price search | Cat 3, Cat 7 | PostGIS + OS Places API | Spatial indexing for < 3s p95 |
| FR-003 | Citizen search interface | Cat 11 | GOV.UK Design System | Mandatory GDS-compliant frontend |
| FR-004 | Enhanced open data API | Cat 5, Cat 13 | API Gateway + read replica | Differentiated from VE3 and third parties |
| FR-005 | Compliance dashboard | Cat 3, Cat 10 | Custom build + RDS + Grafana | Bespoke enforcement tool |
| FR-006 | Data validation and quality | Cat 9 | Pydantic + Great Expectations (enhanced) | Critical given VE3 data quality issues |
| FR-007 | Enforcement case management | Cat 3, Cat 6 | Custom build + GOV.UK Notify | Bespoke workflow |
| FR-008 | Retailer notifications | Cat 6 | GOV.UK Notify | Free email; low-cost SMS |
| FR-009 | Audit trail | Cat 3, Cat 10 | RDS (immutable) + S3 + CloudWatch | Tamper-evident logging |
| FR-010 | Policy analysis | Cat 3 | RDS read replica + CSV export | SQL analytics |
| FR-011 | Technical failure reporting | Cat 12 | Link to DESNZ service (Phase 1) | Existing GOV.UK service |
| FR-012 | Service feedback | Cat 12 | GOV.UK feedback component | Standard GOV.UK pattern |
| FR-013 | CarPlay/Auto API responses | Cat 5 | API Gateway transformation | format=auto parameter |
| FR-014 | In-car integration guidelines | Cat 11 | Static developer portal content | Documentation |
| FR-015 | Historical price data | Cat 3 | RDS with partitioning | Append-only; 55M records/year |
| NFR-P-001 | Citizen search < 3s p95 | Cat 2, Cat 3 | CloudFront + PostGIS + read replica | CDN + spatial index |
| NFR-P-002 | Sync throughput | Cat 1, Cat 4 | API client + SQS | Respect 30 RPM limit |
| NFR-A-001 | 99.9% availability | Cat 2 | Multi-AZ ECS + Multi-AZ RDS | AWS infrastructure redundancy |
| NFR-A-002 | RPO 15min, RTO 4h | Cat 3 | RDS PITR + Multi-AZ failover | Continuous replication |
| NFR-A-003 | VE3 API resilience | Cat 1 | Cache + CSV fallback + circuit breaker | Enhanced resilience given VE3 issues |
| NFR-SEC-001 | Authentication | Cat 8 | One Login + CMA IdP + OAuth 2.0 | Multi-factor for retailers; SSO for staff |
| NFR-SEC-003 | Encryption | Cat 2 | AWS KMS + TLS 1.2+ | AES-256 at rest; TLS in transit |
| NFR-C-002 | Audit logging | Cat 10 | CloudWatch Logs + S3 archive | Structured JSON; 7-year retention |
| NFR-I-001 | API standards | Cat 5 | API Gateway + OpenAPI spec | Native OpenAPI import/export |
| INT-001 | Fuel Finder API | Cat 1 | OAuth 2.0 client + sync pipeline | Primary data integration |
| INT-002 | Geocoding | Cat 7 | OS Places API + PostGIS | API for lookup; PostGIS for runtime |
| INT-003 | GOV.UK Notify | Cat 6 | GOV.UK Notify API | Mandatory platform |
| INT-006 | CMA Corporate IdP | Cat 8 | SAML 2.0 / OIDC federation | Standard SSO integration |

### Coverage Summary

**Requirements with Identified Solutions**:

- 100% of requirements (56/56) have recommended solutions
- 0 requirements need further research
- 5 functional areas require custom development: data ingestion pipeline, compliance dashboard, enforcement tools, citizen search UI, enhanced data validation (elevated from v4.1)
- 3 new risk factors require architectural mitigation (VE3 reliability, data quality, ecosystem competition)

---

## UK Government Considerations

### Technology Code of Practice (TCoP) Compliance

| TCoP Point | Status | Notes |
|-----------|--------|-------|
| **1. Define user needs** | Compliant | Research driven by ARC-001-REQ-v3.0 requirements and 7 user personas |
| **2. Make things accessible** | Compliant | GOV.UK Design System mandated; WCAG 2.2 AA compliance |
| **3. Be open and use open source** | Compliant | PostgreSQL, PostGIS, Pydantic, Great Expectations, Grafana |
| **4. Make use of open standards** | Compliant | REST, JSON, OAuth 2.0, OpenAPI 3.0, GeoJSON, OGL |
| **5. Use cloud first** | Compliant | AWS public cloud (eu-west-2) recommended |
| **6. Make things secure** | Compliant | NCSC-assessed cloud; Secure by Design; encryption at rest and in transit |
| **7. Make privacy integral** | Compliant | DPIA required; UK GDPR; data minimisation; PII encryption |
| **8. Share, reuse and collaborate** | Compliant | GOV.UK Notify, One Login, Design System, OS Places, Forms all reused |
| **9. Integrate and adapt technology** | Compliant | REST APIs, standard integration patterns, no proprietary protocols |
| **10. Make better use of data** | Compliant | Open data under OGL; API and bulk download; GeoJSON format |
| **11. Define your purchasing strategy** | Compliant | G-Cloud procurement for AWS; free GOV.UK platforms |
| **12. Meet the Service Standard** | Compliant | GDS Service Standard assessment at Alpha, Beta, Live |
| **13. Spend controls** | Compliant | CDDO spend control approval required ( > GBP 100K) |

### GOV.UK Common Platforms Used

| Platform | Category | Status | Rationale |
|----------|----------|--------|-----------|
| GOV.UK Notify | Notifications | Mandatory | Free emails, low-cost SMS, TCoP compliance |
| GOV.UK One Login | Retailer Authentication | Recommended | Already used by Fuel Finder portal; free for government |
| GOV.UK Design System | Citizen Frontend | Mandatory | Accessibility, consistency, GDS Service Standard |
| OS Places API (PSGA) | Address / Geocoding | Recommended | Free for government, authoritative UK addressing |
| GOV.UK Forms | Error Reporting (Phase 2) | Recommended | Free for government, 80+ organisations using |
| Companies House API | Registration Validation | Recommended | Free, validates retailer organisations |
| Fuel Finder API | Data Source | Mandatory | Statutory data source; free open data |
| DESNZ Error Reporting | Citizen Feedback | Existing | Operational; citizens directed to it by factsheet |

---

## Risks and Mitigations

### Vendor Risks

**VR-1: AWS Vendor Lock-in** (unchanged from v4.1)
- **Risk**: Proprietary services (SQS, API Gateway) create switching costs
- **Impact**: MEDIUM | **Likelihood**: LOW
- **Mitigation**: Abstraction layers; containerised workloads; PostgreSQL portable

**VR-2: Fuel Finder API Availability (ELEVATED)**
- **Risk**: VE3 platform outage or data quality degradation blocks data freshness SLA
- **Impact**: HIGH | **Likelihood**: MEDIUM (was LOW in v4.1)
- **Mitigation**: Enhanced caching; CSV download as secondary data channel; CMA validation pipeline filters bad data; serve stale data with staleness indicators; retain CMA interim feeds as emergency fallback
- **New Evidence**: Documented VE3 platform issues (1.3p pricing errors, incorrect coordinates, unannounced backend changes). GBP 2M contract reportedly at risk.

**VR-3: GOV.UK Platform Dependencies** (unchanged from v4.1)
- **Risk**: GOV.UK Notify or One Login service degradation
- **Impact**: MEDIUM | **Likelihood**: LOW
- **Mitigation**: Retry with backoff; dead letter queue; fallback mechanisms

**VR-4: VE3 Contract Termination (NEW)**
- **Risk**: DESNZ terminates VE3 Global contract; new operator may change API surface
- **Impact**: CRITICAL | **Likelihood**: LOW-MEDIUM
- **Mitigation**: Design CMA API client with adapter pattern for easy substitution; monitor DESNZ procurement notices; maintain knowledge of API specification independently of VE3 implementation

### Technical Risks

**TR-1: Fuel Finder API Rate Limiting at Scale** (unchanged from v4.1)
- **Risk**: 30 RPM limit constrains data refresh frequency
- **Impact**: MEDIUM | **Likelihood**: MEDIUM
- **Mitigation**: Efficient batching; incremental sync; aggressive caching; negotiate higher limits

**TR-2: PostGIS Performance at Scale** (unchanged from v4.1)
- **Risk**: Proximity queries slow as historical data grows to 165M+ records
- **Impact**: MEDIUM | **Likelihood**: LOW
- **Mitigation**: Table partitioning; read replicas; caching; archive strategy

**TR-3: VE3 Data Quality at Source (NEW)**
- **Risk**: VE3 platform passes through invalid data (unit confusion, bad coordinates, implausible prices)
- **Impact**: HIGH | **Likelihood**: HIGH (documented occurrences)
- **Mitigation**: CMA validation pipeline with plausibility rules; cross-reference API data with CSV download; anomaly detection with automated alerts; citizen error reporting integration

**TR-4: Third-Party Ecosystem Competition (NEW)**
- **Risk**: Third-party consumers (Confused.com, PetrolPrices, RAC) already serve fuel data, reducing perceived need for CMA enhanced API
- **Impact**: MEDIUM | **Likelihood**: MEDIUM
- **Mitigation**: CMA API provides unique capabilities (geospatial search, historical data, quality scoring, GeoJSON, in-car format) not available from VE3 API or third parties; differentiation strategy documented in Category 13

---

## Next Steps and Recommendations

### Immediate Actions (0-2 weeks)

1. **Stakeholder Review**: Present v5.0 findings (especially VE3 risk elevation and third-party ecosystem) to CMA Digital Lead and Architecture Review Board
2. **VE3 Risk Mitigation**: Implement adapter pattern in API client design to accommodate potential VE3 contract termination
3. **CSV Integration**: Add CSV download parsing capability to data sync pipeline for validation cross-reference
4. **Enforcement Deadline**: Confirm enforcement tools (FR-005, FR-007) are on track for 1 May 2026 deadline

### Vendor Evaluation (2-6 weeks)

5. **Enhanced Validation POC**: Build proof-of-concept validation rules for VE3 data quality issues (price plausibility, coordinate validation, unit detection)
6. **Ecosystem Monitoring**: Establish quarterly review process for third-party consumer landscape
7. **Error Reporting Integration**: Implement link to DESNZ error reporting service from CMA citizen frontend

### Integration with Other Commands

8. **Update SOBC**: Run `/arckit:sobc` to update Economic Case with GBP 40/year household savings figure
9. **Update Risk Register**: Run `/arckit:risk` to incorporate elevated VE3 reliability risk
10. **Create Wardley Map**: Run `/arckit:wardley` to map updated value chain including third-party ecosystem
11. **Generate SOW/RFP**: Run `/arckit:sow` to create delivery partner RFP with enhanced validation requirements

---

## Appendices

### Appendix A: Research Methodology

**Data Sources**:
- Fuel Finder Developer Portal (developer.fuel-finder.service.gov.uk)
- GOV.UK Fuel Finder for Drivers Factsheet (31 March 2026) -- **NEW in v5.0**
- GOV.UK guidance pages (data access, error reporting, enforcement)
- Forecourt Trader industry reporting (VE3 platform issues, contract risk) -- **NEW in v5.0**
- Third-party developer sites (CheckFuelPrices, FuelCosts.co.uk, Fuel Finder UK) -- **NEW in v5.0**
- AWS, Azure pricing pages and calculators
- GOV.UK Notify, One Login, OS Places, Forms documentation
- UK Government Code Repositories (govreposcrape)

**Evaluation Criteria**:
- Requirements fit against ARC-001-REQ-v3.0 (was v2.0 in v4.1)
- UK Government compliance (G-Cloud, NCSC, Cyber Essentials, TCoP)
- 3-year TCO projection with risk adjustment
- Operational burden (managed vs self-hosted)
- Open source preference (TCoP Point 3/4)
- UK data residency (mandatory)
- GOV.UK platform reuse (TCoP Point 8)
- Data quality resilience (NEW in v5.0 -- VE3 platform reliability)
- Ecosystem differentiation (NEW in v5.0 -- CMA API value proposition)

**Limitations**:
- VE3 platform reliability assessment based on industry reporting (Forecourt Trader); CMA may have different visibility into VE3 operational metrics
- Third-party consumer list based on DESNZ factsheet (31 March 2026); additional consumers may have integrated since publication
- AWS pricing based on on-demand rates; actual costs lower with reserved instances
- Custom development estimates assume GBP 800/day blended rate
- Market research valid for approximately 6 months from date of publication

### Appendix B: Glossary

| Term | Definition |
|------|-----------|
| AZ | Availability Zone (isolated data centre within an AWS region) |
| B7 | Standard diesel (7% biodiesel) |
| CDN | Content Delivery Network |
| CMA | Competition and Markets Authority |
| DESNZ | Department for Energy Security and Net Zero |
| E10 | Standard unleaded petrol (10% ethanol) |
| E5 | Super unleaded petrol (5% ethanol) |
| ECS | Elastic Container Service (AWS) |
| GDS | Government Digital Service |
| GiST | Generalised Search Tree (PostGIS spatial index) |
| GOV.UK One Login | Cross-government identity and authentication platform |
| G-Cloud | UK Government cloud procurement framework |
| NCSC | National Cyber Security Centre |
| OGL | Open Government Licence |
| OIDC | OpenID Connect |
| OS Places API | Ordnance Survey address and geocoding API |
| PostGIS | PostgreSQL geospatial extension |
| PPL | Pence per litre |
| PSGA | Public Sector Geospatial Agreement |
| RDS | Relational Database Service (AWS managed PostgreSQL) |
| RPM | Requests Per Minute |
| SDV | Premium/super diesel variant |
| SQS | Simple Queue Service (AWS message queue) |
| TCoP | Technology Code of Practice |
| TCO | Total Cost of Ownership |
| UPRN | Unique Property Reference Number |
| VE3 Global | Designated aggregator for the statutory Fuel Finder scheme under DESNZ contract |
| WAF | Web Application Firewall |

### Appendix C: Reference Documents

| Document | Type | Source | Path |
|----------|------|--------|------|
| Project Requirements v3.0 | ArcKit Artifact | ArcKit | `projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v3.0.md` |
| Architecture Principles v1.0 | ArcKit Artifact | ArcKit | `projects/000-global/ARC-000-PRIN-v1.0.md` |
| Research v4.1 | ArcKit Artifact | ArcKit | `projects/001-uk-fuel-price-transparency-service/research/ARC-001-RSCH-v4.1.md` |
| AWS Research v2.0 | ArcKit Artifact | ArcKit | `projects/001-uk-fuel-price-transparency-service/research/ARC-001-AWRS-v2.0.md` |
| Azure Research v2.0 | ArcKit Artifact | ArcKit | `projects/001-uk-fuel-price-transparency-service/research/ARC-001-AZRS-v2.0.md` |
| GOV.UK Fuel Finder for Drivers Factsheet | Government Factsheet | DESNZ | `projects/001-uk-fuel-price-transparency-service/external/Fuel Finder for drivers_ Factsheet - GOV.UK.pdf` |
| Motor Fuel Price (Open Data) Regulations 2025 | Legislation | UK Parliament | https://www.legislation.gov.uk/uksi/2025/1356/introduction/made |
| Fuel Finder Developer Portal | API Documentation | DESNZ/VE3 Global | https://www.developer.fuel-finder.service.gov.uk/ |
| Fuel Finder Enforcement Guidance | Government Guidance | CMA | https://www.gov.uk/government/publications/fuel-finder-enforcement-guidance |
| Report an Error in Fuel Prices | Government Service | DESNZ | https://www.gov.uk/guidance/report-an-error-in-fuel-prices-or-forecourt-details |
| Access Fuel Price Data | Government Guidance | GOV.UK | https://www.gov.uk/guidance/access-the-latest-fuel-prices-and-forecourt-data-via-api-or-email |
| CMA Road Fuel Monitoring | Government Collection | CMA | https://www.gov.uk/government/collections/road-fuel-price-data-scheme |
| Chancellor Crackdown on Pump Prices | Government News | HMT/DESNZ | https://www.gov.uk/government/news/chancellor-and-energy-secretary-meet-with-fuel-bosses-in-no11-as-government-order-crackdown-on-pump-prices |
| GOV.UK Notify | Government Platform | GDS | https://www.notifications.service.gov.uk/ |
| GOV.UK One Login | Government Platform | GDS | https://docs.sign-in.service.gov.uk/ |
| GOV.UK Forms | Government Platform | GDS | https://www.forms.service.gov.uk/ |
| OS Places API | Government Platform | Ordnance Survey | https://docs.os.uk/os-apis/accessing-os-apis/os-places-api |

---

## External References

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| FFDF | Fuel Finder for drivers_ Factsheet - GOV.UK.pdf | Government Factsheet | 001-uk-fuel-price-transparency-service/external/ | DESNZ factsheet on Fuel Finder scheme for drivers, published 31 March 2026 |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| FFDF-C1 | FFDF | Page 1 | Business Requirement | "Fuel Finder is a new scheme designed to help drivers find the cheapest fuel near them." |
| FFDF-C2 | FFDF | Page 1-2 | Integration Requirement | "You can find the cheapest petrol and diesel prices near you on apps and websites, with examples including: Confused.com, DriveScore, Fuel Finder UK, Fuel Spy, MotorMouth, PetrolPrices.com, RAC Fuel Watch" |
| FFDF-C3 | FFDF | Page 2 | Data Requirement | "Drivers can alternatively download data directly" at developer.fuelfinder.service.gov.uk/access-latest-fuelprices |
| FFDF-C4 | FFDF | Page 2 | Data Requirement | "the data is intended for website and app developers, it will not be a useful format for everyone" |
| FFDF-C5 | FFDF | Page 3 | Functional Requirement | "If you visit a petrol station and the price does not match up, you can report it directly to the government's service" |
| FFDF-C6 | FFDF | Page 2 | Compliance Constraint | "Under the scheme, petrol stations across the UK are required to report their fuel prices within 30 minutes of any change." |
| FFDF-C7 | FFDF | Page 2 | Compliance Constraint | "Around 90% of petrol stations are now signed up to Fuel Finder" |
| FFDF-C8 | FFDF | Page 2 | Business Requirement | "We estimate this will save households who own a car an average of GBP 40 a year." |

---

## Spawned Knowledge

The following standalone knowledge files were created or updated from this research:

### Vendor Profiles
- `vendors/ve3-global-profile.md` -- Created
- `vendors/aws-profile.md` -- Updated
- `vendors/govuk-notify-profile.md` -- Updated
- `vendors/ordnance-survey-profile.md` -- Updated

### Tech Notes
- `tech-notes/fuel-finder-api.md` -- Updated
- `tech-notes/fuel-finder-third-party-ecosystem.md` -- Created
- `tech-notes/govuk-forms.md` -- Created

---

**Generated by**: ArcKit `/arckit:research` agent
**Generated on**: 2026-04-06
**ArcKit Version**: 1.0.3
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: Claude Opus 4.6 (1M context)
