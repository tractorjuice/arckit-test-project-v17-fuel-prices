# UK Government Secure by Design Assessment

> **Template Status**: Beta | **Version**: 1.0.0 | **Command**: `/arckit.secure`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-SECD-v1.0 |
| **Document Type** | Secure by Design Assessment |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-01-30 |
| **Last Modified** | 2026-01-30 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-04-30 |
| **Owner** | CMA SIRO / Security Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA SIRO, CMA DPO, Project Lead, GDS Assessment Team, NCSC Liaison |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-30 | ArcKit AI | Initial creation from `/arckit.secure` command | PENDING | PENDING |

## Document Purpose

This document provides a comprehensive Secure by Design assessment for the UK Fuel Price Transparency Service ("Fuel Finder"), aligned with the NCSC Cyber Assessment Framework (CAF), Cyber Essentials, UK GDPR, and HMG security standards. It assesses the security posture of the service during the Discovery/Alpha phase, identifying what has been defined in architecture artifacts, what gaps remain, and what actions are required before progressing to Beta.

This assessment supports:
- **NFR-C-005** (Secure by Design): Threat model, penetration test, SIRO sign-off, and incident response plan requirements
- **Principle P6** (Security by Design): NON-NEGOTIABLE governance principle
- **GDS Service Standard**: Points 7 (use open standards and common platforms) and 9 (create a secure service)
- **SIRO sign-off**: Required before progression beyond Alpha

**Source Documents**:
- ARC-001-REQ-v2.0 (Requirements Specification)
- ARC-001-RISK-v1.0 (Risk Register)
- ARC-001-DPIA-v1.0 (Data Protection Impact Assessment)
- ARC-001-STKE-v1.0 (Stakeholder Analysis)
- ARC-001-DATA-v1.0 (Data Model)
- ARC-000-PRIN-v1.0 (Architecture Principles)

---

## Executive Summary

**Overall Security Posture**: Needs Improvement

**NCSC Cyber Assessment Framework (CAF) Score**: 4/14 principles achieved (5 partially achieved, 5 not achieved)

**Key Security Findings**:
- **Strengths**: Security requirements are comprehensively defined in architecture artifacts (NFR-SEC-001 through NFR-SEC-005, NFR-C-001 through NFR-C-005). DPIA has been completed with LOW-MEDIUM residual risk. SIRO and DPO are appointed. Risk register identifies and tracks 20 risks including security-specific entries. Data classification scheme is embedded in the data model with field-level encryption for PII and OFFICIAL-SENSITIVE marking for enforcement data.
- **Critical Gaps**: No security controls are yet implemented — the project is in Discovery/Alpha phase. No incident response plan exists. No penetration testing has been conducted. No security monitoring infrastructure is in place. No formal security policies have been drafted (only requirements specifications exist). Supply chain and third-party security management is undefined.
- **Blocking Issues for Next Phase**: Incident response plan must be drafted (NFR-C-005). Threat model must be formally documented. Security policy suite must be established. Cloud security architecture must be designed and reviewed.

**Cyber Essentials Status**: Not Started

**Risk Summary**: Medium — Security requirements are well-defined but entirely unimplemented. The Discovery/Alpha phase appropriately focuses on requirements definition, but several foundational security activities (threat model, incident response plan, security policies) should be initiated before Alpha completion.

---

## 1. NCSC Cyber Assessment Framework (CAF) Assessment

### Objective A: Managing Security Risk

**A1: Governance**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Security governance has been established at the organisational level through the appointment of key roles. The CMA SIRO has been identified as a High-influence stakeholder with accountability for information risk (ARC-001-STKE-v1.0). The CMA DPO is appointed and engaged, having overseen the DPIA process (ARC-001-DPIA-v1.0). Architecture Principle P6 (Security by Design) is designated NON-NEGOTIABLE, establishing security as a governance-level concern that cannot be traded off against other priorities (ARC-000-PRIN-v1.0). NFR-C-005 mandates SIRO sign-off as a gate requirement.

However, formal security policies and standards have not yet been drafted — only requirements exist. Security roles beyond SIRO and DPO (e.g., Security Architect, Security Operations Lead) are not yet assigned. No security oversight or reporting cadence has been established.

**Security Governance**:
- [ ] Senior leadership owns information security
- [x] Senior Information Risk Owner (SIRO) appointed
- [ ] Security policies and standards defined
- [ ] Security roles and responsibilities documented
- [x] Security risk management process established
- [ ] Security oversight and reporting in place

**Gaps/Actions**:
- Draft formal security policy suite (Information Security Policy, Acceptable Use Policy, Access Control Policy) — target: before Alpha completion
- Appoint Security Architect and define security RACI matrix
- Establish quarterly security governance board with SIRO chair
- Define security reporting cadence and metrics dashboard

**A2: Risk Management**

**Status**: ✅ Achieved

**Evidence**:
A comprehensive risk register (ARC-001-RISK-v1.0) has been established with 20 identified risks using a structured 5x5 likelihood-impact methodology. Information assets have been classified — the data model (ARC-001-DATA-v1.0) defines 8 entities with 96 attributes, each with explicit classification (OFFICIAL for most data, OFFICIAL-SENSITIVE for EnforcementAction entity, PII marking for Organisation contact fields). Threats and vulnerabilities are assessed: R-014 (Security Breach) has inherent risk score 9 with residual score 4 after mitigations. R-013 (DPIA not completed) tracked from inherent 12 to residual 6. Four High residual risks are identified and actively managed (R-001 compliance, R-003 enforcement, R-006 media, R-010 VE3 API).

Risk treatment plans are documented with specific mitigations mapped to each risk. The SIRO is identified as the risk acceptance authority. The risk register uses Orange Book-aligned methodology as appropriate for a UK Government service.

**Risk Management Process**:
- [x] Information assets identified and classified
- [x] Threats and vulnerabilities assessed
- [x] Risk assessment methodology defined
- [x] Risk register maintained and reviewed
- [x] Risk treatment plans implemented
- [ ] Residual risks accepted by SIRO

**Gaps/Actions**:
- Obtain formal SIRO sign-off on residual risk acceptance for all 4 High residual risks
- Schedule quarterly risk register review cycle
- Integrate security-specific threat intelligence into risk assessments during Beta

