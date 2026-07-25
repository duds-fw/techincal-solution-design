# Release Notes - NexaPay Fraud Detection v1.1

**Release Date:** 2024-11-20
**Release Manager:** Release Management Team
**Status:** Released

---

## Summary

Release v1.1 introduces ML-based real-time fraud detection for the NexaPay Payment Platform. This release replaces the legacy rule-based fraud detection with a machine learning model that provides more accurate risk scoring while maintaining low latency.

---

## New Features

| Feature | Description | Requirement |
|---------|-------------|-------------|
| ML-based Fraud Scoring | Real-time risk scoring using trained ML model | BR-001 |
| Configurable Risk Rules | Business-configurable risk rules without code changes | BR-002 |
| Three-Tier Decision | Approve, step-up authentication, or reject based on risk score | BR-001 |
| Real-Time Alerts | Instant alerts for high-risk transactions | BR-004 |
| Fraud Dashboard | Real-time fraud metrics and monitoring | BR-005 |

---

## Enhancements

| Enhancement | Description | Ticket |
|-------------|-------------|--------|
| Payment latency optimization | Reduced average latency by 15ms | NEXAFD-101 |
| Feature caching | Redis-based feature caching for faster scoring | NEXAFD-102 |

---

## Bug Fixes

| Fix | Description | Ticket |
|-----|-------------|--------|
| Race condition in feature computation | Fixed concurrent access to feature store | NEXAFD-103 |
| Incorrect timeout handling | Fixed timeout propagation in fraud API | NEXAFD-104 |

---

## Breaking Changes

| Change | Impact | Migration |
|--------|--------|-----------|
| New fraud API dependency | Payment Service must call Fraud Detection API | Feature flag controlled |
| New database tables | Requires migration script execution | Automatic via Flyway |

---

## Deprecations

| Feature | Deprecated In | Removal Target | Alternative |
|---------|---------------|----------------|-------------|
| Legacy rule engine | v1.1 | v1.3 | ML-based scoring |

---

## Configuration Changes

| Change | Environment | Value |
|--------|-------------|-------|
| FRAUD_API_TIMEOUT | All | 30ms |
| FRAUD_SCORE_THRESHOLD_LOW | All | 0.3 |
| FRAUD_SCORE_THRESHOLD_HIGH | All | 0.7 |

---

## Database Changes

| Change | Type | Rollback Script |
|--------|------|-----------------|
| fraud_scoring_log table | New | V012__rollback_fraud_scoring_log.sql |
| fraud_alerts table | New | V013__rollback_fraud_alerts.sql |
| risk_rules table | New | V014__rollback_risk_rules.sql |

---

## Known Issues

| Issue | Impact | Workaround | Target Fix |
|-------|--------|------------|------------|
| Dashboard delay (5s) | Minor | None needed | v1.1.1 |

---

## Deployment Instructions

1. Execute database migrations
2. Deploy Fraud Detection Service
3. Deploy Feature Service
4. Deploy Alert Service
5. Enable fraud API call in Payment Service (feature flag)
6. Verify fraud scoring in SIT
7. Deploy to UAT and complete UAT
8. Deploy to PREPROD and complete performance test
9. Deploy to PROD

---

## Rollback Instructions

Reference: ../operations/rollback-procedure.md

1. Disable fraud API feature flag in Payment Service
2. Payment Service reverts to legacy rule engine
3. No database rollback needed (new tables are additive)

---

## Verification Steps

| # | Step | Expected Result | Status |
|---|------|-----------------|--------|
| 1 | Health check fraud detection service | UP | Pass |
| 2 | Test low-risk transaction | Approved | Pass |
| 3 | Test high-risk transaction | Rejected | Pass |
| 4 | Verify latency < 50ms | P99 = 32ms | Pass |
| 5 | Verify alert generation | Alert within 1 minute | Pass |

---

## Monitoring

| Dashboard | URL |
|-----------|-----|
| Fraud Detection | https://grafana.internal/d/fraud-detection |
| Payment Service | https://grafana.internal/d/payment-service |
| Infrastructure | https://grafana.internal/d/infrastructure |

---

## Support Contacts

| Role | Name | Contact |
|------|------|---------|
| Release Manager | Release Team | #release-support |
| Technical Lead | Tech Lead | #tech-lead |
| On-Call Engineer | SRE Team | PagerDuty |

---

## Post-Release Hypercare

| Parameter | Value |
|-----------|-------|
| Duration | 72 hours |
| On-Call Team | SRE + Payment Team |
| Escalation Path | On-Call → Team Lead → Engineering Manager |
