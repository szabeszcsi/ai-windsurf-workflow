# Requirements: {Feature/Project Name}

<!--
This template structures requirements for AI-assisted development.
Fill in sections relevant to your feature. Delete unused sections.
Save to: docs/requirements/{feature-name}.md
-->

**Author:** {Name}
**Date:** {YYYY-MM-DD}
**Status:** Draft | Under Review | Approved
**Version:** 1.0

---

## Problem Statement

**What problem does this solve?**
{2-3 sentences describing the pain point or opportunity}

**Who is affected?**
{Users, developers, systems impacted}

**What happens if we don't solve it?**
{Consequences of inaction}

---

## Goals

**Primary Goal:**
{One clear, measurable outcome}

**Success Metrics:**
- {Metric 1: e.g., "Reduce load time by 50%"}
- {Metric 2: e.g., "Handle 1000 concurrent users"}
- {Metric 3: e.g., "Zero data loss during migration"}

---

## Functional Requirements

### Must Have (P0)
*Critical for MVP. Cannot ship without these.*

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| F1 | {Requirement} | {How to verify it's done} |
| F2 | {Requirement} | {How to verify it's done} |
| F3 | {Requirement} | {How to verify it's done} |

### Should Have (P1)
*Important but not blocking. Target for v1.0.*

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| F4 | {Requirement} | {How to verify it's done} |
| F5 | {Requirement} | {How to verify it's done} |

### Could Have (P2)
*Nice to have. Consider for future iterations.*

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| F6 | {Requirement} | {How to verify it's done} |

---

## Non-Functional Requirements

### Performance
- Response time: {e.g., "< 200ms for 95th percentile"}
- Throughput: {e.g., "100 requests/second"}
- Resource limits: {e.g., "< 512MB memory"}

### Security
- Authentication: {e.g., "JWT tokens required"}
- Authorization: {e.g., "Role-based access control"}
- Data protection: {e.g., "Encrypt PII at rest"}

### Reliability
- Availability: {e.g., "99.9% uptime"}
- Error handling: {e.g., "Graceful degradation"}
- Recovery: {e.g., "Auto-retry with backoff"}

### Scalability
- {e.g., "Horizontal scaling via load balancer"}
- {e.g., "Stateless design for multi-instance"}

---

## Constraints

### Technical
- Must use: {existing tech stack, APIs, databases}
- Cannot use: {blacklisted dependencies, deprecated APIs}
- Must integrate with: {existing systems}

### Business
- Budget: {if applicable}
- Timeline: {hard deadlines, milestones}
- Compliance: {GDPR, SOC2, etc.}

### Dependencies
| Dependency | Type | Owner | Status |
|------------|------|-------|--------|
| {External API} | External | {Team} | Available |
| {Database migration} | Internal | {Name} | In Progress |

---

## Out of Scope

*Explicitly list what this feature does NOT include to prevent scope creep.*

- {Item 1: e.g., "Mobile app support - separate initiative"}
- {Item 2: e.g., "Legacy data migration - handled by data team"}
- {Item 3: e.g., "Admin dashboard - phase 2"}

---

## User Stories (Optional)

*Use if helpful for understanding user perspective.*

**As a** {user type}
**I want to** {action}
**So that** {benefit}

**Acceptance Criteria:**
- Given {context}, when {action}, then {result}
- Given {context}, when {action}, then {result}

---

## Technical Notes (Optional)

*Capture early technical decisions or considerations.*

### Proposed Approach
{High-level technical approach if known}

### Open Questions
- [ ] {Question 1}
- [ ] {Question 2}

### Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| {Risk} | High/Med/Low | {How to address} |

---

## Approvals

| Role | Name | Date | Status |
|------|------|------|--------|
| Product | {Name} | | Pending |
| Tech Lead | {Name} | | Pending |
| Stakeholder | {Name} | | Pending |

---

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | {Date} | {Name} | Initial draft |

---

<!--
USAGE TIPS:
1. Start with Problem Statement and Goals - everything else follows
2. Use MoSCoW prioritization (Must/Should/Could/Won't)
3. Keep acceptance criteria testable and specific
4. Review with stakeholders before starting development
5. Link to this doc from task files: docs/tasks/{task}.md
-->
