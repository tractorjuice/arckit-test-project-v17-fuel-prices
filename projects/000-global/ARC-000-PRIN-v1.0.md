# UK Government Fuel Price Transparency Service — Enterprise Architecture Principles

> **Template Status**: Live | **Version**: 1.0.3 | **Command**: `/arckit.principles`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-000-PRIN-v1.0 |
| **Document Type** | Enterprise Architecture Principles |
| **Project** | UK Government Fuel Price Transparency Service (Project 000 — Global) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-01-30 |
| **Last Modified** | 2026-01-30 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-04-30 |
| **Owner** | Enterprise Architect, Architecture Review Board |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, DESNZ Policy, GDS Assessors, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-30 | ArcKit AI | Initial creation from `/arckit.principles` command | PENDING | PENDING |

---

## Executive Summary

This document establishes the architecture principles governing all technology decisions for the UK Government Fuel Price Transparency Service ("Fuel Finder"). The service operates under the Motor Fuel Price (Open Data) Regulations 2025, ingesting real-time pricing data from approximately 8,500 UK fuel stations and presenting it to citizens, the Competition and Markets Authority (CMA), and the Department for Energy Security and Net Zero (DESNZ).

These principles reflect the obligations of a UK Government digital service: compliance with the GDS Service Standard, the Technology Code of Practice (TCoP), UK GDPR, Secure by Design, and HM Treasury Green Book / Orange Book governance frameworks.

**Scope**: All technology projects, systems, and initiatives within the Fuel Price Transparency Service programme
**Authority**: Architecture Review Board, Senior Responsible Owner (SRO)
**Compliance**: Mandatory unless exception approved through the documented exception process

**Philosophy**: These principles are **technology-agnostic** — they describe WHAT qualities the architecture must have, not HOW to implement them with specific products. Technology selection happens during research and design phases guided by these principles.

---

## I. Strategic Principles

### 1. Open Data by Default

**Principle Statement**:
All fuel price data collected under the Motor Fuel Price (Open Data) Regulations 2025 MUST be published as open data in machine-readable formats, accessible without registration or payment, unless a specific exemption applies.

**Rationale**:
The Fuel Finder exists to increase market transparency for consumers and enable competition analysis. The CMA's open data scheme mandates that fuel pricing data is freely available. Open data publication is a legal obligation, not an optional feature.

**Implications**:
- Data publication pipelines are a first-class architectural concern, not an afterthought
- Published datasets MUST use open, non-proprietary formats
- APIs MUST be documented to open standards with public specification
- Licensing MUST use the Open Government Licence (OGL) or equivalent
- Historical data MUST be retained and accessible for trend analysis
- Bulk download capability alongside real-time API access

**Validation Gates**:
- [ ] Fuel price data published in at least one machine-readable open format
- [ ] API specification publicly available and versioned
- [ ] No registration or payment barrier to access open data
- [ ] Open Government Licence applied to published datasets
- [ ] Bulk download and API access both available

---

### 2. Citizen-Centred Design

**Principle Statement**:
All user-facing services MUST be designed around verified user needs, following the GDS Service Standard's 14 points, and MUST be accessible to all users including those with disabilities.

**Rationale**:
The service exists to help motorists find affordable fuel. GDS Service Standard assessment is mandatory for government digital services. Accessibility is a legal requirement under the Public Sector Bodies (Websites and Mobile Applications) Accessibility Regulations 2018.

**Implications**:
- User research with real motorists and fuel retailers before and during development
- Iterative design through Discovery, Alpha, Beta, and Live phases
- Accessibility compliance to WCAG 2.2 AA as a minimum
- Support for users with low digital confidence
- Performance budgets ensuring usability on low-bandwidth connections and older devices
- Assisted digital support for users unable to use the online service

**Validation Gates**:
- [ ] User research conducted with representative user groups
- [ ] GDS Service Standard self-assessment completed at each phase gate
- [ ] WCAG 2.2 AA compliance verified through automated and manual testing
- [ ] Performance tested on low-bandwidth connections
- [ ] Assisted digital channel available

---

### 3. Scalability and Elasticity

**Principle Statement**:
All systems MUST be designed to scale horizontally to meet demand, handling peak loads (e.g., fuel price spikes driving public interest) without degradation.

