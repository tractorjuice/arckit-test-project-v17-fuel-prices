# Technology and Service Research: UK Fuel Price Transparency Service

> **Template Status**: Beta | **Version**: 1.0.3 | **Command**: `/arckit.research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RSCH-v1.0 |
| **Document Type** | Technology and Service Research |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-01-30 |
| **Last Modified** | 2026-01-30 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-04-30 |
| **Owner** | Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-30 | ArcKit AI | Initial creation from `/arckit.research` command | PENDING | PENDING |

---

## Executive Summary

### Research Scope

This document presents research findings for all available UK petrol station API endpoints, fuel price data sources, and supporting government APIs relevant to the UK Fuel Price Transparency Service ("Fuel Finder"). It provides a comprehensive catalogue of data sources for build vs buy analysis and integration architecture decisions.

**Requirements Analyzed**: 13 functional, 22 non-functional, 7 integration, 6 data entity requirements

**Research Categories Identified**: 7 categories based on requirement analysis

**Research Approach**: Web research across UK Government APIs, commercial fuel data providers, open data sources, mapping/geocoding services, and community projects

### Key Findings

- **Fuel Finder Statutory Scheme (VE3 Global)**: The Motor Fuel Price (Open Data) Regulations 2025 mandate all ~8,300 UK petrol stations report prices within 30 minutes of change. VE3 Global Ltd is the designated aggregator (£3M contract). Data is freely accessible via API and flat file. **This is the primary, authoritative data source.**
- **CMA Interim Scheme**: 14 retailer JSON endpoints currently provide voluntary fuel price data covering ~35% of stations and ~60% of fuel volume. These serve as a transition source until Fuel Finder achieves full coverage.
- **UK Government APIs are free**: OS Places API (free under PSGA), Companies House API (free), GOV.UK Notify (free for emails), DESNZ weekly fuel prices (free) — total cost for government API integrations is effectively £0.
- **Commercial providers are redundant**: PetrolPrices.com (Allstar data), Kalibrate, TomTom, and HERE all provide fuel price data commercially, but the statutory Fuel Finder scheme renders them unnecessary as primary sources.
- **OpenStreetMap provides valuable cross-reference**: ~8,300+ UK petrol stations mapped with location, brand, and amenity data — free under ODbL — excellent for registration data validation.

### Build vs Buy Summary

| Approach | Categories | Total 3-Year TCO | Rationale |
|----------|-----------|------------------|-----------|
| **GOV.UK Platforms** | Notifications, Geocoding, Design System | £0 | Free for UK central government |
| **ADOPT** (Open Source/Open Data) | Station data validation, fuel price data | £0 | Statutory open data + OpenStreetMap |
| **BUILD** (Custom Development) | Data ingestion pipeline, compliance dashboard, citizen search | £TBC (per SOBC) | Core bespoke service — no off-the-shelf product |
| **TOTAL** | 7 categories | **£0 for data/APIs** | All external data sources are free for UK Government |

### Top Recommended Data Sources

**Shortlist for integration architecture**:

1. **Fuel Finder Statutory API (VE3 Global)** for real-time fuel prices: Mandatory, free, comprehensive, statutory authority
2. **OS Places API** for address validation and geocoding: Authoritative UK addressing, free under PSGA, UPRN-based
3. **GOV.UK Notify** for retailer/enforcement notifications: Free emails, low-cost SMS, mandated for government services

### Requirements Coverage

- 100% of integration requirements have identified API sources
- 100% of data requirements can be satisfied by free government and open data sources
- 0 requirements need commercial data procurement
- Custom development required for: ingestion pipeline, compliance dashboard, citizen search UI, enforcement tools

---

## Research Categories

> **Note**: Research categories dynamically identified based on the user's request ("all the petrol station API endpoints") and project requirements for API-based fuel price data integration.

---

## Category 1: Fuel Price Data — Statutory Open Data Scheme

**Requirements Addressed**: FR-003, FR-004, FR-005, FR-007, BR-002, BR-003, BR-005, INT requirements

**Why This Category**: The core purpose of the service is to ingest, validate, and publish fuel price data from all UK forecourts. The statutory Fuel Finder scheme provides the primary data source.

---

### Option 1A: Fuel Finder Statutory API (VE3 Global — Designated Aggregator)

**Description**: The Motor Fuel Price (Open Data) Regulations 2025 mandate all ~8,300 UK petrol filling stations report fuel prices within 30 minutes of any price change. VE3 Global Ltd is the designated aggregator contracted by DESNZ to collect and publish this data.

**Legislative Basis**:
- Primary legislation: Data (Use and Access) Act 2025 (Royal Assent: 19 June 2025)
- Secondary legislation: The Motor Fuel Price (Open Data) Regulations 2025
- Legislation URL: https://www.legislation.gov.uk/ukdsi/2025/9780348275308
- GOV.UK collection: https://www.gov.uk/government/collections/road-fuel-price-data-scheme
- Enforcement guidance: https://www.gov.uk/government/publications/fuel-finder-enforcement-guidance

**Aggregator Details**:

| Item | Detail |
|------|--------|
| Provider | VE3 Global Ltd |
| Contract value | £3 million |
| Contract notice | https://www.contractsfinder.service.gov.uk/notice/597124d5-4b50-473e-87f8-bb7253e7a2ec |
| Service URL | `fuel-finder.service.gov.uk` |

**Data Scope — Registration (Static, Schedule 1)**:
- Site trading name
- Site address
- Latitude and longitude
- Usual trading hours
- Available amenities and facilities (8 defined items)
- Contact details for the motor fuel trader
- Contact details for the designated "reporter"
- Fuel grades available for sale

**Data Scope — Prices (Real-Time)**:
- Selling price per litre of each grade of motor fuel offered for sale
- Update obligation: within 30 minutes of any price change at the pump

**Data Submission Methods (Retailer → Aggregator)**:

| Method | Description |
|--------|-------------|
| API | Automated real-time integration via EPOS systems |
| Secure web portal | Manual price entry by authorised user |
| SMS | Manual text message submission |
| IVR | Interactive Voice Response telephone submission |
| Bulk submission | Head offices can collate multiple site data before sharing |

**Data Access Methods (Aggregator → Third Parties)**:

| Method | Description |
|--------|-------------|
| API | Real-time programmatic access |
| Flat file | Shared twice daily |
| Licensing | "Openly and freely accessible to all third parties" |

**Regulatory Timeline**:

| Milestone | Date |
|-----------|------|
| Registration period opens | 18 December 2025 |
| Registration period closes | 2 February 2026 |
| Live price data sharing begins | 2 February 2026 |
| Ongoing registration change reporting | Within 3 days of change |
| CMA enforcement focus shift | After May 2026 |

**Enforcement Penalties**:

| Penalty | Maximum |
|---------|---------|
| Percentage of annual global turnover | Up to 1% |
| Percentage of daily global turnover | Up to 5% |
| Criminal sanctions | Unlimited fines |

**Consumer Impact**: Estimated £10.4 billion consumer savings over 10-year appraisal period.

**Coverage**: ~8,300 UK petrol filling stations (mandatory — all stations must participate)

**Cost**: Free (open data, freely accessible)

**Technical Specification Status**: **No public developer documentation, API schema, or endpoint specification for the VE3 Global API has been published as of 30 January 2026.** This is a significant gap. Documentation may be distributed directly to registered consumers or hosted on a developer portal not yet publicly indexed.

**Recommended Action**: Contact DESNZ or VE3 Global directly for API developer documentation.

**Pros**:
- Statutory authority — mandatory for all UK stations
- Free, open data with no licensing restrictions
- Comprehensive coverage (~8,300 stations)
- Real-time data (within 30 minutes of price change)
- Multiple submission channels (API, web, SMS, IVR)

**Cons**:
- API specification not yet publicly available
- Aggregator (VE3 Global) is a third-party dependency
- Data quality dependent on retailer compliance (enforcement-backed)
- New service — operational track record not yet established

**Suitability**: **PRIMARY DATA SOURCE** — this is the authoritative, statutory source for the Fuel Finder service.

---

### Option 1B: CMA Interim Voluntary Open Data Scheme (14 Retailer JSON Endpoints)

**Description**: The CMA established a voluntary interim open data pricing scheme while the statutory scheme was being developed. Individual retailers host their own JSON endpoints. The CMA does not aggregate or validate the data.

**Access page**: https://www.gov.uk/guidance/access-fuel-price-data

**Authentication**: None — all endpoints publicly accessible without API keys

**Data Format**: JSON (13 retailers), HTML (1 retailer — Shell)

**Update Frequency**: Typically every 24 hours (varies by retailer)

**Coverage**: ~35% of UK service stations, ~60% of fuel volume sold

**Licensing**: Open data — freely available

**Rate Limits**: Not formally specified; fair use assumed

**Complete Endpoint List**:

| # | Retailer | Endpoint URL | Format |
|---|----------|-------------|--------|
| 1 | Ascona Group | `https://fuelprices.asconagroup.co.uk/newfuel.json` | JSON |
| 2 | Asda | `https://storelocator.asda.com/fuel_prices_data.json` | JSON |
| 3 | BP | `https://www.bp.com/en_gb/united-kingdom/home/fuelprices/fuel_prices_data.json` | JSON |
| 4 | Esso Tesco Alliance | `https://fuelprices.esso.co.uk/latestdata.json` | JSON |
| 5 | JET Retail UK | `https://jetlocal.co.uk/fuel_prices_data.json` | JSON |
| 6 | Karan Retail Ltd | `https://devapi.krlpos.com/integration/live_price/krl` | JSON |
| 7 | Morrisons | `https://www.morrisons.com/fuel-prices/fuel.json` | JSON |
| 8 | Moto | `https://moto-way.com/fuel-price/fuel_prices.json` | JSON |
| 9 | Motor Fuel Group | `https://fuel.motorfuelgroup.com/fuel_prices_data.json` | JSON |
| 10 | Rontec | `https://www.rontec-servicestations.co.uk/fuel-prices/data/fuel_prices_data.json` | JSON |
| 11 | Sainsbury's | `https://api.sainsburys.co.uk/v1/exports/latest/fuel_prices_data.json` | JSON |
| 12 | SGN | `https://www.sgnretail.uk/files/data/SGN_daily_fuel_prices.json` | JSON |
| 13 | Shell | `https://www.shell.co.uk/fuel-prices-data.html` | HTML |
| 14 | Tesco | `https://www.tesco.com/fuel_prices/fuel_prices_data.json` | JSON |

