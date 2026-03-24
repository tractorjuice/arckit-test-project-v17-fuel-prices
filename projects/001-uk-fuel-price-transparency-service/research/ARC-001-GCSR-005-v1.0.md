# Government Code Search Report: UK Fuel Price Transparency Service -- Regulatory Compliance Dashboards

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit:gov-code-search`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GCSR-005-v1.0 |
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
| **Distribution** | CMA Digital, DESNZ Policy, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-24 | ArcKit AI | Initial creation from `/arckit:gov-code-search` agent -- search for regulatory compliance dashboards across UK government open-source repositories | PENDING | PENDING |

---

## Executive Summary

### Search Query

**Original Query**: `regulatory compliance dashboards`

**Query Variations Used**:

- `compliance monitoring dashboard government enforcement`
- `regulatory monitoring and reporting tools`
- `admin dashboard data visualisation GOV.UK`
- `enforcement case management compliance tracking`
- `operational dashboard metrics analytics government service`
- `performance dashboard Ruby on Rails GOV.UK internal tools`
- `data submission compliance monitoring CMA HMRC enforcement`
- `real-time monitoring service health status reporting`
- `internal admin panel reporting statistics government digital service`
- `Grafana Kibana dashboard monitoring alerting government`
- `data quality reporting validation submission tracking`
- `Blazor GDS design system components .NET dashboard`
- `open data portal reporting statistics visualisation charts`

**Platforms Searched**: govreposcrape (indexing approximately 24,500 UK government GitHub repositories)

### Results Found

**Total Results Before Deduplication**: 147 repository references across 14 searches

**Unique Repositories After Deduplication**: 38

**High Relevance Results**: 3

**Medium Relevance Results**: 5

**Low Relevance / Excluded**: 30

### Top Results

| # | Repository | Organisation | Relevance | Language | Last Active |
|---|------------|--------------|-----------|----------|-------------|
| 1 | GdsBlazorComponents | Dorset Council | High | C# / HTML | 2026-03-20 |
| 2 | GIFramework-Maps | Dorset Council | High | TypeScript / C# | 2025-02-20 |
| 3 | FloodOnlineReportingTool.Public | Dorset Council | High | C# | 2025-06-17 |
| 4 | Escc.WebAuthorMonitoring | East Sussex County Council | Medium | C# | 2019-06-13 (archived) |
| 5 | open-data-scotland | Dundee City Council | Medium | Python | 2015-09-01 |

### Key Finding

**No UK government open-source repositories were found that directly implement a "regulatory compliance dashboard" -- that is, a dashboard designed for regulators to monitor regulated entities' compliance with statutory obligations.** The govreposcrape index, which covers approximately 24,500 repositories, returned zero results for the exact query "regulatory compliance dashboards" and yielded only tangentially related results across 13 query variations. This is a significant gap finding.

The most relevant results are component libraries and frameworks (GDS Blazor components, GIS mapping tools) that could be used to *build* a compliance dashboard, rather than pre-built compliance dashboards themselves. This is consistent with the fact that central government organisations (alphagov, NHSDigital, hmrc, dwp, moj, dfe) did not appear in any search results -- the govreposcrape index for this query space is dominated by local council repositories.

---

## Search Results

### High Relevance Results

#### Dorset-Council-UK/GdsBlazorComponents

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Local Authority) |
| **Repository URL** | https://github.com/Dorset-Council-UK/GdsBlazorComponents |
| **Description** | Blazor components styled to match the GOV.UK Design System, providing 30+ reusable UI components for government .NET applications |
| **Language** | C# (41.1%), HTML (45.1%), TypeScript, SCSS |
| **License** | MIT |
| **Last Activity** | 2026-03-20 (v3.0.0) |
| **Stars** | 4 |

**Why Relevant**: This is the most directly useful repository for building a compliance dashboard that conforms to GOV.UK Design System standards. It provides pre-built Blazor components (tables, panels, notification banners, form inputs, buttons, headers, footers) that could form the UI foundation of a CMA enforcement dashboard. The component library supports both Blazor Web App and WebAssembly deployment models.

**Key Patterns**:

- GOV.UK Design System compliance through Blazor component abstraction
- MIT-licensed, enabling unrestricted reuse across government projects
- Actively maintained (latest release March 2026, v3.0.0)
- Originally built for the Flood Online Reporting Tool, demonstrating real-world government service use

---

#### Dorset-Council-UK/GIFramework-Maps

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Local Authority) |
| **Repository URL** | https://github.com/Dorset-Council-UK/GIFramework-Maps |
| **Description** | A .NET-based web mapping application for creating, sharing, and managing maps using OGC web services, with built-in administration tools |
| **Language** | TypeScript (42.7%), C# (37.6%) |
| **License** | MIT |
| **Last Activity** | 2025-02-20 |
| **Stars** | 21 |

**Why Relevant**: While not a compliance dashboard per se, this is the most mature data visualisation platform found in the search. It demonstrates patterns for spatial data querying, interactive filtering, PDF export, and administration panels -- all capabilities needed in a compliance monitoring dashboard. For a fuel price transparency service, geographic visualisation of compliance rates by region would be a natural dashboard feature. The 21 stars and 12 forks indicate meaningful adoption.

**Key Patterns**:

- .NET backend with TypeScript/OpenLayers frontend for interactive data visualisation
- PostgreSQL with PostGIS for spatial data storage and querying
- GUI-based administration interface with configurable views
- PDF export capability for reporting
- Azure AD authentication for secure internal access
- MIT-licensed for government reuse

---

#### Dorset-Council-UK/FloodOnlineReportingTool.Public

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Local Authority) |
| **Repository URL** | https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public |
| **Description** | A .NET web application enabling public flood reporting to local authorities, built on GDS Design System with a distributed messaging architecture |
| **Language** | C# (81.1%) |
| **License** | MIT |
| **Last Activity** | 2025-06-17 |
| **Stars** | 0 |

**Why Relevant**: This is a real-world government regulatory reporting tool -- public submissions of flood reports to authorities for action. While the domain (flood reporting) differs from fuel price compliance, the architectural patterns are highly relevant: a data submission pipeline, distributed messaging via contracts (FloodOnlineReportingTool.Contracts), GDS-styled UI, and PostgreSQL with PostGIS for spatial data. The "mission control" component referenced in the codebase suggests an internal dashboard for managing incoming reports.

**Key Patterns**:

- .NET with Entity Framework Core for data access
- PostgreSQL 13+ with PostGIS for geospatial data
- Distributed architecture with message contracts (separate Contracts NuGet package)
- GOV.UK Design System compliance via GdsBlazorComponents
- Multi-council deployment (single codebase serving multiple authorities)
- Feature flags for progressive rollout of new capabilities

---

### Medium Relevance Results

#### east-sussex-county-council/Escc.WebAuthorMonitoring

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council (Local Authority) |
| **Repository URL** | https://github.com/east-sussex-county-council/Escc.WebAuthorMonitoring |
| **Description** | Quality monitoring tool to report problems with web content to responsible web authors and track previous problems |
| **Language** | C# (77.4%), Classic ASP, PowerShell, JavaScript |
| **License** | Available (unspecified type) |
| **Last Activity** | 2019-06-13 (archived) |
| **Stars** | 0 |

**Why Relevant**: This is a compliance monitoring tool -- it detects content quality issues, routes them to responsible parties, and tracks historical problems. The pattern of "detect non-compliance, notify responsible party, track resolution" maps directly to the CMA enforcement workflow (detect missed fuel price submissions, notify retailer, track resolution). However, the repository is archived and uses legacy technologies (Classic ASP).

**Key Patterns**:

- Detection-notification-tracking pattern for compliance monitoring
- Historical problem tracking for audit trails
- Routing issues to responsible parties based on ownership

---

#### DundeeCityCouncil/open-data-scotland

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dundee City Council (Local Authority) |
| **Repository URL** | https://github.com/DundeeCityCouncil/open-data-scotland |
| **Description** | Curated catalogue of open data resources across Scotland, listing portals with bulk downloads, APIs, or SPARQL endpoints |
| **Language** | Python (92.3%) |
| **License** | Not specified |
| **Last Activity** | 2015-09-01 |
| **Stars** | 0 |

**Why Relevant**: Demonstrates a government approach to cataloguing and monitoring data source compliance -- tracking which organisations are publishing open data and in what formats. The concept of monitoring data publication compliance across multiple entities parallels the Fuel Finder need to monitor ~8,500 forecourt compliance. However, the repository is inactive (last update 2015) and minimal in scope.

**Key Patterns**:

- CSV-based registry of data sources with quality criteria
- Inclusion criteria defining minimum standards for machine-readable data publication
- Catalogue approach to tracking compliance across multiple organisations

---

#### brighton-hove-gov-uk/bhbudget

| Attribute | Value |
|-----------|-------|
| **Organisation** | Brighton & Hove City Council (Local Authority) |
| **Repository URL** | https://github.com/brighton-hove-gov-uk/bhbudget |
| **Description** | Budget planning tool allowing citizens to rank council spending priorities while learning about budget sizes and services |
| **Language** | PHP (50.0%), CSS (30.2%), JavaScript (19.8%) |
| **License** | Not specified |
| **Last Activity** | 2021-03-28 |
| **Stars** | 2 |

**Why Relevant**: A citizen-facing data interaction tool that collects and stores user input for subsequent analysis. The pattern of collecting structured data from users and storing it for reporting is tangentially relevant, though the implementation (PHP/MySQL, manual CSV export) is outdated for modern government services.

**Key Patterns**:

- Citizen-facing data collection with MySQL storage
- Session-based interaction tracking
- Manual data export for analysis (no built-in dashboard)

---

#### BristolCityCouncil/send

| Attribute | Value |
|-----------|-------|
| **Organisation** | Bristol City Council (Local Authority) |
| **Repository URL** | https://github.com/BristolCityCouncil/send |
| **Description** | Special Educational Needs application enabling schools to submit standardised funding applications to the council |
| **Language** | Java (84.8%) |
| **License** | Available (unspecified type) |
| **Last Activity** | 2022-06-06 |
| **Stars** | 0 |

**Why Relevant**: A regulatory submission management system -- schools submit structured applications that are processed by the council. The pattern of regulated entities submitting structured data to a regulatory body parallels the Fuel Finder's forecourt price submission workflow. Uses Spring Boot, Azure Cosmos DB, and Microsoft Graph API.

**Key Patterns**:

- Spring Boot application for structured data submission
- Azure Cosmos DB for document storage
- Microsoft Graph API for integration with Microsoft 365
- Active Directory authentication for secure access
- PDF generation for formal document output
- ClamAV integration for uploaded file scanning

---

#### BathnesDevelopment/processmaker-3.1.2.b2-community

| Attribute | Value |
|-----------|-------|
| **Organisation** | Bath & North East Somerset Council (Local Authority) |
| **Repository URL** | https://github.com/BathnesDevelopment/processmaker-3.1.2.b2-community |
| **Description** | Community fork of ProcessMaker, an open-source workflow and business process management platform |
| **Language** | PHP (66.4%), JavaScript (19.9%) |
| **License** | AGPL-3.0 |
| **Last Activity** | 2016-11-02 |
| **Stars** | 0 |

**Why Relevant**: A workflow and case management platform with RBAC, relevant to enforcement case management. However, this is an outdated (2016) fork of a third-party tool rather than a government-built solution, and the AGPL-3.0 licence imposes copyleft obligations.

**Key Patterns**:

- Workflow engine for business process automation
- Role-based access control (RBAC)
- Case management with configurable process flows

---

## Code Patterns Identified

| Pattern | Repositories Using It | Description |
|---------|----------------------|-------------|
| GOV.UK Design System components | GdsBlazorComponents, FloodOnlineReportingTool.Public | Pre-built UI components conforming to GOV.UK Design System standards, implemented as Blazor components for .NET applications |
| .NET with PostgreSQL/PostGIS | GIFramework-Maps, FloodOnlineReportingTool.Public | .NET backend with Entity Framework Core, PostgreSQL for relational data and PostGIS for spatial queries -- a pattern suitable for geospatial compliance monitoring |
| Distributed messaging architecture | FloodOnlineReportingTool.Public, FloodOnlineReportingTool.Contracts | Service-to-service communication via typed message contracts, enabling decoupled processing pipelines |
| Detection-notification-tracking workflow | Escc.WebAuthorMonitoring | Automated detection of non-compliance, notification to responsible parties, and historical tracking of issues -- directly analogous to CMA enforcement workflows |
| Structured data submission by regulated entities | BristolCityCouncil/send, FloodOnlineReportingTool.Public | External parties (schools, public) submitting structured data to government bodies through validated web forms |
| Azure AD authentication for internal tools | GIFramework-Maps, BristolCityCouncil/send | Azure Active Directory integration for securing internal-facing administration and dashboard interfaces |
| MIT licensing for government code | GdsBlazorComponents, GIFramework-Maps, FloodOnlineReportingTool.Public | MIT licence chosen as the standard permissive licence for local authority open-source code, enabling unrestricted reuse |

**Observations**: The search results reveal a consistent pattern across local authority repositories: .NET (C#) is the dominant backend language, PostgreSQL with PostGIS is the preferred database for geospatially-aware applications, and the GOV.UK Design System is adopted via Blazor components rather than the canonical Nunjucks/Node.js implementation. No central government (alphagov, NHSDigital, hmrc, dwp, moj) repositories appeared in any search results, which is a critical limitation of the govreposcrape index for this query domain. Central government organisations typically build compliance and enforcement dashboards as internal tools that are either not open-sourced or hosted on private infrastructure.

---

## Implementation Approaches Compared

| Approach | Used By | Pros | Cons |
|----------|---------|------|------|
| Blazor .NET with GDS components | GdsBlazorComponents, FloodOnlineReportingTool.Public | GOV.UK Design System compliance out of the box; strong typing; component reuse; active maintenance | Smaller ecosystem than React/Node.js; fewer GDS component libraries available for Blazor vs Nunjucks |
| TypeScript + OpenLayers for spatial visualisation | GIFramework-Maps | Interactive maps; mature spatial data tooling; PDF export; 21 stars indicates adoption | Specialised for geographic data; steep learning curve for OpenLayers; requires PostGIS expertise |
| Spring Boot + Azure Cosmos DB | BristolCityCouncil/send | Mature Java ecosystem; flexible document storage; Microsoft 365 integration | Cosmos DB vendor lock-in; higher operational cost than PostgreSQL; less common in government |
| PHP workflow engine | processmaker (BathnesDevelopment) | Low-code workflow configuration; RBAC built in | Outdated (2016); AGPL licence restrictions; PHP declining in government adoption |

**Recommended Approach for This Project**: The Blazor .NET stack with GDS components (as demonstrated by Dorset Council's GdsBlazorComponents and FloodOnlineReportingTool) is the strongest candidate for building a CMA compliance dashboard, provided the delivery team has .NET skills. This approach provides GOV.UK Design System compliance, active maintenance, MIT licensing, and a proven pattern for government reporting tools. For the geographic visualisation of compliance rates (e.g., map of forecourt submission status by region), the GIFramework-Maps patterns could be adapted.

However, given that the Fuel Finder service's primary technology choices will be determined by ADR decisions (see ARC-001-REQ-v2.0, FR requirements), the compliance dashboard should align with whatever frontend framework is selected for the wider service. If the service uses Node.js/React (the more common GDS stack), these .NET patterns serve as architectural reference rather than direct code reuse.

---

## Project Relevance Mapping

| Repository | Relevant Requirements | How It Helps | Quick Start |
|---|---|---|---|
| Dorset-Council-UK/GdsBlazorComponents | BR-004 (CMA Enforcement), FR-010 (Compliance Dashboard), BR-007 (Governance) | Provides GOV.UK-compliant UI components for building the CMA enforcement dashboard | `git clone https://github.com/Dorset-Council-UK/GdsBlazorComponents.git` |
| Dorset-Council-UK/GIFramework-Maps | BR-003 (Citizen Comparison), BR-004 (Enforcement), NFR-P (Performance) | Demonstrates spatial data visualisation patterns for mapping forecourt compliance geographically | `git clone https://github.com/Dorset-Council-UK/GIFramework-Maps.git` |
| Dorset-Council-UK/FloodOnlineReportingTool.Public | BR-002 (Data Submission), BR-004 (Enforcement), INT requirements | Architectural reference for regulatory data submission pipelines with distributed messaging | `git clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public.git` |
| east-sussex-county-council/Escc.WebAuthorMonitoring | BR-004 (Enforcement), O-3 (Non-compliance detection) | Pattern reference for detection-notification-tracking compliance workflow | `git clone https://github.com/east-sussex-county-council/Escc.WebAuthorMonitoring.git` |
| BristolCityCouncil/send | BR-002 (Data Submission), INT-001 (Retailer Integration) | Pattern reference for structured submissions from external regulated entities | `git clone https://github.com/BristolCityCouncil/send.git` |

