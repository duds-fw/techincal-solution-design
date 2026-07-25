# Database Design Standard

> Enterprise standard for database design, naming conventions, schema management, indexing, and data governance.

---

# 1. Purpose

## Description

This document defines the enterprise standard for database design.

The objective is to ensure all database solutions are designed consistently, perform efficiently, maintain data integrity, support scalability, and comply with organizational data governance requirements.

This standard applies to:

- Relational Databases (PostgreSQL, MySQL, Oracle, SQL Server)
- NoSQL Databases (MongoDB, DynamoDB, Cassandra)
- Data Warehouses
- Cache Stores (Redis, Memcached)

---

# 2. Objectives

This standard aims to:

- Ensure consistent database design.
- Protect data integrity.
- Optimize query performance.
- Support data governance.
- Enable maintainable schemas.
- Standardize migration practices.
- Reduce technical debt.

---

# 3. Design Principles

| Principle | Description |
|-----------|-------------|
| Normalize by default | 3NF unless justified |
| Single source of truth | No duplicate data across systems |
| Data ownership | Clear ownership per entity |
| Immutability preferred | Append over update where possible |
| Referential integrity | Enforce constraints at database level |
| Migration-driven | All changes via migration scripts |

---

# 4. Naming Conventions

## 4.1 Tables

| Rule | Example |
|------|---------|
| Plural nouns | `customers`, `orders` |
| Snake case | `order_items` |
| No prefixes (unless necessary) | `audit_log` not `tbl_audit_log` |
| Descriptive | `customer_addresses` not `addresses` |

## 4.2 Columns

| Rule | Example |
|------|---------|
| Snake case | `created_at`, `first_name` |
| Boolean prefix | `is_active`, `has_permission` |
| Foreign key | `customer_id` (table_name_id) |
| Timestamps | `created_at`, `updated_at`, `deleted_at` |
| No reserved words | Avoid `user`, `order` as column names |

## 4.3 Indexes

| Rule | Example |
|------|---------|
| Table name prefix | `idx_orders_customer_id` |
| Unique constraint | `uniq_customers_email` |
| Composite | `idx_orders_status_created` |

## 4.4 Constraints

| Rule | Example |
|------|---------|
| Primary key | `pk_customers` |
| Foreign key | `fk_orders_customer_id` |
| Unique | `uniq_customers_email` |
| Check | `chk_orders_amount_positive` |

---

# 5. Schema Design

## 5.1 Standard Columns

Every table should include:

| Column | Type | Description |
|--------|------|-------------|
| id | UUID / BIGINT | Primary key |
| created_at | TIMESTAMP | Creation time |
| updated_at | TIMESTAMP | Last update time |
| deleted_at | TIMESTAMP | Soft delete (nullable) |

## 5.2 Primary Keys

| Strategy | When to Use |
|----------|-------------|
| UUID | Distributed systems, public-facing |
| BIGINT (auto-increment) | Internal, high-performance systems |
| Composite | Relationship tables |

## 5.3 Data Types

| Data | Recommended Type |
|------|-----------------|
| UUID | UUID |
| Email | VARCHAR(255) |
| Name | VARCHAR(255) |
| Amount | DECIMAL |
| Boolean | BOOLEAN |
| Date | DATE |
| Timestamp | TIMESTAMP WITH TIME ZONE |
| JSON | JSONB (PostgreSQL) |
| Text | TEXT |

---

# 6. Indexing Strategy

## When to Create Index

| Scenario | Index Type |
|----------|-----------|
| Frequent WHERE clause | B-tree |
| Full-text search | GIN / Full-text |
| Geospatial queries | GiST / R-tree |
| JSON queries | GIN (JSONB) |
| Low cardinality | Bitmap (where supported) |

## Index Rules

- Index columns used in WHERE clauses.
- Index columns used in JOIN conditions.
- Index columns used in ORDER BY.
- Avoid over-indexing (write performance impact).
- Monitor unused indexes.

---

# 7. Constraints

| Constraint | Purpose |
|-----------|---------|
| PRIMARY KEY | Unique identifier |
| FOREIGN KEY | Referential integrity |
| UNIQUE | Prevent duplicates |
| NOT NULL | Mandatory fields |
| CHECK | Business rules |
| DEFAULT | Default values |

Enforce business rules at the database level when data integrity is critical.

---

# 8. Migration Strategy

## Requirements

| Requirement | Standard |
|-------------|----------|
| Version Control | All migrations in version control |
| Forward Migration | Every migration must have a forward script |
| Rollback Migration | Every migration must have a rollback script |
| Idempotent | Migrations must be idempotent where possible |
| Review | Database migrations reviewed by DBA |
| Testing | Migrations tested in lower environments first |
| Data Migration | Separate from schema migration |

## Migration Naming

```
V001__create_customers_table.sql
V002__add_email_index.sql
V003__create_orders_table.sql
```

Format: `V{sequence}__{description}.sql`

---

# 9. Data Retention

| Data Type | Default Retention |
|-----------|-------------------|
| Transactional data | 7 years |
| Audit logs | 7 years |
| PII data | Per regulation |
| Session data | 30 days |
| Temporary data | 90 days |
| Soft-deleted records | 90 days |

---

# 10. Backup Strategy

| Requirement | Standard |
|-------------|----------|
| Full Backup | Daily |
| Incremental | Hourly |
| Transaction Logs | Continuous (where supported) |
| Backup Retention | 30 days minimum |
| Restore Testing | Monthly |
| Cross-Region | Recommended for production |

---

# 11. Performance

| Practice | Description |
|----------|-------------|
| Query Analysis | Use EXPLAIN ANALYZE |
| Connection Pooling | Use connection pool |
| Read Replicas | Offload read queries |
| Pagination | Use cursor-based where possible |
| Batch Operations | Use batch inserts/updates |
| Avoid N+1 | Use JOINs or batch fetching |
| Monitor Slow Queries | Enable slow query log |

---

# 12. NoSQL Guidelines

When using NoSQL databases:

| Guideline | Description |
|-----------|-------------|
| Data Model First | Design access patterns first |
| Denormalize | Expected for performance |
| Partition Key | Choose carefully |
| Sort Key | Optimizes query patterns |
| TTL | Use for temporary data |
| Eventual Consistency | Accept where appropriate |

---

# 13. Database Security

| Requirement | Standard |
|-------------|----------|
| Access Control | Role-based access |
| Encryption at Rest | Required for sensitive data |
| Encryption in Transit | TLS required |
| SQL Injection Prevention | Parameterized queries only |
| Credential Management | Secrets manager |
| Audit Logging | Enable for all production databases |
| Network Isolation | Restricted network access |

Reference: ../architecture/security-standard.md

---

# 14. Review Checklist

Before database design is approved:

- [ ] Naming conventions followed
- [ ] Standard columns included
- [ ] Indexes defined
- [ ] Constraints defined
- [ ] Migration scripts reviewed
- [ ] Rollback scripts reviewed
- [ ] Data retention defined
- [ ] Backup strategy defined
- [ ] Performance considered
- [ ] Security reviewed
- [ ] DBA reviewed

---

# 15. References

- ../design/product-tsd.md
- ../design/project-tsd.md
- ../architecture/security-standard.md
- ../architecture/non-functional-requirements.md
- ../governance/design-review-checklist.md
- ../governance/architecture-review-checklist.md