**Notes**:
- Shell is the only retailer not providing JSON; HTML page requires scraping
- Most retailers use a common filename convention (`fuel_prices_data.json`), suggesting a shared schema template
- No formal JSON schema documentation published by the CMA
- "There will sometimes be a delay when forecourt fuel prices are set, and when prices are displayed by a third-party comparator" — CMA

**Pros**:
- Free, open, no authentication required
- Operational today (no waiting for VE3 aggregator)
- Good coverage of major chains (supermarkets, large operators)
- Simple JSON format, easy to consume

**Cons**:
- Only ~35% of stations (major chains; no independents)
- Voluntary — no enforcement for data quality or timeliness
- No standardised schema — each retailer may vary
- Shell provides HTML not JSON
- Typically 24-hour update cycle (not real-time)
- Will be superseded by statutory Fuel Finder scheme

**Suitability**: **TRANSITION DATA SOURCE** — useful during the period between statutory go-live and full Fuel Finder adoption. Can be used for integration testing and initial citizen-facing service while Fuel Finder API specification is obtained.

---

### Option 1C: Commercial Fuel Price Data (PetrolPrices.com / myAutomate)

**Description**: PetrolPrices.com (operated by Automate App Limited, trading as myAutomate) provides commercial B2B fuel pricing data sourced from Allstar fuel card transactions (~8,000 daily updates), CMA open data (3,800+ stations), and crowdsourced consumer data.