---

## Search Effectiveness Assessment

### Coverage

The search achieved **low coverage** of the original query intent. "Regulatory compliance dashboards" as a concept -- a dashboard used by a regulator to monitor compliance of regulated entities -- returned zero direct matches from the govreposcrape index. The 38 unique repositories found across 14 query variations are tangentially related at best: component libraries, mapping tools, and data submission applications that could contribute to building such a dashboard, but none that implement one.

### Organisation Bias

Results were **entirely dominated by local authority repositories**:

- Dorset Council (6 repos)
- East Sussex County Council (8 repos)
- Bath & NE Somerset Council (5 repos)
- Brighton & Hove City Council (1 repo)
- Bristol City Council (1 repo)
- Dundee City Council (4 repos)
- Camden Council (3 repos)
- Bracknell Forest Council (3 repos)

**No central government organisations appeared**: alphagov (GDS), NHSDigital, hmrc, dwp, moj, dfe, CMA, Ofgem, Ofcom, FCA, or any other regulator. This is a critical coverage gap. Central government regulators (CMA, FCA, Ofgem, Ofcom, ORR) either:

1. Do not open-source their enforcement/compliance tools
2. Host code on private infrastructure (GitLab, Azure DevOps) not indexed by govreposcrape
3. Use commercial off-the-shelf (COTS) case management platforms rather than building bespoke dashboards

