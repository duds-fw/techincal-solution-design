# Architecture Review Checklist (ARC)

> Enterprise Architecture governance checklist for reviewing and approving technical solutions.

---

# 1. Purpose

## Description

The Architecture Review Checklist provides a standardized governance process for evaluating whether a proposed solution complies with enterprise architecture principles, engineering standards, operational requirements, and security policies before implementation.

The objective is not to approve code, but to validate that the proposed solution is technically sound, maintainable, scalable, secure, and operationally supportable.

---

# 2. Objectives

This review ensures:

- Alignment with Enterprise Architecture
- Solution feasibility
- Technology standard compliance
- Security compliance
- Operational readiness
- Non-functional requirement compliance
- Risk visibility
- Long-term maintainability

---

# 3. Review Inputs

The following documents should be available before review.

| Document | Mandatory |
|-----------|-----------|
| Business Requirement | ✅ |
| Product TSD | ✅ |
| Project TSD | ✅ |
| ADR | Optional |
| API Specification | Optional |
| ERD | Optional |
| Security Assessment | Optional |

---

# 4. Review Participants

| Role | Responsibility |
|------|----------------|
| Enterprise Architect | Architecture governance |
| Solution Architect | Solution owner |
| Technical Lead | Technical implementation |
| Engineering Manager | Delivery ownership |
| Security | Security review |
| DevOps | Deployment review |
| Operations | Operational review |
| Product Owner | Business validation |

---

# 5. Business Alignment

## Review Questions

- Does the solution address the business problem?
- Is the scope clearly defined?
- Are assumptions documented?
- Are constraints documented?
- Are business capabilities identified?

Status

- Pass
- Conditional
- Fail

---

# 6. Architecture Alignment

Review:

- Business Architecture
- Application Architecture
- Data Architecture
- Technology Architecture
- Security Architecture

Questions

- Does the solution follow enterprise architecture?
- Does it introduce unnecessary coupling?
- Does it duplicate existing capability?
- Is reuse considered?
- Are architecture deviations documented?

---

# 7. Solution Design

Review:

- Component design
- Service boundaries
- Domain ownership
- Design patterns
- Error handling
- Retry
- Idempotency

Questions

- Is the design understandable?
- Is the design maintainable?
- Is the design testable?
- Is the design extensible?

---

# 8. API Review

Review:

- REST standards
- Naming convention
- Versioning
- Error handling
- Authentication
- Authorization
- Rate limiting
- Backward compatibility

---

# 9. Database Review

Review:

- Normalization
- Index strategy
- Constraints
- Migration
- Rollback
- Data ownership
- Data retention

---

# 10. Integration Review

Review:

- Internal APIs
- External APIs
- Kafka
- MQ
- Scheduler
- File Transfer
- Retry Strategy
- Timeout
- Circuit Breaker

---

# 11. Security Review

Review:

- Authentication
- Authorization
- Encryption
- Secret Management
- Sensitive Data
- Audit Logging
- OWASP
- Compliance

---

# 12. Non Functional Review

Review

- Availability
- Reliability
- Performance
- Capacity
- Scalability
- Resilience
- Recoverability
- Maintainability

---

# 13. Operational Readiness Review

Review

- Logging
- Monitoring
- Metrics
- Dashboards
- Alerts
- Runbook
- Backup
- Disaster Recovery
