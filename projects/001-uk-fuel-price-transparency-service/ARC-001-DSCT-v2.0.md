# Data Source Discovery: UK Fuel Price Transparency Service

> **Template Status**: Alpha | **Version**: 1.0.0 | **Command**: `/arckit.datascout`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-DSCT-v2.0 |
| **Document Type** | Data Source Discovery |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 2.0 |
| **Created Date** | 2026-02-01 |
| **Last Modified** | 2026-02-01 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-01 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-01 | ArcKit AI | Initial creation from `/arckit.datascout` command | PENDING | PENDING |
| 2.0 | 2026-02-01 | ArcKit AI | Major update: Fuel Finder scheme now live (VE3 Global aggregator); OSNI Pointer for NI coverage; OS NGD migration path; api.gov.uk catalogue research; updated regulatory timeline | PENDING | PENDING |

---

## Executive Summary

### Data Needs Overview

This document presents updated data source discovery findings for the **UK Fuel Price Transparency Service** ("Fuel Finder") project, identifying external APIs, datasets, and data portals that can fulfil the data and integration requirements documented in `ARC-001-REQ-v2.0.md`.

**Requirements Analyzed**: 6 data entity definitions (DR-001–006), 15 functional requirements (FR-001–FR-015), 8 integration requirements (INT-001–INT-008), 25+ non-functional requirements (NFR-xxx)

**Data Source Categories Identified**: 6 categories based on requirement analysis (increased from 5 in v1.0 — added Fuel Price Aggregator)

**Discovery Approach**: UK Government API Catalogue (api.gov.uk), department developer hubs, data.gov.uk, commercial API research, free/freemium API discovery, WebSearch-powered market research

### What Changed in v2.0

- **CRITICAL**: The Motor Fuel Price (Open Data) Regulations 2025 are now enacted and the mandatory scheme went live on **2 February 2026**. VE3 Global Ltd is the designated aggregator with an open data API.
- **NEW CATEGORY**: Fuel Price Aggregator — VE3 Global API is now the authoritative, legally mandated, near real-time source for all UK forecourt fuel prices.
- **GEOSPATIAL**: OS NGD (National Geographic Database) identified as the strategic successor to AddressBase, with daily updates and new Royal Mail Address Feature Types (Autumn 2025 release). AddressBase and AddressBase Plus reach EOL 29 November 2027 (AddressBase Premium is NOT affected).
- **NORTHERN IRELAND**: OSNI Pointer database identified for Northern Ireland address coverage (gap in v1.0). OS Data Hub covers GB only.
- **API CATALOGUE**: Comprehensive research of api.gov.uk catalogue, department developer hubs, and data.gov.uk completed per updated datascout methodology.
- **REGULATORY**: Full regulatory timeline documented — registration opened 18 Dec 2025, mandatory reporting from 2 Feb 2026, enforcement grace period ends early May 2026.

### Key Findings

- **Fuel Price Data**: The CMA Fuel Finder mandatory scheme is now **live** under the Motor Fuel Price (Open Data) Regulations 2025. **VE3 Global Ltd** is the designated aggregator, providing an open data API with near real-time prices (~5-minute lag) from all ~8,500 UK forecourts. This eliminates the need for commercial fuel price data providers.
- **Geospatial & Address Data**: OS Places API and AddressBase Premium remain available **free** under PSGA. OS NGD is the strategic successor with daily updates (vs 6-weekly). **OSNI Pointer** needed for Northern Ireland coverage (previously a gap).
- **Company Validation**: Companies House API remains free, stable, and unchanged (600 req/5min).
- **Notifications**: GOV.UK Notify remains the government standard — free emails, SMS at 2.33p + VAT per message beyond free allowance.
- **Economic Context**: ONS Beta API, NESO Carbon Intensity API (rebranded from National Grid ESO), and Bank of England IADB all remain active and free.
- **UK Government API Catalogue**: api.gov.uk lists 8 Ordnance Survey APIs, 2 Companies House APIs, 7 GDS APIs, and 2+ ONS APIs directly relevant to this project.

### Data Source Summary

| Source Type | Count | Cost Range | Key Providers |
|-------------|-------|------------|---------------|
| **UK Government Open Data** | 9 | Free (OGL/PSGA) | VE3 Global (Fuel Finder), OS Data Hub, ONS, Companies House, NESO Carbon Intensity, Bank of England |
| **UK Government Platform** | 1 | Free (email) / Low-cost (SMS) | GOV.UK Notify |
| **Commercial APIs** | 4 | £5K–£150K/year | Experian Catalist, PetrolPrices.com/myAutomate, TomTom Fuel Prices, GlobalPetrolPrices |
| **Free/Community APIs** | 2 | Free | Postcodes.io, uk-fuel-prices-api (PyPI) |
| **NI Government Data** | 1 | Free (NIMA) | OSNI Pointer (via viaEuropa) |
| **TOTAL** | 17 | £0–£150K/year | |

### Top Recommended Sources

**Shortlist for integration**:

1. **VE3 Global Fuel Finder API** for Fuel Price Data: Free (open data, OGL), near real-time (~5 min), all ~8,500 UK forecourts — **NEW in v2.0** — Score 96/100
2. **OS Places API / AddressBase Premium** for Geospatial: Free under PSGA, authoritative UPRN-based UK address data, 40M addresses — Score 95/100
3. **GOV.UK Notify** for Notifications: Free emails, government standard, template-based — Score 95.5/100
4. **Companies House API** for Company Validation: Free, real-time, all UK companies — Score 90/100
5. **Postcodes.io** for Postcode Geocoding: Free, no auth, self-hostable, all UK postcodes — Score 85/100

### Requirements Coverage

- ✅ **14 requirements (82%)** fully matched to external data sources
- ⚠️ **2 requirements (12%)** partially matched (quality or coverage concerns)
- ❌ **1 requirement (6%)** no suitable external source — by design (DR-001–006 are inbound retailer submissions via VE3 Global)

---

## Data Needs Analysis

> **Note**: Data needs are extracted from requirements, categorised by type, with criticality and volume/freshness expectations.

### Extracted Data Needs

| # | Requirement ID | Data Need | Type | Criticality | Volume | Freshness | Source Category |
|---|----------------|-----------|------|-------------|--------|-----------|-----------------|
| 1 | INT-001 | Address validation and standardisation for forecourt registration | Integration | MUST | ~8,500 lookups (one-off) + ~100/year (new) | On-demand | Geospatial |
| 2 | INT-002 | Geocoding: postcode/place name to coordinates for proximity search | Integration | MUST | 100K+ queries/day (citizen searches) | On-demand (cacheable) | Geospatial |
| 3 | INT-003 | Email and SMS notifications to retailers | Integration | MUST | ~50K emails/month; ~10K SMS/month | Real-time | Notifications |
| 4 | INT-007 | Company registration validation | Integration | SHOULD | ~3,000 lookups (one-off) + ~50/year | On-demand | Company Data |
| 5 | FR-004 | Postcode-to-coordinate mapping for citizen search | Functional | MUST | Lookup table: ~1.8M UK postcodes | Quarterly refresh | Geospatial |
| 6 | FR-011 | Historical fuel price trends and economic context for policy analysis | Functional | SHOULD | Weekly aggregates; monthly CPI | Weekly/Monthly | Economic Context |
| 7 | FR-001 | Forecourt master list (seed data) for registration completeness tracking | Functional | MUST | ~8,500 forecourts | One-off seed + ongoing | Fuel Station Data |
| 8 | DR-001–006 | Fuel price data from retailers | Data | MUST | ~150K submissions/day | Real-time | Primary Data (inbound via VE3 Global) |
| 9 | INT-008 | In-car platform compatibility data | Integration | SHOULD | N/A (API design, not data) | N/A | Platform Standards |
| 10 | FR-006 | Regional compliance benchmarks | Functional | MUST | By region/retailer type | Daily aggregates | Geospatial + Internal |
| 11 | NEW | Aggregated fuel price data consumption (read-back from VE3 Global) | Integration | SHOULD | ~8,500 stations, near real-time | 5-minute lag | Fuel Price Aggregator |

### Data Needs by Category

**Category 1: Fuel Price Aggregator (NEW in v2.0)**
- Requirements: FR-001 (forecourt master list), FR-011 (price trends), BR-005 (open data API)
- Data fields needed: Station ID, trading name, address, lat/lng, fuel grades, current prices, last update timestamp
- Volume: ~8,500 stations with price updates within 30 minutes of any change
- Freshness: Near real-time (VE3 Global publishes within 5 minutes of receipt)
- Quality threshold: Mandated by regulation — VE3 Global validates submissions