### Gaps and Alternative Search Strategies

| Gap | Alternative Strategy |
|-----|---------------------|
| No CMA repositories found | Search directly: `https://github.com/CMA-gov` or contact CMA Digital team |
| No alphagov dashboard repos | Search: `https://github.com/alphagov?q=dashboard` -- alphagov has 2,000+ repos that may include internal dashboard patterns |
| No HMRC compliance tools | Search: `https://github.com/hmrc?q=compliance+monitoring` -- HMRC has 1,500+ repos |
| No Ofgem regulatory tools | Ofgem (energy regulator) may have relevant patterns: `https://github.com/search?q=org%3Aofgem+dashboard` |
| No FCA enforcement tools | FCA (Financial Conduct Authority) regulatory dashboard patterns: `https://github.com/search?q=org%3Afca+compliance` |
| No GOV.UK Performance Platform | The former GOV.UK Performance Platform (performance.service.gov.uk) was a government dashboard platform -- search `https://github.com/alphagov?q=performance-platform` |
| No Grafana/Kibana government configs | Central government teams commonly use Grafana and Kibana for operational dashboards but rarely open-source their configurations |

### Index Limitations

The govreposcrape index appears to have strong coverage of local authority repositories (councils) but weak coverage of central government departments and arm's-length regulatory bodies. For a query about regulatory compliance dashboards -- a domain owned by central government regulators -- this represents a fundamental limitation. Users should not conclude that "no government team has built regulatory compliance dashboards" based on these results; rather, the index does not cover the organisations most likely to have built them.