**Rationale**:
Fuel price events (e.g., supply disruptions, budget announcements, media coverage) cause unpredictable traffic spikes. The service must absorb these without manual intervention. Approximately 8,500 stations submit data, and millions of citizens may query it simultaneously during high-interest periods.

**Implications**:
- Design for stateless components that can be replicated
- Avoid hard-coded limits or fixed capacity assumptions
- Plan for distributed deployment across multiple compute nodes
- Use load balancing to distribute traffic across instances
- Implement auto-scaling based on demand metrics
- Separate data ingestion (retailer submissions) from data serving (citizen queries) to scale independently

**Validation Gates**:
- [ ] System can scale horizontally (add more instances)
- [ ] No single points of failure that limit scaling
- [ ] Load testing demonstrates capacity growth with added resources
- [ ] Scaling metrics and triggers defined
- [ ] Cost model accounts for variable capacity
- [ ] Ingestion and serving tiers scale independently

---

### 4. Resilience and Fault Tolerance

**Principle Statement**:
All systems MUST gracefully degrade when dependencies fail and recover automatically without data loss or manual intervention. Fuel price data ingestion MUST continue even when citizen-facing services are degraded.

**Rationale**:
Failures are inevitable in distributed systems. Retailer data submissions operate on regulatory deadlines — lost submissions create compliance gaps. Citizens depend on accurate, current pricing data. The architecture must assume failures will occur and design for resilience.

**Implications**:
- Implement circuit breakers for external dependencies
- Use timeouts on all network calls
- Retry with exponential backoff for transient failures
- Graceful degradation: serve stale data with clear staleness indicators rather than errors
- Automated health checks and recovery
- Avoid cascading failures through bulkhead isolation
- Data ingestion pipeline isolated from query-serving infrastructure

**Validation Gates**:
- [ ] Failure modes identified and mitigated for each component
- [ ] Chaos engineering or fault injection testing performed
- [ ] Recovery Time Objective (RTO) and Recovery Point Objective (RPO) defined
- [ ] Automated failover tested
- [ ] Degraded mode behaviour documented and tested
- [ ] Data ingestion continues during citizen-facing outages

---

### 5. Interoperability and Integration

**Principle Statement**:
All systems MUST expose functionality through well-defined, versioned interfaces using industry-standard protocols. Direct database access across system boundaries is prohibited. Integration with cross-government platforms (e.g., GOV.UK, Notify, Pay) MUST use their published APIs.

**Rationale**:
Loose coupling through standard interfaces enables independent evolution, technology diversity, and composability with the wider government digital ecosystem.

**Implications**:
- Use standardised protocols for all system interfaces
- Version all interfaces with backward compatibility strategy
- Publish interface specifications (API contracts, event schemas)
- No direct database access across system boundaries
- Asynchronous communication for non-real-time interactions
- Align with cross-government API standards and the API Design Guidance

**Validation Gates**:
- [ ] Interface specifications published (OpenAPI, AsyncAPI, or equivalent)
- [ ] Versioning strategy defined with deprecation policy
- [ ] Authentication and authorisation model documented
- [ ] Error handling and retry behaviour specified
- [ ] No direct database coupling across systems
- [ ] Cross-government platform integrations use published APIs

---

### 6. Security by Design (NON-NEGOTIABLE)

**Principle Statement**:
All architectures MUST implement defence-in-depth security with zero-trust principles. Security is NOT a feature to be added later — it is a foundational requirement. The service MUST meet NCSC Secure by Design principles and operate at OFFICIAL classification.

**Rationale**:
The Fuel Finder processes business-sensitive commercial data (retailer pricing, forecourt details) and serves a public-interest function. Compromise could undermine market transparency or expose commercially sensitive timing of price changes. UK Government Secure by Design is mandatory.

**Zero Trust Pillars**:
1. **Identity-Based Access**: No network-based trust; every request authenticated
2. **Least Privilege**: Grant minimum necessary permissions, time-boxed where possible
3. **Encryption Everywhere**: Data encrypted in transit and at rest
4. **Continuous Verification**: Monitor, log, and analyse all access patterns

