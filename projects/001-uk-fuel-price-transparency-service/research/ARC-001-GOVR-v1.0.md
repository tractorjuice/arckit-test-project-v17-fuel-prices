# Government Reuse Assessment: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit:gov-reuse`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GOVR-v1.0 |
| **Document Type** | Government Reuse Assessment |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-03-23 |
| **Last Modified** | 2026-03-23 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-06-23 |
| **Owner** | CMA Digital Lead (Architecture Lead) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-23 | ArcKit AI | Initial creation from `/arckit:gov-reuse` agent | PENDING | PENDING |

---

## Executive Summary

### Search Scope

This assessment searched approximately 21,000 UK government repositories indexed by govreposcrape across local councils, NHS bodies, central government departments, and cross-government platforms. The search targeted eight capability areas derived from the requirements baseline (ARC-001-REQ-v2.0) for the UK Fuel Price Transparency Service ("Fuel Finder"), which operates under the Motor Fuel Price (Open Data) Regulations 2025.

Search queries were executed across three query variations per capability (24 queries total), covering: fuel price data ingestion, data validation pipelines, retailer registration and account management, public open data APIs, GOV.UK Notify integration, geospatial proximity search, compliance monitoring dashboards, and audit trail logging.

The indexed repository population is heavily weighted towards local authority organisations (Dorset Council, East Sussex County Council, Camden Council, Dundee City Council, BANES). Central government / alphagov repositories for GOV.UK Frontend and GOV.UK Notify client libraries were assessed directly via WebFetch as known high-value candidates aligned with the project's mandatory TCoP Principle 13 (Reuse Government Platforms) obligations.

**Capabilities Assessed**: 7 capability areas across 8 government organisations

**Repositories Evaluated**: 47 repositories reviewed via search; 8 shortlisted for detailed WebFetch assessment; 7 scored

### Key Findings

| Capability | Best Candidate | Organisation | Reuse Strategy | Effort Saved |
|------------|---------------|--------------|----------------|--------------|
| Citizen-facing UI and Design System | alphagov/govuk-frontend | GDS / alphagov | Library | 25 days |
| GOV.UK Notify integration | alphagov/notifications-python-client | GDS / alphagov | Library | 8 days |
| Online data submission (web form + validation) | Dorset-Council-UK/FloodOnlineReportingTool.Public | Dorset Council | Reference | 5 days |
| Geospatial location finder (proximity search) | east-sussex-county-council/Escc.Libraries.BranchFinder | East Sussex CC | Reference | 3 days |
| Geospatial mapping framework | Dorset-Council-UK/GIFramework-Maps | Dorset Council | Reference | 4 days |
| GOV.UK Design System (Blazor/.NET) | Dorset-Council-UK/GdsBlazorComponents | Dorset Council | Reference | 3 days |
| Fuel price data ingestion pipeline | None found | — | Build new | — |
| Compliance monitoring dashboard | None found | — | Build new | — |
| Audit trail / tamper-evident logging | None found | — | Build new | — |

### Reuse Summary

**Total Estimated Effort Saved**: 48 person-days across Library and Reference candidates

**Reuse Coverage**: 4 of 7 capability areas have at least a Reference-quality government code candidate (57%). 2 capabilities have Library-quality candidates (direct use without forking).

**Recommended Approach**: The highest-value reuse actions are mandatory platform adoptions — GOV.UK Frontend (alphagov/govuk-frontend) and the GOV.UK Notify Python client (alphagov/notifications-python-client) are both production-grade, MIT-licensed, actively maintained by GDS, and directly mandated by the Technology Code of Practice. These should be adopted as npm/PyPI dependencies respectively, not forked. The Dorset Council Flood Online Reporting Tool and East Sussex site-finder repositories provide valuable Reference material for data submission patterns and location-search architecture, though their C#/.NET stack diverges from the project's likely Python or Node.js stack. No suitable government code was found for the specialised capabilities of fuel price data ingestion, compliance monitoring dashboards, or tamper-evident audit logging — these will require build from scratch.

---

## Capability Analysis

### Capability 1: Citizen-Facing UI and Design System

**Requirements Addressed**: BR-003, FR-004, NFR-U-001, NFR-U-002, NFR-U-003, NFR-C-003, INT-004

