> **Location:** `best-practices/restapi/idempotency-and-versioning.md`

# Idempotency & API Versioning

## 1. Non-idempotent POST endpoints double-execute under retry

**Principle:** Clients (and infra — load balancers, mobile apps with flaky networks, retry middleware) retry requests that time out, without knowing whether the original request actually succeeded server-side. A `POST` that isn't idempotent will duplicate side effects (double charge, duplicate order, duplicate email) on retry.

**Why this happens:** the endpoint's logic is written for the "happy path — one call, one execution" and idempotency is treated as an edge case to handle later, if at all.

### Bad
```go
func (h *Handler) CreateOrder(w http.ResponseWriter, r *http.Request) {
    order := parseOrder(r)
    id := h.repo.Insert(ctx, order) // every call inserts a new row
    respondJSON(w, order)
}
```
A client that times out waiting for the response and retries creates two orders.

### Good
```go
func (h *Handler) CreateOrder(w http.ResponseWriter, r *http.Request) {
    idempotencyKey := r.Header.Get("Idempotency-Key")
    if existing, found := h.repo.FindByIdempotencyKey(ctx, idempotencyKey); found {
        respondJSON(w, existing) // return the original result, don't re-execute
        return
    }
    order := parseOrder(r)
    h.repo.InsertWithIdempotencyKey(ctx, order, idempotencyKey)
    respondJSON(w, order)
}
```
The client generates a unique key per logical operation (not per HTTP attempt) and sends it on every retry of that same operation.

**Checklist:**
- Any `POST`/`PATCH` endpoint that creates a resource or has a side effect with real-world consequences (payment, notification, external system call) should support an idempotency key.
- `GET`, `PUT` (full replace), and `DELETE` are idempotent by HTTP semantics already — don't add unnecessary idempotency-key machinery there, but verify the implementation actually honors that semantics (a `PUT` that appends instead of replaces silently breaks the contract).

---

## 2. Breaking changes without a versioning strategy force lockstep client/server deploys

**Principle:** Removing a field, changing a field's type, or changing validation rules on an existing endpoint breaks any client still expecting the old contract — and REST has no built-in mechanism (unlike GraphQL's deprecation directive) to warn clients before it happens.

### Bad
Editing `GET /v1/orders/{id}` response shape in place — renaming `total` to `totalAmount` — with no transition period. Every client (mobile app in app-store review, external partner integration) breaks simultaneously at deploy time.

### Good
- **Additive changes** (new optional field, new endpoint) ship without versioning concerns.
- **Breaking changes** get a new version (`/v2/orders/{id}`) or, for smaller contracts, an explicit deprecation window: keep both old and new fields present simultaneously, document the migration, remove the old field only after confirming no active clients depend on it (via access logs / header telemetry).

**Checklist:**
- Before changing an existing endpoint's response shape, classify the change: additive (safe) vs breaking (needs versioning or deprecation window).
- Track which API version(s) active clients are actually calling (via logs or an explicit version header) before removing anything — "probably nobody uses the old field" is not a verification step.