**Mandatory Controls**:
- [ ] Multi-factor authentication for all administrative and retailer access
- [ ] Service-to-service authentication (mutual authentication or signed tokens)
- [ ] Secrets management via secure vault (never in code or config files)
- [ ] Network segmentation with minimal trust zones
- [ ] Encryption at rest for all data stores
- [ ] Encrypted transport for all network communication
- [ ] Structured logging of all authentication/authorisation events
- [ ] Regular security testing (penetration testing, vulnerability scanning)
- [ ] OFFICIAL classification handling procedures applied

**Compliance Frameworks**:
- NCSC Secure by Design
- NCSC Cyber Assessment Framework (CAF)
- UK Government Security Classification Policy (OFFICIAL)
- Cyber Essentials Plus

**Exceptions**:
- NONE. Security principles are non-negotiable.
- Specific control implementations may vary with compensating controls approved by the SIRO.

**Validation Gates**:
- [ ] Threat model completed and reviewed
- [ ] Security controls mapped to requirements
- [ ] Secure by Design assessment completed
- [ ] Penetration testing conducted before Live
- [ ] Incident response runbook created
- [ ] SIRO sign-off obtained

---

### 7. Observability and Operational Excellence

**Principle Statement**:
All systems MUST emit structured telemetry (logs, metrics, traces) enabling real-time monitoring, troubleshooting, and capacity planning. Data freshness — the time between a retailer submitting a price and it being available to citizens — MUST be monitored as a primary service metric.

**Rationale**:
We cannot operate what we cannot observe. For a regulatory data service, the ability to detect and diagnose data staleness, ingestion failures, or quality degradation is as critical as uptime. Instrumentation is a first-class architectural requirement.

**Telemetry Requirements**:
- **Logging**: Structured logs with correlation IDs across ingestion and serving pipelines
- **Metrics**: Request volume, latency percentiles (p50, p95, p99), error rates, data freshness
- **Tracing**: Distributed trace context for request flows
- **Alerting**: SLO-based alerting with actionable runbooks

**Required Instrumentation**:
- Request volume, latency distribution, error rate
- Data ingestion rate, pipeline lag, submission completeness
- Resource utilisation (CPU, memory, I/O, network)
- Business metrics (stations reporting, price update frequency, coverage gaps)
- Security events (authentication failures, policy violations, suspicious patterns)

**Log Retention**:
- **Security/audit logs**: Minimum 12 months (aligned with NCSC guidance)
- **Application logs**: 90 days for troubleshooting
- **Metrics**: 2 years with aggregation for capacity planning and trend analysis

**Validation Gates**:
- [ ] Logging, metrics, tracing instrumented across all components
- [ ] Dashboards and alerts configured
- [ ] SLOs and SLIs defined (including data freshness SLI)
- [ ] Runbooks created for common failure scenarios
- [ ] Capacity planning metrics tracked

---

## II. Data Principles

### 8. Data Sovereignty and Governance

**Principle Statement**:
All data MUST be stored and processed within UK sovereign territory. Data classification, residency, retention, and access controls MUST comply with UK GDPR, the Data Protection Act 2018, and UK Government data governance policies.

**Rationale**:
As a UK Government service handling regulatory data and limited personal data (retailer contact information), data sovereignty is non-negotiable. Post-Brexit data adequacy arrangements do not remove the obligation to store government data within UK jurisdiction.

**Data Classification**:
1. **OFFICIAL — PUBLIC**: Published fuel prices, forecourt locations, aggregated statistics
2. **OFFICIAL**: Retailer account details, submission metadata, internal operational data
3. **OFFICIAL — SENSITIVE**: Enforcement case data, CMA investigation material, retailer compliance records

**Data Residency**:
- All data MUST reside in UK-based data centres
- No cross-border data transfers for operational data
- Third-party services MUST process data within UK jurisdiction

**Data Retention**:
- Published fuel price data: Retained indefinitely as public record
- Retailer account data: Duration of registration plus 6 years
- Audit logs: Minimum 12 months
- Enforcement data: As directed by CMA legal requirements
- Automatic deletion after defined retention period for non-permanent data