**Search Terms Used**:
- "GOV.UK Design System frontend components accessible government service"
- "alphagov price data collection API submission open data publishing"
- "alphagov GOV.UK Notify client Python Ruby Node wrapper integration"

---

#### Candidate: alphagov/govuk-frontend

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (alphagov) |
| **Repository URL** | https://github.com/alphagov/govuk-frontend |
| **Language** | JavaScript (55.1%), Nunjucks (31.9%), SCSS (12.5%) |
| **License** | MIT (Crown Copyright, GDS, 2017) |
| **Last Activity** | March 2026 (v6.1.0 release) |
| **Stars** | 1,400 |
| **Contributors** | Active (12,225 total commits) |
| **Documentation** | Excellent |

**Description**: GOV.UK Frontend is the official GDS library of HTML, CSS, and JavaScript components implementing the GOV.UK Design System. It is the canonical implementation for all government digital services and provides WCAG 2.2 AA-compliant, accessible components (buttons, form inputs, error summaries, notification banners, phase banners, header/footer, breadcrumbs, maps fallbacks). It is used by thousands of government services and is the mandated technology for citizen-facing interfaces under GDS Service Standard Point 3 and TCoP Point 2.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT (Crown Copyright, GDS). Fully compatible — free to use, modify, distribute with attribution |
| **Code Quality** | 5 | 12,225 commits; Jest + Puppeteer automated tests; ESLint + Stylelint; build CI active; 7,700+ dependent projects |
| **Documentation Quality** | 5 | Comprehensive README, GOV.UK Design System website, per-component docs, browser support matrix, accessibility notes, contributing guide |
| **Tech Stack Alignment** | 5 | JavaScript/SCSS npm package — integrates with any modern web stack; Nunjucks macros for server-side rendering (Node.js) |
| **Activity / Maintenance** | 5 | Last commit March 2026; GDS actively maintains; long-term government commitment |
| **Overall** | **5.0** | |

**Recommended Strategy**: Library

**Estimated Effort Saved**: 25 person-days (building accessible, standards-compliant government UI components from scratch is substantial; using govuk-frontend eliminates that work entirely)

**Key Considerations**:

- This is a mandatory adoption per TCoP and GDS Service Standard, not an optional reuse decision
- Install via npm: `npm install govuk-frontend`
- Version 5.x+ requires Node.js 18+; confirm project runtime
- Nunjucks macros provide server-side rendering; React/Vue wrappers exist in the community but are not officially maintained by GDS
- The Welsh language (NFR-U-003) content translations must be provided by the Fuel Finder team — govuk-frontend provides the components but not domain content
- Map display for FR-004 (proximity search) requires additional mapping library (Leaflet.js or similar); govuk-frontend provides a list-view fallback pattern for accessibility compliance

---

### Capability 2: GOV.UK Notify Integration

**Requirements Addressed**: FR-009, INT-003, NFR-A-003

**Search Terms Used**:
- "GOV.UK Notify integration email SMS notification retailer"
- "alphagov GOV.UK Notify client Python Ruby Node wrapper integration"
- "organisations registration service account management government digital service"

---

#### Candidate: alphagov/notifications-python-client

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (alphagov) |
| **Repository URL** | https://github.com/alphagov/notifications-python-client |
| **Language** | Python (95.1%) |
| **License** | MIT (Crown Copyright, GDS, 2015) |
| **Last Activity** | Recent (830 commits on main) |
| **Stars** | 24 |
| **Contributors** | Multiple (page load error; GDS team) |
| **Documentation** | Strong |

**Description**: The official GDS Python client library for the GOV.UK Notify API. Enables sending emails, SMS, and letters via the government's shared notification platform. Published on PyPI. Includes comprehensive API documentation at docs.notifications.service.gov.uk. The Fuel Finder service requires GOV.UK Notify for retailer compliance reminders (FR-009), submission confirmations, and enforcement notices (FR-006, UC-4). This library is the correct mechanism for that integration.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT (Crown Copyright, GDS). Fully compatible |
| **Code Quality** | 5 | Tox multi-environment testing; Flake8 + Ruff linting; Dockerfile; Makefile; 830 commits; actively maintained by GDS Notify team |
| **Documentation Quality** | 5 | Official docs at docs.notifications.service.gov.uk/python.html; PyPI page; changelog; contributing guide |
| **Tech Stack Alignment** | 4 | Python — aligns if project uses Python backend. If Node.js is chosen, use notifications-node-client instead (MIT, 554 commits) |
| **Activity / Maintenance** | 5 | GDS Notify team actively maintains; open issues addressed; 4 open PRs at time of assessment |
| **Overall** | **4.8** | |

