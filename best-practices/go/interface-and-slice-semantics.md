> **Location:** `best-practices/go/interface-and-slice-semantics.md`

# Interface Nil Semantics & Slice Aliasing

## 1. A nil pointer stored in an interface is not a nil interface

**Principle:** An interface value is a pair: (type, value). `interfaceVar == nil` is only true when *both* the type and value are nil. If a concrete typed nil pointer is assigned to an interface variable, the interface holds a non-nil type (the pointer's type) and a nil value — so `interfaceVar == nil` is `false`, even though the underlying pointer is nil.

**Why this is especially dangerous in Go:** it happens most often with error returns, where the bug is invisible at the call site and only surfaces when something checks `if err != nil`.

### Bad
```go
type MyError struct{ msg string }
func (e *MyError) Error() string { return e.msg }

func doSomething() *MyError {
    // ... logic that may or may not produce an error ...
    return nil // returns a nil *MyError
}

func caller() error {
    var err *MyError = doSomething()
    return err // err is now a non-nil `error` interface wrapping a nil *MyError
}

// elsewhere:
if err := caller(); err != nil {
    // this branch runs even though the underlying pointer was nil!
    log.Fatal("unexpected error:", err)
}
```

### Good
```go
func caller() error {
    if err := doSomething(); err != nil {
        return err
    }
    return nil // explicitly return the nil interface, not a nil concrete pointer
}
```
Or, avoid the pattern entirely by having functions that can fail return the `error` interface directly, not a concrete pointer type, so there's no concrete-to-interface conversion happening at the return boundary.

**Checklist:**
- Never return a concrete pointer type through an `error`-typed return value (or any interface-typed return) without explicitly checking and converting nil to the interface's nil — write `return nil` explicitly rather than `return concretePtr` when `concretePtr` could be nil.
- If a function's declared return type is a concrete pointer (e.g. `*MyError`, not `error`), converting its result to an interface anywhere downstream is a place to double-check this pattern.
- `go vet` doesn't catch this — it's a semantic issue, not a syntax one. Code review vigilance is the primary defense.

---

## 2. Sub-slices share the underlying array — mutation and unexpected aliasing

**Principle:** Slicing (`s[low:high]`) doesn't copy data — the resulting slice shares the same underlying array as the original. Writes through either slice are visible through the other, until an `append` forces a reallocation (which happens silently, based on capacity, not something the code explicitly controls).

### Bad
```go
func processFirst3(items []Item) []Item {
    first3 := items[:3]
    first3[0].Status = "processed" // mutates the caller's original items[0] too
    return first3
}
```
The caller passing `items` may not expect that calling `processFirst3` mutates their original slice's underlying data — this is surprising because the function signature looks like ordinary pass-by-value.

### Good
```go
func processFirst3(items []Item) []Item {
    first3 := make([]Item, 3)
    copy(first3, items[:3])
    first3[0].Status = "processed" // only mutates the copy
    return first3
}
```
Explicitly copy when the function needs to mutate without affecting the caller's data.

**Checklist:**
- Before mutating elements of a slice received as a parameter, consider whether the caller would be surprised that their original slice changed — if so, copy first.
- Be especially careful with `append` on a sub-slice passed into a function: if capacity allows, `append` overwrites data beyond the sub-slice's length but still within the original array's capacity, silently corrupting data the caller thinks is untouched (`items[:3]` appended to can overwrite `items[3]` in the original array without reallocating).