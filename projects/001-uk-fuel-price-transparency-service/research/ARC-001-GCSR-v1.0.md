# Government Code Search Report: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit.gov-code-search`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GCSR-v1.0 |
| **Document Type** | Government Code Search Report |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-03-23 |
| **Last Modified** | 2026-03-23 |
| **Review Cycle** | On-Demand |
| **Next Review Date** | 2026-06-23 |
| **Owner** | CMA Digital Lead (Product Owner) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-23 | ArcKit AI | Initial creation from `/arckit.gov-code-search` agent — fuel price data ingestion query across UK government repositories | PENDING | PENDING |

---

## Executive Summary

### Search Query

**Original Query**: `fuel price data ingestion`

**Query Variations Used**:

- `open data ingestion pipeline real-time pricing API`
- `data collection aggregation pipeline government open data`
- `GOV.UK data feed ingestion ETL validation processing`
- `third party data submission API webhook scheduled polling`
- `alphagov data pipeline scheduled ingestion open data publishing`
- `REST API data submission validation retailer reporting compliance`
- `price transparency open data API government consumer comparison service`
- `data collection feed aggregation geospatial location finder GOV.UK`
- `CMA competition market data monitoring enforcement analytics`
- `JSON API consumer data submission scheduled batch processing`
- `flood reporting online tool public data submission validation`
- `location finder branch finder postcode search nearby facilities`
- `gritting recycling site finder geospatial API nearby services postcode`
- `open data scotland portal dataset catalogue publishing API`

**Platforms Searched**: GitHub (UK Government organisations via govreposcrape — approximately 21,000 repositories indexed)

### Results Found

**Total Repositories Scanned**: 88 (raw results across all queries, before deduplication)

**Unique Repositories Assessed**: 24 (after deduplication)

**High Relevance Results**: 4

**Medium Relevance Results**: 6

**Low Relevance / Excluded**: 14

### Top Results

| # | Repository | Organisation | Relevance | Language | Last Active |
|---|------------|--------------|-----------|----------|-------------|
| 1 | FloodOnlineReportingTool.Public | Dorset Council | High | C# / .NET | 2026-03 |
| 2 | FloodOnlineReportingTool.Contracts | Dorset Council | High | C# / .NET | 2026-03-11 |
| 3 | GIFramework-Maps | Dorset Council | High | TypeScript / C# | 2025-12-22 |
| 4 | Escc.RubbishAndRecycling.SiteFinder | East Sussex County Council | High | C# / .NET | 2022-12-13 |
| 5 | CamdenCouncil/camdenmaps | Camden Council | Medium | JavaScript (Angular) | 2024 (estimated) |

---

## Search Results

### High Relevance Results

#### FloodOnlineReportingTool.Public

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Dorset-Council-UK) |
| **Repository URL** | https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public |
| **Description** | .NET web application enabling members of the public to report flooding incidents; built on GDS Design System; uses PostgreSQL with PostGIS; includes MigrationService, AppHost, and Test projects |
| **Language** | C# (81.1%), HTML (17.8%) |
| **License** | MIT |
| **Last Activity** | 2026-03 (536 commits, actively maintained) |
| **Stars** | 0 |

**Why Relevant**: This is the closest structural analogue to the Fuel Finder service found in UK government open source. It demonstrates a mandatory public-reporting pattern: citizens (or in this case retailers) submit structured data to a government authority via a GOV.UK Design System-compliant web application. The service ingests, validates, and stores submissions in PostgreSQL/PostGIS. Its microservices decomposition (AppHost, MigrationService, Database, ServiceDefaults, Tests) maps directly onto the Fuel Finder's anticipated data submission and publication pipeline. The use of .NET Aspire (AppHost/ServiceDefaults pattern) is particularly relevant given CDDO cloud-native guidance.

**Key Patterns**:

- Microservices decomposition: AppHost orchestrates AppHost, MigrationService, and main application in a single .NET Aspire-based solution
- PostgreSQL 13+ with PostGIS for geospatial data — directly applicable to storing fuel station lat/lon coordinates and enabling proximity searches
- Entity Framework Core for data access with database-agnostic provider abstraction
- GOV.UK Design System (GDS) HTML components used in frontend, meeting WCAG 2.2 AA accessibility requirements
- MIT licence permits unrestricted reuse and forking by CMA digital team