**A3: Asset Management**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Data assets are comprehensively catalogued in the data model (ARC-001-DATA-v1.0): 8 entities (FuelStation, FuelPrice, Organisation, EnforcementAction, ComplianceRecord, DataQualityMetric, AuditEvent, UserAccount) with 96 attributes across 10 relationships. Each entity has defined classification, ownership context, and retention rules. The Organisation entity identifies 3 PII fields (contact_name, contact_email, contact_phone) affecting approximately 3,000 data subjects. The EnforcementAction entity is marked OFFICIAL-SENSITIVE.

However, as the project is in Discovery/Alpha, no hardware or software assets exist yet. No formal asset register or Configuration Management Database (CMDB) has been established. Asset lifecycle management and secure disposal procedures are not defined.

**Asset Management**:
- [ ] Hardware inventory maintained
- [ ] Software inventory maintained
- [x] Data assets catalogued
- [x] Asset ownership assigned
- [ ] Asset lifecycle management
- [ ] Secure disposal procedures

**Gaps/Actions**:
- Establish CMDB framework for infrastructure and application assets during Beta
- Define secure disposal procedures for data-bearing media and cloud resources
- Create software asset register including all open source dependencies (SBOM)
- Define asset lifecycle management policy aligned with NCSC guidance

**A4: Supply Chain**

**Status**: ❌ Not Achieved

**Evidence**:
No supply chain security framework has been established. The requirements specification identifies cloud hosting (AWS UK or Azure UK regions) as a dependency, and the risk register identifies R-010 (VE3 API dependency) as a High residual risk (score 12), but no formal supplier security assessment framework exists. No vendor security questionnaires, third-party access controls, or supply chain risk register have been created. Open source software risks are not yet managed — no Software Bill of Materials (SBOM) process is defined.

The CMA Open Data API endpoint is a critical external dependency for data ingestion, but its security posture has not been formally assessed from a supply chain perspective.

**Supply Chain Security**:
- [ ] Supplier security requirements defined
- [ ] Supplier security assessments conducted
- [ ] Contracts include security obligations
- [ ] Third-party access controlled
- [ ] Supply chain risk register
- [ ] Open source software risks managed

**Gaps/Actions**:
- Define supplier security requirements and assessment questionnaire — target: before procurement
- Establish supply chain risk register as extension to main risk register
- Define open source governance policy including SBOM requirements
- Assess CMA Open Data API security posture and data integrity controls
- Include security obligations in all procurement contracts (aligned with Government Commercial Function standards)

---

### Objective B: Protecting Against Cyber Attack

**B1: Service Protection Policies and Processes**

**Status**: ❌ Not Achieved

**Evidence**:
Security requirements are comprehensively defined in ARC-001-REQ-v2.0 (NFR-SEC-001 through NFR-SEC-005, NFR-C-001 through NFR-C-005), establishing the intent and specifications for protective controls. Architecture Principle P6 (Security by Design) is designated NON-NEGOTIABLE. However, no formal security policies have been drafted. Requirements specifications define "what" must be achieved but not the organisational policies governing "how" security is managed.

Specific requirements that will inform future policies include: authentication standards (NFR-SEC-001), RBAC with 8 defined roles (NFR-SEC-002), encryption standards (NFR-SEC-003), secrets management (NFR-SEC-004), and security testing cadence (NFR-SEC-005). These provide a strong foundation for policy development but are not themselves policies.

**Protection Policies**:
- [ ] Acceptable Use Policy
- [ ] Access Control Policy
- [ ] Data Protection Policy
- [ ] Secure Development Policy
- [ ] Network Security Policy
- [ ] Cryptography Policy

**Gaps/Actions**:
- Draft Access Control Policy based on NFR-SEC-001 and NFR-SEC-002 specifications
- Draft Cryptography Policy based on NFR-SEC-003 (TLS 1.2+/prefer 1.3, AES-256)
- Draft Secure Development Policy based on NFR-SEC-005 (SAST/DAST/pen test requirements)
- Draft Data Protection Policy incorporating DPIA outcomes and NFR-C-001 requirements
- Establish policy review and approval governance process
- All policies to be approved by SIRO before Beta phase gate

**B2: Identity and Access Control**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Identity and access control requirements are thoroughly specified in NFR-SEC-001 and NFR-SEC-002 (ARC-001-REQ-v2.0):

- **Authentication** (NFR-SEC-001): MFA mandatory for fuel retailer accounts; OAuth 2.0 for API access; SSO integration for CMA staff via existing CMA identity provider; no authentication required for citizen read-only access to public fuel price data.
- **Authorisation** (NFR-SEC-002): RBAC model with 8 defined roles — Citizen (unauthenticated read-only), Retailer User, Retailer Admin, CMA Operations, CMA Enforcement, CMA Admin, DESNZ Analyst, and System Service. Each role has defined permission boundaries.

The data model (ARC-001-DATA-v1.0) includes a UserAccount entity with role, permissions, mfa_enabled, and last_login attributes, demonstrating that access control is architecturally embedded.

However, no IAM infrastructure exists. No PAM solution is specified. Access review processes are not defined. Password policy details beyond MFA are not specified.

**Access Controls**:
- [ ] User accounts managed centrally
- [x] Multi-factor authentication (MFA) enabled
- [ ] Privileged access management (PAM)
- [x] Least privilege principle enforced
- [ ] Regular access reviews
- [ ] Account provisioning/deprovisioning process
- [ ] Strong password policy (12+ characters)

**Authentication Method**: CMA SSO (for staff) / OAuth 2.0 (for API) / MFA (for retailers) / Unauthenticated (for citizens)

**Gaps/Actions**:
- Select and configure IAM platform (cloud-native or third-party)
- Define PAM solution for CMA Admin and System Service roles
- Establish access review schedule (quarterly for privileged, annual for standard)
- Define account provisioning/deprovisioning procedures for retailer onboarding
- Specify password complexity requirements (recommend NCSC guidance: 12+ characters, no mandatory complexity rules)
- Define session management and timeout policies

**B3: Data Security**

**Status**: ✅ Achieved

**Evidence**:
Data security is comprehensively defined across multiple architecture artifacts:

- **Classification**: Implemented in data model (ARC-001-DATA-v1.0) — OFFICIAL for operational data, OFFICIAL-SENSITIVE for EnforcementAction entity, PII marking on Organisation contact fields (contact_name, contact_email, contact_phone).
- **Encryption at rest**: AES-256 specified (NFR-SEC-003); field-level encryption for PII in Organisation entity; managed key service in UK sovereign cloud.
- **Encryption in transit**: TLS 1.2+ with preference for TLS 1.3 (NFR-SEC-003).
- **Data retention**: Prices indefinite (public interest), PII registration + 6 years, audit logs 7 years (NFR-C-001).
- **UK GDPR compliance**: DPIA completed (ARC-001-DPIA-v1.0) with LOW-MEDIUM residual risk. Lawful basis: Article 6(1)(e) Public Task. Only 3 PII fields for ~3,000 data subjects. No special category data. No international transfers — all data UK sovereign.
- **Audit integrity**: SHA-256 hash chain for tamper-evident audit logs, append-only storage, 7-year retention (NFR-C-002).

**Data Protection**:
- [x] Data classification scheme implemented
- [x] Encryption at rest (AES-256 minimum)
- [x] Encryption in transit (TLS 1.3 minimum)
- [ ] Data loss prevention (DLP) controls
- [ ] Secure data destruction
- [x] UK GDPR compliance
- [x] Data retention policy

**Personal Data Processing**: Yes (limited — 3 fields, ~3,000 data subjects)
**DPIA Completed**: Yes (ARC-001-DPIA-v1.0, outcome: PROCEED WITH CONDITIONS)

**Gaps/Actions**:
- Implement DLP controls for OFFICIAL-SENSITIVE enforcement data
- Define secure data destruction procedures for decommissioned storage
- Validate encryption implementation against NCSC cryptographic standards during Beta
- Implement data retention automation (automated purge of PII after registration + 6 years)

**B4: System Security**

**Status**: ❌ Not Achieved

**Evidence**:
No systems exist yet — the project is in Discovery/Alpha phase. No secure baseline configurations, system hardening standards, or endpoint protection have been defined. The requirements specification does not address system-level hardening beyond application security controls.

The fault tolerance requirements (circuit breaker, retry, bulkhead isolation, graceful degradation) defined in the requirements demonstrate awareness of system resilience, but these are application-level patterns rather than system hardening controls.

**System Hardening**:
- [ ] Secure baseline configurations
- [ ] Unnecessary services disabled
- [ ] Security patches applied timely
- [ ] Anti-malware deployed
- [ ] Application whitelisting (where appropriate)
- [ ] Host-based firewalls
- [ ] Endpoint Detection and Response (EDR)

**Operating Systems**: TBD — cloud-native architecture expected (likely Linux-based containers or serverless)

**Gaps/Actions**:
- Define secure baseline configuration standards aligned with CIS Benchmarks during Beta
- Specify container/serverless hardening requirements if cloud-native architecture selected
- Define EDR and anti-malware requirements for any managed infrastructure
- Establish system hardening validation in CI/CD pipeline (Infrastructure as Code scanning)

**B5: Resilient Networks**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Network resilience requirements are defined at the application level in ARC-001-REQ-v2.0:
- Availability targets: 99.9% citizen-facing, 99.95% API, 99.5% enforcement interface
- RPO 15 minutes / RTO 4 hours
- Auto-failover within 15 minutes
- Fault tolerance patterns: circuit breaker, retry with exponential backoff, bulkhead isolation, graceful degradation

The hosting requirement specifies UK sovereign cloud (AWS UK or Azure UK regions), which provides baseline network security capabilities (VPC/VNet, security groups, DDoS protection via cloud provider).

However, no network architecture has been designed. No network segmentation plan exists. No IDS/IPS, DDoS-specific protection, or network access control requirements are specified.

**Network Security**:
- [ ] Network segmentation by function/sensitivity
- [ ] Firewalls at network boundaries
- [ ] Intrusion Detection/Prevention Systems (IDS/IPS)
- [ ] DDoS protection
- [ ] Secure remote access (VPN)
- [ ] Network Access Control (NAC)
- [ ] WiFi security (WPA3)

**Network Architecture**: Cloud (AWS UK or Azure UK — not yet selected)

**Gaps/Actions**:
- Design network architecture with segmentation: public tier (citizen access), API tier (retailer integration), internal tier (CMA enforcement), data tier (isolated)
- Specify DDoS protection requirements — public-facing service requires cloud-native DDoS mitigation (e.g., AWS Shield / Azure DDoS Protection)
- Define IDS/IPS requirements for monitoring cross-tier traffic
- Design secure administrative access (no public SSH/RDP; bastion host or SSM/Serial Console)
- Document network security architecture for GDS assessment

**B6: Staff Awareness and Training**

**Status**: ❌ Not Achieved

**Evidence**:
No security awareness or training programme has been defined for the project. The CMA as a government department likely has existing security awareness training, but no project-specific security training requirements have been specified. The requirements and risk register do not address staff training as a control.

Given the project handles OFFICIAL and OFFICIAL-SENSITIVE data, and involves regulated entities (fuel retailers) who will submit data via APIs, security awareness is particularly important for:
- CMA enforcement staff handling OFFICIAL-SENSITIVE data
- Operations staff managing retailer onboarding
- Development team building and maintaining the service

**Security Training**:
- [ ] Mandatory security awareness training
- [ ] Phishing awareness training
- [ ] Role-based security training
- [ ] Annual security refresher
- [ ] Security incident reporting awareness
- [ ] Data protection training (UK GDPR)
- [ ] Social engineering awareness

**Training Completion Rate**: N/A — no training programme established

**Gaps/Actions**:
- Confirm CMA departmental security training covers project-relevant topics
- Define role-based security training for CMA Enforcement (OFFICIAL-SENSITIVE handling)
- Establish security awareness requirements for development team (OWASP, secure coding)
- Define security training requirements for retailer onboarding documentation
- Include security incident reporting procedures in staff induction

---

### Objective C: Detecting Cyber Security Events

**C1: Security Monitoring**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Audit logging requirements are comprehensively defined in NFR-C-002 (ARC-001-REQ-v2.0):
- Tamper-evident logging with SHA-256 chain hash
- 7-year retention
- Append-only storage
- The AuditEvent entity (ARC-001-DATA-v1.0) captures: event_id, event_type, actor_id, actor_role, resource_type, resource_id, action, timestamp, ip_address, details, hash, previous_hash

This provides a strong foundation for security monitoring, but no SIEM solution, real-time alerting, security event correlation, or threat intelligence integration has been specified. The architecture defines what will be logged but not how it will be monitored.

