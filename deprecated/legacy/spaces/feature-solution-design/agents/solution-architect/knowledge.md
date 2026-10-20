# Solution Architect — Agent-Owned Best Practices

This knowledge is scoped to **cross-boundary solution design**, not a universal technology or product authority.

## Contracts and ownership

- Define a single authoritative owner for each mutable state and action; avoid backend/frontend copies claiming independent authority.
- Make interface semantics explicit where downstream implementers could disagree: field meaning, error categories, idempotency/retry expectations, authorization/trust boundary, state transitions, persistence and compatibility rules.
- Derive API operation shapes from accepted outcomes and real consumers; avoid creating speculative endpoints and generic layers. If active project uses OpenAPI, clarify which artifact owns the source contract.
- Represent incomplete and conflicting outcomes distinctly from success. A frontend success screen cannot repair a backend partial-commit invariant.

## Integrity and security

- Authentication establishes identity/session according to chosen mechanism; it is not automatically resource-level or privileged authorization.
- For resource scope and role grants, require an enforceable trusted server-side relationship/policy where the selected architecture includes a backend. UI action visibility is not a security boundary.
- For multi-record semantic atomicity, distinguish product invariant from implementation strategy: design the required outcome first, then assess transaction/locking/idempotency options. Never assert atomicity from documentation alone.
- Treat external authority/provenance as a separate claim from an internal product role unless original requirements explicitly equate them.
- Project security approval boundaries govern sensitive implementation even if a solution is accepted.

## Decision economy

- Prefer one coherent solution with material rationale over catalogs of hypothetical architectures.
- Preserve specific unresolved decisions requiring Human judgment; leave safe, local stack implementation choices to downstream Specialists.
- Verify with actual current project instructions and applicable official technical sources when consequential; do not rely on another project's historically selected stack or one global Best Practices index.
