# Government Code Search Report: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit.gov-code-search`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GCSR-v2.0 |
| **Document Type** | Government Code Search Report |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 2.0 |
| **Created Date** | 2026-03-23 |
| **Last Modified** | 2026-03-24 |
| **Review Cycle** | On-Demand |
| **Next Review Date** | 2026-06-24 |
| **Owner** | CMA Digital Lead (Product Owner) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-23 | ArcKit AI | Initial creation from `/arckit.gov-code-search` agent -- fuel price data ingestion query across UK government repositories | PENDING | PENDING |
| 2.0 | 2026-03-24 | ArcKit AI | Major update: expanded to 10 query variations (up from 14 in v1.0), 169 raw results (up from 88), 32 unique repositories assessed (up from 24). Added new repos: BristolCityCouncil/send (Spring Boot + Cosmos DB structured submission), BathnesDevelopment/OpenDataScripts, BathnesDevelopment/BathApp (Ionic mobile app with location services), CityOfYork/Lucene-Entity-Search-Tools (search indexing). Refreshed all v1.0 repo metadata. Strengthened search effectiveness assessment. Added project relevance mapping table. | PENDING | PENDING |

---

## Executive Summary

### Search Query

**Original Query**: `fuel price data ingestion`

**Query Variations Used**:

- `fuel price data ingestion`
- `real-time data ingestion pipeline government open data API processing validation`
- `data submission API retailer compliance reporting bulk upload validation`
- `price comparison service location finder postcode search geospatial nearby`
- `CMA competition markets authority data collection enforcement monitoring`
- `alphagov data pipeline ETL batch processing scheduled ingestion open data publishing`
- `HMRC bulk data submission filing API validation JSON schema`
- `event driven message queue async processing data validation pipeline microservices`
- `open data API REST JSON publication government register catalogue dataset`
- `GOV.UK Notify integration email SMS alerts compliance notification government service`

**Platforms Searched**: GitHub (UK Government organisations via govreposcrape -- approximately 24,500 repositories indexed)

### Results Found

**Total Raw Results**: 169 (across all 10 query variations, before deduplication)

**Unique Repositories Assessed**: 32 (after deduplication)

**High Relevance Results**: 5

**Medium Relevance Results**: 7

**Low Relevance / Excluded**: 20

### Top Results

| # | Repository | Organisation | Relevance | Language | Last Active |
|---|------------|--------------|-----------|----------|-------------|
| 1 | FloodOnlineReportingTool.Public | Dorset Council | High | C# / .NET | 2026-03 |
| 2 | FloodOnlineReportingTool.Contracts | Dorset Council | High | C# | 2026-03-11 |
| 3 | GIFramework-Maps | Dorset Council | High | TypeScript / C# | 2025-12-22 |
| 4 | send | Bristol City Council | High | Java (Spring Boot) | 2022-06-06 |
| 5 | Escc.RubbishAndRecycling.SiteFinder | East Sussex County Council | High | C# / .NET | 2022-12-13 |

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

**Why Relevant**: This remains the closest structural analogue to the Fuel Finder service in UK government open source. It demonstrates a mandatory public-reporting pattern: citizens (or in the Fuel Finder case, retailers) submit structured data to a government authority via a GOV.UK Design System-compliant web application. The service ingests, validates, and stores submissions in PostgreSQL/PostGIS. Its microservices decomposition (AppHost, MigrationService, Database, ServiceDefaults, Tests) maps directly onto the Fuel Finder's anticipated data submission and publication pipeline. The use of .NET Aspire (AppHost/ServiceDefaults pattern) aligns with CDDO cloud-native guidance. Appeared in 6 of 10 search queries, confirming broad relevance.

**Key Patterns**:

- Microservices decomposition: AppHost orchestrates application, MigrationService, and database in a single .NET Aspire-based solution
- PostgreSQL 13+ with PostGIS for geospatial data -- directly applicable to storing fuel station lat/lon coordinates and enabling proximity searches
- Entity Framework Core for data access with database-agnostic provider abstraction
- GOV.UK Design System (GDS) HTML components in frontend, meeting WCAG 2.2 AA accessibility requirements
- MIT licence permits unrestricted reuse and forking by the CMA digital team
- Used by councils across southwest England, demonstrating production-grade reliability

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

