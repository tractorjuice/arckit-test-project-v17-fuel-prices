# Tech Note: Fuel Finder Statutory API

> **Template Origin**: Official | **ArcKit Version**: 1.0.3 | **Command**: `/arckit.research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | fuel-finder-api |
| **Document Type** | Tech Note |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.2 |
| **Created Date** | 2026-03-26 |
| **Last Modified** | 2026-04-06 |
| **Review Cycle** | On-Demand |
| **Next Review Date** | 2026-06-26 |
| **Owner** | Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, Delivery Team, Architecture Review Board |
| **Source Research** | ARC-001-RSCH-v5.0 |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-26 | ArcKit AI | Initial creation from `/arckit:research` agent -- live API documentation | PENDING | PENDING |
| 1.1 | 2026-03-27 | ArcKit AI | Updated from official developer portal PDFs: added two API surfaces (Public API, Price Submission API), testing workflow, price submission constraints, data usage restrictions, legislation SI reference | PENDING | PENDING |
| 1.2 | 2026-04-06 | ArcKit AI | Updated from GOV.UK factsheet and industry reporting: added CSV bulk download channel (twice daily), citizen error reporting service, data quality issues (VE3 platform reliability), compliance rate (90% registered), enforcement timeline (May 2026), third-party consumer ecosystem (7 named), VE3 contract risk | PENDING | PENDING |

---

## Summary

The Fuel Finder Statutory API is the production REST API operated by VE3 Global Ltd under contract to DESNZ, providing real-time fuel price data from all ~8,500 registered UK petrol filling stations under [The Motor Fuel Price (Open Data) Regulations 2025](https://www.legislation.gov.uk/uksi/2025/1356/introduction/made). The API launched 2 February 2026 and is accessible via the developer portal at developer.fuel-finder.service.gov.uk.

## Key Findings

### Two Distinct API Surfaces

The platform exposes two API surfaces for different user types:

- **Fuel Finder Public API** (Information Recipients -- read-only): Access trusted open data including current prices by fuel grades, forecourt details (address, operator, brand), site amenities, opening hours, and timestamped updates via GET requests
- **Fuel Finder Price Submission API** (Motor Fuel Traders -- write): Submit fuel price updates for registered Petrol Fuelling Stations (PFS) via POST requests; requires GOV.UK One Login authentication

### Core API Details

- **Base URL**: `https://api.fuelfinder.service.gov.uk/v1/`
- **Forecourt ID Format**: `GB-12345` (e.g., `GET /v1/prices/GB-12345`)
- **Authentication**: OAuth 2.0 client credentials (`POST /api/v1/oauth/generate_access_token`) with scope `fuelfinder.read`; tokens last 3600 seconds
- **Public API Endpoints**: `GET /api/v1/pfs` (station metadata), `GET /api/v1/pfs/fuel-prices` (price data)
- **Fuel Types**: E10 (unleaded), E5 (super unleaded), B7 (diesel), SDV (premium diesel); aliases: DIESEL->B7, UNLEADED->E10, PREMIUM_UNLEADED->E5
- **Pagination**: Batch-number parameter supporting up to 80 batches
- **Incremental Sync**: `effective-start-timestamp` parameter for delta updates
- **Rate Limits**: 30 RPM per client in both test and live environments; burst to 60 RPM in test; 1 concurrent request
- **Data Freshness**: Prices published within 30 minutes of any price change at forecourt (statutory requirement)
- **Caching Guidance**: Station data 1-hour cache; price data 15-minute cache; search results 5-minute cache; use HTTP caching headers; implement cache invalidation
- **Environments**: Separate test (sandbox) and production with distinct credentials; test credentials invalid in production and vice versa
- **Price Format**: GBP per litre to 3 decimal places (e.g., 1.379)
- **Station Fields**: node_id, trading_name, brand_name, location (coordinates, address), fuel_types, amenities, opening_times
- **Error Handling**: 401 for expired/invalid tokens; 429 for rate limit with Retry-After header; exponential backoff recommended
- **External Dependencies**: Ordnance Survey (50/600 RPM), Companies House (strict limits, cache recommended)
- **GOV.UK One Login**: Required for all API access; additionally for motor fuel trader registration and price submission credentials

### Data Access Channels (updated v1.2)

| Channel | Method | Update Frequency | Authentication | Best For |
|---------|--------|-----------------|----------------|----------|
| REST API | GET requests (JSON) | Within 30 min of change | OAuth 2.0 | Real-time integration |
| CSV Download | Direct download at developer.fuelfinder.service.gov.uk/access-latest-fuelprices | Twice daily | GOV.UK One Login | Bulk analytics, DR fallback |
| Email Subscription | Link to latest CSV on publication | On publication | Email | Monitoring, notification |

