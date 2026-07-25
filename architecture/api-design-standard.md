# API Design Standard

> Enterprise standard for designing, implementing, documenting, versioning, and operating APIs.

---

# 1. Purpose

## Description

This document defines the enterprise standard for API design.

The objective is to ensure all APIs are consistent, maintainable, secure, observable, backward compatible, and easy to consume.

This standard applies to:

- REST APIs
- Internal APIs
- External APIs
- Partner APIs
- Microservices
- Public APIs

---

# 2. Objectives

This standard aims to:

- Ensure consistent API design across teams.
- Reduce integration friction.
- Improve API discoverability.
- Support API governance.
- Enable safe API evolution.
- Improve consumer experience.

---

# 3. Scope

This standard applies to:

- All RESTful APIs
- GraphQL APIs (where applicable)
- gRPC APIs (where applicable)
- Internal service-to-service APIs
- External partner APIs
- Public APIs

---

# 4. Design Principles

Every API should be:

- Consumer-first
- Consistent
- Stateless
- Idempotent where applicable
- Secure by default
- Observable
- Backward compatible
- Well documented
- Versioned
- Easy to evolve

---

# 5. Resource Naming

Use nouns.

Good

```
/customers
/customers/{id}
/orders
/orders/{id}/items
```

Avoid

```
/getCustomer
/createOrder
/deleteUser
```

---

# 6. HTTP Methods

| Method | Purpose | Idempotent | Safe |
|---------|----------|------------|------|
| GET | Retrieve resource | Yes | Yes |
| POST | Create resource | No | No |
| PUT | Replace resource | Yes | No |
| PATCH | Partial update | Conditional | No |
| DELETE | Delete resource | Yes | No |

---

# 7. URI Convention

Use:

```
/api/v1/customers
```

Avoid:

```
/api/customerService
```

Rules:

- Lowercase
- Plural nouns
- Hyphen-separated words
- No verbs
- No file extensions

---

# 8. Versioning Strategy

Supported strategies:

| Strategy | Usage |
|----------|-------|
| URI Versioning | `/api/v1/customers` |
| Header Versioning | `Accept: application/vnd.api.v1+json` |

Default enterprise recommendation: URI Versioning.

Breaking changes require a new major version.

### Versioning Rules

| Change Type | Version Impact |
|-------------|---------------|
| New optional field | Minor |
| New endpoint | Minor |
| Removing field | Major |
| Changing type | Major |
| Changing semantics | Major |

---

# 9. Request Design

Every request should define:

- Required fields
- Optional fields
- Validation rules
- Default values

Use ISO-8601 for date/time.

Use UTC unless otherwise specified.

---

# 10. Response Design

Successful responses should be predictable.

Example

```json
{
  "data": {
    "id": "12345",
    "name": "John Doe"
  }
}
```

Collection

```json
{
  "data": [
    {
      "id": "12345",
      "name": "John Doe"
    }
  ]
}
```

---

# 11. Error Response

Every API should return standardized errors.

Example

```json
{
  "error": {
    "code": "CUSTOMER_NOT_FOUND",
    "message": "Customer not found.",
    "traceId": "abc-123"
  }
}
```

Do not expose:

- Stack trace
- SQL errors
- Internal implementation details

---

# 12. HTTP Status Codes

| Status | Usage |
|----------|------|
| 200 | Success |
| 201 | Created |
| 202 | Accepted |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation Error |
| 429 | Too Many Requests |
| 500 | Internal Error |
| 503 | Service Unavailable |

---

# 13. Pagination

Recommended:

```text
GET /customers?page=1&pageSize=20
```

Response

```json
{
  "data": [],
  "pagination": {
    "page": 1,
    "pageSize": 20,
    "totalItems": 500,
    "totalPages": 25
  }
}
```

---

# 14. Filtering

Use query parameters.

Example

```
GET /orders?status=PAID
GET /orders?status=PAID&createdAt=2024-01-01..2024-12-31
```

---

# 15. Sorting

```
GET /orders?sort=createdAt,-amount
```

Prefix `-` for descending order.

---

# 16. Authentication

Supported:

- OAuth 2.1
- OpenID Connect
- JWT
- API Key (exception only)

Never implement custom authentication.

---

# 17. Authorization

Authorization must be enforced by backend.

Never rely on UI permissions.

---

# 18. Idempotency

All mutating operations should support idempotency.

| Method | Idempotency |
|--------|-------------|
| POST | Via `Idempotency-Key` header |
| PUT | Inherently idempotent |
| PATCH | Via `Idempotency-Key` header |
| DELETE | Inherently idempotent |

Idempotency Key:

- Unique per client request
- Valid for 24 hours
- Stored server-side

---

# 19. Rate Limiting

Every external API should implement rate limiting.

Response Headers:

```text
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1640995200
```

When limit exceeded return `429 Too Many Requests`.

---

# 20. API Documentation

Every API should be documented using OpenAPI 3.0+.

Required documentation:

- Endpoint description
- Request schema
- Response schema
- Error codes
- Authentication requirements
- Example requests
- Example responses

---

# 21. API Security

Minimum security requirements:

- TLS 1.2+
- OAuth 2.1 / OpenID Connect
- Input validation
- Output encoding
- Rate limiting
- CORS policy
- Request size limits
- Timeout configuration

Reference: ../architecture/security-standard.md

---

# 22. API Observability

Every API should expose:

- Structured logs
- Request ID propagation
- Latency metrics
- Error rate metrics
- Throughput metrics

Reference: ../operations/monitoring-observability.md

---

# 23. API Lifecycle

| Phase | Description |
|-------|-------------|
| Design | API reviewed and approved |
| Development | API implemented |
| Testing | API validated |
| Published | API documented and available |
| Maintained | API actively supported |
| Deprecated | API scheduled for removal |
| Retired | API no longer available |

---

# 24. Best Practices

| Practice | Description |
|----------|-------------|
| Use standard HTTP methods | GET, POST, PUT, PATCH, DELETE |
| Use plural nouns | `/customers` not `/customer` |
| Use hierarchical URIs | `/customers/{id}/orders` |
| Support filtering | Use query parameters |
| Support pagination | For collection endpoints |
| Return proper status codes | Match semantic meaning |
| Validate input | Reject invalid requests early |
| Implement rate limiting | Protect against abuse |
| Document with OpenAPI | Enable discoverability |
| Version your APIs | Support evolution |
| Use consistent error format | Standardize error responses |
| Log all requests | Enable debugging |

---

# 25. Anti-Patterns

| Anti-Pattern | Why It Is Wrong |
|-------------|----------------|
| Verbs in URLs | REST is resource-oriented |
| Version in body | Hard to route |
| Returning stack traces | Security risk |
| No pagination | Performance risk |
| No rate limiting | Abuse risk |
| Custom authentication | Security risk |
| Tight coupling | Reduces flexibility |
| Ignoring HTTP semantics | Inconsistent behavior |

---

# 26. References

- ../design/product-tsd.md
- ../design/project-tsd.md
- ../architecture/security-standard.md
- ../architecture/integration-standard.md
- ../architecture/non-functional-requirements.md
- ../operations/monitoring-observability.md