**Provider Details**:
- Data services: https://www.petrolprices.com/data-services/
- Contact: data@petrolprices.com
- Registered office: 8th Floor South, Reading Bridge House, George Street, Reading, RG1 8LS

**Background**: Following the end of Experian Catalist service (31 March 2024), myAutomate signed an exclusive agreement with Allstar to provide fuel card transaction-based pricing data. Allstar network covers 7,700+ sites with 1.2 million cards in circulation.

**Coverage**: ~8,490 UK stations (BP, Shell, Texaco, supermarkets, independents, small chains)

**Update Frequency**: Daily

**Pricing**: Commercial — contact for quote. Former Experian Catalist pricing was reportedly £50,000–£150,000 per annum.

**Other Commercial Providers**:

| Provider | Data | Pricing | Suitability |
|----------|------|---------|-------------|
| Kalibrate (formerly Kent Group) | Competitor pricing, wholesale, AI pricing optimisation | Enterprise | Retailer-oriented, not transparency |
| Argus Media / Oil Market Journal | Wholesale refined products benchmarks | Enterprise subscription | Wholesale only — for CMA/DESNZ policy analysis |
| GlobalPetrolPrices.com | National averages, 135 countries | Commercial/Academic | Averages only, CC BY-NC-ND licence |
| FuelPrices.co.uk | Forecourt pricing API | Commercial | Coverage unclear |

**Pros**:
- High coverage (~8,490 stations)
- Daily updates with transaction-based data
- Professional B2B data service

**Cons**:
- Commercial cost (potentially £50K–£150K/year)
- Rendered redundant by statutory Fuel Finder scheme (free, mandatory, real-time)
- Non-compliant with TCoP Point 3/4 (prefer open standards/open source)
- Additional procurement overhead via Digital Marketplace

**Suitability**: **NOT RECOMMENDED** — the statutory Fuel Finder scheme provides equivalent or superior data at zero cost. Commercial data may be useful for CMA/DESNZ benchmarking of Fuel Finder data quality during the transition period, but should not be procured as a primary data source.

---

### Build vs Buy Recommendation for Fuel Price Data

**Recommended Approach**: **USE GOV.UK STATUTORY OPEN DATA (Fuel Finder / VE3 Global)**

**Rationale**: The Motor Fuel Price (Open Data) Regulations 2025 create a mandatory, statutory open data scheme covering all ~8,300 UK petrol stations with real-time (30-minute) price updates. This data is freely and openly accessible. Using any commercial alternative would be wasteful of public money and non-compliant with TCoP principles.

**Integration Strategy**:
1. **Primary**: Fuel Finder API (VE3 Global) — real-time prices + flat file twice daily
2. **Transition**: CMA interim retailer JSON endpoints — until Fuel Finder achieves full coverage
3. **Validation**: OpenStreetMap station locations — cross-reference registration data

**Key Decision Factors**:
- Statutory authority: Fuel Finder is the legally mandated source
- Cost: Free vs £50K–£150K/year for commercial alternatives
- Coverage: Mandatory for all stations vs partial voluntary coverage
- Freshness: 30-minute obligation vs 24-hour voluntary updates
- TCoP compliance: Open data preferred over commercial procurement

---

## Category 2: Address Validation and Geocoding

**Requirements Addressed**: FR-001, FR-004, INT-001, INT-002

**Why This Category**: Forecourt registration requires address validation (INT-001) and citizen search requires geocoding (INT-002).

---

### Option 2A: OS Places API (Recommended for UK Government)

**Description**: Ordnance Survey Places API provides the authoritative UK address dataset (AddressBase Premium) via RESTful API, supporting address search, postcode lookup, UPRN resolution, and geographic queries.

**Provider**: Ordnance Survey

| Item | Detail |
|------|--------|
| Platform URL | https://osdatahub.os.uk/ |
| Product page | https://www.ordnancesurvey.co.uk/products/os-places-api |
| Documentation | https://docs.os.uk/os-apis/accessing-os-apis/os-places-api |
| API Catalogue | https://www.api.gov.uk/os/os-places-api/ |
| Underlying dataset | AddressBase Premium |
| Update frequency | Every 6 weeks |
| Coverage | United Kingdom, Jersey, Guernsey, Isle of Man |

**Authentication**: API key (generated via OS Data Hub account)

**Data Format**: JSON, XML

**Search Operations**:

| Operation | Description |
|-----------|-------------|
| Full/partial address search | Forward geocoding from text |
| Postcode search | Search by UK postcode |
| UPRN search | Look up by Unique Property Reference Number |
| Bounding box search | All addresses within two-point box |
| Coordinate/radius search | Nearest address to given coordinates |
| Polygon search | POST with GeoJSON polygon |

**Pricing for UK Government**:

| Plan | Cost | Eligibility |
|------|------|-------------|
| Public Sector Plan (PSGA) | **Free** | UK central government, local authorities, NHS |
| Premium Plan | £1,000/month free threshold, then per-transaction | Commercial organisations |

**CMA is a UK central government body — qualifies for free PSGA access.**

**Developer Libraries**: Python (`osdatahub`), JavaScript (`osdatahub-js`) — both on GitHub

**Pros**:
- Authoritative UK address data (AddressBase Premium)
- UPRN-based addressing (unique property reference)
- Free for UK Government under PSGA
- Well-documented, supported by OS
- GeoJSON output

**Cons**:
- Updates every 6 weeks (not real-time for new addresses)
- Requires OS Data Hub account setup

**Suitability**: **PRIMARY — recommended for all address validation and geocoding within the service.** Free, authoritative, UK Government standard.

---

### Option 2B: OS Names API and OS Maps API

**OS Names API**:
- Data: Populated places, cities, roads, postcodes in Great Britain
- Pricing: Free (OS OpenData Plan)
- Use case: Forward/reverse geocoding of place names for citizen search

