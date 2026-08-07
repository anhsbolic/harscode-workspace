> **Location:** `best-practices/go/error-wrapping.md`

# Error Wrapping Consistency

## 1. String-matching an error message is a silent coupling to text that can change without warning

**Principle:** `strings.Contains(err.Error(), "not found")` couples your control flow to the literal text of an error message — a text that can change (a dependency upgrade, a refactor, a typo fix) with no compiler warning and no test failure unless that exact scenario is covered. `errors.Is`/`errors.As` couple to the error's *identity/type* instead, which is what actually stays stable across refactors.

### Bad
```go
_, err := repo.FindByID(ctx, id)
if err != nil && strings.Contains(err.Error(), "not found") {
    return nil, ErrNotFound
}
```
If the underlying error message ever changes from `"not found"` to `"no rows found"` (e.g. after swapping the DB driver or ORM), this check silently stops matching — no panic, no test failure unless the test happens to exercise this exact path with the new message.

### Good
```go
_, err := repo.FindByID(ctx, id)
if errors.Is(err, sql.ErrNoRows) {
    return nil, ErrNotFound
}
```
Or, for custom error types:
```go
var notFoundErr *NotFoundError
if errors.As(err, &notFoundErr) {
    return nil, ErrNotFound
}
```

**Checklist:**
- Never branch application logic on `err.Error()` string content — treat this as a code smell to flag in review every time.
- If a dependency returns an error you need to detect reliably and it doesn't expose a sentinel error or typed error, that's worth wrapping at the boundary into your own sentinel/type specifically so the rest of the codebase doesn't need to know the dependency's internal error representation.

---

## 2. Wrapping with `%w` preserves the chain for `errors.Is`/`errors.As`; `%v` silently breaks it

**Principle:** `fmt.Errorf("doing X: %w", err)` wraps `err` so `errors.Is`/`errors.As` can still find it further up the call stack. `fmt.Errorf("doing X: %v", err)` produces a new error with no relationship to the original — any `errors.Is` check higher up the stack silently stops working, with no error or warning that the chain broke.

### Bad
```go
func (s *service) UpdateOrder(ctx context.Context, id string) error {
    if err := s.repo.Update(ctx, id); err != nil {
        return fmt.Errorf("updating order %s: %v", id, err) // chain broken
    }
    return nil
}

// elsewhere:
if errors.Is(err, sql.ErrNoRows) { ... } // never true, even if the root cause was ErrNoRows
```

### Good
```go
return fmt.Errorf("updating order %s: %w", id, err)
```

**Checklist:**
- Default to `%w` when wrapping an error you want callers up the stack to still be able to inspect via `errors.Is`/`errors.As`. Use `%v` only when deliberately hiding the original error's identity is the intent (rare — usually when crossing a boundary where the internal error type genuinely shouldn't leak, e.g. into a public API response).
- When adding a new wrap point to existing code, check whether anything upstream already relies on `errors.Is`/`errors.As` for this error — switching `%w` to `%v` (or vice versa) changes that behavior silently.