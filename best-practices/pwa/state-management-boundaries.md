# state-management-boundaries.md

**Location:** `pwa/state-management-boundaries.md`

**Principle**
Client-side state is best split by domain rather than kept in one monolithic global store — this makes it easier to reason about who can change what state, and limits the blast radius of a given change. More important than the split itself: state/cache invalidation after a mutation must be disciplined, especially after events that change session identity (token refresh, logout) — stale data from a previous session must not linger in another store and be rendered as if it were still valid.

**Bad**
```js
// one global store, and logout doesn't clear the others
function logout() {
  authStore.clear();
  // profileStore, campaignStore, etc. still hold the previous user's data
}
```

**Good**
```js
// state split by domain
const authStore = createStore(...);
const profileStore = createStore(...);
const campaignStore = createStore(...);

function logout() {
  authStore.clear();
  profileStore.reset();
  campaignStore.reset(); // explicitly cleared, not assumed "irrelevant"
  queryClient.clear(); // the data-fetching library's cache is invalidated too
}
```

**Checklist**
- [ ] State is split by domain, not one global store for every concern
- [ ] Events that change session identity (logout, token refresh, account switch) have an explicit list of which stores/caches must be reset
- [ ] No store is "forgotten" during logout because it was assumed unrelated to auth
- [ ] The data-fetching library's cache (not just manual state stores) is included in the invalidation cycle