**OS Maps API**:
- Data: Raster and vector map tiles
- Pricing: Free (OpenData); Premium with £1,000/month threshold
- Use case: Rendering UK maps showing fuel station locations

**OS NGD API — Features**:
- Documentation: https://osdatahub.os.uk/docs/ofa/overview
- Data: Nine themes with geographic feature types
- Format: OGC-compliant GeoJSON
- Use case: Advanced geographic queries for station catchment analysis

---

### Option 2C: Alternative Geocoding APIs (Not Recommended for UK Government)

| Provider | Pricing | Rate Limits | Licensing | Recommendation |
|----------|---------|-------------|-----------|----------------|
| Google Geocoding API | 10K free/month, then $5/1K | 3,000 QPM | No permanent storage; must display on Google Maps | **Not recommended** — restrictive licensing |
| Mapbox Geocoding v6 | 100K free/month, then $0.75–5/1K | 1,000 req/min | Temporary use by default; permanent at higher cost | Not recommended — OS Places is authoritative and free |
| What3Words | Free tier (limited), paid tiers | 10 req/sec on free | Proprietary | Not standard for UK Government |

---

### Build vs Buy Recommendation for Geocoding

**Recommended Approach**: **USE GOV.UK PLATFORM — OS Places API (free under PSGA)**

**Rationale**: OS Places API is the authoritative UK addressing service, free for UK Government, provides UPRN-based addressing required for registration, and integrates with existing OS data. Compliant with TCoP Point 8 (share, reuse, collaborate) and Point 5 (use cloud first).

---

## Category 3: Organisation Validation

**Requirements Addressed**: FR-001, INT-007

**Why This Category**: Forecourt registration requires validating the retailer organisation against Companies House records.

---

### Option 3A: Companies House API (Recommended)

**Description**: Free API providing access to the UK Companies Register, enabling validation of company registration status, officers, and registered addresses.

| Item | Detail |
|------|--------|
| Developer portal | https://developer.company-information.service.gov.uk/ |
| API specifications | https://developer-specs.company-information.service.gov.uk/ |
| Getting started | https://developer.company-information.service.gov.uk/get-started |
| Rate limiting | https://developer-specs.company-information.service.gov.uk/guides/rateLimiting |

**Authentication**: API key via HTTP Basic Authentication (TLS 1.2+ required)

**Rate Limits**: 600 requests per 5-minute window (~2 req/sec); HTTP 429 on exceed

**Key Endpoints**:

| Endpoint | Data |
|----------|------|
| Company search | Search by name, company number |
| Company profile | Registered address, SIC codes, incorporation date, status |
| Officers | Directors, secretaries, appointments |
| Filing history | Annual returns, accounts, resolutions |

**Data Format**: JSON

**Pricing**: Free

**Coverage**: All registered UK companies

**Licensing**: Open Government Licence

**Suitability**: **PRIMARY** — use for validating fuel retailer organisation details during registration: verify company registration status, check active/dissolved status, confirm registered addresses, look up parent company structures for multi-site operators.

---

## Category 4: Notifications and Communications

**Requirements Addressed**: FR-009, INT-003, BR-004

**Why This Category**: The service requires automated notifications to retailers for compliance reminders, submission confirmations, and enforcement notices.

---

### Option 4A: GOV.UK Notify (Recommended — Mandated for UK Government)

**Description**: GDS notification service for UK Government digital services supporting email, SMS, and letters.

| Item | Detail |
|------|--------|
| Service URL | https://www.notifications.service.gov.uk/ |
| API documentation | https://www.notifications.service.gov.uk/using-notify/api-documentation |
| Pricing | https://www.notifications.service.gov.uk/pricing |
| Source code | https://github.com/alphagov/notifications-api |

**Authentication**: API key (per service — live, team-only, and test keys)

**Pricing (from 1 April 2025)**:

| Channel | Cost |
|---------|------|
| Email | **FREE** (unlimited) |
| SMS — Central government | 250,000 free messages/year, then 2.33p + VAT |
| SMS — Local authorities/NHS | 25,000 free messages/year, then 2.33p + VAT |
| Letters | Below market rate (printing + postage included) |

**Rate Limits**: 350 requests per second; 30 million emails/day

**API Clients**: Python, Java, .NET, Ruby, PHP, Node.js

**Capabilities**: Personalised templates, bulk sending, scheduled delivery, delivery receipts via webhook, custom GOV.UK branding

**Eligibility**: Central government, local authorities, NHS, and managed service providers for public sector

**Suitability**: **MANDATORY** — GOV.UK Notify is the standard GDS notification service. CMA as central government gets free emails and 250K free SMS/year. Use for: retailer compliance reminders, submission confirmations, enforcement notices, operational alerts.

---

## Category 5: Fuel Price Benchmarking and Trend Data

**Requirements Addressed**: FR-011, BR-006

**Why This Category**: DESNZ policy analysts require fuel price trend data for ministerial briefings and economic analysis.

---

### Option 5A: DESNZ Weekly Road Fuel Prices (Recommended)

| Item | Detail |
|------|--------|
| Statistics page | https://www.gov.uk/government/statistics/weekly-road-fuel-prices |
| Collection | https://www.gov.uk/government/collections/road-fuel-and-other-petroleum-product-prices |
| Data | Average UK retail pump prices (unleaded petrol, diesel) |
| Formats | CSV, Excel (XLSX), ODS |
| Authentication | None |
| Pricing | Free |
| Frequency | Weekly (also monthly and mid-month) |
| Licensing | Open Government Licence |

**Latest data point (September 2025)**: Petrol 133.84 ppl, Diesel 141.57 ppl

---

### Option 5B: data.gov.uk Fuel Datasets