**Validation Gates**:
- [ ] All data stores located within UK sovereign territory
- [ ] Data classification performed for all data entities
- [ ] Retention policies configured with automated deletion where applicable
- [ ] Access controls enforce least privilege and need-to-know
- [ ] Data Protection Impact Assessment (DPIA) completed

---

### 9. Data Quality and Timeliness

**Principle Statement**:
Fuel price data MUST meet defined quality standards for completeness, accuracy, and timeliness. Data quality issues MUST be detected, reported, and escalated automatically — poor data quality directly undermines the regulatory purpose of the service.

**Rationale**:
The CMA's enforcement powers depend on accurate, timely data. Citizens making purchasing decisions need trustworthy information. The Motor Fuel Price (Open Data) Regulations 2025 place obligations on retailers to submit accurate data within defined timeframes.

**Quality Standards**:
- **Completeness**: All required fields present; coverage across registered forecourts monitored
- **Accuracy**: Validation rules enforced at submission (e.g., price within plausible range)
- **Timeliness**: Freshness SLA from price change to publication defined and monitored
- **Consistency**: Cross-field validation (e.g., fuel type matches available pumps)

**Lineage Requirements**:
- Source-to-publication mapping documented for all data flows
- Transformation logic version-controlled and reviewable
- Data quality metrics tracked per pipeline stage
- Impact analysis capability for schema changes
- Retailer submission provenance retained for enforcement purposes

**Validation Gates**:
- [ ] Data quality rules defined and automated at ingestion
- [ ] Quality metrics dashboard available to operations and CMA
- [ ] Data freshness SLA defined and monitored
- [ ] Anomaly detection for suspicious price submissions
- [ ] Schema evolution strategy documented

---

### 10. Single Source of Truth

**Principle Statement**:
The Fuel Finder service MUST be the single authoritative source for regulated UK fuel pricing data. Derived copies MUST be clearly labelled and synchronised.

**Rationale**:
Multiple authoritative sources create inconsistency and undermine the regulatory purpose. CMA enforcement and citizen trust depend on a single canonical dataset.

**Implications**:
- The ingestion pipeline is the system of record for submitted fuel prices
- Published open data is a derived, read-optimised view — not a separate source
- Third-party consumers (comparison sites, apps) consume from the published API
- No bidirectional synchronisation with external systems
- Aggregated and analytical views clearly labelled as derived

**Validation Gates**:
- [ ] System of record identified for each data entity
- [ ] Derived copies documented with synchronisation frequency
- [ ] No bidirectional sync without conflict resolution strategy
- [ ] Third-party consumers use the published API, not internal data stores

---

## III. Integration Principles

### 11. Loose Coupling

**Principle Statement**:
Systems MUST be loosely coupled through published interfaces, avoiding shared databases, file systems, or tight runtime dependencies. The data ingestion pipeline, processing engine, publication layer, and enforcement tools MUST be independently deployable.

**Rationale**:
Loose coupling enables independent deployment, technology diversity, team autonomy, and system evolution. Different parts of the service have different change velocities — enforcement tools evolve with regulation; citizen-facing interfaces evolve with user needs.

**Implications**:
- Communicate through published APIs or asynchronous events
- No direct database access across system boundaries
- Each subsystem manages its own data lifecycle
- Shared libraries kept minimal (favour duplication over coupling)
- Avoid distributed transactions across systems

**Validation Gates**:
- [ ] Systems communicate via APIs or events, not database queries
- [ ] No shared mutable state across subsystems
- [ ] Each subsystem has independent data store
- [ ] Deployment of one subsystem does not require deployment of another
- [ ] Interface changes versioned with backward compatibility

---

### 12. Asynchronous Communication for Data Pipelines

**Principle Statement**:
Data ingestion and processing pipelines SHOULD use asynchronous, event-driven communication to decouple retailers' submission experience from downstream processing and publication.

**Rationale**:
Asynchronous patterns reduce temporal coupling, improve fault tolerance, and enable better scalability. A retailer submitting a price update should receive acknowledgement immediately, while processing, validation, and publication proceed asynchronously.

**When to Use Async**:
- Retailer data submissions (acknowledge receipt, process asynchronously)
- Data validation and enrichment pipelines
- Publication to open data endpoints
- Notifications to CMA enforcement systems
- Batch analytics and reporting