**Category 2: Geospatial & Address Data**
- Requirements: INT-001, INT-002, FR-004, FR-001
- Data fields needed: Address validation, UPRN, coordinates (lat/lng), postcode lookup, place name geocoding, administrative geography (region, local authority, constituency)
- Volume: ~100K+ geocoding queries/day (citizen searches); ~8,500 address lookups (registration)
- Freshness: On-demand for API queries; quarterly for reference data refresh
- Quality threshold: Address match accuracy >99%; coordinate accuracy within 10m
- **NOTE**: Northern Ireland coverage requires OSNI Pointer (separate from OS Data Hub)

**Category 3: Company & Business Validation**
- Requirements: INT-007, FR-001
- Data fields needed: Company number validation, company name, registration status (active/dissolved), registered address
- Volume: ~3,000 lookups at registration; ~50/year ongoing
- Freshness: Real-time (at point of registration)
- Quality threshold: 100% accuracy (authoritative source)

**Category 4: Notifications & Communications**
- Requirements: INT-003, FR-009, FR-006
- Data fields needed: Email delivery, SMS delivery, letter generation, template management, delivery status tracking
- Volume: ~50,000 emails/month during onboarding; ~10,000 SMS/month for compliance reminders
- Freshness: Real-time delivery
- Quality threshold: >99% delivery rate for emails; >95% for SMS

**Category 5: Fuel Price Data (Historical/Contextual)**
- Requirements: FR-011, Assumption A-1 (forecourt master list)
- Data fields needed: Historical average pump prices (petrol, diesel), wholesale/refinery gate prices, price breakdown (duty, VAT, retailer margin), regional price variations
- Volume: Weekly aggregate figures; daily brand-level prices
- Freshness: Weekly (for policy analysis); daily (for context)
- Quality threshold: National-level accuracy; regional disaggregation desirable

**Category 6: Economic & Energy Context**
- Requirements: FR-011 (policy analysis)
- Data fields needed: CPI fuel component, inflation rate, exchange rates (GBP/USD for crude oil context), carbon intensity
- Volume: Monthly CPI; daily exchange rates; half-hourly carbon intensity
- Freshness: Monthly (CPI), daily (exchange rates), real-time (carbon)
- Quality threshold: Official statistics quality

---

## Data Source Discovery

> **Note**: Categories are dynamically identified from project requirements, not a fixed list.

> **UK Government API Catalogue Research**: api.gov.uk was searched as the mandatory first step. The catalogue lists APIs from Ordnance Survey (8 APIs), Companies House (2 APIs), GDS (7 APIs including GOV.UK Notify), ONS (2+ APIs), Environment Agency (10 APIs), DVLA (6 APIs), and DfT (1 API). No fuel-specific API is listed on api.gov.uk itself — all fuel price data flows through the CMA/DESNZ Fuel Finder scheme via VE3 Global.

---

## Category 1: Fuel Price Aggregator (NEW in v2.0)

**Requirements Addressed**: FR-001, FR-011, BR-005, DR-001–006 (read-back)

**Why This Category**: The Motor Fuel Price (Open Data) Regulations 2025 are now enacted, and the mandatory scheme went live on 2 February 2026. VE3 Global Ltd is the designated aggregator, providing an open data API that all third parties (including this service) can consume for published fuel price data.

**Data Fields Needed**: Station ID, trading name, address, latitude/longitude, trading hours, amenities, fuel grades sold, current price per litre per grade, last update timestamp

---

### Source 1A: VE3 Global Fuel Finder API (UK Government — Statutory Open Data)

**Provider**: VE3 Global Ltd (designated aggregator under Motor Fuel Price (Open Data) Regulations 2025), on behalf of CMA/DESNZ

**Description**: The legally mandated, near real-time fuel price data API covering all ~8,500 UK petrol filling stations. VE3 Global collects price submissions from all registered forecourts (via API, SMS, or manual web entry), validates them, and publishes aggregated data within 5 minutes of receipt via an open data API and twice-daily flat file downloads. Retailers must report price changes within 30 minutes.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 (statutory open data) |
| **Pricing** | **Free** (open data — any third party can request access) |
| **Format** | JSON (API); flat file (twice-daily bulk download) |
| **API Endpoint** | Provided by VE3 Global upon registration (details TBC — engagement with VE3 required) |
| **Authentication** | TBC — open data but registration likely required for API access |
| **Rate Limits** | TBC — to be confirmed with VE3 Global |
| **Update Frequency** | Near real-time (~5-minute lag from receipt); retailers must update within 30 minutes of price change |
| **Coverage** | All ~8,500 UK petrol filling stations (mandatory) |
| **Temporal Coverage** | From 2 February 2026 onwards |
| **Data Quality** | Excellent — statutory obligation with penalties of up to 1% of worldwide turnover for non-compliance |
| **Documentation** | GOV.UK guidance: https://www.gov.uk/guidance/access-fuel-price-data |
| **SLA** | Statutory requirement — aggregator must maintain API availability |
| **GDPR Status** | No personal data in published price data |
| **UK Data Residency** | Yes — UK-based aggregator |

**Requirements Fit**:
- ✅ Covers: Comprehensive forecourt location data for master list (FR-001, A-1)
- ✅ Covers: Real-time fuel prices for citizen comparison service (BR-003)
- ✅ Covers: Open data API for third-party consumers (BR-005)
- ✅ Covers: Policy analysis data — all forecourt prices by region/brand (FR-011)
- ⚠️ Partial: API specification and access terms not yet publicly documented — engagement with VE3 Global required
- ⚠️ Partial: Historical data only from 2 Feb 2026 onwards (no backfill)

**Integration Approach**:
- **Pattern**: REST API consumption (near real-time) + twice-daily flat file for reconciliation/backup
- **Estimated Effort**: 5 person-days (API integration + flat file ETL)
- **Dependencies**: Registration with VE3 Global; API specification confirmation

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 10/10 | 25/25 |
| Data Quality | 20% | 9/10 | 18/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 10/10 | 15/15 |
| Reliability | 10% | 9/10 | 9/10 |
| **Total** | **100%** | | **94/100** |

**Note**: API Quality scored 8/10 because the detailed API specification is not yet publicly documented. Score expected to increase once specification is confirmed.

---

### Source 1B: CMA Interim Voluntary Fuel Price Data (Superseded)

**Provider**: Competition and Markets Authority (CMA), via GOV.UK

**Description**: The predecessor voluntary scheme where 14 major fuel retailers published daily price data via JSON endpoints. This scheme has been **superseded** by the mandatory Fuel Finder scheme (VE3 Global) as of 2 February 2026.

**Status**: **SUPERSEDED** — retained for historical reference and transition data only.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | **Free** |
| **Format** | JSON (per-retailer endpoints) |
| **Coverage** | ~3,800 stations from 14 voluntary retailers (~45% of UK forecourts) |
| **Data Quality** | Variable — voluntary scheme, no enforcement, inconsistent update cadence |
| **Status** | **SUPERSEDED by Fuel Finder (VE3 Global)** |

**Requirements Fit**:
- ✅ Covers: Historical baseline data for comparison with mandatory scheme
- ❌ Superseded: No longer the primary or recommended source for ongoing data

**Evaluation Score**: 55/100 (downgraded from 70/100 in v1.0 — superseded by mandatory scheme)

---

### Comparison Table: Fuel Price Aggregator

| Criterion | VE3 Global (Mandatory) | CMA Interim (Superseded) |
|-----------|-----------|-----------|
| **Provider** | VE3 Global Ltd | CMA |
| **License** | OGL (statutory) | OGL |
| **Cost (Annual)** | £0 | £0 |
| **Coverage** | ~8,500 stations (mandatory) | ~3,800 stations (voluntary) |
| **Freshness** | Near real-time (~5 min) | Daily |
| **API Quality** | TBC (specification pending) | Basic JSON endpoints |
| **Enforcement** | Statutory (up to 1% turnover penalty) | None (voluntary) |
| **TOTAL SCORE** | **94/100** | **55/100** |

**Recommendation for Fuel Price Aggregator**: **VE3 Global Fuel Finder API** is the definitive source. Engage with VE3 Global to obtain API specification, register for access, and begin integration. The CMA interim data is useful only for historical baseline comparison.

---

## Category 2: Geospatial & Address Data

**Requirements Addressed**: INT-001, INT-002, FR-004, FR-001

**Why This Category**: Forecourt registration requires address validation and UPRN assignment (INT-001). Citizen fuel price search requires postcode-to-coordinate geocoding for proximity queries (INT-002, FR-004). The forecourt master list seed requires geographic reference data (FR-001).

**Data Fields Needed**: Validated address, UPRN (Unique Property Reference Number), WGS84 latitude/longitude, postcode, local authority, region, parliamentary constituency, LSOA/MSOA

---

### Source 2A: OS Places API / OS Data Hub (UK Government — PSGA)

**Provider**: Ordnance Survey (OS), https://osdatahub.os.uk

