# loading-empty-error-state-conventions.md

**Location:** `react/loading-empty-error-state-conventions.md`

**Principle**
Every page/section that depends on async data has four states to account for — loading, empty, error, success — and skipping any one of them isn't a visual nitpick, it's a gap agent-generated code falls into by default (the happy path gets built, the other three get an afterthought or nothing). The state most likely to become an actual security issue: error state. Surfacing a raw backend error message, stack trace, or exception string to the user leaks implementation detail (framework version, internal paths, query fragments) to whoever's looking — this is the same "improper error messages" concern security testing already checks for on the backend, and it applies just as much to what the frontend chooses to render from a failed request. A second common gap: a page built from multiple independent data sources (a dashboard with several cards) treating any one source's failure as a full-page failure, when only that one section should degrade.

**Bad**
```tsx
function CampaignList() {
  const { data, isLoading, error } = useQuery(...);
  if (isLoading) return <Spinner />; // generic spinner, no sense of what's coming
  if (error) return <div>{error.message}</div>; // raw error text straight to the user
  if (data.length === 0) return null; // no empty state at all
  return <div>{data.map(c => <CampaignCard key={c.id} campaign={c} />)}</div>;
}
```
```tsx
function Dashboard() {
  const stats = useQuery(...);
  const donations = useQuery(...);
  if (stats.error || donations.error) return <FullPageError />;
  // one card's failure takes down cards that had nothing wrong with their own data
  ...
}
```

**Good**
```tsx
function CampaignList() {
  const { data, isLoading, isError } = useQuery(...);

  if (isLoading) {
    return <CampaignCardSkeleton count={6} />; // shaped like the real cards, not a bare spinner
  }
  if (isError) {
    return (
      <ErrorBanner
        message="Couldn't load campaigns — please try again." // generic, never error.message
        onRetry={() => queryClient.invalidateQueries({ queryKey: campaignKeys.list() })}
      />
    );
  }
  if (data.length === 0) {
    return (
      <EmptyState
        icon={<CampaignIcon />}
        message="No campaigns yet"
        action={canCreate ? <CreateCampaignButton /> : undefined} // only shown if actually authorized
      />
    );
  }
  return <div>{data.map(c => <CampaignCard key={c.id} campaign={c} />)}</div>;
}
```
```tsx
function Dashboard() {
  return (
    <div className="grid grid-cols-3 gap-4">
      <StatsCard /> {/* each card owns and isolates its own loading/error state */}
      <DonationsCard />
      <ReportsCard />
    </div>
  );
}
function StatsCard() {
  const { data, isLoading, isError } = useQuery(...);
  if (isLoading) return <CardSkeleton />;
  if (isError) return <CardError message="Couldn't load stats" />; // this card only — siblings unaffected
  return <CardContent data={data} />;
}
```

**Checklist**
- [ ] Every component consuming async data explicitly handles all four states (loading, empty, error, success) — none silently falls through to `null` or an unstyled default
- [ ] Loading state uses a skeleton shaped like the real content (matching count/layout), not a bare spinner — except inline button-level submit actions, where a small inline spinner is correct
- [ ] Error state renders a generic, user-facing message and a retry action — the raw error object, exception message, or any backend response body text is never interpolated directly into what's shown to the user
- [ ] A "not found" (specific resource genuinely doesn't exist) and a transient fetch error are distinguished with different messages — conflating them either confuses users on a temporary network blip or, worse, can leak existence information in flows where that matters (see enumeration-sensitive endpoints)
- [ ] Empty state shows a create/primary action only when the current viewer is actually authorized to take it — never a disabled or misleading CTA to someone without permission
- [ ] A page built from multiple independent data sources isolates failure per section — one query failing doesn't blank out sections whose own data loaded fine
- [ ] Stale-but-cached data shown while revalidating or offline is visually distinguished from confirmed-fresh data, especially for financial or status-sensitive values — this isn't the same as the Error state, it's a freshness caveat, not a failure