# server-client-component-boundary.md

**Location:** `react/server-client-component-boundary.md`

**Principle**
In a framework with React Server Components (Next.js App Router and equivalents), the Server/Client boundary isn't just a performance knob — it's a trust boundary. Code in a Server Component runs only on the server and can safely read secrets/env vars and call internal services directly; code in a Client Component (`'use client'`) ships to the browser as-is, so anything referenced there — including values merely *imported* from a server-only module, not just ones visibly used — can end up bundled and exposed. The second common failure is the opposite direction: fetching or computing something in a Server Component using request-specific identity (the current user's session) without accounting for the framework's caching behavior, so one user's data is served to another from a shared cache.

**Bad**
```tsx
// lib/config.ts — meant to be server-only
export const INTERNAL_API_KEY = process.env.INTERNAL_API_KEY;
export const PUBLIC_FEATURE_FLAG = true;

// components/Banner.tsx
'use client';
import { INTERNAL_API_KEY, PUBLIC_FEATURE_FLAG } from '@/lib/config';
// importing from this module at all risks bundling INTERNAL_API_KEY into
// client JS, even if only PUBLIC_FEATURE_FLAG is actually used here —
// bundlers don't reliably tree-shake based on usage inside a 'use client' file
```
```tsx
// app/dashboard/page.tsx — Server Component
export default async function DashboardPage() {
  const data = await fetch('https://api.internal/me', { /* no cache option set */ });
  // default fetch caching behavior varies by framework version/config;
  // a request-scoped, per-user response cached and reused for the next
  // request is a cross-user data leak, not just a staleness bug
  return <Dashboard data={data} />;
}
```

**Good**
```tsx
// lib/config.server.ts — naming signals server-only, never imported from a 'use client' file
export const INTERNAL_API_KEY = process.env.INTERNAL_API_KEY;

// lib/config.public.ts — explicitly the only thing safe to import client-side
export const PUBLIC_FEATURE_FLAG = true;
```
```tsx
// app/dashboard/page.tsx — Server Component, explicit no-store for per-user data
export default async function DashboardPage() {
  const data = await fetch('https://api.internal/me', { cache: 'no-store' });
  return <Dashboard data={data} />;
}
```

**Checklist**
- [ ] Server-only modules (secrets, internal service clients, DB access) live in files clearly named/scoped as server-only, and are never imported — directly or transitively — from a file marked `'use client'`
- [ ] A framework-level guard (e.g. a `server-only` import marker package) is used where available, so an accidental client import fails the build instead of silently shipping
- [ ] Every server-side fetch/data-read that depends on the current request's identity (session, auth header, cookie) has an explicit caching directive — never left on a framework default without checking what that default actually does
- [ ] `'use client'` is added at the leaf/smallest component that actually needs interactivity, not hoisted to a whole page — keeps the server-only surface as large as possible by default, rather than accidentally client-ifying everything beneath one interactive element
- [ ] Environment variables intended for the browser use the framework's explicit public-prefix convention (e.g. `NEXT_PUBLIC_*`) — anything without that prefix is assumed server-only and never referenced from client code