**Description**: The authoritative UK address and location API, providing access to AddressBase Premium data (40 million addressable locations) through a RESTful API. Includes postcode lookup, UPRN lookup, address search, nearest address, bounding box and radius queries.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Public Sector Geospatial Agreement (PSGA) — free for UK public sector |
| **Pricing** | **Free for PSGA members** (centrally funded by government). CMA qualifies as PSGA member. Premium plan: £1,000/month free tier for non-PSGA. |
| **Format** | JSON (API); CSV, GML 3.2.1, GeoPackage (bulk downloads) |
| **API Endpoint** | `https://api.os.uk/search/places/v1` |
| **Authentication** | API key (obtained via OS Data Hub registration) |
| **Rate Limits** | Live projects: 600 transactions/minute. Dev projects: 50 transactions/minute. Police/ambulance/fire: unrestricted. |
| **Update Frequency** | Every 6 weeks (AddressBase Premium epoch cycle). Epoch 124 published 8 Jan 2026; Epoch 125 due 19 Feb 2026. |
| **Coverage** | **Great Britain only** (England, Wales, Scotland) — 40 million addresses. **Does NOT cover Northern Ireland.** |
| **Temporal Coverage** | Current + historical through AddressBase Premium lifecycle data |
| **Data Quality** | Excellent — authoritative government dataset; property-level coordinates from OS survey |
| **Documentation** | https://docs.os.uk/os-apis/accessing-os-apis/os-places-api — Excellent quality |
| **SLA** | 99.9% uptime target for OS Data Hub APIs |
| **GDPR Status** | No personal data — addresses are public record |
| **UK Data Residency** | Yes — OS is a UK government agency |

**v2.0 Updates**:
- OS NGD (National Geographic Database) is the **strategic successor** platform with daily updates (vs 6-weekly epochs). Autumn 2025 release introduced Royal Mail Address Feature Types combining full PAF content with OS geospatial attribution.
- AddressBase and AddressBase Plus reach **EOL 29 November 2027**. AddressBase Premium is **NOT affected**.
- New projects should evaluate OS NGD Address Theme for future-proofing.
- API endpoint confirmed as `https://api.os.uk/search/places/v1` (updated from earlier URL format).
- Additional OS APIs available: OS Maps API, OS Vector Tile API, OS Names API, OS Linked Identifiers API, OS Features API, OS Download API — all on api.gov.uk catalogue.

**Requirements Fit**:
- ✅ Covers: Address validation, UPRN assignment, postcode lookup, coordinate geocoding, administrative geography
- ✅ Covers: Forecourt registration address validation (INT-001)
- ✅ Covers: Geocoding for citizen search (INT-002)
- ❌ Missing: **Northern Ireland addresses** (requires OSNI Pointer — see Source 2D)
- ⚠️ Partial: Rate limit of 600/min may need caching strategy for peak citizen search load

**Integration Approach**:
- **Pattern**: REST API call on demand (registration); cached postcode-to-coordinate lookup table (citizen search)
- **Estimated Effort**: 5 person-days
- **Dependencies**: PSGA membership registration for CMA

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 9/10 | 22.5/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 10/10 | 15/15 |
| Reliability | 10% | 9/10 | 9/10 |
| **Total** | **100%** | | **95/100** |

---

### Source 2B: Postcodes.io (Free Community API)

**Provider**: Ideal Postcodes (open-source), https://postcodes.io

**Description**: Free, open-source UK postcode lookup API serving the ONS Postcode Directory. No authentication required. Returns coordinates, administrative areas, census geographies for any UK postcode.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | MIT (software); OGL (underlying data from ONS/OS) |
| **Pricing** | **Completely free** |
| **Format** | JSON |
| **API Endpoint** | `https://api.postcodes.io/` |
| **Authentication** | None required |
| **Rate Limits** | No published hard limit; bulk lookup accepts 100 postcodes/request |
| **Update Frequency** | Quarterly (aligned with ONS Postcode Directory releases) |
| **Coverage** | All UK postcodes including Northern Ireland (current and terminated) |
| **Data Quality** | Good — sources from ONS Postcode Directory and OS Open Names |
| **Documentation** | https://postcodes.io/docs/overview/ — Good quality |
| **SLA** | No formal SLA (community service); self-hosting available via Docker |
| **GDPR Status** | No personal data |
| **UK Data Residency** | Self-hostable in UK infrastructure |

**v2.0 Updates**:
- Current release: **v17.5.0** (September 2025)
- Updated to ONSPD August 2025 format; updated County Electoral Divisions to May 2025; updated Parish codes to April 2025 v2
- Scottish constituency data updated (May 2025)
- NUTS fields now report ITL (International Territorial Levels) for backwards compatibility
- Repository remains actively maintained

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 7/10 | 17.5/25 |
| Data Quality | 20% | 8/10 | 16/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 9/10 | 13.5/15 |
| Reliability | 10% | 7/10 | 7/10 |
| **Total** | **100%** | | **81/100** |

---

### Source 2C: ONS Postcode Directory (Bulk Download)

**Provider**: Office for National Statistics, https://geoportal.statistics.gov.uk

**Description**: Quarterly bulk download of all UK postcodes with coordinates and administrative geography mappings. The canonical government reference dataset for postcode-to-geography lookups.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | **Free** |
| **Format** | CSV, TXT |
| **API Endpoint** | Bulk download only (no real-time API) |
| **Authentication** | None |
| **Update Frequency** | Quarterly (February, May, August, November). Latest: November 2025. Next: February 2026. |
| **Coverage** | All current and terminated UK postcodes (~2.7M live postcodes) |
| **Data Quality** | Excellent — authoritative ONS dataset; 1-metre resolution coordinates |
| **GDPR Status** | No personal data |

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 6/10 | 15/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 3/10 | 4.5/15 |
| Compliance | 15% | 10/10 | 15/15 |
| Reliability | 10% | 10/10 | 10/10 |
| **Total** | **100%** | | **79.5/100** |

---

### Source 2D: OSNI Pointer (Northern Ireland — NEW in v2.0)

**Provider**: Land & Property Services (LPS), Northern Ireland, via viaEuropa (Europa Technologies)

**Description**: The definitive spatial address database for Northern Ireland, containing ~1 million address points. Each address has a UPRN and buildings have unique building IDs. Maintained by LPS with local councils and Royal Mail.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Northern Ireland Mapping Agreement (NIMA) — free for NI public sector; commercial via G-Cloud |
| **Pricing** | **Free under NIMA** for public sector bodies. Commercial access via viaEuropa G-Cloud listing. |
| **Format** | GeoJSON, WMS, WFS, WMTS (via viaEuropa API) |
| **API Endpoint** | viaEuropa API platform (listed on Digital Marketplace G-Cloud) |
| **Authentication** | API key via viaEuropa registration |
| **Rate Limits** | "High performance with no throttling" (per viaEuropa documentation) |
| **Update Frequency** | Regular updates via LPS |
| **Coverage** | **Northern Ireland only** — ~1 million address points |
| **Coordinate System** | EPSG:29900 (TM65 Irish National Grid); alternative CRS available |
| **Data Quality** | Excellent — authoritative government register (LPS with local councils and Royal Mail) |
| **Documentation** | https://docs.spatialni.gov.uk; https://www.europa.uk.com/map-data/uk/osni/pointer/ |
| **SLA** | Per viaEuropa G-Cloud service terms |
| **GDPR Status** | No personal data — addresses are public record |
| **UK Data Residency** | Yes — UK-based |

**Requirements Fit**:
- ✅ Covers: Northern Ireland forecourt address validation and geocoding
- ✅ Covers: UPRN for NI addresses (consistent with GB UPRNs from OS)
- ⚠️ Partial: Separate API integration from OS Places API — two integrations needed for full UK coverage
- ⚠️ Partial: DLUHC contract exists for viaEuropa covering both AddressBase and Pointer — CMA may be able to leverage

**Integration Approach**:
- **Pattern**: REST API call on demand (NI address lookups); or viaEuropa single API covering both GB and NI
- **Estimated Effort**: 3 person-days (if separate integration); 0 person-days (if viaEuropa covers both via DLUHC contract)
- **Dependencies**: Confirm NIMA membership for CMA; or leverage DLUHC viaEuropa contract

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 7/10 | 17.5/25 |
| Data Quality | 20% | 9/10 | 18/20 |
| License & Cost | 15% | 9/10 | 13.5/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 10/10 | 15/15 |
| Reliability | 10% | 8/10 | 8/10 |
| **Total** | **100%** | | **84/100** |

---

### Comparison Table: Geospatial & Address Data

