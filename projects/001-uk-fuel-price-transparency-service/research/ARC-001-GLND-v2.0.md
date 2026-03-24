# Government Landscape Analysis: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit.gov-landscape`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GLND-v2.0 |
| **Document Type** | Government Landscape Analysis |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 2.0 |
| **Created Date** | 2026-03-24 |
| **Last Modified** | 2026-03-24 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-06-24 |
| **Owner** | CMA Digital Lead (Product Owner) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-23 | ArcKit AI | Initial creation from `/arckit.gov-landscape` agent -- 12 govreposcrape queries executed, 15 repositories WebFetch assessed | PENDING | PENDING |
| 2.0 | 2026-03-24 | ArcKit AI | Major revision -- expanded to 12 govreposcrape queries (278 raw results, 62 unique repos after deduplication), 20 repositories WebFetch assessed, 10 organisation pages reviewed. Significant new findings: Dorset Council CSIDE (Blazor/.NET 9 + GOV.UK Notify + Azure AD B2C), notifications-net-client (GOV.UK Notify .NET fork), GdsBlazorComponents-Demo. Updated all activity dates from WebFetch. Expanded organisation profiles with full repo inventories. Added search effectiveness assessment. Strengthened project relevance mapping. | PENDING | PENDING |

---

## Executive Summary

### Domain Overview

The domain of **fuel price open data, real-time pricing services, consumer price transparency, and competition regulation** sits at the intersection of regulatory enforcement, energy policy, open data publication, and citizen-facing digital services. Under the Motor Fuel Price (Open Data) Regulations 2025, approximately 8,500 UK fuel forecourts are mandated to publish real-time pricing data. The Fuel Finder service must ingest, validate, and re-publish this data as a free open dataset while providing citizens with a location-based price comparison tool and equipping the CMA with compliance monitoring and enforcement capabilities.

This landscape analysis searched approximately 21,000 UK government open-source repositories across local authorities, central government departments, NHS bodies, and arms-length bodies to map existing code, patterns, and standards relevant to building this service. Twelve search queries were executed against the govreposcrape index, yielding 278 raw results that reduced to 62 unique repositories across 10 organisations after deduplication. Twenty repositories were assessed in detail via WebFetch, and 10 organisation GitHub pages were reviewed.

The findings confirm the v1.0 assessment's central conclusion: **no government organisation has built a direct equivalent** -- a national, regulatory-mandated fuel price data ingestion and publication service -- in open source. However, this v2.0 analysis identifies a significantly stronger reuse baseline than v1.0 reported, principally through the discovery of **Dorset Council's CSIDE application** (a .NET 9 Blazor system using GOV.UK Notify, Azure AD B2C, PostgreSQL/PostGIS, and OS DataHub) and their **GOV.UK Notify .NET client fork**. These findings, combined with the previously identified GIFramework-Maps and FORT repositories, establish Dorset Council as the single most architecturally relevant organisation in the indexed government open-source landscape for this project.

The landscape matters because it defines the reuse baseline: what the team can adopt rather than build, which organisations to engage for collaboration, and where genuine build-from-scratch effort is unavoidable.

**Domain**: Fuel Price Open Data / Real-Time Pricing Services / Consumer Price Transparency / Competition and Markets Regulation / Geospatial Facility Finders / Government Open Data Platforms

**Analysis Date**: 2026-03-24

**Platforms Searched**: GitHub (UK Government organisations via govreposcrape -- approximately 21,000 repositories indexed), supplemented by direct WebFetch assessment of 20 repositories and 10 organisation pages

### Organisations Identified

**Total Organisations**: 10

**Central Government / Cross-Government**: 1 (GDS / alphagov -- assessed via prior research; not directly in govreposcrape results but mandatory platform dependency)

**Arms Length Bodies / NDPBs**: 0 (CMA and DESNZ have no relevant public open-source repositories)

**Local Government**: 8 (Dorset Council, East Sussex County Council, Dundee City Council, Bath and North East Somerset Council, Camden Council, Brighton and Hove, City of York, Bracknell Forest Council)

**NHS / Health**: 0