**Why Relevant**: This companion repository to FORT.Public demonstrates the message-contract pattern used to decouple data submission from data processing in a distributed government service. For the Fuel Finder, the equivalent contracts would define commands (e.g., `SubmitFuelPrices`, `ValidateFuelStationRecord`) and events (e.g., `FuelPricesReceived`, `ValidationFailed`, `PricesPublished`). The pattern of separating contracts into a standalone library enables independent versioning of producer and consumer services -- critical for a service where approximately 8,500 retailers submit data on varying schedules. Appeared in 3 of 10 queries.

**Key Patterns**:

- Separate NuGet-publishable contracts library -- enables independent versioning between submission API and processing pipeline
- Command/Event message types align with an event-driven ingestion pattern (submit to validate to publish)
- Distributed system architecture using async messaging -- decouples retailer-facing submission API from internal processing
- Active release cadence (v3.2.0, March 2026) indicates mature, production-grade pattern
- MIT licence permits direct reuse as a reference architecture for Fuel Finder contract definitions
- Security contact published (fort@dorsetcouncil.gov.uk) indicating responsible disclosure process

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

**Why Relevant**: GIFramework Maps demonstrates how a UK council builds a production geospatial web service that ingests data from multiple OGC web service sources, stores spatial data in PostgreSQL/PostGIS, and exposes it to end users. The Fuel Finder's "find fuel stations near me" citizen-facing feature requires the same stack: geospatial data ingest, PostGIS proximity queries, and a mapping frontend. With 21 stars and 12 forks, this is the most widely adopted geospatial codebase identified in this search. v1.10.0 added annotation management, PDF export, GPS tracking and export, multiple configurable search services, and Azure AD authentication. Appeared in 5 of 10 queries.

**Key Patterns**:

- OGC web services integration -- standard protocol for ingesting external geospatial data feeds, applicable to consuming fuel station location data
- PostgreSQL 13+ with PostGIS -- shared stack with FORT.Public; consistent recommendation across Dorset Council repos
- OpenLayers for web mapping -- open-source mapping library preferred over commercial alternatives, meeting TCoP open standards requirements
- .NET backend with TypeScript/Bootstrap frontend -- well-supported stack within GDS/CDDO guidance
- Entity Framework Core with database-agnostic provider abstraction -- testable data layer
- Deployable to IIS, Kestrel, or Azure -- flexible hosting matches UK Government cloud preferences
- Azure AD authentication support for secure deployments

---

#### BristolCityCouncil/send

| Attribute | Value |
|-----------|-------|
| **Organisation** | Bristol City Council (BristolCityCouncil) |
| **Repository URL** | https://github.com/BristolCityCouncil/send |
| **Description** | Special Educational Needs funding assessment application enabling structured data submission from schools to the local authority, with workflow-based processing, validation, and document generation |
| **Language** | Java (84.8%) |
| **License** | Available (see repository) |
| **Last Activity** | 2022-06-06 |
| **Stars** | 0 |

**Why Relevant**: This is a new finding not present in the v1.0 search. The SEND application demonstrates a structured data submission pattern from external parties (schools) to a government authority (Bristol City Council) -- directly analogous to fuel retailers submitting price data to the CMA. The application guides users through assessment creation, data validation, and submission with PDF generation. Its use of Azure Cosmos DB (NoSQL, JSON format) for storing submitted assessments is an alternative data architecture pattern to the PostgreSQL approach seen in the Dorset Council repos. The ClamAV virus scanning integration for document uploads is relevant to the Fuel Finder if file attachments are accepted. Appeared in 4 of 10 queries.

**Key Patterns**:

- Spring Boot (Java 11) structured data submission application -- alternative technology stack to .NET
- Azure Cosmos DB (NoSQL) for storing submitted assessments in JSON format -- alternative to PostgreSQL for document-oriented submission data
- Active Directory authentication for submitting parties (schools/retailers)
- ClamAV virus scanning integration for uploaded documents
- Microsoft Graph API integration for SharePoint document storage
- FreeMarker templating for PDF generation from submitted data
- Workflow-based processing: create assessment, document needs, select provisions, submit with validation
- Phase 2 enhancements added funding calculations, duplicate removal, and email confirmations -- demonstrates iterative government service delivery

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

