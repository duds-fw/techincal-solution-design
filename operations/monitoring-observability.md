# Monitoring & Observability Standard

> Enterprise standard for logging, metrics, tracing, dashboards, and alerting.

---

# 1. Purpose

## Description

This document defines the enterprise standard for monitoring and observability.

The objective is to ensure every production system provides sufficient visibility to detect issues, diagnose problems, understand behavior, and maintain operational health.

This standard applies to:

- All production applications
- All production infrastructure
- All production databases
- All production integrations
- CI/CD pipelines

---

# 2. Objectives

This standard aims to:

- Ensure comprehensive system visibility.
- Reduce mean time to detect (MTTD).
- Reduce mean time to resolve (MTTR).
- Support proactive issue identification.
- Enable performance optimization.
- Support capacity planning.
- Facilitate troubleshooting.

---

# 3. The Three Pillars

| Pillar | Purpose |
|--------|---------|
| Logs | Detailed event records |
| Metrics | Numerical measurements over time |
| Traces | Request flow across services |

---

# 4. Logging

## 4.1 Log Levels

| Level | When to Use |
|-------|-------------|
| ERROR | System error requiring attention |
| WARN | Unexpected condition, not an error |
| INFO | Significant business or system event |
| DEBUG | Detailed diagnostic information |
| TRACE | Highly detailed diagnostic (temporary) |

## 4.2 Log Format

Use structured logging (JSON).

```json
{
  "timestamp": "2024-01-15T10:30:00Z",
  "level": "ERROR",
  "service": "order-service",
  "traceId": "abc-123",
  "spanId": "def-456",
  "message": "Failed to process order",
  "orderId": "ORD-789",
  "error": "Connection timeout",
  "stackTrace": "..."
}
```

## 4.3 Required Fields

| Field | Required | Description |
|-------|----------|-------------|
| timestamp | Yes | ISO-8601 UTC |
| level | Yes | Log level |
| service | Yes | Service name |
| traceId | Yes | Distributed trace ID |
| message | Yes | Human-readable message |
| error | Conditional | Error details |
| stackTrace | Conditional | Stack trace |

## 4.4 Sensitive Data

Never log:

- Passwords
- Secrets
- Full credit card numbers
- Social security numbers
- Authentication tokens

Mask sensitive fields:

```json
{
  "email": "j***@example.com",
  "phone": "***1234"
}
```

---

# 5. Metrics

## 5.1 Metric Types

| Type | Description | Example |
|------|-------------|---------|
| Counter | Monotonically increasing | Request count |
| Gauge | Can increase or decrease | CPU usage |
| Histogram | Distribution of values | Response time |
| Summary | Pre-calculated quantiles | P99 latency |

## 5.2 RED Method (Services)

| Metric | Description |
|--------|-------------|
| Rate | Requests per second |
| Errors | Errors per second |
| Duration | Request latency |

## 5.3 USE Method (Resources)

| Metric | Description |
|--------|-------------|
| Utilization | % resource in use |
| Saturation | Work queued |
| Errors | Error events |

## 5.4 Application Metrics

| Metric | Type | Description |
|--------|------|-------------|
| http_requests_total | Counter | Total HTTP requests |
| http_request_duration_seconds | Histogram | Request latency |
| http_requests_errors_total | Counter | Total errors |
| db_connection_pool_active | Gauge | Active DB connections |
| kafka_messages_published_total | Counter | Messages published |
| kafka_messages_consumed_total | Counter | Messages consumed |

## 5.5 Infrastructure Metrics

| Metric | Type | Description |
|--------|------|-------------|
| cpu_usage_percent | Gauge | CPU utilization |
| memory_usage_percent | Gauge | Memory utilization |
| disk_usage_percent | Gauge | Disk utilization |
| network_io_bytes | Gauge | Network traffic |

---

# 6. Distributed Tracing

## Requirements

| Requirement | Standard |
|-------------|----------|
| Protocol | OpenTelemetry |
| Propagation | W3C Trace Context |
| Sampling | Configurable (default: 1%) |
| Export | OTLP to collector |
| Services | All microservices |

## Trace Context

Every request must propagate:

- `traceparent` header
- `tracestate` header (optional)

---

# 7. Dashboards

## 7.1 Required Dashboards

| Dashboard | Audience | Contents |
|-----------|----------|----------|
| Service Overview | All | RED metrics, health |
| Infrastructure | Ops | CPU, memory, disk, network |
| Database | DBA/Dev | Connections, queries, locks |
| Business | Product | Key business metrics |
| Error Tracking | Dev | Errors, stack traces |

## 7.2 Dashboard Design

- Use consistent time ranges.
- Use consistent color coding.
- Include thresholds.
- Include links to runbooks.
- Use consistent naming convention.

---

# 8. Alerting

## 8.1 Alert Levels

| Level | Description | Response |
|-------|-------------|----------|
| Critical | System down or data loss | Immediate action |
| Warning | Degraded performance | Investigate soon |
| Info | Noteworthy event | Review when possible |

## 8.2 Alert Rules

| Rule | Threshold |
|------|-----------|
| Error Rate | > 1% (Warning), > 5% (Critical) |
| Response Time P95 | > 1s (Warning), > 5s (Critical) |
| CPU Usage | > 80% (Warning), > 95% (Critical) |
| Memory Usage | > 80% (Warning), > 95% (Critical) |
| Disk Usage | > 80% (Warning), > 90% (Critical) |
| DB Connections | > 80% pool (Warning), > 95% (Critical) |

## 8.3 Alert Routing

| Severity | Channel |
|----------|---------|
| Critical | PagerDuty / Phone |
| Warning | Slack / Email |
| Info | Dashboard only |

## 8.4 Alert Fatigue Prevention

- Tune thresholds based on baseline.
- Use multi-condition alerts.
- Require human action for critical alerts.
- Review alerts quarterly.

---

# 9. Health Checks

## 9.1 Endpoint

Every service must expose:

```
GET /health
GET /health/live
GET /health/ready
```

## 9.2 Health Check Response

```json
{
  "status": "UP",
  "components": {
    "database": { "status": "UP" },
    "cache": { "status": "UP" },
    "kafka": { "status": "DOWN" }
  }
}
```

---

# 10. Observability Checklist

Before production deployment:

- [ ] Structured logging implemented
- [ ] Log levels configured
- [ ] Sensitive data masked
- [ ] Application metrics exposed
- [ ] Dashboard created
- [ ] Alerts configured
- [ ] Health check endpoint implemented
- [ ] Distributed tracing configured
- [ ] Runbook linked from dashboard

---

# 11. Technology Stack

| Layer | Recommended |
|-------|------------|
| Logging | ELK / Loki / CloudWatch |
| Metrics | Prometheus / CloudWatch |
| Tracing | OpenTelemetry / Jaeger |
| Dashboards | Grafana / CloudWatch |
| Alerting | Prometheus AlertManager / PagerDuty |

---

# 12. References

- ../operations/operational-runbook.md
- ../operations/incident-runbook.md
- ../architecture/non-functional-requirements.md
- ../design/product-tsd.md
- ../design/project-tsd.md
