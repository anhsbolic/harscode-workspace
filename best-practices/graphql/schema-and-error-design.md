> **Location:** `best-practices/graphql/schema-and-error-design.md`

# Schema & Error Design

## 1. Nullable-by-default fields hide contract intent; be deliberate about non-null

**Principle:** GraphQL fields are nullable unless explicitly marked `!`. It's tempting to leave everything nullable "to be safe," but this pushes null-checking burden onto every client and erases the actual guarantee the API is making.

**Why this matters more than it seems:** a field that's *always* present in practice but declared nullable forces clients to write defensive null checks forever. A field that's declared non-null but the resolver can actually fail to produce it causes a much worse failure: a single resolver error nulls out the entire non-null chain up to the nearest nullable ancestor (GraphQL's null-propagation rule), potentially wiping out unrelated data in the same response.

### Bad
```graphql
type Order {
  id: ID!
  customer: Customer  # nullable, but customer is actually a required FK in the DB
}
```
Every client now writes `order.customer?.name` defensively, even though `customer` is never actually null in practice.

### Good
```graphql
type Order {
  id: ID!
  customer: Customer!  # matches the real guarantee: every order has a customer
}
```
But only if the resolver can genuinely always produce a `Customer` — if the underlying FK can be missing/orphaned in real data, keep it nullable and let clients handle it explicitly rather than crashing the resolver.

**Checklist:**
- Before marking a field non-null, verify the resolver can never legitimately return null/error for it in production data — including edge cases like soft-deleted related records.
- Before marking a field nullable "to be safe," check whether that pushes an unnecessary null-check burden onto every client for something that's actually always present.

---

## 2. Distinguish business errors from system errors in the response shape

**Principle:** GraphQL's top-level `errors` array is designed for *unexpected* failures (resolver exceptions, validation failures). Predictable business outcomes (validation failed, insufficient balance, item already exists) should be modeled as part of the schema's `data`, not thrown as GraphQL errors — otherwise clients can't reliably distinguish "something broke" from "your request was rejected for a normal business reason."

### Bad
```go
func (r *mutationResolver) CreateOrder(ctx context.Context, input CreateOrderInput) (*Order, error) {
    if input.Quantity > stock.Available {
        return nil, errors.New("insufficient stock") // surfaces as a generic GraphQL error
    }
    ...
}
```
The client sees this identically to a database connection failure — same `errors` array, same handling path, even though "insufficient stock" is an expected, actionable outcome the UI should render specifically.

### Good
```graphql
union CreateOrderResult = CreateOrderSuccess | InsufficientStockError | ValidationError

type CreateOrderSuccess { order: Order! }
type InsufficientStockError { available: Int!, requested: Int! }
```
Business outcomes are part of the typed schema, and clients handle them with normal type-narrowing instead of parsing error message strings.

**Checklist:**
- Before returning an error from a mutation resolver, ask: "is this a system failure, or a predictable business outcome the client's UI needs to render specifically?" Predictable outcomes belong in the schema as a result union or typed field, not the error channel.
- Reserve actual GraphQL errors for things a client genuinely can't plan for (auth failures, unexpected server errors, malformed requests).

---

## 3. Breaking schema changes are easy to make accidentally

**Principle:** Removing a field, renaming a field, changing a field from nullable to non-null (or vice versa in the wrong direction), or narrowing an enum are all breaking changes for existing clients — even if they compile fine on the server.

**Checklist:**
- Adding a field, adding an enum value, or widening nullable→required only when you've verified no existing data can violate it: generally safe.
- Removing a field, renaming a field, narrowing an enum, or changing a list to non-list: breaking. Deprecate (`@deprecated(reason: "...")`) and give clients a migration window before removing.
- Run schema diff checks in CI against the previous published schema before merging, rather than relying on manual review to catch this.