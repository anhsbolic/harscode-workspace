# authorization-and-idor.md

**Location:** `go/authorization-and-idor.md`

**Principle**
Authentication ("who you are") and authorization ("are you allowed to access this specific resource") are two concerns that must be enforced separately. Holding a valid role does not automatically mean access to any given resource is allowed — a resource-level ownership/scope check is required on every operation that accepts a resource ID from input (URL param, body, etc.). Pattern: explicitly check "is this resource within this actor's scope" at the service/middleware layer, not just "does this actor hold role X." This is especially critical in systems with multiple actor roles whose resource ownership overlaps.

**Bad**
```go
func GetCampaign(w http.ResponseWriter, r *http.Request) {
    campaignID := chi.URLParam(r, "id")
    // only checks role, never checks ownership
    if !hasRole(actor, "org_staff") {
        http.Error(w, "forbidden", 403)
        return
    }
    campaign := repo.GetByID(campaignID) // actor A can access a campaign owned by org B
    json.NewEncoder(w).Encode(campaign)
}
```

**Good**
```go
func GetCampaign(w http.ResponseWriter, r *http.Request) {
    campaignID := chi.URLParam(r, "id")
    campaign := repo.GetByID(campaignID)
    if campaign == nil {
        http.Error(w, "not found", 404)
        return
    }
    // explicit ownership/scope check, not just role check
    if !actor.HasScopeOver(campaign.OrgID) {
        http.Error(w, "not found", 404) // 404, not 403 — avoid resource-existence leak
        return
    }
    json.NewEncoder(w).Encode(campaign)
}
```

**Checklist**
- [ ] Every endpoint that accepts a resource ID from input has a scope/ownership check, not just a role check
- [ ] Scope checks are performed consistently at the service/middleware layer, not ad-hoc per handler
- [ ] The response for "resource exists but not in actor's scope" doesn't leak the resource's existence (consider 404 vs. 403 as appropriate)
- [ ] There is a dedicated IDOR test: actor A attempts to access/modify a resource owned by actor B, and it must be rejected