**Why Relevant**: This repository demonstrates the consumer side of a "find nearest facility" service built by a UK local authority. Its pattern of consuming a JSON facility-data API combined with GOV.UK locate-api for postcode-to-coordinates conversion is directly analogous to the Fuel Finder citizen search journey. The interface-based architecture for both external dependencies allows the Fuel Finder team to swap implementations (e.g., use OS Names API instead of locate-api) without changing core business logic. Appeared in 3 of 10 queries.

**Key Patterns**:

- GOV.UK locate-api for postcode-to-lat/lon geocoding -- standard government approach, avoids commercial geocoding costs
- JSON API consumption with configurable endpoint URLs -- 12-factor app configuration via settings files
- Interface-based abstraction for external dependencies -- enables unit testing without live API calls
- Two query modes: proximity search (postcode filter) and full listing (for search engine crawling) -- dual-mode useful for Fuel Finder open data API
- NuGet package integration for Umbraco CMS environments

---

### Medium Relevance Results

#### CamdenCouncil/camdenmaps

| Attribute | Value |
|-----------|-------|
| **Organisation** | Camden Council |
| **Repository URL** | https://github.com/CamdenCouncil/camdenmaps |
| **Description** | "Where's My Nearest" citizen-facing service at maps.camden.gov.uk; Angular.js frontend with Node.js backend; comprehensive test suite; Gulp build tooling |
| **Language** | JavaScript (82.9%), CSS (9.7%), HTML (7.1%) |
| **License** | Not specified |
| **Last Activity** | Estimated 2024 (1,750 commits on dev branch) |
| **Stars** | 0 |

**Why Relevant**: Demonstrates a JavaScript-stack approach to a proximity/nearest-facility citizen service. The Node.js/Express pattern for serving location data JSON to a frontend map is a simpler alternative to the .NET stack used by Dorset and East Sussex repos. The 1,750 commits indicate long-term production use. The absence of licence information is a reuse blocker without further clarification from Camden. Travis CI with automated Heroku deployment demonstrates CI/CD practices. Appeared in 6 of 10 queries -- the joint highest frequency alongside FORT.Public.

**Key Patterns**:

- Angular.js SPA consuming a backend JSON API -- JavaScript-native alternative to .NET approach
- Node.js as lightweight JSON API server for location data
- Mocha unit tests, WebDriver/Selenium end-to-end tests, SauceLabs integration
- Travis CI with automated Heroku deployment on master branch
- Gulp build pipeline for frontend asset compilation

---

#### DundeeCityCouncil/OpenData

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dundee City Council |
| **Repository URL** | https://github.com/DundeeCityCouncil/OpenData |
| **Description** | Jupyter Notebook repository of code samples illustrating how to consume Dundee's open geospatial datasets; thematic directories for recycling, streets, and analysis |
| **Language** | Jupyter Notebook (100%) |
| **License** | Mixed licensing -- not all data publishable under OGL |
| **Last Activity** | Not stated (14 commits, master branch) |
| **Stars** | 0 |

**Why Relevant**: Provides reference examples of how local authorities structure and document open data offerings, including location datasets. Relevant as a pattern for how the Fuel Finder open data API and developer documentation might be structured. The Jupyter Notebook format is appropriate for CMA policy analysts consuming fuel price data for enforcement analytics and trend analysis.

**Key Patterns**:

- Thematic organisation of open datasets (recycling, streets, analysis) -- applicable model for a fuel price open data catalogue
- Jupyter Notebook samples for data consumption -- useful for CMA/DESNZ policy analysts consuming fuel price data
- Per-dataset licensing documentation -- good practice for Fuel Finder's open data licence documentation under Motor Fuel Price (Open Data) Regulations 2025
- Explicit licensing complexity acknowledgement (not all data is OGL) -- relevant caution for Fuel Finder data that may include commercially sensitive retailer information

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
| **Stars** | 0 |

**Why Relevant**: Demonstrates the metadata catalogue approach to open data publishing -- maintaining a machine-readable directory of datasets with standardised access methods. The inclusion criteria (bulk download, documented API, or SPARQL endpoint) maps well to the Fuel Finder's open data publication obligations. Appeared in 4 of 10 queries.

**Key Patterns**:

- CSV-based machine-readable data catalogue with standardised access method fields
- Python Makefile build for catalogue generation -- simple, reproducible open data publishing
- Inclusion criteria (bulk download, documented API, or SPARQL endpoint) -- maps to Fuel Finder's open data publication obligations under the Motor Fuel Price (Open Data) Regulations 2025
- Forked from okfnscot/open-data-scotland, demonstrating government open data community collaboration

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
| **Stars** | 4 |

