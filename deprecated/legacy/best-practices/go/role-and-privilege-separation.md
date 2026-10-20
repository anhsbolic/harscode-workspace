# role-and-privilege-separation.md

**Location:** `go/role-and-privilege-separation.md`

**Principle**
If there is a design constraint such as "role X and role Y must never be held by the same entity" or "role X must recuse itself from resources it is related to," that constraint must be enforced at the service/DB layer — not just validated in the UI or described in a policy document. A constraint that only lives in the UI or documentation is a privilege-escalation vector: anyone who bypasses the UI (a direct API call, a bug, an insider) can violate it.

**Bad**
```go
// the "admin cannot also be reviewer" constraint is only checked in the frontend
func AssignReviewerRole(actorID string) error {
    return repo.AddRole(actorID, "reviewer") // no server-side check of existing roles
}
```

**Good**
```go
func AssignReviewerRole(actorID string) error {
    existingRoles, err := repo.GetRoles(actorID)
    if err != nil { return err }
    if slices.Contains(existingRoles, "admin") {
        return ErrIncompatibleRole // enforced at the service layer, not just the UI
    }
    return repo.AddRole(actorID, "reviewer")
}

// ideally also enforced at the DB level (constraint/trigger) as defense-in-depth
```

**Checklist**
- [ ] Every "role A and role B cannot coexist" constraint is enforced at the service layer, not just the UI
- [ ] "Must recuse from a related resource" constraints are checked at the decision point (approval, review), not only at initial assignment
- [ ] The most critical constraints have DB-level defense-in-depth (constraint/trigger)
- [ ] There is a test that attempts to violate the constraint directly via a service call, bypassing the UI