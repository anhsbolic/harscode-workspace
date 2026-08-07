> **Location:** `best-practices/go/nil-and-zero-values.md`

# Nil vs Zero-Value Semantics

## 1. Nil map reads are safe, nil map writes panic — and both look identical at the call site

**Principle:** A nil map (declared but never `make`'d, or a zero-value struct field) reads as if it were empty (`m["key"]` returns the zero value, `ok` is `false`), but writing to it (`m["key"] = v`) panics at runtime. The two operations look symmetrical in code but behave completely differently.

### Bad
```go
type Config struct {
    Overrides map[string]string // zero value is nil if never explicitly initialized
}

func (c *Config) SetOverride(key, value string) {
    c.Overrides[key] = value // panics if Overrides was never initialized
}
```
This compiles fine, works fine in any test that happens to initialize `Overrides` first, and panics in production the first time a `Config` is constructed via its zero value and `SetOverride` is called before anything else touches `Overrides`.

### Good
```go
func NewConfig() *Config {
    return &Config{Overrides: make(map[string]string)}
}

// or, defensively, at the point of write:
func (c *Config) SetOverride(key, value string) {
    if c.Overrides == nil {
        c.Overrides = make(map[string]string)
    }
    c.Overrides[key] = value
}
```

**Checklist:**
- Any struct with a map field should either initialize it in a constructor, or every write path to that field must nil-check and initialize defensively — pick one convention and apply it consistently, don't leave it to chance which code path runs first.
- Reading from a nil map is genuinely safe and idiomatic (`if v, ok := m[key]; ok` works fine on nil `m`) — don't over-correct by unnecessarily initializing maps that are only ever read.

---

## 2. Nil slice vs empty slice serialize differently — this bites hardest at API/GraphQL boundaries

**Principle:** `var s []string` (nil) and `s := []string{}` (empty, non-nil) both have `len(s) == 0` and behave identically for most Go operations (`append`, `range`, `len`) — but they're not the same for JSON marshaling. A nil slice marshals to `null`; an empty non-nil slice marshals to `[]`. Clients that distinguish "no data" from "no results" will see a difference they didn't expect.

### Bad
```go
func (r *queryResolver) SearchProducts(ctx context.Context, filter Filter) ([]*Product, error) {
    var results []*Product // nil if no matches found
    for _, p := range r.products {
        if matches(p, filter) {
            results = append(results, p)
        }
    }
    return results, nil // returns null in the GraphQL/JSON response if no matches
}
```
A client expecting `"products": []` for "search ran, found nothing" instead sees `"products": null` — and depending on the client's null-handling, this can be treated as an error state rather than an empty result.

### Good
```go
func (r *queryResolver) SearchProducts(ctx context.Context, filter Filter) ([]*Product, error) {
    results := make([]*Product, 0) // explicitly non-nil, marshals to []
    for _, p := range r.products {
        if matches(p, filter) {
            results = append(results, p)
        }
    }
    return results, nil
}
```

**Checklist:**
- For any field/response that crosses a serialization boundary (JSON API response, GraphQL list field), decide deliberately whether "empty" and "absent/unknown" are meant to be distinguishable — if not, initialize slices as empty (`make([]T, 0)` or `[]T{}`), not nil, before returning them from that boundary.
- Internal-only code (not crossing a serialization boundary) can freely use nil slices — `append` to a nil slice works fine, and forcing unnecessary non-nil initialization everywhere adds no value there.

---

## 3. Calling a method on a nil pointer is sometimes fine, sometimes a panic — depends entirely on what the method touches

**Principle:** Go allows calling a method with a pointer receiver on a nil pointer — the call itself doesn't panic. Whether it actually panics depends on whether the method body dereferences the receiver (`ths.field`) without a nil check first.

### Bad
```go
type Node struct {
    Value int
    Next  *Node
}

func (n *Node) Sum() int {
    if n == nil {
        return 0
    }
    return n.Value + n.Next.Sum() // fine — relies on the nil check at the top of the next call
}

func (n *Node) Describe() string {
    return fmt.Sprintf("Node(%d)", n.Value) // no nil check — panics if n is nil
}
```
`Sum()` is safe by design (nil-check-first pattern, common for recursive structures). `Describe()` looks similarly innocent but panics on a nil receiver — the difference isn't visible from the call site, only from reading the method body.

### Good
Be consistent: if a type is meant to support nil-receiver calls (common for tree/list-like recursive structures, or types that wrap an optional value), every method on it should nil-check at the top, documented as part of the type's contract. If a type isn't meant to support nil receivers, that's fine too — but callers need to know which contract applies, typically via doc comments on the type.

**Checklist:**
- When designing a type where nil receivers are meaningful (recursive structures, optional wrappers), nil-check consistently across every method, not just some — inconsistency here is what turns "should be safe" into "panics in production."
- When reviewing a method with a pointer receiver, check whether the body assumes a non-nil receiver — if the type is ever constructed as `var x *T` or returned as nil from another function, that assumption needs verifying, not assuming.