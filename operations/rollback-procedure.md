# Rollback Procedure

> Enterprise procedure for rolling back application, database, infrastructure, and configuration changes.

---

# 1. Purpose

## Description

The Rollback Procedure defines the steps to safely revert production changes when a deployment causes issues.

This document covers rollback strategies for applications, databases, configurations, and infrastructure.

---

# 2. Objectives

This procedure aims to:

- Minimize production downtime.
- Provide clear rollback steps.
- Reduce rollback execution time.
- Ensure data integrity during rollback.
- Support quick recovery.

---

# 3. Rollback Triggers

| Trigger | Action |
|---------|--------|
| Smoke test failure | Immediate rollback |
| Error rate > 5% | Immediate rollback |
| Critical defect | Immediate rollback |
| Performance degradation > 50% | Assess and rollback |
| Business stakeholder request | Immediate rollback |

---

# 4. Rollback Decision

| Step | Action |
|------|--------|
| 1 | Confirm issue severity |
| 2 | Check if hotfix is feasible (< 15 min) |
| 3 | If hotfix not feasible → Rollback |
| 4 | Notify stakeholders |
| 5 | Execute rollback |
| 6 | Validate rollback |
| 7 | Document in release notes |

---

# 5. Application Rollback

## 5.1 Container/Kubernetes Rollback

| Step | Command / Action |
|------|-----------------|
| 1 | Check current deployment status |
| 2 | Execute rollback to previous revision |
| 3 | Verify pod health |
| 4 | Validate application endpoints |
| 5 | Monitor error rates |

## 5.2 Traditional Deployment Rollback

| Step | Action |
|------|--------|
| 1 | Identify the last known good version |
| 2 | Deploy previous version to all instances |
| 3 | Verify health checks |
| 4 | Run smoke tests |
| 5 | Monitor for 15 minutes |

## 5.3 Blue/Green Rollback

| Step | Action |
|------|--------|
| 1 | Switch traffic back to blue environment |
| 2 | Verify traffic routing |
| 3 | Validate application health |
| 4 | Run smoke tests |

---

# 6. Database Rollback

## 6.1 Schema Rollback

| Step | Action |
|------|--------|
| 1 | Identify the migration to rollback |
| 2 | Execute rollback migration script |
| 3 | Verify schema state |
| 4 | Validate application compatibility |
| 5 | Test critical queries |

**Warning:** Schema rollback may require application rollback if new code depends on new schema.

## 6.2 Data Rollback

| Step | Action |
|------|--------|
| 1 | Assess data impact |
| 2 | Restore from backup if needed |
| 3 | Verify data integrity |
| 4 | Validate business rules |

---

# 7. Configuration Rollback

## 7.1 Environment Variable Rollback

| Step | Action |
|------|--------|
| 1 | Identify changed configuration |
| 2 | Restore previous values |
| 3 | Restart affected services |
| 4 | Validate behavior |

## 7.2 Feature Flag Rollback

| Step | Action |
|------|--------|
| 1 | Disable feature flag |
| 2 | Verify feature is hidden |
| 3 | Validate user experience |
| 4 | Monitor error rates |

## 7.3 ConfigMap Rollback (Kubernetes)

| Step | Action |
|------|--------|
| 1 | Restore previous ConfigMap version |
| 2 | Rolling restart affected pods |
| 3 | Verify configuration loaded |
| 4 | Validate behavior |

---

# 8. Infrastructure Rollback

| Step | Action |
|------|--------|
| 1 | Identify infrastructure change |
| 2 | Revert infrastructure change |
| 3 | Verify infrastructure health |
| 4 | Validate application connectivity |
| 5 | Monitor system health |

---

# 9. Rollback Checklist

| # | Item | Status |
|---|------|--------|
| 1 | Rollback decision confirmed | |
| 2 | Stakeholders notified | |
| 3 | Rollback steps documented | |
| 4 | Rollback executed | |
| 5 | Application health verified | |
| 6 | Smoke tests passed | |
| 7 | Error rates normal | |
| 8 | Performance normal | |
| 9 | Business validation completed | |
| 10 | Incident ticket updated | |

---

# 10. Rollback Validation

After rollback, verify:

| Check | Expected Result |
|-------|----------------|
| Application health | All endpoints healthy |
| Error rate | Below threshold |
| Response time | Within SLA |
| Data integrity | No data corruption |
| Business functions | Core functions working |
| External integrations | All integrations functional |

---

# 11. Rollback Risks

| Risk | Mitigation |
|------|------------|
| Data loss | Backup before rollback |
| Incompatibility | Rollback application with database |
| Cascading failure | Validate dependencies |
| State inconsistency | Clear caches if needed |

---

# 12. Post-Rollback

| Step | Action |
|------|--------|
| 1 | Update incident ticket |
| 2 | Communicate rollback status |
| 3 | Schedule post-mortem |
| 4 | Document root cause |
| 5 | Plan fix for next release |

---

# 13. Rollback Time Targets

| Deployment Type | Target Rollback Time |
|-----------------|---------------------|
| Application | < 5 minutes |
| Feature Flag | < 1 minute |
| Configuration | < 10 minutes |
| Database | < 30 minutes |
| Infrastructure | < 30 minutes |

---

# 14. See Also

- ../release/release-management.md
- ../release/release-checklist.md
- ../operations/operational-runbook.md
- ../operations/incident-runbook.md
- ../design/project-tsd.md
