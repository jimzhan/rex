# Database Schema & Performance Standards

Applies to PostgreSQL (Primary) and Redis (Cache).

## 1. Schema Design Conventions
- **Naming:** Tables in `snake_case`, Columns in `snake_case`. Primary keys must be `id` (UUID v7).
- **Timestamps:** Every table MUST contain `updated_at` (TIMESTAMP) columns unless it's for auditting.
- **Not Null:** Avoid nullable columns where possible; define strict defaults instead.

## 2. Sharding & Partitioning Strategy
- **Hash Sharding:** For horizontal scaling, shard by `user_id` or `tenant_id`.
- **Time-based Partitioning:** For logs or event tables, partition by range (e.g., by month).
- **Routing:** Application logic must route queries to the correct shard; database views are not allowed for cross-shard joins.

## 3. Transaction Norms
- **Short Transactions:** Keep database transactions as short as possible. Avoid user I/O or network calls inside a database transaction.
- **Isolation Level:** Use `READ COMMITTED` as default. Use `REPEATABLE READ` only when strictly necessary for consistency.
- **Pessimistic Locking:** Use `SELECT ... FOR UPDATE` sparingly; prefer Optimistic Locking using a `version` column.

## 4. Performance Guardrails
- **Indexing:** Any query used in a `WHERE` clause or `JOIN` condition must be indexed.
- **Query Complexity:** Queries joining more than 3 tables must be reviewed for optimization. Avoid `SELECT *` in production code.
- **Rate Limiting:** Connection pool size must be capped to avoid "Too Many Connections" errors.

