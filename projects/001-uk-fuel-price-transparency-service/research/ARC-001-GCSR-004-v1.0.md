# Government Code Search Report: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit.gov-code-search`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GCSR-004-v1.0 |
| **Document Type** | Government Code Search Report |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-03-24 |
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
| 1.0 | 2026-03-24 | ArcKit AI | Initial creation from `/arckit.gov-code-search` agent -- real-time data validation pipelines query across UK government repositories | PENDING | PENDING |

---

## Executive Summary

### Search Query

**Original Query**: `real-time data validation pipelines`

**Query Variations Used**:

- `data validation processing pipeline government open data quality checks`
- `streaming data ingestion validation schema enforcement real-time`
- `ETL data pipeline validation rules API submission processing`
- `data quality checks automated testing JSON schema validation service`
- `alphagov data pipeline publishing platform API ingestion`
- `HMRC data submission validation error handling compliance reporting`
- `open data publishing platform CSV JSON validation transformation data.gov.uk`
- `flood monitoring sensor data collection real-time alerting environment agency`
- `form data validation GOV.UK frontend error messages input checking`
- `NHS digital data pipeline patient record validation HL7 FHIR processing`

**Platforms Searched**: govreposcrape (UK Government GitHub repository index covering approximately 21,000 repositories), with WebFetch verification against GitHub for shortlisted repositories.

### Results Found

**Total Repository Hits (Pre-Deduplication)**: 195 results across 11 query variations

**Unique Repositories After Deduplication**: 62

**High Relevance Results**: 0

**Medium Relevance Results**: 7

**Low Relevance / Excluded**: 55

### Top Results

| # | Repository | Organisation | Relevance | Language | Last Active |
|---|------------|--------------|-----------|----------|-------------|
| 1 | FloodOnlineReportingTool.Contracts | Dorset-Council-UK | Medium | C# | 2026-03-11 |
| 2 | FloodOnlineReportingTool.Public | Dorset-Council-UK | Medium | C# | 2025-01-20 |
| 3 | GdsBlazorComponents | Dorset-Council-UK | Medium | C# / HTML | 2026-03-20 |
| 4 | open-data-scotland | DundeeCityCouncil | Medium | Python | Unknown |
| 5 | OpenData | DundeeCityCouncil | Medium | Jupyter Notebook | Unknown |

**Critical Finding**: The govreposcrape index returned **zero high-relevance results** for real-time data validation pipelines. No repositories directly implement the data validation pipeline patterns needed for the Fuel Price Transparency Service. The index is heavily weighted towards local council repositories and does not include central government organisations (alphagov, NHSDigital, hmrc, dwp, moj, dfe, defra) where data pipeline implementations are most likely to reside.

---

## Search Results

### High Relevance Results

No repositories returned from govreposcrape directly address real-time data validation pipelines. This is a significant gap attributable to index coverage limitations rather than an absence of such implementations across UK government. See the **Search Effectiveness Assessment** section for alternative search strategies.

---

### Medium Relevance Results

#### Dorset-Council-UK/FloodOnlineReportingTool.Contracts

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts |
| **Description** | Message contracts for the Flood Online Reporting Tool (FORT) enabling inter-service communication in a distributed system architecture |
| **Language** | C# (100%) |
| **License** | MIT |
| **Last Activity** | 2026-03-11 |
| **Stars** | 0 |

**Why Relevant**: Demonstrates a message contract pattern for distributed service communication. While not a data validation pipeline itself, the contract-first approach to defining message structures is a foundational pattern for building validation pipelines -- incoming data can be validated against shared contract definitions.

**Key Patterns**:

- Contract-first service design with shared message definitions
- Distributed architecture with command and event messaging
- NuGet package distribution for contract sharing across services

---

#### Dorset-Council-UK/FloodOnlineReportingTool.Public

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public |
| **Description** | .NET web application enabling public flood reporting to local authorities |
| **Language** | C# (81.1%) |
| **License** | MIT |
| **Last Activity** | 2025-01-20 |
| **Stars** | 0 |

**Why Relevant**: Implements a public data submission workflow (citizens reporting floods) with form validation, data processing, and storage. The pattern of accepting user-submitted data, validating it, and processing it is analogous to the fuel price submission pipeline. Uses Entity Framework Core with PostgreSQL/PostGIS, demonstrating geospatial data handling.

**Key Patterns**:

- Public data submission with server-side validation
- GDS Design System compliance for form interfaces
- Entity Framework Core with PostgreSQL and PostGIS for geospatial data
- Security-conscious approach (private vulnerability reporting)

---

#### Dorset-Council-UK/GdsBlazorComponents

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/GdsBlazorComponents |
| **Description** | Blazor components styled according to the GOV.UK Design System |
| **Language** | HTML (45.1%), C# (41.1%), TypeScript (8.1%) |
| **License** | MIT |
| **Last Activity** | 2026-03-20 |
| **Stars** | 4 |