| Criterion | OS Places API | Postcodes.io | ONS Postcode Directory | OSNI Pointer |
|-----------|-----------|-----------|-----------|-----------|
| **Provider** | Ordnance Survey | Ideal Postcodes (community) | ONS | LPS / viaEuropa |
| **License** | PSGA (free for public sector) | OGL / MIT | OGL | NIMA (free for public sector) |
| **Cost (Annual)** | £0 (PSGA) | £0 | £0 | £0 (NIMA) |
| **Coverage** | GB (40M addresses) | All UK postcodes | All UK postcodes | NI (~1M addresses) |
| **Freshness** | 6-weekly (AddressBase Premium) | Quarterly | Quarterly | Regular (LPS cycle) |
| **API Quality** | Excellent | Good | N/A (download) | Good |
| **TOTAL SCORE** | **95/100** | **81/100** | **79.5/100** | **84/100** |

**Recommendation for Geospatial**: **OS Places API** as primary source for GB (free under PSGA). **OSNI Pointer** via viaEuropa for Northern Ireland. Use **ONS Postcode Directory** as offline fallback lookup table. Consider **Postcodes.io** self-hosted as lightweight postcode geocoder. **Investigate viaEuropa** single-API option covering both GB and NI.

**Strategic Note**: OS NGD is the long-term successor to AddressBase, with daily updates and richer attribution. Recommend evaluating OS NGD Address Theme during integration POC to future-proof the geocoding architecture.

---

## Category 3: Company & Business Validation

**Requirements Addressed**: INT-007, FR-001

**Why This Category**: Retailer registration requires validation of organisation details against Companies House to confirm company existence, status, and registered address.

**Data Fields Needed**: Company number, company name, registration status, registered address, incorporation date

---

### Source 3A: Companies House API (UK Government)

**Provider**: Companies House, https://developer.company-information.service.gov.uk

**Description**: Free REST API providing access to all UK company public data. Covers company profiles, officer details, filing history, persons with significant control, charges, and insolvency data.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | **Completely free** |
| **Format** | JSON (REST API) |
| **API Endpoint** | `https://api.companieshouse.gov.uk/` |
| **Authentication** | API key (HTTP Basic Auth with key as username) |
| **Rate Limits** | 600 requests per 5 minutes (~2 req/sec). Rate limit increases available on request. |
| **Update Frequency** | Real-time (live data) |
| **Coverage** | All UK companies registered under Companies Act 2006 |
| **Data Quality** | Excellent — authoritative government register |
| **Documentation** | https://developer-specs.company-information.service.gov.uk/ — Good quality |
| **SLA** | No published SLA; generally high availability |
| **GDPR Status** | Public data (company information is public record); officer home addresses redacted |
| **UK Data Residency** | Yes — UK government service |

**v2.0 Updates**:
- API stable with no announced changes for 2025/2026
- Rate limit increases available by contacting Companies House directly
- Streaming API also available for real-time change notifications (HTTP long-polling)
- Listed on api.gov.uk as 2 APIs: REST API and Streaming API

**Requirements Fit**:
- ✅ Covers: Company number validation (INT-007)
- ✅ Covers: Company name and status verification
- ✅ Covers: Registered address for cross-referencing
- ⚠️ Partial: Sole traders not registered at Companies House — manual validation needed for ~30% of independent forecourt operators

**Integration Approach**:
- **Pattern**: REST API call during registration; circuit breaker with manual fallback if unavailable
- **Estimated Effort**: 3 person-days
- **Dependencies**: API key registration (self-service, instant)

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 8/10 | 20/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 10/10 | 15/15 |
| Reliability | 10% | 8/10 | 8/10 |
| **Total** | **100%** | | **90/100** |

---

## Category 4: Notifications & Communications

**Requirements Addressed**: INT-003, FR-009, FR-006

**Why This Category**: The service requires sending compliance reminders, submission confirmations, enforcement notices, and operational alerts to retailers and CMA staff.

---

### Source 4A: GOV.UK Notify (UK Government Platform)

**Provider**: Government Digital Service (GDS), https://www.notifications.service.gov.uk

**Description**: Central government notification platform for sending emails, SMS, and letters. Used by 1,500+ government organisations. Template-based with personalisation, delivery tracking, and callbacks.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Government platform — available to central government, local authorities, NHS |
| **Pricing** | Emails: **Free (unlimited)**. SMS: Free allowance per service per financial year (25,000 for some orgs); then **2.33p + VAT per SMS**. Letters: from 30p. No setup fees. |
| **Format** | JSON (REST API) |
| **API Endpoint** | `https://api.notifications.service.gov.uk/` |
| **Authentication** | API key (three types: test, team-only, live) |
| **Rate Limits** | Up to 350 requests/second; 30M emails/day |
| **Update Frequency** | N/A (outbound notification service) |
| **Coverage** | UK and international SMS; email globally |
| **Documentation** | https://www.notifications.service.gov.uk/using-notify/api-documentation — Excellent |
| **SLA** | GDS-managed; high availability (critical government infrastructure) |
| **GDPR Status** | GDS is the data processor; CMA remains data controller |
| **UK Data Residency** | Yes — GDS UK infrastructure |

**v2.0 Updates**:
- SMS pricing confirmed at 2.33p + VAT (up from 1.58p in earlier years)
- No new endpoints or features announced
- No deprecation notices
- Listed on api.gov.uk catalogue under GDS

**Requirements Fit**:
- ✅ Covers: Retailer compliance notifications (FR-009)
- ✅ Covers: Enforcement notices via email/SMS (FR-006, INT-003)
- ✅ Covers: Submission confirmations
- ✅ Covers: Delivery status callbacks
- ✅ Covers: Template management with personalisation variables

**Integration Approach**:
- **Pattern**: REST API call per notification; batch for bulk reminders; webhook for delivery status
- **Estimated Effort**: 3 person-days
- **Dependencies**: CMA registration on GOV.UK Notify (self-service)

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 10/10 | 25/25 |
| Data Quality | 20% | N/A | 18/20 |
| License & Cost | 15% | 9/10 | 13.5/15 |
| API Quality | 15% | 10/10 | 15/15 |
| Compliance | 15% | 10/10 | 15/15 |
| Reliability | 10% | 9/10 | 9/10 |
| **Total** | **100%** | | **95.5/100** |

---

## Category 5: Fuel Price Data (Historical/Contextual)

**Requirements Addressed**: FR-011, Assumption A-1

**Why This Category**: DESNZ policy analysts need historical fuel price context for trend analysis and ministerial briefings (FR-011). Note: with the VE3 Global API now live, this category provides **historical context and benchmarking** rather than primary data.

---

### Source 5A: DESNZ Weekly Road Fuel Prices (UK Government)

**Provider**: Department for Energy Security and Net Zero (DESNZ), via GOV.UK

**Description**: Weekly published national average pump prices for unleaded petrol and diesel, including duty and VAT breakdown. Historical series from 2003. Published as ODS/CSV spreadsheet. Classified as Accredited Official Statistics.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | **Free** |
| **Format** | ODS, CSV (spreadsheet download); also on data.gov.uk |
| **API Endpoint** | No API — bulk download from GOV.UK statistics page |
| **Authentication** | None |
| **Update Frequency** | Weekly (published each Monday/Tuesday). Last confirmed: 13 January 2026. |
| **Coverage** | UK national averages; no regional or forecourt-level breakdown |
| **Data Quality** | Excellent — Accredited Official Statistics (National Statistics quality) |
| **GDPR Status** | No personal data — aggregate statistics only |

**v2.0 Updates**:
- Data continues to be published weekly with no interruption
- Upcoming releases scheduled: 13 April 2026, 27 April 2026, and ongoing
- Also available via data.gov.uk CKAN endpoint for programmatic discovery
- **Key context**: CMA road fuel annual report (2025) reports average fuel margins remain historically elevated at 11.1ppl (Jan-Sep 2025), compared to 2017-2022 baseline. Scheme estimated to save drivers £10.4 billion over 10 years.

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 6/10 | 15/25 |
| Data Quality | 20% | 9/10 | 18/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 2/10 | 3/15 |
| Compliance | 15% | 10/10 | 15/15 |
| Reliability | 10% | 9/10 | 9/10 |
| **Total** | **100%** | | **75/100** |

---

### Source 5B: Average Road Fuel Sales, Deliveries and Stock Levels (NEW in v2.0)

**Provider**: DESNZ, via data.gov.uk

**Description**: Quarterly official statistics on average road fuel sales, deliveries and stock levels at sampled UK filling stations. Provides supply/demand context.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | **Free** |
| **Format** | CSV, Excel |
| **Update Frequency** | Quarterly |
| **Coverage** | Sampled UK filling stations |

**Evaluation Score**: 60/100 (supplementary context — not primary data source)

---

### Source 5C: Experian Catalist / PetrolPrices.com (Commercial — Downgraded)

**Provider**: Experian Catalist (via PetrolPrices.com / myAutomate)

