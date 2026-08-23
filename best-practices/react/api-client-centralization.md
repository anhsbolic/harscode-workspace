# api-client-centralization.md

**Location:** `react/api-client-centralization.md`

**Principle**
Every state-changing request needs the same handful of things attached correctly: the in-memory access token, the CSRF/custom header the backend expects on state-changing endpoints, and `credentials: 'include'` for the auth cookie to travel. If each component calls `fetch` directly, these requirements get re-implemented at every call site — and it only takes one page missing one header to silently break CSRF protection or auth for that one flow, in a way that's easy to miss in review because the fetch call "looks normal." A single, centralized client is what makes `restapi/csrf-and-cookie-security.md` and `pwa/token-storage-and-refresh.md`'s guarantees actually hold everywhere, instead of being true only where someone remembered to apply them.

**Bad**
```ts
// components/DonationForm.tsx
async function submitDonation(payload: DonationPayload) {
  const res = await fetch('/api/donations', {
    method: 'POST',
    body: JSON.stringify(payload),
    // no Authorization header, no CSRF header, no credentials — this one call
    // silently drops all three unless someone remembers to add them here too
  });
  return res.json();
}
```
```ts
// components/CampaignEdit.tsx — a different page, adds credentials but forgets the CSRF header
async function updateCampaign(id: string, payload: CampaignPayload) {
  const res = await fetch(`/api/campaigns/${id}`, {
    method: 'PATCH',
    body: JSON.stringify(payload),
    credentials: 'include', // present here, but the header below still isn't
  });
  return res.json();
}
```

**Good**
```ts
// lib/api/client.ts — single point every request goes through
async function apiFetch(path: string, init: RequestInit = {}) {
  const token = getAccessToken(); // in-memory, per token-storage-and-refresh.md
  const isMutating = init.method && init.method !== 'GET';

  const res = await fetch(path, {
    ...init,
    credentials: 'include', // auth cookie travels on every request, always
    headers: {
      ...init.headers,
      ...(token ? { Authorization: `Bearer ${token}` } : {}),
      ...(isMutating ? { 'X-Requested-With': 'kencleng-frontend' } : {}), // CSRF header, only where required
    },
  });

  if (res.status === 401) {
    await tryRefreshOnce(); // one retry after a silent refresh, not a retry loop
  }
  return res;
}

// every fetch function in lib/api/ goes through apiFetch, never a raw fetch() call
export const submitDonation = (payload: DonationPayload) =>
  apiFetch('/api/donations', { method: 'POST', body: JSON.stringify(payload) });
```

**Checklist**
- [ ] There is exactly one low-level request function (`apiFetch` or equivalent) that attaches the auth token, the CSRF/custom header, and `credentials: 'include'` — every typed fetch function in `lib/api/` calls through it, none call `fetch` directly
- [ ] The CSRF/custom header is attached based on HTTP method (state-changing verbs), not hardcoded per endpoint — so a newly added mutation gets it automatically, not by remembering to copy it
- [ ] A 401 response triggers exactly one silent-refresh retry, not an unbounded retry loop and not silence (a failed refresh should surface as a logged-out state, not a hung request)
- [ ] No component or hook constructs its own `fetch` call for anything hitting the app's own backend — direct `fetch` usage outside the centralized client is treated as a review flag, not a style nitpick
- [ ] Response error shapes (422 vs 5xx vs network failure) are normalized once in the centralized client, so every caller handles the same shape instead of each component parsing errors differently