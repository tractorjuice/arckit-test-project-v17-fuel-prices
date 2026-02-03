# UK Government Fuel Price Transparency Service

**Architecture governance project for a government service consuming petrol and diesel price data via the CMA Fuel Finder open data scheme.**

Built with [ArcKit](https://tractorjuice.github.io/arc-kit/) — 43 AI-driven slash commands for architecture governance across Claude Code, Gemini CLI, and Codex CLI.

## Project Context

The **Competition and Markets Authority (CMA)** established the [Fuel Finder](https://www.gov.uk/government/publications/fuel-finder-enforcement-guidance) open data scheme under the **Motor Fuel Price (Open Data) Regulations 2025**. This scheme requires approximately 8,500 UK fuel retailers to publish real-time pricing data to increase market transparency and help consumers find the cheapest fuel.

This project designs and governs a government service that:

- **Consumes** real-time petrol and diesel price data from the Fuel Finder open data scheme
- **Aggregates** fuel price data across regions, retailers, and fuel types
- **Publishes** price comparison tools and analytics for citizens and policy teams
- **Monitors** compliance with the Motor Fuel Price (Open Data) Regulations 2025
- **Reports** on fuel price trends to support CMA enforcement and DESNZ policy activity

| | |
|---|---|
| **Classification** | OFFICIAL |
| **Hosting** | UK Government cloud (AWS UK / Azure UK regions) |

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

The project has produced the following architecture artifacts in `projects/`:

### Global Governance (`000-global/`)

| Document | Description |
|----------|-------------|
| `ARC-000-PRIN-v1.0.md` | Cross-project architecture principles |

### Fuel Price Service (`001-uk-fuel-price-transparency-service/`)

| Document | Description |
|----------|-------------|
| `ARC-001-PLAN-v1.0.md` | Project plan with timeline, phases, and gates |
| `ARC-001-STKE-v1.0.md` | Stakeholder drivers, goals, and outcomes |
| `ARC-001-RISK-v1.0.md` | Risk register (HM Treasury Orange Book) |
| `ARC-001-REQ-v1.0.md` | Business and technical requirements |
| `ARC-001-REQ-v2.0.md` | Requirements (updated) |
| `ARC-001-DATA-v1.0.md` | Data model with GDPR compliance |
| `ARC-001-RSCH-v1.0.md` | Technology research with build vs buy analysis |
| `ARC-001-SECD-v1.0.md` | Secure by Design assessment |
| `ARC-001-DPIA-v1.0.md` | Data Protection Impact Assessment |
| `ARC-001-BKLG-v1.0.md` | Prioritised product backlog |
| `ARC-001-DIAG-001-v1.0.md` | Architecture diagrams (Mermaid) |
| `ARC-001-AWRS-v1.0.md` | AWS services research |
| `ARC-001-AZRS-v1.0.md` | Azure services research |

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

43 slash commands are available across Claude Code, Gemini CLI, and Codex CLI:

### Core Workflow
- `/arckit.plan` - Create project plan with timeline and Mermaid diagrams
- `/arckit.principles` - Create or update architecture principles
- `/arckit.stakeholders` - Analyze stakeholder drivers, goals, and outcomes
- `/arckit.risk` - Create comprehensive risk register (Orange Book)
- `/arckit.sobc` - Create Strategic Outline Business Case (Green Book 5-case)
- `/arckit.requirements` - Define comprehensive requirements
- `/arckit.data-model` - Create data model with ERD, GDPR compliance, data governance
- `/arckit.research` - Research technology, services, and products with build vs buy analysis
- `/arckit.datascout` - Discover external data sources, APIs, and open data portals
- `/arckit.wardley` - Create strategic Wardley Maps for build vs buy and procurement strategy
- `/arckit.adr` - Document architectural decisions with options analysis

### Cloud Research
- `/arckit.aws-research` - Research AWS services using AWS Knowledge MCP
- `/arckit.azure-research` - Research Azure services using Microsoft Learn MCP

### Vendor Procurement
- `/arckit.sow` - Generate Statement of Work (RFP)
- `/arckit.dos` - Digital Outcomes and Specialists (DOS) procurement
- `/arckit.gcloud-search` - Search G-Cloud services on UK Digital Marketplace
- `/arckit.gcloud-clarify` - Validate G-Cloud services and generate clarification questions
- `/arckit.evaluate` - Create vendor evaluation framework and score vendors

### Design & Delivery
- `/arckit.diagram` - Generate visual architecture diagrams using Mermaid
- `/arckit.hld-review` - Review High-Level Design
- `/arckit.dld-review` - Review Detailed Design
- `/arckit.backlog` - Generate prioritised product backlog with GDS user stories
- `/arckit.devops` - Create DevOps strategy with CI/CD pipelines
- `/arckit.finops` - Create FinOps strategy for cloud cost management
- `/arckit.mlops` - Create MLOps strategy with model lifecycle and governance
- `/arckit.roadmap` - Create strategic architecture roadmap

### UK Government Compliance
- `/arckit.service-assessment` - GDS Service Standard assessment preparation
- `/arckit.tcop` - Technology Code of Practice assessment
- `/arckit.ai-playbook` - AI Playbook compliance for responsible AI
- `/arckit.dpia` - Data Protection Impact Assessment (UK GDPR Article 35)
- `/arckit.secure` - UK Government Secure by Design assessment
- `/arckit.mod-secure` - MOD Secure by Design assessment (CAAT)
- `/arckit.atrs` - Algorithmic Transparency Recording Standard
- `/arckit.jsp-936` - MOD JSP 936 AI assurance documentation
- `/arckit.principles-compliance` - Architecture principles compliance scorecard

### Service Management
- `/arckit.servicenow` - Generate ServiceNow service design
- `/arckit.operationalize` - Create operational readiness pack with runbooks and DR/BCP
- `/arckit.traceability` - Generate requirements traceability matrix
- `/arckit.analyze` - Comprehensive governance quality analysis
- `/arckit.data-mesh-contract` - Federated data product contracts
- `/arckit.platform-design` - Platform strategy using Platform Design Toolkit

### Reporting
- `/arckit.story` - Generate project story with timeline and governance achievements
- `/arckit.pages` - Generate GitHub Pages site for project documentation

## Project Structure

```
arckit-test-project-v17-fuel-prices/
├── .arckit/
│   ├── scripts/bash/          # Utility scripts (list-projects, create-project, etc.)
│   └── templates/             # 44 markdown templates for artifact generation
├── .claude/commands/          # 43 ArcKit slash commands (Claude Code)
├── .codex/prompts/arckit/     # Mirrored commands (Codex CLI)
├── .gemini/commands/arckit/   # Mirrored commands (Gemini CLI, TOML)
├── .mcp.json                  # MCP server config (AWS Knowledge, Microsoft Learn)
├── docs/                      # GitHub Pages site
│   ├── guides/                # 30+ implementation guides
│   └── index.html
├── projects/
│   ├── 000-global/
│   │   └── ARC-000-PRIN-v1.0.md
│   └── 001-uk-fuel-price-transparency-service/
│       ├── ARC-001-*.md       # 10 architecture artifacts
│       ├── diagrams/          # Architecture diagrams
│       ├── research/          # AWS and Azure research
│       ├── decisions/         # Architecture Decision Records
│       ├── wardley-maps/      # Wardley Maps
│       ├── data-contracts/    # Data product contracts
│       ├── reviews/           # HLD/DLD reviews
│       ├── vendors/           # Vendor evaluations
│       └── final/             # Final deliverables
├── CHANGELOG.md
├── DEPENDENCY-MATRIX.md
├── WORKFLOW-DIAGRAMS.md
└── VERSION
```

## Documentation

- [ArcKit Documentation](https://tractorjuice.github.io/arc-kit/)
- [Dependency Matrix](DEPENDENCY-MATRIX.md)
- [Workflow Diagrams](WORKFLOW-DIAGRAMS.md)
- [Changelog](CHANGELOG.md)
- [CMA Fuel Finder Enforcement Guidance](https://www.gov.uk/government/publications/fuel-finder-enforcement-guidance)
- [Motor Fuel Price (Open Data) Regulations 2025](https://www.legislation.gov.uk/ukdsi/2025)
