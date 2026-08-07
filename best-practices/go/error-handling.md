# Error Handling & Contract Correctness

## 1. Never return a valid result alongside a non-nil error

**Principle:** A function returning `(result, error)` must guarantee: `err == nil` → `result` can be trusted, `err != nil` → `result` must be entirely ignored by the caller. Don't let `result` already be populated before the error has even been checked.

**Why this happens:** the `return x, someCall(...)` pattern looks clean and "correct" at a glance, especially when writing multi-return functions quickly. But Go evaluates both operands before the `return` executes — `x` is computed and bound regardless of what `someCall(...)` returns.

### Bad
```go
return computedResult, ths.doSideEffectingWrite(ctx, params)
```
`computedResult` is already non-nil even if `doSideEffectingWrite` fails. A caller that only logs the error and continues using `computedResult` will act on a value that was never actually persisted or validated.

### Good
```go
if err := ths.doSideEffectingWrite(ctx, params); err != nil {
    return nil, tracerr.Wrap(err)
}
return computedResult, nil
```
The write and the return are separate statements. If the write fails, the result is dropped along with it — there's no window where a caller can grab a stale value.

**Checklist:**
- Any time you write `return a, b` where `b` is a call to another function (not a plain error literal) → check whether `a` can become stale if `b` fails. If so, split into two statements.

---

## 2. Named constants for load-bearing literals

**Principle:** String/number literals whose meaning is tied to another contract in the system (another function's output format, a path convention, a key naming scheme, etc.) should be a named constant near their source of truth — not a bare literal repeated in multiple places.

### Bad
```go
if strings.HasPrefix(field, "meta.") {
```
`"meta."` must exactly match the prefix emitted by whatever produces `field`. If that source changes its format (`meta.foo` → `meta/foo`), this check silently breaks with no compile-time error and no test failure unless someone happens to exercise this exact path.

### Good
```go
// constants.go — placed near the code that owns the format
const MetaFieldPrefix = "meta."

if strings.HasPrefix(field, MetaFieldPrefix) {
```

**Checklist:**
- A literal that appears in more than one place, or whose value derives from another function's contract (not a business value that genuinely never changes), should be a constant.
- Place the constant near its source of truth, with a comment noting what it's coupled to, so a future change to that source is more likely to surface this dependency.