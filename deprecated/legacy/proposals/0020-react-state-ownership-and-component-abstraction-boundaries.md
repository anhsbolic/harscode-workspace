# 0020 — React state ownership and component abstraction boundaries

Status: Accepted  
Date: 2026-09-07  
Protection Tier: general  
Triggered by: Frontend best-practices gap audit while preparing Harscode for agent-driven React development. Existing guidance already covers server-state fetching, form validation, PWA store cleanup, and prototype translation, but does not define the earlier decision points of whether a value needs state ownership at all, where that state should live, or when repeated UI should become a shared abstraction. The audit also exposed ambiguous wording in existing PWA/prototype guidance that could encourage copying server-owned data into client stores or treating prototype decomposition as an approved production boundary.  
Target area: best-practices  
Target file(s):

- New: `best-practices/react/state-ownership-and-derivation.md`
- New: `best-practices/react/component-composition-and-abstraction.md`
- `best-practices/pwa/state-management-boundaries.md` — clarify that it governs genuinely client-owned shared state and identity-scoped cleanup, not mirrors of server-authoritative data
- `best-practices/react/ai-prototype-to-production-translation.md` — clarify that prototype component decomposition is evidence, not an automatically approved production component boundary; translate scratch state according to ownership semantics
- `best-practices/index.md` — add two React routing rows

## Gap found

### 1. React guidance starts after the state-ownership decision

`react/data-fetching-conventions.md` correctly governs query keys, invalidation, waterfalls, optimistic updates, and other server-state mechanics once a data-fetching owner has already been selected.

`react/form-validation-boundary.md` governs validation authority once a form exists.

`pwa/state-management-boundaries.md` governs domain separation and identity-change cleanup once shared client stores already exist.

What is missing is the decision layer before all three:

- Does this value need independent state at all?
- Is it a deterministic projection that should simply be derived?
- Is it server-owned, URL-owned, form-owned, local UI state, or genuinely shared client-owned state?
- Is a global store solving an actual lifetime/sharing requirement, or just making access convenient?

Without this layer, agent-generated React code can create duplicate sources of truth through `useState` plus synchronization effects or by copying server data into global stores.

### 2. No React-general abstraction boundary exists

The workspace has backend abstraction guidance, but no equivalent React guidance for distinguishing:

- extracting a meaningful component from merely shortening a file;
- stable shared semantics from superficial JSX duplication;
- genuine binary props from structural mode flags;
- useful wrappers from pass-through indirection;
- feature-local composition from prematurely promoted global/shared components.

This is particularly relevant to coding agents because repeated markup is easy to mechanically generalize before its semantic variation is understood.

A rigid rule-of-three would be too mechanical. Repetition should instead be treated as evidence worth evaluating. One occurrence can still justify extraction when it represents a meaningful independent responsibility.

### 3. Existing guidance has two wording ambiguities

`pwa/state-management-boundaries.md` currently demonstrates `profileStore` and `campaignStore` alongside `queryClient`, which can be interpreted as endorsing server-data mirroring into global stores.

`react/ai-prototype-to-production-translation.md` currently says prototype component decomposition is a reasonable shape to "mirror", and its local-state checklist reduces translation to "server state via query library, client state via the real store, forms via the real validation library." That wording is too coarse once state ownership is made explicit: much client state should remain local or be derived and needs no global store at all.

## Proposed change

### New: `react/state-ownership-and-derivation.md`