---

#### FloodOnlineReportingTool.Contracts

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Dorset-Council-UK) |
| **Repository URL** | https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts |
| **Description** | C# class library defining message contracts (commands and events) for inter-service communication across the FORT distributed system using a messaging framework |
| **Language** | C# (100%) |
| **License** | MIT |
| **Last Activity** | 2026-03-11 (v3.2.0, 13 releases, 109 commits) |
| **Stars** | 0 |

**Why Relevant**: This companion repository to FORT.Public demonstrates the message-contract pattern used to decouple data submission from data processing in a distributed government service. For the Fuel Finder, the equivalent contracts would define commands (e.g., `SubmitFuelPrices`, `ValidateFuelStationRecord`) and events (e.g., `FuelPricesReceived`, `ValidationFailed`, `PricesPublished`). The pattern of separating contracts into a standalone library enables independent versioning of producer and consumer services — critical for a service where approximately 8,500 retailers submit data on varying schedules.

**Key Patterns**:

- Separate NuGet-publishable contracts library — enables independent versioning between submission API and processing pipeline
- Command/Event message types align with an event-driven ingestion pattern (submit to validate to publish)
- Distributed system architecture using async messaging — decouples retailer-facing submission API from internal processing
- Active release cadence (v3.2.0, March 2026) indicates mature, production-grade pattern
- MIT licence permits direct reuse as a reference architecture for Fuel Finder contract definitions

---

#### GIFramework-Maps

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Dorset-Council-UK) |
| **Repository URL** | https://github.com/Dorset-Council-UK/GIFramework-Maps |
| **Description** | .NET and TypeScript web mapping application for creating, sharing, and managing web maps using data from multiple OGC web services; used in production by Dorset Council staff and public |
| **Language** | TypeScript (42.7%), C# (37.6%), HTML (18.1%) |
| **License** | MIT |
| **Last Activity** | 2025-12-22 (v1.10.0, 202 commits) |
| **Stars** | 21 |

**Why Relevant**: GIFramework Maps demonstrates how a UK council builds a production geospatial web service that ingests data from multiple OGC web service sources, stores spatial data in PostgreSQL/PostGIS, and exposes it to end users. The Fuel Finder's "find fuel stations near me" citizen-facing feature requires the same stack: geospatial data ingest, PostGIS proximity queries, and a mapping frontend. The 21 stars and 12 forks indicate broader adoption beyond Dorset, making it the most widely adopted geospatial codebase identified in this search.

**Key Patterns**:

- OGC web services integration — standard protocol for ingesting external geospatial data feeds, applicable to consuming fuel station location data
- PostgreSQL 13+ with PostGIS — shared stack with FORT.Public; consistent recommendation across Dorset Council repos
- OpenLayers for web mapping — open-source mapping library preferred over commercial alternatives, meeting TCoP open standards requirements
- .NET backend with TypeScript/Bootstrap frontend — well-supported stack within GDS/CDDO guidance
- Entity Framework Core with database-agnostic provider abstraction — testable data layer
- Deployable to IIS, Kestrel, or Azure — flexible hosting matches UK Government cloud preferences

---

#### Escc.RubbishAndRecycling.SiteFinder

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council |
| **Repository URL** | https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder |
| **Description** | ASP.NET application enabling postcode-based search for waste and recycling sites; consumes a JSON data feed API for facility data and the GOV.UK locate-api for postcode geocoding |
| **Language** | C# (69.9%), PowerShell (11.3%), HTML (6.8%) |
| **License** | Available via LICENSE.md |
| **Last Activity** | 2022-12-13 (72 commits) |
| **Stars** | 0 |