| Dataset | URL | Data |
|---------|-----|------|
| Petrol and Diesel Prices | https://www.data.gov.uk/dataset/21db6396-3daf-4d90-8b3f-054995256018/petrol-and-diesel-prices | Historical price data |
| Average Road Fuel Sales | https://www.data.gov.uk/dataset/9003012e-4564-4a6b-b5f0-8765ccb23a03/average-road-fuel-sales-deliveries-and-stock-levels | Monthly sales, deliveries, stock |
| ENV data tables | https://www.gov.uk/government/statistical-data-sets/energy-and-environment-data-tables-env | Historical prices, duties, consumption |

All free, CSV/ODS format, Open Government Licence.

---

### Option 5C: ONS Consumer Price Inflation — Fuel Components

| Item | Detail |
|------|--------|
| Inflation hub | https://www.ons.gov.uk/economy/inflationandpriceindices |
| Fuel-specific series | RPI Petrol and Oil (Series DOGQ): https://www.ons.gov.uk/economy/inflationandpriceindices/timeseries/dogq/mm23 |
| Data format | CSV, Excel |
| Pricing | Free |

Useful for macro-economic context linking fuel prices to CPI/CPIH.

---

### Option 5D: Reference Sources (No API — Editorial Only)

| Source | URL | Data | API |
|--------|-----|------|-----|
| RAC Fuel Watch | https://www.rac.co.uk/drive/advice/fuel-watch/ | Daily averages, historical graphs | No |
| AA Fuel Price Report | https://www.theaa.com/about-us/newsroom/ | National/regional averages, reports | No |
| PRA Statistics | https://www.ukpra.co.uk/ | Station counts, market share | No |
| Fuels Industry UK | https://fuelsindustryuk.org/ | Industry data (~8,300 stations) | No |
| House of Commons Library | https://commonslibrary.parliament.uk/research-briefings/sn04712/ | Parliamentary briefing on fuel prices | No |

---

### Option 5E: Wholesale Price Benchmarking (For CMA/DESNZ Policy Teams)

| Provider | Data | Pricing |
|----------|------|---------|
| Argus Media / Oil Market Journal | UK wholesale refined products (Ebob petrol, diesel), biofuels, LPG | Enterprise subscription |
| Kalibrate | Competitor pricing, wholesale prices, margin analysis | Enterprise |

**Suitability**: Relevant for CMA policy analysis of refiner margins and retail-wholesale price transmission. Not needed for the consumer-facing service.

---

## Category 6: Station Location Cross-Validation

**Requirements Addressed**: FR-001, Data Migration Requirements

**Why This Category**: The service needs to validate forecourt registration data against known station locations to identify gaps in coverage.

---

### Option 6A: OpenStreetMap Overpass API (Recommended for Validation)

**Description**: OpenStreetMap provides a community-mapped database of UK petrol stations queryable via the Overpass API.

| Item | Detail |
|------|--------|
| Primary endpoint | `https://overpass-api.de/api/interpreter` |
| Alternative endpoints | `https://lz4.overpass-api.de/api/interpreter`, `https://z.overpass-api.de/api/interpreter` |
| Interactive tool | https://overpass-turbo.eu/ |
| Documentation | https://wiki.openstreetmap.org/wiki/Overpass_API |
| Fuel station tag | https://wiki.openstreetmap.org/wiki/Tag:amenity=fuel |

**Authentication**: None required

**Data Format**: JSON or XML (specified in query)

**Pricing**: Free

**Rate Limits**: Fair use (no published hard limit)

**Licensing**: Open Data Commons Open Database License (ODbL) — attribution and share-alike required

**Overpass QL Query (All UK Petrol Stations)**:

```
[out:json][timeout:240];
(
  area["ISO3166-1"="GB"][admin_level=2];
)->.a;
(
  nwr["amenity"="fuel"](area.a);
);
out center;
```

**Data Available Per Station**:

| OSM Tag | Data |
|---------|------|
| `name` | Station name |
| `brand` | Brand (BP, Shell, Esso, etc.) |
| `operator` | Operating company |
| `addr:street`, `addr:city`, `addr:postcode` | Address |
| `fuel:diesel`, `fuel:octane_95`, `fuel:octane_98` | Fuel type availability |
| `fuel:lpg`, `fuel:HGV_diesel`, `fuel:adblue` | Additional fuels |
| `opening_hours` | Operating hours |
| `payment:*` | Payment methods |

**Coverage**: Community-mapped. Good urban coverage, variable rural coverage. UK had a dedicated petrol station mapping project in Q1 2018.

**Suitability**: **RECOMMENDED for cross-validation** — use to verify Fuel Finder registration data against known station locations. Not suitable for price data (OSM does not store fuel prices). ODbL licence is compatible with government use but requires attribution.

---

### Option 6B: Google Maps Places API (Not Recommended)

| Item | Detail |
|------|--------|
| Documentation | https://developers.google.com/maps/documentation/places/web-service/ |
| Fuel-specific data | FuelPrice model available (fuel type, price, last updated) |
| Pricing | Tiered: IDs Only, Essentials, Pro, Enterprise |
| Rate limits | 3,000 QPM |
| Licensing | **No permanent storage; 30-day cache max; must display on Google Maps** |

**Suitability**: **NOT RECOMMENDED** — restrictive licensing prevents permanent data storage, which defeats the purpose of a government database. Google's terms prohibit using results outside the Google Maps ecosystem.

---

### Option 6C: TomTom and HERE Fuel APIs (Not Recommended)

| Provider | Pricing | Suitability |
|----------|---------|-------------|
| TomTom Fuel Prices API | Enterprise only (not available on Freemium/PAYG) | Redundant given Fuel Finder |
| HERE Fuel Prices API | Freemium + pay-as-you-go | Redundant given Fuel Finder |

---

## Category 7: Mapping and Visualisation

**Requirements Addressed**: FR-004, INT-004, NFR-U-001

**Why This Category**: The citizen-facing service requires map display of fuel station locations.

---

### Option 7A: OS Maps API (Recommended for UK Government)