**Why Relevant**: Directly relevant if the Fuel Finder delivery team adopts Blazor for the retailer registration/submission portal or citizen-facing search interface. Provides 30+ GOV.UK Design System components covering form inputs, selection controls, layout elements, feedback components, and data display. Created by the same Dorset Council team responsible for FORT, validated in production against GDS standards. Appeared in 4 of 10 queries.

**Key Patterns**:

- 30+ GDS Design System components: text inputs, date inputs, checkboxes, radios, selects, breadcrumbs, footer, header, error messages, notifications, banners, tables, panels, tags
- Supports both Blazor Web App and Blazor WebAssembly variants
- Active release cadence (v3.0.0, March 2026) -- not abandoned
- MIT licence -- freely reusable without restriction
- Integration via CSS/JS asset inclusion and `@using GdsBlazorComponents` directive

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

**Why Relevant**: Structural twin of Escc.RubbishAndRecycling.SiteFinder, confirming the East Sussex pattern of building facility-finder services as thin ASP.NET consumers of JSON data feeds backed by GOV.UK locate-api. The duplicated pattern across two independent services strengthens confidence in the approach. Appeared in 3 of 10 queries.

**Key Patterns**:

- Identical architectural pattern to SiteFinder: postcode geocoding API plus JSON facility data API
- Interface abstraction enabling testable, swappable external service dependencies
- Configuration-driven endpoint URLs for all external dependencies
- Modest codebase size (70 commits) -- demonstrates a finder service need not be large or complex to be production-ready

---

#### BathnesDevelopment/BathApp

| Attribute | Value |
|-----------|-------|
| **Organisation** | Bath and North East Somerset Council (BathnesDevelopment) |
| **Repository URL** | https://github.com/BathnesDevelopment/BathApp |
| **Description** | Ionic Framework cross-platform mobile application (MYPlace) providing residents with location-based local information and civic services including nearby facility search |
| **Language** | JavaScript (82.8%) |
| **License** | MIT |
| **Last Activity** | 2015-03-10 (303 commits) |
| **Stars** | 0 |

**Why Relevant**: New finding not in v1.0. While dated (2015), this is one of the few UK government open-source mobile applications demonstrating a "find nearest" pattern on a mobile device. It originated from a 2014 community hackathon. Relevant to the Fuel Finder's future in-car/mobile use case (Persona 7: Mike). The Open 311 GeoReport integration for issue reporting is an interesting pattern for standardised API submission.

**Key Patterns**:

- Ionic Framework + Apache Cordova for cross-platform mobile app (iOS/Android)
- Leaflet for interactive mapping on mobile devices
- Open 311 GeoReport standard integration for structured civic reporting -- standardised submission API pattern
- Address-based data retrieval from council iShare system
- D3/NVD3 for data visualisation
- Location-aware service discovery with geolocation

---

## Code Patterns Identified