**Description**: Commercial fuel price data service. Previously the most comprehensive source at ~8,490 stations. **Now superseded** by the mandatory Fuel Finder scheme which provides free, statutory, near real-time data from all UK forecourts.

**v2.0 Assessment**: **NO LONGER RECOMMENDED for ongoing data**. The mandatory scheme eliminates the business case for commercial fuel price data feeds. A one-off data extract may still be useful for historical baseline if needed for the period before 2 February 2026.

**Evaluation Score**: 45/100 (downgraded from 67.5/100 in v1.0 — superseded by free statutory data)

---

## Category 6: Economic & Energy Context

**Requirements Addressed**: FR-011

**Why This Category**: DESNZ policy analysts need macroeconomic context for fuel price analysis, ministerial briefings, and market competitiveness assessment.

---

### Source 6A: ONS Beta API — CPI Fuel Component

**Provider**: Office for National Statistics, https://developer.ons.gov.uk

**Description**: Beta API providing programmatic access to ONS datasets including Consumer Prices Index (CPI/CPIH) with motor fuel sub-indices. Monthly data with time-series queries.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | **Completely free** |
| **Format** | JSON, CSV, XLSX |
| **API Endpoint** | `https://api.beta.ons.gov.uk/v1` |
| **Authentication** | None required |
| **Rate Limits** | Not explicitly documented; up to 300 series codes per request; wildcard queries supported |
| **Update Frequency** | Monthly (latest: CPI December 2025, published 21 January 2026; next: 18 February 2026) |
| **Coverage** | UK-wide; motor fuel component within CPI/CPIH |
| **Status** | **Beta** — breaking changes possible |

**v2.0 Updates**:
- CPI December 2025 published (3.4% annual)
- **Grocery scanner data** to be introduced into consumer price statistics from February 2026, with first publication March 2026 — could provide more granular price index data
- Still in beta; limited dataset coverage compared to full ONS catalogue

**Evaluation Score**: 72/100

---

### Source 6B: NESO Carbon Intensity API (Rebranded)

**Provider**: National Energy System Operator (NESO) — formerly National Grid ESO, https://carbonintensity.org.uk and https://api.neso.energy

**Description**: Free API providing real-time and forecast carbon intensity of Great Britain's electricity system. Half-hourly data with regional breakdown across 14 GB regions. Uses ML ensemble regression models for forecasting.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | CC BY 4.0 |
| **Pricing** | **Completely free** |
| **Format** | JSON |
| **API Endpoint** | `https://api.carbonintensity.org.uk/` (legacy, still active) and `https://api.neso.energy` (new portal) |
| **Authentication** | None required |
| **Coverage** | Great Britain; 14 DNO regions |

**v2.0 Updates**:
- Organisation rebranded from National Grid ESO to **NESO** (National Energy System Operator) at `neso.energy`
- New **NESO Data Portal** provides unified data discovery and API access layer
- Legacy `carbonintensity.org.uk` endpoint still active alongside new NESO portal
- Forecast horizon: 96+ hours ahead of real-time; 30-minute temporal resolution

**Evaluation Score**: 68/100 (secondary/contextual use)

---

### Source 6C: Bank of England IADB

**Provider**: Bank of England, https://www.bankofengland.co.uk/boeapps/database/

**Description**: Statistical database providing UK monetary and financial data including exchange rates (GBP/USD — relevant to crude oil pricing), interest rates, and inflation data. Programmatic access via CSV URL pattern.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open for non-commercial and research use |
| **Pricing** | **Completely free** |
| **Format** | CSV (URL-based download) |
| **Authentication** | None required |
| **Update Frequency** | Daily (exchange rates), monthly (monetary statistics) |
| **Coverage** | UK monetary and financial statistics |

**v2.0 Updates**:
- Database last updated 26 January 2026
- Supports up to 300 series codes per request; provisional data available with `VPD=Y` parameter
- Taxonomy update v1.3.1 effective from mid-June 2026 (end-May data) — validation fixes and data point model changes
- 2026 release schedule: monthly releases (6 Feb, 6 Mar, 9 Apr, etc.)

**Evaluation Score**: 65/100 (supporting context)

---

## Evaluation Matrix

### Overall Scoring Summary

| Category | Recommended Source | Type | Score | Annual Cost | Integration Effort |
|----------|-------------------|------|-------|-------------|-------------------|
| Fuel Price Aggregator | VE3 Global Fuel Finder API | UK Gov Statutory | 94/100 | £0 | 5 days |
| Geospatial & Address (GB) | OS Places API | UK Gov (PSGA) | 95/100 | £0 | 5 days |
| Geospatial & Address (NI) | OSNI Pointer (viaEuropa) | NI Gov (NIMA) | 84/100 | £0 | 3 days |
| Company Validation | Companies House API | UK Gov Open Data | 90/100 | £0 | 3 days |
| Notifications | GOV.UK Notify | UK Gov Platform | 95.5/100 | ~£500 (SMS) | 3 days |
| Fuel Price Context | DESNZ Weekly Prices | UK Gov Open Data | 75/100 | £0 | 3 days |
| Postcode Geocoding | Postcodes.io (supplementary) | Free/Open Source | 81/100 | £0 | 2 days |
| Economic Context | ONS Beta API | UK Gov Open Data | 72/100 | £0 | 2 days |
| **TOTAL** | | | **Avg: 86/100** | **~£500/year** | **26 days** |

### Evaluation Criteria Explained

| Criterion | Weight | What It Measures |
|-----------|--------|-----------------|
| **Requirements Fit** | 25% | Does the source cover the required data fields, scope, granularity, and volume? |
| **Data Quality** | 20% | Accuracy, completeness, consistency, timeliness, and known quality issues |
| **License & Cost** | 15% | License terms (OGL, CC, proprietary), pricing sustainability, total cost |
| **API Quality** | 15% | REST/GraphQL, documentation quality, SDKs, versioning, error handling, pagination |
| **Compliance** | 15% | GDPR, UK data residency, data classification, terms of use, DPA 2018 |
| **Reliability** | 10% | SLA, uptime history, vendor stability, community/support, track record |

---

## Data Integration Architecture

### Integration Patterns by Source

| Source | Pattern | Auth | Caching | Error Handling | Monitoring |
|--------|---------|------|---------|----------------|------------|
| VE3 Global API | REST API (near real-time) + flat file reconciliation | TBC (registration) | TTL: 5 min (price data) | Circuit breaker; flat file fallback | Price freshness SLIs; API health |
| OS Places API | REST API on demand | API Key | TTL: 6 weeks (address data stable) | Circuit breaker; fallback to manual entry | Health check; transaction count |
| OSNI Pointer (viaEuropa) | REST API on demand | API Key | TTL: 6 weeks | Circuit breaker; fallback to manual entry | Health check |
| Companies House | REST API on demand | API Key (Basic) | TTL: 24h (company status) | Circuit breaker; fallback to deferred verification | Rate limit monitoring |
| GOV.UK Notify | REST API per event | API Key | None (outbound only) | Retry with exponential backoff; dead letter queue | Delivery rate; failure alerts |
| DESNZ Prices | Scheduled ETL (weekly) | None | Full cache (weekly refresh) | Retry download; serve stale if unavailable | Freshness check every Tuesday |
| ONS API | REST API on demand | None | TTL: 30 days (monthly data) | Circuit breaker; serve cached data | Freshness check monthly |
| Postcodes.io | REST API / Self-hosted | None | TTL: 3 months (quarterly data) | Fallback to ONSPD lookup table | Health check |
| ONSPD | Scheduled bulk load (quarterly) | None | Full cache in database | Retry download; serve previous quarter | Quarterly refresh check |

### Recommended Integration Architecture

```
Data Integration Layer:
- VE3 Global API as primary fuel price data source (near real-time consumption)
- API Gateway with circuit breakers for all external dependencies
- Caching layer (Redis) for geocoding results (TTL aligned to source update frequency)
- ETL pipeline for scheduled data loads (DESNZ weekly, ONSPD quarterly)
- Flat file ingestion for VE3 Global twice-daily reconciliation files
- Fallback strategy: ONSPD lookup table for geocoding if OS Places API unavailable
- Monitoring: API health dashboard, data freshness SLIs, rate limit utilisation alerts
```

### Authentication and Access

| Source | Auth Method | Credentials Required | Registration Process | Lead Time |
|--------|-----------|---------------------|---------------------|-----------|
| VE3 Global API | TBC | Registration with VE3 Global | Contact VE3 Global via GOV.UK guidance | TBC — engage immediately |
| OS Places API | API Key | PSGA membership + API key | PSGA registration via OS website | 1-2 weeks |
| OSNI Pointer | API Key | NIMA membership + viaEuropa registration | NIMA via LPS; viaEuropa via G-Cloud | 2-4 weeks |
| Companies House | API Key (Basic) | Developer account + key | Self-service portal | Instant |
| GOV.UK Notify | API Key | GOV.UK Notify account | Self-service (government email) | Instant |
| ONS API | None | None | None | Instant |
| NESO Carbon | None | None | None | Instant |
| Postcodes.io | None | None | None | Instant |

