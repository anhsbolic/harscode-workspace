> **Location:** `best-practices/graphql/resolver-n-plus-one.md`

# Resolver N+1 & Dataloader Discipline

## 1. A field resolver that queries per-item is invisible in isolation, catastrophic at scale

**Principle:** A resolver written to fetch data for a single parent object looks completely correct when tested with one item. The N+1 problem only appears when a list query returns N parents, and each triggers its own resolver call — turning 1 query into 1 + N queries.

**Why this happens:** resolvers are naturally written "per object" — GraphQL's execution model calls a field resolver once per object in the result set, so the straightforward implementation is "given this one parent, fetch its related data," which is exactly the shape that causes N+1 when not batched.

### Bad
```go
func (r *orderResolver) Customer(ctx context.Context, obj *Order) (*Customer, error) {
    return r.customerRepo.GetByID(ctx, obj.CustomerID) // one DB call per order
}
```
A query for 100 orders with their customers issues 1 query for orders + 100 queries for customers.

### Good
```go
func (r *orderResolver) Customer(ctx context.Context, obj *Order) (*Customer, error) {
    return dataloader.FromContext(ctx).CustomerLoader.Load(ctx, obj.CustomerID)
}
```
The dataloader batches all `CustomerLoader.Load` calls issued within the same execution tick into a single `WHERE id IN (...)` query, then distributes results back to each caller.

**Checklist:**
- Any resolver for a field that references another entity (not a scalar already present on the parent) is a dataloader candidate by default — write it with a loader unless you've confirmed the field is never requested in a list context.
- When adding a new relation field to an existing type, check whether a loader for the target entity already exists before writing a direct per-item fetch.

---

## 2. Dataloaders must be request-scoped, not shared globally

**Principle:** A dataloader caches results for the duration of a single request/execution to avoid re-fetching the same entity multiple times within one query. Sharing a loader instance across requests leaks stale data between unrelated users/requests and can leak data across tenants.

### Bad
```go
var globalCustomerLoader = dataloader.New(...) // package-level singleton
```
Once a customer is cached, every subsequent request sees the stale cached value indefinitely — and in a multi-tenant system, this can serve data across tenant boundaries if cache keys aren't tenant-scoped.

### Good
```go
func Middleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        loaders := NewLoaders(dbClient) // fresh loader set per request
        ctx := context.WithValue(r.Context(), loadersKey, loaders)
        next.ServeHTTP(w, r.WithContext(ctx))
    })
}
```

**Checklist:**
- A dataloader instance's lifetime must match request lifetime — constructed fresh per request (typically in middleware), never as a package-level variable.
- If multi-tenancy is in play, verify the loader's batch function itself scopes queries by tenant — the loader's per-request cache alone doesn't enforce tenant isolation.

---

## 3. Batching doesn't help if the resolver still fetches more than it needs

**Principle:** Solving N+1 with a dataloader fixes the *query count* problem but not necessarily the *over-fetching* problem — a batched query that still does `SELECT *` across many related rows for a field the client didn't ask for is still wasteful.

**Checklist:**
- For expensive relations (large objects, deeply nested fields), consider whether the GraphQL query's requested field selection can be pushed down into the batch query's column list, rather than always fetching full rows.
- Watch for resolvers that fetch and construct an entire nested object graph even when the client's query only selects one scalar field from it.