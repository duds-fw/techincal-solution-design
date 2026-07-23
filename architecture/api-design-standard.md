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

# 2. Design Principles

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

# 3. Resource Naming

Use nouns.

Good

```
/customers
/customers/{id}
/orders
/orders/{id}
```

Avoid

```
/getCustomer
/createOrder
/deleteUser
```

---

# 4. HTTP Methods

| Method | Purpose |
|---------|----------|
| GET | Retrieve resource |
| POST | Create resource |
| PUT | Replace resource |
| PATCH | Partial update |
| DELETE | Delete resource |

---

# 5. URI Convention

Use:

```
/api/v1/customers
```

Avoid:

```
/api/customerService
```

Rules:

- lowercase
- plural nouns
- hyphen-separated words
- no verbs
- no file extensions

---

# 6. Versioning Strategy

Supported strategies:

- URI Versioning
- Header Versioning

Default enterprise recommendation:

```
/api/v1/
```

Breaking changes require a new major version.

---

# 7. Request Design

Every request should define:

- Required fields
- Optional fields
- Validation rules
- Default values

Use ISO-8601 for date/time.

Use UTC unless otherwise specified.

---

# 8. Response Design

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
    {}
  ]
}
```

---

# 9. Error Response

Every API should return standardized errors.

Example

```json
{
  "error": {
    "code": "CUSTOMER_NOT_FOUND",
    "message": "Customer not found.",
    "traceId": "..."
  }
}
```

Do not expose:

- stack trace
- SQL errors
- internal implementation

---

# 10. HTTP Status Codes

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

# 11. Pagination

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

# 12. Filtering

Use query parameters.

Example

```
GET /orders?status=PAID
```

---

# 13. Sorting

```
GET /orders?sort=createdAt,-amount
```

---

# 14. Authentication

Supported:

- OAuth 2.1
- OpenID Connect
- JWT
- API Key (exception only)

Never implement custom authentication.

---

# 15. Authorization

Authorization must be enforced by backend.

Never rely on UI permissions.

---

# 16. Idempotency
