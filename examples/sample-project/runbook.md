# Operational Runbook - NexaPay Fraud Detection Service

| Field | Value |
|-------|-------|
| System Name | NexaPay Fraud Detection Service |
| Product Owner | Payment Platform Team |
| Technical Lead | Tech Lead |
| Operations Lead | SRE Team |
| Criticality | Business Critical |

---

# 1. System Overview

The Fraud Detection Service provides real-time ML-based risk scoring for payment transactions.

**Architecture:**

- Fraud Detection API (Java/Spring Boot)
- Feature Service (Python)
- ML Model Service (Python/TensorFlow Serving)
- Redis (Feature Store)
- PostgreSQL (Scoring Logs)

---

# 2. Monitoring & Dashboards

| Dashboard | URL | Purpose |
|-----------|-----|---------|
| Fraud Detection | https://grafana.internal/d/fraud-detection | Service health |
| ML Model | https://grafana.internal/d/ml-model | Model performance |
| Feature Store | https://grafana.internal/d/feature-store | Redis metrics |

---

# 3. Alerting

| Alert | Condition | Severity | Action |
|-------|-----------|----------|--------|
| High Error Rate | > 1% | Critical | Investigate immediately |
| High Latency | P99 > 50ms | Warning | Check model service |
| Redis Down | Connection failed | Critical | Check Redis cluster |
| Model Stale | Score unchanged > 1h | Warning | Check model pipeline |

---

# 4. Common Operations

## 4.1 Restart Fraud Detection Service

| Step | Action |
|------|--------|
| 1 | Identify affected pod |
| 2 | kubectl rollout restart deployment/fraud-detection -n nexapay |
| 3 | Verify pod health |
| 4 | Verify scoring latency |

## 4.2 Update Risk Rules

| Step | Action |
|------|--------|
| 1 | Access risk rules admin API |
| 2 | Update rule configuration |
| 3 | Verify rules loaded |
| 4 | Test with sample transaction |

## 4.3 ML Model Update

| Step | Action |
|------|--------|
| 1 | Deploy new model to model registry |
| 2 | Update model version config |
| 3 | Rolling restart model service |
| 4 | Validate model accuracy |
| 5 | Monitor latency |

---

# 5. Troubleshooting

## 5.1 High Latency

| Step | Action |
|------|--------|
| 1 | Check feature store latency |
| 2 | Check model service health |
| 3 | Check Redis connection pool |
| 4 | Check for cold start issues |
| 5 | Scale model service if needed |

## 5.2 High Error Rate

| Step | Action |
|------|--------|
| 1 | Check application logs |
| 2 | Check Redis connectivity |
| 3 | Check model service health |
| 4 | Check Payment Service calls |
| 5 | Enable legacy fallback if critical |

---

# 6. Escalation Matrix

| Severity | Response | Escalation |
|----------|----------|------------|
| P1 | 15 minutes | SRE → Team Lead → Engineering Manager |
| P2 | 30 minutes | SRE → Team Lead |
| P3 | 2 hours | SRE |

---

# 7. Known Issues

| Issue | Impact | Workaround | Status |
|-------|--------|------------|--------|
| Cold start latency spike | First request slow | Pre-warm pods | Monitoring |
