# server-vs-client-driven-rendering.md

**Location:** `hybrid-monolith/server-vs-client-driven-rendering.md`

**Principle**
In a server-rendered-bridge architecture (Inertia.js, Turbo/Hotwire, HTMX, and similar), most page data should arrive through the initial server-driven render (page props on a full page visit or a framework-native partial reload) — that's simpler, has no separate loading state to manage, and stays consistent with the rest of the page automatically. Client-side fetching should be reserved for interactions that genuinely can't wait for a page visit: search/autocomplete-as-you-type, a polling badge, anything that would feel wrong to trigger a full page reload for. The failure mode isn't picking one or the other — it's picking **both** for the *same* piece of data on the same page: a server-driven revisit refreshes it one way, a client-side query cache invalidates and refetches it another way, and now there are two sources of truth for one value that can disagree mid-session, especially right after a mutation. Pick one mechanism per data need and keep the boundary explicit — file/folder naming or a clear convention should make it obvious at a glance which pieces of a page are server-driven props and which are client-fetched.

**Bad**
```tsx
// Page component receives unread count as a server-driven prop...
export default function Dashboard({ unreadCount }: { unreadCount: number }) {
  // ...but ALSO polls it client-side on an interval, for the same value.
  const { data: liveUnreadCount } = useQuery({
    queryKey: ['unread-count'],
    queryFn: fetchUnreadCount,
    refetchInterval: 15000,
  });

  // Which one is "correct" right after the user reads a notification?
  // The server prop won't update until the next page visit; the client
  // query might overwrite it with a stale value it fetched moments before
  // the server-side state changed. Two sources of truth, no defined winner.
  return <Badge count={liveUnreadCount ?? unreadCount} />;
}
```

**Good**
```tsx
// Server-driven: page data delivered once via props, refreshed only on
// navigation/revisit — no client fetch for this at all.
export default function CampaignList({ campaigns }: { campaigns: Campaign[] }) {
  return <CampaignTable data={campaigns} />;
}

// Client-driven: genuinely needs to update without a page visit — polling
// is the ONLY mechanism for this value, no server-prop equivalent exists.
export function UnreadBadge() {
  const { data: unreadCount } = useQuery({
    queryKey: ['unread-count'],
    queryFn: fetchUnreadCount,
    refetchInterval: 15000,
  });
  return <Badge count={unreadCount ?? 0} />;
}

// Client-driven: search-as-you-type, no server-prop equivalent needed
export function CampaignSearch() {
  const [query, setQuery] = useState('');
  const { data: results } = useQuery({
    queryKey: ['campaign-search', query],
    queryFn: () => searchCampaigns(query),
    enabled: query.length > 2,
  });
  return <SearchResults results={results} onChange={setQuery} />;
}

// After a mutation that changes server-driven data, the reload goes through
// the server-driven mechanism (a page revisit / partial reload), NOT a
// client-side cache invalidation of the same data:
// router.reload({ only: ['campaigns'] }); // Inertia partial reload
```

**Checklist**
- [ ] For every piece of data on a page, there is exactly one delivery mechanism — server-driven props/partial reload, or a client-side fetch — never both for the same value
- [ ] Client-side fetching is reserved for interactions that genuinely can't wait for a page visit (search-as-you-type, polling, background refresh) — not used as a default for data that could just as well be a server prop
- [ ] After a mutation, the affected data refreshes through whichever mechanism owns it — a server-driven partial reload for server-driven data, a query invalidation for client-driven data — not through both, and not through the wrong one
- [ ] A naming/folder convention makes it visible at a glance which parts of a page are server-driven vs client-fetched (e.g. co-locating client-fetch hooks in a distinctly named folder, not scattering ad-hoc `useQuery` calls next to prop-driven components)
- [ ] Adding a new interactive widget to an existing server-driven page is a deliberate decision point — reviewed for whether it should be a client fetch or whether the page's server-driven props should just include the new data instead
