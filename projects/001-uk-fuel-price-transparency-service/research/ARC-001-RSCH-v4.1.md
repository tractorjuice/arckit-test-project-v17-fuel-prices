# Technology and Service Research: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 1.0.3 | **Command**: `/arckit.research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RSCH-v4.1 |
| **Document Type** | Technology and Service Research |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 4.1 |
| **Created Date** | 2026-03-26 |
| **Last Modified** | 2026-03-27 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-06-26 |
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
| 4.1 | 2026-03-27 | ArcKit AI | Updated from official Fuel Finder developer portal PDFs (5 documents): added two distinct API surfaces (Public API for information recipients, Price Submission API for motor fuel traders), price submission constraints, testing workflow, legislation SI reference, data usage restrictions, forecourt ID format | PENDING | PENDING |

---

## Executive Summary

### Research Scope

This document presents comprehensive market research findings for technologies, services, and platforms required to build and operate the UK Fuel Price Transparency Service. It incorporates the **now-live Fuel Finder developer API** (https://www.developer.fuel-finder.service.gov.uk/) with documented REST endpoints, OAuth 2.0 authentication, and published developer guidelines -- a material change from prior research versions (v1.0-v2.0) which were written before the API existed.

**Requirements Analyzed**: 15 functional (FR-001 to FR-015), 17 non-functional (NFR-P, NFR-A, NFR-S, NFR-SEC, NFR-C, NFR-U, NFR-M, NFR-I), 8 integration (INT-001 to INT-008), 6 data entity requirements

**Research Categories Identified**: 10 categories based on requirement analysis

**Research Approach**: Web research across UK Government developer portal, GOV.UK platforms, Digital Marketplace, open source repositories (GitHub, PyPI), vendor documentation, pricing calculators, G2/Gartner reviews, and UK government code repositories (govreposcrape)

### Key Findings

- **Fuel Finder API is now production-ready**: The developer portal at developer.fuel-finder.service.gov.uk exposes REST endpoints (`GET /api/v1/pfs`, `GET /api/v1/pfs/fuel-prices`) with OAuth 2.0 client credentials authentication, 30 RPM rate limits, and 4 fuel types (E10, E5, B7, SDV). This eliminates the need for the CMA interim scheme's 14 individual retailer JSON feeds as the primary data source.
- **GOV.UK platforms cover 4 categories at zero cost**: GOV.UK Notify (notifications), GOV.UK One Login (retailer authentication), GOV.UK Design System (frontend), and OS Places API (geocoding/address) are all free for UK central government under existing agreements.
- **AWS is the recommended cloud platform**: G-Cloud listed, NCSC-assessed, UK region (eu-west-2) with 3 availability zones, GBP billing, and widespread UK Government adoption. Estimated 3-year infrastructure TCO of GBP 195K-250K.
- **Custom build required for core service logic**: No off-the-shelf product exists for a regulatory fuel price transparency service. Data ingestion pipeline, compliance dashboard, enforcement tools, and citizen search are all bespoke.
- **Open source stack reduces cost and lock-in**: PostgreSQL + PostGIS for geospatial queries, Pydantic for API validation, Great Expectations for data quality, and Prometheus + Grafana for observability -- all proven in UK Government contexts.

### Build vs Buy Summary

| Approach | Categories | Total 3-Year TCO | Rationale |
|----------|-----------|------------------|-----------|
| **BUILD** (Custom Development) | 4 categories | GBP 1,200K-1,600K | Core bespoke service logic -- no off-the-shelf product |
| **BUY** (Managed Cloud Services) | 3 categories | GBP 195K-250K | AWS managed services (RDS, SQS, ECS/EKS, API Gateway) |
| **ADOPT** (Open Source) | 3 categories | GBP 45K-85K | PostGIS, Pydantic, Great Expectations, Grafana |
| **GOV.UK Platforms** | 4 categories | GBP 5K-15K | Notify, One Login, Design System, OS Places (integration effort only) |
| **TOTAL** | 10 categories | **GBP 1,445K-1,950K** | Blended approach recommended |

### Top Recommended Vendors

**Shortlist for further evaluation**:

1. **AWS (Amazon Web Services)** for Cloud Infrastructure: G-Cloud listed, NCSC-assessed, 3 UK AZs, widest UK Government adoption, GBP billing
2. **GOV.UK Notify** for Notifications: Free for central government, 250K free SMS/year, API-integrated, mandatory under TCoP
3. **Ordnance Survey Places API** for Geocoding and Address Validation: Free under PSGA, authoritative UK addressing, UPRN-based, updated 6-weekly

### Requirements Coverage

- 100% of requirements have identified solutions (build, buy, adopt, or GOV.UK platform)
- 4 requirements need custom development (no suitable off-the-shelf): data ingestion pipeline, compliance dashboard, enforcement tools, citizen search UI
- 0 requirements need further research -- the Fuel Finder API launch resolves the previously open question about the statutory data source specification

---

## Research Categories

> **Note**: Research categories dynamically identified from analysis of ARC-001-REQ-v2.0 functional, non-functional, and integration requirements.

---

## Category 1: Fuel Price Data Source -- Statutory Fuel Finder API

**Requirements Addressed**: FR-003, FR-004, FR-005, FR-007, FR-014, BR-002, BR-003, BR-005, INT-008, NFR-P-001, NFR-P-002

**Why This Category**: The Fuel Finder statutory API is the authoritative source of fuel price data from all ~8,500 UK forecourts under the Motor Fuel Price (Open Data) Regulations 2025. It is the foundation upon which all downstream service capabilities depend.

---

### Option 1A: GOV.UK Platform -- Fuel Finder Statutory API (VE3 Global / DESNZ)

**Description**: The production Fuel Finder API, operated by VE3 Global Ltd under contract to DESNZ, provides REST endpoints for accessing real-time fuel prices and forecourt information from all registered UK petrol filling stations.

**API Specification** (as documented at developer.fuel-finder.service.gov.uk and verified from official developer portal PDF documentation):

The Fuel Finder platform exposes **two distinct API surfaces**:

| API Surface | Users | HTTP Methods | Purpose |
|-------------|-------|--------------|---------|
| **Fuel Finder Public API** | Information Recipients (read-only) | GET | Access trusted open data: current prices by fuel grades, forecourt details, amenities, timestamped updates |
| **Fuel Finder Price Submission API** | Motor Fuel Traders (MFTs) | POST | Submit fuel price updates for registered Petrol Fuelling Stations (PFS) |

**Common API Details**:

| Aspect | Detail |
|--------|--------|
| **Base URL** | `https://api.fuelfinder.service.gov.uk/v1/` |
| **Token Endpoint** | `POST /api/v1/oauth/generate_access_token` |
| **Authentication** | OAuth 2.0 client credentials (client_id + client_secret + scope) |
| **Token Lifetime** | 3600 seconds (1 hour), Bearer token |
| **Transport** | HTTPS (TLS 1.2+) mandatory |
| **Data Format** | JSON |
| **Versioning** | URL path (`/v1/`) |
| **Legislation** | [The Motor Fuel Price (Open Data) Regulations 2025](https://www.legislation.gov.uk/uksi/2025/1356/introduction/made) |
| **Environments** | Test (sandbox) and Production with separate credentials; test credentials invalid in production and vice versa |
| **Forecourt ID Format** | `GB-12345` (e.g. `GET /v1/prices/GB-12345`) |
| **Rate Limit (Test)** | 30 RPM per client (burst to 60 RPM), 1 concurrent request |
| **Rate Limit (Live)** | 30 RPM per client, 1 concurrent request |
| **Data Freshness** | Prices published within 30 minutes of any change (statutory requirement) |

**Public API Endpoints** (Information Recipients — read-only):

| Endpoint | Purpose | Scope |
|----------|---------|-------|
| `GET /api/v1/pfs` | Station metadata (address, operator, brand, amenities, opening hours) | `fuelfinder.read` |
| `GET /api/v1/pfs/fuel-prices` | Current fuel prices by grade with timestamps | `fuelfinder.read` |
| **Pagination** | Batch-number parameter (up to 80 batches) | |
| **Incremental Sync** | `effective-start-timestamp` parameter for delta updates | |

**Price Submission API** (Motor Fuel Traders — write):

| Constraint | Detail |
|-----------|--------|
| **Sequential Processing** | MFT must not send another request until the response for the previous request is received; API returns 429 if violated |
| **Changed Prices Only** | Price submission requests must only include price changes for each fuel type; unchanged prices must not be resent |
| **No Timestamp Manipulation** | Fuel types with unchanged prices must not be resent by changing the timestamp (creates unnecessary load; future versions will return an error code) |
| **Transaction Polling** | Submit price update → poll transaction for status → handle accepted or rejected outcomes |
| **GOV.UK One Login Required** | Motor fuel traders must authenticate via GOV.UK One Login for price submission credentials |

**Fuel Types Supported**:

| API Code | Display Name | Description |
|----------|-------------|-------------|
| E10 | Unleaded | Standard unleaded petrol (10% ethanol) |
| E5 | Super Unleaded | Premium unleaded petrol (5% ethanol) |
| B7 | Diesel | Standard diesel (7% biodiesel) |
| SDV | Premium Diesel | Super/premium diesel variant |

**Aliases**: `DIESEL` maps to B7, `UNLEADED` maps to E10, `PREMIUM_UNLEADED` maps to E5, `B7_STANDARD` maps to B7

**Station Data Fields**: `node_id`, `trading_name`, `brand_name`, `location` (coordinates, address), `fuel_types` (list), `amenities` (list), `opening_times`

**Price Data Fields**: `price` (GBP per litre to 3 decimal places), `fuel_type`, `price_last_updated`, `price_change_effective_timestamp`

**Developer Guidelines** (from developer.fuel-finder.service.gov.uk/dev-guideline and official PDF documentation):

| Guideline | Detail |
|-----------|--------|
| **Caching** | Station data: 1 hour; Price data: 15 minutes; Search results: 5 minutes; use HTTP caching headers when available; implement cache invalidation strategies |
| **Security** | Never expose secrets in client-side code or public repos; store in env vars or secret managers; use separate credentials per environment and per application; HTTPS only (TLS 1.2+); rotate secrets regularly and immediately if compromise suspected; request minimum scopes (least privilege); do not log secrets or tokens — mask sensitive values; monitor token usage for anomalies (unexpected IPs, request spikes); run OAuth on backend services only — never expose to browsers or mobile apps |
| **Error Handling** | Check HTTP status codes; exponential backoff retry; 20-second timeout default; translate technical errors into user-friendly language; provide actionable suggestions; offer alternative actions |
| **Rate Limiting** | Respect limits; 429 returns Retry-After header; up to 3 retries with exponential backoff; test keys must not be used for performance testing or high-volume traffic |
| **Request Optimisation** | Use appropriate pagination to limit response sizes; request only needed data fields; implement request batching; use compression for large requests; avoid unnecessary requests |
| **Testing** | Unit test all endpoints; use sandbox environment; mock API responses for consistent testing; test error handling scenarios; validate data parsing; integration test with various data scenarios; verify rate limiting behaviour |
| **Monitoring** | Track request success/failure rates; monitor response times; alert on unusual usage patterns; track rate limit usage; include request IDs for tracing; implement log rotation and retention policies |
| **Data Validation** | Check required fields are present; validate data types and formats; handle null/undefined values gracefully; sanitize user inputs before API requests |
| **Data Usage** | Do not redistribute raw API data; attribute data sources appropriately; respect intellectual property rights; data available under OGL v3.0 |
| **Compliance** | Do not circumvent security; use data responsibly and ethically; respect user privacy and data protection; follow applicable laws and regulations |
| **External Dependencies** | OS: 50 RPM dev / 600 RPM live; Companies House: strict limits — use cached or mocked responses to avoid quota exhaustion |

**Testing Environments** (from API Testing documentation):

| Environment | Access | Notes |
|-------------|--------|-------|
| **Live** | Production APIs; real data | Public data APIs (read-only) and Price Submission APIs |
| **Test** | Mirrors live API versions | Separate test account via fuel-finder.service.gov.uk; dedicated OAuth credentials |
| **Public API testing** | Can test against live or test | Read-only; no production data impact |
| **Price Submission testing** | Test environment only | Register MFT org and PFS → use forecourt IDs → obtain sandbox token → submit → poll for status |

**Eligibility**: GOV.UK One Login required for all API access; information recipients get read-only access; motor fuel traders additionally get price submission credentials

**Cost Model**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| API Usage | GBP 0 | GBP 0 | GBP 0 | Free open data |
| Integration Development | GBP 15K | GBP 0 | GBP 0 | OAuth client, pagination, error handling |
| Maintenance | GBP 0 | GBP 3K | GBP 3K | API version updates, monitoring |
| **Total** | **GBP 15K** | **GBP 3K** | **GBP 3K** | |
| **3-Year TCO** | | | **GBP 21K** | |

**Pros**:

- Free, authoritative, statutory data source covering all ~8,500 UK forecourts
- RESTful API with OAuth 2.0 -- standard integration pattern
- Incremental sync capability reduces polling overhead
- Separate test and production environments
- Published developer guidelines with caching and rate limit advice

**Cons**:

- 30 RPM rate limit requires efficient batching and caching strategy
- Sequential price submission processing limits throughput (429 if previous request not complete)
- No webhook/push notification for price changes -- polling required
- API documentation split across React SPA pages (not a single OpenAPI spec download)
- Batch pagination (up to 80 batches) requires careful orchestration
- Data usage restriction: raw API data must not be redistributed; data sources must be attributed
- Test keys must not be used for performance testing or high-volume traffic

**Technology Code of Practice Alignment**:

- Point 3 (Be open): Open data under OGL
- Point 4 (Open standards): REST, JSON, OAuth 2.0
- Point 8 (Share, reuse): Government platform
- Point 10 (Make better use of data): Statutory open data scheme

**Source Citations**:
- [Fuel Finder Developer Portal](https://www.developer.fuel-finder.service.gov.uk/)
- [Fuel Finder Public API](https://www.developer.fuel-finder.service.gov.uk/public-api)
- [Fuel Finder REST API](https://www.developer.fuel-finder.service.gov.uk/apicontent)
- [API Authentication](https://www.developer.fuel-finder.service.gov.uk/api-authentication)
- [Developer Guidelines](https://www.developer.fuel-finder.service.gov.uk/dev-guideline)
- [API Testing](https://www.developer.fuel-finder.service.gov.uk/api-testing)
- [The Motor Fuel Price (Open Data) Regulations 2025](https://www.legislation.gov.uk/uksi/2025/1356/introduction/made)
- [GOV.UK Guidance: Access fuel price data](https://www.gov.uk/guidance/access-the-latest-fuel-prices-and-forecourt-data-via-api-or-email)
- [Fuel-Prices-UK Home Assistant Integration (API client source)](https://github.com/beecho01/Fuel-Prices-UK)
- Official Fuel Finder Developer Portal PDFs (5 documents): Api Authentication, Api Testing, Developer Guidelines, Public Api, Rest Api (local copies in `/fuelapi/`)

---

### Option 1B: Adopt -- CMA Interim Scheme (14 Retailer JSON Feeds)

**Description**: The pre-statutory voluntary scheme where 14 major retailers publish fuel prices as individual JSON endpoints. Covers ~35% of stations and ~60% of fuel volume. Previously the primary data source; now superseded by the statutory API.

**Status**: **Superseded by Fuel Finder statutory API**. Retained for reference and as a fallback during any statutory API outages.

**Retailer Endpoints** (14 feeds):
- Ascona Group: `https://fuelprices.asconagroup.co.uk/newfuel.json`
- Asda: `https://storelocator.asda.com/fuel_prices_data.json`
- bp: `https://www.bp.com/en_gb/united-kingdom/home/fuelprices/fuel_prices_data.json`
- Esso/Tesco Alliance: `https://fuelprices.esso.co.uk/latestdata.json`
- JET: `https://jetlocal.co.uk/fuel_prices_data.json`
- Karan Retail: `https://devapi.krlpos.com/integration/live_price/krl`
- Morrisons: `https://www.morrisons.com/fuel-prices/fuel.json`
- Moto: `https://moto-way.com/fuel-price/fuel_prices.json`
- Motor Fuel Group: `https://fuel.motorfuelgroup.com/fuel_prices_data.json`
- Rontec: `https://www.rontec-servicestations.co.uk/fuel-prices/data/fuel_prices_data.json`
- Sainsbury's: `https://api.sainsburys.co.uk/v1/exports/latest/fuel_prices_data.json`
- SGN: `https://www.sgnretail.uk/files/data/SGN_daily_fuel_prices.json`
- Shell: `https://www.shell.co.uk/fuel-prices-data.html`
- Tesco: `https://www.tesco.com/fuel_prices/fuel_prices_data.json`

**Recommendation**: **Do not use as primary source**. The statutory API provides comprehensive coverage. Retain knowledge of these endpoints for cross-reference validation and as an emergency fallback data source.

**Source Citations**:
- [GOV.UK: Access fuel price data](https://www.gov.uk/guidance/access-fuel-price-data)

---

### Option 1C: Adopt -- pyfuelprices (Python Library)

**Description**: Open source Python library wrapping CMA interim scheme feeds with async support and pluggable provider architecture.

**Project Details**:
- **License**: MIT
- **GitHub**: github.com/pantherale0/pyfuelprices -- 6 stars, 3 forks
- **Maturity**: Stable (17 releases, v2025.11.1)
- **Last Release**: November 2025
- **PyPI**: `pip3 install pyfuelprices`

**Recommendation**: Useful for prototyping and cross-reference but does not yet support the statutory Fuel Finder API. Monitor for updates.

---

### Build vs Buy Recommendation for Fuel Price Data Source

**Recommended Approach**: GOV.UK Platform -- Fuel Finder Statutory API

**Rationale**: The statutory API is the sole authoritative data source mandated by the Motor Fuel Price (Open Data) Regulations 2025. It provides complete coverage of all ~8,500 UK forecourts through a standard REST API with OAuth 2.0 authentication. There is no alternative that provides equivalent coverage or authority. Integration requires building a custom API client with OAuth token management, batch pagination, incremental sync, and caching -- estimated at 3-4 person-weeks of development effort.

**Key Decision Factors**:
- Statutory authority: legally mandated data source
- Complete coverage: all registered UK forecourts (vs 35% for interim scheme)
- Standard integration pattern: REST + OAuth 2.0 + JSON
- Zero data procurement cost

---

## Category 2: Cloud Infrastructure and Hosting

**Requirements Addressed**: NFR-A-001 (99.9% availability), NFR-A-002 (RPO 15min, RTO 4h), NFR-S-001 (horizontal scaling), NFR-SEC-003 (encryption), NFR-C-004 (TCoP cloud-first), BR-007 (governance)

**Why This Category**: All application components require cloud hosting in a UK sovereign data centre with G-Cloud procurement, NCSC assessment, and managed services to minimise operational burden.

---

### Option 2A: Buy -- AWS (Amazon Web Services) UK Region

**Description**: AWS eu-west-2 (London) provides 3 availability zones with comprehensive managed services. AWS is G-Cloud listed, NCSC-assessed for OFFICIAL workloads, Cyber Essentials Plus certified, and widely adopted across UK Government.

**Key Services Required**:

| AWS Service | Purpose | Mapped Requirements |
|-------------|---------|---------------------|
| ECS Fargate / EKS | Container orchestration | NFR-S-001, NFR-A-001 |
| RDS PostgreSQL | Relational database with PostGIS | FR-004, NFR-A-002 |
| SQS / SNS | Message queue for async pipeline | FR-007, NFR-P-002 |
| API Gateway | REST API management | FR-003, FR-005, NFR-I-001 |
| S3 | Object storage for bulk data/audit | FR-005, FR-010 |
| CloudFront | CDN for citizen service | NFR-P-001 |
| Secrets Manager | Secrets rotation | NFR-SEC-004 |
| CloudWatch | Monitoring and alerting | NFR-M-001 |
| WAF | Web application firewall | NFR-SEC-001 |
| KMS | Encryption key management | NFR-SEC-003 |

**Cost Estimate (AWS eu-west-2)**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| ECS Fargate (3 services, 2 tasks each) | GBP 25K | GBP 28K | GBP 30K | Avg 2 vCPU / 4GB per task |
| RDS PostgreSQL (db.r6g.large Multi-AZ) | GBP 22K | GBP 22K | GBP 22K | ~USD 0.34/hr on-demand; savings with RI |
| SQS | GBP 1K | GBP 1.5K | GBP 2K | ~USD 0.40/M requests; ~150K msgs/day Y1 |
| API Gateway | GBP 4K | GBP 6K | GBP 8K | USD 3.50/M REST requests |
| S3 + CloudFront | GBP 3K | GBP 4K | GBP 5K | Storage + CDN egress |
| WAF + Shield Standard | GBP 4K | GBP 4K | GBP 4K | WAF rules + managed rule groups |
| CloudWatch + Logs | GBP 5K | GBP 6K | GBP 7K | Log ingestion + dashboards |
| Secrets Manager + KMS | GBP 1K | GBP 1K | GBP 1K | Per-secret and per-key charges |
| **Total** | **GBP 65K** | **GBP 72.5K** | **GBP 79K** | |
| **3-Year TCO** | | | **GBP 216.5K** | |

**Compliance**:
- G-Cloud 14 listed on Digital Marketplace
- NCSC Cloud Security Principles assessment published
- Cyber Essentials Plus certified
- ISO 27001, SOC 2 Type II certified
- UK data residency (eu-west-2, 3 AZs)
- GBP billing available
- Dedicated UK Government support tier

**Pros**:
- Widest UK Government adoption (HMRC, DWP, Home Office, MOD, NHS)
- 3 availability zones in London for high availability
- Comprehensive managed services reducing operational burden
- GBP billing eliminates FX risk
- Mature IaC support (CloudFormation, Terraform, CDK)

**Cons**:
- Potential vendor lock-in for proprietary services (SQS, API Gateway)
- Complex pricing model requires FinOps discipline
- Egress charges can be significant at scale

**Source Citations**:
- [AWS G-Cloud UK](https://aws.amazon.com/government-education/g-cloud-uk/)
- [AWS RDS PostgreSQL Pricing](https://aws.amazon.com/rds/postgresql/pricing/)
- [AWS SQS Pricing](https://aws.amazon.com/sqs/pricing/)
- [Vantage RDS db.r6g.large](https://instances.vantage.sh/aws/rds/db.r6g.large)

---

### Option 2B: Buy -- Azure UK Regions

**Description**: Azure UK South (London) and UK West (Cardiff) provide managed services with G-Cloud listing and NCSC assessment. Strong for organisations using Microsoft ecosystem.

**Cost Estimate**: Comparable to AWS at GBP 200K-260K over 3 years for equivalent workload.

**Compliance**: G-Cloud listed, NCSC-assessed, ISO 27001, SOC 2, UK data residency, GBP billing.

**Recommendation**: Valid alternative. Prefer AWS due to wider UK Government adoption and 3 AZs in London (vs 3 AZs for UK South).

**Source Citation**: [Azure UK G-Cloud Compliance](https://learn.microsoft.com/en-us/azure/compliance/offerings/offering-uk-g-cloud)

---

### Build vs Buy Recommendation for Cloud Infrastructure

**Recommended Approach**: BUY -- AWS eu-west-2 (London)

**Rationale**: AWS offers the widest UK Government adoption, G-Cloud procurement, NCSC assessment, 3 London AZs, and comprehensive managed services. The 3-year infrastructure TCO of GBP 195K-250K (with reserved instance savings) provides excellent value for a service requiring 99.9% availability and multi-AZ DR. Azure is a credible alternative but AWS has deeper cross-government community of practice.

---

## Category 3: Database and Geospatial Search

**Requirements Addressed**: FR-004 (citizen proximity search), FR-001 (forecourt registry), FR-007 (data pipeline), FR-010 (audit trail), NFR-P-001 ( < 3s p95), NFR-A-002 (RPO 15min), NFR-S-002 (55M records/year)

**Why This Category**: The service requires a relational database with geospatial query capabilities for proximity-based fuel price search across ~8,500 forecourts.

---

### Option 3A: Buy -- AWS RDS PostgreSQL with PostGIS

**Description**: Managed PostgreSQL on AWS RDS with the PostGIS extension for geospatial queries. PostGIS provides spatial indexing (GiST), proximity search (ST_DWithin, ST_Distance), and GeoJSON output -- all critical for the citizen fuel price search use case.

**PostGIS Capabilities**:

| Capability | Requirement | PostGIS Feature |
|-----------|-------------|-----------------|
| Proximity search | FR-004: find forecourts within radius | `ST_DWithin(geography, geography, distance_metres)` |
| Distance calculation | FR-004: display distance to forecourt | `ST_Distance(geography, geography)` |
| GeoJSON output | NFR-I-003: open data format | `ST_AsGeoJSON(geometry)` |
| Spatial indexing | NFR-P-001: < 3s response time | GiST spatial index on forecourt locations |
| Bounding box queries | FR-014: in-car nearby search | `&&` operator with spatial index |

**RDS Instance Sizing**:

| Metric | Year 1 | Year 3 | Instance |
|--------|--------|--------|----------|
| Forecourts | 8,500 | 10,000 | db.r6g.large (2 vCPU, 16GB) |
| Price records/day | 150K | 300K | Multi-AZ for HA |
| Historical records | 55M | 165M | 500GB GP3 storage growing |
| Read replicas | 1 | 2 | For analytics and citizen queries |

**Cost Estimate**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| RDS Primary (Multi-AZ) | GBP 18K | GBP 18K | GBP 18K | db.r6g.large with 1-year RI |
| Read Replica | GBP 9K | GBP 9K | GBP 18K | 1 replica Y1-2, 2 replicas Y3 |
| Storage (GP3) | GBP 3K | GBP 4K | GBP 5K | Growing from 200GB to 500GB |
| Backups | GBP 1K | GBP 1.5K | GBP 2K | PITR + cross-region |
| **Total** | **GBP 31K** | **GBP 32.5K** | **GBP 43K** | |
| **3-Year TCO** | | | **GBP 106.5K** | |

**Pros**:
- PostGIS is the gold standard for geospatial queries in PostgreSQL
- Managed by AWS (patching, backups, failover)
- PITR recovery meets RPO 15-minute requirement
- Multi-AZ automatic failover meets RTO requirement
- Read replicas isolate citizen queries from ingestion writes
- Widely used across UK Government (numerous PostGIS deployments found in govreposcrape)

**Cons**:
- At 165M+ records (Year 3), may need partitioning strategy for historical data
- PostGIS adds operational complexity vs plain PostgreSQL
- Reserved Instance commitment required for cost-effective pricing

**Source Citations**:
- [PostGIS](https://postgis.net/)
- [PostgreSQL as Geospatial Database](https://mapscaping.com/podcast/postgresql-an-open-source-geospatial-database-for-gis-practitioners/)
- [osmuk2pgsql -- UK OpenStreetMap in PostGIS](https://github.com/osm-uk/osmuk2pgsql)

---

### Build vs Buy Recommendation for Database

**Recommended Approach**: BUY -- AWS RDS PostgreSQL with PostGIS extension

**Rationale**: PostgreSQL with PostGIS is the established open source standard for geospatial queries and is used extensively across UK Government. AWS RDS provides managed operations (patching, backups, failover) that meet the NFR-A-002 disaster recovery requirements. The combination of PostGIS spatial indexing and read replicas supports the NFR-P-001 response time target of < 3 seconds p95 for citizen proximity searches across 8,500+ forecourts.

---

## Category 4: Message Queue and Event Streaming

**Requirements Addressed**: FR-007 (async data pipeline), NFR-P-002 (5,000 submissions/min peak), NFR-A-003 (fault tolerance), Principle 12 (async communication)

**Why This Category**: The data ingestion pipeline requires asynchronous message processing to decouple retailer submission acknowledgement from downstream validation, enrichment, and publication.

---

### Option 4A: Buy -- AWS SQS (Simple Queue Service)

**Description**: Fully managed message queue with unlimited throughput, at-least-once delivery, and no operational overhead. Standard queues support virtually unlimited messages per second.

**Cost Estimate**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| SQS Standard | GBP 800 | GBP 1.2K | GBP 1.5K | USD 0.40/M requests; ~150K msgs/day Y1 |
| SQS FIFO (audit) | GBP 400 | GBP 600 | GBP 800 | USD 0.50/M for ordered audit events |
| **Total** | **GBP 1.2K** | **GBP 1.8K** | **GBP 2.3K** | |
| **3-Year TCO** | | | **GBP 5.3K** | |

**Pros**:
- Zero operational overhead -- fully managed
- Unlimited throughput for Standard queues (meets 5,000/min peak)
- Dead letter queue support for failed messages
- Native integration with ECS, Lambda, and other AWS services
- Extremely low cost (effectively pennies per day at this volume)

**Cons**:
- AWS-specific (vendor lock-in risk)
- Standard queues: at-least-once delivery (consumers must be idempotent)
- FIFO queues: 300 messages/second without batching

**Recommendation**: BUY -- AWS SQS. At GBP 5.3K over 3 years, the cost is negligible and the operational burden is zero. Use Standard queues for the ingestion pipeline and FIFO queues for audit event ordering.

**Source Citation**: [AWS SQS Pricing](https://aws.amazon.com/sqs/pricing/)

---

## Category 5: API Gateway and Management

**Requirements Addressed**: FR-003 (API submission, rate limiting), FR-005 (open data API), FR-014 (CarPlay/Auto responses), NFR-I-001 (REST, OpenAPI), NFR-SEC-001 (WAF protection)

**Why This Category**: The service exposes two distinct API surfaces -- a retailer submission API (authenticated, rate-limited) and a public read API (unauthenticated, rate-limited by IP) -- requiring managed API gateway capabilities.

---

### Option 5A: Buy -- AWS API Gateway

**Description**: Managed REST API gateway with throttling, API key management, OpenAPI import, request/response transformation, and CloudWatch integration.

**Cost Estimate**: GBP 4K-8K/year based on 10M-30M API calls/year (growing with third-party adoption).

**Pros**:
- Native AWS integration (WAF, CloudWatch, IAM)
- Per-request pricing aligns with usage growth
- OpenAPI import/export for developer portal
- Request throttling and API key management built in
- Response transformation for FR-014 (carplay/auto format)

**Cons**:
- AWS vendor lock-in
- 29-second integration timeout (adequate for this use case)
- Complex pricing at very high volumes

---

### Option 5B: Adopt -- Kong Gateway (Open Source)

**Description**: Open source API gateway with plugin ecosystem, rate limiting, authentication, and multi-cloud portability. Self-hosted on ECS/EKS.

**Cost Estimate**: GBP 15K-25K/year including infrastructure and operational overhead for self-managed deployment.

**Recommendation**: AWS API Gateway preferred over Kong for this project. The managed service eliminates operational overhead and the per-request pricing is cost-effective at projected volumes. Kong would be appropriate if multi-cloud portability were a requirement, which it is not for this UK Government service.

**Source Citations**:
- [Kong vs AWS API Gateway](https://konghq.com/blog/enterprise/kong-vs-aws-api-gateway)
- [Top API Gateways 2026](https://www.digitalapi.ai/blogs/best-api-gateway)

---

### Build vs Buy Recommendation for API Gateway

**Recommended Approach**: BUY -- AWS API Gateway

**Rationale**: AWS API Gateway provides managed rate limiting, authentication integration, OpenAPI support, and WAF integration at a cost-effective per-request price. The projected volume (10M-30M requests/year) keeps costs well under GBP 10K/year. Response transformation capability supports the FR-014 in-car format requirement.

---

## Category 6: Notifications and Communications

**Requirements Addressed**: FR-009 (retailer notifications), FR-006 (enforcement notifications), INT-003 (GOV.UK Notify), BR-004 (enforcement capability)

**Why This Category**: The service must send automated email and SMS notifications to retailers for compliance reminders, submission confirmations, and enforcement actions.

---

### Option 6A: GOV.UK Platform -- GOV.UK Notify

**Description**: The cross-government notification platform providing email, SMS, and letter sending via API. Free for central government email; SMS at 2.33p per message.

**Pricing**:

| Channel | Cost | Free Allowance | Notes |
|---------|------|----------------|-------|
| Email | Free | Unlimited | No setup, monthly, or per-email charge |
| SMS | 2.33p/message (+ VAT) | 250,000 free texts/year for central gov | After allowance, pay per message |
| Letters | From 36p/letter (+ VAT) | None | Physical mail option |

**Cost Estimate**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Email (compliance reminders) | GBP 0 | GBP 0 | GBP 0 | Free for all volumes |
| SMS (urgent compliance) | GBP 0 | GBP 500 | GBP 1K | Within free allowance Y1; growing Y2-3 |
| Integration Development | GBP 5K | GBP 0 | GBP 0 | API client, templates, callbacks |
| **Total** | **GBP 5K** | **GBP 500** | **GBP 1K** | |
| **3-Year TCO** | | | **GBP 6.5K** | |

**API Integration**:
- REST API with API key authentication
- Template-based messaging (personalisation via placeholders)
- Delivery status callbacks (webhook)
- Batch sending for bulk compliance reminders
- Python, Java, Ruby, Node.js client libraries available

**Compliance**:
- Mandatory under TCoP Point 8 (Share, reuse and collaborate)
- UK data residency
- GDPR compliant
- Accessibility compliant

**Recommendation**: GOV.UK Notify is **mandatory** for this UK Government service. It is free for email, low-cost for SMS, provides delivery tracking, and meets all TCoP requirements. Integration effort is low (1-2 person-weeks) with mature client libraries.

**Source Citations**:
- [GOV.UK Notify](https://www.notifications.service.gov.uk/)
- [GOV.UK Notify Pricing](https://www.notifications.service.gov.uk/pricing)
- [GOV.UK Notify Features](https://www.notifications.service.gov.uk/features)

---

## Category 7: Address Validation and Geocoding

**Requirements Addressed**: INT-001 (address gazetteer), INT-002 (geocoding), FR-001 (registration address validation), FR-004 (citizen postcode search)

**Why This Category**: Forecourt registration requires address validation against an authoritative UK address dataset, and citizen search requires postcode-to-coordinate geocoding.

---

### Option 7A: GOV.UK Platform -- Ordnance Survey Places API (PSGA)

**Description**: The authoritative UK address lookup and geocoding API, free for public sector under the Public Sector Geospatial Agreement (PSGA). Provides UPRN-based address matching, postcode lookup, and coordinate geocoding.

**Capabilities**:

| Capability | Requirement | API Feature |
|-----------|-------------|-------------|
| Address validation | FR-001, INT-001 | Full/partial address search |
| Postcode lookup | FR-004, INT-002 | Postcode to coordinates + addresses |
| UPRN matching | FR-001 | Unique Property Reference Number |
| Coordinate geocoding | FR-004 | Lat/lng for each address |

**Pricing**: Free under PSGA for UK central government.

**Rate Limits**: 50 RPM (development), 600 RPM (live) -- per Fuel Finder developer guidelines.

**Data Currency**: Updated every 6 weeks from AddressBase Premium.

**Cost Estimate**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| API Usage | GBP 0 | GBP 0 | GBP 0 | Free under PSGA |
| Integration | GBP 5K | GBP 0 | GBP 0 | Address lookup + geocoding client |
| **Total** | **GBP 5K** | **GBP 0** | **GBP 0** | |
| **3-Year TCO** | | | **GBP 5K** | |

**Recommendation**: OS Places API is the **recommended** address validation and geocoding service. It is authoritative, free under PSGA, and provides UPRN matching which is the UK Government standard for property identification. Supplement with PostGIS for runtime proximity calculations to avoid API rate limit constraints during citizen searches.

**Source Citations**:
- [OS Places API](https://www.ordnancesurvey.co.uk/products/os-places-api)
- [OS Places API Docs](https://docs.os.uk/os-apis/accessing-os-apis/os-places-api)
- [PSGA Free Access](https://www.gov.uk/guidance/access-free-address-data-using-addressbase)

---

## Category 8: Authentication and Identity

**Requirements Addressed**: NFR-SEC-001 (authentication), NFR-SEC-002 (authorisation), INT-005 (GOV.UK One Login), INT-006 (CMA IdP), FR-008 (retailer account management)

**Why This Category**: Multiple authentication flows are required: retailer web login with MFA, API client credentials for automated submission, CMA SSO for enforcement dashboard, and unauthenticated citizen access.

---

### Option 8A: GOV.UK Platform -- GOV.UK One Login (Retailer Authentication)

**Description**: The cross-government identity platform for citizen and business user authentication. Supports OIDC/OAuth 2.0 with optional identity verification. The Fuel Finder developer portal already uses GOV.UK One Login for motor fuel trader access.

**Key Facts**:
- Available for 200+ government services (as of February 2026)
- OIDC-compliant with integration and production environments
- Identity verification levels: low (email + password), medium (document check), high (biometric)
- Free for government services (funded centrally)

**Cost Estimate**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Platform Usage | GBP 0 | GBP 0 | GBP 0 | Free for government services |
| OIDC Integration | GBP 8K | GBP 0 | GBP 0 | 2 person-weeks integration |
| **Total** | **GBP 8K** | **GBP 0** | **GBP 0** | |
| **3-Year TCO** | | | **GBP 8K** | |

**Note**: The Fuel Finder statutory API already uses GOV.UK One Login for motor fuel trader authentication. Aligning the CMA service's retailer authentication with this is architecturally consistent.

**Source Citations**:
- [GOV.UK One Login](https://www.sign-in.service.gov.uk/)
- [One Login Technical Documentation](https://docs.sign-in.service.gov.uk/)
- [One Login Integration Guide](https://docs.sign-in.service.gov.uk/integrate-with-integration-environment/)

---

### Option 8B: CMA Corporate Identity Provider (CMA Staff SSO)

**Description**: Federation with CMA's corporate IdP via SAML 2.0 or OIDC for enforcement dashboard access. This is an integration requirement (INT-006), not a procurement decision.

**Cost Estimate**: GBP 5K integration effort (1 person-week for SAML/OIDC federation setup).

---

### Option 8C: OAuth 2.0 Client Credentials (API Submission)

**Description**: Standard OAuth 2.0 client credentials grant for automated price submission by large retailers. The Fuel Finder API already implements this pattern -- the CMA service should mirror it for consistency.

**Implementation**: Custom build using a standard OAuth 2.0 library. Client ID and secret issued per retailer organisation, stored in AWS Secrets Manager, rotated every 90 days.

**Cost Estimate**: GBP 10K development (included in core build estimate).

---

### Build vs Buy Recommendation for Authentication

**Recommended Approach**: GOV.UK Platform (One Login for retailers) + CMA IdP federation (staff) + Custom OAuth 2.0 (API clients)

**Rationale**: GOV.UK One Login is the mandated government authentication platform and is already in use by the Fuel Finder service itself. Using it for retailer web authentication provides consistency and compliance. CMA staff SSO is a standard SAML/OIDC federation. API client credentials follow the OAuth 2.0 pattern already established by the Fuel Finder API.

---

## Category 9: Data Validation and Quality

**Requirements Addressed**: FR-007 (data validation pipeline), NFR-P-002 (15-minute freshness SLA), Principle 9 (data quality)

**Why This Category**: Fuel price submissions must be validated for schema correctness, plausibility (price within range), completeness (all fuel types), and anomaly detection (suspicious price changes) before publication.

---

### Option 9A: Adopt -- Pydantic (Python Schema Validation)

**Description**: Python library for data validation using type annotations. Ideal for validating API request payloads and internal data models. Listed by the UK Home Office among its users.

**License**: MIT. **GitHub**: 20K+ stars. **Maturity**: Production-ready.

**Use Case**: Validate incoming fuel price submission payloads against the data schema defined in the Fuel Finder API specification.

---

### Option 9B: Adopt -- Great Expectations (Data Quality Framework)

**Description**: Open source Python framework for defining, running, and documenting data quality expectations. Provides automated data profiling, validation rules, and quality documentation.

**License**: Apache 2.0. **GitHub**: 10K+ stars. **Maturity**: Production-ready.

**Use Case**: Define and automate data quality rules for the ingestion pipeline -- price plausibility ranges, completeness checks, anomaly detection thresholds, freshness monitoring.

**Cost Estimate (Combined)**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Development (validation rules) | GBP 20K | GBP 5K | GBP 5K | Schema + plausibility + anomaly rules |
| Infrastructure | GBP 0 | GBP 0 | GBP 0 | Runs within application containers |
| **Total** | **GBP 20K** | **GBP 5K** | **GBP 5K** | |
| **3-Year TCO** | | | **GBP 30K** | |

**Recommendation**: ADOPT -- Pydantic for API schema validation + Great Expectations for pipeline data quality. Both are MIT/Apache licensed, widely adopted, and zero licensing cost.

**Source Citations**:
- [Pydantic](https://docs.pydantic.dev/)
- [Great Expectations](https://greatexpectations.io/)
- [2026 Open Source Data Quality Landscape](https://datakitchen.io/the-2026-open-source-data-quality-and-data-observability-landscape/)

---

## Category 10: Observability and Monitoring

**Requirements Addressed**: NFR-M-001 (observability), NFR-C-002 (audit logging), Principle 7 (operational excellence), FR-010 (audit trail)

**Why This Category**: Comprehensive telemetry (logs, metrics, traces) is required for operational monitoring, data freshness SLIs, compliance dashboards, and security event detection.

---

### Option 10A: Buy -- AWS CloudWatch + CloudWatch Logs

**Description**: Native AWS monitoring with metrics, logs, alarms, and dashboards. Zero-setup integration with all AWS services.

**Cost Estimate**: GBP 5K-7K/year for log ingestion, metric storage, and dashboard hosting.

---

### Option 10B: Adopt -- Prometheus + Grafana (Self-Hosted)

**Description**: Open source observability stack. Prometheus for metrics collection and alerting; Grafana for dashboards and visualisation. Industry standard for cloud-native monitoring.

**Cost Estimate**: GBP 3K-5K/year infrastructure + GBP 5K setup.

---

### Option 10C: Buy -- Amazon Managed Grafana + Amazon Managed Prometheus

**Description**: AWS-managed versions of Prometheus and Grafana. Eliminates operational overhead of self-hosting while retaining open source tooling benefits and avoiding lock-in.

**Cost Estimate**: GBP 6K-9K/year for managed services.

**Recommendation**: Hybrid approach -- AWS CloudWatch for infrastructure metrics and log aggregation (zero setup for AWS services) + Amazon Managed Grafana for custom dashboards including data freshness SLIs and compliance metrics. This provides native AWS integration with the flexibility of Grafana's dashboard capabilities.

**Source Citations**:
- [Grafana Cloud](https://grafana.com/products/cloud/)
- [Grafana on G-Cloud Digital Marketplace](https://www.applytosupply.digitalmarketplace.service.gov.uk/g-cloud/services/469867075438151)
- [Amazon Managed Grafana](https://aws.amazon.com/grafana/)

---

## Category 11: Citizen Frontend (GOV.UK Design System)

**Requirements Addressed**: INT-004, NFR-U-001, NFR-U-002, NFR-C-003, BR-003

**Why This Category**: The citizen-facing fuel price comparison service must use the GOV.UK Design System and meet WCAG 2.2 AA accessibility requirements.

### Recommendation: GOV.UK Platform -- GOV.UK Design System

**Description**: The mandatory frontend framework for UK Government citizen-facing services. Provides accessible, tested UI components, patterns, and styles.

**Cost**: Free (open source, MIT licence). Integration effort only: GBP 0 for framework, development effort included in core build estimate.

**Source Citation**: [GOV.UK Design System](https://design-system.service.gov.uk/)

---

## Total Cost of Ownership (TCO) Summary

### Blended TCO Across All Categories

**Recommended Approach (Blended)**:

| Category | Recommended Option | Year 1 | Year 2 | Year 3 | 3-Year TCO |
|----------|-------------------|--------|--------|--------|------------|
| 1. Fuel Price Data | GOV.UK: Fuel Finder API | GBP 15K | GBP 3K | GBP 3K | GBP 21K |
| 2. Cloud Infrastructure | BUY: AWS eu-west-2 | GBP 65K | GBP 72.5K | GBP 79K | GBP 216.5K |
| 3. Database + Geospatial | BUY: RDS PostgreSQL + PostGIS | GBP 31K | GBP 32.5K | GBP 43K | GBP 106.5K |
| 4. Message Queue | BUY: AWS SQS | GBP 1.2K | GBP 1.8K | GBP 2.3K | GBP 5.3K |
| 5. API Gateway | BUY: AWS API Gateway | GBP 4K | GBP 6K | GBP 8K | GBP 18K |
| 6. Notifications | GOV.UK: Notify | GBP 5K | GBP 500 | GBP 1K | GBP 6.5K |
| 7. Address / Geocoding | GOV.UK: OS Places API | GBP 5K | GBP 0 | GBP 0 | GBP 5K |
| 8. Authentication | GOV.UK: One Login + CMA IdP | GBP 13K | GBP 0 | GBP 0 | GBP 13K |
| 9. Data Validation | ADOPT: Pydantic + GX | GBP 20K | GBP 5K | GBP 5K | GBP 30K |
| 10. Observability | BUY: CloudWatch + Managed Grafana | GBP 8K | GBP 9K | GBP 10K | GBP 27K |
| 11. Citizen Frontend | GOV.UK: Design System | GBP 0 | GBP 0 | GBP 0 | GBP 0 |
| **Custom Dev (Core Service)** | BUILD: Pipeline, Dashboard, Search, Enforcement | GBP 600K | GBP 200K | GBP 200K | GBP 1,000K |
| **TOTAL** | | **GBP 767.2K** | **GBP 330.3K** | **GBP 351.3K** | **GBP 1,448.8K** |

### Alternative Scenarios

**Scenario A: Build Everything Custom**:
- 3-Year TCO: GBP 2,200K-2,800K
- Pros: Maximum control, no vendor dependencies
- Cons: Highest cost, longest delivery (18+ months), highest operational burden
- Risk: Team must maintain message queues, API gateway, monitoring stack

**Scenario B: Buy Everything (Managed SaaS)**:
- 3-Year TCO: GBP 1,800K-2,200K
- Pros: Fastest delivery, lowest operational burden
- Cons: Higher subscription costs, vendor lock-in, less flexibility
- Risk: SaaS price increases, feature limitations

**Scenario C: Open Source Everything (Self-Hosted)**:
- 3-Year TCO: GBP 1,600K-2,000K
- Pros: No licence costs, maximum flexibility, no lock-in
- Cons: Highest operational burden, requires specialist skills
- Risk: Maintenance overhead, security patching burden

**Scenario D: Recommended Blended Approach**:
- 3-Year TCO: GBP 1,445K-1,950K
- Pros: Balance of cost, speed, control, and risk; leverages free GOV.UK platforms; managed services for infrastructure; open source for flexibility
- Cons: Multiple technology choices to manage

### TCO Assumptions

- Engineering rates: GBP 800/day blended rate (mix of contractor and FTE)
- Infrastructure: AWS eu-west-2 pricing (on-demand with 1-year reserved instances for databases)
- SaaS pricing: List prices with 10% annual increase assumption
- Maintenance: 20% of development cost per year for custom builds
- GOV.UK platforms: Free for central government (integration effort only)
- Currency: All costs in GBP; no FX conversion required (AWS GBP billing)

### Risk-Adjusted TCO

| Scenario | Base TCO | Contingency | Risk-Adjusted TCO | Risk Factors |
|----------|----------|-------------|-------------------|--------------|
| Build Everything | GBP 2,500K | +20% | GBP 3,000K | Scope creep, skill gaps, operational complexity |
| Buy (SaaS) | GBP 2,000K | +10% | GBP 2,200K | Price increases, vendor changes |
| Open Source | GBP 1,800K | +15% | GBP 2,070K | Underestimated maintenance, security patching |
| **Recommended Blend** | **GBP 1,450K** | **+12%** | **GBP 1,624K** | Blended risk profile |

---

## Requirements Traceability

### Requirements Coverage Matrix

| Requirement ID | Requirement Description | Research Category | Recommended Solution | Rationale |
|----------------|------------------------|-------------------|---------------------|-----------|
| FR-001 | Forecourt registration | Cat 3 (DB), Cat 7 (Address), Cat 8 (Auth) | RDS PostgreSQL + OS Places + One Login | Address validation via OS Places; data stored in RDS; auth via One Login |
| FR-002 | Manual price submission | Cat 3 (DB), Cat 8 (Auth) | Custom build + RDS | GOV.UK Design System form, validated, stored in RDS |
| FR-003 | API price submission | Cat 1 (Data), Cat 5 (API GW), Cat 9 (Validation) | API Gateway + Pydantic + SQS | Rate limiting via API Gateway; schema validation; async processing |
| FR-004 | Citizen fuel price search | Cat 3 (DB + PostGIS), Cat 7 (Geocoding) | PostGIS proximity queries + CloudFront CDN | Spatial indexing for < 3s p95; CDN for static assets |
| FR-005 | Open data API | Cat 5 (API GW), Cat 1 (Data) | API Gateway + read replica | Public unauthenticated API; rate limited by IP |
| FR-006 | Compliance dashboard | Cat 3 (DB), Cat 10 (Observability) | Custom build + RDS + Grafana | Bespoke enforcement tool; data from RDS |
| FR-007 | Data validation pipeline | Cat 4 (Queue), Cat 9 (Validation) | SQS + Pydantic + Great Expectations | Async processing; schema + plausibility validation |
| FR-008 | Retailer account management | Cat 8 (Auth), Cat 3 (DB) | One Login + RDS | Account management with GOV.UK One Login SSO |
| FR-009 | Retailer notifications | Cat 6 (Notify) | GOV.UK Notify | Free email; low-cost SMS; template-based |
| FR-010 | Audit trail | Cat 3 (DB), Cat 10 (Observability) | RDS (immutable audit table) + S3 (archive) + CloudWatch Logs | Tamper-evident logging; S3 for long-term archive |
| FR-011 | Policy analysis | Cat 3 (DB) | RDS read replica + CSV export | SQL analytics on read replica; CSV/JSON export |
| FR-012 | Technical failure reporting | Cat 3 (DB), Cat 11 (Frontend) | Custom build (GOV.UK Design System form) | Simple web form, stored in RDS |
| FR-013 | Service feedback | Cat 11 (Frontend) | GOV.UK Design System feedback component | Standard GOV.UK pattern |
| FR-014 | CarPlay/Auto API responses | Cat 5 (API GW), Cat 1 (Data) | API Gateway response transformation | format=carplay parameter; simplified schema |
| FR-015 | In-car integration guidelines | Cat 11 (Frontend) | Static content on developer portal | Documentation, not code |
| NFR-P-001 | Citizen search < 3s p95 | Cat 2 (Cloud), Cat 3 (DB) | CloudFront + PostGIS + read replica | CDN + spatial indexing + read isolation |
| NFR-P-002 | 5,000 submissions/min peak | Cat 4 (Queue), Cat 2 (Cloud) | SQS + ECS auto-scaling | Unlimited SQS throughput; ECS scales horizontally |
| NFR-A-001 | 99.9% availability | Cat 2 (Cloud), Cat 3 (DB) | Multi-AZ ECS + Multi-AZ RDS | AWS infrastructure redundancy |
| NFR-A-002 | RPO 15min, RTO 4h | Cat 3 (DB) | RDS PITR + Multi-AZ failover | Continuous replication; automatic failover |
| NFR-SEC-001 | Authentication | Cat 8 (Auth) | One Login + CMA IdP + OAuth 2.0 | Multi-factor for retailers; SSO for staff; client creds for API |
| NFR-SEC-003 | Encryption | Cat 2 (Cloud) | AWS KMS + TLS 1.2+ | AES-256 at rest; TLS in transit |
| NFR-C-002 | Audit logging | Cat 10 (Observability) | CloudWatch Logs + S3 archive | Structured JSON; 7-year retention |
| NFR-I-001 | API standards (REST, OpenAPI) | Cat 5 (API GW) | API Gateway + OpenAPI spec | Native OpenAPI import/export |
| INT-001 | Address gazetteer | Cat 7 (Address) | OS Places API (PSGA) | Free, authoritative, UPRN-based |
| INT-002 | Geocoding | Cat 7 (Address) | OS Places API + PostGIS | API for lookup; PostGIS for runtime proximity |
| INT-003 | GOV.UK Notify | Cat 6 (Notify) | GOV.UK Notify | Mandatory platform |
| INT-006 | CMA Corporate IdP | Cat 8 (Auth) | SAML 2.0 / OIDC federation | Standard SSO integration |
| INT-007 | Companies House API | Cat 7 (Address) | Companies House API (free) | Registration validation |
| INT-008 | Android Auto / Apple CarPlay | Cat 1 (Data), Cat 5 (API GW) | API response transformation | Third-party app responsibility; API optimised responses |

### Coverage Summary

**Requirements with Identified Solutions**:

- 100% of requirements (46/46) have recommended solutions
- 0 requirements need further research
- 4 functional areas require custom development (data ingestion pipeline, compliance dashboard, enforcement tools, citizen search UI) -- these are core bespoke capabilities with no off-the-shelf alternative

---

## UK Government Considerations

### Technology Code of Practice (TCoP) Compliance

| TCoP Point | Status | Notes |
|-----------|--------|-------|
| **1. Define user needs** | Compliant | Research driven by ARC-001-REQ-v2.0 requirements and user personas |
| **2. Make things accessible** | Compliant | GOV.UK Design System mandated; WCAG 2.2 AA compliance |
| **3. Be open and use open source** | Compliant | PostgreSQL, PostGIS, Pydantic, Great Expectations, Grafana -- all open source |
| **4. Make use of open standards** | Compliant | REST, JSON, OAuth 2.0, OpenAPI 3.0, GeoJSON, OGL |
| **5. Use cloud first** | Compliant | AWS public cloud (eu-west-2) recommended |
| **6. Make things secure** | Compliant | NCSC-assessed cloud; Secure by Design; encryption at rest and in transit |
| **7. Make privacy integral** | Compliant | DPIA required; UK GDPR; data minimisation; PII encryption |
| **8. Share, reuse and collaborate** | Compliant | GOV.UK Notify, One Login, Design System, OS Places API all reused |
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
| Companies House API | Registration Validation | Recommended | Free, validates retailer organisations |
| Fuel Finder API | Data Source | Mandatory | Statutory data source; free open data |

### Digital Marketplace Procurement Strategy

**G-Cloud 14** (Cloud hosting, software, support):
- AWS: G-Cloud listed with direct call-off available
- Grafana Cloud: Listed on Digital Marketplace (service 469867075438151)

**Procurement Approach**:
1. AWS infrastructure via G-Cloud 14 direct call-off (established framework)
2. GOV.UK platforms: no procurement required (free cross-government services)
3. Open source tools: no procurement required (MIT/Apache licensed)
4. Custom development: DOS framework or existing delivery partner contract

---

## Integration with Wardley Mapping

### Value Chain Components by Evolution

| Component | Evolution Stage | Recommended Approach | Rationale |
|-----------|----------------|---------------------|-----------|
| Fuel Price Data (Statutory API) | Commodity | GOV.UK Platform | Mandated open data; no differentiation possible |
| Cloud Infrastructure (AWS) | Commodity | Buy Managed Service | Standard utility; pay per use |
| Database (PostgreSQL/PostGIS) | Product/Commodity | Buy Managed (RDS) | Mature product, managed hosting |
| Message Queue (SQS) | Commodity | Buy Managed Service | Standard utility |
| API Gateway | Product | Buy Managed (AWS) | Mature product, standard capability |
| Notifications (GOV.UK Notify) | Commodity | GOV.UK Platform | Government utility service |
| Address/Geocoding (OS Places) | Product | GOV.UK Platform | Government-provided service |
| Authentication (One Login) | Product | GOV.UK Platform | Government identity platform |
| Data Validation Pipeline | Custom | Build Custom | Bespoke business rules specific to fuel price regulations |
| Compliance Dashboard | Custom | Build Custom | Bespoke enforcement tool; no off-the-shelf equivalent |
| Citizen Fuel Price Search | Custom | Build Custom | Core user-facing service with unique regulatory context |
| In-Car API Responses | Custom | Build Custom | Novel format optimisation for automotive platforms |

---

## Integration with SOBC Economic Case

### Options Analysis for SOBC

**Option 0: Do Nothing (Baseline)**:
- Cost: GBP 0
- Benefits: None
- Risk: Statutory obligations unmet; CMA enforcement impossible; citizens have no price transparency

**Option 1: Build Everything Custom** (including infrastructure):
- 3-Year TCO: GBP 2,500K-3,000K (risk-adjusted)
- Benefits: Maximum control
- Risks: Highest cost, longest delivery, highest operational burden

**Option 2: Recommended Blended Approach**:
- 3-Year TCO: GBP 1,450K-1,624K (risk-adjusted)
- Benefits: Balance of cost, speed, and risk; leverages free GOV.UK platforms
- Risks: Moderate; multiple technology choices

**Preferred Option**: Option 2 -- Blended approach

**CAPEX (Initial Investment)**: GBP 767K (Year 1 -- development + infrastructure setup + integration)

**OPEX (Ongoing Annual)**: GBP 330K-351K/year (infrastructure + maintenance + subscriptions)

---

## Vendor Shortlist for Further Evaluation

### Top 3 Vendors/Products Recommended

#### 1. AWS (Amazon Web Services) for Cloud Infrastructure

**Overall Rating**: 5/5

**Strengths**:
- Widest UK Government adoption; cross-government community of practice
- G-Cloud listed; NCSC-assessed; Cyber Essentials Plus; ISO 27001; SOC 2
- 3 availability zones in London (eu-west-2)
- GBP billing; dedicated UK Government support tier

**Concerns**:
- Vendor lock-in for proprietary services (mitigate with abstraction layers)
- Complex pricing (mitigate with FinOps tooling and reserved instances)

#### 2. GOV.UK Notify for Notifications

**Overall Rating**: 5/5

**Strengths**:
- Free for central government email; mandatory under TCoP
- Mature API with Python/Java/Node client libraries
- Template-based messaging with delivery status tracking
- UK data residency; GDPR compliant

**Concerns**:
- Dependency on GDS platform availability (mitigate with retry/dead letter queue)

#### 3. Ordnance Survey Places API for Address and Geocoding

**Overall Rating**: 5/5

**Strengths**:
- Authoritative UK addressing data (AddressBase Premium)
- Free under PSGA for UK central government
- UPRN-based matching -- UK Government standard
- Updated every 6 weeks

**Concerns**:
- Rate limits (600 RPM live) -- mitigate with PostGIS for runtime proximity queries
- 6-week data update cycle -- acceptable for address data (not real-time)

---

## Risks and Mitigations

### Vendor Risks

**VR-1: AWS Vendor Lock-in**
- **Risk**: Proprietary services (SQS, API Gateway) create switching costs
- **Impact**: MEDIUM -- migration effort if AWS relationship changes
- **Likelihood**: LOW -- AWS is the dominant UK Government cloud provider
- **Mitigation**: Use abstraction layers; containerised workloads portable to any Kubernetes; PostgreSQL/PostGIS portable to any cloud; open source observability stack

**VR-2: Fuel Finder API Availability**
- **Risk**: Statutory API outage blocks data freshness SLA
- **Impact**: HIGH -- stale prices undermine citizen trust
- **Likelihood**: LOW -- production service backed by SLA
- **Mitigation**: Implement caching (15-minute price cache, 1-hour station cache per developer guidelines); serve stale data with staleness indicators; retain knowledge of CMA interim feeds as emergency fallback

**VR-3: GOV.UK Platform Dependencies**
- **Risk**: GOV.UK Notify or One Login service degradation
- **Impact**: MEDIUM -- notifications delayed; retailer login impaired
- **Likelihood**: LOW -- government platforms are highly available
- **Mitigation**: Retry with exponential backoff; dead letter queue for notifications; fallback authentication mechanism for emergency access

### Technical Risks

**TR-1: Fuel Finder API Rate Limiting at Scale**
- **Risk**: 30 RPM limit constrains data refresh frequency as third-party adoption grows
- **Impact**: MEDIUM -- potential data freshness degradation
- **Likelihood**: MEDIUM -- rate limit is conservative
- **Mitigation**: Efficient batching (80-batch pagination); incremental sync via effective-start-timestamp; aggressive caching strategy; negotiate higher rate limits with DESNZ/VE3 Global

**TR-2: PostGIS Performance at Scale**
- **Risk**: Proximity queries slow as historical data grows to 165M+ records
- **Impact**: MEDIUM -- citizen search response time degrades
- **Likelihood**: LOW -- PostGIS spatial indexing is highly optimised
- **Mitigation**: Table partitioning by date; read replicas for query isolation; caching of frequently queried areas; archive historical data to warm/cold storage

---

## Next Steps and Recommendations

### Immediate Actions (0-2 weeks)

1. **Stakeholder Review**: Present research findings to CMA Digital Lead and Architecture Review Board
2. **AWS Procurement**: Initiate G-Cloud 14 call-off for AWS infrastructure
3. **Developer Portal Registration**: Register for Fuel Finder API test credentials via GOV.UK One Login
4. **GOV.UK Platform Onboarding**: Register with GOV.UK Notify; request OS Places API PSGA access

### Vendor Evaluation (2-6 weeks)

5. **API Integration POC**: Build proof-of-concept Fuel Finder API client with OAuth 2.0, batch pagination, and incremental sync
6. **PostGIS POC**: Load 8,500 forecourt locations; benchmark proximity query performance
7. **GOV.UK Notify POC**: Configure notification templates for compliance reminders and enforcement actions
8. **Infrastructure POC**: Deploy reference architecture on AWS eu-west-2 with IaC (Terraform/CDK)

### Integration with Other Commands

9. **Update SOBC**: Run `/arckit:sobc` to update Economic Case with TCO data from this research
10. **Create Wardley Map**: Run `/arckit:wardley` to map value chain with evolution positioning
11. **Generate SOW/RFP**: Run `/arckit:sow` to create delivery partner RFP with technical requirements

---

## Appendices

### Appendix A: Research Methodology

**Data Sources**:
- Fuel Finder Developer Portal (developer.fuel-finder.service.gov.uk) -- primary API documentation
- GOV.UK guidance pages -- scheme information and data access
- GitHub (Fuel-Prices-UK Home Assistant integration) -- reverse-engineered API client for endpoint verification
- AWS, Azure pricing pages and calculators
- GOV.UK Notify, One Login, OS Places documentation
- G2, Gartner reviews for vendor maturity assessment
- UK Government Code Repositories (govreposcrape) -- code reuse search across ~21,000 repos
- PyPI and GitHub for open source tool assessment

**Evaluation Criteria**:
- Requirements fit against ARC-001-REQ-v2.0
- UK Government compliance (G-Cloud, NCSC, Cyber Essentials, TCoP)
- 3-year TCO projection with risk adjustment
- Operational burden (managed vs self-hosted)
- Open source preference (TCoP Point 3/4)
- UK data residency (mandatory)
- GOV.UK platform reuse (TCoP Point 8)

**Limitations**:
- ~~Fuel Finder API documentation is hosted in a React SPA which limited automated extraction~~ **Resolved in v4.1**: Official developer portal PDF documentation (5 documents) now available and verified against live portal content
- AWS pricing based on on-demand rates; actual costs will be lower with reserved instances and savings plans
- Custom development estimates assume GBP 800/day blended rate; actual rates depend on delivery model
- Market research valid for approximately 6 months from date of publication

### Appendix B: Glossary

| Term | Definition |
|------|-----------|
| AZ | Availability Zone (isolated data centre within an AWS region) |
| CDN | Content Delivery Network |
| CMA | Competition and Markets Authority |
| DESNZ | Department for Energy Security and Net Zero |
| E10 | Standard unleaded petrol (10% ethanol) |
| E5 | Super unleaded petrol (5% ethanol) |
| B7 | Standard diesel (7% biodiesel) |
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
| PSGA | Public Sector Geospatial Agreement |
| RDS | Relational Database Service (AWS managed PostgreSQL) |
| RPM | Requests Per Minute |
| SDV | Premium/super diesel variant |
| SQS | Simple Queue Service (AWS message queue) |
| TCoP | Technology Code of Practice |
| TCO | Total Cost of Ownership |
| UPRN | Unique Property Reference Number |
| VE3 Global | Designated aggregator for the statutory Fuel Finder scheme |
| WAF | Web Application Firewall |

### Appendix C: Reference Documents

| Document | Type | Source | Path |
|----------|------|--------|------|
| Project Requirements v2.0 | ArcKit Artifact | ArcKit | `projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md` |
| Architecture Principles v1.0 | ArcKit Artifact | ArcKit | `projects/000-global/ARC-000-PRIN-v1.0.md` |
| Research v1.0 (Data Sources) | ArcKit Artifact | ArcKit | `projects/001-uk-fuel-price-transparency-service/research/ARC-001-RSCH-v1.0.md` |
| Research v2.0 (Open Source Tools) | ArcKit Artifact | ArcKit | `projects/001-uk-fuel-price-transparency-service/research/ARC-001-RSCH-v2.0.md` |
| AWS Research v2.0 | ArcKit Artifact | ArcKit | `projects/001-uk-fuel-price-transparency-service/research/ARC-001-AWRS-v2.0.md` |
| Azure Research v2.0 | ArcKit Artifact | ArcKit | `projects/001-uk-fuel-price-transparency-service/research/ARC-001-AZRS-v2.0.md` |
| Motor Fuel Price (Open Data) Regulations 2025 | Legislation | UK Parliament | https://www.legislation.gov.uk/uksi/2025/1356/introduction/made |
| Fuel Finder Developer Portal | API Documentation | DESNZ/VE3 Global | https://www.developer.fuel-finder.service.gov.uk/ |
| Fuel Finder API Authentication | API Documentation | DESNZ/VE3 Global | https://www.developer.fuel-finder.service.gov.uk/api-authentication |
| Fuel Finder Developer Guidelines | API Documentation | DESNZ/VE3 Global | https://www.developer.fuel-finder.service.gov.uk/dev-guideline |
| Fuel Finder API Testing | API Documentation | DESNZ/VE3 Global | https://www.developer.fuel-finder.service.gov.uk/api-testing |
| Fuel Finder Public API | API Documentation | DESNZ/VE3 Global | https://www.developer.fuel-finder.service.gov.uk/public-api |
| Fuel Finder REST API | API Documentation | DESNZ/VE3 Global | https://www.developer.fuel-finder.service.gov.uk/apicontent |
| Fuel Finder Developer Portal PDFs (5 docs) | Official PDF Documentation | DESNZ/VE3 Global | Local: `/fuelapi/` |
| GOV.UK Fuel Price Data Guidance | Government Guidance | GOV.UK | https://www.gov.uk/guidance/access-the-latest-fuel-prices-and-forecourt-data-via-api-or-email |
| CMA Interim Fuel Price Data | Government Guidance | GOV.UK | https://www.gov.uk/guidance/access-fuel-price-data |
| Fuel-Prices-UK (Home Assistant) | Open Source | GitHub | https://github.com/beecho01/Fuel-Prices-UK |
| GOV.UK Notify | Government Platform | GDS | https://www.notifications.service.gov.uk/ |
| GOV.UK One Login | Government Platform | GDS | https://docs.sign-in.service.gov.uk/ |
| OS Places API | Government Platform | Ordnance Survey | https://docs.os.uk/os-apis/accessing-os-apis/os-places-api |
| NCSC Cloud Security Principles | Security Guidance | NCSC | https://www.ncsc.gov.uk/collection/cloud/the-cloud-security-principles |

---

**Generated by**: ArcKit `/arckit:research` agent
**Generated on**: 2026-03-26
**ArcKit Version**: 1.0.3
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: Claude Opus 4.6 (1M context)
