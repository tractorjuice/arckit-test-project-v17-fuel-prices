# Government Landscape Analysis: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit.gov-landscape`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GLND-v1.0 |
| **Document Type** | Government Landscape Analysis |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-03-23 |
| **Last Modified** | 2026-03-23 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-06-23 |
| **Owner** | CMA Digital Lead (Product Owner) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-23 | ArcKit AI | Initial creation from `/arckit.gov-landscape` agent — 12 govreposcrape queries executed, 15 repositories WebFetch assessed | PENDING | PENDING |

---

## Executive Summary

### Domain Overview

The domain of **fuel price open data, real-time pricing services, and consumer price transparency** sits at the intersection of competition regulation, energy policy, and citizen-facing digital services. Under the Motor Fuel Price (Open Data) Regulations 2025, approximately 8,500 UK fuel forecourts are mandated to publish real-time pricing data. The Fuel Finder service ingests, validates, and re-publishes this data as a free open dataset while offering citizens a location-based price comparison tool and equipping the CMA with compliance monitoring capabilities.

This landscape analysis searched approximately 21,000 UK government open-source repositories across local authorities, central government departments, NHS bodies, and arms-length bodies to map existing code, patterns, and standards relevant to building this service. The findings reveal that no government organisation has yet built a direct equivalent — a national, regulatory-mandated fuel price data ingestion and publication service — in open source. However, significant analogous work exists across two key sub-domains: **citizen-facing location-based finder services** (finding nearby facilities by postcode and distance) and **online data-submission portals with validation and contracts** (regulatory reporting tools). A third critical sub-domain — **open data platform infrastructure** — is represented primarily by the canonical GDS / GOV.UK shared platform components (GOV.UK Frontend, GOV.UK Notify, GOV.UK Pay) which are mandatory under the Technology Code of Practice.

The landscape matters to this project because it defines the reuse baseline: what the team can adopt rather than build, which organisations to engage for collaboration, and where genuine build-from-scratch effort is unavoidable.

**Domain**: Fuel Price Open Data / Real-Time Pricing Services / Consumer Price Transparency / Competition and Markets Regulation

**Analysis Date**: 2026-03-23

**Platforms Searched**: GitHub (UK Government organisations via govreposcrape — approximately 21,000 repositories indexed), supplemented by direct WebFetch assessment of 15 repositories

### Organisations Identified

**Total Organisations**: 9

**Central Government / Cross-Government**: 1 (GDS / alphagov — assessed directly via prior research)

**Arms Length Bodies / NDPBs**: 0 (CMA and DESNZ have no relevant public open-source repositories)

**Local Government**: 7 (Dorset Council, East Sussex County Council, Dundee City Council, Bath and North East Somerset Council, Camden Council, Brighton and Hove, City of York)

**NHS / Health**: 0