| Pattern | Repositories Using It | Description |
|---------|-----------------------|-------------|
| PostgreSQL + PostGIS for geospatial data | FloodOnlineReportingTool.Public, GIFramework-Maps | Both Dorset Council services use PostgreSQL 13+ with PostGIS for storing and querying spatial data. PostGIS enables proximity queries (e.g., fuel stations within 5 miles) directly in SQL without application-layer geo-calculations. This is the predominant UK government geospatial data store pattern in this search. |
| GOV.UK locate-api for postcode geocoding | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder | Both East Sussex services use the GOV.UK locate-api to convert user-entered postcodes into lat/lon coordinates, avoiding commercial geocoding costs and keeping the citizen journey within government infrastructure. |
| Interface-based external service abstraction | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder, BristolCityCouncil/send | All three repos define interfaces for external API calls, with production and test implementations. This enables unit testing without network calls and allows swapping data providers without code changes. |
| Event-driven microservices with message contracts | FloodOnlineReportingTool.Contracts, FloodOnlineReportingTool.Public | The FORT ecosystem separates commands and events into a standalone NuGet library. Services communicate asynchronously -- submission API publishes a command; the processing service consumes it; the publication service responds to a processed event. This decouples high-volume retailer submission from the aggregation and publication pipeline. |
| Entity Framework Core with provider agnosticism | FloodOnlineReportingTool.Public, GIFramework-Maps | Both Dorset services use EF Core with explicit support for alternative compatible providers. This reduces database vendor lock-in, consistent with TCoP open standards requirements. |
| .NET Aspire orchestration (AppHost / ServiceDefaults) | FloodOnlineReportingTool.Public | The FORT repo separates AppHost and ServiceDefaults projects -- a .NET 8/9 Aspire pattern for local development orchestration and cloud-native deployment. This is the most modern .NET pattern identified and aligns with CDDO cloud-native service guidance. |
| GDS Design System in .NET contexts | FloodOnlineReportingTool.Public, GdsBlazorComponents | Both FORT and the companion component library implement GOV.UK Design System patterns in C#/.NET. GdsBlazorComponents offers a ready-made Blazor component library (30+ components) for teams adopting that framework. |
| JSON facility data feed consumption | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder, CamdenCouncil/camdenmaps | All three finder services consume external JSON APIs for facility data at configurable endpoints. This mirrors the Fuel Finder's core data flow: retailers POST JSON price data to an ingestion API; the citizen-facing search service consumes aggregated data from the same store. |
| Structured data submission from external parties | BristolCityCouncil/send, FloodOnlineReportingTool.Public | Both applications accept structured data submissions from external parties (schools, members of the public) with validation, workflow processing, and document generation. This is the core Fuel Finder pattern: retailers submit structured price data that is validated, processed, and published. |
| NoSQL document store for submissions | BristolCityCouncil/send | Bristol's SEND app uses Azure Cosmos DB to store JSON assessment submissions. This is an alternative to the relational PostgreSQL pattern, better suited to variable-schema document submissions. Relevant if the Fuel Finder needs to handle varying submission formats during the transition period. |
| Configuration-driven endpoint URLs (12-factor app) | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder, BristolCityCouncil/send | All external API URLs and authentication tokens stored in configuration rather than code. Enables deployment across dev, staging, and production environments without code changes -- aligned with the 12-factor app methodology recommended in CDDO cloud guidance. |
| MIT licence for government open source | FloodOnlineReportingTool.Public, FloodOnlineReportingTool.Contracts, GIFramework-Maps, GdsBlazorComponents, BathApp | Five of the highest-relevance repositories use the MIT licence, consistent with GDS guidance that government open source should use permissive licences. |