### Rate Limits and Capacity Planning

| Source | Rate Limit | Projected Usage | Headroom | Upgrade Option |
|--------|-----------|----------------|----------|---------------|
| VE3 Global API | TBC | Continuous (near real-time) | TBC | Engage with VE3 Global |
| OS Places API | 600 req/min | ~100 req/min (peak registration) | 500% | PSGA — no limit upgrade needed; consider bulk pre-load |
| Companies House | 600 req/5min | ~10 req/5min (registration) | 5,900% | Rate limit increase available on request |
| GOV.UK Notify | 350 req/sec | ~2 req/sec (peak compliance batch) | 17,400% | N/A |
| ONS API | Undocumented | ~5 req/min (dashboard refresh) | Ample | N/A |

---

## Data Utility Analysis

> **Note**: Most data sources have alternative and secondary uses beyond their primary requirement. Identifying these latent uses increases the strategic value of data investments.

### Utility by Source

| Source | Primary Use (Requirement) | Secondary Uses | Strategic Value | Combination Opportunities |
|--------|--------------------------|----------------|-----------------|--------------------------|
| VE3 Global API | BR-003/BR-005: Citizen price comparison & open data | 1. Market competition analysis (CMA statutory function) 2. Regional price disparity monitoring 3. Retailer margin analysis against wholesale prices 4. EV vs petrol cost comparison | **CRITICAL** | Combines with ONS CPI to measure real price changes; combines with OS geography for deprivation analysis |
| OS Places API | INT-001: Address validation & UPRN | 1. Geographic analysis of forecourt coverage gaps 2. Cross-referencing with deprivation indices via UPRN 3. Accessibility analysis (forecourt distance from rural communities) | HIGH | Combines with ONS data to identify fuel deserts in deprived areas |
| Companies House | INT-007: Retailer validation | 1. Due diligence on retailer financial health 2. Identifying ownership networks across forecourt chains 3. Persons of significant control analysis | MEDIUM | Combines with enforcement data to identify corporate non-compliance patterns |
| DESNZ Prices | FR-011: Policy analysis context | 1. Wholesale-retail margin analysis 2. Tax policy impact modelling 3. International price comparison benchmarking 4. Pre-scheme vs post-scheme price comparison | HIGH | Combines with VE3 Global data to assess whether transparency reduces margins |
| ONS CPI | FR-011: Inflation context | 1. Real vs nominal fuel price tracking 2. Fuel cost as % of household spend 3. Regional cost of living analysis | HIGH | Combines with VE3 Global prices to assess real price changes |
| NESO Carbon | Secondary: Energy context | 1. Carbon comparison (EV vs petrol/diesel) 2. Environmental policy evidence 3. Net zero progress monitoring | MEDIUM | Combines with fuel prices to show "carbon cost per mile" comparisons |

### Common Secondary Use Patterns Identified

| Pattern | Source | Primary Use | Secondary Use | Value |
|---------|--------|-------------|---------------|-------|
| **Cross-Domain Enrichment** | OS Places + ONS IMD | Address validation | Identifying fuel poverty in deprived areas | Policy evidence for DESNZ |
| **Trend Detection** | DESNZ Prices + VE3 Global | Price context | Detecting whether transparency scheme reduces wholesale-retail margin | CMA effectiveness evidence |
| **Benchmark & Comparison** | ONS CPI + VE3 Global | Inflation context | Comparing VE3 Global prices against national average benchmarks | Data quality validation |
| **Predictive Feature** | BoE exchange rates + DESNZ wholesale | Economic context | Forecasting fuel price movements from GBP/USD and crude oil trends | Proactive policy briefing |
| **Regulatory Evidence** | VE3 Global + Companies House | Price & company data | Identifying whether specific ownership groups maintain elevated margins | CMA enforcement targeting |

### Data Combination Opportunities

1. **Fuel Poverty Analysis**: OS Places API (UPRNs) + ONS Index of Multiple Deprivation (IMD) + VE3 Global fuel prices → Identify areas where high fuel prices overlap with deprivation
2. **Transparency Effectiveness**: DESNZ wholesale prices + VE3 Global retail prices → Measure whether price transparency reduces retailer margins over time (core CMA evidence). CMA reports margins at 11.1ppl (2025) vs 2017-2022 baseline — this service provides the data to track whether mandatory transparency drives margins down.
3. **Carbon Cost Comparison**: NESO Carbon Intensity + VE3 Global prices → Calculate and compare cost-per-mile for petrol/diesel vs EV electricity in each region
4. **Competition Analysis**: VE3 Global prices + Companies House ownership data → Identify whether branded/independent/supermarket forecourts price differently and whether ownership concentration affects pricing

---

## Gap Analysis

### Requirements Without Suitable Data Sources

**GAP-1**: DR-001–006 — Real-time fuel prices from all ~8,500 UK forecourts
- **Data Need**: Current fuel prices submitted by every registered forecourt
- **Why No Source**: This IS the data that Fuel Finder collects — it does not consume this data externally; it creates it from retailer submissions via VE3 Global
- **Impact**: No impact — this is by design. The mandatory scheme under Motor Fuel Price (Open Data) Regulations 2025 creates this data
- **Severity**: N/A (not a gap — architectural design)
- **Recommended Action**: No external source needed — data flows from retailers into VE3 Global, which aggregates and publishes via API
- **v2.0 Update**: VE3 Global is now live as the designated aggregator. The CMA/Fuel Finder service consumes the aggregated data back from VE3 Global's open data API for its own citizen-facing and enforcement views.

**GAP-2**: Northern Ireland address coverage
- **Data Need**: Address validation and geocoding for NI forecourts
- **Why Identified in v2.0**: OS Data Hub covers GB only. NI has ~250 fuel stations that need address validation.
- **Impact**: Without OSNI Pointer, NI forecourts cannot be validated to the same standard as GB
- **Severity**: HIGH
- **Recommended Action**: Engage with LPS for NIMA membership; evaluate viaEuropa G-Cloud service for single-API coverage of both GB (AddressBase) and NI (Pointer)
- **Estimated Effort**: 3-5 person-days
- **Cost Estimate**: £0 under NIMA

**GAP-3** (Resolved in v2.0): Authoritative forecourt master list
- **Previous Status**: HIGH gap — no authoritative open data source of all UK fuel stations
- **v2.0 Resolution**: VE3 Global registration data (mandatory from 18 Dec 2025 - 2 Feb 2026) now provides the definitive forecourt register. All ~8,500 stations are required to register under the Motor Fuel Price (Open Data) Regulations 2025. **GAP CLOSED.**

### Gap Summary

| Gap | Requirement | Severity | Recommended Action | Effort | Cost |
|-----|-------------|----------|-------------------|--------|------|
| GAP-1 | DR-001–006 | N/A | By design — retailer submissions via VE3 Global | — | — |
| GAP-2 | INT-001 (NI) | HIGH | NIMA membership + viaEuropa integration | 3-5 days | £0 (NIMA) |
| GAP-3 | A-1 | **CLOSED** | VE3 Global registration data resolves this | — | — |

---

## Recommendations & Shortlist

### Top 6 Recommended Sources

#### 1. VE3 Global Fuel Finder API for Fuel Price Data (NEW)

**Overall Score**: 94/100

**Rationale**: The legally mandated, near real-time fuel price aggregator covering all ~8,500 UK forecourts. Provides free open data under OGL, eliminating the need for commercial fuel price data providers. This is the single most important data source for the service.

**Key Strengths**:
- ✅ Free statutory open data (OGL v3.0)
- ✅ Comprehensive coverage (~8,500 stations, mandatory)
- ✅ Near real-time (~5-minute lag)
- ✅ Eliminates £50K–£150K/year commercial data cost

**Key Concerns**:
- ⚠️ API specification not yet publicly documented — engagement with VE3 Global required
- ⚠️ Historical data only from 2 Feb 2026 onwards (no backfill)
- ⚠️ Scheme is newly launched — operational maturity to be validated

**Cost**: Free (statutory open data)
**Integration Effort**: 5 person-days
**Risk Level**: LOW-MEDIUM (scheme is statutory, but operationally new)

**Next Steps**:
- [ ] **URGENT**: Contact VE3 Global to obtain API specification and register for access
- [ ] Conduct integration POC (3 days)
- [ ] Establish twice-daily flat file ingestion as backup/reconciliation
- [ ] Set up monitoring for API availability and data freshness

