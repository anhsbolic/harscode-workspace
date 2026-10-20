# service-worker-caching.md

**Location:** `pwa/service-worker-caching.md`

**Principle**
Service worker cache strategy should differ by resource type: stale-while-revalidate suits static assets (fine to be slightly stale for speed), network-first suits data that must always be fresh. The most important thing to avoid: API responses containing auth-sensitive data (user profile, balance, personal data) must never be cached by the service worker by accident through an overly general cache-matching pattern (e.g. caching all GET requests).

**Bad**
```js
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((cached) => cached || fetch(event.request))
  ); // every GET request is cached without exception, including auth-sensitive endpoints
});
```

**Good**
```js
const STATIC_CACHE = 'static-v1';
const isStaticAsset = (url) => /\.(js|css|png|svg|woff2)$/.test(url.pathname);
const isSensitiveAPI = (url) => url.pathname.startsWith('/api/auth') || url.pathname.startsWith('/api/profile');

self.addEventListener('fetch', (event) => {
  const url = new URL(event.request.url);
  if (isSensitiveAPI(url)) {
    return; // not intercepted at all, always goes to network
  }
  if (isStaticAsset(url)) {
    event.respondWith(staleWhileRevalidate(event.request, STATIC_CACHE));
  } else {
    event.respondWith(networkFirst(event.request));
  }
});
```

**Checklist**
- [ ] Auth-sensitive endpoints (profile, balance, personal data) are explicitly excluded from service worker caching
- [ ] Static assets use stale-while-revalidate; data that must stay fresh uses network-first
- [ ] There is no "cache all GET requests" pattern without exceptions
- [ ] Old cache versions are cleared when the service worker updates (cache invalidation on deploy)