```md
# state-ownership-and-derivation.md

Location: `react/state-ownership-and-derivation.md`

Principle Before introducing state, determine whether the value needs independent ownership at all. A value that is a deterministic projection of existing state should be derived, not stored and synchronized as another source of truth.

When independent ownership is required, place state according to its authority, lifetime, and sharing semantics, using the narrowest owner that satisfies those requirements. Server-authoritative data stays with the data-fetching owner already responsible for it — server render/loader, query cache, or equivalent — rather than being copied into client state for convenience. Navigation state that should survive reload/share/back-forward belongs in the URL; form-lifecycle values belong with the form; ephemeral interaction belongs locally. Shared client state is appropriate only when genuinely client-owned state must span or outlive its natural component boundary.

Bad

    function CampaignPage({ id }) {
      const { data: campaign } = useCampaign(id);
      const setCampaign = useCampaignStore((s) => s.setCampaign);
      const [canDonate, setCanDonate] = useState(false);

      useEffect(() => {
        if (campaign) setCampaign(campaign); // duplicates server-owned data
      }, [campaign, setCampaign]);

      useEffect(() => {
        setCanDonate(
          Boolean(campaign?.status === 'ACTIVE' && campaign.remaining > 0)
        );
      }, [campaign]); // deterministic projection stored as another state
    }

Good

    function CampaignPage({ id }) {
      const { data: campaign } = useCampaign(id);

      // campaign remains owned by its data-fetching layer;
      // canDonate has no independent owner
      const canDonate =
        campaign?.status === 'ACTIVE' && campaign.remaining > 0;

      ...
    }

Ownership decision order

1. Can the value be derived reliably from state that already exists? If yes, derive it instead of introducing another owner.
2. Is an external/server data source authoritative? Keep the value with the existing data-fetching owner rather than mirroring it into client state.
3. Must the value survive reload, be linkable/shareable, or participate in back/forward navigation? Consider URL state.
4. Does the value exist for the lifecycle of a form? Keep it with the form.
5. Is it ephemeral interaction state whose consumers share a natural component owner? Keep it local or lift it only to that owner.
6. Use shared client state only when the value is genuinely client-owned and its required lifetime or consumers exceed a natural local boundary.

Checklist

- [ ] No deterministic value is stored solely so an effect can synchronize it with another value
- [ ] Server/external authoritative data is not mirrored into global client state merely for convenient access
- [ ] Reload/share/back-forward semantics are considered before navigation-relevant state is kept only in memory
- [ ] Form-lifecycle state stays with the form unless another lifetime is explicitly required
- [ ] Ephemeral UI state starts at the narrowest meaningful owner rather than defaulting to context/global state
- [ ] Shared client state has a concrete lifetime or cross-tree requirement that local ownership cannot satisfy
```

### New: `react/component-composition-and-abstraction.md`

```md
# component-composition-and-abstraction.md

Location: `react/component-composition-and-abstraction.md`

Principle Extract components around meaningful UI or behavioral responsibilities, not line count. Abstract multiple implementations only when they demonstrate stable shared semantics; repeated code is evidence worth evaluating, not proof that a shared abstraction is required.

Prefer explicit composition and stable named variants over generic components whose behavior is controlled by a growing configuration surface. A small amount of feature-local duplication is cheaper than an abstraction that hides meaning, couples unrelated features, or accumulates structural mode flags.

Bad

    <DonationForm
      compact
      embedded
      admin
      hideHeader
      showCampaign
      allowAnonymous
    />

    function CampaignButton(props) {
      return <Button {...props} />; // no added semantics or contract
    }

Good

    <DonationForm>
      <DonationAmount />
      <DonorIdentity />
      <DonationSubmit />
    </DonationForm>

    <AdminDonationPanel>
      <DonationForm />
    </AdminDonationPanel>

When a structurally different variant becomes stable and meaningful, give it an explicit entry point rather than continually adding mode flags.

One occurrence can justify extraction when it represents a meaningful independent concept or behavior. Multiple occurrences justify evaluating whether shared semantics exist, but repetition alone does not justify generalization.

Decision order

1. Does extraction create a meaningful responsibility, interaction boundary, or independently understandable UI concept?
2. If implementations repeat, is the similarity semantic/behavioral or merely visual/structural coincidence?
3. Are the shared variation axes stable and understood?
4. Can children, slots, or explicit variants express the differences more clearly than configuration flags?
5. Does the abstraction reduce complexity for callers without hiding important behavior?
6. Is the abstraction genuinely cross-feature, or should feature-specific composition remain close to its feature?

Checklist

- [ ] Components are extracted for meaningful responsibility rather than file length alone
- [ ] Repetition triggers evaluation of shared semantics; no mechanical rule-of-three decides architecture
- [ ] Genuine binary state props (`disabled`, `required`, `open`) are distinguished from flags selecting structural/behavioral modes
- [ ] Growing structural-mode flags trigger reconsideration of composition or explicit variants
- [ ] Pass-through wrappers add semantics, behavior, constraints, defaults, or an intentional stable project API
- [ ] Feature-specific composition remains feature-local until cross-feature semantics are demonstrated
- [ ] Compound-component/context patterns are introduced only when simpler composition no longer expresses the contract clearly
- [ ] Component boundaries are not distorted merely to expose implementation details to tests
```

