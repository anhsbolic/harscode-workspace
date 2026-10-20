# offline-and-sync.md

**Location:** `pwa/offline-and-sync.md`

**Principle**
If a PWA supports offline data storage (e.g. form drafts), there must be a clear line between what's safe to store offline (non-sensitive drafts that can be lost with no security consequence) versus what must never be stored in client storage under any circumstance (anything related to authentication credentials or payment data). A sync-on-reconnect strategy must handle conflicts explicitly (server data changed while offline), not just assume "last write wins" without consideration.

**Bad**
```js
// storing a draft including payment data in IndexedDB with no distinction
await db.drafts.put({ id, formData: entireForm }); // entireForm includes card/credential fields
```

**Good**
```js
const OFFLINE_SAFE_FIELDS = ['title', 'description', 'category']; // explicit whitelist

async function saveDraftOffline(id, formData) {
  const safeData = pick(formData, OFFLINE_SAFE_FIELDS); // sensitive fields never included
  await db.drafts.put({ id, formData: safeData, savedAt: Date.now() });
}

async function syncOnReconnect(draft) {
  const serverVersion = await fetchLatestVersion(draft.id);
  if (serverVersion.updatedAt > draft.savedAt) {
    return promptUserToResolveConflict(draft, serverVersion); // conflict handled explicitly
  }
  return pushDraft(draft);
}
```

**Checklist**
- [ ] There is an explicit whitelist of fields allowed to be stored offline, not the entire form state
- [ ] Credential/payment-related data is never stored offline in any form
- [ ] Sync-on-reconnect handles possible conflicts, not an unexamined last-write-wins assumption
- [ ] There is a time limit/cleanup for offline drafts that are never synced (they don't accumulate indefinitely)