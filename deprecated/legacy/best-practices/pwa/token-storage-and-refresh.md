# token-storage-and-refresh.md

**Location:** `pwa/token-storage-and-refresh.md`

**Principle**
For a SPA/PWA with a token-based backend, storing the access token in memory (not `localStorage`/`sessionStorage`) and the refresh token in an `HttpOnly` cookie is the right trade-off for XSS resilience — an in-memory access token can't be stolen by an injected script reading browser storage. The consequence: token state is lost on page reload, so a silent-refresh-on-mount is needed (calling the refresh endpoint as soon as the app loads, using the still-present cookie, to obtain a new access token without forcing the user to log in again). For multi-tab scenarios, use `BroadcastChannel` (or equivalent) so a logout/refresh event in one tab is synced to other tabs, preventing stale token state in inactive tabs.

**Bad**
```js
localStorage.setItem('accessToken', token); // readable by any script injection
```

**Good**
```js
// access token lives in memory (app state), not browser storage
let accessToken = null;

async function onAppMount() {
  const res = await fetch('/auth/refresh', { credentials: 'include' }); // uses the HttpOnly cookie
  if (res.ok) {
    const { token } = await res.json();
    accessToken = token;
  }
}

const channel = new BroadcastChannel('auth');
channel.onmessage = (event) => {
  if (event.data.type === 'logout') accessToken = null; // synced across tabs
};
```

**Checklist**
- [ ] The access token is stored in application memory, not `localStorage`/`sessionStorage`
- [ ] The refresh token is stored in an `HttpOnly` cookie (see also `restapi/csrf-and-cookie-security.md`)
- [ ] There is a silent-refresh-on-mount so page reloads don't force a re-login
- [ ] Auth events (login/logout/refresh) are synced across tabs, not only effective in the tab that triggered them