#### 2. OS Places API / AddressBase Premium for Geospatial

**Overall Score**: 95/100

**Rationale**: The authoritative UK address and location service, available free to CMA under PSGA. Provides UPRN-based address validation, geocoding, and proximity search. OS NGD is the strategic successor for future-proofing.

**Key Strengths**:
- ✅ Free under PSGA (no procurement cost)
- ✅ Authoritative government data source (40M addresses)
- ✅ UPRN enables cross-referencing with other government datasets
- ✅ RESTful API with excellent documentation

**Key Concerns**:
- ⚠️ Rate limit of 600/min requires caching strategy for high-volume citizen search
- ⚠️ Coverage gap: Northern Ireland (OSNI Pointer needed)
- ⚠️ AddressBase/AddressBase Plus EOL Nov 2027 (but AddressBase Premium unaffected)

**Cost**: Free (PSGA)
**Integration Effort**: 5 person-days
**Risk Level**: LOW

**Next Steps**:
- [ ] Confirm CMA PSGA membership status
- [ ] Register for OS Data Hub API key
- [ ] Evaluate OS NGD Address Theme during POC for future-proofing
- [ ] Design caching strategy for postcode lookups

#### 3. GOV.UK Notify for Notifications

**Overall Score**: 95.5/100

**Rationale**: The government standard notification platform. Required by architecture principles (P13: Reuse Government Platforms). Free emails, low-cost SMS, excellent API.

**Cost**: ~£500/year (SMS overage)
**Integration Effort**: 3 person-days
**Risk Level**: LOW

#### 4. Companies House API for Company Validation

**Overall Score**: 90/100

**Rationale**: Free, authoritative API for validating retailer company registrations. Streaming API available for real-time change notifications.

**Cost**: Free
**Integration Effort**: 3 person-days
**Risk Level**: LOW

#### 5. OSNI Pointer for Northern Ireland (NEW)

**Overall Score**: 84/100

**Rationale**: Required for full UK coverage. OS Data Hub covers GB only; NI has ~250 fuel stations needing address validation. Available free under NIMA for public sector.

**Cost**: Free (NIMA)
**Integration Effort**: 3 person-days
**Risk Level**: LOW-MEDIUM (separate integration or viaEuropa single-API option)

**Next Steps**:
- [ ] Confirm CMA NIMA membership eligibility
- [ ] Evaluate viaEuropa G-Cloud service for single-API GB+NI coverage
- [ ] If viaEuropa not suitable, build separate OSNI integration

#### 6. Postcodes.io for Postcode Geocoding

**Overall Score**: 81/100

**Rationale**: Free, zero-auth postcode geocoder as a lightweight supplement. Self-hostable via Docker for resilience. Full UK coverage including NI.

**Cost**: Free
**Integration Effort**: 2 person-days
**Risk Level**: LOW

---

## Impact on Data Model

> **Note**: Based on existing data model (`ARC-001-DATA-v1.0`)

### New Entities from External Sources

| Entity | Source | Description | Key Attributes | Sync Strategy |
|--------|--------|-------------|---------------|---------------|
| PostcodeGeography | ONS Postcode Directory / Postcodes.io | Geographic context per postcode | postcode, lat, lng, lsoa, msoa, local_authority, region, constituency | Batch quarterly (ONSPD bulk load) |
| FuelPriceBenchmark | DESNZ Weekly Prices | National average price benchmarks | week_ending, fuel_type, avg_price_ppl, duty_ppl, vat_ppl, retailer_margin_ppl | Batch weekly (ETL every Tuesday) |
| VE3AggregatedPrice | VE3 Global API (NEW) | Published aggregated fuel prices from VE3 | station_id, fuel_type, price_ppl, last_updated, source_timestamp | Near real-time (API consumption) |

### New Attributes on Existing Entities

| Existing Entity | New Attribute | Source | Type | Update Frequency |
|----------------|---------------|--------|------|-----------------|
| Forecourt (E-002) | uprn | OS Places API | VARCHAR(12) | One-off at registration |
| Forecourt (E-002) | lsoa_code | ONSPD | VARCHAR(9) | Quarterly refresh |
| Forecourt (E-002) | local_authority_code | ONSPD | VARCHAR(9) | Quarterly refresh |
| Forecourt (E-002) | region | ONSPD | VARCHAR(100) | Quarterly refresh |
| Forecourt (E-002) | ve3_station_id | VE3 Global (NEW) | VARCHAR(50) | One-off at registration |
| Organisation (E-001) | ch_company_status | Companies House API | VARCHAR(30) | On registration + periodic refresh |
| Organisation (E-001) | ch_registered_address | Companies House API | TEXT | On registration |

### New Relationships

| From Entity | To Entity | Relationship | Source | Description |
|-------------|-----------|-------------|--------|-------------|
| Forecourt | PostcodeGeography | N:1 | ONSPD | Forecourt postcode maps to geographic context |
| PublishedPrice | FuelPriceBenchmark | N:1 | DESNZ | Published price compared against national benchmark |
| Forecourt | VE3AggregatedPrice | 1:N | VE3 Global (NEW) | Forecourt maps to VE3 published prices |

### Sync Strategy

| Source | Pattern | Frequency | Staleness Tolerance | Fallback |
|--------|---------|-----------|--------------------|---------|
| VE3 Global API | API consumption (near real-time) | Continuous | 5 minutes | Twice-daily flat file; serve last known price |
| OS Places API | API call on demand | Per registration event | N/A (synchronous) | Allow manual address entry |
| OSNI Pointer | API call on demand | Per registration event (NI) | N/A (synchronous) | Allow manual address entry |
| Companies House | API call on demand | Per registration event | 24h (status cache) | Accept manual entry; verify later |
| GOV.UK Notify | API call per event | Per notification | N/A (fire-and-forget with retry) | Queue for retry; alert ops |
| ONSPD | Bulk ETL | Quarterly | 3 months | Serve previous quarter |
| DESNZ Prices | Bulk ETL | Weekly | 1 week | Serve previous week |
| ONS CPI | API call | Monthly | 1 month | Serve previous month |

---

## UK Government Open Data Opportunities

### TCoP Point 10: Make Better Use of Data

**Open Data Consumed**:

| Source | Dataset | License | Requirement | Status |
|--------|---------|---------|-------------|--------|
| VE3 Global | Fuel Finder Price Data | OGL v3.0 | BR-003, BR-005 | ✅ **NEW** — Live from 2 Feb 2026 |
| ONS | Postcode Directory (ONSPD) | OGL v3.0 | INT-002, FR-004 | ✅ Recommended |
| DESNZ | Weekly Road Fuel Prices | OGL v3.0 | FR-011 | ✅ Recommended |
| DESNZ | Average Road Fuel Sales & Stock | OGL v3.0 | FR-011 (context) | ✅ **NEW** — Supplementary |
| Companies House | Company Public Data | OGL v3.0 | INT-007 | ✅ Recommended |
| NESO | Carbon Intensity | CC BY 4.0 | FR-011 (secondary) | ✅ Optional |
| Bank of England | IADB Statistics | Open terms | FR-011 (secondary) | ✅ Optional |

**Open Data Publishing Opportunities**:
- **Fuel Finder price data**: Published as open data under OGL v3.0 (core requirement — BR-005). VE3 Global API already provides this; Fuel Finder service should also publish via its own API.
- **Forecourt register**: Publish list of registered forecourts with locations as open data
- **Compliance statistics**: Publish anonymised compliance rates by region as open data
- **API usage statistics**: Publish API consumer metrics to demonstrate third-party adoption
- **Price analysis**: Publish derived datasets (regional averages, margin analysis) as open data

**Common Data Standards Used**:
- UPRN for property addresses (OS AddressBase standard)
- Company Number for business entities (Companies House standard)
- GSS 9-character codes for geographic areas (ONS standard)
- WGS84 for coordinates (international standard)
- UK postcode (Royal Mail standard)
- VE3 Station ID for fuel stations (new Fuel Finder standard)

**Data Ethics Framework Compliance**:
- [x] Clear user need for data collection (statutory obligation)
- [x] Proportionate to the need (minimum data for regulatory purpose)
- [x] Lawful basis established (Public Task — GDPR Art 6(1)(e))
- [x] Data minimisation applied (only price, location, and contact data)
- [x] Transparency about data use (privacy notice at registration)
- [x] Data quality maintained (validation pipeline — FR-007; VE3 Global validation)

---

## Requirements Traceability

### Full Mapping Table

