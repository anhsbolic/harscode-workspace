# goqu — Query Builder Best Practices

> Status: DRAFT (generic industry knowledge). Not yet grounded in real codebase examples —
> refine with actual cases from the monorepo before treating this as settled guidance.
> Category: `best-practices/go/` (library usage in Go, not Postgres-rule-specific).

## When this file applies
Trigger keywords: `goqu`, `query builder`, `dynamic filter`, `dialect`, `dataset`, `.ToSQL()`.
Applies whenever code builds SQL via goqu instead of raw string concatenation or a full ORM.

## Why goqu at all (context, not dogma)
goqu sits between raw SQL and a full ORM: keeps SQL-shaped thinking (explicit control over
joins, subqueries, dialect quirks) while removing manual string concatenation. Best fit for
teams that want SQL visibility without hand-rolling `fmt.Sprintf` queries. Not a replacement
for hand-written SQL when a query is genuinely complex (deep CTEs, window functions) — goqu
supports raw SQL escape hatches for those cases; don't force everything through the builder.

---

## 1. Dialect setup — do it once, not per-query
```go
var dialect = goqu.Dialect("postgres")
```
Set the dialect at package/app init, not inline in every query function. A per-query
`goqu.Dialect(...)` call scattered across the codebase is a smell — if the DB ever changes,
that's a single-line fix, not a grep-and-replace.

## 2. Always parameterize — never string-build predicate values
```go
// Good — goqu parameterizes automatically
ds := dialect.From("orders").Where(goqu.Ex{"status": status})

// Bad — defeats the entire point of using a query builder
ds := dialect.From("orders").Where(goqu.L("status = '" + status + "'"))
```
`goqu.Ex{}` and `goqu.C()` expressions parameterize values by default. The moment `goqu.L()`
(raw SQL literal) is used with string-concatenated user input, goqu's safety guarantee is
gone — this is a SQL injection vector, not a style nitpick. `goqu.L()` should only wrap
static SQL fragments (function calls, casts), never anything derived from request input.

## 3. Prefer `Prepared(true)` for anything hitting production paths
```go
ds := dialect.From("orders").Where(goqu.Ex{"id": orderID}).Prepared(true)
sql, args, err := ds.ToSQL()
```
`Prepared(true)` returns placeholder syntax (`$1`, `$2`, ...) + a separate args slice instead
of inlined literals. This is what should be passed to `db.Query`/`db.Exec`. Inlined-literal
SQL (`Prepared(false)`, the default) is fine for debug logging/printing a query, never for
execution.

## 4. Dynamic filters — build conditionally, don't branch the whole query
```go
ds := dialect.From("orders")
if status != "" {
    ds = ds.Where(goqu.Ex{"status": status})
}
if fromDate != nil {
    ds = ds.Where(goqu.C("created_at").Gte(fromDate))
}
```
Reassign the dataset per condition rather than writing N branches that each build a
near-duplicate full query. goqu datasets are immutable value types — `.Where()` returns a
new dataset, so this pattern is safe and idiomatic, not a footgun.

## 5. Struct scanning — mind the tag and the zero-value trap
```go
type Order struct {
    ID     int64  `db:"id"`
    Status string `db:"status"`
}
```
- Every field goqu should scan into needs a `db:"..."` tag — goqu does not default to
  lowercased field names reliably across all scan paths.
- Nullable columns need `sql.NullString`/`sql.NullInt64` (or a pointer type) — scanning a
  NULL into a bare `string` will error at scan time, not compile time. This is a common
  "works until a null shows up in prod" gap.

## 6. Transactions — pass `*goqu.TxDatabase`, not raw `*sql.Tx`, through query-building code
```go
tx, err := goqu.NewTx(dialect, rawTx) // or db.WithTx(func(td *goqu.TxDatabase) error {...})
```
If a function builds goqu datasets, keep it consistent with goqu's own tx wrapper rather than
mixing raw `*sql.Tx` calls and goqu dataset calls in the same function — avoids subtle bugs
where half a function's queries silently run outside the transaction.

## 7. Testing — assert on generated SQL, not just execution
```go
sql, args, _ := ds.Prepared(true).ToSQL()
assert.Equal(t, `SELECT * FROM "orders" WHERE "status" = $1`, sql)
assert.Equal(t, []interface{}{"pending"}, args)
```
For non-trivial dynamic-filter logic, a unit test asserting the exact generated SQL +
args catches silent regressions (wrong operator, missing parenthesization on OR/AND
combinations) that an integration test against a real DB might not isolate as clearly.

## 8. Common pitfalls checklist
- [ ] No `goqu.L()` wrapping user-controlled input (→ injection risk)
- [ ] `Prepared(true)` used on every execution path (not just `ToSQL()` for logging)
- [ ] Every scanned struct field has a `db` tag
- [ ] Nullable columns use nullable Go types, not bare primitives
- [ ] Dialect instantiated once, not per-call
- [ ] Transaction-scoped queries all go through the same tx wrapper — no mixing raw `*sql.Tx`
- [ ] Complex queries (CTEs, window functions) use raw SQL escape hatch instead of being
      forced through the builder awkwardly

---

## Open questions (to resolve once real cases exist)
- Does the monorepo have a house convention for where dialect gets instantiated (DI
  container? package-level var? per-repository-struct?) — this file currently only states
  the generic "once, not per-query" principle.
- Any existing pattern for building reusable predicate fragments (e.g. a `scopes`-style
  helper) to avoid duplicating `goqu.Ex{}` blocks across query functions?
- Real examples of dynamic filter code in the monorepo to replace/supplement the generic
  snippet in §4.