---
name: data
description: Apply data modeling, migration, and pipeline standards. Use when designing schemas, writing migrations, optimizing queries, building data pipelines, or handling sensitive data. Invoke when the user mentions databases, migrations, queries, ETL, data quality, or data modeling.
---

# Data

## Data Modeling
- Define schemas explicitly — no implicit types
- Use meaningful column/field names: `created_at` not `ts`
- Always include: `id`, `created_at`, `updated_at` in persistent entities
- Normalize by default — denormalize only with documented justification
- Document relationships and cardinality

## Migrations
- Never edit a migration file that has already been applied
- Always create a new migration file for changes
- Migration names: descriptive and sequential (`20240315_add_user_role_column`)
- Always define rollback strategy before applying
- Test migrations in a staging environment first

## Query Standards
- Index columns used in frequent WHERE, JOIN, ORDER BY clauses
- Avoid SELECT * in production queries — be explicit
- Paginate large result sets — never return unbounded queries
- For security rules on queries (parameterization, injection prevention), see security skill.

## Data Pipelines
- Idempotency: re-running a pipeline should produce the same result
- Define clear source of truth for each dataset
- Document data lineage: origin, transformations applied
- Implement data quality checks at ingestion and transformation layers

## Medallion Architecture (when applicable)
- **Bronze**: raw data as-is, append-only, never modified
- **Silver**: cleaned, validated, deduplicated
- **Gold**: aggregated, business-ready, optimized for consumption

## Sensitive Data
- PII must be identified and documented
- Apply masking/anonymization in non-production environments
- Access to sensitive data must be logged and restricted
- Retention policies must be defined and enforced