| Requirement ID | Requirement Description | Data Source | Score | Status | Notes |
|----------------|------------------------|-------------|-------|--------|-------|
| INT-001 | Address gazetteer for forecourt registration | OS Places API (PSGA) + OSNI Pointer (NI) | 95/100 | ✅ Matched | Free under PSGA/NIMA; UPRN-enabled; full UK coverage with NI addition |
| INT-002 | Geocoding service for proximity search | OS Places API + Postcodes.io | 92/100 | ✅ Matched | Primary + fallback strategy |
| INT-003 | GOV.UK Notify for retailer communications | GOV.UK Notify | 95.5/100 | ✅ Matched | Government standard platform |
| INT-007 | Companies House company validation | Companies House API | 90/100 | ⚠️ Partial | Covers limited companies; sole traders need manual validation |
| INT-008 | Android Auto / Apple CarPlay compatibility | N/A (API design, not data) | — | ✅ Constraint | API response format, not external data source |
| FR-001 | Forecourt registration | OS Places API + Companies House + VE3 Global | 94/100 | ✅ Matched | Address + company + station ID validation |
| FR-004 | Citizen fuel price search (location) | OS Places API + Postcodes.io + ONSPD | 93/100 | ✅ Matched | Multi-source geocoding strategy |
| FR-011 | Policy analysis and reporting | DESNZ Prices + ONS CPI + BoE + VE3 Global | 80/100 | ✅ Matched | Multiple context sources; VE3 data adds granularity |
| FR-009 | Retailer notifications | GOV.UK Notify | 95.5/100 | ✅ Matched | Email + SMS |
| BR-003 | Citizen price comparison service | VE3 Global API | 94/100 | ✅ Matched | **NEW** — statutory open data from all forecourts |
| BR-005 | Open data API for third parties | VE3 Global API | 94/100 | ✅ Matched | **NEW** — VE3 provides; Fuel Finder republishes |
| DR-001–006 | Fuel price data entities | Retailer submissions via VE3 Global (inbound) | — | ✅ By Design | Data created by this service, not consumed |
| A-1 | Forecourt master list seed | VE3 Global registration data | 94/100 | ✅ **CLOSED** | **Resolved in v2.0** — mandatory registration provides definitive list |
| NFR-C-001 | UK GDPR compliance | All sources | — | ✅ Constraint | All recommended sources are GDPR-compliant |
| NFR-I-002 | Open standards | All sources | — | ✅ Constraint | All sources use JSON/CSV open formats |

### Coverage Summary

**Requirements with Identified Sources**:
- ✅ **14 requirements (82%)** have recommended data sources (up from 71% in v1.0)
- ⚠️ **2 requirements (12%)** partially covered (INT-007 sole trader gap; FR-011 limited regional granularity in DESNZ data)
- ❌ **1 requirement (6%)** no external source needed (DR-001–006 are inbound data by design)

**v2.0 Improvements**:
- GAP-3 (Forecourt master list) **CLOSED** — VE3 Global mandatory registration resolves this
- NI coverage gap **IDENTIFIED** — OSNI Pointer recommended
- Commercial data dependency **ELIMINATED** — VE3 Global replaces Experian Catalist

---

## Next Steps

### Immediate Actions (0-2 weeks)

1. **URGENT: Engage with VE3 Global** to obtain API specification, register for data access, and begin integration planning
2. **Confirm CMA PSGA membership** for free OS Places API / AddressBase access
3. **Register for API keys**: Companies House, OS Data Hub, GOV.UK Notify
4. **Confirm CMA NIMA eligibility** for OSNI Pointer (NI coverage)
5. **Evaluate viaEuropa G-Cloud service** for single-API GB+NI address coverage

### Data Model Updates (2-4 weeks)

6. **Update data model** with VE3AggregatedPrice entity and ve3_station_id attribute (`/arckit.data-model`)
7. **Create ADR** for VE3 Global API integration strategy (`/arckit.adr`)
8. **Create ADR** for geocoding strategy: OS Places API primary (GB), OSNI Pointer (NI), Postcodes.io fallback, ONSPD offline (`/arckit.adr`)
9. **Create ADR** for OS NGD migration path evaluation (`/arckit.adr`)

### Gap Resolution (4-8 weeks)

10. **Integrate OSNI Pointer** for Northern Ireland coverage (GAP-2)
11. **Design sole trader validation** alternative for Companies House gap (HMRC reference or manual verification)
12. **Build VE3 Global flat file ETL** for twice-daily reconciliation
13. **Build DESNZ weekly price ETL pipeline** for policy analysis context

### Integration (Ongoing)

14. **Build VE3 Global API consumption pipeline** (primary fuel price data)
15. **Build data ingestion pipelines** for all recommended sources
16. **Implement caching layer** (Redis) for geocoding and company lookup results
17. **Set up data freshness monitoring** for all data feeds
18. **Document data lineage** from VE3 Global through to published data

---

## Appendices

### Appendix A: Research Methodology

**Data Sources Searched**:
- **UK Government API Catalogue** (api.gov.uk) — mandatory first step per updated datascout methodology
  - Dashboard: Full department listing and API counts
  - Relevant departments: OS (8 APIs), Companies House (2 APIs), GDS (7 APIs), ONS (2+ APIs)
- **Department developer hubs**: OS Data Hub, Companies House developer portal, GOV.UK Notify, ONS developer hub
- **data.gov.uk**: Fuel prices dataset, petrol and diesel prices, average road fuel sales
- UK Government open data portals (ONS, OS Data Hub, Companies House)
- GOV.UK guidance pages (access-fuel-price-data, fuel-finder, Motor Fuel Price Regulations)
- Commercial data provider websites (Experian Catalist, PetrolPrices.com, TomTom)
- Open source projects (Postcodes.io, uk-fuel-prices-api PyPI package)
- Policy and regulatory documents (Motor Fuel Price (Open Data) Regulations 2025, Data (Use and Access) Act 2025)
- Parliamentary records (Hansard Commons and Lords debates on Regulations)
- CMA publications (Road Fuel Annual Report 2025, Fuel Finder enforcement guidance)

**Evaluation Methodology**:
- Weighted scoring across 6 criteria (Requirements Fit 25%, Data Quality 20%, License & Cost 15%, API Quality 15%, Compliance 15%, Reliability 10%)
- All scores based on verified information from official sources via web research (February 2026)
- Pricing verified from vendor websites or documentation
- API quality assessed from documentation review
- Regulatory status verified from legislation.gov.uk and Hansard

**Limitations**:
- VE3 Global API specification not yet publicly documented — scores may change once confirmed
- Pricing for commercial sources (Experian Catalist, TomTom) based on market intelligence — exact quotes require procurement engagement
- API quality assessed from documentation, not hands-on testing
- Data quality indicators from provider claims (validate during POC)
- Market evolves — discovery valid for approximately 6 months
- Fuel Finder scheme is newly operational (2 Feb 2026) — operational maturity yet to be established

### Appendix B: Regulatory Timeline

| Date | Milestone |
|------|-----------|
| 19 June 2025 | Data (Use and Access) Act 2025 receives Royal Assent |
| 4 November 2025 | Draft Motor Fuel Price (Open Data) Regulations 2025 debated in Commons |
| 4 December 2025 | Regulations debated in Lords Grand Committee |
| 18 December 2025 | Forecourt registration period opens |
| **2 February 2026** | **Mandatory price reporting begins (LIVE)** |
| Early May 2026 | CMA enforcement grace period ends; formal enforcement begins |

### Appendix C: Glossary

- **API**: Application Programming Interface
- **ETL**: Extract, Transform, Load
- **OGL**: Open Government Licence
- **PSGA**: Public Sector Geospatial Agreement (centrally-funded access to OS premium data for UK public sector)
- **NIMA**: Northern Ireland Mapping Agreement (equivalent of PSGA for NI)
- **UPRN**: Unique Property Reference Number (12-digit identifier for every addressable location in GB)
- **UDPRN**: Unique Delivery Point Reference Number (Royal Mail identifier)
- **GDPR**: General Data Protection Regulation (UK GDPR / EU GDPR)
- **DPA 2018**: Data Protection Act 2018
- **TCoP**: Technology Code of Practice (UK Government)
- **SLA**: Service Level Agreement
- **TTL**: Time To Live (cache expiry)
- **ONSPD**: ONS Postcode Directory
- **PII**: Personally Identifiable Information
- **NESO**: National Energy System Operator (formerly National Grid ESO)
- **CPI/CPIH**: Consumer Prices Index / Consumer Prices Index including owner occupiers' Housing costs
- **IMD**: Index of Multiple Deprivation
- **VE3 Global**: Designated aggregator under Motor Fuel Price (Open Data) Regulations 2025
- **OS NGD**: OS National Geographic Database (strategic successor to AddressBase products)
- **LPS**: Land & Property Services (Northern Ireland)
- **PAF**: Postcode Address File (Royal Mail)

---

**Generated by**: ArcKit `/arckit.datascout` command
**Generated on**: 2026-02-01
**ArcKit Version**: 1.1.0
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: claude-opus-4-5-20251101