**Why Relevant**: This repository demonstrates the consumer side of a "find nearest facility" service built by a UK local authority. Its pattern of consuming a JSON facility-data API combined with GOV.UK locate-api for postcode-to-coordinates conversion is directly analogous to the Fuel Finder citizen search journey. The interface-based architecture for both external dependencies allows the Fuel Finder team to swap implementations (e.g., use OS Names API instead of locate-api) without changing core business logic.

**Key Patterns**:

- GOV.UK locate-api for postcode-to-lat/lon geocoding — standard government approach, avoids commercial geocoding costs
- JSON API consumption with configurable endpoint URLs — 12-factor app configuration via settings files
- Interface-based abstraction for external dependencies — enables unit testing without live API calls
- Two query modes: proximity search (postcode filter) and full listing (for search engine crawling) — dual-mode useful for Fuel Finder open data API
- Umbraco CMS integration for content management — shows pattern of separating dynamic data (API) from editorial content (CMS)

---

### Medium Relevance Results

#### CamdenCouncil/camdenmaps

| Attribute | Value |
|-----------|-------|
| **Organisation** | Camden Council |
| **Repository URL** | https://github.com/CamdenCouncil/camdenmaps |
| **Description** | "Where's My Nearest" citizen-facing service at maps.camden.gov.uk; Angular.js frontend with Node.js/Express backend; Selenium-based end-to-end tests; Gulp build tooling |
| **Language** | JavaScript (82.9%), CSS (9.7%), HTML (7.1%) |
| **License** | Not specified |
| **Last Activity** | 2024 (estimated; 1,750 commits on dev branch) |
| **Stars** | Not stated |

**Why Relevant**: Demonstrates a JavaScript-stack approach to a proximity/nearest-facility citizen service. The Node.js/Express pattern for serving location data JSON to a frontend map is a simpler alternative to the .NET stack used by Dorset and East Sussex repos. The 1,750 commits indicate long-term production use. The absence of licence information is a reuse blocker without further clarification from Camden.

**Key Patterns**:

- Angular.js SPA consuming a backend JSON API — JavaScript-native alternative to .NET approach
- Node.js/Express as lightweight JSON API server for location data
- Selenium end-to-end tests for location-based search journeys
- Gulp build pipeline for frontend asset compilation

---

#### DundeeCityCouncil/OpenData

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dundee City Council |
| **Repository URL** | https://github.com/DundeeCityCouncil/OpenData |
| **Description** | Jupyter Notebook repository of code samples illustrating how to consume Dundee's open geospatial datasets; thematic directories for recycling, streets, and analysis |
| **Language** | Jupyter Notebook (100%) |
| **License** | Varies per dataset — check licence conditions before reuse |
| **Last Activity** | Not stated (14 commits, master branch) |
| **Stars** | Not stated |

**Why Relevant**: Provides reference examples of how local authorities structure and document open data offerings, including location datasets. Relevant as a pattern for how the Fuel Finder open data API and developer documentation might be structured. The Jupyter Notebook format is appropriate for CMA policy analysts consuming fuel price data for enforcement analytics.

**Key Patterns**:

- Thematic organisation of open datasets (recycling, streets, analysis) — applicable model for a fuel price open data catalogue
- Jupyter Notebook samples for data consumption — useful for CMA policy analysts consuming fuel price data
- Per-dataset licensing documentation — good practice for Fuel Finder's open data licence documentation under Motor Fuel Price Regulations 2025

---

#### DundeeCityCouncil/open-data-scotland

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dundee City Council |
| **Repository URL** | https://github.com/DundeeCityCouncil/open-data-scotland |
| **Description** | Python-maintained CSV catalogue of Scottish open data portals; lists sites providing bulk download, documented API, or SPARQL endpoint access |
| **Language** | Python (92.3%), Makefile (7.7%) |
| **License** | Available via LICENSE.md |
| **Last Activity** | Not stated (45 commits, master branch) |
| **Stars** | Not stated |

**Why Relevant**: Demonstrates the metadata catalogue approach to open data publishing — maintaining a machine-readable directory of datasets with standardised access methods. The Fuel Finder's open data API discovery documentation could adopt the same structured catalogue pattern, making it easy for third parties (mapping apps, price comparison services) to find and consume fuel price data.

**Key Patterns**:

- CSV-based machine-readable data catalogue with standardised access method fields
- Python Makefile build for catalogue generation — simple, reproducible open data publishing
- Inclusion criteria (bulk download, documented API, or SPARQL endpoint) — maps to Fuel Finder's open data publication obligations under the Motor Fuel Price (Open Data) Regulations 2025

---

#### Dorset-Council-UK/GdsBlazorComponents

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/GdsBlazorComponents |
| **Description** | Blazor components implementing GOV.UK Design System styling for use in .NET Blazor web applications; originally created for the Flood Online Reporting Tool |
| **Language** | HTML (45.1%), C# (41.1%), TypeScript (8.1%) |
| **License** | MIT |
| **Last Activity** | 2026-03-20 (v3.0.0, 297 commits, actively maintained) |
| **Stars** | Not stated |

**Why Relevant**: Directly relevant if the Fuel Finder delivery team adopts Blazor for the retailer registration/submission portal or citizen-facing search interface. These components remove the need to manually implement GDS Design System patterns in .NET Blazor, accelerating delivery of a compliant frontend. Created by the same Dorset Council team responsible for FORT, so validated in production against GDS standards.

**Key Patterns**:

- GDS Design System components (buttons, forms, tables, navigation) as reusable Blazor components
- Supports both Blazor Web App and Blazor WebAssembly variants
- Active release cadence (v3.0.0, March 2026) — not abandoned
- MIT licence — freely reusable without restriction

---

#### east-sussex-county-council/Escc.Libraries.BranchFinder

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council |
| **Repository URL** | https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder |
| **Description** | ASP.NET "Find your library" tool consuming a postcode API and a JSON library data feed to return nearest library branches |
| **Language** | C# (68.1%), PowerShell, HTML, JavaScript |
| **License** | Available via LICENSE.md |
| **Last Activity** | 2022-12-07 (70 commits) |
| **Stars** | 0 |

**Why Relevant**: Structural twin of Escc.RubbishAndRecycling.SiteFinder, confirming the East Sussex pattern of building facility-finder services as thin ASP.NET consumers of JSON data feeds backed by GOV.UK locate-api. The duplicated pattern across two independent services strengthens confidence in the approach. Its interface-based design and configurable endpoint URLs are directly applicable reference code for the Fuel Finder's station search feature.

**Key Patterns**:

- Identical architectural pattern to SiteFinder: postcode geocoding API plus JSON facility data API
- Interface abstraction enabling testable, swappable external service dependencies
- Configuration-driven endpoint URLs for all external dependencies
- Modest codebase size (70 commits) — demonstrates a finder service need not be large or complex to be production-ready

---

## Code Patterns Identified