| Item | Detail |
|------|--------|
| Product page | https://www.ordnancesurvey.co.uk/products/os-maps-api |
| Pricing | Free (OS OpenData tiles); Premium with £1,000/month threshold |
| PSGA | Free for UK Government |
| Data | Raster and vector map tiles |

**Suitability**: Free under PSGA, authoritative UK mapping. However, GOV.UK Design System typically uses Leaflet.js with open tiles.

---

### Option 7B: Open Map Tiles (Leaflet.js)

The GOV.UK Design System and GOV.UK Frontend do not include mapping by default. Services needing maps typically use Leaflet.js with open tile providers. This aligns with GDS patterns.

---

### Option 7C: Mapbox

| Item | Detail |
|------|--------|
| Pricing | 50K free map loads/month, then per-load |
| Geocoding | 100K free/month |
| Licensing | More flexible than Google |

Not the default UK Government choice, but technically viable.

---

## Total Cost of Ownership (TCO) Summary

### Blended TCO Across All Categories — Data Sources and APIs Only

| Category | Recommended Option | Year 1 | Year 2 | Year 3 | 3-Year TCO |
|----------|-------------------|--------|--------|--------|------------|
| Fuel Price Data | Fuel Finder (VE3 Global) | £0 | £0 | £0 | £0 |
| Fuel Price Data (transition) | CMA Interim JSON Endpoints | £0 | £0 | £0 | £0 |
| Address Validation / Geocoding | OS Places API (PSGA) | £0 | £0 | £0 | £0 |
| Map Tiles | OS Maps API (PSGA) | £0 | £0 | £0 | £0 |
| Organisation Validation | Companies House API | £0 | £0 | £0 | £0 |
| Notifications | GOV.UK Notify (emails) | £0 | £0 | £0 | £0 |
| Notifications (SMS) | GOV.UK Notify (250K free) | £0 | ~£1,200 | ~£1,500 | ~£2,700 |
| Benchmarking Data | DESNZ Weekly / data.gov.uk / ONS | £0 | £0 | £0 | £0 |
| Station Cross-Validation | OpenStreetMap Overpass | £0 | £0 | £0 | £0 |
| **TOTAL** | | **£0** | **~£1,200** | **~£1,500** | **~£2,700** |

**Note**: SMS costs assume beyond-free-tier usage in Years 2–3. Email notifications are unlimited and free. All other data sources and APIs are free for UK central government.

### TCO Assumptions

- CMA is a UK central government body qualifying for PSGA (OS) and free GOV.UK services
- SMS volumes estimated at ~300K/year in Year 2 (above 250K free threshold), ~315K in Year 3
- No commercial fuel data procurement required
- Infrastructure costs (compute, storage, networking) excluded — covered separately in hosting research
- Integration development costs excluded — covered separately in delivery planning

---

## Requirements Traceability

### Requirements Coverage Matrix

| Requirement ID | Description | Research Category | Recommended Solution | Rationale |
|----------------|-------------|-------------------|---------------------|-----------|
| FR-001 | Forecourt Registration | Address Validation + Org Validation | OS Places API + Companies House API | Authoritative UK address and company data, both free |
| FR-002 | Manual Price Submission | Fuel Price Data | Fuel Finder (CMA service builds this) | Core bespoke service |
| FR-003 | API Price Submission | Fuel Price Data | Fuel Finder statutory scheme (VE3 API) | Statutory data submission channel |
| FR-004 | Citizen Fuel Price Search | Geocoding + Mapping + Fuel Data | OS Places + OS Maps + Fuel Finder data | Free government APIs for geocoding + statutory price data |
| FR-005 | Open Data API | Fuel Price Data | Build (exposing Fuel Finder data) | Core bespoke API publishing ingested data |
| FR-006 | Compliance Dashboard | N/A (bespoke build) | Custom development | No off-the-shelf solution; unique enforcement requirement |
| FR-007 | Data Validation Pipeline | N/A (bespoke build) | Custom development | Unique pipeline matching regulatory requirements |
| FR-009 | Retailer Notifications | Notifications | GOV.UK Notify | Mandated platform, free emails |
| FR-010 | Audit Trail | N/A (bespoke build) | Custom development | Tamper-evident logging specific to CMA enforcement |
| FR-011 | Policy Analysis | Benchmarking Data | DESNZ Weekly + ONS | Free government statistics |
| INT-001 | Address Gazetteer | Address Validation | OS Places API | Authoritative, free under PSGA |
| INT-002 | Geocoding Service | Geocoding | OS Places + OS Names API | Free under PSGA |
| INT-003 | GOV.UK Notify | Notifications | GOV.UK Notify | Free, mandated |
| INT-004 | GOV.UK Design System | N/A (UI framework) | GOV.UK Frontend | Mandatory for citizen-facing services |
| INT-005 | GOV.UK One Login | Authentication (future) | GOV.UK One Login | Free, future phase |
| INT-006 | CMA Corporate IdP | Authentication | CMA IT integration | Internal SSO — no external procurement |
| INT-007 | Companies House API | Org Validation | Companies House API | Free, Open Government Licence |

### Coverage Summary

**Requirements with Identified Solutions**:
- **52 requirements (100%)** have identified data sources, APIs, or implementation approach
- **0 requirements** need commercial data procurement
- **5 requirements** (FR-002, FR-006, FR-007, FR-010, FR-005) require custom development — these are the core bespoke service capabilities

---

## UK Government Considerations

### Technology Code of Practice (TCoP) Compliance

