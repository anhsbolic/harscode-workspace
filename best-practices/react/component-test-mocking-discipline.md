# component-test-mocking-discipline.md

**Location:** `react/component-test-mocking-discipline.md`

**Principle**
A component test's value comes from how close it stays to what actually runs in production. Network-layer mocking (MSW or equivalent, intercepting at the `fetch`/HTTP level) is preferable to mocking the data-fetching hook or client directly, because the component still exercises its real fetch call, real query library, and real error/loading state transitions — only the network response is substituted. The failure mode to watch for is over-mocking: stubbing out so much (the fetching hook itself, the whole child tree, context providers reduced to trivial pass-throughs) that the test can no longer fail even when the component is broken. A second common failure: tests written against implementation detail (component internal state, class names, DOM structure) instead of user-observable behavior (role, text, accessible name) — these break on harmless refactors and don't verify anything a real user would experience.

**Bad**
```tsx
// mocking the hook directly — the test never exercises the real fetch/query logic,
// so it can't catch a broken query key, a wrong endpoint, or a serialization bug
vi.mock('@/lib/hooks/useCampaign', () => ({
  useCampaign: () => ({ data: mockCampaign, isLoading: false }),
}));

test('renders campaign title', () => {
  render(<CampaignDetail id="1" />);
  expect(screen.getByText(mockCampaign.title)).toBeInTheDocument();
});
```
```tsx
// asserting on implementation detail instead of observable behavior
expect(wrapper.find('.campaign-title').text()).toBe('...');
expect(component.state.isOpen).toBe(true);
```

**Good**
```tsx
// MSW intercepts at the network layer — component runs its real fetch/query path
const server = setupServer(
  http.get('/api/campaigns/:id', () => HttpResponse.json(mockCampaign)),
);

test('renders campaign title after loading', async () => {
  render(<CampaignDetail id="1" />);
  expect(screen.getByRole('status', { name: /loading/i })).toBeInTheDocument(); // loading state exercised too
  expect(await screen.findByRole('heading', { name: mockCampaign.title })).toBeInTheDocument();
});

test('shows retry banner on server error', async () => {
  server.use(http.get('/api/campaigns/:id', () => HttpResponse.error()));
  render(<CampaignDetail id="1" />);
  expect(await screen.findByRole('alert')).toHaveTextContent(/couldn't load/i);
  expect(screen.getByRole('button', { name: /retry/i })).toBeInTheDocument();
});
```

**Checklist**
- [ ] API calls are mocked at the network layer (MSW) using the same OpenAPI-generated response shape the app actually receives — not a hand-rolled mock object that can silently drift from the real contract
- [ ] Queries/hooks are not mocked directly except where the network-layer mock genuinely can't reach the case being tested (e.g. a client-only derived-state bug) — this should be the exception, not the default
- [ ] Assertions query by role/label/text (`getByRole`, `getByLabelText`) — not by class name, test-id-as-a-crutch for everything, or component internal state
- [ ] Loading and error states are covered by dedicated test cases, not just the success path — these are exactly the states most likely to be wrong in agent-generated code and least likely to be caught by a quick manual click-through
- [ ] Any component rendering user-controlled Markdown/HTML has a test asserting a script/event-handler payload is stripped, not just that normal content renders — this is a security-relevant test, not just a coverage checkbox
