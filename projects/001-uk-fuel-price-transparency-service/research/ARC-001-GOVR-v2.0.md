# Government Reuse Assessment: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit.gov-reuse`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GOVR-v2.0 |
| **Document Type** | Government Reuse Assessment |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 2.0 |
| **Created Date** | 2026-03-24 |
| **Last Modified** | 2026-03-24 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-06-24 |
| **Owner** | CMA Digital Lead (Architecture Lead) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-23 | ArcKit AI | Initial creation from `/arckit.gov-reuse` agent | PENDING | PENDING |
| 2.0 | 2026-03-24 | ArcKit AI | Expanded search scope (10 query variations, 62 repos reviewed); added Capability 8 (Rapid Prototyping) with alphagov/govuk-prototype-kit; added new candidate DundeeCityCouncil/open-data-scotland for open data publishing; added BristolCityCouncil/send as reference for assessment workflow patterns; refreshed WebFetch data for all shortlisted candidates; updated scoring and effort estimates; supersedes v1.0 | PENDING | PENDING |

---

## Executive Summary

### Search Scope

This assessment searched approximately 21,000 UK government repositories indexed by govreposcrape across local councils, NHS bodies, central government departments, and cross-government platforms. Ten query variations were executed across eight capability areas derived from the requirements baseline (ARC-001-REQ-v2.0) for the UK Fuel Price Transparency Service ("Fuel Finder"), which operates under the Motor Fuel Price (Open Data) Regulations 2025.

Search queries covered: fuel price data ingestion, data validation pipelines, open data API publishing, retailer registration and account management, GOV.UK Notify integration, geospatial proximity search, compliance monitoring dashboards, audit trail logging, API rate limiting, rapid prototyping, and CKAN/open data portals. Results were cross-referenced against known alphagov platform repositories (govuk-frontend, notifications clients, govuk-prototype-kit) which are directly mandated by TCoP Principle 13.

The indexed repository population is heavily weighted towards local authority organisations (Dorset Council, East Sussex County Council, Camden Council, Dundee City Council, BANES, Bristol City Council, City of York, Brighton and Hove). Central government alphagov repositories were assessed directly via WebFetch as known high-value candidates.

**Capabilities Assessed**: 8 capability areas across 10 government organisations

**Repositories Evaluated**: 62 repositories reviewed via search; 12 shortlisted for detailed WebFetch assessment; 10 scored

### Key Findings

| Capability | Best Candidate | Organisation | Reuse Strategy | Effort Saved |
|------------|---------------|--------------|----------------|--------------|
| Citizen-facing UI and Design System | alphagov/govuk-frontend | GDS / alphagov | Library | 25 person-days |
| GOV.UK Notify integration | alphagov/notifications-python-client | GDS / alphagov | Library | 8 person-days |
| Rapid prototyping (Alpha phase) | alphagov/govuk-prototype-kit | GDS / alphagov | Library | 10 person-days |
| Online data submission (web form + validation) | Dorset-Council-UK/FloodOnlineReportingTool.Public | Dorset Council | Reference | 5 person-days |
| Geospatial mapping framework | Dorset-Council-UK/GIFramework-Maps | Dorset Council | Reference | 4 person-days |
| Geospatial location finder (proximity search) | east-sussex-county-council/Escc.Libraries.BranchFinder | East Sussex CC | Reference | 3 person-days |
| GOV.UK Design System (Blazor/.NET) | Dorset-Council-UK/GdsBlazorComponents | Dorset Council | Reference | 3 person-days |
| Open data catalogue pattern | DundeeCityCouncil/open-data-scotland | Dundee City Council | Reference | 1 person-day |
| Fuel price data ingestion pipeline | None found | -- | Build new | -- |
| Compliance monitoring dashboard | None found | -- | Build new | -- |
| Audit trail / tamper-evident logging | None found | -- | Build new | -- |

### Reuse Summary

**Total Estimated Effort Saved**: 59 person-days across Library and Reference candidates (up from 48 in v1.0)

**Reuse Coverage**: 5 of 8 capability areas have at least a Reference-quality government code candidate (63%). 3 capabilities have Library-quality candidates suitable for direct adoption as dependencies.

**Recommended Approach**: The highest-value reuse actions are mandatory platform adoptions -- GOV.UK Frontend (alphagov/govuk-frontend), the GOV.UK Notify client libraries, and the GOV.UK Prototype Kit are all production-grade, MIT-licensed, actively maintained by GDS, and directly mandated or recommended by the Technology Code of Practice. These should be adopted as npm/PyPI dependencies, not forked. The Prototype Kit (new in v2.0) is particularly valuable for the Alpha phase, enabling rapid prototyping of the citizen fuel price finder and retailer submission journey for user research sessions. The Dorset Council and East Sussex CC repositories provide valuable Reference material for data submission patterns and location-search architecture, though their C#/.NET stack diverges from the project's likely Python or Node.js stack. No suitable government code was found for the specialised capabilities of fuel price data ingestion, compliance monitoring dashboards, or tamper-evident audit logging -- these remain genuine gaps requiring build from scratch.

---

## Capability Analysis

### Capability 1: Citizen-Facing UI and Design System

**Requirements Addressed**: BR-003, FR-004, NFR-U-001, NFR-U-002, NFR-U-003, NFR-C-003, INT-004

**Search Terms Used**:
- "GOV.UK Design System frontend components accessible government service"
- "GOV.UK frontend design system accessible WCAG components"

---

