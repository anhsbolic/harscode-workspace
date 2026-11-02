# State Ownership, Data Fetching, and Client Cache

> **Applicable when:** frontend state has multiple consumers, async data, forms, filters, session/tenant identity, cache invalidation, optimistic updates or navigation. Do not assume a particular state library; follow the project stack.

## Decide ownership before choosing a store

Ask:
1. Is this value a deterministic projection of existing truth? If so, derive it rather than create another synchronized owner.
2. Is it server/API-authoritative? Keep authority with the permitted server data layer or query cache and explicitly understand freshness.
3. Must the value be shareable/bookmarkable/back-button aware, and is it nonsensitive? Consider URL state.
4. Is it form-lifecycle data? Keep it with the project form mechanism.
5. Is it ephemeral UI interaction (open panel, current tab) with a natural component owner? Prefer local state.
6. Is genuinely client-owned state shared beyond a natural component boundary? Then use an appropriate shared owner—not by default.

Do not copy server-fetched resources into a global store “for convenience” and then attempt to synchronize two independent truths. A larger app does not automatically justify a general store.

## Query ownership and invalidation

When query caching is used, choose stable identity-aware keys and a consistent invalidation/update strategy for mutations. Include account/resource/filters only where semantically required and avoid storing secrets in key/log output. A mutation changing list and detail views must not leave one stale until an unrelated refresh. Avoid unnecessary data-fetch waterfalls when independent requests are known early; do not parallelize requests that really depend on a prior trusted result.

Optimistic UI is a presentation technique, not confirmation of a backend effect. Use it only for actions whose risk and accepted result semantics permit rollback/reconciliation. For consequential operations, sending the request, getting an ambiguous timeout, receiving 202 Accepted or showing a spinner is **not** equivalent to complete success. Provide truthful unknown/pending states and a contract-supported inspection/recovery path.

## Identity, private state and lifecycle

On logout, session expiration, account/tenant switch or material change of effective permission, re-evaluate and clear/scope private state and in-flight responses. Late arrival from the prior identity must not hydrate the new identity's view. Verify identity scoping at the point of displayed truth and data fetching, not merely with hidden controls. Persist only allowed data, for allowed lifetime, with suitable protection; never make browser storage a substitute for session authority.

## Observable failure cases

Prefer tests or inspection, as allowed by project SOP, that distinguish fresh vs stale response, account A vs B, rejected vs lost mutation result, form state vs server state, and rollback vs committed effect. Record which were actually exercised. Don't turn a new state manager or cache abstraction into a prerequisite unless present failure warrants it.
