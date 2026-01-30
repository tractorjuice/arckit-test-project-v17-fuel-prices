# UK Government Fuel Price Transparency Service

**Architecture governance project for a government service consuming petrol and diesel price data via the CMA Fuel Finder open data scheme.**

## Project Context

The **Competition and Markets Authority (CMA)** established the [Fuel Finder](https://www.gov.uk/government/publications/fuel-finder-enforcement-guidance) open data scheme under the **Motor Fuel Price (Open Data) Regulations 2025**. This scheme requires fuel retailers to publish real-time pricing data to increase market transparency and help consumers find the cheapest fuel.

This project designs and governs a government service that:

- **Consumes** real-time petrol and diesel price data from the Fuel Finder open data scheme
- **Aggregates** fuel price data across regions, retailers, and fuel types
- **Publishes** price comparison tools and analytics for citizens and policy teams
- **Monitors** compliance with the Motor Fuel Price (Open Data) Regulations 2025
- **Reports** on fuel price trends to support CMA enforcement activity

## Key Stakeholders

| Stakeholder | Interest |
|-------------|----------|
| Competition and Markets Authority (CMA) | Enforcement of Fuel Finder regulations |
| Department for Energy Security & Net Zero (DESNZ) | Fuel market policy |
| Citizens / Motorists | Finding cheapest fuel prices |
| Fuel Retailers | Compliance with open data regulations |
| HM Treasury | Impact on cost of living / inflation |

## Regulatory Context

- **Motor Fuel Price (Open Data) Regulations 2025** - Mandates fuel price data publication
- **CMA Fuel Finder Enforcement Guidance** (December 2025) - How CMA uses enforcement powers
- **UK GDPR** - Data protection for any personal data in the pipeline
- **GDS Service Standard** - 14-point assessment for government digital services
- **Technology Code of Practice (TCoP)** - 13-point UK Government technology standards

## Getting Started

1. Start your AI assistant (Claude Code, Gemini CLI, or Codex CLI)
2. Run `/arckit.principles` to establish architecture governance
3. Run `/arckit.stakeholders` to analyze stakeholder drivers and goals
4. Run `/arckit.requirements` to define requirements for the fuel price service

## Available Commands

Once you start your AI assistant, you'll have access to these commands:

### Core Workflow
- `/arckit.principles` - Create or update architecture principles
- `/arckit.stakeholders` - Analyze stakeholder drivers, goals, and outcomes
- `/arckit.risk` - Create comprehensive risk register (Orange Book)
- `/arckit.sobc` - Create Strategic Outline Business Case (Green Book 5-case)
- `/arckit.requirements` - Define comprehensive requirements
- `/arckit.data-model` - Create data model with ERD, GDPR compliance, data governance
- `/arckit.research` - Research technology, services, and products with build vs buy analysis
- `/arckit.wardley` - Create strategic Wardley Maps for build vs buy and procurement strategy

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

### UK Government Compliance
- `/arckit.service-assessment` - GDS Service Standard assessment preparation
- `/arckit.tcop` - Technology Code of Practice assessment
- `/arckit.ai-playbook` - AI Playbook compliance for responsible AI
- `/arckit.dpia` - Data Protection Impact Assessment (UK GDPR Article 35)
- `/arckit.secure` - UK Government Secure by Design assessment

### Service Management
- `/arckit.servicenow` - Generate ServiceNow service design
- `/arckit.operationalize` - Create operational readiness pack with runbooks and DR/BCP
- `/arckit.traceability` - Generate requirements traceability matrix
- `/arckit.analyze` - Comprehensive governance quality analysis

## Project Structure

```
arckit-test-project-v17-fuel-prices/
├── .arckit/
│   ├── scripts/bash/
│   └── templates/
├── .claude/commands/
├── .codex/prompts/arckit/
├── .gemini/commands/arckit/
├── docs/
│   ├── guides/
│   └── README.md
├── projects/
│   ├── 000-global/
│   │   └── ARC-000-PRIN-v1.0.md
│   └── 001-fuel-price-service/
└── DEPENDENCY-MATRIX.md
```

## Documentation

- [ArcKit Documentation](https://tractorjuice.github.io/arc-kit/)
- [CMA Fuel Finder Enforcement Guidance](https://www.gov.uk/government/publications/fuel-finder-enforcement-guidance)
- [Motor Fuel Price (Open Data) Regulations 2025](https://www.legislation.gov.uk/ukdsi/2025)