---

## Recommendations

### Immediate Next Steps

1. **Clone and Review**: Dorset-Council-UK/GdsBlazorComponents -- examine the component library for applicability to a .NET-based compliance dashboard; review the live demo at the Azure-hosted site
2. **Architecture Reference**: Dorset-Council-UK/FloodOnlineReportingTool.Public -- study the distributed messaging architecture (via Contracts package) as a pattern for the data submission and compliance monitoring pipeline
3. **Direct GitHub Search**: Search alphagov (GDS) and hmrc organisations directly on GitHub for dashboard, performance-platform, and compliance repositories not indexed by govreposcrape
4. **Contact CMA Digital**: As the owning department, CMA Digital should check whether existing internal tools, Salesforce configurations, or Power BI dashboards are already in use for other CMA enforcement domains (competition, consumer protection) that could be extended for fuel price compliance
5. **Explore GOV.UK Performance Platform heritage**: The now-retired GOV.UK Performance Platform (alphagov/performance-platform-*) may contain reusable dashboard patterns and visualisation code

### Search Refinements

If further searching is needed, consider these refined queries:

- `alphagov performance platform dashboard visualisation` -- may surface the GOV.UK Performance Platform codebase
- `HMRC risk scoring compliance monitoring service` -- HMRC has extensive compliance monitoring capabilities
- `Ofgem energy market monitoring regulatory reporting` -- closest regulatory domain to fuel price monitoring
- `case management enforcement investigation government` -- broader search for enforcement tooling patterns

### Related ArcKit Commands

- Run `/arckit:gov-reuse` for a full reusability assessment of GdsBlazorComponents and GIFramework-Maps
- Run `/arckit:gov-landscape` for a broader landscape analysis of dashboard and data visualisation tools across government
- Run `/arckit:research` to investigate commercial compliance dashboard platforms (e.g., Salesforce Compliance, ServiceNow GRC, Power BI) as build-vs-buy alternatives

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-001-REQ-v2.0 | Requirements | Project 001 | BR-004 (CMA Enforcement Capability), FR-010 (Compliance Dashboard), O-3 (Non-compliance detection < 24h) | projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md |
| GOV.UK Design System | Standard | GDS | Component patterns for government-compliant UI | https://design-system.service.gov.uk/ |
| GOV.UK Performance Platform (archived) | Platform | alphagov | Historical dashboard platform for government services | https://github.com/alphagov?q=performance-platform |

---

**Generated by**: ArcKit `/arckit:gov-code-search` agent
**Generated on**: 2026-03-24
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: Claude Opus 4.6 (1M context)
