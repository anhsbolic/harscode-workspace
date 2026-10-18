# React State Ownership and Derivation

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** React/Next.js state across local interaction, forms, URLs and server-owned data.
> **Triggers:** useState, useEffect, derived state, server data, cache, form, pending mutation, role display, Zustand.

## 01 — Applicability

Use when deciding whether a value should be stored, derived, fetched or shared. Particularly important for consequential submit flows, delayed server responses and durable server-authoritative identity/role information.

## 02 — Principle / Rule

- Do not duplicate independently stored state that can be derived deterministically from authoritative inputs during rendering.
- Place genuine state according to **authority and lifetime**: short-lived interaction locally; form edits with form state; navigation/shareable non-sensitive state in URL when appropriate; server-owned data in an authoritative fetch/cache; global client stores only for genuinely shared client state.
- A server-successful mutation is not established merely because a button was pressed or an optimistic UI changed. Derive durable success from an actual authoritative response/state.
- Treat pending, failed, uncertain and completed transitions distinctly when their product meaning differs; avoid contradictory booleans and duplicated copies of current server state.
- Never put tokens, personal secrets or privileged authorization decisions into client state as if storage or visibility were security authority.

## 03 — Rationale & Risk

Mirrored props or duplicated query/global state become stale. Premature local success UI can claim a durable server consequence that did not commit. Over-globalization creates synchronization and privacy costs.

## 04 — Application Guidance

1. Ask who owns the truth, how long it must live, who consumes it and whether it can be derived.
2. Compute derived display values from source state, e.g. `const fullName = first + " " + last`, instead of synchronizing extra `useState`.
3. Store form drafts separately from accepted server data; after mutation invalidate/refetch or apply contract-valid cache updates as needed.
4. If optimistic updates are appropriate, distinguish provisional UI from confirmed outcome, implement rollback and handle request-unknown states honestly.
5. Keep a single source for identity/resource role state; server-side authorization remains independently enforced.

## 05 — Verification

Test editing, success, validation failure, network loss, duplicate submit, navigation/reload and stale-cache refresh where relevant. Verify a transient success message is not the sole durable evidence of server-owned state. Run browser-level checks where displayed trust/status meaning matters.

## 06 — Boundaries & Trade-offs

This is not a ban on local copies of editable form data, nor a mandate to use any state library. Avoid needless request storms caused by aggressive invalidation. State architecture should follow actual client/server contract and project rendering model.

## References

- https://react.dev/learn/choosing-the-state-structure
- https://react.dev/learn/sharing-state-between-components