### `pwa/state-management-boundaries.md`

Replace the opening Principle:

```md
Principle Client-side state is best split by domain rather than kept in one monolithic global store — this makes it easier to reason about who can change what state, and limits the blast radius of a given change. More important than the split itself: state/cache invalidation after a mutation must be disciplined, especially after events that change session identity (token refresh, logout) — stale data from a previous session must not linger in another store and be rendered as if it were still valid.
```

with:

```md
Principle When shared client-owned state is required, split it by domain rather than keeping one monolithic global store — this makes it easier to reason about who can change what and limits the blast radius of a change. Do not use client stores as mirrors of server-authoritative data; that data stays with its existing data-fetching owner. More important than the split itself: stores and caches that can contain identity-scoped data must be invalidated explicitly when session identity changes — stale data from a previous session must not be rendered as if it were still valid.
```

Replace the Good example with:

```md
Good

    // genuinely client-owned shared state split by domain
    const authStore = createStore(...);
    const campaignDraftStore = createStore(...);
    const accountUiStore = createStore(...);

    function logout() {
      authStore.clear();
      campaignDraftStore.reset();
      accountUiStore.reset();
      queryClient.clear(); // externally authoritative cached data is cleared at its owner
    }
```

Replace the first checklist item:

```md
- [ ] State is split by domain, not one global store for every concern
```

with:

```md
- [ ] Shared client-owned state is split by domain; server-authoritative data is not duplicated into those stores
```

The remaining identity-change/reset checklist items remain unchanged.

### `react/ai-prototype-to-production-translation.md`

Replace:

```md
- [ ] Component decomposition and composition (how the reference splits a page into sub-components) is a reasonable starting shape to mirror
```

with:

```md
- [ ] Component decomposition and composition in the reference is useful evidence for the intended page structure, but remains a candidate starting shape — production boundaries are re-evaluated against meaningful responsibilities and the real application's existing component conventions
```

Replace:

```md
- [ ] Local component state (`useState` scattered through the export) is replaced with the real app's actual state-management conventions (server state via a query library, client state via the real store, forms via the real validation library) — not preserved as-is because it "already works"
```

with:

```md
- [ ] Scratch state in the export is translated according to the real application's ownership model — derive deterministic values; keep externally authoritative data with its real data-fetching owner; keep form state with the real form convention; keep ephemeral interaction local; introduce shared client state only when its lifetime or consumers require it
```

### `best-practices/index.md`

Add:

```md
react | [react/state-ownership-and-derivation.md](react/state-ownership-and-derivation.md) | state ownership, derived state, duplicate state, state synchronization, useEffect synchronization, global state, global store, zustand, url state, local state | no | Place state by authority and lifetime; deterministic projections have no independent owner; do not mirror externally authoritative data into client state

react | [react/component-composition-and-abstraction.md](react/component-composition-and-abstraction.md) | component abstraction, component composition, reusable component, shared component, extract component, boolean props, prop explosion, compound component, generic component, wrapper component | no | Extract meaningful responsibilities; repetition is evidence to evaluate rather than proof to abstract; prefer composition and stable variants over configuration-heavy generic components
```

Place `state-ownership-and-derivation.md` before `data-fetching-conventions.md`, and `component-composition-and-abstraction.md` before `component-test-mocking-discipline.md`.

## Rationale

The proposed guidance is React-general rather than project-specific:

- every React application must decide whether data is derived or independently owned;
- server, URL, form, local, and shared-client lifetimes exist independently of any one state-management library;
- component extraction and abstraction boundaries are architecture concerns independent of a particular design system or application domain;
- the proposal deliberately avoids prescribing TanStack Query, Zustand, React Hook Form, Tailwind, or any Kencleng-specific structure as mandatory tools;
- the compatibility edits remove ambiguity from existing generic guidance rather than introducing project policy.

The weak abstraction heuristic is intentional: repetition should cause an agent to evaluate whether shared semantics exist, but no usage-count threshold substitutes for semantic judgment.

---

After human review: update the Status above. If Accepted, merge into the target documents and leave this proposal in place — it serves as the proposal log/changelog.