**When Synchronous is Acceptable**:
- Citizen-facing price lookup queries (read-only, low-latency)
- Retailer authentication and session management
- Health check and status endpoints

**Validation Gates**:
- [ ] Async patterns used for data ingestion and processing
- [ ] Message durability and delivery guarantees defined
- [ ] Event schemas versioned and published
- [ ] Dead letter handling and error escalation configured
- [ ] Submission acknowledgement returned synchronously, processing async

---

### 13. Reuse Government Platforms

**Principle Statement**:
The service MUST reuse existing cross-government platforms and shared services (e.g., GOV.UK, GOV.UK Notify, GOV.UK Pay, GOV.UK One Login) where they meet user needs, rather than building bespoke equivalents.

**Rationale**:
The Technology Code of Practice mandates reuse of government shared platforms. These platforms are already assured, accessible, and maintained at scale. Building bespoke alternatives wastes public money and creates maintenance burden.

**Implications**:
- Evaluate Government as a Platform (GaaP) services before building custom components
- Use GOV.UK design patterns and the GOV.UK Design System for citizen-facing interfaces
- Use GOV.UK Notify for emails, SMS, and letters to retailers
- Use GOV.UK One Login for citizen identity (if identity verification is needed)
- Architecture must accommodate integration with these platforms

**Validation Gates**:
- [ ] Cross-government platform assessment completed (build vs reuse)
- [ ] GOV.UK Design System used for citizen-facing interfaces
- [ ] GOV.UK Notify used for notifications
- [ ] Justification documented for any bespoke build where a shared platform exists
- [ ] TCoP compliance assessment includes platform reuse evidence

---

## IV. Quality Attributes

### 14. Performance and Efficiency

**Principle Statement**:
All systems MUST meet defined performance targets under expected load with efficient use of computational resources. Citizen-facing price lookups MUST return results within defined latency targets.

**Performance Targets** (define for each system):
- **Response Time**: p50, p95, p99 latency targets for citizen queries
- **Throughput**: Concurrent retailer submissions; citizen queries per second
- **Data Freshness**: Time from retailer submission to public availability
- **Resource Efficiency**: Cost-per-query and cost-per-ingestion metrics

**Implications**:
- Performance requirements defined before implementation
- Load testing performed before production deployment
- Performance monitoring continuous, not just point-in-time
- Caching strategies for read-heavy citizen queries
- Efficient data structures for geographic and price-range queries

**Validation Gates**:
- [ ] Performance requirements defined with measurable targets
- [ ] Load testing performed at expected and peak capacity
- [ ] Performance metrics monitored in production
- [ ] Data freshness SLA met under load
- [ ] Cost efficiency tracked against usage growth

---

### 15. Availability and Reliability

**Principle Statement**:
All systems MUST meet defined availability targets with automated recovery and minimal data loss. The data ingestion endpoint MUST be highly available to avoid retailers being unable to meet their regulatory obligations.

**Availability Targets** (define for each system):
- **Uptime SLA**: Citizen-facing service and retailer submission endpoint
- **Recovery Time Objective (RTO)**: Maximum acceptable downtime
- **Recovery Point Objective (RPO)**: Maximum acceptable data loss

**High Availability Patterns**:
- Redundancy across availability zones within UK regions
- Automated health checks and failover
- Active-active or active-passive configurations
- Regular disaster recovery testing
- Maintenance windows communicated in advance to retailers

**Validation Gates**:
- [ ] Availability SLA defined for each tier (ingestion, serving, admin)
- [ ] RTO and RPO requirements documented
- [ ] Redundancy strategy implemented
- [ ] Failover tested regularly
- [ ] Backup and restore procedures validated
- [ ] Disaster recovery plan tested at least annually

---

### 16. Maintainability and Evolvability

**Principle Statement**:
All systems MUST be designed for change, with clear separation of concerns, modular architecture, and comprehensive documentation. The regulatory landscape will evolve — the architecture must accommodate changes to data requirements, enforcement rules, and reporting obligations without wholesale redesign.