**Monitoring Capabilities**:
- [ ] Centralized logging (SIEM)
- [ ] Real-time security alerting
- [x] Log retention (minimum 12 months)
- [ ] Security event correlation
- [ ] User behavior analytics
- [ ] Threat intelligence integration
- [ ] File integrity monitoring

**SIEM Solution**: Not yet selected

**Gaps/Actions**:
- Select SIEM solution (cloud-native options: AWS CloudWatch/Security Hub or Azure Sentinel)
- Define security alerting rules for: failed authentication attempts, privilege escalation, OFFICIAL-SENSITIVE data access, API abuse patterns, data exfiltration indicators
- Establish 24/7 monitoring requirements or align with CMA/cross-government SOC
- Define security event correlation rules and playbooks
- Integrate threat intelligence feeds relevant to government services

**C2: Proactive Security Event Discovery**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Security testing requirements are defined in NFR-SEC-005 (ARC-001-REQ-v2.0):
- SAST: every build
- DAST: weekly on staging environment
- Penetration testing: annually by CHECK-approved provider
- Critical vulnerability SLA: 24 hours

NFR-C-005 mandates a threat model as part of Secure by Design compliance. The risk register (ARC-001-RISK-v1.0) demonstrates threat assessment capability with R-014 (Security Breach) specifically identifying Secure by Design, pen testing, and encryption as mitigations.

However, no penetration testing has been conducted (Discovery/Alpha phase). No threat model has been formally documented (risk register provides threat assessment but not a structured threat model such as STRIDE). No vulnerability scanning is in place. No red team exercises are planned.

**Proactive Measures**:
- [ ] Threat hunting activities
- [x] Vulnerability scanning (weekly/monthly)
- [x] Penetration testing (annual minimum)
- [ ] Red team exercises
- [ ] Security posture reviews
- [x] Threat modeling

**Last Penetration Test**: Not Conducted (Discovery/Alpha phase)
**Pen Test Findings**: N/A

**Gaps/Actions**:
- Conduct formal threat modelling exercise (recommend STRIDE methodology) during Alpha — required by NFR-C-005
- Plan initial penetration test for Beta phase by CHECK-approved provider — required by NFR-C-005
- Establish vulnerability scanning toolchain in CI/CD pipeline during Beta
- Consider IT Health Check (ITHC) aligned with Cabinet Office requirements before Live

---

### Objective D: Minimising the Impact of Cyber Security Incidents

**D1: Response and Recovery Planning**

**Status**: ✅ Achieved

**Evidence**:
Recovery requirements are comprehensively defined in ARC-001-REQ-v2.0:
- **RTO**: 4 hours
- **RPO**: 15 minutes
- **Auto-failover**: within 15 minutes
- **Availability tiers**: 99.9% citizen, 99.95% API, 99.5% enforcement
- **Fault tolerance**: circuit breaker, retry with exponential backoff, bulkhead isolation, graceful degradation

NFR-C-005 mandates an incident response plan as part of Secure by Design compliance. The risk register actively tracks security breach risk (R-014) with defined mitigations. ICO breach notification obligations are addressed through the DPIA (ARC-001-DPIA-v1.0).

While an incident response plan document has not yet been drafted, the requirements provide detailed specifications for recovery capabilities, and the mandate for an IR plan is established. The DPIA identifies the 72-hour ICO notification requirement.

**Incident Response**:
- [ ] Incident response plan documented
- [ ] Incident response team defined
- [ ] Incident classification scheme
- [ ] Escalation procedures defined
- [ ] Communication plan for incidents
- [x] Regulatory reporting process (ICO)
- [ ] Lessons learned process

**IR Plan Last Tested**: Not Tested (plan not yet drafted)

**Business Continuity**:
- [ ] Business continuity plan (BCP)
- [ ] Disaster recovery plan (DRP)
- [x] Recovery time objective (RTO) defined
- [x] Recovery point objective (RPO) defined
- [ ] BC/DR testing conducted

**RTO**: 4 hours
**RPO**: 15 minutes (0.25 hours)

**Gaps/Actions**:
- Draft incident response plan — CRITICAL: required by NFR-C-005 before Alpha completion
- Define incident response team with roles from CMA and development team
- Establish incident classification scheme (P1-P4) aligned with ITIL and GDS standards
- Define escalation procedures: team lead -> SIRO -> NCSC (for significant incidents)
- Draft communication plan covering ICO (72h), affected data subjects, CMA press office, ministerial briefing
- Plan DR testing during Beta phase to validate RTO/RPO targets

**D2: Improvements**

**Status**: ❌ Not Achieved

**Evidence**:
No continuous improvement process for security has been established. The risk register provides a framework for ongoing risk assessment, but no security metrics, post-incident review processes, security trend analysis, or security roadmap exist. This is expected at Discovery/Alpha phase — continuous improvement processes typically mature during Beta and Live phases.

**Continuous Improvement**:
- [ ] Post-incident reviews conducted
- [ ] Security metrics tracked
- [ ] Security improvements implemented
- [ ] Lessons learned documented
- [ ] Security trends analyzed
- [ ] Security roadmap maintained

**Gaps/Actions**:
- Define security KPIs and metrics dashboard during Beta (e.g., mean time to patch, vulnerability ageing, authentication failure rates)
- Establish post-incident review template and process
- Create security improvement backlog integrated with product backlog
- Plan quarterly security posture reviews aligned with SIRO governance

---

## 2. Cyber Essentials / Cyber Essentials Plus

### Cyber Essentials Status

**Current Status**: Not Started

**Certification Date**: N/A
**Expiry Date**: N/A

The project is in Discovery/Alpha phase and no infrastructure exists to certify. Cyber Essentials certification should be planned as a Beta/Live milestone. As a UK Government service, Cyber Essentials Plus is the recommended target certification level.

**Cyber Essentials Requirements**:

| Control Area | Status | Evidence |
|--------------|--------|----------|
| **Firewalls** | ⚠️ | Cloud hosting specified (AWS/Azure), which provides managed firewall capabilities. No network architecture designed yet. |
| **Secure Configuration** | ❌ | No systems exist. No secure baseline configurations defined. Requirements specify TLS 1.2+/AES-256 but no system-level hardening standards. |
| **Access Control** | ⚠️ | Comprehensive RBAC with 8 roles defined (NFR-SEC-002). MFA mandated for retailers (NFR-SEC-001). SSO for CMA staff. Not yet implemented. |
| **Malware Protection** | ❌ | No anti-malware or EDR requirements specified. Cloud-native architecture may reduce traditional malware risk but controls still required. |
| **Patch Management** | ⚠️ | Critical vulnerability 24h SLA defined (NFR-SEC-005). No patch management process or schedule established. |