**International Equivalents**: 1 (noted for reference -- Ireland's CCPC fuel price checker; not in govreposcrape scope)

### Repositories Analysed

**Total Repositories Found**: 62 unique repositories (across 12 searches, after deduplication)

**Active (commits < 6 months)**: 5

**Maintained (commits 6-18 months)**: 3

**Stale (commits > 18 months)**: 10

**Archived / Abandoned**: 4

### Key Findings

- **Most Active Organisations**: Dorset Council (Dorset-Council-UK) -- 8 domain-relevant repos including 3 actively developed in 2026; East Sussex County Council (east-sussex-county-council) -- 93 total repos, maintained; GDS/alphagov -- platform mandates
- **Dominant Tech Stack**: C# / .NET (ASP.NET, Blazor, .NET 9), TypeScript, JavaScript; PostgreSQL + PostGIS for geospatial; Azure services (AD B2C, Blob Storage)
- **Common Standards**: GOV.UK Design System (GDS), GOV.UK Notify, MIT Licence, Open Government Licence, PostgreSQL/PostGIS for geospatial data, GOV.UK locate-api for postcode lookup, Azure AD / AD B2C for authentication
- **Maturity Level**: Mixed -- Dorset Council's GIFramework-Maps, CSIDE, and GdsBlazorComponents are Production-Grade to Mature; FORT repos are Mature; East Sussex finder repos are Developing but stale; all open data catalogue repos are Experimental

---

## Domain Landscape Map

### Organisations Overview

| Organisation | Repos Found | Primary Language | Focus Area | Activity Level |
|-------------|-------------|-----------------|------------|----------------|
| [Dorset Council UK](https://github.com/Dorset-Council-UK) | 15 (8 domain-relevant) | C# / TypeScript | Data submission portals, web mapping, GDS-compliant UI, countryside management, GOV.UK Notify | Active |
| [East Sussex County Council](https://github.com/east-sussex-county-council) | 93 (14 domain-relevant) | C# | Location-based finder services, postcode search, address lookup, CMS integration, Azure services | Maintained |
| [Dundee City Council](https://github.com/DundeeCityCouncil) | 8 (5 domain-relevant) | Python / JavaScript / C# | GIS open data catalogues, ArcGIS-based mapping, land and property gazetteer | Stale |
| [Bath and NE Somerset Council](https://github.com/BathnesDevelopment) | 17 (4 domain-relevant) | JavaScript / C# / PHP | Open data scripts, public web apps, geographic needs, design standards | Stale |
| [Bristol City Council](https://github.com/BristolCityCouncil) | 4 (2 domain-relevant) | Java / JavaScript | SEN funding assessments (Spring Boot / Azure Cosmos DB), frontend toolkit | Stale |
| [Camden Council](https://github.com/CamdenCouncil) | 3 (2 domain-relevant) | JavaScript / HTML | Location-based "Where's My Nearest" mapping, UX asset library | Stale |
| [Brighton and Hove](https://github.com/brighton-hove-gov-uk) | 1 | PHP | Public budget engagement tool with CSV export | Stale |
| [City of York Council](https://github.com/CityOfYork) | 1 | C# | Full-text entity search library (Lucene.NET) -- archived | Archived |
| [Bracknell Forest Council](https://github.com/BracknellForestCouncil) | 3 (0 domain-relevant) | N/A | Backup repos and government.github.com fork only | Stale |
| [GDS / alphagov](https://github.com/alphagov) | -- | JavaScript / Python / Ruby | GOV.UK shared platform: Frontend, Notify, Pay, Registers -- mandatory platform | Active |

**Legend**: Active (commits < 6 months) | Maintained (6-18 months) | Stale ( > 18 months)

---

### Dorset Council UK

**GitHub**: https://github.com/Dorset-Council-UK

**Total Public Repos**: 15

**Focus**: Dorset Council's digital and GIS teams build open-source tools for citizen-facing environmental reporting, countryside access management, geospatial data presentation, and GDS-compliant UI components. Their repositories represent the most architecturally relevant government code in the indexed landscape for this project. Of particular note for v2.0 is the discovery of **CSIDE** (Countryside Management System), which uses the same technology stack as GIFramework-Maps but adds GOV.UK Notify integration, Azure AD B2C authentication, and OS DataHub -- all capabilities directly required by the Fuel Finder. Additionally, their **notifications-net-client** fork confirms active use of the GOV.UK Notify .NET client, validating the .NET + Notify integration path.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [GIFramework-Maps](https://github.com/Dorset-Council-UK/GIFramework-Maps) | .NET web mapping application -- OpenLayers, Bootstrap, PostgreSQL/PostGIS, Azure AD auth, OGC services. 202 commits, v1.10.0 | TypeScript / C# | 21 | 2025-12-22 (release) |
| [CSIDE](https://github.com/Dorset-Council-UK/CSIDE) | .NET 9 Blazor countryside management system -- Azure AD B2C, PostgreSQL/PostGIS, Azure Blob Storage, GOV.UK Notify, OS DataHub. 145 commits, v1.2.0 | C# | 0 | 2026-03-18 (release) |
| [GdsBlazorComponents](https://github.com/Dorset-Council-UK/GdsBlazorComponents) | Blazor component library implementing 29 GOV.UK Design System components -- v3.0.0 | C# / HTML | 4 | 2026-03-20 (release) |
| [FloodOnlineReportingTool.Public](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public) | Citizen-facing flood reporting portal -- data submission, validation, GOV.UK Design System, PostgreSQL/PostGIS | C# | 0 | 2025-06-17 |
| [FloodOnlineReportingTool.Contracts](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts) | Message contract definitions for FORT inter-service communication (commands and events) -- 13 releases, v3.2.0 | C# | 0 | 2026-03-11 |
| [notifications-net-client](https://github.com/Dorset-Council-UK/notifications-net-client) | Fork of alphagov/notifications-net-client -- GOV.UK Notify .NET API client | C# | 0 | 2026-03-18 |
| [GdsBlazorComponents-Demo](https://github.com/Dorset-Council-UK/GdsBlazorComponents-Demo) | Demo application showcasing GdsBlazorComponents library -- .NET 10 SDK | HTML / C# | 0 | 2026-02-05 |
| [qgis-configurable-search](https://github.com/Dorset-Council-UK/qgis-configurable-search) | QGIS plugin for multi-source search across APIs and layers -- JSON config export/import | Python | 0 | 2024-12-03 |

**Architectural Approach**: Modern .NET stack (.NET 9, Blazor, Entity Framework Core) with microservices-influenced patterns. Message-based inter-service communication via versioned contracts library. PostgreSQL/PostGIS for all spatial data. Azure ecosystem: AD B2C for authentication, Blob Storage for media, GOV.UK Notify for notifications. GDS Design System compliance via custom Blazor component library. OGC standards for geospatial services. GitHub Actions CI/CD. Deployable to IIS, Kestrel, or Azure.

**Standards Followed**: GOV.UK Design System, GOV.UK Notify, MIT Licence, Open Government Licence 3.0, WCAG accessibility (via GDS components), Azure AD B2C, OGC WFS/WMS, OS DataHub, GitHub Actions CI/CD

---

### East Sussex County Council

**GitHub**: https://github.com/east-sussex-county-council

**Total Public Repos**: 93

**Focus**: East Sussex County Council maintains the largest repository portfolio in the landscape, predominantly comprising Umbraco CMS customisations for their main website. Of highest relevance to the Fuel Finder are their location-based finder services -- a pattern of postcode-to-coordinates geocoding (via GOV.UK locate-api) followed by proximity-sorted results retrieval. This is the closest analogue in government open source to the "find fuel stations near me" capability. Their Azure services integration library and cloud cache refresh pattern (now archived) demonstrate early cloud adoption, though most of their codebase targets legacy .NET Framework and IIS hosting.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [Escc.RubbishAndRecycling.SiteFinder](https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder) | Postcode-based waste and recycling site finder -- GOV.UK locate-api, JSON data API, distance sorting | C# | 0 | 2015-04-13 |
| [Escc.Libraries.BranchFinder](https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder) | "Find your library" tool -- postcode geocoding, Umbraco JSON API, proximity results, 1 fork | C# | 0 | 2022-12-07 |
| [Escc.AddressAndPersonalDetails](https://github.com/east-sussex-county-council/Escc.AddressAndPersonalDetails) | Address capture and validation library with postcode lookup | C# | 0 | 2022-12 |
| [Escc.Gritting.GrittingMap](https://github.com/east-sussex-county-council/Escc.Gritting.GrittingMap) | Real-time gritter vehicle location tracking on Google Maps -- ARCHIVED 2019 | C# / JS | 0 | 2019-06 |
| [Escc.Services.Azure](https://github.com/east-sussex-county-council/Escc.Services.Azure) | Azure Storage Queue implementations for asynchronous email processing | C# | 0 | 2014-06-20 |
| [cloud-umbraco-cache-refresh](https://github.com/east-sussex-county-council/cloud-umbraco-cache-refresh) | Distributed cache invalidation for cloud Umbraco instances -- ARCHIVED 2019 | C# | 0 | 2019-06-13 |
| [Escc.Feeds](https://github.com/east-sussex-county-council/Escc.Feeds) | RSS and data feed processing library -- ARCHIVED 2019 | C# | 0 | 2019-06-13 |
| [Escc.WebApplicationSetupScripts](https://github.com/east-sussex-county-council/Escc.WebApplicationSetupScripts) | PowerShell IIS setup automation -- app pool, website, SSL config. 1 star, 2 forks | PowerShell | 1 | 2015-01-14 |

**Architectural Approach**: ASP.NET (legacy .NET Framework) with interface-based abstraction for external API dependencies (GOV.UK locate-api, Umbraco data APIs). Monolithic web application architecture. IIS hosting with PowerShell deployment automation. Early Azure Queue adoption for async processing. No containerisation evidence.

**Standards Followed**: GOV.UK locate-api for postcode geocoding, interface abstraction for testability and vendor independence, unit test projects included, consistent NuGet packaging

---

### Bristol City Council

**GitHub**: https://github.com/BristolCityCouncil

**Total Public Repos**: 4

**Focus**: Bristol City Council maintains a small but notable set of repositories. Their `send` application (Special Educational Needs funding assessment) is the only Java/Spring Boot application in the landscape, using Azure Cosmos DB -- an architectural outlier. Their `web_styles` frontend toolkit (4 stars, 3 forks) represents one of the more community-adopted local government frontend resources.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [send](https://github.com/BristolCityCouncil/send) | SEN funding assessment app -- Spring Boot, Azure Cosmos DB, Active Directory, SharePoint integration, ClamAV scanning | Java | 0 | 2022-06-06 |
| [web_styles](https://github.com/BristolCityCouncil/web_styles) | Frontend toolkit for Bristol council websites -- 4 stars, 3 forks | JavaScript | 4 | 2014-02-10 |

**Architectural Approach**: Java 11 / Spring Boot with layered architecture. Azure Cosmos DB for NoSQL JSON storage. Active Directory authentication via Microsoft Graph API. SharePoint integration for document storage. ClamAV for file scanning. GDPR-conscious design (minimal PII storage).

**Standards Followed**: GDPR-by-design (stores only UPN and assessment IDs), file virus scanning, AD authentication

---

### Dundee City Council

**GitHub**: https://github.com/DundeeCityCouncil

**Total Public Repos**: 8

**Focus**: Dundee City Council's GIS team maintains repositories focused on geospatial data management, ArcGIS/ESRI tooling, and open data cataloguing. Their `open-data-scotland` repository (a fork of Open Knowledge Foundation Scotland) catalogues Scottish open data portals. The `CAG-tools` repository manages land and property gazetteer data in the Data Transfer Format (DTF 7.3) -- a niche but relevant data processing pattern.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [open-data-scotland](https://github.com/DundeeCityCouncil/open-data-scotland) | Curated catalogue of Scottish open data portals (fork of okfnscot) | Python | 0 | 2015-09 |
| [CAG-tools](https://github.com/DundeeCityCouncil/CAG-tools) | Land and property gazetteer data processing in DTF 7.3 format -- record type extraction | C# | 0 | Unknown |
| [OpenData](https://github.com/DundeeCityCouncil/OpenData) | Jupyter notebook code samples for Dundee's geospatial open data APIs | Jupyter Notebook | 0 | Unknown |
| [GIS](https://github.com/DundeeCityCouncil/GIS) | ArcGIS web mapping utilities and tools | JavaScript | 0 | Unknown |
| [WABWidgets](https://github.com/DundeeCityCouncil/WABWidgets) | ArcGIS Web AppBuilder custom widgets | JavaScript | 0 | Unknown |

**Architectural Approach**: ArcGIS/ESRI platform-dependent tooling. Python scripting for data workflows. Jupyter notebooks for data exploration. C# console applications for data processing. No cloud-native or GDS-aligned patterns.

**Standards Followed**: GPL-3.0, AGPL-3.0 (ArcGIS widgets), DTF 7.3 data format

---

### Bath and North East Somerset Council

**GitHub**: https://github.com/BathnesDevelopment

**Total Public Repos**: 17

**Focus**: B&NES Council's IT Development team maintains internal digital tools, open data utilities, and SharePoint customisations. Their development standards document and geographic needs web application are of marginal relevance. Most repositories are 2015-era and inactive.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [OpenDataScripts](https://github.com/BathnesDevelopment/OpenDataScripts) | Scripts to publish data from backend systems as open data | Unknown | 1 | 2015-02 |
| [GeographicalNeeds-Web](https://github.com/BathnesDevelopment/GeographicalNeeds-Web) | Web application for geographic needs assessment | JavaScript | 0 | Unknown |
| [BathnesDevelopment-Standards](https://github.com/BathnesDevelopment/BathnesDevelopment-Standards) | Development standards documentation | Unknown | 0 | Unknown |
| [BathApp](https://github.com/BathnesDevelopment/BathApp) | Public-facing mobile web application for Bath | JavaScript | 0 | Unknown |

**Architectural Approach**: PHP, JavaScript, C#, and PowerShell across various tools. Predominantly SharePoint-integrated. Drupal for public websites. No modern DevOps patterns evident.

**Standards Followed**: Minimal -- development standards document exists but no evidence of GDS, CI/CD, or modern standards adoption

---

### Camden Council

**GitHub**: https://github.com/CamdenCouncil

**Total Public Repos**: 3

**Focus**: Camden Council's `camdenmaps` repository implements a "Where's My Nearest" service -- a location-based facility finder web application. Their `camden-asset-library` provides UX guidelines and Bootstrap templates for their digital platform. Both repos are inactive (2015 vintage).

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [camdenmaps](https://github.com/CamdenCouncil/camdenmaps) | "Where's My Nearest" location-based service finder -- AngularJS, Gulp, Selenium tests, Travis CI, Heroku deployment | JavaScript | 0 | 2015-04-29 |
| [camden-asset-library](https://github.com/CamdenCouncil/camden-asset-library) | UX guidance, Bootstrap templates, and reference implementation for Camden digital platform | HTML / JS / CSS | 0 | Unknown |

**Architectural Approach**: Single-page application (AngularJS/Browserify) with server-side API. Heroku deployment. Selenium acceptance testing with SauceLabs cross-browser testing. Travis CI for CI/CD.

**Standards Followed**: End-to-end test coverage, Heroku deployment pipeline, Bootstrap-based design system

---

### Minor Contributors

| Organisation | Repos | Key Repo | Relevance | Status |
|-------------|-------|----------|-----------|--------|
| [Brighton and Hove](https://github.com/brighton-hove-gov-uk) | 1 | [bhbudget](https://github.com/brighton-hove-gov-uk/bhbudget) -- PHP budget engagement tool with CSV export | Low -- citizen engagement pattern only | Stale (2014) |
| [City of York Council](https://github.com/CityOfYork) | 1 | [Lucene-Entity-Search-Tools](https://github.com/CityOfYork/Lucene-Entity-Search-Tools) -- .NET Lucene search library, 3 stars, 2 forks, Apache-2.0 | Low -- entity search pattern reference only | Archived (2017) |
| [Bracknell Forest Council](https://github.com/BracknellForestCouncil) | 3 | government.github.com fork, backup repos | None -- no domain-relevant code | Stale |

---

## Technology Stack Analysis

### Languages

| Language | Repo Count | Percentage | Notable Projects |
|----------|------------|------------|-----------------|
| C# | 22 | 36% | CSIDE, GIFramework-Maps, FloodOnlineReportingTool.Public, GdsBlazorComponents, notifications-net-client, Escc.RubbishAndRecycling.SiteFinder, CAG-tools, Lucene-Entity-Search-Tools |
| JavaScript / TypeScript | 15 | 24% | GIFramework-Maps (TS), camdenmaps (JS), DundeeCityCouncil/GIS, web_styles, camden-asset-library |
| HTML / CSS | 5 | 8% | GdsBlazorComponents-Demo, camden-asset-library, BathApp |
| Python | 4 | 6% | open-data-scotland, qgis-configurable-search |
| Java | 1 | 2% | BristolCityCouncil/send (Spring Boot) |
| Jupyter Notebook | 1 | 2% | DundeeCityCouncil/OpenData |
| PHP | 1 | 2% | bhbudget |
| PowerShell | 1 | 2% | Escc.WebApplicationSetupScripts |
| Other / Markdown / Mixed | 12 | 18% | Documentation repos, config repos, SharePoint customisations |

### Frameworks

| Framework | Language | Repo Count | Notes |
|-----------|----------|------------|-------|
| ASP.NET / .NET (various versions) | C# | 10 | Dominant pattern across local gov; mix of .NET Framework (East Sussex) and .NET 9 (Dorset) |
| Blazor (.NET 9/10) | C# | 3 | CSIDE, GdsBlazorComponents, GdsBlazorComponents-Demo -- modern .NET SPA pattern |
| Entity Framework Core | C# | 4 | CSIDE, FORT, GIFramework-Maps -- ORM over PostgreSQL/PostGIS |
| OpenLayers | TypeScript | 2 | GIFramework-Maps, CSIDE -- open-source web mapping library |
| Bootstrap | TypeScript/HTML | 3 | GIFramework-Maps, GdsBlazorComponents, camden-asset-library |
| Spring Boot | Java | 1 | BristolCityCouncil/send -- Java outlier in otherwise .NET landscape |
| AngularJS | JavaScript | 1 | camdenmaps -- legacy framework, effectively unsupported |
| MkDocs Material | Markdown | 2 | DorsetExplorer-Docs, FloodOnlineReportingTool.HelpDocumentation |

### Databases and Storage

| Technology | Type | Repo Count | Common Use |
|-----------|------|------------|------------|
| PostgreSQL + PostGIS | Relational / Geospatial | 3 | CSIDE, FORT, GIFramework-Maps -- primary spatial data store |
| Azure Blob Storage | Object Storage | 1 | CSIDE -- media attachments and document storage |
| Azure Cosmos DB | NoSQL | 1 | BristolCityCouncil/send -- JSON document storage for SEN assessments |
| Azure Storage Queues | Message Queue | 1 | Escc.Services.Azure -- async email processing |
| Umbraco CMS (SQL Server) | CMS / Relational | 3 | East Sussex location finders -- data served via Umbraco APIs |
| MySQL | Relational | 1 | bhbudget -- budget prioritisation data capture |

### Infrastructure and Deployment

| Technology | Repo Count | Notes |
|-----------|------------|-------|
| GitHub Actions | 4 | CSIDE, FORT, GIFramework-Maps, GdsBlazorComponents -- modern CI/CD |
| Azure AD / AD B2C | 3 | CSIDE (AD B2C), GIFramework-Maps (Azure AD), BristolCityCouncil/send (AD) |
| IIS / Kestrel | 6 | On-premises or Azure VM hosting for .NET apps |
| Azure (App Service / Blob / Cosmos) | 3 | CSIDE, GIFramework-Maps, BristolCityCouncil/send |
| Travis CI | 1 | camdenmaps -- legacy; Travis CI no longer free for open source |
| Heroku | 1 | camdenmaps -- PaaS; no longer relevant for UK Gov (TCoP compliance) |
| GOV.UK Notify | 2 | CSIDE (direct integration), notifications-net-client (fork) |
| OS DataHub | 1 | CSIDE -- Ordnance Survey data subscriptions |

---

## Standards and Patterns

| Standard / Pattern | Adoption | Description | Repos |
|-------------------|----------|-------------|-------|
| GOV.UK Design System | 4 repos (20%) | GDS component library for accessible, government-standard UI -- mandated by TCoP | GdsBlazorComponents, GdsBlazorComponents-Demo, FloodOnlineReportingTool.Public, CSIDE |
| GOV.UK Notify | 2 repos (10%) | Government notification service for email/SMS/letter -- mandatory under TCoP Principle 13 | CSIDE (integrated), notifications-net-client (fork) |
| MIT Licence | 10 repos (50%) | Open-source permissive licence enabling reuse without restriction | CSIDE, FORT, GIFramework-Maps, GdsBlazorComponents, notifications-net-client, qgis-configurable-search, Lucene-Entity-Search-Tools |
| Open Government Licence 3.0 | 2 repos (10%) | Standard UK government open data licence -- applied to documentation and datasets | GIFramework-Maps (docs), DundeeCityCouncil/OpenData |
| PostgreSQL / PostGIS | 3 repos (15%) | Geospatial relational database -- OGC-compatible spatial queries for proximity search | CSIDE, FloodOnlineReportingTool.Public, GIFramework-Maps |
| Azure AD / AD B2C | 3 repos (15%) | Microsoft identity platform for authentication and authorisation | CSIDE (AD B2C), GIFramework-Maps (Azure AD), BristolCityCouncil/send (AD) |
| GOV.UK locate-api | 2 repos (10%) | Postcode-to-coordinates geocoding service (note: deprecated) | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder |
| OGC Web Services (WMS/WFS) | 2 repos (10%) | Standards-based geospatial API for map layer consumption | GIFramework-Maps, CSIDE |
| OS DataHub | 1 repo (5%) | Ordnance Survey data services subscription | CSIDE |
| Message-based inter-service contracts | 1 repo (5%) | Versioned command/event contracts for distributed service communication | FloodOnlineReportingTool.Contracts |
| Interface abstraction for external APIs | 2 repos (10%) | Replaceable interface pattern for external dependencies (geocoding, data APIs) -- enables testing and vendor independence | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder |
| GitHub Actions CI/CD | 4 repos (20%) | Modern automated build, test, and release pipelines | CSIDE, FORT, GIFramework-Maps, GdsBlazorComponents |
| WCAG Accessibility | 4 repos (20%) | Accessibility compliance via GDS Design System components | GdsBlazorComponents, CSIDE, FloodOnlineReportingTool.Public, GdsBlazorComponents-Demo |
| Entity Framework Core | 4 repos (20%) | ORM enabling database provider independence | CSIDE, FORT, GIFramework-Maps (stated provider-agnostic) |

---

## Maturity Assessment

| Repository | Activity | Documentation | Tests | CI/CD | Community | Overall |
|------------|----------|---------------|-------|-------|-----------|---------|
| [GIFramework-Maps](https://github.com/Dorset-Council-UK/GIFramework-Maps) | 4 | 5 | 4 | 4 | 3 | **4.0** |
| [CSIDE](https://github.com/Dorset-Council-UK/CSIDE) | 5 | 4 | 3 | 4 | 2 | **3.6** |
| [GdsBlazorComponents](https://github.com/Dorset-Council-UK/GdsBlazorComponents) | 5 | 4 | 3 | 4 | 2 | **3.6** |
| [FloodOnlineReportingTool.Public](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public) | 3 | 4 | 3 | 3 | 2 | **3.0** |
| [FloodOnlineReportingTool.Contracts](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts) | 5 | 3 | 2 | 2 | 2 | **2.8** |
| [notifications-net-client](https://github.com/Dorset-Council-UK/notifications-net-client) | 5 | 4 | 4 | 4 | 1 | **3.6** |
| [GdsBlazorComponents-Demo](https://github.com/Dorset-Council-UK/GdsBlazorComponents-Demo) | 4 | 3 | 2 | 2 | 1 | **2.4** |
| [qgis-configurable-search](https://github.com/Dorset-Council-UK/qgis-configurable-search) | 3 | 4 | 2 | 1 | 1 | **2.2** |
| [BristolCityCouncil/send](https://github.com/BristolCityCouncil/send) | 2 | 3 | 3 | 2 | 1 | **2.2** |
| [Escc.Libraries.BranchFinder](https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder) | 2 | 3 | 3 | 1 | 1 | **2.0** |
| [Escc.RubbishAndRecycling.SiteFinder](https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder) | 1 | 3 | 3 | 1 | 1 | **1.8** |
| [camdenmaps](https://github.com/CamdenCouncil/camdenmaps) | 1 | 2 | 3 | 2 | 1 | **1.8** |
| [open-data-scotland](https://github.com/DundeeCityCouncil/open-data-scotland) | 1 | 2 | 1 | 1 | 1 | **1.2** |
| [DundeeCityCouncil/OpenData](https://github.com/DundeeCityCouncil/OpenData) | 1 | 2 | 1 | 1 | 1 | **1.2** |
| [Lucene-Entity-Search-Tools](https://github.com/CityOfYork/Lucene-Entity-Search-Tools) | 1 | 3 | 2 | 1 | 1 | **1.6** |
| [OpenDataScripts](https://github.com/BathnesDevelopment/OpenDataScripts) | 1 | 1 | 1 | 1 | 1 | **1.0** |
| [bhbudget](https://github.com/brighton-hove-gov-uk/bhbudget) | 1 | 1 | 1 | 1 | 1 | **1.0** |

**Scale**: 1 = Poor | 2 = Below average | 3 = Adequate | 4 = Good | 5 = Excellent

**Criteria Definitions**:

- **Activity**: Frequency of commits, issue responses, PR reviews in past 12 months (5 = commits within 3 months; 4 = within 6 months; 3 = within 12 months; 2 = within 24 months; 1 = no activity > 24 months)
- **Documentation**: README quality, API docs, deployment/contribution guides (5 = comprehensive with architecture docs; 4 = good README + setup guide; 3 = adequate README; 2 = minimal; 1 = absent)
- **Tests**: Unit, integration, and end-to-end test coverage (5 = full suite + coverage reporting; 4 = comprehensive tests; 3 = unit tests present; 2 = some tests; 1 = no tests)
- **CI/CD**: Automated build, test, and deployment pipelines (5 = full CI/CD with deployment; 4 = CI with automated tests; 3 = basic CI; 2 = manual build scripts; 1 = no automation)
- **Community**: Stars, forks, contributor count, external contributions (5 = multi-org contributors; 4 = > 5 contributors; 3 = 3-5 contributors + forks; 2 = 2 contributors; 1 = single contributor/team)

**Maturity Classification Summary**:

| Classification | Threshold | Count | Repos |
|---------------|-----------|-------|-------|
| Production-Grade | 4.0+ | 1 | GIFramework-Maps (4.0) |
| Mature | 3.0-3.9 | 4 | CSIDE (3.6), GdsBlazorComponents (3.6), notifications-net-client (3.6), FORT.Public (3.0) |
| Developing | 2.0-2.9 | 5 | FORT.Contracts (2.8), GdsBlazorComponents-Demo (2.4), qgis-configurable-search (2.2), BristolCityCouncil/send (2.2), BranchFinder (2.0) |
| Experimental | < 2.0 | 7 | SiteFinder (1.8), camdenmaps (1.8), Lucene-Entity-Search-Tools (1.6), open-data-scotland (1.2), OpenData (1.2), OpenDataScripts (1.0), bhbudget (1.0) |

---

## Collaboration Opportunities

| Opportunity | Organisations | Description | Potential Value |
|-------------|--------------|-------------|-----------------|
| Adopt CSIDE's GOV.UK Notify + Azure AD B2C integration pattern | Dorset Council, CMA Digital | CSIDE already integrates GOV.UK Notify for notifications and Azure AD B2C for user authentication within a .NET 9 Blazor application using PostgreSQL/PostGIS. This is precisely the integration stack the Fuel Finder needs for retailer notifications and retailer portal authentication. Rather than building these integrations from scratch, the CMA Digital team can study CSIDE's implementation as a proven reference architecture. | Estimated 10-15 person-days saved on identity + notification integration; reduces technical risk by adopting a working government pattern |
| Extend GdsBlazorComponents for data-entry use cases | Dorset Council, CMA Digital | GdsBlazorComponents v3.0.0 already implements 29 GOV.UK Design System components in Blazor. If the Fuel Finder uses .NET/Blazor for the retailer registration portal, contributing fuel-price-specific form components (validated price-entry, station address lookup) back to this library would benefit the wider .NET government community. | Cross-government reuse of components; Dorset Council actively maintaining under MIT licence |
| Standardise postcode-to-proximity search pattern | East Sussex CC, Dorset Council, CMA Digital | Three organisations (East Sussex SiteFinder, East Sussex BranchFinder, Dorset GIFramework-Maps) have independently implemented postcode geocoding plus proximity-sorted results. A shared, maintained, open-source postcode-to-proximity library -- replacing the deprecated GOV.UK locate-api with postcodes.io or OS Names API -- would prevent further duplication. | Estimated 5-10 person-days saved per future government finder service; standardises an at-risk pattern (GOV.UK locate-api deprecated) |
| GIFramework-Maps as fuel station mapping layer | Dorset Council, CMA Digital | GIFramework-Maps v1.10.0 (21 stars, 12 forks, 202 commits, actively maintained) supports multi-source OGC layer rendering, PostGIS spatial queries, and configurable search. Publishing fuel station locations as an OGC/WFS layer and integrating with GIFramework-Maps could deliver a production-grade station-map view with significantly reduced frontend build effort. | Estimated 8-12 person-days saved on map visualisation; strengthens the GIFramework-Maps project by adding a high-profile national use case |
| Open FORT data-submission pattern as reusable template | Dorset Council, multiple councils | FORT's data-submission architecture (citizen form, validation, message contract, database, publication) mirrors the Fuel Finder's retailer price-submission flow. Publishing a generalised "regulatory data submission" template from FORT would benefit councils needing similar patterns. | Reduces build risk for CMA Digital; Dorset Council gains a higher-profile reference consumer |

---

## Gaps and Opportunities

| Gap / Opportunity | Current State | Impact | Recommended Action |
|------------------|---------------|--------|--------------------|
| No government open-source fuel price data ingestion pipeline | Zero repositories implement fuel price data collection, normalisation, or open data publication at national scale | High -- this is the project's core unique capability; no reuse possible | Build from scratch; publish under MIT/OGL to establish the government pattern for other regulated data schemes (EV charging, prescription pricing) |
| No government open-source compliance monitoring or enforcement dashboard | No central government org has open-sourced a regulatory compliance monitoring tool with alerting and case management | High -- CMA enforcement tooling is a bespoke requirement | Build from scratch; consider modular design separating monitoring logic from fuel-price specifics for future reuse |
| No CMA or DESNZ open-source presence | Neither the Competition and Markets Authority nor DESNZ has any public GitHub organisation or repositories | High -- the project's sponsoring departments have no existing open-source baseline to build upon | Establish a CMA GitHub organisation under the government.github.com umbrella; publish the Fuel Finder as the CMA's first open-source project |
| Postcode geocoding pattern at risk -- GOV.UK locate-api deprecated | Two East Sussex repos rely on the deprecated GOV.UK locate-api. No current maintained government alternative exists in open source | Medium -- affects existing services and new builds | Adopt postcodes.io (open-source, MIT, actively maintained) or OS Names API; publish wrapper library under MIT |
| No open-source national-scale geospatial station registry | GIFramework-Maps supports mapping but requires data source provision; no government repo manages a national-scale point-of-interest registry with real-time attribute updates | Medium -- station registry is a novel open data asset | Publish the fuel station registry as an OGC WFS endpoint under OGL; enables third-party apps and GIFramework-Maps integration |
| Open data publication tooling absent at central government level | Local council open data repos (Dundee, B&NES) are stale (2015 era); no recent central government open-source data catalogue tooling in govreposcrape | Medium -- DESNZ/CMA will need data.gov.uk integration | Use data.gov.uk APIs (CKAN-based) for dataset registration; no need to build custom catalogue |
| Limited testing culture across landscape | Only Dorset Council repos show comprehensive automated testing; East Sussex and other councils have minimal or no CI/CD | Medium -- low quality bar in reference code | Treat East Sussex repos as architectural pattern references only; do not copy untested code or deployment patterns |
| No government open-source rate-limiting or API key management library | API access management for open data endpoints is not addressed in any indexed repo | Low-Medium -- required for protecting the submission and open data API endpoints | Adopt established API gateway patterns (AWS API Gateway, Azure APIM) rather than custom code; evaluate CDDO API Management |
| Landscape heavily biased toward local government | 8 of 10 organisations are local councils; central government departments (HMRC, DWP, Home Office, MOJ) are absent from results despite having large open-source portfolios | Medium -- search results may not reflect the full government landscape | See Search Effectiveness Assessment below for mitigation strategies |

---

## Search Effectiveness Assessment

### Coverage Analysis

Twelve govreposcrape queries were executed across the domain, yielding 278 raw results that reduced to 62 unique repositories after deduplication. The queries covered:

| Query Tier | Queries Executed | Unique Repos Found | Assessment |
|-----------|-----------------|-------------------|------------|
| Broad domain (fuel price, open data, geospatial, competition) | 4 | 38 | Good coverage of local government GIS and open data repos; zero results for competition/regulation |
| Medium sub-domain (energy data, validation/submission, GOV.UK design, real-time processing) | 4 | 18 additional | Strong results for GOV.UK Design System usage; limited for energy data and real-time processing |
| Specific technology (PostGIS/OGC, CKAN/data.gov.uk, price comparison, cloud/CI-CD) | 4 | 6 additional | Heavy overlap with previous tiers; confirmed PostGIS dominance but no new discoveries |

### Organisation Bias

Results are **heavily dominated by local government organisations**, particularly:
- East Sussex County Council (93 repos in their org, many appearing across queries due to broad descriptions)
- Dorset Council (15 repos, highly relevant)
- Dundee City Council (8 repos, mostly stale GIS tools)
- Bath and NE Somerset (17 repos, mostly SharePoint customisations)

**Central government is notably absent** from results. Major departments with large open-source portfolios -- including alphagov (GDS), hmrc, dwp, ministryofjustice, ukhomeoffice, and defra -- did not appear in domain-specific queries. This does not mean they have no relevant code; it means the govreposcrape semantic search did not match their repository descriptions to these domain queries.

### Gaps vs Reality

| Apparent Gap | Likely Reality | Mitigation Strategy |
|-------------|---------------|---------------------|
| No alphagov repos in results | GDS repos (govuk-frontend, notifications-api-client, etc.) exist and are mandatory platform dependencies. They did not appear because the search terms were domain-specific (fuel, geospatial) rather than platform-specific. | Assess directly via https://github.com/alphagov -- already documented as mandatory platform dependencies |
| No HMRC repos in results | HMRC has 100+ public repos but none related to fuel pricing or geospatial services. Their data submission patterns (MTD APIs, Self Assessment) are relevant architecturally but would require HMRC-specific search terms. | Search govreposcrape for "HMRC data submission API" or browse https://github.com/hmrc directly for submission portal patterns |
| No DEFRA repos in results | DEFRA has environmental data repos (air quality, water quality) that share the "government environmental data publication" pattern. They did not appear because search terms focused on fuel/pricing. | Search govreposcrape for "DEFRA environmental data API" or browse https://github.com/defra for data publication patterns |
| No NHS Digital repos in results | NHS Digital has 100+ repos including geospatial service finders (NHS Service Search). Not matched because search terms did not include health-specific vocabulary. | Browse https://github.com/NHSDigital for "service search" and "organisation data service" repos as finder pattern references |
| No CMA or DESNZ repos anywhere | These organisations genuinely have no public GitHub presence. This is a real gap, not a search limitation. | Confirmed gap -- the Fuel Finder will be the first open-source project for these departments |

---

## Project Relevance Mapping

| Landscape Finding | Relevant Requirements | Implication for Project | Action |
|---|---|---|---|
| CSIDE uses GOV.UK Notify + Azure AD B2C + PostgreSQL/PostGIS + .NET 9 Blazor | BR-001 (registration), FR-001-FR-003, INT-003 (GOV.UK Notify), NFR-SEC (authentication) | Validates the .NET/Blazor + Azure AD B2C + Notify stack as a proven government combination. CSIDE is the closest architectural reference for the retailer portal. | **Adopt pattern** -- study CSIDE's Notify and AD B2C integration. `git clone https://github.com/Dorset-Council-UK/CSIDE.git` |
| GdsBlazorComponents v3.0.0 implements 29 GOV.UK Design System components in Blazor | BR-003 (citizen service), NFR-A (accessibility) | If using .NET/Blazor, this library provides immediate GOV.UK Design System compliance without building custom components. | **Adopt library** -- `dotnet add package GdsBlazorComponents` (if published to NuGet) or reference from source |
| GIFramework-Maps v1.10.0 -- production-grade OGC mapping with PostGIS | BR-003 (citizen fuel price comparison), FR-007 (map view) | Could serve as the mapping client for the citizen-facing "find stations near me" map view if fuel station data is published as OGC WFS. | **Investigate** -- evaluate whether OGC WFS publication of station data enables GIFramework-Maps integration |
| notifications-net-client fork actively maintained by Dorset Council | INT-003 (GOV.UK Notify integration) | Confirms the official .NET Notify client works in production government contexts. Dorset Council's fork may contain useful patches. | **Adopt** -- use the official alphagov/notifications-net-client; monitor Dorset fork for useful extensions |
| FORT data submission pattern (form, validation, message contract, database) | BR-002 (price submission), FR-004-FR-006 | The FORT submission flow mirrors the retailer price-submission journey. Message contract versioning is particularly relevant for the submission API schema evolution. | **Reference architecture** -- study FORT's validation and contract patterns; do not directly reuse legacy .NET Framework code |
| East Sussex finder pattern (postcode geocode, proximity sort, JSON results) | BR-003 (citizen finder), FR-007-FR-008 | Core "find nearest" UX pattern is well-established. Interface abstraction for geocoding API is a good practice to adopt. | **Reference pattern** -- study interface abstraction for geocoding; replace deprecated locate-api with postcodes.io |
| No government fuel price ingestion pipeline exists | BR-002 (price submission), FR-004-FR-006, INT-001 (submission API) | Confirms that the data ingestion pipeline must be built from scratch. This is the project's primary novel contribution. | **Build** -- design as a reusable pattern; publish under MIT/OGL |
| No government compliance monitoring dashboard exists | BR-004 (enforcement), FR-010-FR-012 | Confirms that CMA enforcement tooling is entirely bespoke. No reference architecture available. | **Build** -- design modular compliance engine separable from fuel-specific logic |
| PostgreSQL + PostGIS dominant for geospatial across landscape | DR-001 (data storage), NFR-P (performance) | PostgreSQL/PostGIS is the de facto standard for government geospatial applications. Three production repos validate this choice. | **Adopt** -- PostgreSQL/PostGIS for station registry and geospatial queries |
| Azure AD B2C emerging as government auth pattern | NFR-SEC (authentication) | CSIDE and GIFramework-Maps both use Azure identity. This is consistent with Azure UK hosting. | **Investigate** -- evaluate Azure AD B2C vs GOV.UK One Login for retailer authentication |

---

## Recommendations

### Strategic Recommendations

1. **Engage Dorset Council (Dorset-Council-UK) as primary collaboration partner**: Dorset Council is the most active, highest-maturity government organisation in the indexed landscape. Their CSIDE application (GOV.UK Notify + Azure AD B2C + PostgreSQL/PostGIS + .NET 9 Blazor) is the closest architectural reference to the Fuel Finder's retailer portal. GIFramework-Maps is the only Production-Grade geospatial tool. GdsBlazorComponents is the only .NET implementation of the GOV.UK Design System. The CMA Digital team should contact Dorset Council's GIS team (via their GitHub discussions repo or directly) to discuss shared patterns and potential contribution back to their libraries.

2. **Adopt the GOV.UK shared platform stack without deviation**: The mandatory reuse obligations under TCoP Principle 13 are clear -- GOV.UK Frontend (alphagov/govuk-frontend), GOV.UK Notify (alphagov/notifications-python-client or notifications-net-client), and GOV.UK Pay (if payment flows arise) must be used. The landscape confirms these are the only universally adopted cross-government platforms. Dorset Council's active use of the .NET Notify client validates the .NET integration path.

3. **Build the data-ingestion pipeline from scratch under MIT/OGL**: No government open-source analogue exists for national-scale regulated-market price data collection and publication. The Fuel Finder will establish a new government pattern. Publishing the ingest pipeline under MIT licence would make it available to other regulated-market schemes (EV charging data, prescription price data, broadband pricing).

4. **Adopt PostgreSQL/PostGIS as the geospatial data standard**: Three production government applications (CSIDE, FORT, GIFramework-Maps) use PostgreSQL 13+ with PostGIS. This is the de facto standard for government geospatial workloads. The project should adopt this without evaluating alternatives.

5. **Establish a CMA GitHub organisation**: Neither CMA nor DESNZ has a public GitHub presence. Creating a CMA GitHub organisation and publishing the Fuel Finder as open source would be a significant step toward meeting TCoP Principle 8 (Share, Reuse, Collaborate) and establishing CMA's digital credibility.

### For This Project Specifically

The landscape confirms that the Fuel Finder sits at the frontier of UK government open-source practice in its domain. There is no government precedent for a national, regulatory-mandated, real-time price data ingestion and publication service -- so roughly 60% of the system is genuinely novel. The remaining 40% (retailer portal UI, notification integration, geospatial finder, web mapping, authentication) has strong government reference code available, primarily from Dorset Council.

The v2.0 analysis significantly strengthens the reuse case compared to v1.0 through the discovery of CSIDE. Where v1.0 identified FORT and GIFramework-Maps as the primary reference architectures, v2.0 adds CSIDE as a more complete reference that includes GOV.UK Notify integration, Azure AD B2C authentication, OS DataHub subscription, and audit logging -- all capabilities directly required by the Fuel Finder. The project team should prioritise studying CSIDE's codebase over FORT for the retailer portal design.

The dominant technology stack across relevant government repos is C# / .NET 9 with Blazor frontend, PostgreSQL/PostGIS, and Azure services (AD B2C, Blob Storage). If the project team selects .NET as the primary stack, the reuse potential is maximised -- GdsBlazorComponents, notifications-net-client, and CSIDE's patterns become directly adoptable. If the team selects Python or Node.js, these Dorset Council resources serve as architectural references only (patterns and approaches, not code reuse). The TCoP is technology-agnostic at the language level, so either approach is compliant.

### Related ArcKit Commands

- Run `/arckit.gov-reuse` to perform a detailed reusability assessment of the top candidates (CSIDE, GIFramework-Maps, GdsBlazorComponents, notifications-net-client)
- Run `/arckit.gov-code-search` to search for specific code patterns within Dorset Council's repositories (Notify integration, AD B2C setup, PostGIS queries)
- Run `/arckit.research` for broader market and vendor research beyond government open source
- Run `/arckit.wardley` to map the domain evolution and identify commodity vs genesis components
- Run `/arckit.framework` to evaluate technology framework options (.NET vs Python vs Node.js) informed by this landscape data

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-001-GLND-v1.0 | Government Landscape Analysis (superseded) | Project research | Baseline landscape -- 12 queries, 47 unique repos, 9 organisations, 15 repos assessed | projects/001-uk-fuel-price-transparency-service/research/ARC-001-GLND-v1.0.md |
| ARC-001-GCSR-v1.0 | Government Code Search Report | Project research | 12 search queries, 24 unique repositories, top 4 high-relevance repos identified | projects/001-uk-fuel-price-transparency-service/research/ARC-001-GCSR-v1.0.md |
| ARC-001-GOVR-v1.0 | Government Reuse Assessment | Project research | 7 capability areas scored, 48 person-days estimated reuse savings | projects/001-uk-fuel-price-transparency-service/research/ARC-001-GOVR-v1.0.md |
| ARC-001-REQ-v2.0 | Requirements | Project | Open data publication requirements, citizen-facing finder, CMA enforcement tools, GOV.UK Notify integration | projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md |
| ARC-000-PRIN-v1.0 | Architecture Principles | Project | Open Data by Default, Citizen-Centred Design, TCoP compliance, OGL licensing mandate | projects/000-global/ARC-000-PRIN-v1.0.md |

---

**Generated by**: ArcKit `/arckit.gov-landscape` agent
**Generated on**: 2026-03-24
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: claude-opus-4-6[1m]