| Pattern | Repositories Using It | Description |
|---------|-----------------------|-------------|
| PostgreSQL + PostGIS for geospatial data | FloodOnlineReportingTool.Public, GIFramework-Maps | Both Dorset Council services use PostgreSQL 13+ with PostGIS for storing and querying spatial data. PostGIS enables proximity queries (e.g., fuel stations within 5 miles) directly in SQL without application-layer geo-calculations. This is the predominant UK government geospatial data store pattern in this search. |
| GOV.UK locate-api for postcode geocoding | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder | Both East Sussex services use the GOV.UK locate-api to convert user-entered postcodes into lat/lon coordinates, avoiding commercial geocoding costs and keeping the citizen journey within government infrastructure. |
| Interface-based external service abstraction | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder | Both repos define C# interfaces for all external API calls, with production and test implementations. This enables unit testing without network calls and allows swapping data providers without code changes. |
| Event-driven microservices with message contracts | FloodOnlineReportingTool.Contracts, FloodOnlineReportingTool.Public | The FORT ecosystem separates commands and events into a standalone NuGet library. Services communicate asynchronously — submission API publishes a command; the processing service consumes it; the publication service responds to a processed event. This decouples high-volume retailer submission from the aggregation and publication pipeline. |
| Entity Framework Core with provider agnosticism | FloodOnlineReportingTool.Public, GIFramework-Maps | Both Dorset services use EF Core with explicit support for alternative compatible providers. This reduces database vendor lock-in, consistent with TCoP open standards requirements. |
| .NET Aspire orchestration (AppHost / ServiceDefaults) | FloodOnlineReportingTool.Public | The FORT repo separates AppHost and ServiceDefaults projects — a .NET 8/9 Aspire pattern for local development orchestration and cloud-native deployment. This is the most modern .NET pattern identified and aligns with CDDO cloud-native service guidance. |
| GDS Design System in .NET contexts | FloodOnlineReportingTool.Public, GdsBlazorComponents | Both FORT and the companion component library implement GOV.UK Design System patterns in C#/.NET. GdsBlazorComponents offers a ready-made Blazor component library for teams adopting that framework. |
| JSON facility data feed consumption | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder, CamdenCouncil/camdenmaps | All three finder services consume external JSON APIs for facility data at configurable endpoints. This mirrors the Fuel Finder's core data flow: retailers POST JSON price data to an ingestion API; the citizen-facing search service consumes aggregated data from the same store. |
| Configuration-driven endpoint URLs (12-factor app) | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder | All external API URLs and authentication tokens stored in configuration rather than code. This enables deployment across dev, staging, and production environments without code changes — aligned with the 12-factor app methodology recommended in CDDO cloud guidance. |
| MIT licence for government open source | FloodOnlineReportingTool.Public, FloodOnlineReportingTool.Contracts, GIFramework-Maps, GdsBlazorComponents | All four highest-relevance repositories use the MIT licence, consistent with GDS guidance that government open source should use permissive licences. This allows the Fuel Finder team to fork and adapt any of these repos without licence friction. |