#### Candidate: alphagov/govuk-frontend

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (alphagov) |
| **Repository URL** | https://github.com/alphagov/govuk-frontend |
| **Language** | JavaScript (55.1%), Nunjucks (31.9%), SCSS (12.5%) |
| **License** | MIT (Crown Copyright, GDS, 2017) |
| **Last Activity** | March 2026 (v6.1.0 release, 2 March 2026) |
| **Stars** | 1,400 |
| **Contributors** | Active (12,225 total commits; 7,700+ dependent projects) |
| **Documentation** | Excellent |

**Description**: GOV.UK Frontend is the official GDS library of HTML, CSS, and JavaScript components implementing the GOV.UK Design System. It is the canonical implementation for all government digital services and provides WCAG 2.2 AA-compliant, accessible components (buttons, form inputs, error summaries, notification banners, phase banners, header/footer, breadcrumbs). It is used by thousands of government services and is mandated for citizen-facing interfaces under GDS Service Standard Point 3 and TCoP Point 2.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT (Crown Copyright, GDS). Fully compatible -- free to use, modify, distribute with attribution |
| **Code Quality** | 5 | 12,225 commits; Jest + Puppeteer automated tests; ESLint + Stylelint; build CI active; 7,700+ dependent projects; 100+ releases |
| **Documentation Quality** | 5 | Comprehensive README, GOV.UK Design System website (629 stars, 7,031 commits), per-component docs, browser support matrix, accessibility notes, contributing guide |
| **Tech Stack Alignment** | 5 | JavaScript/SCSS npm package -- integrates with any modern web stack; Nunjucks macros for server-side rendering (Node.js) |
| **Activity / Maintenance** | 5 | v6.1.0 released 2 March 2026; GDS actively maintains; long-term government commitment; 128 contributors to design system docs |
| **Overall** | **5.0** | |

**Recommended Strategy**: Library

**Estimated Effort Saved**: 25 person-days (building accessible, standards-compliant government UI components from scratch is substantial; using govuk-frontend eliminates that work entirely)

**Key Considerations**:

- This is a mandatory adoption per TCoP and GDS Service Standard, not an optional reuse decision
- Install via npm: `npm install govuk-frontend`
- Version 6.x requires Node.js 18+; confirm project runtime
- Nunjucks macros provide server-side rendering; React/Vue wrappers exist in the community but are not officially maintained by GDS
- Welsh language (NFR-U-003) content translations must be provided by the Fuel Finder team -- govuk-frontend provides components but not domain content
- Map display for FR-004 (proximity search) requires additional mapping library (Leaflet.js or similar); govuk-frontend provides a list-view fallback pattern for accessibility compliance
- The companion govuk-design-system repo (MIT, 629 stars, 7,031 commits) provides pattern documentation and examples

---

### Capability 2: GOV.UK Notify Integration

**Requirements Addressed**: FR-009, INT-003, NFR-A-003

**Search Terms Used**:
- "GOV.UK Notify integration email SMS notification retailer"
- "registration account management authentication OAuth API key government service"

---

#### Candidate: alphagov/notifications-python-client

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (alphagov) |
| **Repository URL** | https://github.com/alphagov/notifications-python-client |
| **Language** | Python (95.1%) |
| **License** | MIT (Crown Copyright, GDS, 2015) |
| **Last Activity** | Active (830 commits on main; 1 open issue, 4 open PRs) |
| **Stars** | 24 |
| **Contributors** | GDS Notify team (23 forks) |
| **Documentation** | Strong |

**Description**: The official GDS Python client library for the GOV.UK Notify API. Enables sending emails, SMS, and letters via the government's shared notification platform. Published on PyPI. Includes comprehensive API documentation at docs.notifications.service.gov.uk. The Fuel Finder service requires GOV.UK Notify for retailer compliance reminders (FR-009), submission confirmations, and enforcement notices (FR-006, UC-4).

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT (Crown Copyright, GDS). Fully compatible |
| **Code Quality** | 5 | Tox multi-environment testing; Flake8 + Ruff linting; Dockerfile; Makefile; 830 commits; actively maintained by GDS Notify team |
| **Documentation Quality** | 5 | Official docs at docs.notifications.service.gov.uk/python.html; PyPI page; changelog; contributing guide |
| **Tech Stack Alignment** | 4 | Python -- aligns if project uses Python backend. If Node.js is chosen, use notifications-node-client instead |
| **Activity / Maintenance** | 5 | GDS Notify team actively maintains; open issues addressed; 4 open PRs at time of assessment |
| **Overall** | **4.8** | |

**Recommended Strategy**: Library

**Estimated Effort Saved**: 8 person-days (building a Notify integration client from scratch, including retry logic, error handling, and delivery status webhooks)

**Key Considerations**:

- Install via pip: `pip install notifications-python-client`
- If the project adopts Node.js, use `alphagov/notifications-node-client` instead (MIT, JavaScript 88.4%, 554 commits, 18 stars -- same quality tier)
- GOV.UK Notify service itself requires a service account and API key -- separate onboarding step with GDS Notify team
- Retry logic and dead letter queue handling for failed notifications (NFR-A-003) must be implemented by the Fuel Finder team on top of the client library
- Bulk notification (reminders to thousands of retailers) should use the Notify bulk send API endpoints; the client library supports this

---

#### Candidate: alphagov/notifications-node-client

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (alphagov) |
| **Repository URL** | https://github.com/alphagov/notifications-node-client |
| **Language** | JavaScript (88.4%), TypeScript (8.6%) |
| **License** | MIT |
| **Last Activity** | Active (554 commits on main) |
| **Stars** | 18 |
| **Contributors** | GDS Notify team |
| **Documentation** | Strong |