### Price Submission Constraints

- **Sequential processing**: MFT must not send another request until the response for the previous request is received; API returns 429 if violated
- **Changed prices only**: Submissions must only include price changes for each fuel type; unchanged prices must not be resent
- **No timestamp manipulation**: Resending unchanged prices by changing the timestamp creates unnecessary load; future versions will return an error code
- **Transaction flow**: Submit price update -> poll transaction for mock status updates -> handle accepted or rejected outcomes

### Testing Environments

- **Live**: All production APIs; public data APIs are read-only and can be safely tested against live
- **Test**: Mirrors live API versions; separate test account via fuel-finder.service.gov.uk; write operations (price submission) must be done in test only
- **MFT test flow**: Register MFT organisation and associated PFS via FF service staging URL -> use forecourt IDs -> obtain sandbox token -> submit -> poll for status
- **Restriction**: Test keys must not be used for performance testing or high-volume traffic; use mocked or cached responses

### Security and Data Usage

- Never expose client secrets or access tokens in client-side code or public repositories
- Store secrets in env vars or secure secrets manager; separate credentials per environment and per application
- Do not log secrets or tokens; mask sensitive values in logs
- Run OAuth on backend services only -- never expose to browsers or mobile apps
- Monitor token usage for anomalies (unexpected IPs, request spikes)
- **Data usage restriction**: Do not redistribute raw API data; attribute data sources appropriately; data available under OGL v3.0

### Platform Reliability Issues (added v1.2)

Documented VE3 platform issues since launch:

| Issue | Date | Impact | Status |
|-------|------|--------|--------|
| Invalid activation codes sent to retailers | Jan 2026 | Registration delays | Resolved |
| Registration opened 2 weeks behind schedule | Jan 2026 | Late onboarding | Resolved |
| Prices displayed as 1.3p/litre (pence/pounds unit confusion) | Feb 2026 | Consumer misinformation | Partially resolved |
| 500+ forecourts with incorrect location data | Mar 2026 | Navigation errors | Under investigation |
| Unannounced backend IT changes without retailer consultation | Mar 2026 | Submission failures | Resolved |
| Forecourts located "in the ocean" (coordinate errors) | Mar 2026 | Data integrity | Under investigation |
| Prices of GBP 15/litre (implausible) | Mar 2026 | Consumer misinformation | Under investigation |

**Root Cause (pricing errors)**: The system accepts prices in both pence-per-litre (e.g., 131) and pounds-per-litre (e.g., 1.31) format. This denomination ambiguity causes 1.31 to be displayed as 1.3p when misinterpreted.

**Implication**: CMA data validation pipeline must implement plausibility checks (50-500 PPL range) to catch unit confusion errors before serving to citizens.

### Compliance and Adoption Rates (added v1.2)

- **Registration**: ~90% of UK petrol stations signed up as of 31 March 2026 (~7,650 of ~8,500)
- **At launch**: 6,243 of 8,279 (75.4%) registered by 2 February 2026 deadline
- **Enforcement**: CMA enforcement powers activate from 1 May 2026
- **Grace period**: Focus on supporting compliance rather than enforcement until May 2026

### Citizen Error Reporting (added v1.2)

DESNZ operates an error reporting service at gov.uk/guidance/report-an-error-in-fuel-prices-or-forecourt-details where citizens can report pricing discrepancies, incorrect facilities, inaccurate opening times, location errors, and temporary closures.

### Third-Party Consumer Ecosystem (added v1.2)

7 named consumers confirmed live as of 31 March 2026: Confused.com, DriveScore, Fuel Finder UK, Fuel Spy, MotorMouth, PetrolPrices.com, RAC Fuel Watch. Additional consumers include GoCompare, AA App, myRAC App, and Waze.

## Relevance to Projects

- **Project 001 (UK Fuel Price Transparency Service)**: Primary data source. All fuel price data ingested from this API. Integration architecture must implement OAuth token management, batch pagination, incremental sync, caching strategy, rate limit compliance, **enhanced data validation (given VE3 quality issues)**, CSV download as secondary channel, and respect data usage restrictions (no raw redistribution; attribution required).

---

**Generated by**: ArcKit `/arckit:research` agent
**Generated on**: 2026-03-26
**ArcKit Version**: 1.0.3
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: Claude Opus 4.6 (1M context)