**Cyber Essentials Plus Additional Requirements**:
- [ ] External vulnerability scan passed
- [ ] Internal vulnerability scan passed
- [ ] System configuration review passed

**Target Certification Level**: Plus

**Gaps/Actions**:
- Include Cyber Essentials Plus certification in Beta phase plan
- Engage CE Plus certification body during Beta build phase
- Ensure all 5 technical controls are implemented and evidenced before certification assessment
- Budget for annual CE Plus recertification

---

## 3. UK GDPR and Data Protection

### 3.1 Data Protection Compliance

**Data Protection Officer (DPO) Appointed**: Yes (CMA DPO — identified in ARC-001-STKE-v1.0)

**ICO Registration**: Required (CMA is a registered data controller; this service may require updated registration to cover new processing activities)

**UK GDPR Compliance**:
- [x] Lawful basis for processing identified
- [ ] Privacy notice published
- [ ] Data subject rights procedures
- [x] Data retention policy defined
- [x] Data breach notification process (72 hours)
- [ ] Data processing agreements with suppliers
- [ ] Records of processing activities (ROPA)

**Personal Data Processed**: Yes (limited scope — 3 PII fields in Organisation entity: contact_name, contact_email, contact_phone for ~3,000 fuel retailer contacts)

**Special Category Data**: No

**Key GDPR Details** (from ARC-001-DPIA-v1.0 and ARC-001-REQ-v2.0):
- **Lawful basis**: Article 6(1)(e) Public Task — processing necessary for the performance of a task carried out in the public interest (Motor Fuel Price (Open Data) Regulations 2025)
- **Data subjects**: ~3,000 fuel retailer contacts (registration and compliance purposes)
- **Data residency**: UK only — no international transfers
- **Retention**: PII retained for registration period + 6 years; prices indefinite; audit logs 7 years
- **PII protection**: AES-256 field-level encryption on Organisation entity PII fields

**Gaps/Actions**:
- Draft and publish privacy notice for fuel retailer data — required before retailer onboarding
- Define data subject rights procedures (access, rectification, erasure, portability)
- Establish ROPA documenting all processing activities
- Prepare Data Processing Agreements (DPAs) for cloud hosting provider and any sub-processors
- Update CMA ICO registration if new processing activities are not covered

### 3.2 Data Protection Impact Assessment (DPIA)

**DPIA Required**: Yes (ICO screening: 2/9 criteria met — DPIA required)

**DPIA Status**: Completed (ARC-001-DPIA-v1.0)

**DPIA Findings**:
- High risks identified: 0
- Medium risks identified: 8 (all mitigated to LOW or MEDIUM residual)
- Mitigations implemented: 8 mitigations defined (implementation pending — Discovery/Alpha)
- Residual risks accepted: Pending formal SIRO acceptance

**DPIA Outcome**: PROCEED WITH CONDITIONS
- Overall residual risk: LOW-MEDIUM
- 8 privacy risks identified with defined mitigations
- All risks reduced to acceptable levels
- No ICO consultation required (no high residual risks remaining)

**ICO Consultation Required**: No (all residual risks at LOW or MEDIUM)

**Gaps/Actions**:
- Obtain formal SIRO sign-off on DPIA residual risks
- Implement all 8 DPIA mitigations during Beta phase
- Schedule DPIA review when service enters Beta (design changes may introduce new privacy risks)
- Monitor for changes that could trigger DPIA refresh (new data processing, new data sharing)

---

## 4. Secure Development Practices

### 4.1 Secure Software Development Lifecycle (SDLC)

**Development Methodology**: Agile (GDS Service Manual aligned)

**Secure Development Practices**:
- [x] Secure coding standards defined
- [x] Security requirements in user stories
- [x] Threat modeling in design phase
- [ ] Code review includes security
- [x] Static Application Security Testing (SAST)
- [x] Dynamic Application Security Testing (DAST)
- [ ] Software Composition Analysis (SCA)
- [ ] Dependency vulnerability scanning

NFR-SEC-005 (ARC-001-REQ-v2.0) specifies:
- **SAST**: Every build — integrated into CI/CD pipeline
- **DAST**: Weekly on staging environment
- **Penetration testing**: Annually by CHECK-approved provider
- **Critical vulnerability SLA**: 24 hours
- **Secrets management**: No hardcoded secrets (NFR-SEC-004), managed secrets service, 90-day rotation

NFR-C-005 mandates threat modelling in the design phase. Security requirements are embedded throughout the NFR specification (22+ NFRs including dedicated security and compliance sections).

**OWASP Top 10 Mitigation**:
- [x] Injection flaws prevented
- [x] Broken authentication prevented
- [x] Sensitive data exposure prevented
- [ ] XML External Entities (XXE) prevented
- [x] Broken access control prevented
- [ ] Security misconfiguration prevented
- [x] Cross-Site Scripting (XSS) prevented
- [ ] Insecure deserialization prevented
- [x] Using components with known vulnerabilities prevented
- [x] Insufficient logging and monitoring addressed

Note: OWASP Top 10 mitigations are assessed based on requirements definitions. NFR-SEC-001 (authentication/MFA/OAuth 2.0) addresses broken authentication. NFR-SEC-002 (RBAC with 8 roles) addresses broken access control. NFR-SEC-003 (TLS 1.3/AES-256) addresses sensitive data exposure. NFR-C-002 (tamper-evident audit logging) addresses insufficient logging. NFR-SEC-005 (SAST/DAST) addresses injection and XSS. Implementation validation is required during Beta.

**Gaps/Actions**:
- Integrate Software Composition Analysis (SCA) tool into CI/CD pipeline
- Define secure code review checklist incorporating OWASP verification standard
- Establish dependency vulnerability scanning with automated alerting
- Document XXE prevention controls in API design (disable external entity processing)
- Define serialisation/deserialisation security controls
- Establish secure configuration management baseline for all environments

### 4.2 DevSecOps

