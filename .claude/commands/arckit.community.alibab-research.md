---
description: Research Alibaba Cloud services against project requirements with UK Government compliance checks
argument-hint: "<project ID or name>"
---

You are generating an Alibab Cloud Research document using a community template.

## User Input

```text
$ARGUMENTS
```

## Instructions

1. **Identify the target project**:
   - Use the **ArcKit Project Context** (above) to find the project matching the user's input
   - If no match, create a new project directory

2. **Read the template**:
   - Read `.arckit/templates-custom/alibab-research-template.md`

3. **Read project requirements**:
   - Find and read the latest `ARC-{PROJECT_ID}-REQ-v*.md` in the target project
   - Extract functional and non-functional requirements to evaluate services against

4. **Research Alibaba Cloud services**:
   - For each major requirement area, identify candidate Alibaba Cloud services
   - Assess capability fit, UK regional availability, pricing, and compliance posture
   - Check G-Cloud / Digital Marketplace listing status
   - Evaluate against NCSC Cloud Security Principles and TCoP

5. **Generate the document** following the template structure:
   - Fill the Service Research Summary with all evaluated services
   - Complete Detailed Service Assessments for top candidates
   - Build the Requirements Coverage Matrix mapping requirements to services
   - Complete the UK Government Compliance Checklist with pass/fail evidence
   - Document gaps, risks, and prioritised recommendations

6. **Write the output** using the Write tool to `projects/{project-dir}/ARC-{PROJECT_ID}-ALRS-v1.0.md`

7. **Show summary only** (NOT the full document):
   - Number of services evaluated
   - Requirements coverage percentage
   - Compliance checklist pass rate
   - Top recommendations