**Description**: Official GDS Node.js client for GOV.UK Notify. Functionally equivalent to the Python client. Relevant if the Fuel Finder backend is Node.js/TypeScript rather than Python. TypeScript type definitions included.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT. Fully compatible |
| **Code Quality** | 4 | spec/ test directory; 554 commits; active GDS maintenance |
| **Documentation Quality** | 5 | docs.notifications.service.gov.uk; NPM package; changelog |
| **Tech Stack Alignment** | 4 | Node.js -- aligns if project uses Node.js backend |
| **Activity / Maintenance** | 5 | Actively maintained by GDS |
| **Overall** | **4.6** | |

**Recommended Strategy**: Library

**Estimated Effort Saved**: 8 person-days (same as Python client -- alternative based on tech stack choice)

**Key Considerations**:

- Install via npm: `npm install notifications-node-client`
- Choose either Python or Node.js client based on the project's backend language choice -- not both
- TypeScript type definitions included for type-safe integration

---

### Capability 3: Rapid Prototyping (Alpha Phase)

**Requirements Addressed**: BR-003, BR-007, FR-004, UC-1, UC-2, UC-6, UC-7

**Search Terms Used**:
- "GOV.UK frontend design system accessible WCAG components"
- "GOV.UK prototype kit rapid prototyping government service"

---

#### Candidate: alphagov/govuk-prototype-kit

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (alphagov) |
| **Repository URL** | https://github.com/alphagov/govuk-prototype-kit |
| **Language** | JavaScript (89%) |
| **License** | MIT |
| **Last Activity** | March 2026 (v13.19.1 released 5 March 2026) |
| **Stars** | 334 |
| **Contributors** | GDS Design System team (4,057 total commits) |
| **Documentation** | Excellent |

**Description**: The GOV.UK Prototype Kit enables rapid creation of interactive HTML prototypes that look like pages on GOV.UK. It integrates with govuk-frontend components and is the standard tool for government service teams during Discovery and Alpha phases. For the Fuel Finder project, this is directly applicable to prototyping the citizen fuel price finder (UC-1), retailer price submission journey (UC-2), forecourt registration flow (UC-6), and the in-car interface concept (UC-7) for user research sessions.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT. Fully compatible |
| **Code Quality** | 5 | 4,057 commits; actively maintained by GDS; 100+ releases; automated testing |
| **Documentation Quality** | 5 | Comprehensive documentation; step-by-step tutorials; GDS-maintained guides; large user community |
| **Tech Stack Alignment** | 5 | JavaScript/Nunjucks -- builds on govuk-frontend; outputs standard HTML prototypes |
| **Activity / Maintenance** | 5 | v13.19.1 released 5 March 2026; maintained by GDS Design System team; supports current and previous Node.js LTS |
| **Overall** | **5.0** | |

**Recommended Strategy**: Library

**Estimated Effort Saved**: 10 person-days (building custom prototypes from scratch for user research would take significantly longer; the Prototype Kit provides immediate access to all GOV.UK components and patterns, enabling the team to test user journeys within days rather than weeks)

**Key Considerations**:

- Install and start prototyping immediately during Alpha
- Must be password-protected if published online to prevent public confusion with the live service
- Prototypes are for user research only -- not for building the production service
- The kit supports current and previous Node.js LTS versions
- GDS assessment teams expect to see evidence of prototyping with the kit during Alpha assessments (BR-007)
- Minimal support from GDS -- the team should be comfortable with basic Node.js and Nunjucks
- Prototype code for the citizen fuel finder (UC-1) and retailer submission (UC-2) journeys can inform production design decisions

---

### Capability 4: Online Data Submission (Web Form and Validation Pipeline)

**Requirements Addressed**: FR-002, FR-003, FR-007, FR-012, BR-002, NFR-P-002

**Search Terms Used**:
- "data ingestion pipeline validation processing queue async government"
- "open data API publishing fuel price energy data REST government"
- "registration account management authentication OAuth API key government service"

---

#### Candidate: Dorset-Council-UK/FloodOnlineReportingTool.Public

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public |
| **Language** | C# (81.1%), HTML (17.8%) |
| **License** | MIT |
| **Last Activity** | Active (536 commits on main; 21 open issues) |
| **Stars** | 0 |
| **Contributors** | Dorset Council digital team |
| **Documentation** | Strong |

**Description**: A public-facing .NET web application enabling members of the public to report flooding to lead local flood authorities. The application follows a submission-and-processing pattern highly analogous to the Fuel Finder's retailer price submission flow: public users submit structured data through a web form; data is validated; an asynchronous processing pipeline handles downstream actions; the system uses message contracts (FloodOnlineReportingTool.Contracts) to decouple components; GOV.UK Design System components are used for the frontend; PostgreSQL with PostGIS handles geospatial data. The architectural pattern (web form, validation, async processing, notification via GOV.UK Notify, audit record) mirrors FR-002 and FR-007 requirements closely.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT. Fully compatible for study and adaptation |
| **Code Quality** | 4 | Tests directory present; GitHub Actions CI; 536 commits; CONTRIBUTING.md, SECURITY.md present; code of conduct included |
| **Documentation Quality** | 4 | Strong README with deployment options (IIS, Kestrel, Azure), PostgreSQL/PostGIS dependency documentation, contributing and security docs |
| **Tech Stack Alignment** | 2 | C# / .NET -- significant divergence if Fuel Finder uses Python or Node.js. Patterns are reusable but direct code reuse is not viable across language boundaries |
| **Activity / Maintenance** | 5 | 536 commits; 21 open issues being actively addressed; Entity Framework Core + PostgreSQL/PostGIS; actively developed |
| **Overall** | **4.0** | High on all axes except tech stack |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 5 person-days (studying the architectural patterns, message contract structure, async processing approach, and GOV.UK Design System integration saves design and research time for FR-002, FR-007)

