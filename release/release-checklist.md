# Release Checklist

> Mandatory checklist for validating release readiness before production deployment.

---

# 1. Purpose

## Description

This checklist ensures every production release is thoroughly validated before deployment.

The checklist covers architecture, development, testing, security, operations, and communication aspects of a release.

No release should proceed to production without all mandatory items completed.

---

# 2. Objectives

This checklist aims to:

- Validate release readiness.
- Prevent incomplete releases.
- Reduce deployment risk.
- Ensure stakeholder alignment.
- Support release governance.
- Maintain production stability.

---

# 3. When to Use

Complete this checklist:

- Before every production deployment.
- Before CAB review.
- During release planning.

---

# 4. Release Information

| Field | Value |
|-------|-------|
| Release Name | |
| Version | |
| Release Date | |
| Release Manager | |
| Change Type | Major / Minor / Patch / Hotfix |

---

# 5. Architecture & Design

| # | Item | Status | Owner |
|---|------|--------|-------|
| 1 | Architecture review completed | | Enterprise Architect |
| 2 | Design review completed | | Solution Architect |
| 3 | ADR approved (if applicable) | | Solution Architect |
| 4 | API design compliant | | Technical Lead |
| 5 | Database design compliant | | DBA |
| 6 | Integration design compliant | | Technical Lead |

---

# 6. Development

| # | Item | Status | Owner |
|---|------|--------|-------|
| 1 | All code merged to release branch | | Developer |
| 2 | Code review completed | | Technical Lead |
| 3 | Unit tests written and passing | | Developer |
| 4 | Integration tests passing | | Developer |
| 5 | No critical SonarQube issues | | Developer |
| 6 | Code coverage meets threshold | | Developer |
| 7 | Database migration scripts reviewed | | DBA |
| 8 | Configuration changes documented | | Technical Lead |

---

# 7. Testing

| # | Item | Status | Owner |
|---|------|--------|-------|
| 1 | SIT completed and signed off | | QA |
| 2 | UAT completed and signed off | | Product Owner |
| 3 | Regression testing completed | | QA |
| 4 | Performance testing completed | | QA |
| 5 | Security testing completed | | Security |
| 6 | Failover testing completed | | DevOps |
| 7 | Smoke tests documented | | QA |
| 8 | Edge cases tested | | QA |

---

# 8. Security

| # | Item | Status | Owner |
|---|------|--------|-------|
| 1 | Security review completed | | Security |
| 2 | OWASP checklist reviewed | | Security |
| 3 | Dependency scan clean | | Developer |
| 4 | SAST scan clean | | Developer |
| 5 | DAST scan clean (if applicable) | | Security |
| 6 | Secrets management verified | | Security |
| 7 | Sensitive data handling verified | | Security |

---

# 9. Database

| # | Item | Status | Owner |
|---|------|--------|-------|
| 1 | Migration scripts reviewed | | DBA |
| 2 | Rollback scripts reviewed | | DBA |
| 3 | Index impact assessed | | DBA |
| 4 | Performance impact assessed | | DBA |
| 5 | Backup verified | | DBA |
| 6 | Data migration tested | | DBA |

---

# 10. Operations

| # | Item | Status | Owner |
|---|------|--------|-------|
| 1 | Monitoring configured | | SRE |
| 2 | Alerting configured | | SRE |
| 3 | Dashboard updated | | SRE |
| 4 | Runbook complete | | Operations |
| 5 | Rollback plan documented | | Technical Lead |
| 6 | Rollback plan validated | | DevOps |
| 7 | Escalation path defined | | Operations |
| 8 | Support team notified | | Operations |

---

# 11. Communication

| # | Item | Status | Owner |
|---|------|--------|-------|
| 1 | Release notes drafted | | Release Manager |
| 2 | Stakeholders notified | | Release Manager |
| 3 | Support team briefed | | Release Manager |
| 4 | Deployment window confirmed | | Release Manager |
| 5 | Business team confirmed readiness | | Product Owner |

---

# 12. CAB Approval

| # | Item | Status | Owner |
|---|------|--------|-------|
| 1 | CAB package submitted | | Release Manager |
| 2 | CAB review completed | | CAB |
| 3 | CAB approval obtained | | Release Manager |
| 4 | Conditions addressed (if any) | | Release Manager |

---

# 13. Final Sign-Off

| Role | Name | Approved | Date |
|------|------|----------|------|
| Release Manager | | | |
| Enterprise Architect | | | |
| Solution Architect | | | |
| Technical Lead | | | |
| Security | | | |
| DBA | | | |
| Operations | | | |
| Product Owner | | | |

---

# 14. See Also

- ../release/release-management.md
- ../release/release-notes-template.md
- ../release/post-implementation-review.md
- ../operations/rollback-procedure.md
- ../operations/operational-runbook.md
- ../governance/definition-of-done.md
- ../governance/architecture-review-checklist.md
