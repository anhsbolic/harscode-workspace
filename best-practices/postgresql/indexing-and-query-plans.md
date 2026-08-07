> **Location:** `best-practices/postgresql/indexing-and-query-plans.md`

# Indexing & Query Plans

## 1. An index on a column doesn't mean the query uses it

**Principle:** Postgres only uses an index if the query's predicate matches the index's structure. Wrapping an indexed column in a function, casting its type, or comparing it against a mismatched type silently forces a sequential scan — no error, just slow.

### Bad
```sql
-- index exists on created_at (timestamp)
SELECT * FROM orders WHERE DATE(created_at) = '2026-08-01';
```
`DATE(created_at)` wraps the column in a function. Postgres can't use a plain b-tree index on `created_at` for this — it scans every row and applies the function per row.

### Good
```sql
SELECT * FROM orders
WHERE created_at >= '2026-08-01' AND created_at < '2026-08-02';
```
Range comparison directly on the raw column lets the planner use the index.

**Checklist:**
- Never wrap an indexed column in a function/cast in the `WHERE` clause unless you have a matching expression index.
- If a function-based filter is unavoidable and frequent, create an expression index: `CREATE INDEX ON orders (DATE(created_at));`.
- Run `EXPLAIN (ANALYZE, BUFFERS)` on any new query that filters on a supposedly-indexed column before merging — don't assume the index is used just because it exists.

---

## 2. Composite index column order must match the query's filter pattern

**Principle:** A composite index `(a, b, c)` is only useful as a full index for queries that filter on `a`, or `a AND b`, or `a AND b AND c` — in that left-to-right order. A query that filters on `b` alone, or `b AND c` without `a`, can't use this index efficiently (it may still be used, but only via a much less selective partial scan).

### Bad
```sql
-- index: (tenant_id, status, created_at)
SELECT * FROM orders WHERE status = 'pending' AND created_at > now() - interval '1 day';
```
This query never filters on `tenant_id`, so the composite index provides little help — Postgres likely falls back to a sequential scan or an inefficient index scan.

### Good
Either reorder the index to match actual query patterns (`(status, created_at, tenant_id)` if `status` is the most common leading filter), or add a second index tailored to this specific access pattern. Don't assume one composite index serves every query shape against the same table.

**Checklist:**
- Before adding a composite index, list the actual `WHERE` clauses that will hit this table and check the leading column matches the most common/most selective filter.
- A table with several genuinely different query shapes may need several indexes — don't force one composite index to serve all of them.

---

## 3. `SELECT *` and wide row fetches defeat covering indexes

**Principle:** A covering index (an index that includes all columns a query needs) lets Postgres answer a query from the index alone, without touching the heap (table data). `SELECT *` almost always forces a heap fetch regardless of index design, because the index can't cover columns it wasn't built to include.

### Good
```sql
CREATE INDEX ON orders (tenant_id, status) INCLUDE (total_amount, created_at);

SELECT total_amount, created_at FROM orders WHERE tenant_id = $1 AND status = 'pending';
```
This query can be answered index-only if the visibility map is up to date (helped by regular `VACUUM`).

**Checklist:**
- For hot-path queries with a known, narrow set of returned columns, consider `INCLUDE` columns on the index instead of relying on the heap fetch.
- Avoid `SELECT *` in application code querying large or frequently-hit tables — it's both a bandwidth cost and an index-effectiveness cost.

---

## 4. `LIKE '%term%'` can't use a standard b-tree index

**Principle:** A leading wildcard search defeats a standard b-tree index because b-trees are ordered structures — a search that could match anywhere in the string can't be narrowed by tree traversal.

### Bad
```sql
SELECT * FROM products WHERE name LIKE '%widget%';
```
Full sequential scan regardless of any b-tree index on `name`.

### Good
For genuine substring/full-text search, use `pg_trgm` (trigram) indexes for `LIKE`/`ILIKE` patterns, or Postgres full-text search (`tsvector`/`tsquery`) for word-based search:
```sql
CREATE EXTENSION IF NOT EXISTS pg_trgm;
CREATE INDEX ON products USING gin (name gin_trgm_ops);
```

**Checklist:**
- If a feature needs "search anywhere in the string," don't assume a plain index will help — check whether `pg_trgm` or full-text search is the actual right tool before shipping the query.