**Key Considerations**:

- Direct code reuse requires adopting C# / .NET, which conflicts with the likely Python or Node.js stack
- The message contracts pattern (FloodOnlineReportingTool.Contracts -- C# interfaces for commands/events) is highly instructive for designing the Fuel Finder's async submission pipeline regardless of language
- PostgreSQL + PostGIS approach directly maps to the Fuel Finder's geospatial requirements for forecourt locations and proximity search
- Entity Framework Core data access patterns demonstrate government-grade data handling with audit capabilities
- Examine the `FloodOnlineReportingTool.Contracts` companion repository alongside this one -- it demonstrates the decoupled event contract pattern for FR-007

---

#### Candidate: BristolCityCouncil/send

| Attribute | Value |
|-----------|-------|
| **Organisation** | Bristol City Council |
| **Repository URL** | https://github.com/BristolCityCouncil/send |
| **Language** | Java (84.8%), Gherkin (12.4%) |
| **License** | Available (repository-level) |
| **Last Activity** | June 2022 (last commit) |
| **Stars** | 0 |
| **Contributors** | Bristol City Council digital team |
| **Documentation** | Comprehensive |

**Description**: SEND (Special Educational Needs) is a web application enabling school coordinators to submit structured funding applications to Bristol City Council. It implements an assessment workflow with data submission, validation, document uploads with ClamAV virus scanning, PDF export, and Azure Cosmos DB storage. The submission-review-approval pattern is architecturally analogous to the Fuel Finder's retailer registration and price submission review workflows. Uses Spring Boot, FreeMarker templates, Active Directory authentication, and Microsoft Graph API integration.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 4 | License present in repository; needs verification of specific terms |
| **Code Quality** | 3 | Gherkin BDD tests (12.4% of codebase); GitHub Actions CI; Maven-based build |
| **Documentation Quality** | 4 | Comprehensive README with setup instructions and architecture details |
| **Tech Stack Alignment** | 2 | Java / Spring Boot -- diverges from Python/Node.js. Azure Cosmos DB differs from PostgreSQL. Patterns are reusable |
| **Activity / Maintenance** | 2 | Last commit June 2022 -- nearly 4 years inactive. Effectively archived |
| **Overall** | **3.0** | |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 2 person-days (the assessment workflow pattern with virus scanning and document handling provides reference for retailer registration document upload requirements)

**Key Considerations**:

- Last active June 2022 -- treat as archived reference material only
- The BDD test approach (Gherkin) is a useful pattern for Fuel Finder acceptance testing regardless of language
- ClamAV virus scanning integration is relevant if the Fuel Finder accepts document uploads during registration
- Azure Cosmos DB usage diverges from the PostGIS/PostgreSQL approach; the Flood Tool is a better reference for geospatial data

---

### Capability 5: Geospatial Location Finder (Proximity Search)

**Requirements Addressed**: FR-004, INT-001, INT-002, NFR-P-001

**Search Terms Used**:
- "postcode geocoding location search proximity finder service"
- "GIS mapping geospatial framework interactive maps council government"

---

#### Candidate: east-sussex-county-council/Escc.Libraries.BranchFinder

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council |
| **Repository URL** | https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder |
| **Language** | C# (68.1%) |
| **License** | Open Government Licence v3 |
| **Last Activity** | December 2022 (last commit 6 December 2022) |
| **Stars** | 0 |
| **Contributors** | East Sussex County Council digital team |
| **Documentation** | Adequate |

**Description**: A 'Find your library' service for the East Sussex County Council website. Users enter a postcode; the service converts it to coordinates using a GOV.UK locate-API implementation; it queries an Umbraco content API for library branch locations and returns results sorted by distance. The architectural pattern -- postcode input, geocoding via external API, spatial proximity ranking, and results display -- is directly analogous to Fuel Finder FR-004 (citizen fuel price search).

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | OGL v3 -- optimal for UK government reuse. Free to copy, adapt, redistribute with attribution |
| **Code Quality** | 3 | Test project present (BranchFinder.Tests); no visible CI; ASP.NET MVC pattern; adequate but not modern |
| **Documentation Quality** | 3 | README covers configuration, dependencies, and setup. Assumes IIS knowledge; no deployment guide |
| **Tech Stack Alignment** | 2 | C# / ASP.NET MVC -- diverges from Python/Node.js stack. Patterns are adaptable but direct reuse not viable cross-language |
| **Activity / Maintenance** | 2 | Last commit December 2022 -- over 3 years ago. Effectively in maintenance mode |
| **Overall** | **3.0** | |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 3 person-days (the proximity search architecture and geocoding integration pattern are instructive; saves design research time for INT-002)

**Key Considerations**:

- The GOV.UK locate-api it integrates with may be deprecated -- verify currency before adopting the integration approach
- The interface abstraction for geocoding providers is a good pattern worth replicating regardless of language
- Consider using the Postcodes.io open API (free, covers UK postcodes, returns lat/lng and administrative geography) as an alternative geocoding provider
- Escc.RubbishAndRecycling.SiteFinder (also East Sussex, OGL v3, C#, December 2022) uses the same proximity-search pattern for additional reference

---

#### Candidate: Dorset-Council-UK/GIFramework-Maps

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/GIFramework-Maps |
| **Language** | TypeScript (42.7%), C# (37.6%), HTML (18.1%) |
| **License** | MIT (code); OGL v3 (documentation) |
| **Last Activity** | December 2025 (v1.10.0 released 22 December 2025) |
| **Stars** | 21 |
| **Contributors** | Active (Dorset Council GIS team; 12 forks) |
| **Documentation** | Excellent |

**Description**: A full-featured .NET + TypeScript web mapping application enabling organisations to create, share, and manage interactive maps using OpenLayers and Bootstrap. Features include spatial querying, GPS tracking, PDF exports, annotations, multiple search services, and Azure AD-protected administrative interface. Production-deployed by Dorset Council with 21 stars -- high for UK local government open source. For Fuel Finder, relevant as Reference for the citizen-facing map display component of FR-004, particularly the OpenLayers layer integration and postcode/text search patterns.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT for code; OGL v3 for docs. Both fully compatible |
| **Code Quality** | 4 | Dedicated test project (GIFrameworkMaps.Tests); CI/CD via GitHub Actions (development and production builds); 21 stars; 36 open issues; 202 commits |
| **Documentation Quality** | 5 | README, CONTRIBUTING.md, DEVELOPING.md, CODE_OF_CONDUCT.md, SECURITY.md; admin guide in separate repo (GIFramework-Maps-Admin-Guide) |
| **Tech Stack Alignment** | 3 | TypeScript frontend is adaptable; C# backend diverges. Can study TypeScript/OpenLayers patterns for citizen map display without adopting C# backend |
| **Activity / Maintenance** | 4 | v1.10.0 released December 2025; 36 open issues being addressed; 12 forks indicate community adoption; no open PRs suggests core team manages contributions |
| **Overall** | **4.2** | |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 4 person-days (TypeScript mapping patterns, spatial query design, GOV.UK-compatible UI integration approach, and admin interface patterns are directly applicable)

**Key Considerations**:

- The TypeScript frontend layer (using OpenLayers) can be studied for Fuel Finder map display without adopting the C# backend
- Uses Bootstrap rather than govuk-frontend for styling -- the Fuel Finder should use govuk-frontend instead
- Admin interface pattern (Azure AD protected configuration) is instructive for CMA enforcement dashboard auth
- The project's OGC web service integration is more complex than Fuel Finder needs -- the map display is simpler (show approximately 20 forecourt pins with prices)
- 36 open issues suggests active use and community engagement but also a maintenance backlog

---

### Capability 6: GOV.UK Design System Components (.NET/Blazor)

**Requirements Addressed**: NFR-U-001, NFR-U-002, INT-004

**Search Terms Used**:
- "GOV.UK Design System frontend components accessible government service"
- "GOV.UK frontend design system accessible WCAG components"

---

#### Candidate: Dorset-Council-UK/GdsBlazorComponents

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/GdsBlazorComponents |
| **Language** | HTML (45.1%), C# (41.1%) |
| **License** | MIT |
| **Last Activity** | March 2026 (v3.0.0 release, 20 March 2026) |
| **Stars** | 4 |
| **Contributors** | Dorset Council digital team |
| **Documentation** | Comprehensive |

**Description**: Reusable Blazor components styled using the GOV.UK Design System, enabling C# Blazor applications to use GDS-compliant UI components. Originally developed for the Flood Online Reporting Tool, now published for broader government reuse. Covers 28+ GDS components with individual documentation pages and a live demo website. Only relevant to Fuel Finder if the team adopts .NET Blazor -- otherwise superseded by alphagov/govuk-frontend.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT. Fully compatible |
| **Code Quality** | 3 | GitHub Actions CI present; v3.0.0 released March 2026; 4 stars and limited adoption outside Dorset Council |
| **Documentation Quality** | 5 | 28+ component docs; live demo website; setup instructions for Blazor Web App and WebAssembly variants |
| **Tech Stack Alignment** | 2 | Only relevant for .NET Blazor frontends -- significant divergence from JavaScript govuk-frontend approach |
| **Activity / Maintenance** | 5 | v3.0.0 March 2026; actively updated to track GOV.UK Design System version changes |
| **Overall** | **4.0** | |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 3 person-days (saves research into mapping GOV.UK Design System to .NET Blazor if that framework is chosen)

**Key Considerations**:

- Only adopt if Fuel Finder frontend uses .NET Blazor; for all other framework choices, use alphagov/govuk-frontend directly
- Maintained by a small Dorset Council team -- not a GDS-assured library; govuk-frontend remains the primary standard
- Verify that v3.0.0 maps to the current GOV.UK Design System version (5.x+)
- Reference candidate only because govuk-frontend is the authoritative source

---

### Capability 7: Open Data Publishing Pattern

**Requirements Addressed**: BR-005, FR-011, FR-013

**Search Terms Used**:
- "open data API publishing fuel price energy data REST government"
- "CKAN open data publishing API platform government portal dataset"
- "open data Scotland catalogue CKAN data portal publishing council"

---

#### Candidate: DundeeCityCouncil/open-data-scotland

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dundee City Council |
| **Repository URL** | https://github.com/DundeeCityCouncil/open-data-scotland |
| **Language** | Python (92.3%) |
| **License** | Available (LICENSE.md) |
| **Last Activity** | September 2015 (last commit) |
| **Stars** | 0 |
| **Contributors** | Dundee City Council |
| **Documentation** | Minimal |

**Description**: A curated index of Scottish data platforms that provide programmatic access to datasets through bulk downloads, APIs, or SPARQL endpoints. Maintains a CSV registry documenting external open data resources with inclusion criteria based on machine-readability and API availability. The catalogue approach (metadata-about-datasets rather than hosting datasets) provides a lightweight reference pattern for how the Fuel Finder's open data catalogue metadata could be structured, though the scale and complexity are far below what the Fuel Finder requires.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 4 | LICENSE.md present; specific terms to be verified |
| **Code Quality** | 2 | No tests; no CI; Makefile for build; minimal Python scripting |
| **Documentation Quality** | 2 | Basic README explaining inclusion criteria; no API docs or setup guide |
| **Tech Stack Alignment** | 3 | Python -- aligns with project if Python backend chosen; CSV catalogue is universal |
| **Activity / Maintenance** | 1 | Last commit September 2015 -- over 10 years inactive. Archived in practice |
| **Overall** | **2.4** | |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 1 person-day (the open data catalogue metadata schema and inclusion criteria provide a starting reference for how the Fuel Finder publishes its data catalogue entry on data.gov.uk)

**Key Considerations**:

- Over 10 years inactive -- treat as historical reference only
- The CSV catalogue structure demonstrates a minimal open data metadata schema
- The Fuel Finder's open data API (BR-005) is vastly more complex than this catalogue; this provides only the conceptual pattern, not implementation guidance
- For the Fuel Finder's open data publication, the primary reference should be the data.gov.uk publishing guidelines and DCAT metadata standards, not this repository
- DundeeCityCouncil/OpenData is a companion repo but similarly inactive and minimal

---

### Capability 8: Fuel Price Data Ingestion Pipeline

**Requirements Addressed**: FR-003, FR-007, BR-002, NFR-P-002, NFR-S-001, NFR-S-002

**Search Terms Used**:
- "data ingestion pipeline validation processing queue async government"
- "open data API publishing fuel price energy data REST government"
- "API rate limiting throttle middleware security government service"

**Outcome**: No suitable candidates found across all query variations.

No government repositories were identified that implement a fuel price or commodity price data ingestion pipeline with asynchronous processing, bulk API submission, idempotency handling, and data quality validation analogous to FR-003 and FR-007. The Flood Online Reporting Tool (Capability 4) provides partial architectural reference for the submission-and-processing pattern, but does not cover bulk API submission at scale (5,000 submissions/minute at peak -- NFR-P-002), idempotency logic, or real-time price data freshness monitoring.

The east-sussex-county-council/Escc.Services.Azure repository was investigated but found to be a narrow Azure email queuing utility (last commit 2014) with no relevance to data ingestion pipelines.

This capability is a genuine gap with no direct government code analogue in the indexed repositories.

---

### Capability 9: Compliance Monitoring Dashboard and Audit Trail

**Requirements Addressed**: FR-006, FR-010, BR-004, NFR-C-002, NFR-SEC-001, NFR-SEC-002

**Search Terms Used**:
- "compliance monitoring enforcement dashboard regulatory government"
- "audit trail logging immutable event store evidence government"
- "API rate limiting throttle middleware security government service"

**Outcome**: No suitable candidates found.

The search for compliance monitoring and audit trail implementations returned no repositories with enforcement dashboard functionality, tamper-evident audit logging, role-based access control for enforcement officers, or evidence preservation workflows analogous to FR-006 and FR-010. Only 2 results were returned for the compliance monitoring query (BracknellForestCouncil/government.github.com and Dorset-Council-UK/DorsetExplorer-Docs) -- neither relevant.

The audit trail search returned 4 results, none of which implement tamper-evident logging: Escc.Events.Website is an events listing site, Escc.Redmine.Sql is a Redmine SQL export, cloud-umbraco-cache-refresh is a CMS cache utility, and FloodOnlineReportingTool.Public (already assessed) provides basic audit recording but not cryptographic integrity verification.

This capability is a genuine gap -- no suitable government code reference was found for either compliance monitoring or tamper-evident audit logging.

---

## License Compatibility Matrix

| Repository | License | Commercial Use | Modification | Distribution | Attribution | Compatible |
|------------|---------|---------------|--------------|--------------|-------------|------------|
| alphagov/govuk-frontend | MIT (Crown Copyright) | Yes | Yes | Yes | Required | Yes |
| alphagov/notifications-python-client | MIT (Crown Copyright) | Yes | Yes | Yes | Required | Yes |
| alphagov/notifications-node-client | MIT | Yes | Yes | Yes | Required | Yes |
| alphagov/govuk-prototype-kit | MIT | Yes | Yes | Yes | Required | Yes |
| Dorset-Council-UK/FloodOnlineReportingTool.Public | MIT | Yes | Yes | Yes | Required | Yes |
| Dorset-Council-UK/GIFramework-Maps | MIT (code) / OGL v3 (docs) | Yes | Yes | Yes | Required | Yes |
| Dorset-Council-UK/GdsBlazorComponents | MIT | Yes | Yes | Yes | Required | Yes |
| east-sussex-county-council/Escc.Libraries.BranchFinder | OGL v3 | Yes | Yes | Yes | Required | Yes |
| BristolCityCouncil/send | Available (verify) | Likely | Likely | Likely | Likely | Verify |
| DundeeCityCouncil/open-data-scotland | Available (verify) | Likely | Likely | Likely | Likely | Verify |

**Notes**: All primary candidates carry fully compatible licenses for UK government reuse. MIT and OGL v3 are the dominant licenses in this set. No GPL or proprietary licenses were encountered in the core shortlisted candidates. Crown Copyright applies to the alphagov repositories -- UK Government is the copyright holder, which is directly compatible with a CMA/DESNZ-owned service. Attribution requirements for MIT and OGL v3 are satisfied by maintaining license files in any forked or derived codebase. The Bristol City Council and Dundee City Council repositories have license files present but specific terms should be verified before any code adoption.

---

## Tech Stack Alignment

| Repository | Language | Framework | Infrastructure | Aligns With Project | Adaptation Needed |
|------------|----------|-----------|----------------|---------------------|-------------------|
| alphagov/govuk-frontend | JavaScript / SCSS | None (vanilla) | npm package | Yes -- any modern web stack | Install as npm dependency; configure SCSS build pipeline |
| alphagov/notifications-python-client | Python | None (API client) | PyPI package | Yes -- if Python backend | Install via pip; wrap with retry/dead-letter logic |
| alphagov/notifications-node-client | JavaScript | None (API client) | npm package | Yes -- if Node.js backend | Install via npm; alternative to Python client |
| alphagov/govuk-prototype-kit | JavaScript | Nunjucks | Node.js | Yes -- prototyping tool | Install; create prototype routes and pages |
| Dorset-Council-UK/FloodOnlineReportingTool.Public | C# | ASP.NET Core + EF Core | IIS / Kestrel / Azure / PostgreSQL | Partial -- patterns reusable | Significant: full language translation for direct reuse |
| Dorset-Council-UK/GIFramework-Maps | TypeScript + C# | ASP.NET Core + OpenLayers | Azure | Partial -- TypeScript layer adaptable | Extract TypeScript mapping patterns; discard C# backend |
| Dorset-Council-UK/GdsBlazorComponents | C# | Blazor | .NET | No -- only if Blazor chosen | Full stack change required for direct adoption |
| east-sussex-county-council/Escc.Libraries.BranchFinder | C# | ASP.NET MVC | IIS | No | Full language translation required |
| BristolCityCouncil/send | Java | Spring Boot | Azure Cosmos DB | No | Full language and database translation required |
| DundeeCityCouncil/open-data-scotland | Python | None (scripts) | None | Partial -- Python aligns | Minimal code; conceptual reference only |

**Project Tech Stack**: The Fuel Finder's technology stack has not yet been formally decided (Alpha phase). Based on ARC-001-REQ-v2.0 and TCoP compliance (Point 3 -- open source, Point 5 -- cloud first), the most likely stack is: Python (Django or FastAPI) or Node.js (Express/Fastify) for the backend API; govuk-frontend (JavaScript) for the citizen-facing UI; PostgreSQL + PostGIS for geospatial data; a managed message queue (AWS SQS, Azure Service Bus) for async pipeline; deployed to AWS UK or Azure UK regions. All alphagov library candidates align directly. The C#/.NET candidates from Dorset Council and East Sussex CC are reference-only given this likely stack direction. The Java candidate from Bristol City Council is similarly reference-only.

---

## Gap Analysis

| Capability | Status | Notes | Recommended Action |
|------------|--------|-------|--------------------|
| Citizen-facing UI / Design System | Reusable | alphagov/govuk-frontend -- mandatory Library adoption | Adopt as npm dependency immediately |
| GOV.UK Notify integration | Reusable | alphagov/notifications-python-client or notifications-node-client | Adopt matching client for chosen backend language |
| Rapid prototyping | Reusable | alphagov/govuk-prototype-kit -- mandatory for Alpha phase | Adopt as prototyping tool for user research |
| Online data submission pattern | Partial | FloodOnlineReportingTool.Public provides Reference architecture; C# stack diverges | Study patterns; build in project language |
| Geospatial proximity search | Partial | Escc.Libraries.BranchFinder and GIFramework-Maps provide Reference patterns; outdated or C# stack | Study patterns; consider Postcodes.io as geocoding provider |
| Open data publishing pattern | Partial | DundeeCityCouncil/open-data-scotland is minimal and inactive; conceptual reference only | Use data.gov.uk publishing guidelines; build open data API from scratch |
| Fuel price data ingestion pipeline | No match | No government code found after 4 query variations -- genuine gap | Build from scratch; consider contributing back under OGL |
| Compliance monitoring dashboard | No match | No government code found after 3 query variations -- genuine gap | Build from scratch; reuse GOV.UK Design System for UI |
| Audit trail / tamper-evident logging | No match | No government code found after 3 query variations -- genuine gap | Build from scratch; use append-only cloud storage with integrity hashing |

**Legend**: Reusable | Partial | No match

---

## Recommendations

### Reuse Strategy Summary

The highest-priority reuse actions are both mandatory and straightforward: alphagov/govuk-frontend, the GOV.UK Notify client libraries, and alphagov/govuk-prototype-kit must be adopted -- they are the canonical government-provided implementations for their respective functions, they carry permissive MIT licenses, and they are directly mandated or recommended by TCoP Principle 13 (Reuse Government Platforms) and Architecture Principle 13 from ARC-000-PRIN-v1.0. These are Library adoptions (install as dependencies), not Fork candidates. Adopting govuk-frontend eliminates approximately 25 person-days of UI component development and ensures WCAG 2.2 AA compliance is built-in rather than retrofitted. Adopting the Notify client eliminates the need to build a custom Notify HTTP integration layer. The Prototype Kit (new in this v2.0 assessment) saves an estimated 10 person-days during Alpha by providing immediate access to GOV.UK-styled interactive prototypes for user research, and its use is expected by GDS assessment teams.

Beyond the mandatory library adoptions, the Dorset Council repositories (FloodOnlineReportingTool.Public and GIFramework-Maps) remain the most valuable Reference candidates in the govreposcrape index for this project domain. Both are actively maintained, MIT-licensed, and structurally relevant: the Flood Tool demonstrates the async data submission, message contracting, and GOV.UK Notify integration pattern in a government context; GIFramework-Maps demonstrates geospatial data display and search in a .NET + TypeScript stack with excellent documentation. Neither is a Fork candidate because the C# backend language diverges too significantly from the Fuel Finder's likely Python or Node.js stack. The Bristol City Council SEND application provides additional reference for structured assessment workflows with BDD testing patterns, though its June 2022 last commit limits its currency. Developers should allocate time to studying these codebases during the Alpha phase architecture spike.

Three capabilities -- fuel price data ingestion pipeline, compliance monitoring dashboard, and tamper-evident audit trail -- have no government code precedent in the indexed repositories. This was confirmed through expanded search queries in v2.0 (10 query variations versus 7 in v1.0) and remains a genuine gap. Real-time commodity price ingestion at regulatory scale is a novel UK government problem, and enforcement dashboard tooling tends to be built bespoke per regulatory context. These should be built from scratch during Beta, following the architectural principles established in ARC-000-PRIN-v1.0 (asynchronous pipeline, zero-trust security, audit-by-default). The CMA/DESNZ team should plan to publish the resulting implementations under OGL v3 to enable cross-government reuse -- this would fulfil TCoP Point 8 (Share, reuse and collaborate) and GDS Service Standard Point 12 (Make new source code open).

### Implementation Priority

| Priority | Repository | Capability | Action | Estimated Effort | Timeline |
|----------|------------|------------|--------|-----------------|----------|
| 1 | alphagov/govuk-prototype-kit | Rapid prototyping | Install; build prototype journeys for UC-1, UC-2, UC-6 | 2 days setup + ongoing | Alpha Sprint 1 |
| 2 | alphagov/govuk-frontend | Citizen UI / Design System | Install as npm dependency; configure SCSS pipeline | 2 days setup | Alpha Sprint 1 |
| 3 | alphagov/notifications-python-client (or node-client) | GOV.UK Notify integration | Install via pip/npm; build retry wrapper and DLQ | 3 days setup + testing | Alpha Sprint 2 |
| 4 | Dorset-Council-UK/FloodOnlineReportingTool.Public | Async submission pattern | Study architecture; extract async pipeline design | 3 days research | Alpha architecture spike |
| 5 | Dorset-Council-UK/GIFramework-Maps | Geospatial map display | Study TypeScript/OpenLayers mapping patterns; adapt for FR-004 | 2 days research | Alpha architecture spike |
| 6 | east-sussex-county-council/Escc.Libraries.BranchFinder | Proximity search | Study postcode geocoding pattern; evaluate Postcodes.io | 1 day research | Alpha architecture spike |
| 7 | -- | Fuel price ingestion pipeline | Build from scratch; async queue + validator + publisher | 45 days | Beta Sprint 1-6 |
| 8 | -- | Compliance monitoring dashboard | Build from scratch; RBAC + GOV.UK Frontend | 30 days | Beta Sprint 4-8 |
| 9 | -- | Audit trail and evidence store | Build from scratch; append-only + cryptographic integrity | 15 days | Beta Sprint 2-4 |

### Risk Considerations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| govuk-frontend major version upgrade during development breaks existing UI | Medium | Medium | Pin to specific version in package.json; schedule upgrade sprints; follow GDS release notes |
| GOV.UK Notify client library lags behind Notify API changes | Low | Low | Library actively maintained by GDS; monitor repo; fallback to direct HTTP if needed |
| FloodOnlineReportingTool C#/.NET patterns require significant translation effort to Python/Node.js | Medium | Low | Reference patterns only -- design time, not code time; budget 1 day per pattern studied |
| GIFramework-Maps TypeScript patterns require OpenLayers or specialist mapping knowledge | Medium | Medium | Allocate a developer with TypeScript + mapping experience to Alpha architecture spike |
| No government precedent for fuel price ingestion pipeline creates higher design risk | High | High | Invest in dedicated Alpha technical spike (2 weeks); prototype async pipeline before Beta; engage NCSC/GDS for peer review |
| Escc.Libraries.BranchFinder depends on deprecated GOV.UK locate-API | High | Low | Impact is low -- Reference use only; validate geocoding approach against Postcodes.io |
| govuk-prototype-kit prototypes mistaken for production service | Low | Medium | Password-protect all published prototypes; add clear "This is a prototype" banners; follow GDS guidance |
| Bristol SEND and Dundee open-data-scotland repos are effectively archived (2022/2015) | High | Low | Treat as historical reference only; do not depend on updates; verify any patterns against current best practice |

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-001-REQ-v2.0 | Requirements Baseline | Project 001 | Capability areas, requirements IDs, use cases | projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md |
| ARC-000-PRIN-v1.0 | Architecture Principles | Project 000 | Principle 13 (Reuse Government Platforms) | projects/000-global/ |
| GOV.UK Design System | Documentation | GDS | Component patterns, accessibility guidance | https://design-system.service.gov.uk/ |
| GOV.UK Notify Documentation | API Documentation | GDS | Python/Node.js client integration guides | https://docs.notifications.service.gov.uk/ |
| GOV.UK Prototype Kit Documentation | Documentation | GDS | Prototyping setup and usage guides | https://prototype-kit.service.gov.uk/ |
| Technology Code of Practice | Governance | CDDO | Point 2 (Design System), Point 8 (Share), Point 13 (Reuse) | https://www.gov.uk/guidance/the-technology-code-of-practice |
| ARC-001-GOVR-v1.0 | Previous Version | Project 001 | Superseded by this document | projects/001-uk-fuel-price-transparency-service/research/ARC-001-GOVR-v1.0.md |

---

**Generated by**: ArcKit `/arckit.gov-reuse` agent
**Generated on**: 2026-03-24
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: claude-opus-4-6