**Rationale**:
The Motor Fuel Price Regulations may be amended. CMA enforcement approaches will mature. New fuel types (hydrogen, EV charging) may be added. The architecture must support these changes incrementally.

**Implications**:
- Modular architecture with clear boundaries
- Separation of concerns (business logic, data access, presentation)
- Configuration-driven rules for validation and business logic where practical
- Architecture Decision Records (ADRs) for significant choices
- Automated testing to enable confident refactoring

**Validation Gates**:
- [ ] Architecture documentation exists and is current
- [ ] Module boundaries clear with defined responsibilities
- [ ] Automated test coverage enables safe refactoring
- [ ] ADRs document key choices
- [ ] Regulatory change impact assessment process defined

---

## V. Development Practices

### 17. Infrastructure as Code

**Principle Statement**:
All infrastructure MUST be defined as code, version-controlled, and deployed through automated pipelines. No manual changes to any environment.

**Rationale**:
Manual infrastructure changes create drift, inconsistency, and undocumented state. Infrastructure as Code (IaC) enables repeatability, auditability, and disaster recovery — critical for a government service that must demonstrate governance and compliance.

**Implications**:
- All infrastructure defined in declarative code
- Infrastructure changes go through code review
- Environments are reproducible from code
- No manual changes to production infrastructure ("ClickOps" prohibited)
- Infrastructure versioned alongside application code

**Validation Gates**:
- [ ] Infrastructure defined as code in version control
- [ ] Automated deployment pipeline for infrastructure
- [ ] No manual infrastructure changes in any environment
- [ ] Environment parity (dev/staging/production) maintained through IaC

---

### 18. Automated Testing

**Principle Statement**:
All code changes MUST be validated through automated testing before deployment to production. Data quality validation rules MUST have their own test suites.

**Test Pyramid**:
- **Unit Tests**: Fast, isolated, high coverage (70–80% of tests)
- **Integration Tests**: Test component interactions (15–20% of tests)
- **End-to-End Tests**: Critical user journeys (5–10% of tests)

**Required Test Types**:
- Functional tests (does it work?)
- Performance tests (is it fast enough under load?)
- Security tests (SAST, DAST, dependency scanning)
- Data quality tests (do validation rules catch bad submissions?)
- Accessibility tests (automated WCAG checks)

**Validation Gates**:
- [ ] Automated tests exist and pass before merge
- [ ] Test coverage meets defined thresholds
- [ ] Critical paths have end-to-end tests
- [ ] Security scanning integrated into pipeline
- [ ] Accessibility checks automated where possible

---

### 19. Continuous Integration and Deployment

**Principle Statement**:
All code changes MUST go through automated build, test, and deployment pipelines with quality gates at each stage. Deployments to production MUST be automated, auditable, and reversible.

**Pipeline Stages**:
1. **Source Control**: All changes committed to version control
2. **Build**: Automated compilation and packaging
3. **Test**: Automated test execution (unit, integration, security, accessibility)
4. **Security Scan**: Dependency and code vulnerability scanning
5. **Deployment**: Automated deployment to environments
6. **Verification**: Post-deployment smoke tests and canary checks

**Quality Gates**:
- All tests must pass
- No critical or high security vulnerabilities
- Code review approval required
- Deployment requires production readiness checklist
- Rollback tested and documented

**Validation Gates**:
- [ ] Automated CI/CD pipeline exists
- [ ] Pipeline includes security scanning
- [ ] Deployment is automated and repeatable
- [ ] Rollback capability tested
- [ ] Deployment audit trail maintained

---

## VI. Regulatory and Government-Specific Principles

### 20. Regulatory Compliance by Design

**Principle Statement**:
The architecture MUST be designed to support CMA enforcement activities, including audit trails, evidence preservation, and compliance reporting. Regulatory requirements MUST be traceable to architectural decisions.

**Rationale**:
The Motor Fuel Price (Open Data) Regulations 2025 grant CMA enforcement powers. The service must generate evidence of retailer compliance (or non-compliance) that is admissible and auditable. The enforcement grace period (until early May 2026) means the architecture must support both supportive onboarding and formal enforcement from day one.

