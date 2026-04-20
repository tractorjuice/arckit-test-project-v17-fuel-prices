# UK Government Fuel Price Transparency Service

**Architecture governance project for a government service consuming petrol and diesel price data via the CMA Fuel Finder open data scheme.**

Built with [ArcKit](https://tractorjuice.github.io/arc-kit/) **v4.7.2** — 100+ AI-driven slash commands for architecture governance across Claude Code, Gemini CLI, and Codex CLI.

## Project Context

The **Competition and Markets Authority (CMA)** established the [Fuel Finder](https://www.gov.uk/government/publications/fuel-finder-enforcement-guidance) open data scheme under the **Motor Fuel Price (Open Data) Regulations 2025**. This scheme requires approximately 8,500 UK fuel retailers to publish real-time pricing data to increase market transparency and help consumers find the cheapest fuel.

This project designs and governs a government service that **consumes the VE3 Fuel Finder API** (the open data aggregator for the scheme) rather than building submission infrastructure. The service:

- **Consumes** real-time petrol and diesel price data from the VE3 Fuel Finder API
- **Aggregates** fuel price data across regions, retailers, and fuel types
- **Publishes** price comparison tools and analytics for citizens and policy teams
- **Monitors** compliance with the Motor Fuel Price (Open Data) Regulations 2025
- **Reports** on fuel price trends to support CMA enforcement and DESNZ policy activity

| | |
|---|---|
| **Classification** | OFFICIAL |
| **Hosting** | UK Government cloud (AWS UK / Azure UK regions) |
| **Upstream data** | VE3 Fuel Finder API (open data scheme aggregator) |

## Key Stakeholders

| Stakeholder | Interest |
|-------------|----------|
| Competition and Markets Authority (CMA) | Enforcement of Fuel Finder regulations |
| Department for Energy Security & Net Zero (DESNZ) | Fuel market policy |
| Citizens / Motorists | Finding cheapest fuel prices |
| Fuel Retailers | Compliance with open data regulations |
| Government Digital Service (GDS) / CDDO | Service Standard and TCoP compliance |
| HM Treasury | Impact on cost of living / inflation |

## Regulatory Context

- **Motor Fuel Price (Open Data) Regulations 2025** — Mandates fuel price data publication
- **CMA Fuel Finder Enforcement Guidance** (December 2025) — How CMA uses enforcement powers
- **UK GDPR** — Data protection for any personal data in the pipeline
- **GDS Service Standard** — 14-point assessment for government digital services
- **Technology Code of Practice (TCoP)** — 13-point UK Government technology standards
- **Secure by Design** — UK Government security assessment framework

## Generated Artifacts

The project has produced **51+ architecture artifacts** across the following categories. Latest versions shown — see `projects/` for the full set.

### Global Governance (`000-global/`)

| Document | Description |
|----------|-------------|
| `ARC-000-PRIN-v1.0.md` | Cross-project architecture principles |

### Core Artifacts (`001-uk-fuel-price-transparency-service/`)

| Document | Description |
|----------|-------------|
| `ARC-001-PLAN-v2.0.md` | Project plan with timeline, phases, and gates |
| `ARC-001-STKE-v1.0.md` | Stakeholder drivers, goals, and outcomes |
| `ARC-001-RISK-v2.0.md` | Risk register (HM Treasury Orange Book) |
| `ARC-001-SOBC-v1.0.md` | Strategic Outline Business Case (Green Book) |
| `ARC-001-REQ-v3.0.md` | Requirements — 56 items, VE3 API consumer architecture |
| `ARC-001-DATA-v3.0.md` | Data model (derived from live VE3 CSV) |
| `ARC-001-DIAG-001-v1.0.md` | Architecture diagrams (Mermaid) |
| `decisions/ARC-001-ADR-001-v1.0.md` | VE3 API consumer architecture decision |

### Governance & Compliance

| Document | Description |
|----------|-------------|
| `ARC-001-ANAL-v4.0.md` | Governance quality analysis |
| `ARC-001-TRAC-v2.0.md` | Requirements traceability matrix |
| `ARC-001-TCOP-v2.0.md` | Technology Code of Practice assessment |
| `ARC-001-SECD-v1.0.md` | Secure by Design assessment |
| `ARC-001-DPIA-v2.0.md` | Data Protection Impact Assessment (UK GDPR Art. 35) |
| `ARC-001-BKLG-v1.0.md` | Prioritised product backlog |

### Research (`research/`)

| Document | Description |
|----------|-------------|
| `ARC-001-RSCH-v5.0.md` | Technology research with build vs buy analysis |
| `ARC-001-AWRS-v2.0.md` | AWS services research (eu-west-2) |
| `ARC-001-AZRS-v2.0.md` | Azure services research (UK South) |
| `ARC-001-DSCT-v2.0.md` | External data source discovery |
| `ARC-001-GOVR-v2.0.md` | Government reuse assessment |
| `ARC-001-GLND-v2.0.md` | Government code landscape analysis |
| `ARC-001-GCSR-*.md` | Government code search reports (5 queries) |
| `ARC-001-GRNT-v1.0.md` | UK grants and funding research |

### Vendor Profiles (`vendors/`)

- `ve3-global-profile.md` — VE3 Fuel Finder API provider (primary upstream)
- `aws-profile.md` — AWS UK (eu-west-2) candidate hosting
- `govuk-notify-profile.md` — GOV.UK Notify for alerting
- `ordnance-survey-profile.md` — OS geospatial data

### Tech Notes (`tech-notes/`)

- `fuel-finder-api.md` — VE3 Fuel Finder API reference
- `fuel-finder-third-party-ecosystem.md` — existing consumers
- `energy-smart-data-scheme.md` — related DESNZ initiative
- `oauth-20-client-credentials.md` — authentication pattern
- `postgis-geospatial-search.md` — location-based search
- `govuk-forms.md`, `regulators-pioneer-fund.md`

### External Documents (`external/`)

- `Fuel Finder for drivers_ Factsheet - GOV.UK.pdf`
- `UpdatedFuelPrice-1775466000049.csv` — live VE3 pricing sample

## Getting Started

1. Start your AI assistant (Claude Code, Gemini CLI, or Codex CLI)
2. Run `/arckit.principles` to establish architecture governance
3. Run `/arckit.stakeholders` to analyze stakeholder drivers and goals
4. Run `/arckit.requirements` to define requirements for the fuel price service

The recommended workflow order is:

```
plan → principles → stakeholders → risk → sobc → requirements → data-model →
research → wardley → diagram → dpia → tcop → secure → service-assessment
```

Full dependency ordering is documented in [`DEPENDENCY-MATRIX.md`](DEPENDENCY-MATRIX.md).

## Available Commands

100+ slash commands are available across Claude Code, Gemini CLI, and Codex CLI. The full catalogue is published at [docs/guides/](docs/guides/) and rendered on the [documentation site](docs/index.html).

### Core Workflow
`plan`, `principles`, `stakeholders`, `risk`, `sobc`, `requirements`, `data-model`, `research`, `datascout`, `wardley`, `adr`, `diagram`, `backlog`, `roadmap`, `strategy`

### Cloud & Platform Research
`aws-research`, `azure-research`, `gcp-research`, `platform-design`

### Governance & Compliance (UK Government)
`service-assessment`, `tcop`, `secure`, `mod-secure`, `dpia`, `ai-playbook`, `atrs`, `jsp-936`, `principles-compliance`, `conformance`, `analyze`, `traceability`, `impact`, `health`

### Procurement
`sow`, `dos`, `gcloud-search`, `gcloud-clarify`, `evaluate`, `score`

### Design Reviews & Delivery
`hld-review`, `dld-review`, `dld-review`, `devops`, `mlops`, `finops`, `servicenow`, `operationalize`, `data-mesh-contract`, `data-model`

### Government Reuse & Landscape
`gov-reuse`, `gov-code-search`, `gov-landscape`, `grants`

### Reporting
`story`, `presentation`, `pages`, `framework`, `glossary`, `search`

### Community (EU & French Government)
EU: `eu-ai-act`, `eu-nis2`, `eu-dora`, `eu-rgpd`, `eu-cra`, `eu-dsa`, `eu-data-act`
French: `fr-anssi`, `fr-rgpd`, `fr-secnumcloud`, `fr-dinum`, `fr-dr`, `fr-ebios`, `fr-pssi`, `fr-marche-public`, `fr-code-reuse`, `fr-anssi-carto`, `fr-algorithme-public`

## Project Structure

```
arckit-test-project-v17-fuel-prices/
├── .arckit/
│   ├── scripts/bash/          # Utility scripts (list-projects, create-project, etc.)
│   ├── templates/             # Markdown templates for artifact generation
│   └── memory/                # Session memory (session-learner hook)
├── .codex/prompts/arckit/     # Mirrored commands (Codex CLI)
├── .gemini/commands/arckit/   # Mirrored commands (Gemini CLI, TOML)
├── .mcp.json                  # MCP server config (AWS Knowledge, Microsoft Learn)
├── docs/                      # GitHub Pages site
│   ├── guides/                # 108 command guides + 18 DDaT role guides
│   ├── index.html             # Dashboard, sidebar, Mermaid renderer
│   ├── manifest.json          # Document index
│   ├── llms.txt               # LLM/agent index (llmstxt.org)
│   └── health.json            # Artifact health scan output
├── projects/
│   ├── 000-global/
│   │   └── ARC-000-PRIN-v1.0.md
│   └── 001-uk-fuel-price-transparency-service/
│       ├── ARC-001-*.md       # 27 core/governance artifacts (REQ, DATA, TCOP, ANAL, TRAC, ...)
│       ├── decisions/         # Architecture Decision Records (ADR-001 VE3 API)
│       ├── diagrams/          # Architecture diagrams (Mermaid / PlantUML)
│       ├── research/          # 22 research artefacts (AWS, Azure, GOVR, GLND, GCSR, RSCH, GRNT)
│       ├── tech-notes/        # 7 topic-specific tech notes
│       ├── vendors/           # 4 vendor profiles (VE3, AWS, GOV.UK Notify, OS)
│       └── external/          # Live CSV sample + GOV.UK factsheet
├── CHANGELOG.md
├── DEPENDENCY-MATRIX.md
├── WORKFLOW-DIAGRAMS.md
└── CLAUDE.md                  # AI assistant guidance for this repo
```

## Documentation

- [ArcKit Documentation](https://tractorjuice.github.io/arc-kit/)
- [Dependency Matrix](DEPENDENCY-MATRIX.md)
- [Workflow Diagrams](WORKFLOW-DIAGRAMS.md)
- [Changelog](CHANGELOG.md)
- [CMA Fuel Finder Enforcement Guidance](https://www.gov.uk/government/publications/fuel-finder-enforcement-guidance)
- [Motor Fuel Price (Open Data) Regulations 2025](https://www.legislation.gov.uk/ukdsi/2025)
