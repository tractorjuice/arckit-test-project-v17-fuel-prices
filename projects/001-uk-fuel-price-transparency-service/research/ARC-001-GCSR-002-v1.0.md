# Government Code Search Report: UK Fuel Price Transparency Service -- Geospatial Facility Finder with PostGIS

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit:gov-code-search`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GCSR-002-v1.0 |
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
| 1.0 | 2026-03-24 | ArcKit AI | Initial creation from `/arckit:gov-code-search` agent -- geospatial facility finder with PostGIS | PENDING | PENDING |

---

## Executive Summary

### Search Query

**Original Query**: `geospatial facility finder with PostGIS`

**Query Variations Used**:

- `location based search nearest facility map service`
- `PostGIS spatial database geolocation proximity search government`
- `find nearest service by postcode geospatial API`
- `geographic information system mapping coordinates latitude longitude`
- `fuel station locator petrol station finder near me`

**Platforms Searched**: GitHub (UK Government organisations indexed by govreposcrape -- approximately 21,000 repositories across local authority, central government, and devolved administration organisations)

### Results Found

**Total Results Across All Queries**: 177 (before deduplication)

**Unique Repositories After Deduplication**: 47

**High Relevance Results**: 6

**Medium Relevance Results**: 8

**Low Relevance / Excluded**: 33

### Top Results

| # | Repository | Organisation | Relevance | Language | Last Active |
|---|------------|--------------|-----------|----------|-------------|
| 1 | [GIFramework-Maps](https://github.com/Dorset-Council-UK/GIFramework-Maps) | Dorset Council | High | TypeScript / C# | 2025-12-22 |
| 2 | [FloodOnlineReportingTool.Public](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public) | Dorset Council | High | C# | 2025-06-17 |
| 3 | [Escc.RubbishAndRecycling.SiteFinder](https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder) | East Sussex County Council | High | C# | 2022-12-06 |
| 4 | [Escc.Libraries.BranchFinder](https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder) | East Sussex County Council | High | C# | 2022-12-06 |
| 5 | [camdenmaps](https://github.com/CamdenCouncil/camdenmaps) | Camden Council | High | JavaScript | 2021-12-20 |

---

## Search Results

### High Relevance Results

#### GIFramework-Maps

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Local Authority) |
| **Repository URL** | [https://github.com/Dorset-Council-UK/GIFramework-Maps](https://github.com/Dorset-Council-UK/GIFramework-Maps) |
| **Description** | A .NET-based web mapping application for creating, sharing, and managing web maps using OGC web services. Powers the DorsetExplorer mapping platform. |
| **Language** | TypeScript (42.7%), C# (37.6%), HTML (18.1%) |
| **License** | MIT |
| **Last Activity** | 2025-12-22 (v1.10.0 release) |
| **Stars** | 21 |

**Why Relevant**: This is the most directly relevant repository found. GIFramework-Maps explicitly requires PostgreSQL 13+ with PostGIS extension, uses .NET with Entity Framework Core for the backend, and OpenLayers with TypeScript on the frontend. It provides a full-stack web mapping application with spatial data querying, location search, and GPS tracking -- all capabilities needed by the Fuel Finder "find nearest station" feature. It is actively maintained (latest release December 2025), has the highest star count among results (21), and is MIT-licensed for reuse. Dorset Council has built a production-grade GIS platform that directly addresses the pattern of "geospatial facility finder with PostGIS."

**Key Patterns**:

- PostgreSQL + PostGIS as the spatial database backend with Entity Framework Core ORM
- OpenLayers for interactive map rendering on the frontend (TypeScript)
- OGC web services (WMS/WFS) for data layer interoperability
- Multi-service location search (configurable search providers)
- Azure AD authentication integration for secure deployments
- Built-in admin GUI for managing map configurations
- Nunjucks templating for customizable spatial query result presentation
- Deployment options: IIS, Kestrel, or Azure

---

#### FloodOnlineReportingTool.Public

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Local Authority) |
| **Repository URL** | [https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public) |
| **Description** | A .NET-based web application enabling citizens to report flooding to local flood authorities, built with the GDS Design System via GdsBlazorComponents. |
| **Language** | C# (81.1%) |
| **License** | MIT |
| **Last Activity** | 2025-06-17 |
| **Stars** | 0 |

**Why Relevant**: This repository demonstrates a production government service that combines PostGIS (PostgreSQL 13+ with PostGIS extension explicitly required) with GDS Design System compliance. The citizen-facing flood reporting interface uses location-based input, and the application architecture (C# .NET with Entity Framework Core and PostGIS) is directly transferable to the Fuel Finder's geospatial requirements. The same team at Dorset Council built the GdsBlazorComponents library (Blazor components styled to GOV.UK Design System, MIT-licensed, actively maintained with v3.0.0 released March 2026), demonstrating an integrated approach to GDS-compliant geospatial services.

**Key Patterns**:

- PostgreSQL + PostGIS for spatial data storage and querying
- .NET with Entity Framework Core database abstraction
- GDS Design System compliance via the companion GdsBlazorComponents library
- Citizen-facing location-based reporting (geospatial input workflow)
- Open source with MIT licence, designed for reuse by other local authorities and government departments

---

#### Escc.RubbishAndRecycling.SiteFinder

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council (Local Authority) |
| **Repository URL** | [https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder](https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder) |
| **Description** | Search facility for waste and recycling sites in East Sussex. Allows citizens to find their nearest recycling site by postcode. |
| **Language** | C# (69.9%) |
| **License** | Available (LICENSE.md) |
| **Last Activity** | 2022-12-06 |
| **Stars** | 0 |

**Why Relevant**: This is a direct "facility finder" implementation -- citizens enter a postcode and the system returns the nearest waste/recycling sites sorted by distance. The pattern is highly analogous to the Fuel Finder's "find nearest fuel station" use case (UC-1). It uses the GOV.UK locate-api for postcode-to-coordinate geocoding, then calculates distances to facility locations. While it does not use PostGIS (relying instead on application-level distance calculation), the user journey and API integration pattern are directly relevant to understanding how UK councils have implemented "find nearest X" services.

**Key Patterns**:

- Postcode-centric geocoding via GOV.UK locate-api (latitude/longitude centre point)
- Application-layer distance calculation from user location to facility locations
- Query-string-based search API (`?postcode=AB12CD&type=Anything`)
- JSON API for facility data served from Umbraco CMS
- NuGet package for embedding the search form in different site templates

---

#### Escc.Libraries.BranchFinder

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council (Local Authority) |
| **Repository URL** | [https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder](https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder) |
| **Description** | "Find your library" tool for the East Sussex County Council website. Allows citizens to find their nearest library branch by postcode. |
| **Language** | C# (68.1%) |
| **License** | Available (LICENSE.md) |
| **Last Activity** | 2022-12-06 |
| **Stars** | 0 |

**Why Relevant**: Another direct "facility finder" implementation, almost identical in architecture to the SiteFinder above but for library branches. It reinforces the pattern of postcode-based geocoding via GOV.UK locate-api with distance-sorted results. The replication of this pattern across two different finder tools by the same council demonstrates its maturity as a reusable approach. The user journey (enter postcode, get sorted nearest results) maps directly to the Fuel Finder's primary citizen use case.

**Key Patterns**:

- Same GOV.UK locate-api postcode geocoding pattern as SiteFinder
- Shared architectural approach across multiple "find nearest" applications
- JSON API data source for facility (library) location data
- C# .NET backend with server-side distance computation

---

#### camdenmaps

| Attribute | Value |
|-----------|-------|
| **Organisation** | Camden Council (London Borough) |
| **Repository URL** | [https://github.com/CamdenCouncil/camdenmaps](https://github.com/CamdenCouncil/camdenmaps) |
| **Description** | Camden Council's "Where's My Nearest" service (maps.camden.gov.uk). A general-purpose facility finder for local council services and amenities. |
| **Language** | JavaScript (82.9%), CSS (9.7%), HTML (7.1%) |
| **License** | Not specified |
| **Last Activity** | 2021-12-20 |
| **Stars** | 0 |

**Why Relevant**: The "Where's My Nearest" branding and concept is directly analogous to the Fuel Finder's purpose -- finding the nearest instance of a facility type. Camden's implementation appeared in 5 of 6 search queries, indicating strong relevance signal. The project includes Selenium acceptance testing and CI/CD via Travis CI with Heroku deployment, demonstrating a mature development and testing approach. However, the README lacks technical architecture detail about the mapping libraries or spatial backend used.

**Key Patterns**:

- "Where's My Nearest" as the user-facing concept -- directly transferable language for fuel station finding
- JavaScript-based frontend implementation
- Automated acceptance testing with Selenium and SauceLabs
- Performance monitoring built into the CI pipeline
- CI/CD pipeline (Travis CI) with automated deployment (Heroku)

---

#### BathApp

| Attribute | Value |
|-----------|-------|
| **Organisation** | Bath and North East Somerset Council (Local Authority) |
| **Repository URL** | [https://github.com/BathnesDevelopment/BathApp](https://github.com/BathnesDevelopment/BathApp) |
| **Description** | Cross-platform mobile application for BANES residents, providing local information and council services with location-based facility finding ("MyNearest" feature). |
| **Language** | JavaScript (82.8%) |
| **License** | MIT |
| **Last Activity** | 2015-03-10 (inactive) |
| **Stars** | 0 |

**Why Relevant**: BathApp implements a "MyNearest" feature that identifies nearby libraries, medical services, and community facilities using device geolocation. It uses Leaflet for interactive mapping and Cordova geolocation plugin for GPS positioning. While the project is no longer active (last updated 2015), its architecture demonstrates the mobile-first facility finder pattern using Leaflet.js and Open311 GeoReport standards -- both relevant reference patterns for the Fuel Finder's mobile-responsive design and potential future mobile app.

**Key Patterns**:

- Leaflet.js for interactive map rendering
- Cordova geolocation plugin for device GPS positioning
- "MyNearest" proximity-based facility finding feature
- Open311 GeoReport integration for location-tagged citizen reporting
- Ionic Framework for cross-platform mobile delivery (iOS/Android)
- MIT licence

---

### Medium Relevance Results

#### GeographicalNeeds-Web

| Attribute | Value |
|-----------|-------|
| **Organisation** | Bath and North East Somerset Council (Local Authority) |
| **Repository URL** | [https://github.com/BathnesDevelopment/GeographicalNeeds-Web](https://github.com/BathnesDevelopment/GeographicalNeeds-Web) |
| **Description** | Web application with geographical data services. Structure includes Data Loading Tool, DataAccessServices, GeographicalNeedsService. |
| **Language** | C# (71.7%), JavaScript (25.2%) |
| **License** | Not specified |
| **Last Activity** | Unknown (13 commits total) |
| **Stars** | 1 |

**Why Relevant**: The repository name and structure suggest geographical data processing capabilities, but the README failed to load and no detailed documentation is available. The presence of a "GeographicalNeedsService" and "DataAccessServices" directory hints at a service-oriented geospatial architecture. The limited documentation reduces its immediate utility as a reference.

**Key Patterns**:

- Service-oriented architecture for geographical data
- Separate data loading and data access layers
- C# .NET backend

---

#### Escc.Gritting.GrittingMap

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council (Local Authority) |
| **Repository URL** | [https://github.com/east-sussex-county-council/Escc.Gritting.GrittingMap](https://github.com/east-sussex-county-council/Escc.Gritting.GrittingMap) |
| **Description** | Google Map showing the real-time position of gritting vehicles as they move around East Sussex. |
| **Language** | C# (48.2%) |
| **License** | Available (LICENSE.md) |
| **Last Activity** | 2019-06-13 (archived) |
| **Stars** | 0 |

**Why Relevant**: Demonstrates real-time geospatial tracking of mobile assets on a map -- a different but related pattern to facility finding. The Google Maps integration and vehicle tracking approach could inform the Fuel Finder's map display of fuel stations. However, the project is archived and uses Google Maps (which has licensing cost implications for government services).

**Key Patterns**:

- Google Maps for geospatial visualisation
- Real-time location tracking of mobile assets
- C# backend with JavaScript frontend

---

#### DorsetExplorer-Docs

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Local Authority) |
| **Repository URL** | [https://github.com/Dorset-Council-UK/DorsetExplorer-Docs](https://github.com/Dorset-Council-UK/DorsetExplorer-Docs) |
| **Description** | User guide for DorsetExplorer, the public-facing mapping platform powered by GIFramework-Maps. Documentation built with MkDocs Material. |
| **Language** | Markdown (documentation) |
| **License** | Not specified |
| **Last Activity** | 2023-02-07 |
| **Stars** | 0 |

**Why Relevant**: Companion documentation for GIFramework-Maps, demonstrating how a local authority has documented and deployed a PostGIS-backed public mapping service. Useful as a reference for how to present geospatial tools to end users.

**Key Patterns**:

- MkDocs Material for user-facing documentation
- Documentation-as-code approach alongside the mapping platform

---

#### GdsBlazorComponents

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Local Authority) |
| **Repository URL** | [https://github.com/Dorset-Council-UK/GdsBlazorComponents](https://github.com/Dorset-Council-UK/GdsBlazorComponents) |
| **Description** | Blazor components styled to match the GOV.UK Design System. 30+ pre-built components for forms, navigation, and layout. |
| **Language** | C# (41.1%) |
| **License** | MIT |
| **Last Activity** | 2026-03-20 (v3.0.0) |
| **Stars** | 4 |

**Why Relevant**: While not directly geospatial, this library is used by the FloodOnlineReportingTool and provides the GDS Design System compliance layer for .NET Blazor applications. If the Fuel Finder adopted a .NET/Blazor stack with PostGIS, this library would provide immediate GDS compliance for the frontend.

**Key Patterns**:

- GOV.UK Design System as Blazor components
- 30+ components covering forms, inputs, error handling, navigation
- Actively maintained (March 2026 release)
- MIT licence for reuse

---

#### QGIS.Mosaic.Builder

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dorset Council (Local Authority) |
| **Repository URL** | [https://github.com/Dorset-Council-UK/QGIS.Mosaic.Builder](https://github.com/Dorset-Council-UK/QGIS.Mosaic.Builder) |
| **Description** | QGIS plugin for copying features from multiple layers and merging them into a single outline or maintaining as individual polygons. |
| **Language** | Python (66.8%) |
| **License** | MIT |
| **Last Activity** | 2026-02-05 (v1.0.5) |
| **Stars** | 0 |

**Why Relevant**: Demonstrates Dorset Council's broader GIS tooling ecosystem. The QGIS plugin pattern is relevant for internal spatial data preparation (e.g., preparing fuel station catchment areas or administrative boundary layers). Not directly applicable to the citizen-facing Fuel Finder.

**Key Patterns**:

- QGIS plugin development in Python
- Polygon merging and spatial data consolidation
- Designed for non-GIS professionals

---

#### DundeeCityCouncil/GIS

| Attribute | Value |
|-----------|-------|
| **Organisation** | Dundee City Council (Scottish Local Authority) |
| **Repository URL** | [https://github.com/DundeeCityCouncil/GIS](https://github.com/DundeeCityCouncil/GIS) |
| **Description** | GIS repository containing JavaScript API code and GeoServer style configurations. |
| **Language** | JavaScript (63.2%), Scheme (36.8%) |
| **License** | GPL-3.0 |
| **Last Activity** | Unknown |
| **Stars** | 0 |

**Why Relevant**: Minimal documentation, but the presence of GeoServer style configurations alongside JavaScript API code suggests a WMS/WFS-based mapping approach similar to GIFramework-Maps. Useful only as a signal that GeoServer is used across multiple UK councils.

**Key Patterns**:

- GeoServer for spatial data serving
- JavaScript API for map interaction
- GPL-3.0 licence (note: more restrictive than MIT for reuse)

---

#### Escc.AddressAndPersonalDetails

| Attribute | Value |
|-----------|-------|
| **Organisation** | East Sussex County Council (Local Authority) |
| **Repository URL** | [https://github.com/east-sussex-county-council/Escc.AddressAndPersonalDetails](https://github.com/east-sussex-county-council/Escc.AddressAndPersonalDetails) |
| **Description** | C# library for managing UK addresses conforming to BS7666 and UK Government Data Standards Catalogue standards. |
| **Language** | C# (76.7%) |
| **License** | Available (LICENSE.md) |
| **Last Activity** | 2014-02 |
| **Stars** | 0 |

**Why Relevant**: Provides UK address data structure standards (BS7666, Royal Mail AddressPoint) that would apply to fuel station address storage. Does not provide geocoding or location search, but the data modelling standards are relevant for ensuring address data quality in the forecourt register.

**Key Patterns**:

- BS7666 UK address standard implementation
- Royal Mail address formatting
- C# data structure library

---

## Code Patterns Identified

| Pattern | Repositories Using It | Description |
|---------|----------------------|-------------|
| PostgreSQL + PostGIS spatial database | GIFramework-Maps, FloodOnlineReportingTool.Public | PostGIS extension on PostgreSQL for spatial data storage, indexing, and querying. Both repos require PostgreSQL 13+ with PostGIS. Entity Framework Core provides the ORM layer. |
| Postcode-centric geocoding via GOV.UK locate-api | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder | Postcode entered by user is geocoded to lat/long via the GOV.UK locate-api, then distance calculations are performed against facility locations. No spatial database required -- computation happens at application layer. |
| OpenLayers for map rendering | GIFramework-Maps | OpenLayers JavaScript library for interactive map display, supporting WMS/WFS layers, GPS tracking, annotations, and measurement tools. |
| Leaflet.js for lightweight mapping | BathApp | Leaflet library for displaying points of interest on interactive maps, combined with device geolocation. |
| GDS Design System compliance | FloodOnlineReportingTool.Public, GdsBlazorComponents | GOV.UK Design System components implemented as Blazor components for .NET applications. 30+ components covering forms, navigation, and accessibility. |
| OGC web services (WMS/WFS) | GIFramework-Maps, DundeeCityCouncil/GIS | Open Geospatial Consortium standards for serving and consuming spatial data layers. GeoServer commonly used as the data serving backend. |
| "Find nearest X" user journey | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder, camdenmaps, BathApp | Common citizen-facing pattern: enter postcode or allow geolocation, receive distance-sorted list of nearest facilities. Consistent across multiple councils and facility types. |
| C# .NET backend | GIFramework-Maps, FloodOnlineReportingTool.Public, Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder | Dominant backend language across geospatial government repos. .NET with Entity Framework Core is the most common stack for PostGIS-backed services. |

**Observations**: Two distinct implementation approaches dominate UK government geospatial facility finders. The first (and more sophisticated) uses PostgreSQL with PostGIS for server-side spatial queries, exemplified by Dorset Council's GIFramework-Maps and FloodOnlineReportingTool. The second (and more common among smaller councils) uses postcode geocoding via the GOV.UK locate-api with application-layer distance calculations, requiring no spatial database. The PostGIS approach supports complex spatial queries (e.g., polygon containment, buffer zones, route-based proximity) while the postcode approach is simpler but limited to point-to-point distance ranking. For the Fuel Finder's ~8,500 stations with radius and route-based search requirements, the PostGIS approach is the stronger architectural fit.

C# .NET is the dominant backend language across the most relevant results, which differs from the typical central government (alphagov) preference for Ruby on Rails, Python, or Node.js. This reflects the local authority origin of most geospatial repos in the index. OpenLayers and Leaflet are the two mapping libraries in use -- both are open source and avoid commercial licensing costs (unlike Google Maps, which the archived Gritting project used).

---

## Implementation Approaches Compared

| Approach | Used By | Pros | Cons |
|----------|---------|------|------|
| **PostGIS spatial database with .NET backend** | GIFramework-Maps, FloodOnlineReportingTool.Public | Supports complex spatial queries (nearest-neighbour, polygon intersection, buffer zones); scales to large datasets; spatial indexing for performance; industry-standard OGC compliance; MIT-licensed reference implementations available | Requires PostGIS operational expertise; more complex infrastructure (PostgreSQL + PostGIS extension); learning curve for spatial SQL; heavier than needed for simple distance queries |
| **Postcode geocoding with application-layer distance calculation** | Escc.RubbishAndRecycling.SiteFinder, Escc.Libraries.BranchFinder | Simple to implement; no spatial database needed; uses existing GOV.UK locate-api; minimal infrastructure requirements; works with any data store | Does not scale well beyond ~1,000 facilities; no support for polygon queries or route-based search; geocoding dependency on external API; limited to postcode granularity (not precise GPS coordinates); cannot support "stations along my route" use case |
| **JavaScript mapping frontend with API backend** | camdenmaps, BathApp | Rich interactive map experience; device geolocation integration; mobile-responsive; familiar web technologies | Requires separate spatial backend for query processing; frontend-heavy architecture may not suit GOV.UK progressive enhancement requirements; client-side distance calculations limited by browser performance |
| **GeoServer + OGC services** | GIFramework-Maps, DundeeCityCouncil/GIS | Standards-based interoperability; supports WMS/WFS/WMTS; mature Java-based platform; can serve data to multiple frontends | Additional infrastructure component; Java-based (separate from .NET backend); requires GIS expertise for configuration; potential performance overhead for simple queries |

**Recommended Approach for This Project**: **PostGIS spatial database** -- The Fuel Finder requires proximity search across ~8,500 fuel stations with sub-second response times, support for both postcode and GPS-coordinate-based location, distance-sorted results within configurable radii (default 5 miles per UC-1), and future potential for route-based search. PostGIS provides spatial indexing (R-tree via GiST) that makes nearest-neighbour queries efficient at this scale, and `ST_DWithin` / `ST_Distance` functions directly implement the "find within radius" requirement. The GOV.UK locate-api postcode geocoding approach should be used as an input layer (converting postcodes to coordinates) but the spatial querying itself should use PostGIS for performance and flexibility. GIFramework-Maps from Dorset Council provides a strong MIT-licensed reference implementation.

---

## Project Relevance Mapping

| Repository | Relevant Requirements | How It Helps | Quick Start |
|---|---|---|---|
| [Dorset-Council-UK/GIFramework-Maps](https://github.com/Dorset-Council-UK/GIFramework-Maps) | FR-006 (fuel price display by location), FR-007 (map view), UC-1 (citizen finds cheapest fuel nearby), NFR-P (performance at scale) | Full PostGIS + .NET + OpenLayers reference architecture for geospatial facility finding. Demonstrates spatial query patterns, map rendering, and GPS integration. | `git clone https://github.com/Dorset-Council-UK/GIFramework-Maps.git` |
| [Dorset-Council-UK/FloodOnlineReportingTool.Public](https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public) | BR-003 (citizen-facing service), BR-007 (GDS compliance), UC-1 (location-based citizen service) | GDS-compliant .NET service with PostGIS backend. Shows how to combine spatial data handling with GOV.UK Design System compliance. | `git clone https://github.com/Dorset-Council-UK/FloodOnlineReportingTool.Public.git` |
| [Dorset-Council-UK/GdsBlazorComponents](https://github.com/Dorset-Council-UK/GdsBlazorComponents) | BR-007 (GDS compliance), NFR-A (accessibility, WCAG 2.2 AA) | Ready-made GOV.UK Design System components for .NET Blazor if the team adopts a .NET stack. Saves significant frontend development effort. | `dotnet add package GdsBlazorComponents` |
| [east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder](https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder) | UC-1 (find nearest facility by postcode), FR-006 (location search) | Reference implementation for the postcode-based "find nearest" user journey. Directly analogous to UC-1's main flow. | `git clone https://github.com/east-sussex-county-council/Escc.RubbishAndRecycling.SiteFinder.git` |
| [east-sussex-county-council/Escc.Libraries.BranchFinder](https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder) | UC-1 (find nearest facility by postcode) | Second "find nearest" reference reinforcing the GOV.UK locate-api geocoding pattern. Validates the approach across multiple facility types. | `git clone https://github.com/east-sussex-county-council/Escc.Libraries.BranchFinder.git` |
| [CamdenCouncil/camdenmaps](https://github.com/CamdenCouncil/camdenmaps) | UC-1 (citizen finds nearest), FR-007 (map display) | "Where's My Nearest" branding and concept validation. Includes automated acceptance testing patterns for location-based services. | `git clone https://github.com/CamdenCouncil/camdenmaps.git` |

---

## Search Effectiveness Assessment

### Coverage

The search results predominantly come from **local authority** GitHub organisations (Dorset Council, East Sussex County Council, Camden Council, Bath and North East Somerset Council, Dundee City Council, Bristol City Council). No results were returned from central government organisations such as:

- **alphagov** (GDS) -- which hosts significant geospatial work including the OS Places API integrations and GOV.UK location services
- **NHSDigital** -- which has facility finder implementations (e.g., NHS service search)
- **defra** -- which has significant PostGIS usage for environmental mapping
- **communitiesuk / DLUHC** -- which has geospatial planning tools
- **hmrc** -- which has address validation services
- **OS (Ordnance Survey)** -- which publishes open geospatial data APIs

This means the results reflect local council approaches to geospatial finding but **miss the central government production services** that are most architecturally relevant to a national-scale service like Fuel Finder.

### Gaps

The following topics returned no directly relevant results:

| Gap | Alternative Search Strategy |
|-----|---------------------------|
| Central government PostGIS implementations (alphagov, defra) | Search directly: `https://github.com/search?q=org%3Aalphagov+postgis&type=code` and `https://github.com/search?q=org%3Adefra+postgis&type=code` |
| NHS facility finder / service locator architecture | Search directly: `https://github.com/search?q=org%3ANHSDigital+service+finder&type=repositories` |
| Ordnance Survey Places API integration patterns | Official docs: `https://osdatahub.os.uk/docs/places/overview` |
| GOV.UK locate-api / OS Places API reference implementation | Search: `https://github.com/search?q=org%3Aalphagov+locate+api&type=repositories` |
| Route-based proximity search ("stations along my route") | No UK gov open-source implementations found. Consider OSRM (Open Source Routing Machine) or Valhalla for route generation combined with PostGIS `ST_DWithin` on route geometries. |
| High-volume geospatial API design (caching, CDN, rate limiting) | Review API design patterns from `https://github.com/alphagov/content-store` and `https://www.api.gov.uk` |

### Index Limitations

The govreposcrape index (approximately 21,000 repositories) is dominated by local authority organisations. Central government organisations (alphagov alone has > 2,000 repos) are represented but their geospatial repositories may not surface well for these queries due to different naming conventions and README content. The search returned 177 total results across 6 queries but unique repos numbered only 47 after deduplication, with significant overlap between queries. The "fuel station locator" query returned only 4 results, confirming that no UK government fuel-station-specific geospatial code exists in the index.

---

## Recommendations

### Immediate Next Steps

1. **Clone and Review**: [GIFramework-Maps](https://github.com/Dorset-Council-UK/GIFramework-Maps) -- Examine the PostGIS database schema, Entity Framework Core spatial query implementations, and OpenLayers map configuration. Focus on the location search and spatial querying modules.
2. **Architecture Spike**: Build a minimal PostGIS-backed "find nearest fuel station" prototype using the GIFramework-Maps database patterns with a simplified API endpoint (`GET /api/stations/nearest?lat=X&lon=Y&radius=5`).
3. **License Verification**: GIFramework-Maps and FloodOnlineReportingTool.Public both use MIT licence -- confirm this permits the intended reuse pattern (library dependency, code reference, or fork).
4. **Community Contact**: Reach out to the Dorset Council GIS team regarding their experience running PostGIS at scale and their GDS compliance approach. Their FloodOnlineReportingTool + GdsBlazorComponents combination demonstrates an integrated approach worth learning from.
5. **Central Government Gap-Fill**: Search alphagov and defra GitHub organisations directly for PostGIS usage, as the govreposcrape index did not surface these results.

### Search Refinements

If further searching is needed, consider these refined queries:

- `NHS service finder facility locator near me API` -- to surface NHS facility finder implementations that may use similar patterns
- `Ordnance Survey Places API postcode lookup geocoding integration` -- to find OS Places API client implementations across government
- `Ruby on Rails geospatial nearest neighbour PostGIS` -- to find central government (alphagov-style) implementations in the dominant GDS tech stack
- `Python Flask geospatial spatial query API` -- to find Python-based spatial API implementations used by data science teams (defra, ONS)

### Related ArcKit Commands

- Run `/arckit:gov-reuse` for a full reusability assessment of GIFramework-Maps and FloodOnlineReportingTool.Public, including code quality, documentation, tech stack alignment, and licence compatibility analysis
- Run `/arckit:research` for a broader technology research report comparing PostGIS with alternative geospatial approaches (Elasticsearch geo queries, MongoDB geospatial, cloud-native options like AWS Location Service or Azure Maps)

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| ARC-001-REQ-v2.0 | Requirements | Project 001 | UC-1 (find nearest fuel station), FR-006, FR-007, search radius 5 miles, 8,500 stations | `projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md` |
| GIFramework-Maps README | Repository Documentation | Dorset Council (GitHub) | PostGIS requirement, OpenLayers frontend, .NET backend, MIT licence | [GitHub](https://github.com/Dorset-Council-UK/GIFramework-Maps) |
| GOV.UK Design System | Standard | GDS | Component library for government digital services | [https://design-system.service.gov.uk/](https://design-system.service.gov.uk/) |
| PostGIS Documentation | Technical Reference | OSGeo | Spatial functions: ST_DWithin, ST_Distance, ST_MakePoint, spatial indexing | [https://postgis.net/documentation/](https://postgis.net/documentation/) |
| OGC Web Services Standards | Standard | Open Geospatial Consortium | WMS, WFS, WMTS specifications for interoperable geospatial data | [https://www.ogc.org/standards/](https://www.ogc.org/standards/) |

---

**Generated by**: ArcKit `/arckit:gov-code-search` agent
**Generated on**: 2026-03-24
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: Claude Opus 4.6 (1M context)