**Implications**:
- Immutable audit trail for all retailer submissions (timestamp, content, source)
- Non-repudiation: ability to prove a retailer did or did not submit data
- Evidence preservation: submissions retained in tamper-evident storage
- Compliance dashboards for CMA showing submission rates, timeliness, and coverage
- Separation of operational data from enforcement/investigation data

**Validation Gates**:
- [ ] Audit trail captures all retailer submissions with timestamp and provenance
- [ ] Tamper-evident storage for enforcement evidence
- [ ] Compliance reporting available to CMA
- [ ] Data retention meets CMA legal requirements
- [ ] Separation between operational and enforcement data access

---

### 21. Privacy by Design

**Principle Statement**:
Personal data processing MUST be minimised, purpose-limited, and compliant with UK GDPR and the Data Protection Act 2018. A Data Protection Impact Assessment (DPIA) MUST be completed before processing personal data.

**Rationale**:
The service processes limited personal data (retailer contact details, potentially fuel station operator names). Privacy by design is a legal obligation under UK GDPR Article 25.

**Implications**:
- Collect only the minimum personal data necessary for the regulatory purpose
- Clear lawful basis identified for each processing activity (likely public task under Article 6(1)(e))
- Privacy notices provided to retailers at point of data collection
- Data subject rights (access, rectification, erasure) implementable
- Pseudonymisation or anonymisation applied where full identification is unnecessary
- DPIA completed and reviewed by DPO

**Validation Gates**:
- [ ] DPIA completed before processing personal data
- [ ] Lawful basis documented for each processing activity
- [ ] Privacy notices published
- [ ] Data subject rights processes operational
- [ ] Data minimisation verified — no unnecessary personal data collected
- [ ] DPO review completed

---

### 22. Sustainability and Cost Efficiency

**Principle Statement**:
Architecture decisions MUST consider environmental sustainability and cost efficiency. Public money MUST be spent wisely, and the service SHOULD minimise its carbon footprint in line with the Greening Government ICT and Digital Services Strategy.

**Rationale**:
UK Government services are expected to demonstrate value for money (HM Treasury Green Book) and contribute to net-zero targets. Cloud resource over-provisioning wastes both money and energy.

**Implications**:
- Right-size compute resources; avoid persistent over-provisioning
- Use auto-scaling to match resource consumption to actual demand
- Select energy-efficient architectures (serverless, managed services) where appropriate
- Monitor and report on carbon emissions from infrastructure
- Design data retention policies to avoid storing data beyond its useful life
- Regular cost reviews and optimisation

**Validation Gates**:
- [ ] Cost model defined with forecasts at expected and peak usage
- [ ] Auto-scaling configured to avoid idle resources
- [ ] Carbon impact considered in architecture decisions
- [ ] Regular cost optimisation reviews scheduled
- [ ] Data retention prevents unnecessary storage growth

---

## VII. Exception Process

### Requesting Architecture Exceptions

Principles are mandatory unless a documented exception is approved by the Architecture Review Board and, for security principles, the Senior Information Risk Owner (SIRO).

**Valid Exception Reasons**:
- Technical constraints that prevent compliance
- Regulatory or legal requirements that conflict
- Transitional state during migration (time-bound)
- Pilot/proof-of-concept with defined end date

**Exception Request Requirements**:
- [ ] Justification with business/technical rationale
- [ ] Alternative approach and compensating controls
- [ ] Risk assessment and mitigation plan
- [ ] Expiration date (exceptions are time-bound, maximum 6 months)
- [ ] Remediation plan to achieve compliance

**Approval Process**:
1. Submit exception request to Architecture Review Board
2. Review by architecture peers
3. SIRO approval required for security principle exceptions
4. SRO approval for any principle rated CRITICAL
5. Document exception in project architecture documentation
6. Quarterly review of all active exceptions

---

## VIII. Governance and Compliance

### Architecture Review Gates

All projects must pass architecture reviews at key milestones aligned with the GDS service phases:

**Discovery**:
- [ ] Architecture principles understood by delivery team
- [ ] High-level approach aligns with principles
- [ ] No obvious principle violations in proposed direction

**Alpha**:
- [ ] Prototype architecture reviewed against principles
- [ ] Technology choices justified against principles (not the reverse)
- [ ] Exceptions identified and submitted early
- [ ] GDS Service Standard alignment confirmed

