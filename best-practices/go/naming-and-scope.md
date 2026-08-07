# Naming & Test Scope

## 1. Variable names should reveal *source* and *purpose*, not just *shape*

**Principle:** If two computed results share the same shape (e.g., both `[]string` diff results) within the same scope, but the parameters/filters that produced them differ, generic naming (`updates`, `changes`, `result`) hides that difference and opens the door to misuse.

**Pattern:** a function is called twice in one scope with different filtering parameters — once to answer question A, once to answer question B — and both calls happen to return the same type. Without explicit naming, both look like an interchangeable "generic diff," even though their contents and intended use differ substantially.

### Bad
```go
changesA, _, err := ths.GetChanges(old, new, append(ths.config.SkipFieldsA, "x"))
...
changesB, rawB, err := ths.GetChanges(old, new, ths.config.SkipFieldsB)
```
`changesA` vs `changesB` — different names, but neither says "careful, both are diff paths but with different filtering concepts." Another developer can easily grab the wrong one for logic that actually needed the other basis.

### Good
```go
triggerDecisionChanges, _, err := ths.GetChanges(old, new, append(ths.config.SkipFieldsA, "x"))
// used ONLY for: the status-transition decision + downstream trigger

auditLogChanges, rawAuditChangelog, err := ths.GetChanges(old, new, ths.config.SkipFieldsB)
// used ONLY for: change-type classification, indexing, snapshotting
```

**Checklist:**
- If the same function is called twice in one scope with different parameters, the result variables must have names that distinguish *intended use*, not just generic technical names.
- Add a one-line comment next to the declaration stating "used only for X" whenever there's a real risk of the two being swapped.

---

## 2. Test at the lowest level that still exposes the behavior; don't duplicate tests across a dimension the code doesn't read

**Principle:** If logic can be tested as a pure function, test it as a pure function — no mocks. Don't duplicate test cases across a dimension (e.g., type A vs type B) unless the code under test actually reads that dimension.

### Bad
A large matrix of paired test cases (type-A/type-B × every scenario) for a method requiring a fully mocked service (tracer, toggle, external client, repo) — even though the condition being tested never actually reads the field that distinguishes type A from type B.

### Good
```go
func TestShouldTriggerNotification(t *testing.T) {
    matchingEntity := &Entity{Category: &CategorySpec{}}
    nonMatchingEntity := &Entity{}
    tests := []struct{ name string; entity *Entity; changes []string; want bool }{
        {"single relevant field", matchingEntity, []string{"category.code"}, true},
        {"multiple relevant fields", matchingEntity, []string{"category.code", "category.type"}, true},
        {"relevant plus unrelated field", matchingEntity, []string{"category.code", "name"}, false},
        {"unrelated field only", matchingEntity, []string{"name"}, false},
        {"no changes", matchingEntity, nil, false},
        {"non-matching entity", nonMatchingEntity, []string{"category.code"}, false},
    }
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            require.Equal(t, tt.want, shouldTriggerNotification(tt.entity, tt.changes))
        })
    }
}
```
A handful of predicate cases (no mocks) plus a small set of builder cases (mocking only the one real dependency) covers the same ground as a much larger matrix, with no loss of real coverage.

**Checklist:**
- Before writing paired test scenarios (type A vs type B), first check whether the code under test actually branches on that distinction. If not, one representative scenario plus a comment is enough.