**Why Relevant**: Provides reusable GOV.UK Design System form components for Blazor applications, including input validation patterns. Relevant to the front-end validation layer of the fuel price submission forms (manual entry by retailers like Persona "Raj"). Over 30 components with built-in validation messaging.

**Key Patterns**:

- GOV.UK Design System component library for .NET Blazor
- Client-side and server-side form validation patterns
- NuGet distribution for component reuse
- Accessibility-compliant form error messaging

---

#### DundeeCityCouncil/open-data-scotland

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dundee City Council |
| **Repository URL** | https://github.com/DundeeCityCouncil/open-data-scotland |
| **Description** | Curated list of open data resources and portals operating in Scotland |
| **Language** | Python (92.3%) |
| **License** | Available (LICENSE.md) |
| **Last Activity** | Unknown (45 total commits) |
| **Stars** | 0 |

**Why Relevant**: Catalogues open data portals with criteria for machine-readable formats (CSV, RSS, XML), documented APIs, and SPARQL endpoints. Demonstrates data quality criteria assessment for open data sources -- relevant to defining validation standards for fuel price open data publication.

**Key Patterns**:

- Open data catalogue with quality criteria (machine-readable, API access, SPARQL)
- CSV-based data management for catalogue entries
- Data source quality assessment methodology

---

#### DundeeCityCouncil/OpenData

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dundee City Council |
| **Repository URL** | https://github.com/DundeeCityCouncil/OpenData |
| **Description** | Open data repository with code samples for using council data services |
| **Language** | Jupyter Notebook (100%) |
| **License** | Not specified |
| **Last Activity** | Unknown (14 total commits) |
| **Stars** | 0 |

**Why Relevant**: Provides code samples for consuming open data APIs, including location-based datasets. Demonstrates patterns for data access and analysis that third-party consumers of the Fuel Finder API might follow. Includes examples across multiple domains (recycling, streets, analysis).

**Key Patterns**:

- Jupyter Notebook data analysis examples for open data consumers
- Location-based dataset publication and consumption
- Multi-domain data organisation (recycling, streets, analysis)

---

#### Dorset-Council-UK/GIFramework-Maps

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/GIFramework-Maps |
| **Description** | .NET-based web mapping application built with OpenLayers and Bootstrap |
| **Language** | TypeScript (42.7%), C# (37.6%), HTML (18.1%) |
| **License** | MIT |
| **Last Activity** | 2025-12-22 |
| **Stars** | 21 |

**Why Relevant**: The most actively maintained and popular repository found. Implements geospatial data ingestion, querying, and display from multiple OGC web services. The pattern of ingesting spatial data from multiple sources, validating it, and presenting it to users mirrors the Fuel Finder's need to ingest fuel prices (with location data) and display them on a map.

**Key Patterns**:

- Multi-source geospatial data ingestion from OGC web services
- PostgreSQL with PostGIS for spatial data storage and querying
- .NET with Entity Framework Core data access layer
- Azure AD authentication integration
- OpenLayers for map rendering with custom query templates

---

#### east-sussex-county-council/Escc.FormControls.WebForms

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council |
| **Repository URL** | https://github.com/east-sussex-county-council/Escc.FormControls.WebForms |
| **Description** | Generic form controls and validators for use on WebForms pages |
| **Language** | C# (100%) |
| **License** | Available (LICENSE.md) |
| **Last Activity** | 2022-12-06 |
| **Stars** | 0 |

**Why Relevant**: Implements reusable server-side validation components including address lookup (postcode validation) and reCAPTCHA integration. Demonstrates the pattern of centralised validation controls that can be applied consistently across multiple forms -- relevant to standardising validation for fuel price submission forms.

**Key Patterns**:

- Centralised validation control library
- Postcode-based address lookup integration
- Server-side reCAPTCHA validation
- Web.config-based control mapping for consistent deployment

---

## Code Patterns Identified

| Pattern | Repositories Using It | Description |
|---------|----------------------|-------------|
| Contract-First Messaging | FloodOnlineReportingTool.Contracts | Shared message contracts define data structures for inter-service communication, enabling validation against known schemas in distributed systems |
| GDS Design System Form Validation | GdsBlazorComponents, FloodOnlineReportingTool.Public | GOV.UK Design System patterns for accessible form validation with standardised error messaging and input checking |
| Entity Framework Core + PostgreSQL | FloodOnlineReportingTool.Public, GIFramework-Maps | .NET data access pattern using EF Core with PostgreSQL (and PostGIS for spatial data), providing model validation at the ORM layer |
| Open Data Quality Criteria | open-data-scotland, OpenData | Assessment frameworks for data quality (machine-readability, API availability, format standards) applied to open data catalogues |
| Geospatial Data Ingestion | GIFramework-Maps, FloodOnlineReportingTool.Public | Ingesting, validating, and storing location-based data using PostGIS spatial extensions |
| Centralised Validation Controls | Escc.FormControls.WebForms, GdsBlazorComponents | Reusable validation component libraries distributed via package managers (NuGet) for consistent application across services |

