# state-management-boundaries.md

Location: `pwa/state-management-boundaries.md`

Principle When shared client-owned state is required, split it by domain rather than keeping one monolithic global store — this makes it easier to reason about who can change what and limits the blast radius of a change. Do not use client stores as mirrors of server-authoritative data; that data stays with its existing data-fetching owner. More important than the split itself: stores and caches that can contain identity-scoped data must be invalidated explicitly when session identity changes — stale data from a previous session must not be rendered as if it were still valid.

Bad

```
// one global store, and logout does not clear identity-scoped state
function logout() {
  authStore.clear();
  // client-owned stores and query cache still contain previous-session data
}
```

Good

```
// genuinely client-owned shared state split by domain
const authStore = createStore(...);
const editorDraftStore = createStore(...);
const accountUiStore = createStore(...);

function logout() {
  authStore.clear();
  editorDraftStore.reset();
  accountUiStore.reset();
  queryClient.clear(); // server-authoritative cached data is cleared at its owner
}
```

Checklist

* [ ] Shared client-owned state is split by domain; server-authoritative data is not duplicated into those stores
* [ ] Events that change session identity (logout, token refresh, account switch) have an explicit list of which stores/caches must be reset
* [ ] No store is "forgotten" during logout because it was assumed unrelated to auth
* [ ] The data-fetching layer's cache, not just manual client stores, is included in the invalidation cycle