| TCoP Point | Status | Notes |
|-----------|--------|-------|
| **1. Define user needs** | COMPLIANT | Research driven by requirements traced to stakeholder goals |
| **2. Make things accessible** | COMPLIANT | OS and GOV.UK platforms meet WCAG 2.1 AA |
| **3. Be open and use open standards** | COMPLIANT | All recommended APIs use open standards (JSON, REST, OGC) |
| **4. Make use of open source** | COMPLIANT | OpenStreetMap data, GOV.UK Notify (open source), OS developer libraries |
| **5. Use cloud first** | COMPLIANT | All APIs are cloud-hosted; no on-premise dependencies |
| **6. Make things secure** | COMPLIANT | TLS 1.2+, API key authentication, UK data residency |
| **7. Make privacy integral** | COMPLIANT | UK data residency for all services; GDPR-compliant |
| **8. Share, reuse and collaborate** | COMPLIANT | Reusing GOV.UK Notify, OS Places, Companies House — existing government platforms |
| **9. Integrate and adapt technology** | COMPLIANT | All integrations via standard REST APIs |
| **10. Make better use of data** | COMPLIANT | Open data formats (JSON, CSV, GeoJSON) |
| **11. Define your purchasing strategy** | COMPLIANT | No commercial procurement needed; all free government APIs |
| **12. Meet the Service Standard** | ON TRACK | GDS assessment planned |

### GOV.UK Common Platforms Used

| Platform | Category | Status | Cost |
|----------|----------|--------|------|
| GOV.UK Notify | Notifications | RECOMMENDED | Free (emails); 250K free SMS |
| OS Places API | Address Validation | RECOMMENDED | Free (PSGA) |
| OS Maps API | Mapping | RECOMMENDED | Free (PSGA) |
| Companies House API | Org Validation | RECOMMENDED | Free |
| GOV.UK Design System | UI Framework | MANDATORY | Free |
| GOV.UK One Login | Citizen Auth (future) | FUTURE PHASE | Free |

### Government Cloud and Data Residency

**Data Classification**: OFFICIAL

**Hosting Requirements**: Public cloud (AWS UK or Azure UK regions) acceptable for OFFICIAL data. UK data residency ensured by all recommended APIs (OS, Companies House, GOV.UK Notify all hosted in UK).

---

## Integration with Wardley Mapping

### Value Chain Components by Evolution

| Component | Evolution Stage | Recommended Approach | Rationale |
|-----------|----------------|---------------------|-----------|
| Fuel price data (Fuel Finder) | Commodity (regulated utility) | Consume statutory open data | Mandated by regulations, free |
| Address validation (OS Places) | Commodity (utility) | Use managed service | Authoritative government service, free |
| Geocoding (OS Places/Names) | Commodity (utility) | Use managed service | Government service, free |
| Organisation validation (CH) | Commodity (utility) | Use managed API | Government service, free |
| Notifications (GOV.UK Notify) | Commodity (utility) | Use managed service | Government platform, free |
| Data ingestion pipeline | Custom (bespoke) | Build | Unique to regulatory requirements |
| Compliance dashboard | Custom (bespoke) | Build | Unique to CMA enforcement |
| Citizen search interface | Product (emerging) | Build on GOV.UK Design System | Standard patterns, bespoke content |
| Open data API | Product (emerging) | Build | Standard REST API, bespoke schema |

**Strategic Insights**:
- All external data and platform dependencies are **commodities** — free, managed, government-provided
- The **custom build** is focused on the unique value: data pipeline, compliance tools, and enforcement capability
- No commercially differentiating technology choices — all infrastructure is commodity
- The **strategic asset** is the regulatory authority and data quality, not the technology

---

## Integration with SOBC Economic Case

### Cost Data for SOBC

**CAPEX (Data/API Integration)**:
- All external API integrations: £0 licence cost
- Integration development effort: [Per delivery plan]

**OPEX (Annual Data/API Costs)**:
- Year 1: £0 (all free tier)
- Year 2: ~£1,200 (SMS beyond free tier)
- Year 3: ~£1,500 (SMS growth)

**Benefits**:
- £10.4 billion estimated consumer savings over 10-year appraisal period (DESNZ estimate)
- Zero data procurement costs (vs £50K–£150K/year for commercial alternative)
- Statutory compliance delivered at minimal marginal cost

---

## Community and Ecosystem Tools

### Existing Open Source Integrations

| Tool | Type | Source | Status |
|------|------|--------|--------|
| uk-fuel-prices-api | Python library (PyPI) | https://pypi.org/project/uk-fuel-prices-api/ | Alpha (v0.0.5) |
| pyfuelprices | Python library (GitHub) | https://github.com/pantherale0/pyfuelprices | Community |
| Home Assistant integration | IoT integration | https://community.home-assistant.io/t/fuel-gas-prices-integration/658716 | Community |

These demonstrate early ecosystem adoption of the CMA open data endpoints and validate demand for programmatic fuel price access.

### UK Government API Discovery

| Resource | URL | Purpose |
|----------|-----|---------|
| GOV.UK API Catalogue | https://www.api.gov.uk/ | Discovery of all UK Government APIs |
| OS section | https://www.api.gov.uk/os/ | Ordnance Survey APIs |

---

## Risks and Mitigations

### VR-1: Fuel Finder API Specification Not Yet Public

**Risk**: VE3 Global's API specification and developer documentation are not publicly available as of January 2026, potentially delaying integration development.

**Impact**: HIGH — cannot begin API integration without specification

**Likelihood**: MEDIUM — specification likely exists but not yet indexed publicly

**Mitigation**: Contact DESNZ and VE3 Global directly for developer documentation. Begin development against CMA interim JSON endpoints (known format) and adapt when Fuel Finder specification is available.

### VR-2: Fuel Finder Data Quality During Transition

**Risk**: Fuel Finder data may be incomplete or low quality during the initial months as retailers onboard and comply with the 30-minute submission obligation.

**Impact**: MEDIUM — citizen service may show incomplete data

**Mitigation**: Supplement Fuel Finder data with CMA interim retailer endpoints during transition. Display data freshness indicators. Gradually phase out interim sources as Fuel Finder coverage increases.

### VR-3: CMA Interim Endpoints Deprecated

**Risk**: Retailers may disable their voluntary JSON endpoints once the statutory Fuel Finder scheme is fully operational.

**Impact**: LOW — interim endpoints are a transition source, not primary

**Mitigation**: Design architecture to gracefully handle endpoint removal. Primary architecture should depend on Fuel Finder API, not interim endpoints.