**Observations**: The dominant pattern across UK local government open source for this type of service remains a .NET (C#) backend with PostgreSQL/PostGIS for geospatial data, consuming external JSON APIs for operational data, and exposing a GOV.UK Design System-compliant frontend. Dorset Council's Flood Online Reporting Tool suite is the most architecturally mature example, having evolved to .NET Aspire microservices with event-driven message contracts -- a production-grade government pattern directly relevant to the Fuel Finder's data ingestion and publication pipeline. The addition of BristolCityCouncil/send in this v2.0 search introduces a Java/Spring Boot alternative with Azure Cosmos DB, broadening the technology comparison. No central government repositories (alphagov, HMRC, DWP, NHS, MOJ) appeared in search results despite targeted queries including "HMRC bulk data submission" and "alphagov data pipeline". This confirms the v1.0 finding that this domain is novel at central government level, and local council analogues remain the closest available government reuse candidates. The search index (govreposcrape, approximately 24,500 repos) is biased towards local authorities; many central government data pipelines exist in private repositories not indexed here.

---

## Implementation Approaches Compared

| Approach | Used By | Pros | Cons |
|----------|---------|------|------|
| .NET Aspire microservices with event-driven contracts | FloodOnlineReportingTool.Public + Contracts | Decouples retailer submission from validation and publication; supports high volume (approx. 8,500 stations); independently scalable services; cloud-native; actively maintained by Dorset Council; MIT licence | Higher operational complexity; requires message broker infrastructure (e.g., Azure Service Bus or RabbitMQ); steeper learning curve for smaller teams |
| Spring Boot + Azure Cosmos DB structured submission | BristolCityCouncil/send | Proven Java-based government submission pattern; Azure Cosmos DB handles variable-schema JSON submissions; workflow-based processing; Active Directory authentication; ClamAV malware scanning | Java 11 (not the latest LTS); Cosmos DB vendor lock-in to Azure; last updated June 2022 -- may not reflect current best practices; licence not explicitly confirmed as permissive |
| ASP.NET JSON API consumer with interface abstraction | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder | Simple and proven pattern; easy to unit test; low operational overhead; well-understood by .NET developers across government; postcode geocoding via GOV.UK locate-api | Synchronous API consumption may not scale to 8,500 concurrent submissions; no built-in retry or dead-letter handling; tightly couples submission and processing steps |
| JavaScript SPA + Node.js/Express backend | CamdenCouncil/camdenmaps | Lightweight; familiar to frontend-heavy teams; comprehensive test suite (unit, integration, E2E); CI/CD via Travis CI; 1,750 commits showing production maturity | No licence confirmed -- reuse blocked; Angular.js is end-of-life; no evidence of GDS Design System compliance; less suited to regulated data submission context |
| Ionic cross-platform mobile app | BathnesDevelopment/BathApp | Cross-platform mobile (iOS/Android); Leaflet mapping; Open 311 standard API for structured submissions; MIT licence | Dated (2015); Ionic v1/Cordova superseded by modern frameworks; not actively maintained; not suitable for primary data ingestion but relevant to mobile consumption pattern |
| Python scripts for open data cataloguing | DundeeCityCouncil/open-data-scotland | Very simple; suitable for batch processing and data catalogue generation; good for analytical workloads; reproducible via Makefile | Not suitable for real-time ingestion; no web application or API layer; appropriate only for the open data publication catalogue side of Fuel Finder |

**Recommended Approach for This Project**: .NET Aspire microservices with event-driven contracts (as demonstrated by FloodOnlineReportingTool) -- this pattern handles the Fuel Finder's specific challenge of decoupling high-volume retailer data submission (approximately 8,500 stations, submitting on different schedules) from validation, aggregation, and publication. The event-driven approach ensures a slow or failing validation step does not block submission ingestion. PostgreSQL/PostGIS handles the geospatial proximity queries needed for the citizen search journey. The GOV.UK Design System integration (enhanced by GdsBlazorComponents if using Blazor) ensures GDS service assessment compliance. The Spring Boot + Cosmos DB approach from Bristol is a credible alternative if the delivery team has stronger Java capabilities, though the .NET ecosystem has stronger representation across the government repos identified. This recommendation should be validated against the delivery team's capabilities and the infrastructure provisioning timelines given the immovable May 2026 enforcement deadline.

---

## Project Relevance Mapping

| Repository | Relevant Requirements | How It Helps | Quick Start |
|---|---|---|---|
| Dorset-Council-UK/FloodOnlineReportingTool.Public | FR-001 (Registration), FR-002 (Manual Submission), FR-005 (Validation), NFR-P (Performance), NFR-SEC (Security) | Reference architecture for public data submission service with validation, PostGIS geospatial storage, GDS frontend, .NET Aspire microservices decomposition | `git clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public.git` |
| Dorset-Council-UK/FloodOnlineReportingTool.Contracts | FR-003 (API Submission), INT-001 (Integration Points), DR-001 (Data Processing) | Message contract library pattern for event-driven ingestion pipeline -- template for `SubmitFuelPrices`, `PricesValidated`, `PricesPublished` commands/events | `git clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts.git` |
| Dorset-Council-UK/GIFramework-Maps | FR-006 (Citizen Map Search), FR-007 (Location-Based Results), INT-003 (OS/Geo Integration) | Production geospatial web mapping application with PostGIS, OpenLayers, OGC web services -- forkable for citizen fuel station map view | `git clone https://github.com/Dorset-Council-UK/GIFramework-Maps.git` |
| BristolCityCouncil/send | FR-002 (Manual Submission), FR-005 (Validation), FR-009 (Document Generation) | Alternative submission architecture (Spring Boot + Cosmos DB) with workflow validation, PDF generation, virus scanning | `git clone https://github.com/BristolCityCouncil/send.git` |
| Dorset-Council-UK/GdsBlazorComponents | FR-001 (Registration UI), FR-002 (Submission UI), NFR-A (Accessibility) | 30+ ready-made GOV.UK Design System Blazor components -- accelerates GDS-compliant frontend delivery | `dotnet add package GdsBlazorComponents` (if published to NuGet) or `git clone https://github.com/Dorset-Council-UK/GdsBlazorComponents.git` |
| east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder | FR-006 (Citizen Search), FR-007 (Postcode Lookup) | Proven GOV.UK locate-api postcode geocoding + JSON facility API pattern for "find nearest" citizen journey | `git clone https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder.git` |
| DundeeCityCouncil/open-data-scotland | BR-005 (Open Data Publication), INT-005 (Open Data API) | Open data catalogue structure with machine-readable access method metadata -- model for Fuel Finder's API developer portal | `git clone https://github.com/DundeeCityCouncil/open-data-scotland.git` |

---

## Search Effectiveness Assessment

### Coverage

The 10 query variations covered the following aspects of the original "fuel price data ingestion" information need:

- **Data ingestion pipeline patterns**: Partially covered. The FORT microservices pattern is the strongest match. No dedicated ETL/data pipeline repositories (e.g., Apache Airflow, dbt, or Kafka-based pipelines) were found in the government index.
- **Structured data submission from external parties**: Well covered. FORT.Public and BristolCityCouncil/send both demonstrate this pattern.
- **Geospatial facility-finder services**: Well covered. GIFramework-Maps, SiteFinder, BranchFinder, and camdenmaps collectively demonstrate the citizen search journey.
- **Open data publication**: Partially covered. Dundee's open-data-scotland and OpenData repos show catalogue patterns but no production API publication patterns were found.
- **Event-driven processing**: Partially covered. FORT.Contracts shows the message contract pattern, but no complete message broker implementations (RabbitMQ, Azure Service Bus consumers) were found.
- **CMA/Competition enforcement**: Not covered. No enforcement monitoring, compliance dashboards, or case management tools were found in any government open-source repository. This is expected -- enforcement tools are typically internal-use-only.
- **Central government data pipelines**: Not covered. Despite targeted queries for alphagov, HMRC, DWP, and NHS patterns, no central government data pipeline repos appeared. These are likely in private repositories.

### Gaps

| Gap | Alternative Search Strategy |
|-----|---------------------------|
| No alphagov/GDS data pipeline repos | Search directly: `https://github.com/alphagov?q=data+pipeline&type=repositories`. Also check GOV.UK Registers codebase: `https://github.com/openregister` |
| No HMRC Making Tax Digital submission pattern repos | HMRC repos are mostly private. API documentation is public: `https://developer.service.hmrc.gov.uk/api-documentation`. WebSearch: `HMRC Making Tax Digital API architecture` |
| No NHS data ingestion pipeline repos | Check NHSDigital org directly: `https://github.com/NHSDigital?q=data+pipeline`. NHS Spine/MESH messaging patterns are documented at `https://digital.nhs.uk/services/message-exchange-for-social-care-and-health-mesh` |
| No enforcement/compliance monitoring tools | These are internal government tools unlikely to be open-sourced. Reference: HMRC Risk and Intelligence Service patterns, Ofgem enforcement tools. WebSearch: `UK government regulatory enforcement dashboard architecture` |
| No message broker implementation patterns | WebSearch: `site:github.com/alphagov RabbitMQ OR "Azure Service Bus"`. Also check: `https://github.com/alphagov/govuk-puppet` for infrastructure patterns |
| No GOV.UK Notify integration examples in council repos | GOV.UK Notify client libraries are at `https://github.com/alphagov/notifications-python-client` (Python), `https://github.com/alphagov/notifications-java-client` (Java), `https://github.com/alphagov/notifications-net-client` (.NET) |

### Index Limitations

The govreposcrape index (approximately 24,500 repositories) has the following biases relevant to this search:

- **Dominated by local authorities**: Dorset Council, East Sussex County Council, Camden Council, Dundee City Council, Bath and North East Somerset Council, Bracknell Forest Council, and Brighton & Hove account for the vast majority of results. Central government departments (alphagov, HMRC, DWP, MOJ, Home Office, DESNZ, DEFRA) are underrepresented or absent from results.
- **Technology bias towards .NET/C#**: The most active local authority repos (Dorset, East Sussex) are predominantly .NET. Central government teams more commonly use Ruby, Python, Java, and Node.js, but these repos did not surface.
- **No fuel-specific repos exist**: There are no UK government open-source repositories specifically addressing fuel pricing, fuel station data, or motor fuel regulation. The Fuel Finder service will be the first of its kind.
- **Private repos not indexed**: HMRC, DWP, and MOJ maintain substantial private codebases. HMRC's Making Tax Digital (the closest central government analogue to mass external data submission) is not available via this search.

---

## Recommendations

### Immediate Next Steps

1. **Clone and Review FORT.Public**: Clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public -- examine the AppHost project, MigrationService, and database schema to understand how public submissions are ingested, stored, and processed. The PostgreSQL/PostGIS schema is directly applicable to the Fuel Finder's fuel station and price data model.

2. **Clone and Review FORT.Contracts**: Clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts -- use this as a reference for designing the Fuel Finder's own message contract library. Define command types (`SubmitFuelPrices`, `RegisterFuelStation`) and event types (`PricesValidated`, `PricesPublished`, `ValidationFailed`, `StationNonCompliant`) following the same NuGet library pattern.

3. **Fork GIFramework-Maps for Citizen Map View**: Evaluate https://github.com/Dorset-Council-UK/GIFramework-Maps as the basis for the citizen-facing map view showing nearby fuel stations and prices. The OGC web services ingestion, PostGIS spatial queries, and OpenLayers frontend are all immediately applicable. Confirm MIT licence compatibility with Crown copyright delivery obligations.

4. **Evaluate BristolCityCouncil/send as Alternative Architecture**: If the delivery team has Java/Spring Boot expertise, review https://github.com/BristolCityCouncil/send for an alternative submission architecture. The Cosmos DB + workflow pattern may suit the early-phase retailer registration workflow where submission schemas are still being finalised.

5. **Evaluate GdsBlazorComponents if adopting Blazor**: If the delivery team selects Blazor for the retailer registration portal, adopt https://github.com/Dorset-Council-UK/GdsBlazorComponents (v3.0.0, MIT) to avoid rebuilding 30+ GDS Design System components from scratch. Run a compatibility spike against the project's target .NET version.

6. **Contact Dorset Council**: Reach out to fort@dorsetcouncil.gov.uk to discuss similarities between Fuel Finder and FORT, potential for knowledge sharing, and lessons learned from operating a public data submission service under UK data protection requirements and GDS service assessment.

7. **License Verification**: Confirm MIT licence compatibility with Crown copyright obligations for all Dorset Council repos before forking. Confirm BristolCityCouncil/send licence terms. Consult GDS open source guidance and Cabinet Office legal team if uncertain.

### Search Refinements

If further searching is needed, consider these refined queries:

- `alphagov open-data-api JSON schema validation publication` -- may surface GDS-produced data pipeline tooling not returned in current searches
- `HMRC bulk data submission filing API validation` -- HMRC runs high-volume third-party data submission services (Self Assessment, Making Tax Digital) analogous to retailer price submissions; many repos may be private
- `DWP data ingest batch processing government service` -- DWP processes large-volume structured submissions with validation pipelines
- `NHS data collection real-time feed aggregation API` -- NHS has extensive data ingestion patterns that, while health-specific, demonstrate well-proven government data pipeline architecture
- `DVLA vehicle data API open government licence` -- DVLA's open vehicle data APIs demonstrate government open data API design patterns relevant to the Fuel Finder's public API
- `PostgreSQL PostGIS geospatial query nearest location government` -- narrow search for spatial query implementations

### Related ArcKit Commands

- Run `/arckit:gov-reuse` for a full reusability assessment of the FORT.Public, FORT.Contracts, GIFramework-Maps, and BristolCityCouncil/send repositories against the Fuel Finder project stack and timelines
- Run `/arckit:research` for a broader technology landscape analysis covering data ingestion frameworks (Apache Kafka, Azure Event Hubs, AWS Kinesis) applicable to the approximately 8,500 station submission volume requirement

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-001-REQ-v2.0 | Requirements | Project repository | Data submission API requirements, throughput NFRs, geospatial search requirements, retailer registration, in-car platform use case | projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md |
| ARC-001-DATA-v1.0 | Data Model | Project repository | Fuel station and price data entities, geospatial coordinate fields | projects/001-uk-fuel-price-transparency-service/ARC-001-DATA-v1.0.md |
| ARC-001-GCSR-v1.0 | Previous Search | Project repository | Baseline search results -- 88 raw results, 24 unique repos, 4 high relevance | projects/001-uk-fuel-price-transparency-service/research/ARC-001-GCSR-v1.0.md |

---

**Generated by**: ArcKit `/arckit.gov-code-search` agent
**Generated on**: 2026-03-24
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: Claude Opus 4.6 (1M context)