**Observations**: The dominant pattern across UK local government open source for this type of service is a .NET (C#) backend with PostgreSQL/PostGIS for geospatial data, consuming external JSON APIs for operational data, and exposing a GOV.UK Design System-compliant frontend. Dorset Council's Flood Online Reporting Tool suite is the most architecturally mature example, having evolved to .NET Aspire microservices with event-driven message contracts — a production-grade government pattern directly relevant to the Fuel Finder's data ingestion and publication pipeline. No central government repositories (alphagov, HMRC, DWP, NHS) appeared in search results for fuel-price-specific or general data ingestion pipeline queries, suggesting this domain is novel at central government level. Local council analogues represent the closest available government reuse candidates. The search coverage limitation should be noted: govreposcrape indexes approximately 21,000 UK government repositories, which is a subset of all government open-source activity; HMRC and DWP maintain additional private repositories not searchable here.

---

## Implementation Approaches Compared

| Approach | Used By | Pros | Cons |
|----------|---------|------|------|
| .NET Aspire microservices with event-driven contracts | FloodOnlineReportingTool.Public + Contracts | Decouples retailer submission from validation and publication; supports high volume (approx. 8,500 stations); independently scalable services; cloud-native; actively maintained by Dorset Council | Higher operational complexity; requires message broker infrastructure (e.g., Azure Service Bus or RabbitMQ); steeper learning curve for smaller teams |
| ASP.NET JSON API consumer with interface abstraction | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder | Simple and proven pattern; easy to unit test; low operational overhead; well-understood by .NET developers across government | Synchronous API consumption may not scale to 8,500 concurrent submissions; no built-in retry or dead-letter handling; tightly couples submission and processing steps |
| JavaScript SPA + Node.js/Express backend | CamdenCouncil/camdenmaps | Lightweight; familiar to frontend-heavy teams; rapid iteration; large npm ecosystem | No licence confirmed — reuse blocked without clarification; Angular.js is end-of-life; no evidence of GDS Design System compliance; less suited to regulated data submission context |
| Python scripts for open data cataloguing | DundeeCityCouncil/open-data-scotland | Very simple; suitable for batch processing and data catalogue generation; good for analytical workloads | Not suitable for real-time ingestion; no web application or API layer; appropriate only for the open data publication catalogue side of Fuel Finder |

**Recommended Approach for This Project**: .NET Aspire microservices with event-driven contracts (as demonstrated by FloodOnlineReportingTool) — this pattern handles the Fuel Finder's specific challenge of decoupling high-volume retailer data submission (approximately 8,500 stations, submitting on different schedules) from validation, aggregation, and publication. The event-driven approach ensures a slow or failing validation step does not block submission ingestion. PostgreSQL/PostGIS handles the geospatial proximity queries needed for the citizen search journey. The GOV.UK Design System integration ensures GDS service assessment compliance. This recommendation should be validated against the delivery team's .NET capability and the infrastructure provisioning timelines given the immovable May 2026 enforcement deadline.

---

## Recommendations

### Immediate Next Steps

1. **Clone and Review FORT.Public**: Clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public — examine the AppHost project, MigrationService, and database schema to understand how public submissions are ingested, stored, and processed. The PostgreSQL/PostGIS schema is directly applicable to the Fuel Finder's fuel station and price data model.

2. **Clone and Review FORT.Contracts**: Clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts — use this as a reference for designing the Fuel Finder's own message contract library. Define command types (`SubmitFuelPrices`, `RegisterFuelStation`) and event types (`PricesValidated`, `PricesPublished`, `ValidationFailed`, `StationNonCompliant`) following the same NuGet library pattern.

3. **Fork GIFramework-Maps for Citizen Map View**: Evaluate https://github.com/Dorset-Council-UK/GIFramework-Maps as the basis for the citizen-facing map view showing nearby fuel stations and prices. The OGC web services ingestion, PostGIS spatial queries, and OpenLayers frontend are all immediately applicable. Confirm MIT licence compatibility with Crown copyright delivery obligations.

4. **Evaluate GdsBlazorComponents if adopting Blazor**: If the delivery team selects Blazor for the retailer registration portal, adopt https://github.com/Dorset-Council-UK/GdsBlazorComponents (v3.0.0, MIT) to avoid rebuilding GDS Design System components from scratch. Run a compatibility spike against the project's target .NET version.

5. **Contact Dorset Council**: Reach out to fort@dorsetcouncil.gov.uk to discuss similarities between Fuel Finder and FORT, potential for knowledge sharing, and lessons learned from operating a public data submission service under UK data protection requirements and GDS service assessment.

6. **License Verification**: Confirm MIT licence compatibility with Crown copyright obligations for all Dorset Council repos before forking. Consult GDS open source guidance and Cabinet Office legal team if uncertain.

### Search Refinements

If further searching is needed, consider these refined queries:

- `alphagov open-data-api JSON schema validation publication` — may surface GDS-produced data pipeline tooling not returned in current searches
- `HMRC bulk data submission filing API validation` — HMRC runs high-volume third-party data submission services (Self Assessment, Making Tax Digital) analogous to retailer price submissions; many repos may be private
- `DWP data ingest batch processing government service` — DWP processes large-volume structured submissions with validation pipelines
- `NHS data collection real-time feed aggregation API` — NHS has extensive data ingestion patterns that, while health-specific, demonstrate well-proven government data pipeline architecture
- `DVLA vehicle data API open government licence` — DVLA's open vehicle data APIs demonstrate government open data API design patterns relevant to the Fuel Finder's public API

### Related ArcKit Commands

- Run `/arckit:gov-reuse` for a full reusability assessment of the FORT.Public, FORT.Contracts, and GIFramework-Maps repositories against the Fuel Finder project stack and timelines
- Run `/arckit:research` for a broader technology landscape analysis covering data ingestion frameworks (Apache Kafka, Azure Event Hubs, AWS Kinesis) applicable to the approximately 8,500 station submission volume requirement

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-001-REQ-v2.0 | Requirements | Project repository | Data submission API requirements, throughput NFRs, geospatial search requirements, retailer registration | projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md |
| ARC-001-DATA-v1.0 | Data Model | Project repository | Fuel station and price data entities, geospatial coordinate fields | projects/001-uk-fuel-price-transparency-service/ARC-001-DATA-v1.0.md |

---

**Generated by**: ArcKit `/arckit.gov-code-search` agent
**Generated on**: 2026-03-23
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: claude-sonnet-4-6