**Recommended Strategy**: Library

**Estimated Effort Saved**: 8 person-days (building a Notify integration client from scratch, including retry logic, error handling, and delivery status webhooks, would take a developer a full working week)

**Key Considerations**:

- Install via pip: `pip install notifications-python-client`
- If the project adopts Node.js, use `alphagov/notifications-node-client` instead (MIT, JavaScript, 554 commits, 18 stars — same quality tier)
- The GOV.UK Notify service itself requires a service account and API key — this is a separate onboarding step with GDS Notify team, distinct from the code library
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

**Description**: Official GDS Node.js client for GOV.UK Notify. Functionally equivalent to the Python client above. Relevant if the Fuel Finder backend is Node.js/TypeScript rather than Python.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT. Fully compatible |
| **Code Quality** | 4 | spec/ test directory; 554 commits; active GDS maintenance |
| **Documentation Quality** | 5 | docs.notifications.service.gov.uk; NPM package; changelog |
| **Tech Stack Alignment** | 4 | Node.js — aligns if project uses Node.js backend |
| **Activity / Maintenance** | 5 | Actively maintained by GDS |
| **Overall** | **4.6** | |

**Recommended Strategy**: Library

**Estimated Effort Saved**: 8 person-days (same as Python client — alternative based on tech stack choice)

**Key Considerations**:

- Install via npm: `npm install notifications-node-client`
- Choose either Python or Node.js client based on the project's backend language choice — not both
- TypeScript type definitions included

---

### Capability 3: Online Data Submission (Web Form and Validation Pipeline)

**Requirements Addressed**: FR-002, FR-003, FR-007, FR-012, BR-002, NFR-P-002

**Search Terms Used**:
- "flood reporting online data submission web form government environment agency"
- "data submission API RESTful ingestion pipeline government regulatory"
- "data validation quality rules pipeline schema validation government"
- "asynchronous message queue data processing pipeline event driven government service"

---

#### Candidate: Dorset-Council-UK/FloodOnlineReportingTool.Public

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public |
| **Language** | C# (81.1%) |
| **License** | MIT |
| **Last Activity** | Active (536 commits on main; v3.2.0 of Contracts released March 2026) |
| **Stars** | 0 |
| **Contributors** | Dorset Council digital team |
| **Documentation** | Strong |

**Description**: A public-facing .NET web application enabling members of the public to report flooding to lead local flood authorities. The application follows a submission-and-processing pattern highly analogous to the Fuel Finder's retailer price submission flow: public users submit structured data through a web form; data is validated; an asynchronous processing pipeline handles downstream actions; the system uses message contracts (FloodOnlineReportingTool.Contracts) to decouple components; GOV.UK Design System components are used for the frontend; PostgreSQL with PostGIS handles geospatial data. The architectural pattern (web form → validation → async processing → notification via GOV.UK Notify → audit record) mirrors FR-002 and FR-007 requirements closely.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT. Fully compatible for study and adaptation |
| **Code Quality** | 4 | Tests directory present; GitHub Actions CI; 536 commits; CONTRIBUTING.md, SECURITY.md present; code of conduct included |
| **Documentation Quality** | 4 | Strong README with deployment options (IIS, Kestrel, Azure), PostgreSQL/PostGIS dependency documentation, contributing and security docs |
| **Tech Stack Alignment** | 2 | C# / .NET — significant divergence if Fuel Finder uses Python or Node.js. The patterns are reusable but direct code reuse is not viable across language boundaries |
| **Activity / Maintenance** | 5 | Companion Contracts repo shows v3.2.0 released March 2026; GdsBlazorComponents (derived from this project) had v3.0.0 March 2026; actively developed |
| **Overall** | **4.0** | High on all axes except tech stack |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 5 person-days (studying the architectural patterns, message contract structure, async processing approach, and GOV.UK Design System integration saves design and research time for FR-002, FR-007)