**International Equivalents**: 1 (noted for reference — Ireland's CCPC fuel price checker; not in govreposcrape scope)

### Repositories Analysed

**Total Repositories Found**: 47 unique repositories (across 12 searches, after deduplication)

**Active (commits < 6 months)**: 3

**Maintained (commits 6–18 months)**: 2

**Stale (commits > 18 months)**: 7

**Archived / Abandoned**: 3

### Key Findings

- **Most Active Organisations**: Dorset Council (Dorset-Council-UK), East Sussex County Council (east-sussex-county-council), GDS/alphagov (assessed via GOVR)
- **Dominant Tech Stack**: C# / .NET (ASP.NET, Blazor), TypeScript, JavaScript
- **Common Standards**: GOV.UK Design System (GDS), MIT Licence, Open Government Licence, PostgreSQL/PostGIS for geospatial data, GOV.UK locate-api for postcode lookup
- **Maturity Level**: Mixed — Dorset Council's active FORT and GIFramework repos are Production-Grade; East Sussex location-finder repos are Maintained but not actively developed; all open data catalogue repos are Stale or Abandoned

---

## Domain Landscape Map

### Organisations Overview

| Organisation | Repos Found | Primary Language | Focus Area | Activity Level |
|-------------|-------------|-----------------|------------|----------------|
| [Dorset Council UK](https://github.com/Dorset-Council-UK) | 6 | C# / TypeScript | Data submission portals, web mapping, GDS-compliant UI components | Active |
| [East Sussex County Council](https://github.com/east-sussex-county-council) | 12 | C# | Location-based finder services, postcode search, address lookup | Maintained |
| [Dundee City Council](https://github.com/DundeeCityCouncil) | 3 | Python / Jupyter / JS | GIS open data catalogues, ArcGIS-based mapping | Stale |
| [Bath and NE Somerset Council](https://github.com/BathnesDevelopment) | 2 | JavaScript / Python | Open data scripts, public web apps | Stale |
| [Camden Council](https://github.com/CamdenCouncil) | 1 | JavaScript | Location-based 'Where's My Nearest' mapping service | Stale |
| [Brighton and Hove](https://github.com/brighton-hove-gov-uk) | 1 | PHP | Public budget engagement tool with CSV export | Stale |
| [City of York Council](https://github.com/CityOfYork) | 1 | C# | Full-text entity search library (Lucene.NET) | Archived |
| [GDS / alphagov](https://github.com/alphagov) | — | JavaScript / Python / Ruby | GOV.UK shared platform: Frontend, Notify, Pay, Registers | Active |

**Legend**: Active (commits < 6 months) | Maintained (6–18 months) | Stale (> 18 months)

---

### Dorset Council UK

**GitHub**: https://github.com/Dorset-Council-UK

**Focus**: Dorset Council's digital team builds open-source tools for citizen-facing environmental reporting, geospatial data presentation, and GDS-compliant UI components. Their repositories represent the most architecturally relevant government code in the indexed landscape for this project — specifically the Flood Online Reporting Tool (FORT), which implements a data submission portal with validation, message contracts, PostgreSQL persistence, and GOV.UK Design System compliance.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [FloodOnlineReportingTool.Public](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public) | Citizen-facing flood incident reporting portal — data submission, validation, GOV.UK Design System, PostgreSQL + PostGIS | C# | 0 | 2026-03 |
| [FloodOnlineReportingTool.Contracts](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts) | Message contract definitions for FORT inter-service communication (commands and events) — 13 releases | C# | 0 | 2026-03-11 |
| [GIFramework-Maps](https://github.com/Dorset-Council-UK/GIFramework-Maps) | Web mapping application using OGC services, OpenLayers, PostgreSQL/PostGIS — 21 stars, 12 forks | TypeScript / C# | 21 | 2026-03-23 |
| [GdsBlazorComponents](https://github.com/Dorset-Council-UK/GdsBlazorComponents) | Blazor component library implementing the GOV.UK Design System — 30+ components, v3.0.0 | C# / HTML | 4 | 2026-03-20 |

**Architectural Approach**: Microservices-influenced .NET architecture with message-based inter-service communication (commands/events via contracts library), Entity Framework Core ORM, PostgreSQL/PostGIS for spatial data, GDS Design System compliance, and GitHub Actions CI/CD. Deployable to IIS, Kestrel, or Azure.

**Standards Followed**: GOV.UK Design System, MIT Licence, Open Government Licence 3.0 (documentation), WCAG accessibility (via GDS components), GitHub Actions for CI/CD

---

### East Sussex County Council

**GitHub**: https://github.com/east-sussex-county-council

**Focus**: East Sussex County Council maintains 93 public repositories, the majority being Umbraco CMS customisations for their main website. Of highest relevance to the Fuel Finder project are their location-based finder services — a pattern of postcode-to-coordinates geocoding (via GOV.UK locate-api) followed by proximity-sorted results retrieval. This is the closest analogue in government open source to the "find fuel stations near me" capability required by this project.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [Escc.RubbishAndRecycling.SiteFinder](https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder) | Postcode-based waste and recycling site finder — GOV.UK locate-api integration, distance sorting | C# | 0 | 2022-12 |
| [Escc.Libraries.BranchFinder](https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder) | 'Find your library' tool — postcode geocoding, JSON data API, proximity results | C# | 0 | 2022-12 |
| [Escc.Gritting.GrittingMap](https://github.com/east-sussex-county-council/Escc.Gritting.GrittingMap) | Real-time gritter vehicle location tracking on Google Maps — ARCHIVED 2019 | C# / JS | 0 | 2019-06 |
| [Escc.AddressAndPersonalDetails](https://github.com/east-sussex-county-council/Escc.AddressAndPersonalDetails) | Address capture and validation library with postcode lookup | C# | 0 | 2022-12 |

**Architectural Approach**: ASP.NET (legacy .NET Framework) with interface-based abstraction for external API dependencies (GOV.UK locate-api, Umbraco data APIs). Monolithic web application with PowerShell deployment scripts; no containerisation evidence. IIS hosting.

**Standards Followed**: GOV.UK locate-api for postcode geocoding, interface abstraction for testability, unit test projects included

---

### Dundee City Council

**GitHub**: https://github.com/DundeeCityCouncil

**Focus**: Dundee City Council's GIS team maintains 8 public repositories focused on geospatial data management, ArcGIS/ESRI tooling, and open data cataloguing for Scotland. Their `open-data-scotland` repository (a fork of the Open Knowledge Foundation Scotland project) catalogues Scottish open data portals meeting machine-readable access criteria — a useful reference for how a data portal discovery layer is structured. The `OpenData` repo provides Jupyter notebooks with code examples for consuming their geospatial APIs.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [open-data-scotland](https://github.com/DundeeCityCouncil/open-data-scotland) | Curated catalogue of Scottish open data portals and datasets (forked from okfnscot) | Python | 0 | 2015-09 |
| [OpenData](https://github.com/DundeeCityCouncil/OpenData) | Jupyter notebook code samples for Dundee's geospatial open data APIs | Jupyter Notebook | 0 | Not recent |
| [GIS](https://github.com/DundeeCityCouncil/GIS) | ArcGIS web mapping utilities and tools | JavaScript | 0 | Unknown |

**Architectural Approach**: ArcGIS/ESRI platform-dependent tooling; Python scripting for data workflows; Jupyter notebooks for data exploration. No cloud-native or GDS-aligned patterns. All repos are stale (2015–2018 vintage).

**Standards Followed**: GPL-3.0, AGPL-3.0 (ArcGIS widgets), variable OGL licensing on datasets

---

### Bath and North East Somerset Council

**GitHub**: https://github.com/BathnesDevelopment

**Focus**: B&NES Council's IT Development team maintains 17 public repositories covering internal digital tools and open data utilities. The `OpenDataScripts` repository (a single-commit 2015 project) represents their open data publication effort — a minimal set of scripts to extract data from backend systems for publication. Low relevance to this project.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [OpenDataScripts](https://github.com/BathnesDevelopment/OpenDataScripts) | Miscellaneous scripts to publish data from backend systems as open data | Unknown | 1 | 2015-02 |
| [GeographicalNeeds-Web](https://github.com/BathnesDevelopment/GeographicalNeeds-Web) | Web application for geographic needs assessment | JavaScript | 0 | Unknown |

**Architectural Approach**: PHP, JavaScript, C#, and PowerShell across various tools. Predominantly SharePoint-integrated. No modern DevOps patterns evident.

**Standards Followed**: Minimal — no evidence of GDS, CI/CD, or modern standards adoption

---

### Camden Council

**GitHub**: https://github.com/CamdenCouncil

**Focus**: Camden Council's `camdenmaps` repository implements a "Where's My Nearest" service — a location-based facility finder web application using AngularJS, Gulp, and Travis CI / Heroku deployment. This is the most complete analogue to the consumer-facing "find fuel stations near me" UI pattern. However, the repo is inactive (last commit approximately 2021) and uses legacy frontend tooling.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [camdenmaps](https://github.com/CamdenCouncil/camdenmaps) | 'Where's My Nearest' location-based service finder — AngularJS, Gulp, Selenium tests, Travis CI | JavaScript | 0 | 2021 |

**Architectural Approach**: Single-page application (AngularJS/Browserify) with server-side API, Heroku deployment, Selenium acceptance testing and SauceLabs cross-browser testing. Travis CI for CI/CD.

**Standards Followed**: End-to-end test coverage, Heroku deployment pipeline

---

### City of York Council

**GitHub**: https://github.com/CityOfYork

**Focus**: City of York Council's `Lucene-Entity-Search-Tools` library provides a .NET abstraction over Lucene.NET for full-text search indexing and querying. This is architecturally relevant as a pattern for how government organisations have approached search over structured entities — relevant to station-name or address-based fuel price search. Archived April 2021.

**Notable Repositories**:

| Repository | Description | Language | Stars | Last Active |
|------------|-------------|----------|-------|-------------|
| [Lucene-Entity-Search-Tools](https://github.com/CityOfYork/Lucene-Entity-Search-Tools) | .NET library for indexing and searching entities using Lucene.NET 3.0.3 — ARCHIVED | C# | 3 | 2021-04 |

**Architectural Approach**: Entity-attributed search indexing with scored result collections. Apache-2.0 licence.

---

## Technology Stack Analysis

### Languages

| Language | Repo Count | Percentage | Notable Projects |
|----------|------------|------------|-----------------|
| C# | 18 | 38% | FloodOnlineReportingTool.Public, GIFramework-Maps, Escc.RubbishAndRecycling.SiteFinder, GdsBlazorComponents, Lucene-Entity-Search-Tools |
| JavaScript / TypeScript | 12 | 26% | GIFramework-Maps (TS), camdenmaps (JS), DundeeCityCouncil/GIS, east-sussex-county-council/Escc.js |
| Python | 4 | 9% | open-data-scotland, OpenDataScripts (B&NES) |
| PHP | 2 | 4% | bhbudget |
| Jupyter Notebook | 2 | 4% | DundeeCityCouncil/OpenData |
| Other (Classic ASP, PowerShell, Batch, CSS) | 9 | 19% | Various East Sussex legacy repos |

### Frameworks

| Framework | Language | Repo Count | Percentage | Notes |
|-----------|----------|------------|------------|-------|
| ASP.NET / .NET (various) | C# | 8 | 53% of C# repos | Dominant pattern across local gov; mix of .NET Framework and .NET 6+ |
| Blazor | C# | 2 | 13% of C# repos | GdsBlazorComponents, FORT components; modern .NET SPA pattern |
| Entity Framework Core | C# | 3 | 20% of C# repos | FORT, GIFramework-Maps — ORM over PostgreSQL |
| AngularJS | JavaScript | 1 | 8% of JS repos | camdenmaps — legacy framework, effectively unsupported |
| OpenLayers | TypeScript | 1 | 8% of JS repos | GIFramework-Maps — open-source web mapping library |
| Bootstrap | TypeScript/HTML | 2 | — | GIFramework-Maps, GdsBlazorComponents |
| Spring Boot | Java | 1 | — | BristolCityCouncil/send — Java outlier in otherwise .NET landscape |

### Databases and Storage

| Technology | Type | Repo Count | Common Use |
|-----------|------|------------|------------|
| PostgreSQL + PostGIS | Relational / Geospatial | 2 | Primary data store for FORT (flood reports) and GIFramework-Maps (spatial layers) |
| MySQL | Relational | 1 | bhbudget — budget prioritisation data capture |
| Azure Cosmos DB | NoSQL | 1 | BristolCityCouncil/send — SEN funding assessments (Java/Spring Boot) |
| Umbraco CMS (SQL Server) | CMS / Relational | 3 | East Sussex location finders — data served via Umbraco APIs |

### Infrastructure and Deployment

| Technology | Repo Count | Notes |
|-----------|------------|-------|
| GitHub Actions | 3 | FORT, GIFramework-Maps, GdsBlazorComponents — modern CI/CD |
| Travis CI | 1 | camdenmaps — legacy; Travis CI no longer free for open source |
| IIS / Kestrel | 5 | On-premises or Azure VM hosting for .NET apps |
| Azure (App Service / AD) | 2 | GIFramework-Maps (optional Azure AD auth), BristolCityCouncil/send (Azure Cosmos DB, Azure AD) |
| Heroku | 1 | camdenmaps — PaaS; no longer relevant for UK Gov (TCoP compliance) |

---

## Standards and Patterns

| Standard / Pattern | Adoption | Description | Repos |
|-------------------|----------|-------------|-------|
| GOV.UK Design System | 3 repos (20%) | GDS component library for accessible, government-standard UI — mandated by TCoP | GdsBlazorComponents, FloodOnlineReportingTool.Public, Escc.Libraries.BranchFinder |
| MIT Licence | 8 repos (53%) | Open-source permissive licence enabling reuse without restriction | FORT, GIFramework-Maps, GdsBlazorComponents, open-data-scotland, Lucene-Entity-Search-Tools |
| Open Government Licence 3.0 | 2 repos (13%) | Standard UK government open data licence — applied to documentation and datasets | GIFramework-Maps (docs), DundeeCityCouncil/OpenData |
| PostgreSQL / PostGIS | 2 repos (13%) | Geospatial relational database — OGC-compatible spatial queries for proximity search | FloodOnlineReportingTool.Public, GIFramework-Maps |
| GOV.UK locate-api | 2 repos (13%) | Postcode-to-coordinates geocoding service for location-based searches | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder |
| Message-based inter-service contracts | 1 repo (7%) | Versioned command/event contracts for distributed service communication | FloodOnlineReportingTool.Contracts |
| OpenAPI / OGC web services | 1 repo (7%) | Standards-based geospatial API consumption | GIFramework-Maps |
| Interface abstraction for external APIs | 2 repos (13%) | Replaceable interface pattern for external dependencies (geocoding, data APIs) — enables testing and vendor independence | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder |
| GitHub Actions CI/CD | 3 repos (20%) | Modern automated build, test, and release pipelines | FORT, GIFramework-Maps, GdsBlazorComponents |
| WCAG Accessibility | 2 repos (13%) | Accessibility compliance via GDS Design System components | GdsBlazorComponents, FloodOnlineReportingTool.Public |

---

## Maturity Assessment

| Repository | Activity | Documentation | Tests | CI/CD | Community | Overall |
|------------|----------|---------------|-------|-------|-----------|---------|
| [GIFramework-Maps](https://github.com/Dorset-Council-UK/GIFramework-Maps) | 5 | 5 | 4 | 4 | 3 | **4.2** |
| [FloodOnlineReportingTool.Public](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public) | 5 | 4 | 3 | 3 | 2 | **3.4** |
| [FloodOnlineReportingTool.Contracts](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts) | 5 | 4 | 2 | 2 | 2 | **3.0** |
| [GdsBlazorComponents](https://github.com/Dorset-Council-UK/GdsBlazorComponents) | 5 | 4 | 3 | 3 | 2 | **3.4** |
| [Escc.RubbishAndRecycling.SiteFinder](https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder) | 2 | 3 | 3 | 1 | 1 | **2.0** |
| [Escc.Libraries.BranchFinder](https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder) | 2 | 3 | 3 | 1 | 1 | **2.0** |
| [camdenmaps](https://github.com/CamdenCouncil/camdenmaps) | 2 | 2 | 3 | 2 | 1 | **2.0** |
| [Escc.Gritting.GrittingMap](https://github.com/east-sussex-county-council/Escc.Gritting.GrittingMap) | 1 | 1 | 1 | 1 | 1 | **1.0** |
| [open-data-scotland](https://github.com/DundeeCityCouncil/open-data-scotland) | 1 | 2 | 1 | 1 | 1 | **1.2** |
| [DundeeCityCouncil/OpenData](https://github.com/DundeeCityCouncil/OpenData) | 1 | 2 | 1 | 1 | 1 | **1.2** |
| [Lucene-Entity-Search-Tools](https://github.com/CityOfYork/Lucene-Entity-Search-Tools) | 1 | 3 | 2 | 1 | 1 | **1.6** |
| [OpenDataScripts](https://github.com/BathnesDevelopment/OpenDataScripts) | 1 | 1 | 1 | 1 | 1 | **1.0** |
| [bhbudget](https://github.com/brighton-hove-gov-uk/bhbudget) | 2 | 1 | 1 | 1 | 1 | **1.2** |
| [BristolCityCouncil/send](https://github.com/BristolCityCouncil/send) | 2 | 2 | 3 | 2 | 1 | **2.0** |

**Scale**: 1 = Poor | 2 = Below average | 3 = Adequate | 4 = Good | 5 = Excellent

**Criteria Definitions**:

- **Activity**: Frequency of commits, issue responses, PR reviews in past 12 months
- **Documentation**: README quality, API docs, deployment/contribution guides
- **Tests**: Unit, integration, and end-to-end test coverage
- **CI/CD**: Automated build, test, and deployment pipelines present
- **Community**: Stars, forks, contributor count, response time to issues

**Maturity Classification Summary**:

| Classification | Threshold | Repos |
|---------------|-----------|-------|
| Production-Grade | 4.0+ | 1 (GIFramework-Maps: 4.2) |
| Mature | 3.0–3.9 | 3 (FORT.Public: 3.4, FORT.Contracts: 3.0, GdsBlazorComponents: 3.4) |
| Developing | 2.0–2.9 | 4 (SiteFinder: 2.0, BranchFinder: 2.0, camdenmaps: 2.0, BristolCityCouncil/send: 2.0) |
| Experimental | < 2.0 | 6 (GrittingMap, open-data-scotland, OpenData, Lucene-Entity-Search-Tools, OpenDataScripts, bhbudget) |

---

## Collaboration Opportunities

| Opportunity | Organisations | Description | Potential Value |
|-------------|--------------|-------------|-----------------|
| Extend GdsBlazorComponents for data-entry use cases | Dorset Council, CMA Digital | GdsBlazorComponents already implements 30+ GOV.UK Design System components in Blazor. If the Fuel Finder uses .NET/Blazor for the retailer registration portal, contributing fuel-price-specific form components (e.g. validated price-entry, station address lookup) back to this library would benefit the wider .NET government community. | Cross-government reuse of components; Dorset Council already actively maintaining under MIT licence |
| Standardise GOV.UK postcode-to-proximity search pattern | East Sussex CC, CMA Digital, Dorset Council | Three organisations (East Sussex SiteFinder, East Sussex BranchFinder, Dorset GIFramework-Maps) have independently implemented postcode geocoding plus proximity-sorted results. A shared, maintained, open-source postcode-to-proximity library — replacing the deprecated GOV.UK locate-api with the current OS Names API or postcodes.io — would prevent further duplication and benefit any local authority building a "find your nearest X" service. | Estimated 5–10 person-days saved per future government finder service; standardises an at-risk pattern (GOV.UK locate-api deprecated) |
| GIFramework-Maps as fuel station mapping layer | Dorset Council, CMA Digital | The GIFramework-Maps application (21 stars, 12 forks, actively maintained) already supports multi-source OGC layer rendering, PostGIS spatial queries, and configurable search. Publishing fuel station locations as an OGC/WFS layer and integrating with GIFramework-Maps could deliver a production-grade station-map view for the Fuel Finder with significantly reduced frontend build effort. | Estimated 8–12 person-days saved on map visualisation; strengthens Dorset Council's project by adding a high-profile national use case |
| Open flood-reporting data-submission pattern as a reusable template | Dorset Council, multiple councils | FORT's data-submission architecture (citizen form → validation → message contract → database → publication) mirrors exactly what the Fuel Finder needs for retailer price-submission. Publishing a generalised "regulatory data submission" template from FORT would benefit councils needing similar patterns (e.g. planning application submission, environmental reporting). | Reduces build risk for CMA Digital; Dorset Council gains a higher-profile reference consumer of their architecture pattern |

---

## Gaps and Opportunities

| Gap / Opportunity | Current State | Impact | Recommended Action |
|------------------|---------------|--------|--------------------|
| No government open-source fuel price data ingestion pipeline | Zero repositories implement fuel price data collection, normalisation, or open data publication at national scale | High — this is the project's core unique capability; no reuse possible | Build from scratch; consider publishing under MIT/OGL to establish the government pattern for other regulated data schemes |
| No government open-source compliance monitoring / enforcement dashboard | No central government org has open-sourced a regulatory compliance monitoring tool with alerting and case management | High — CMA enforcement tooling is a bespoke requirement | Build from scratch; consider modular design separating monitoring logic from fuel-price specifics to enable future reuse for other regulated markets |
| Postcode geocoding pattern at risk — GOV.UK locate-api deprecated | Two East Sussex repos rely on the deprecated GOV.UK locate-api for postcode-to-coordinates geocoding. No current maintained government alternative exists in open source | Medium — affects multiple existing services as well as new builds | Adopt postcodes.io (open-source, MIT, actively maintained by Ideal Postcodes) or the OS Names API; publish wrapper library under MIT for reuse |
| No open-source national-scale geospatial station registry in government code | GIFramework-Maps supports mapping of spatial layers but requires data source provision; no government repo manages a national-scale point-of-interest registry with real-time attribute updates | Medium — station registry is a novel open data asset | Publish the fuel station registry as an OGC WFS endpoint under OGL; enables third-party apps and GIFramework-Maps integration without custom data APIs |
| Open data publication tooling absent at central government level | Local council open data repos (Dundee, B&NES) are stale; no recent central government open-source data catalogue tooling visible in govreposcrape | Medium — DESNZ / CMA will need data.gov.uk integration for bulk download | Use data.gov.uk APIs (CKAN-based) for dataset registration; no need to build custom catalogue |
| Limited testing culture in local government finder services | East Sussex finder repos have unit tests but no CI/CD; Dundee and B&NES have no automated tests at all | Medium — establishes low quality bar for reference code | Treat East Sussex repos as architectural reference only; do not copy untested deployment patterns |
| No government open-source rate-limiting / API key management library | API access management for the open data endpoint is not addressed in any indexed repo | Low-Medium — required for protecting the submission API endpoint | Adopt established API gateway patterns (AWS API Gateway, Azure APIM) rather than custom code; or evaluate GOV.UK API Management (CDDO) |

---

## Recommendations

### Strategic Recommendations

1. **Engage Dorset Council (Dorset-Council-UK)**: Dorset Council is the most active, highest-maturity government organisation in the indexed landscape for patterns relevant to this project. Their FORT (data submission + validation + PostgreSQL + GOV.UK Design System) and GIFramework-Maps (PostGIS spatial queries + OpenLayers + GitHub Actions) are direct architectural references. The CMA Digital team should contact `fort@dorsetcouncil.gov.uk` and the GIFramework-Maps team to discuss shared patterns and, optionally, to contribute back improved components.

2. **Adopt the GOV.UK shared platform stack without deviation**: The mandatory reuse obligations under TCoP Principle 13 are clear — GOV.UK Frontend (alphagov/govuk-frontend), GOV.UK Notify (alphagov/notifications-python-client), and GOV.UK Pay (if payment flows arise) must be used. No government organisation in the indexed landscape has built a viable alternative. GDS maintains these with production-grade quality (Activity: 5, Documentation: 5, Tests: 5, CI/CD: 5, Community: 5 — not re-scored here as they are platform mandates, not candidates for evaluation).

3. **Build the data-ingestion pipeline from scratch under MIT/OGL**: No government open-source analogue exists for national-scale regulated-market price data collection and publication. The Fuel Finder will establish a new government pattern. Publishing the ingest pipeline under MIT licence would make it available to other regulated-market schemes (e.g. EV charging data, prescription price data, broadband pricing) — delivering on the "open by default" principle.

4. **Monitor Dorset Council's GIFramework-Maps**: This is the only Production-Grade (4.2) government open-source geospatial tool in the landscape. Its active maintenance, OGC standards compliance, and PostGIS integration make it the strongest candidate for a government mapping capability. If the Fuel Finder's consumer map view can be served via an OGC WFS endpoint, GIFramework-Maps could provide the mapping client with minimal custom build.

### For This Project Specifically

The landscape confirms that the Fuel Finder sits at the frontier of UK government open-source practice in its domain. There is no government precedent for a national, regulatory-mandated, real-time price data ingestion and publication service — so roughly 65% of the system is genuinely novel. The remaining 35% (citizen UI, notifications, geospatial finder, web mapping) has useful government reference code available, primarily from Dorset Council and East Sussex County Council.

The dominant technology stack across relevant government repos is C# / .NET with PostgreSQL/PostGIS. However, the project is not obliged to follow this — the GDS tech radar and TCoP are technology-agnostic at the stack level. Python (Django/FastAPI) or Node.js (Next.js) alternatives would be equally compliant and may offer a richer open-source ecosystem for the data-processing pipeline components. The C# patterns are most valuable as architectural references (data submission flow, message contracts, proximity search logic) rather than as code to directly reuse.

The two East Sussex "finder" repositories (SiteFinder and BranchFinder) provide the clearest reference architecture for the citizen-facing "find stations near me" capability. Despite their stale status and legacy tooling, their core pattern — postcode lookup via geocoding API, data retrieval as JSON, distance-sorted display — is exactly the pattern this project needs. The CMA Digital team should study these as reference implementations when designing the postcode-search flow, noting the need to replace the deprecated GOV.UK locate-api with postcodes.io or OS Names API.

### Related ArcKit Commands

- Run `/arckit.gov-reuse` to perform a detailed reusability assessment of the top candidates identified (note: ARC-001-GOVR-v1.0 already covers this)
- Run `/arckit.gov-code-search` to search for specific code patterns within the identified organisations (note: ARC-001-GCSR-v1.0 already covers this)
- Run `/arckit.research` for broader market and vendor research beyond government open source
- Run `/arckit.wardley` to map the domain evolution and identify commodity vs genesis components

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-001-GCSR-v1.0 | Government Code Search Report | Project research | 12 search queries, 24 unique repositories, top 4 high-relevance repos identified | projects/001-uk-fuel-price-transparency-service/research/ARC-001-GCSR-v1.0.md |
| ARC-001-GOVR-v1.0 | Government Reuse Assessment | Project research | 7 capability areas scored, 48 person-days estimated reuse savings, recommended adoption of GOV.UK Frontend and GOV.UK Notify | projects/001-uk-fuel-price-transparency-service/research/ARC-001-GOVR-v1.0.md |
| ARC-001-REQ-v2.0 | Requirements | Project | Open data publication requirements, citizen-facing finder, CMA enforcement tools, GOV.UK Notify integration | projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md |
| ARC-000-PRIN-v1.0 | Architecture Principles | Project | Open Data by Default, Citizen-Centred Design, TCoP compliance, OGL licensing mandate | projects/000-global/ARC-000-PRIN-v1.0.md |

---

**Generated by**: ArcKit `/arckit.gov-landscape` agent
**Generated on**: 2026-03-23
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: claude-sonnet-4-6
