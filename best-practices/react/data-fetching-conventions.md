# data-fetching-conventions.md

**Location:** `react/data-fetching-conventions.md`

**Principle**
A server-state library (TanStack Query or equivalent) is only as reliable as its query-key discipline and invalidation strategy. Two failures show up repeatedly in agent-generated code: query keys built ad hoc per call site (so the same logical data ends up cached under multiple different keys, and a mutation that should invalidate it misses some of them), and mutations that don't invalidate/update the affected queries at all — leaving stale data on screen until an unrelated refetch happens to occur. A related but distinct failure is request waterfalls: sequential `useQuery` calls where the second depends on data the first already has, issued one-after-another inside a component tree instead of being fetched in parallel or co-located in one call.

**Bad**
```ts
// query key built inline, slightly different at each call site
useQuery({ queryKey: ['campaign', id], queryFn: () => getCampaign(id) });
useQuery({ queryKey: ['campaigns', id, 'detail'], queryFn: () => getCampaign(id) }); // same data, different key — cached twice, invalidation misses one
```
```ts
// mutation with no invalidation — UI silently shows stale data after a successful edit
const mutation = useMutation({ mutationFn: updateCampaign });
// caller just calls mutation.mutate(payload) and moves on
```
```tsx
// waterfall: second query doesn't start until the first resolves, purely from
// component nesting, when both could be requested together
function CampaignPage({ id }) {
  const { data: campaign } = useQuery(['campaign', id], () => getCampaign(id));
  return campaign ? <Donors campaignId={campaign.id} /> : null;
}
function Donors({ campaignId }) {
  const { data: donors } = useQuery(['donors', campaignId], () => getDonors(campaignId));
  // this could have started at the same time as the campaign fetch — campaignId
  // is already known from the route param, not something only the first query reveals
}
```

**Good**
```ts
// centralized key factory — one definition, reused everywhere, keys are structurally consistent
export const campaignKeys = {
  detail: (id: string) => ['campaigns', id] as const,
  list: (filters: CampaignFilters) => ['campaigns', 'list', filters] as const,
};

useQuery({ queryKey: campaignKeys.detail(id), queryFn: () => getCampaign(id) });
```
```ts
const mutation = useMutation({
  mutationFn: updateCampaign,
  onSuccess: (updated) => {
    queryClient.invalidateQueries({ queryKey: campaignKeys.detail(updated.id) });
    queryClient.invalidateQueries({ queryKey: campaignKeys.list }); // list view also affected
  },
});
```
```tsx
function CampaignPage({ id }) {
  const { data: campaign } = useQuery({ queryKey: campaignKeys.detail(id), queryFn: () => getCampaign(id) });
  const { data: donors } = useQuery({ queryKey: donorKeys.byCampaign(id), queryFn: () => getDonors(id) });
  // both fire in parallel — id is known up front, neither query depends on the other's result
  ...
}
```

**Checklist**
- [ ] Query keys come from a single shared factory per resource type, not built inline at each call site — the same logical data is never cached under two structurally different keys
- [ ] Every mutation that changes server state either invalidates the affected query keys or applies an explicit optimistic/direct cache update (`setQueryData`) — never left to an incidental future refetch
- [ ] Two queries are only sequenced (one depending on the other's result) when the second genuinely needs data only the first response provides — not because of component nesting alone
- [ ] Optimistic updates roll back on error (`onError` restores the previous cache snapshot) — an optimistic update with no rollback path leaves the UI confidently wrong after a failed mutation
- [ ] Stale/cached data shown while revalidating (or while offline) is visually distinguishable from confirmed-fresh data wherever the value is financial, status-sensitive, or otherwise consequential if acted on while stale