**Beta (Private and Public)**:
- [ ] Detailed architecture documented
- [ ] Compliance with each principle validated with evidence
- [ ] Exceptions approved and documented
- [ ] Security and data principles validated (Secure by Design assessment)
- [ ] Performance and resilience testing completed

**Live / Pre-Production**:
- [ ] Implementation matches approved architecture
- [ ] All validation gates passed
- [ ] Operational readiness verified
- [ ] GDS Service Assessment passed
- [ ] SIRO sign-off for go-live

### Enforcement

- Architecture reviews are **mandatory** at each phase gate
- Principle violations must be remediated before production deployment
- Approved exceptions are time-bound (maximum 6 months) and reviewed quarterly
- Post-live compliance reviews conducted annually
- Non-compliance escalated to SRO

---

## IX. Appendix

### Principle Summary Checklist

| # | Principle | Category | Criticality | Validation |
|---|-----------|----------|-------------|------------|
| 1 | Open Data by Default | Strategic | CRITICAL | Open format, public API, OGL |
| 2 | Citizen-Centred Design | Strategic | CRITICAL | User research, WCAG 2.2 AA, GDS assessment |
| 3 | Scalability and Elasticity | Strategic | HIGH | Load testing, auto-scaling |
| 4 | Resilience and Fault Tolerance | Strategic | CRITICAL | Chaos testing, RTO/RPO |
| 5 | Interoperability and Integration | Strategic | HIGH | API specs, versioning |
| 6 | Security by Design | Strategic | CRITICAL | Threat model, pen testing, Secure by Design |
| 7 | Observability | Strategic | HIGH | Metrics, logs, traces, data freshness SLI |
| 8 | Data Sovereignty and Governance | Data | CRITICAL | UK residency, classification, DPIA |
| 9 | Data Quality and Timeliness | Data | CRITICAL | Quality rules, freshness SLA |
| 10 | Single Source of Truth | Data | HIGH | Data lineage, canonical dataset |
| 11 | Loose Coupling | Integration | HIGH | Independent deployment |
| 12 | Asynchronous Communication | Integration | MEDIUM | Async ingestion pipeline |
| 13 | Reuse Government Platforms | Integration | HIGH | GaaP assessment, TCoP compliance |
| 14 | Performance and Efficiency | Quality | HIGH | Load testing, latency targets |
| 15 | Availability and Reliability | Quality | CRITICAL | SLA monitoring, DR testing |
| 16 | Maintainability and Evolvability | Quality | MEDIUM | ADRs, modular design |
| 17 | Infrastructure as Code | DevOps | HIGH | IaC coverage, no manual changes |
| 18 | Automated Testing | DevOps | HIGH | Test coverage, security scanning |
| 19 | CI/CD | DevOps | HIGH | Pipeline exists, rollback tested |
| 20 | Regulatory Compliance by Design | Government | CRITICAL | Audit trail, evidence preservation |
| 21 | Privacy by Design | Government | CRITICAL | DPIA, UK GDPR compliance |
| 22 | Sustainability and Cost Efficiency | Government | MEDIUM | Cost model, carbon impact |

### Applicable Standards and Frameworks

| Standard | Relevance |
|----------|-----------|
| GDS Service Standard (14 points) | Mandatory for government digital services |
| Technology Code of Practice (TCoP) | Mandatory for government technology |
| UK GDPR / Data Protection Act 2018 | Personal data processing |
| NCSC Secure by Design | Security architecture |
| NCSC Cyber Assessment Framework | Security assurance |
| HM Treasury Green Book | Business case and value for money |
| HM Treasury Orange Book | Risk management |
| Motor Fuel Price (Open Data) Regulations 2025 | Primary regulatory basis |
| Public Sector Bodies Accessibility Regulations 2018 | Accessibility |
| Open Government Licence (OGL) | Data publication |
| Greening Government ICT Strategy | Sustainability |

---

**Generated by**: ArcKit `/arckit.principles` command
**Generated on**: 2026-01-30
**ArcKit Version**: 1.0.3
**Project**: UK Government Fuel Price Transparency Service (Project 000)
**AI Model**: Claude Opus 4.5
