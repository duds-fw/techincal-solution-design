# Definition of Done (DoD)

> Enterprise standard for determining when a development task, story, or project is considered complete.

---

# 1. Purpose

## Description

The Definition of Done (DoD) defines the mandatory conditions that must be met before any piece of work is considered complete.

The DoD ensures consistency across teams, prevents incomplete work from reaching production, and establishes a shared understanding of quality expectations.

This document applies to all software delivery activities including development, testing, documentation, deployment, and operational readiness.

---

# 2. Objectives

This document aims to:

- Define clear completion criteria.
- Prevent incomplete work from reaching production.
- Improve quality across teams.
- Reduce rework and defects.
- Support continuous delivery.
- Establish shared quality expectations.
- Enable transparent progress tracking.

---

# 3. Scope

The DoD applies to:

- User Stories
- Technical Tasks
- Bugs
- Spikes
- Epics (aggregated)
- Projects (aggregated)

---

# 4. Story-Level Definition of Done

## 4.1 Development

| # | Criteria | Mandatory |
|---|----------|-----------|
| 1 | Code compiles without errors | Yes |
| 2 | Code follows coding standards | Yes |
| 3 | Unit tests written and passing | Yes |
| 4 | Code reviewed and approved | Yes |
| 5 | No critical or high SonarQube issues | Yes |
| 6 | Integration tests passing | Yes |
| 7 | API documentation updated | Conditional |
| 8 | Database migration tested | Conditional |

## 4.2 Testing

| # | Criteria | Mandatory |
|---|----------|-----------|
| 1 | Acceptance criteria verified | Yes |
| 2 | Edge cases tested | Yes |
| 3 | Error scenarios tested | Yes |
| 4 | Regression tests passing | Yes |
| 5 | Performance impact assessed | Conditional |
| 6 | Security impact assessed | Conditional |

## 4.3 Documentation

| # | Criteria | Mandatory |
|---|----------|-----------|
| 1 | Technical documentation updated | Yes |
| 2 | API documentation updated | Conditional |
| 3 | Runbook updated | Conditional |
| 4 | Configuration documented | Conditional |

## 4.4 Deployment

| # | Criteria | Mandatory |
|---|----------|-----------|
| 1 | Feature deployed to lower environment | Yes |
| 2 | Feature flag configured (if applicable) | Conditional |
| 3 | Rollback plan documented | Yes |
| 4 | Deployment validated in lower environment | Yes |

---

# 5. Sprint-Level Definition of Done

| # | Criteria | Mandatory |
|---|----------|-----------|
| 1 | All stories in sprint meet story-level DoD | Yes |
| 2 | Integration tests passing | Yes |
| 3 | Build pipeline green | Yes |
| 4 | Code coverage meets threshold | Yes |
| 5 | No open critical defects | Yes |
| 6 | Sprint demo completed | Yes |
| 7 | Sprint retrospective conducted | Yes |

---

# 6. Release-Level Definition of Done

| # | Criteria | Mandatory |
|---|----------|-----------|
| 1 | All stories meet story-level DoD | Yes |
| 2 | All sprints meet sprint-level DoD | Yes |
| 3 | Architecture review completed | Yes |
| 4 | Security review completed | Yes |
| 5 | Performance testing completed | Yes |
| 6 | UAT sign-off obtained | Yes |
| 7 | Release notes drafted | Yes |
| 8 | Runbook complete | Yes |
| 9 | Monitoring configured | Yes |
| 10 | Alerting configured | Yes |
| 11 | Rollback plan validated | Yes |
| 12 | CAB approval obtained | Yes |
| 13 | Operations team notified | Yes |
| 14 | Hypercare plan defined | Yes |

---

# 7. Project-Level Definition of Done

| # | Criteria | Mandatory |
|---|----------|-----------|
| 1 | All releases deployed to production | Yes |
| 2 | All acceptance criteria met | Yes |
| 3 | All non-functional requirements validated | Yes |
| 4 | Post-implementation review completed | Yes |
| 5 | Documentation complete and up-to-date | Yes |
| 6 | Knowledge transfer completed | Yes |
| 7 | Operational handover completed | Yes |
| 8 | Technical debt documented | Yes |
| 9 | Lessons learned captured | Yes |

---

# 8. Quality Gates

| Gate | Trigger | Approver |
|------|---------|----------|
| Design Review | Before development | Solution Architect |
| Code Review | Before merge | Technical Lead |
| Security Review | Before release | Security |
| Architecture Review | Before release | Enterprise Architect |
| Performance Review | Before release | Performance Engineer |
| CAB Approval | Before production | Change Advisory Board |

---

# 9. DoD Compliance Tracking

Compliance should be tracked per sprint using the following format:

| Story ID | DoD Met | Exceptions | Approver | Date |
|----------|---------|------------|----------|------|

---

# 10. Exceptions

Any exception to the DoD must be:

- Documented
- Approved by the Product Owner and Technical Lead
- Tracked
- Resolved in a subsequent sprint

---

# 11. See Also

- ../governance/architecture-review-checklist.md
- ../governance/design-review-checklist.md
- ../release/release-checklist.md
- ../release/release-management.md
- ../design/project-tsd.md