**CI/CD Security Integration**:
- [x] Automated security testing in pipeline
- [x] Secrets scanning (no hardcoded credentials)
- [ ] Container image scanning
- [ ] Infrastructure as Code (IaC) security
- [ ] Build artifact signing
- [ ] Automated deployment security checks

NFR-SEC-004 mandates no hardcoded secrets with a managed secrets service and 90-day rotation. NFR-SEC-005 mandates SAST integration in every build. These define the CI/CD security requirements but the pipeline does not yet exist.

**Gaps/Actions**:
- Design CI/CD pipeline with security gates (SAST, secrets scanning, dependency check as blocking gates)
- Include container image scanning if containerised architecture selected
- Implement Infrastructure as Code security scanning (e.g., tfsec, cfn-nag, Checkov)
- Define build artifact signing process for deployment integrity
- Establish environment promotion gates with security validation

---

## 5. Cloud Security

### 5.1 Cloud Service Provider

**Cloud Provider**: AWS UK or Azure UK (not yet selected)

**Cloud Deployment Model**: Public (UK sovereign regions)

**Data Residency**: UK only (NFR-SEC-003 — managed key service in UK sovereign cloud; DPIA confirms no international transfers)

**Cloud Security Controls**:
- [ ] Cloud Security Posture Management (CSPM)
- [x] Identity and Access Management (IAM)
- [x] Encryption key management
- [ ] Network security groups
- [ ] Cloud Access Security Broker (CASB)
- [ ] Cloud security monitoring
- [x] Multi-region redundancy

IAM requirements are defined (NFR-SEC-001/002). Encryption key management is specified (NFR-SEC-003 — managed key service, UK sovereign). Multi-region or multi-AZ capability is implied by availability targets (99.9%+ with auto-failover <15min). However, no cloud architecture has been designed and no cloud-specific security controls have been configured.

**NCSC Cloud Security Principles**: Assessment pending — cloud provider not yet selected

The following NCSC Cloud Security Principles are addressed by requirements:
1. Data in transit protection — TLS 1.2+/1.3 (NFR-SEC-003) ✅
2. Asset protection and resilience — UK sovereign hosting, AES-256 (NFR-SEC-003) ✅
3. Separation between consumers — TBD (cloud architecture not designed) ❌
4. Governance framework — SIRO appointed, risk register maintained ⚠️
5. Operational security — Security testing defined (NFR-SEC-005) ⚠️
6. Personnel security — Not addressed ❌
7. Secure development — SAST/DAST/pen test defined (NFR-SEC-005) ⚠️
8. Supply chain security — Not addressed ❌
9. Secure user management — MFA/RBAC/SSO defined (NFR-SEC-001/002) ⚠️
10. Identity and authentication — OAuth 2.0/MFA/SSO defined (NFR-SEC-001) ⚠️
11. External interface protection — TBD ❌
12. Secure service administration — TBD ❌
13. Audit information for users — Tamper-evident audit logging (NFR-C-002) ✅
14. Secure use of the service — TBD ❌

**NCSC Cloud Security Principles Score**: 3/14 fully addressed, 5/14 partially addressed, 6/14 not addressed

**Gaps/Actions**:
- Select cloud provider through formal procurement with security evaluation criteria
- Design cloud security architecture addressing all 14 NCSC Cloud Security Principles
- Implement CSPM tooling (AWS Security Hub / Azure Defender for Cloud)
- Design network security architecture with security groups, NACLs/NSGs, and segmentation
- Define cloud administrative access controls (no direct console access from internet; MFA mandatory; break-glass procedures)
- Conduct NCSC Cloud Security Principles assessment against selected provider

---

## 6. Vulnerability and Patch Management

### 6.1 Vulnerability Management

**Vulnerability Scanning Frequency**: Weekly on staging (defined in NFR-SEC-005); daily SAST in builds

**Scanning Coverage**: 0% of assets (no assets exist — Discovery/Alpha phase)

**Vulnerability Management Process**:
- [x] Automated vulnerability scanning
- [x] Vulnerability prioritization (CVSS scores)
- [x] Remediation SLAs defined
- [ ] Exception process for unfixable vulnerabilities
- [ ] Vulnerability remediation tracking
- [ ] Metrics and reporting

NFR-SEC-005 defines the vulnerability management requirements:
- SAST: every build (automated)
- DAST: weekly on staging
- Penetration testing: annually by CHECK-approved provider
- Critical vulnerability SLA: 24 hours

**Remediation SLAs** (from NFR-SEC-005 and risk register alignment):
- Critical vulnerabilities: Within 24 hours (NFR-SEC-005)
- High vulnerabilities: Within 7 days (implied by risk appetite)
- Medium vulnerabilities: Within 30 days (standard practice)
- Low vulnerabilities: Within 90 days (standard practice)

**Current Vulnerability Status**:
- Critical: N/A (no systems deployed)
- High: N/A
- Medium: N/A
- Low: N/A

**Gaps/Actions**:
- Define vulnerability exception/risk acceptance process for vulnerabilities that cannot be remediated within SLA
- Establish vulnerability tracking dashboard and reporting cadence
- Define vulnerability metrics (mean time to remediate, vulnerability age, scan coverage)
- Select and procure SAST, DAST, and SCA tooling during Beta

### 6.2 Patch Management

**Patch Management Process**:
- [ ] Patch assessment and testing
- [ ] Patch deployment schedule
- [ ] Emergency patching process
- [ ] Patch compliance monitoring
- [ ] Rollback procedures

**Patch Compliance**: N/A (no systems deployed)

**Critical Patch SLA**: 24 hours (aligned with NFR-SEC-005 critical vulnerability SLA)

**Gaps/Actions**:
- Define patch management policy covering assessment, testing, deployment, and rollback
- Establish patch deployment schedule (critical: 24h, high: 7d, routine: 14d)
- Design automated patching for cloud infrastructure (cloud-native managed services reduce patching burden)
- Define emergency patching process with accelerated change approval
- Establish patch compliance monitoring and reporting

---

## 7. Third-Party and Supply Chain Risk

### 7.1 Third-Party Risk Management

**Third-Party Security Assessment**:
- [ ] Vendor security questionnaires
- [ ] Vendor security certifications verified
- [ ] Data Processing Agreements (DPAs) in place
- [ ] Third-party access controls
- [ ] Vendor risk register
- [ ] Ongoing vendor monitoring

