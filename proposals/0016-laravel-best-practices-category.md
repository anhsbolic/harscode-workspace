# New category: laravel/

**Status:** Proposed
**Date:** 2026-09-07
**Protection Tier:** general
**Triggered by:** locking the tech stack for a new project (Laravel 12 + Inertia + React), surfacing three architecture decisions with concrete rationale that don't fit any existing category
**Target area:** best-practices
**Target file(s):**
- `best-practices/laravel/service-action-pattern.md` — new file
- `best-practices/laravel/policy-based-authorization.md` — new file
- `best-practices/laravel/seeder-only-rbac.md` — new file
- `best-practices/index.md` — new `laravel` category rows + Security Concern Map entries

## Gap found

No `laravel/` (or any PHP-framework) category exists yet — the closest analog is `react/`, a framework-specific sibling to language-level `go/`. Three recurring Laravel-specific decisions came up while locking a new project's stack, each with a concrete failure mode if not followed:

1. Repository Pattern is a common Laravel anti-pattern in this ecosystem (mirrors Eloquent's own Active Record with zero added abstraction) — but rejecting it wholesale can leave controllers doing business orchestration since "don't use Repository" doesn't say what replaces it.
2. Middleware permission gates (`can:`) and query scopes are frequently mistaken for complete authorization — neither one catches a request for someone else's resource by ID if the endpoint's query isn't scoped correctly.
3. Runtime role/permission management UIs are a common Laravel starter-kit default that widens attack surface for apps that don't actually need per-tenant custom roles.

None of these are one-off — they're structural to how Eloquent-based Laravel apps are built, independent of any one project's domain.

## Proposed change

Add a new `best-practices/laravel/` folder with three files (full content below), plus new rows in `best-practices/index.md`.

### `index.md` additions

New rows in the main trigger-keyword table:

| Category | File | Trigger keywords | Security-critical | Summary |
|---|---|---|---|---|
| laravel | [laravel/service-action-pattern.md](laravel/service-action-pattern.md) | repository pattern, action class, service class, eloquent, active record, controller bloat | no | Skip generic Repository over Eloquent; route business orchestration into single-purpose Action/Service classes, reusable queries into Model scopes |
| laravel | [laravel/policy-based-authorization.md](laravel/policy-based-authorization.md) | policy, form request, authorize, ownership check, ability, gate | yes | Middleware permission gates and query scopes are not a complete authorization check — need an explicit, independent ownership/scope check in a Policy/FormRequest |
| laravel | [laravel/seeder-only-rbac.md](laravel/seeder-only-rbac.md) | spatie permission, rbac, seeder, role management, runtime role | yes | Restrict all role/permission mutation to seeders when the app doesn't need per-tenant custom roles, to shrink attack surface |

Security Concern Map additions:

| Concern | Files (add to) |
|---|---|
| authz | + `laravel/policy-based-authorization.md`, `laravel/seeder-only-rbac.md` |

### New files

See attached file contents (`service-action-pattern.md`, `policy-based-authorization.md`, `seeder-only-rbac.md`) — full text ready to paste into `best-practices/laravel/`.

## Rationale

All three principles are generic to any Eloquent-based Laravel application — none reference a specific project's domain, table names, or business rules. They follow the same shape as existing categories:
- `service-action-pattern.md` mirrors `go/abstraction-boundaries.md`'s concern (don't add indirection without abstraction value; separate orchestration from data access) applied to Eloquent specifically.
- `policy-based-authorization.md` is the Laravel-specific instance of the same concern already covered generically for Go in `go/authorization-and-idor.md` — same underlying failure mode (resource-level check missing despite a role check existing), different framework's idiom (Policy/FormRequest vs handler-level check).
- `seeder-only-rbac.md` has no existing analog — it's a deployment/attack-surface trade-off specific to how Laravel's permission packages (Spatie Laravel-Permission is the de facto standard, referenced the same way `react/data-fetching-conventions.md` names TanStack Query by name) structure runtime vs seed-time mutation.

This doesn't belong in a project's own `AGENTS.md` because none of the three principles depend on that project's specific domain — they're reusable the same way `react/`'s general-knowledge files are, pending enrichment via `laravel/examples.md` once real implementation exists (same pattern documented for `react/` in `index.md`'s coverage note).

---

*After human review: update the Status above. If Accepted, merge into
the target document and leave this proposal in place (don't delete
it) — it serves as this folder's changelog. See `proposals/README.md`
for the Protection Tier distinction and numbering convention.*