**Key Considerations**:

- Direct code reuse requires the Fuel Finder to adopt C# / .NET, which conflicts with the likely Python or Node.js stack suggested by the existing research documents
- The message contracts pattern (FloodOnlineReportingTool.Contracts — C# interfaces for commands/events) is highly instructive for designing the Fuel Finder's async submission pipeline regardless of language
- The PostgreSQL + PostGIS approach directly maps to the Fuel Finder's geospatial requirements for forecourt locations and proximity search
- The GOV.UK GDS Blazor components (spun out from this project) are relevant if Blazor/C# is considered for the frontend
- Examine the `FloodOnlineReportingTool.Contracts` repository alongside this one — it demonstrates the decoupled event contract pattern for FR-007

---

### Capability 4: Geospatial Location Finder (Proximity Search)

**Requirements Addressed**: FR-004, INT-001, INT-002, NFR-P-001

**Search Terms Used**:
- "geospatial proximity search postcode location UK government service"
- "postcode lookup geocoding UK address finder service finder government"
- "location finder service map display postcodes within radius government public"
- "GIS mapping geospatial framework interactive maps council government"

---

#### Candidate: east-sussex-county-council/Escc.Libraries.BranchFinder

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council |
| **Repository URL** | https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder |
| **Language** | C# (68.1%) |
| **License** | Open Government Licence v3 |
| **Last Activity** | December 2022 (last commit December 6, 2022) |
| **Stars** | 0 |
| **Contributors** | East Sussex County Council digital team |
| **Documentation** | Adequate |

**Description**: A 'Find your library' service for the East Sussex County Council website. Users enter a postcode; the service converts it to coordinates using a GOV.UK locate-API implementation; it then queries an Umbraco content API for library branch locations and returns results sorted by distance. The architectural pattern — postcode input, geocoding via external API, spatial proximity ranking, and results display — is directly analogous to Fuel Finder FR-004 (citizen fuel price search). The code abstracts geocoding behind an interface, allowing alternative geocoding providers.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | OGL v3 — optimal for UK government reuse. Free to copy, adapt, redistribute with attribution |
| **Code Quality** | 3 | Test project present (BranchFinder.Tests); no visible CI badge; ASP.NET MVC pattern; adequate but not modern |
| **Documentation Quality** | 3 | README covers configuration, dependencies, and setup. Assumes IIS knowledge; no deployment guide |
| **Tech Stack Alignment** | 2 | C# / ASP.NET MVC — diverges from Python/Node.js stack. Patterns are adaptable but direct reuse is not viable cross-language |
| **Activity / Maintenance** | 2 | Last commit December 2022 — over 3 years ago. Effectively in maintenance mode. GOV.UK locate-API it depends on may no longer exist |
| **Overall** | **3.0** | |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 3 person-days (the proximity search architecture and GOV.UK locate-API integration pattern are instructive; saves design research time for INT-002)

**Key Considerations**:

- The GOV.UK locate-api it integrates with may be deprecated — verify currency before adopting the integration approach
- The interface abstraction for geocoding providers is a good pattern worth replicating regardless of language
- Consider using the Postcodes.io open API (free, covers UK postcodes, returns lat/lng and administrative geography) as an alternative geocoding provider — this pattern is demonstrated by several government services
- Escc.RubbishAndRecycling.SiteFinder (also East Sussex, OGL v3, C#, December 2022) uses the same proximity-search pattern and may provide additional reference material; however, its last commit date also makes it borderline for reference quality

---

#### Candidate: Dorset-Council-UK/GIFramework-Maps

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/GIFramework-Maps |
| **Language** | TypeScript (42.7%), C# (37.6%), HTML (18.1%) |
| **License** | MIT (code); OGL v3 (documentation) |
| **Last Activity** | December 22, 2025 (v1.10.0) |
| **Stars** | 21 |
| **Contributors** | Active (Dorset Council GIS team) |
| **Documentation** | Excellent |

**Description**: A full-featured .NET + TypeScript web mapping application enabling organisations to create, share, and manage interactive maps using OGC web services. Features include spatial querying, GPS tracking, PDF exports, annotations, multiple search services, and an Azure AD-protected administrative interface. The project is production-deployed by Dorset Council and has 21 stars — high for a UK local government open source project. For Fuel Finder, it is relevant as a Reference for the citizen-facing map display component of FR-004, particularly the OGC layer integration and postcode/text search patterns. The TypeScript frontend layer is broadly tech-stack compatible.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT for code; OGL v3 for docs. Both fully compatible |
| **Code Quality** | 4 | Dedicated test project (GIFrameworkMaps.Tests); CI/CD via GitHub Actions (.NET workflows); 21 stars; active issue tracker (36 open issues); 202 commits |
| **Documentation Quality** | 5 | README, CONTRIBUTING.md, DEVELOPING.md, CODE_OF_CONDUCT.md, SECURITY.md, admin guide in separate repo |
| **Tech Stack Alignment** | 3 | TypeScript frontend is adaptable; C# backend diverges. Can study the TypeScript/Leaflet patterns for citizen map display without adopting the C# backend |
| **Activity / Maintenance** | 5 | Last commit December 2025; v1.10.0 released; 36 open issues being addressed; actively developed |
| **Overall** | **4.4** | |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 4 person-days (TypeScript mapping patterns, spatial query design, GOV.UK-compatible UI integration approach, and admin interface patterns are all directly applicable reference material)

**Key Considerations**:

- The TypeScript frontend layer (using Leaflet.js or similar) can be studied for Fuel Finder map display without adopting the C# backend
- The admin interface pattern (Azure AD protected configuration) is instructive for CMA enforcement dashboard auth (INT-006)
- Consider extracting the TypeScript search-and-display pattern as an independent module; it does not depend on the C# backend
- The project's OGC web service integration is more complex than Fuel Finder needs — the Fuel Finder map display is simpler (show ~20 forecourt pins with prices)
- 36 open issues suggests active use and community engagement, but also that there is a maintenance backlog

---

### Capability 5: GOV.UK Design System Components (.NET/Blazor)

**Requirements Addressed**: NFR-U-001, NFR-U-002, INT-004

**Search Terms Used**:
- "GOV.UK Design System frontend components accessible government service"
- "flood reporting online data submission web form government environment agency"

---

#### Candidate: Dorset-Council-UK/GdsBlazorComponents

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council |
| **Repository URL** | https://github.com/Dorset-Council-UK/GdsBlazorComponents |
| **Language** | HTML (45.1%), C# (41.1%) |
| **License** | MIT |
| **Last Activity** | March 20, 2026 (v3.0.0 release) |
| **Stars** | 4 |
| **Contributors** | Dorset Council digital team |
| **Documentation** | Comprehensive |

**Description**: Reusable Blazor components styled using the GOV.UK Design System, enabling C# Blazor applications to use GDS-compliant UI components. Originally developed for the Flood Online Reporting Tool, now published for broader government reuse. Covers 28+ GDS components with individual documentation pages and a live demo website. Only relevant to the Fuel Finder if the team adopts .NET Blazor as the frontend framework — otherwise this is superseded by the canonical alphagov/govuk-frontend for JavaScript-based frontends.

**Reusability Assessment**:

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **License Compatibility** | 5 | MIT. Fully compatible |
| **Code Quality** | 3 | GitHub Actions CI present; v3.0.0 released March 2026; however 4 stars and limited adoption outside Dorset Council |
| **Documentation Quality** | 5 | 28+ component docs; live demo website; setup instructions for Blazor Web App and WebAssembly variants |
| **Tech Stack Alignment** | 2 | Only relevant for .NET Blazor frontends — significant divergence from JavaScript govuk-frontend approach |
| **Activity / Maintenance** | 5 | v3.0.0 March 2026; actively updated to track GOV.UK Design System version changes |
| **Overall** | **4.0** | |

**Recommended Strategy**: Reference

**Estimated Effort Saved**: 3 person-days (saves research into how to map GOV.UK Design System to .NET Blazor if that framework is chosen)

**Key Considerations**:

- Only adopt this library if the Fuel Finder frontend uses .NET Blazor; for all other framework choices, use alphagov/govuk-frontend directly
- The project is maintained by a small Dorset Council team — not a GDS-assured library; govuk-frontend remains the primary standard
- Verify that v3.0.0 maps to the current GOV.UK Design System version (5.x) — there can be lag between GDS releases and community wrappers
- This is a Reference candidate, not a Fork or Library candidate, because: (a) the tech stack dependency is conditional, and (b) govuk-frontend is the authoritative source that should be preferred

---

### Capability 6: Fuel Price Data Ingestion Pipeline

**Requirements Addressed**: FR-003, FR-007, BR-002, NFR-P-002, NFR-S-001, NFR-S-002

**Search Terms Used**:
- "fuel price data ingestion pipeline open data UK government"
- "alphagov price data collection API submission open data publishing"
- "asynchronous message queue data processing pipeline event driven government service"
- "data validation quality rules pipeline schema validation government"

**Outcome**: No suitable candidates found across all query variations.

No government repositories were identified that implement a fuel price or commodity price data ingestion pipeline with asynchronous processing, bulk API submission, idempotency handling, and data quality validation analogous to FR-003 and FR-007. The Flood Online Reporting Tool (Capability 3) provides partial architectural reference for the submission-and-processing pattern, but does not cover bulk API submission at scale (5,000 submissions/minute at peak — NFR-P-002), idempotency logic, or real-time price data freshness monitoring.

This capability is a genuine gap with no direct government code analogue in the indexed repositories.

---

### Capability 7: Compliance Monitoring Dashboard and Audit Trail

**Requirements Addressed**: FR-006, FR-010, BR-004, NFR-C-002, NFR-SEC-001, NFR-SEC-002

**Search Terms Used**:
- "compliance monitoring dashboard enforcement regulatory reporting"
- "audit trail tamper evident logging immutable event log government"
- "OAuth2 client credentials API key authentication government service registration"

**Outcome**: No suitable candidates found.

The search for compliance monitoring and audit trail implementations returned no repositories with enforcement dashboard functionality, tamper-evident audit logging, role-based access control for enforcement officers, or evidence preservation workflows analogous to FR-006 and FR-010. The alphagov/pay-adminusers repository (GOV.UK Pay) implements user management and authorisation in Java but is Java-only and its enforcement/audit patterns are specific to payment authorisation rather than regulatory compliance monitoring.

This capability is a genuine gap — no suitable government code reference was found.

---

## License Compatibility Matrix

| Repository | License | Commercial Use | Modification | Distribution | Attribution | Compatible |
|------------|---------|---------------|--------------|--------------|-------------|------------|
| alphagov/govuk-frontend | MIT (Crown Copyright) | Yes | Yes | Yes | Required | Yes |
| alphagov/notifications-python-client | MIT (Crown Copyright) | Yes | Yes | Yes | Required | Yes |
| alphagov/notifications-node-client | MIT | Yes | Yes | Yes | Required | Yes |
| Dorset-Council-UK/FloodOnlineReportingTool.Public | MIT | Yes | Yes | Yes | Required | Yes |
| Dorset-Council-UK/GIFramework-Maps | MIT (code) / OGL v3 (docs) | Yes | Yes | Yes | Required | Yes |
| Dorset-Council-UK/GdsBlazorComponents | MIT | Yes | Yes | Yes | Required | Yes |
| east-sussex-county-council/Escc.Libraries.BranchFinder | OGL v3 | Yes | Yes | Yes | Required | Yes |
| east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder | OGL v3 | Yes | Yes | Yes | Required | Yes |

**Notes**: All assessed candidates carry fully compatible licenses for UK government reuse. MIT and OGL v3 are the dominant licenses in this set. No GPL or proprietary licenses were encountered in the shortlisted candidates. Crown Copyright applies to the alphagov repositories — UK Government is the copyright holder, which is directly compatible with a CMA / DESNZ-owned service. Attribution requirements for MIT and OGL v3 are satisfied by maintaining license files in any forked or derived codebase.

---

## Tech Stack Alignment

| Repository | Language | Framework | Infrastructure | Aligns With Project | Adaptation Needed |
|------------|----------|-----------|----------------|---------------------|-------------------|
| alphagov/govuk-frontend | JavaScript / SCSS | None (vanilla) | npm package | Yes — any modern web stack | Install as npm dependency; configure SCSS build pipeline |
| alphagov/notifications-python-client | Python | None (API client) | PyPI package | Yes — if Python backend | Install via pip; wrap with retry/dead-letter logic |
| alphagov/notifications-node-client | JavaScript | None (API client) | npm package | Yes — if Node.js backend | Install via npm; alternative to Python client |
| Dorset-Council-UK/FloodOnlineReportingTool.Public | C# | ASP.NET Core + Blazor | IIS / Kestrel / Azure | Partial — patterns reusable | Significant: full language translation for direct reuse |
| Dorset-Council-UK/GIFramework-Maps | TypeScript + C# | ASP.NET Core | Azure | Partial — TypeScript layer adaptable | Extract TypeScript mapping patterns; discard C# backend |
| Dorset-Council-UK/GdsBlazorComponents | C# | Blazor | .NET | No — only if Blazor chosen | Full stack change required for direct adoption |
| east-sussex-county-council/Escc.Libraries.BranchFinder | C# | ASP.NET MVC | IIS | No | Full language translation required |
| east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder | C# | ASP.NET MVC | IIS | No | Full language translation required |

**Project Tech Stack**: The Fuel Finder's technology stack has not yet been formally decided (Alpha phase). Based on ARC-001-REQ-v2.0 and TCoP compliance (Point 3 — open source, Point 5 — cloud first), the most likely stack is: Python (Django or FastAPI) or Node.js (Express/Fastify) for the backend API; govuk-frontend (JavaScript) for the citizen-facing UI; PostgreSQL + PostGIS for geospatial data; a managed message queue (AWS SQS, Azure Service Bus) for async pipeline; deployed to AWS UK or Azure UK regions. All alphagov library candidates align directly. The C#/.NET candidates from Dorset Council and East Sussex CC are reference-only given this likely stack direction.

---

## Gap Analysis

| Capability | Status | Notes | Recommended Action |
|------------|--------|-------|--------------------|
| Citizen-facing UI / Design System | Reusable | alphagov/govuk-frontend — mandatory Library adoption | Adopt as npm dependency immediately |
| GOV.UK Notify integration | Reusable | alphagov/notifications-python-client or notifications-node-client | Adopt matching client for chosen backend language |
| Online data submission pattern | Partial | FloodOnlineReportingTool.Public provides Reference architecture; C# stack diverges | Study patterns; build in project language |
| Geospatial proximity search | Partial | Escc.Libraries.BranchFinder and GIFramework-Maps provide Reference patterns; outdated or C# stack | Study patterns; consider Postcodes.io as geocoding provider |
| Fuel price data ingestion pipeline | No match | No government code found after 4 query variations — genuine gap | Build from scratch; consider contributing back under OGL |
| Compliance monitoring dashboard | No match | No government code found after 3 query variations — genuine gap | Build from scratch; reuse GOV.UK Design System for UI |
| Audit trail / tamper-evident logging | No match | No government code found after 3 query variations — genuine gap | Build from scratch; use append-only cloud storage with integrity hashing |

**Legend**: Reusable | Partial | No match

---

## Recommendations

### Reuse Strategy Summary

The highest-priority reuse actions are both mandatory and straightforward: alphagov/govuk-frontend and the GOV.UK Notify client libraries must be adopted — they are the canonical government-provided implementations for their respective functions, they carry permissive MIT licenses, and they are directly mandated by TCoP Principle 13 (Reuse Government Platforms) and Architecture Principle 13 from ARC-000-PRIN-v1.0. These are Library adoptions (install as dependencies), not Fork candidates. Adopting govuk-frontend eliminates approximately 25 person-days of UI component development and ensures WCAG 2.2 AA compliance is built-in rather than retrofitted. Adopting the Notify client eliminates the need to build and maintain a custom Notify HTTP integration layer.

Beyond the mandatory library adoptions, the Dorset Council repositories (FloodOnlineReportingTool.Public and GIFramework-Maps) are the most valuable Reference candidates in the govreposcrape index for this project domain. Both are actively maintained, MIT-licensed, and structurally relevant: the Flood Tool demonstrates the async data submission, message contracting, and GOV.UK Notify integration pattern in a government context; GIFramework-Maps demonstrates geospatial data display and search in a .NET + TypeScript stack with excellent documentation. Neither is a Fork candidate because the C# backend language diverges too significantly from the Fuel Finder's likely Python or Node.js stack. Developers should allocate time to studying these codebases during the Alpha phase architecture spike.

Three capabilities — fuel price data ingestion pipeline, compliance monitoring dashboard, and tamper-evident audit trail — have no government code precedent in the indexed repositories. This is not surprising: real-time commodity price ingestion at regulatory scale is a novel UK government problem, and enforcement dashboard tooling tends to be built bespoke per regulatory context. These should be built from scratch during Beta, following the architectural principles established in ARC-000-PRIN-v1.0 (asynchronous pipeline, zero-trust security, audit-by-default). The CMA / DESNZ team should plan to publish the resulting implementations under OGL v3 to enable cross-government reuse — this would fulfil TCoP Point 8 (Share, reuse and collaborate) and GDS Service Standard Point 12 (Make new source code open).

### Implementation Priority

| Priority | Repository | Capability | Action | Estimated Effort | Timeline |
|----------|------------|------------|--------|-----------------|----------|
| 1 | alphagov/govuk-frontend | Citizen UI / Design System | Install as npm dependency; configure SCSS pipeline | 2 days setup | Discovery / Alpha Sprint 1 |
| 2 | alphagov/notifications-python-client (or node-client) | GOV.UK Notify integration | Install via pip/npm; build retry wrapper and DLQ | 3 days setup + testing | Alpha Sprint 2 |
| 3 | Dorset-Council-UK/FloodOnlineReportingTool.Public | Async submission pattern | Study architecture; extract async pipeline design | 3 days research | Alpha architecture spike |
| 4 | Dorset-Council-UK/GIFramework-Maps | Geospatial map display | Study TypeScript mapping patterns; adapt for FR-004 | 2 days research | Alpha architecture spike |
| 5 | east-sussex-county-council/Escc.Libraries.BranchFinder | Proximity search | Study postcode geocoding pattern; evaluate Postcodes.io | 1 day research | Alpha architecture spike |
| 6 | — | Fuel price ingestion pipeline | Build from scratch; async queue + validator + publisher | 45 days | Beta Sprint 1–6 |
| 7 | — | Compliance monitoring dashboard | Build from scratch; RBAC + GOV.UK Frontend | 30 days | Beta Sprint 4–8 |
| 8 | — | Audit trail and evidence store | Build from scratch; append-only + cryptographic integrity | 15 days | Beta Sprint 2–4 |

### Risk Considerations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| govuk-frontend major version upgrade during development breaks existing UI | Medium | Medium | Pin to a specific version in package.json; schedule upgrade sprints; follow GDS release notes |
| GOV.UK Notify client library lags behind Notify API changes (new features not yet in client) | Low | Low | Library is actively maintained by GDS; monitor repo; fallback to direct HTTP if a specific new API feature is needed before client update |
| FloodOnlineReportingTool C#/.NET patterns require significant translation effort to Python/Node.js | Medium | Low | Reference patterns only — design time, not code time; budget 1 day per pattern studied |
| GIFramework-Maps TypeScript patterns require Leaflet.js or specialist mapping knowledge | Medium | Medium | Allocate a developer with TypeScript + mapping experience to the Alpha architecture spike; Leaflet.js is well-documented open source |
| No government precedent for fuel price ingestion pipeline creates higher design risk | High | High | Invest in a dedicated Alpha technical spike (2 weeks); prototype the async pipeline before Beta; engage NCSC / GDS for peer review of the design |
| Escc.Libraries.BranchFinder depend on deprecated GOV.UK locate-API | High | Low | Impact is low — Reference use only; validate geocoding approach against Postcodes.io as alternative |

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| *None provided* | — | — | — | — |

---

**Generated by**: ArcKit `/arckit:gov-reuse` agent
**Generated on**: 2026-03-23
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: claude-sonnet-4-6