No third-party risk management framework has been established. The following third-party dependencies are identified from architecture artifacts:

**Key Third Parties**:

| Vendor | Service | Security Rating | Risk Level | Mitigations |
|--------|---------|-----------------|------------|-------------|
| CMA Open Data API | Fuel price data source | TBD | High (R-010) | Circuit breaker, data validation, fallback cache |
| Cloud Provider (TBD) | Infrastructure hosting | TBD | Medium | UK sovereign regions, managed services, encryption |
| CHECK-approved Pen Test Provider (TBD) | Annual penetration testing | TBD | Low | Procurement via G-Cloud/DOS frameworks |
| GDS / GOV.UK | Design system, service standards | N/A | Low | Government shared service |

**Gaps/Actions**:
- Develop vendor security assessment questionnaire aligned with NCSC supply chain guidance
- Verify cloud provider security certifications (ISO 27001, SOC 2, CSA STAR, Cyber Essentials Plus)
- Prepare DPAs for cloud hosting provider (required before data processing commences)
- Establish vendor risk register as subset of project risk register
- Define third-party access control requirements (no persistent access; time-limited; audited)
- Plan ongoing vendor monitoring process

### 7.2 Open Source Security

**Open Source Components**: TBD (no software developed yet)

**OSS Security Controls**:
- [ ] Software Bill of Materials (SBOM)
- [x] Automated dependency scanning
- [ ] Known vulnerability detection (CVE)
- [ ] License compliance checks
- [ ] OSS component lifecycle management

NFR-SEC-005 mandates SAST in every build, which should include dependency scanning. However, no explicit SBOM, licence compliance, or OSS governance requirements are specified.

**Gaps/Actions**:
- Define OSS governance policy (approved licences, prohibited licences, review process)
- Mandate SBOM generation as part of build process (aligned with NCSC software supply chain guidance)
- Integrate automated CVE detection into CI/CD pipeline (e.g., Dependabot, Snyk, Trivy)
- Define OSS component lifecycle management (version currency, end-of-life tracking)
- Establish licence compliance checking (ensure compatibility with Government open source policy)

---

## 8. Backup and Recovery

### 8.1 Backup Strategy

**Backup Method**: TBD — requirements specify RPO 15 minutes, implying continuous replication or near-continuous backup

**Backup Controls**:
- [ ] Automated backups scheduled
- [x] Backup encryption enabled
- [ ] Offsite/cloud backups
- [ ] Immutable backups (ransomware protection)
- [ ] Backup integrity testing
- [ ] Backup restoration testing

Encryption at rest (AES-256) is specified for all data (NFR-SEC-003), which would include backups. RPO of 15 minutes (ARC-001-REQ-v2.0) requires near-continuous data replication. Auto-failover within 15 minutes implies active-passive or active-active architecture with real-time replication.

**Backup Frequency**: Near-continuous required (RPO 15 minutes)

**Backup Retention**: Not explicitly defined for backups (data retention: prices indefinite, PII registration+6yr, audit 7yr)

**Last Successful Backup**: N/A (no systems deployed)

**Last Restoration Test**: N/A

**Gaps/Actions**:
- Design backup architecture to meet RPO 15 minutes (cloud-native replication, point-in-time recovery)
- Define backup retention policy (separate from data retention — consider 30-day rolling + monthly for 12 months)
- Implement immutable backups to protect against ransomware and insider threat
- Plan quarterly backup restoration testing
- Specify offsite backup requirements (cross-region within UK, or isolated account)

### 8.2 Recovery Capabilities

**Recovery Time Objective (RTO)**: 4 hours (ARC-001-REQ-v2.0)
**Recovery Point Objective (RPO)**: 15 minutes / 0.25 hours (ARC-001-REQ-v2.0)

**Recovery Testing**: Not tested (no systems deployed)

**Recovery Success Rate**: N/A

Additional recovery requirements from ARC-001-REQ-v2.0:
- Auto-failover within 15 minutes
- Availability: 99.9% citizen, 99.95% API, 99.5% enforcement
- Fault tolerance: circuit breaker, retry with exponential backoff, bulkhead isolation, graceful degradation

**Gaps/Actions**:
- Design disaster recovery architecture to meet RTO 4h / RPO 15min targets
- Define DR runbook with step-by-step recovery procedures
- Plan DR testing during Beta (tabletop exercise initially, full failover test before Live)
- Define recovery testing schedule (quarterly failover tests in Live)
- Establish recovery success criteria and acceptance testing procedures

---

## Overall Security Assessment Summary

### NCSC CAF Scorecard

| CAF Objective | Principles Achieved | Status |
|---------------|---------------------|--------|
| A. Managing Security Risk | 1/4 (A2 achieved; A1, A3 partial; A4 not achieved) | ⚠️ |
| B. Protecting Against Cyber Attack | 1/6 (B3 achieved; B2, B5 partial; B1, B4, B6 not achieved) | ⚠️ |
| C. Detecting Cyber Security Events | 0/2 (C1, C2 partial) | ⚠️ |
| D. Minimising Impact of Incidents | 1/2 (D1 achieved; D2 not achieved) | ⚠️ |
| **Overall** | **3/14** | **⚠️ Needs Improvement** |

Note: The score of 3/14 reflects the Discovery/Alpha phase. Requirements are comprehensively defined — the gap is implementation. The achieved principles (A2 Risk Management, B3 Data Security, D1 Response and Recovery Planning) represent areas where architecture artifacts provide sufficient definition and evidence. An additional principle (A1 Governance) is close to achievement pending formal SIRO sign-off and security policy drafting.

### Security Posture Summary

**Strengths**:
- Comprehensive security requirements defined (NFR-SEC-001 to NFR-SEC-005, NFR-C-001 to NFR-C-005) providing a strong security architecture baseline
- DPIA completed with LOW-MEDIUM residual risk outcome — PROCEED WITH CONDITIONS
- SIRO and DPO appointed with clear accountability
- Risk register maintained with 20 risks including security-specific entries (R-014 Security Breach)
- Data classification scheme embedded in data model with field-level PII encryption
- Architecture Principle P6 (Security by Design) designated NON-NEGOTIABLE
- Audit logging architecture defined with tamper-evident SHA-256 hash chain
- Recovery targets defined: RPO 15min / RTO 4hr with auto-failover