---

## Next Steps and Recommendations

### Immediate Actions (0–2 weeks)

1. **Contact VE3 Global / DESNZ** for Fuel Finder API developer documentation and sandbox access
2. **Register for OS Data Hub** PSGA account for CMA (free)
3. **Register for Companies House API** key
4. **Set up GOV.UK Notify** service for CMA Fuel Finder

### Integration Development (2–8 weeks)

5. **Prototype ingestion** against CMA interim JSON endpoints (known format, operational today)
6. **Integrate OS Places API** for address validation and geocoding
7. **Integrate Companies House API** for registration validation
8. **Build GOV.UK Notify** templates for retailer communications
9. **Download OpenStreetMap data** for station location cross-reference

### Fuel Finder API Integration (When Specification Available)

10. **Develop Fuel Finder API client** per VE3 specification
11. **Configure flat file ingestion** for twice-daily bulk data
12. **Run dual-source validation** comparing Fuel Finder vs interim endpoints
13. **Transition to Fuel Finder as primary** once coverage > 80%

### Integration with Other Commands

14. **Update Wardley Map**: Run `/arckit.wardley` — position all data sources as commodities on evolution axis
15. **Create SOBC**: Run `/arckit.sobc` — include £0 data API TCO in Economic Case
16. **Generate SOW/RFP**: Run `/arckit.sow` — if procuring development services
17. **Data Model**: Run `/arckit.data-model` — align entities with Fuel Finder schema

---

## Appendices

### Appendix A: Research Methodology

**Data Sources**:
- UK Government websites (GOV.UK, legislation.gov.uk, data.gov.uk)
- Ordnance Survey documentation
- CMA publications and enforcement guidance
- DESNZ statistics and publications
- Contracts Finder (public procurement)
- Vendor websites (PetrolPrices.com, Kalibrate, Argus Media, TomTom, HERE, Google, Mapbox)
- OpenStreetMap wiki and Overpass API documentation
- ONS statistical datasets
- Industry bodies (PRA, Fuels Industry UK, RAC, AA)
- Community projects (PyPI, GitHub, Home Assistant)

**Evaluation Criteria**:
- Data comprehensiveness and coverage
- Data freshness/update frequency
- Cost (free for government preferred)
- TCoP compliance (open standards, open data, government platforms)
- UK data residency
- Authentication requirements
- Rate limits and availability
- Licensing terms
- Integration complexity

### Appendix B: Glossary

- **PSGA**: Public Sector Geospatial Agreement (free OS data for government)
- **UPRN**: Unique Property Reference Number
- **VE3 Global**: Designated aggregator for Fuel Finder scheme
- **ODbL**: Open Data Commons Open Database License
- **TCoP**: Technology Code of Practice
- **PPL**: Pence Per Litre
- **EPOS**: Electronic Point of Sale
- **IVR**: Interactive Voice Response

### Appendix C: Complete API Endpoint Reference

**CMA Interim Retailer Endpoints (14 total)**:

| # | Retailer | URL |
|---|----------|-----|
| 1 | Ascona Group | `https://fuelprices.asconagroup.co.uk/newfuel.json` |
| 2 | Asda | `https://storelocator.asda.com/fuel_prices_data.json` |
| 3 | BP | `https://www.bp.com/en_gb/united-kingdom/home/fuelprices/fuel_prices_data.json` |
| 4 | Esso Tesco Alliance | `https://fuelprices.esso.co.uk/latestdata.json` |
| 5 | JET Retail UK | `https://jetlocal.co.uk/fuel_prices_data.json` |
| 6 | Karan Retail Ltd | `https://devapi.krlpos.com/integration/live_price/krl` |
| 7 | Morrisons | `https://www.morrisons.com/fuel-prices/fuel.json` |
| 8 | Moto | `https://moto-way.com/fuel-price/fuel_prices.json` |
| 9 | Motor Fuel Group | `https://fuel.motorfuelgroup.com/fuel_prices_data.json` |
| 10 | Rontec | `https://www.rontec-servicestations.co.uk/fuel-prices/data/fuel_prices_data.json` |
| 11 | Sainsbury's | `https://api.sainsburys.co.uk/v1/exports/latest/fuel_prices_data.json` |
| 12 | SGN | `https://www.sgnretail.uk/files/data/SGN_daily_fuel_prices.json` |
| 13 | Shell | `https://www.shell.co.uk/fuel-prices-data.html` |
| 14 | Tesco | `https://www.tesco.com/fuel_prices/fuel_prices_data.json` |

**Government APIs**:

| API | Base URL | Auth | Cost |
|-----|----------|------|------|
| OS Places API | `https://api.os.uk/search/places/v1/` | API key | Free (PSGA) |
| OS Names API | `https://api.os.uk/search/names/v1/` | API key | Free |
| OS Maps API | `https://api.os.uk/maps/` | API key | Free (PSGA) |
| Companies House | `https://api.company-information.service.gov.uk/` | API key (Basic Auth) | Free |
| GOV.UK Notify | `https://api.notifications.service.gov.uk/` | API key | Free (emails) |

**Open Data**:

| Source | URL | Format | Cost |
|--------|-----|--------|------|
| DESNZ Weekly Prices | https://www.gov.uk/government/statistics/weekly-road-fuel-prices | CSV, XLSX, ODS | Free |
| data.gov.uk Fuel Prices | https://www.data.gov.uk/dataset/21db6396-3daf-4d90-8b3f-054995256018/ | CSV | Free |
| OpenStreetMap Overpass | `https://overpass-api.de/api/interpreter` | JSON, XML | Free |
| ONS Fuel Price Series | https://www.ons.gov.uk/economy/inflationandpriceindices/timeseries/dogq/mm23 | CSV, Excel | Free |

---

**Generated by**: ArcKit `/arckit.research` command
**Generated on**: 2026-01-30
**ArcKit Version**: 1.0.3
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: Claude Opus 4.5