**Observations**: The repositories found demonstrate front-end form validation and data access patterns rather than back-end data pipeline validation. No repositories in the govreposcrape index implement the kind of streaming or batch data validation pipeline (e.g., Apache Kafka consumers with schema registry, AWS Step Functions with validation stages, or event-driven validation microservices) that the Fuel Price Transparency Service requires.

The dominant technology stack across results is **.NET / C#** with PostgreSQL, reflecting the local council technology preferences in the index. Central government departments (alphagov, HMRC, DWP, MOJ) that typically use Ruby on Rails, Python, Java, or Node.js are not represented in these results.

The most transferable pattern is the **contract-first messaging** approach from Dorset Council's FORT system, which could inform the design of message validation schemas for fuel price submissions. The **GDS Design System validation** patterns are directly applicable to the manual submission forms.

---

## Implementation Approaches Compared

| Approach | Used By | Pros | Cons |
|----------|---------|------|------|
| Contract-First Distributed Messaging (C# shared libraries) | FloodOnlineReportingTool.Contracts | Strong typing, compile-time validation, clear service boundaries | Language-locked (C# only), tight coupling via shared NuGet packages |
| Server-Side Form Validation (WebForms / Blazor) | Escc.FormControls.WebForms, GdsBlazorComponents | GDS-compliant, accessible, proven patterns | Front-end only -- does not address back-end pipeline validation |
| ORM Model Validation (Entity Framework Core) | FloodOnlineReportingTool.Public, GIFramework-Maps | Database constraint enforcement, migration support, type safety | Validation at persistence layer only -- late in the pipeline |
| Open Data Quality Assessment (Manual Criteria) | open-data-scotland | Clear quality standards, human-readable | Not automated -- criteria applied manually to catalogue entries |

**Recommended Approach for This Project**: None of the approaches found are sufficient individually for the Fuel Finder's real-time data validation pipeline. The project requires a **multi-layer validation architecture** combining:

1. **API schema validation** (OpenAPI / JSON Schema) at the submission endpoint -- not found in govreposcrape results
2. **Business rule validation** (price range checks, fuel type validation, geospatial bounds) in a processing layer -- not found
3. **Data quality scoring** (timeliness, completeness, consistency) for compliance monitoring -- partially addressed by open-data-scotland's quality criteria approach
4. **Front-end form validation** for manual submission -- addressed by GdsBlazorComponents patterns

The team should look beyond govreposcrape for pipeline validation implementations. See Search Refinements below.

---

## Search Effectiveness Assessment

### Coverage

The search achieved **very low coverage** of the query's intent. The govreposcrape index is dominated by **local council repositories** from a small number of organisations:

- East Sussex County Council (approximately 25% of all results)
- BathnesDevelopment / Bath and North East Somerset Council (approximately 20%)
- Dorset Council (approximately 15%)
- Dundee City Council (approximately 10%)
- Other local councils (approximately 30%)

**Central government organisations not found in results**:

| Organisation | GitHub Org | Expected Content |
|---|---|---|
| Government Digital Service | alphagov | GOV.UK publishing pipeline, content validation, registers |
| HMRC | hmrc | Tax data validation, MTD submission pipelines |
| NHS Digital | NHSDigital | Patient data validation, FHIR pipelines, MESH |
| Department for Work and Pensions | dwp | Benefits data processing pipelines |
| Ministry of Justice | ministryofjustice | Case data validation, CJSE |
| Environment Agency | DEFRA / EnvironmentAgency | Flood monitoring real-time data pipelines |
| Office for National Statistics | ONSdigital | Statistical data validation pipelines |

These organisations maintain thousands of repositories on GitHub that are highly likely to contain data validation pipeline implementations but are not indexed by govreposcrape.

### Gaps

The following specific topics returned no relevant results:

| Gap | Why Expected | Alternative Search Strategy |
|-----|---|---|
| Streaming data validation (Kafka, SQS, EventBridge) | Central gov services use event-driven architectures | Search `https://github.com/alphagov?q=pipeline` and `https://github.com/hmrc?q=validation` directly |
| JSON Schema / OpenAPI validation middleware | Standard pattern for API submission validation | Search `https://github.com/alphagov?q=schema+validation` |
| Data quality scoring and monitoring | HMRC MTD and ONS both implement this | Search `https://github.com/ONSdigital?q=data+quality` |
| AWS Step Functions / Lambda validation pipelines | Common serverless validation pattern in gov | Search `https://github.com/alphagov?q=step+functions` or `https://github.com/dwp?q=lambda+validation` |
| Great Expectations / dbt data validation | Modern data quality frameworks used in gov | Search `https://github.com/ministryofjustice?q=great+expectations` |

### Index Limitations

The govreposcrape index has a **significant central government coverage gap**. Results are biased towards:

- **Local councils** over central government departments
- **.NET / C# / SharePoint** over Ruby, Python, Node.js, Java
- **Front-end / CMS** repositories over back-end data processing
- **Small utility libraries** over large service implementations

Users should not conclude that "UK government has not built real-time data validation pipelines" based on these results. The reality is that the index does not cover the organisations most likely to have built them.

---

## Project Relevance Mapping

| Repository | Relevant Requirements | How It Helps | Quick Start |
|---|---|---|---|
| Dorset-Council-UK/FloodOnlineReportingTool.Contracts | FR-004 (Price Submission API), INT-001 | Contract-first message design pattern for defining fuel price submission schemas | `git clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Contracts.git` |
| Dorset-Council-UK/FloodOnlineReportingTool.Public | FR-003 (Manual Price Submission), BR-002 | Public data submission workflow with GDS-compliant form validation | `git clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public.git` |
| Dorset-Council-UK/GdsBlazorComponents | FR-003, NFR-A (Accessibility) | GOV.UK Design System form validation components (if using .NET Blazor) | `dotnet add package GdsBlazorComponents` |
| Dorset-Council-UK/GIFramework-Maps | FR-001 (Fuel Price Display), FR-002 (Map View) | Geospatial data ingestion and map display with PostGIS | `git clone https://github.com/Dorset-Council-UK/GIFramework-Maps.git` |
| DundeeCityCouncil/open-data-scotland | BR-005 (Open Data Publication), NFR-DQ (Data Quality) | Data quality criteria framework for open data publishing | `git clone https://github.com/DundeeCityCouncil/open-data-scotland.git` |

---

## Recommendations

### Immediate Next Steps

1. **Search Central Government GitHub Organisations Directly**: The govreposcrape index does not cover the organisations most likely to have data validation pipeline implementations. Manually search alphagov, hmrc, NHSDigital, ONSdigital, dwp, and ministryofjustice GitHub organisations
2. **Clone and Review FloodOnlineReportingTool.Contracts**: Examine the message contract pattern for applicability to fuel price submission schema design. Focus on how contracts enforce data structure validation across distributed services
3. **Evaluate GIFramework-Maps Geospatial Stack**: Review the PostGIS data ingestion and query patterns for applicability to the fuel price map display component (FR-001, FR-002)
4. **Contact Dorset Council FORT Team**: Their distributed service architecture with message contracts is the closest pattern found to a validation pipeline. Reach out via their GitHub organisation to discuss reuse opportunities

### Search Refinements

If further searching is needed, consider these refined queries against alternative sources:

- `org:alphagov data pipeline validation` on GitHub Search -- would surface GOV.UK publishing pipeline validation implementations
- `org:hmrc schema validation submission` on GitHub Search -- would surface Making Tax Digital submission validation patterns
- `org:NHSDigital FHIR validation pipeline` on GitHub Search -- would surface NHS data interoperability validation
- `org:ONSdigital data quality pipeline` on GitHub Search -- would surface statistical data validation frameworks
- `org:defra flood monitoring real-time` on GitHub Search -- would surface Environment Agency real-time sensor data pipelines
- `org:ministryofjustice data platform validation` on GitHub Search -- would surface MOJ Analytical Platform data validation

### Related ArcKit Commands

- Run `/arckit:gov-reuse` for a full reusability assessment of the Dorset Council FORT repositories
- Run `/arckit:gov-landscape` for a broader landscape analysis of data pipeline implementations across government
- Run `/arckit:research` to investigate commercial and open-source data validation frameworks (Great Expectations, dbt, Apache Beam, AWS Glue DataBrew) suitable for the Fuel Finder pipeline

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-001-REQ-v2.0 | Requirements | Project 001 | FR-003, FR-004, BR-002, BR-005 -- data submission and validation requirements | projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md |
| ARC-001-GCSR-v1.0 | Prior GCSR | Project 001 | Previous search for "fuel price data ingestion" -- complementary findings | projects/001-uk-fuel-price-transparency-service/research/ARC-001-GCSR-v1.0.md |
| GOV.UK Design System | Standard | GDS | Form validation patterns and error messaging guidance | https://design-system.service.gov.uk/patterns/ |
| GDS API Technical and Data Standards | Standard | GDS/CDDO | API design standards including validation approaches | https://www.gov.uk/guidance/gds-api-technical-and-data-standards |

---

**Generated by**: ArcKit `/arckit:gov-code-search` agent
**Generated on**: 2026-03-24
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: Claude Opus 4.6 (1M context)