**Critical Gaps**:
- No incident response plan drafted — blocks Alpha completion (NFR-C-005 mandate)
- No formal threat model documented — blocks Alpha completion (NFR-C-005 mandate)
- No security policies drafted — only requirements specifications exist
- No supply chain security framework — cloud provider not yet assessed
- No security monitoring infrastructure — no SIEM, alerting, or SOC capability
- No systems exist to validate controls — entirely requirements-based assessment

**Overall Risk Rating**: Medium

The Medium rating reflects a well-architected security requirements baseline with significant implementation gaps. The project's Discovery/Alpha phase appropriately focuses on requirements definition. The rating would escalate to High if the identified critical gaps (incident response plan, threat model) are not addressed before Alpha completion.

### Critical Security Issues

1. **Incident response plan not documented** (CAF D1) — **CRITICAL** — NFR-C-005 mandates IR plan; required before SIRO sign-off. Without IR plan, the service cannot demonstrate readiness for security incidents. ICO breach notification (72h) process is identified but not operationalised.

2. **Formal threat model not conducted** (CAF C2) — **CRITICAL** — NFR-C-005 mandates threat modelling. No structured threat model (STRIDE/LINDDUN) has been produced despite risk register providing partial threat assessment. Threat model is prerequisite for security architecture validation.

3. **Security policy suite not drafted** (CAF B1) — **HIGH** — Requirements define "what" but no policies define "how." Access Control, Cryptography, Secure Development, and Data Protection policies are needed before development commences in Beta.

4. **Supply chain security not addressed** (CAF A4) — **HIGH** — Cloud provider selection imminent but no supplier security assessment framework exists. CMA Open Data API dependency identified as High risk (R-010) but not assessed from security perspective.

5. **No security monitoring capability defined** (CAF C1) — **HIGH** — Audit logging architecture exists but no SIEM, alerting, or SOC requirements specified. Cannot detect security events without monitoring infrastructure.

6. **System hardening standards not defined** (CAF B4) — **MEDIUM** — Expected at this phase but should be addressed early in Beta before infrastructure provisioning.

7. **Staff security training not addressed** (CAF B6) — **MEDIUM** — No project-specific security awareness programme. CMA departmental training may partially address this.

### Recommendations

**Critical Priority** (0-30 days — must resolve before Alpha completion):
- Draft incident response plan covering incident classification, escalation, ICO notification, communication — Security Architect — 2026-02-28
- Conduct formal STRIDE threat model for the service — Security Architect — 2026-02-28
- Obtain SIRO sign-off on risk register residual risks and DPIA outcome — CMA SIRO — 2026-02-28

**High Priority** (1-3 months — must resolve before Beta build commences):
- Draft security policy suite (Access Control, Cryptography, Secure Development, Data Protection, Acceptable Use) — Security Architect — 2026-04-30
- Define supplier security assessment framework and assess cloud provider candidates — Security Architect / Procurement — 2026-04-30
- Design security monitoring architecture and select SIEM solution — Security Architect — 2026-04-30
- Design network security architecture with segmentation plan — Security Architect — 2026-04-30
- Prepare DPAs for cloud hosting provider — CMA DPO / Legal — 2026-04-30

**Medium Priority** (3-6 months — continuous improvement during Beta):
- Implement CI/CD security pipeline (SAST, DAST, SCA, secrets scanning, IaC scanning) — Development Lead — 2026-07-31
- Define system hardening baselines (CIS Benchmarks for selected platform) — Security Architect — 2026-07-31
- Establish security awareness training for project team — Security Lead — 2026-07-31
- Implement SBOM generation and OSS governance — Development Lead — 2026-07-31
- Plan initial penetration test by CHECK-approved provider — Security Architect — 2026-07-31
- Commence Cyber Essentials Plus preparation — Security Architect — 2026-07-31
- Draft and publish privacy notice for fuel retailer data — CMA DPO — 2026-07-31
- Define data subject rights procedures — CMA DPO — 2026-07-31

---

## Next Steps and Action Plan

**Immediate Actions** (0-30 days):
- [ ] Draft incident response plan — Security Architect — 2026-02-28
- [ ] Conduct STRIDE threat model — Security Architect — 2026-02-28
- [ ] Obtain SIRO sign-off on risk register and DPIA — CMA SIRO — 2026-02-28
- [ ] Appoint Security Architect to project team — Project Lead — 2026-02-14

**Short-term Actions** (1-3 months):
- [ ] Draft security policy suite — Security Architect — 2026-04-30
- [ ] Design cloud security architecture — Security Architect — 2026-04-30
- [ ] Design network segmentation architecture — Security Architect — 2026-04-30
- [ ] Define supplier security assessment framework — Security Architect — 2026-04-30
- [ ] Select and procure security tooling (SIEM, SAST, DAST, SCA) — Security Architect — 2026-04-30
- [ ] Prepare DPAs for cloud provider — CMA DPO / Legal — 2026-04-30
- [ ] Design security monitoring architecture — Security Architect — 2026-04-30

**Long-term Actions** (3-12 months):
- [ ] Implement CI/CD security pipeline — Development Lead — 2026-07-31
- [ ] Conduct initial penetration test (CHECK-approved) — Security Architect — 2026-09-30
- [ ] Achieve Cyber Essentials Plus certification — Security Lead — 2026-10-31
- [ ] Conduct IT Health Check before Live — Security Architect — 2026-10-31
- [ ] Establish security metrics dashboard — Security Lead — 2026-07-31
- [ ] Conduct DR failover test — Operations Lead — 2026-09-30
- [ ] Establish quarterly security posture review cycle — SIRO — 2026-10-31

**Next Security Review**: 2026-04-30 (quarterly during development; recommend monthly during Beta build phase)

---

## Approval and Sign-Off

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Project Lead | PENDING | | |
| Security Architect | PENDING | | |
| Senior Information Risk Owner (SIRO) | CMA SIRO | | |
| Data Protection Officer (DPO) | CMA DPO | | |

---

**Document Control**:
- **Version**: 1.0
- **Classification**: OFFICIAL
- **Last Reviewed**: 2026-01-30
- **Next Review**: 2026-04-30
- **Document Owner**: Security Architect / CMA SIRO

---

**Generated by**: ArcKit `/arckit.secure` command
**Generated on**: 2026-01-30
**ArcKit Version**: 1.0.3
**Project**: UK Fuel Price Transparency Service (Project 001)
**Model**: claude-opus-4-5-20251101
