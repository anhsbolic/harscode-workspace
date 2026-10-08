# Add reusable pre-engineering commitment-route guidance

**Status:** Proposed
**Date:** 2026-10-08
**Protection Tier:** general
**Triggered by:** Kencleng Pilot #3 produced one complete real commitment route from product-semantic readiness through interaction exploration, confirmed behavior, requirements, and durable engineering handoff. The run also exposed a repeatability requirement: future commitments should be able to run in separate sessions without relying on remembered conversation.
**Target area:** new shared upstream pre-engineering guidance
**Target file(s):**
- `AGENTS.md` — route product-behavior pre-engineering work to a dedicated guidance area.
- `README.md` — add pre-engineering to the workspace mental model and authority boundary.
- `pre-engineering/AGENTS.md` — lightweight router + hard rules.
- `pre-engineering/README.md` — scope, authority, whole-enough → commitment-frontier model.
- `pre-engineering/commitment-route.md` — reusable depth-first commitment route and stage-exit discipline.
- `pre-engineering/kickoff-prompt.md` — fresh-session bootstrap contract for one commitment.
- `pre-engineering/control-tower.md` — optional derived visual progress-dashboard guidance; explicitly non-authoritative.

## Gap found

Current Harscode separates:

```text
product/domain truth
→ product-design when materially open
→ engineering Exploration
→ Techplan
→ Build / Review / Testing / PR
```

This is strong when product/domain behavior is already sufficiently concrete, or when the remaining upstream ambiguity is primarily product-brand/UI/design authority.

A real Kencleng validation run exposed a separate upstream gap:

> Product/domain truth can be semantically correct while still being too abstract for engineering, and the missing work is not necessarily visual design.

The missing reusable discipline includes:

- understanding the whole product only far enough to avoid local semantic mistakes;
- actor outcomes / responsibilities;
- representative workflow scenarios;
- deriving bounded product commitments;
- testing whether a commitment is meaningful, semantically ready, dependency-closed enough, truthful, and bounded;
- taking one ready commitment depth-first through interaction exploration;
- confirming product behavior before writing requirements;
- deriving Experience Requirements and Engineering Requirements from the same behavior;
- producing a durable handoff usable without the original conversation;
- carrying this state across fresh chat / agent sessions;
- visualizing progress without turning the visualization into a second source of truth.

Without guidance here, an agent can jump from high-level product truth directly into engineering Exploration / Techplan, or can misuse `product-design/` as a container for business/product semantics it does not own.

The Kencleng run also exposed two workflow failure modes worth preventing generically:

1. **full-roadmap drift** — resolving every blocked future commitment before allowing one ready commitment to progress;
2. **chat-memory dependency** — a commitment is only understandable if the same long conversation continues.

## Proposed change

### 1. Add a dedicated `pre-engineering/` area

Proposed ownership:

> `pre-engineering/` owns reusable discipline for turning project-owned product/domain truth into bounded confirmed product behavior and traceable requirements that engineering can consume without reconstructing the originating product conversation.

It does **not** own project product semantics.

Project-specific product/domain truth remains in the target repository.

It does **not** own technical architecture, API/database design, implementation strategy, or code.

It does **not** replace `product-design/`. Product-design remains responsible for reusable product-brand/UI/UX authority-building. A pre-engineering commitment may invoke product-design guidance when visual / interaction authority is materially open.

### 2. Update the root routing model

Proposed root `AGENTS.md` routing addition:

```text
- Turning project-owned product/domain truth into confirmed product behavior,
  traceable requirements, and a durable pre-engineering handoff
  → pre-engineering/AGENTS.md.
```

Proposed root `README.md` routing model:

```text
                         ┌─ pre-engineering/
                         │  when product behavior /
project product truth ───┤  requirement meaning is materially open
                         │
                         ├─ product-design/
                         │  when product-brand / UI / UX
                         │  authority is materially open
                         │
                         └─ engineering Exploration
                            when upstream meaning is ready enough
```

`pre-engineering/` and `product-design/` are **conditional sibling upstream routes**, not mandatory sequential phases.

They may expose gaps owned by the other route:

```text
pre-engineering
→ material product-brand / UI / UX ambiguity
→ product-design

product-design
→ missing product / behavioral semantics
→ return to project Product Authority / pre-engineering
```

Neither route may silently take authority owned by the other.

### 3. Add `pre-engineering/AGENTS.md`

Proposed hard-rule surface:

```markdown
# AGENTS.md — pre-engineering/

Use this area when project-owned Product Truth exists but product behavior is
not yet concrete enough for engineering to proceed without inventing meaning.

## Hard rules

- Project product/domain truth remains owned by the target project.
- Read current product authority before historical specs, implementation, or code.
- Existing implementation, prototypes, schemas, and historical artifacts are evidence,
  not automatic Product Authority.
- Work scenario/workflow-first; do not default to persona × feature matrices.
- Distinguish capability / product behavior from feature / surface / implementation.
- Do not solve technical architecture, API, database, component, or implementation design here.
- A ready commitment may progress without resolving unrelated blocked future commitments.
- Default to one active commitment route at a time.
- A minimum prerequisite behavior may travel inside the active commitment only when it is materially required for dependency closure and the combined scope remains meaningful, semantically ready enough, truthful, and bounded.
- Reaching durable pre-engineering handoff does **not** prove that a prerequisite's real product behavior has been implemented / delivered.
- Interaction exploration precedes confirmed behavior; confirmed behavior precedes requirements.
- Derive Experience Requirements and Engineering Requirements from the same confirmed behavior.
- Durable correctness must not depend on remembered chat context.
- Human approval is required for substantive product decisions before promoting them to durable state.
- A progress dashboard may visualize state but must not become Product Authority.

## Routing

- Overall scope / authority / model → README.md
- Run one commitment depth-first → commitment-route.md
- Start a fresh commitment session → kickoff-prompt.md
- Maintain an optional visual progress dashboard → control-tower.md
```

### 4. Add `pre-engineering/README.md`

Proposed core model:

```text
Product / Domain Truth
→ Whole-enough Product Understanding
→ Actor Outcomes / Responsibilities
→ Representative Scenarios
→ Commitment Frontier
→ one ELIGIBLE commitment
→ Interaction Exploration
→ Confirmed Product Behavior
→ Experience + Engineering Requirements
→ Durable Engineering Handoff
```

Important qualification:

- this is a **starting model**, not a mandatory fixed taxonomy;
- names / artifact shapes may vary by project;
- do not require complete product specification before one commitment can progress;
- the reusable quality floor is semantic readiness, dependency closure, truthfulness, boundedness, explicit authority, and durable handoff.

Proposed readiness concept:

```text
A commitment is ELIGIBLE when it is:

- meaningful;
- semantically ready enough;
- dependency-closed enough for its product claim;
- truthful;
- bounded.
```

`ELIGIBLE` is sufficient readiness to enter the commitment route. Do not add a redundant “selected” readiness gate.

If multiple independent items are ELIGIBLE, choosing execution order among them is not another readiness state.

### Dependency semantics

Dependency closure is about the **real product behavior required for the active commitment's claim**, not merely the existence of an upstream specification / handoff.

```text
prerequisite reaches durable pre-engineering handoff
≠ prerequisite is implemented
≠ prerequisite is delivered / real in the product
≠ downstream dependency automatically satisfied
```

A completed prerequisite handoff proves that the prerequisite behavior is sufficiently defined for engineering; it does not prove that the behavior exists in delivery.

For an active commitment whose prerequisite is not yet real, valid options are:

```text
WAIT
→ keep the commitment dependency-blocked until the prerequisite becomes real

or

INCLUDE
→ carry only the minimum required prerequisite behavior inside the active commitment
   when the combined claim remains meaningful, semantically ready enough,
   dependency-closed enough, truthful, and bounded
```

Do not use the INCLUDE option to pull unrelated future scope into the commitment.

### 5. Add `pre-engineering/commitment-route.md`

Proposed runtime loop:

```text
ELIGIBLE commitment
↓
Interaction Exploration
↓
Confirmed Product Behavior
↓
Experience Requirements + Engineering Requirements
↓
Durable Engineering Handoff
↓
route complete
```

#### Interaction Exploration

Make the product concrete without jumping directly to a form / screen / implementation.

For each material scene ask:

```text
what the actor knows
what the actor sees
what the actor can do
what the product knows
what state changes
what must remain distinguishable
what can fail
how recovery behaves
```

Classify surfaced ambiguity as appropriate:

- OPEN PRODUCT DECISION
- OPEN EXPERIENCE / DESIGN DECISION
- OPEN ENGINEERING CONSTRAINT
- OBSERVATION / EVIDENCE
- PARKED — NOT NEEDED YET

Resolve only blockers required for the active commitment to remain truthful.

Default to one active commitment route at a time. This is not rigid isolation: a minimum prerequisite behavior may be included when the active product claim cannot otherwise become dependency-closed, but only if the combined commitment still passes the readiness / boundedness gates.

#### Confirmed Product Behavior

Promote tested interaction evidence into behavior / invariants.

Do not:

- invent a new scenario in this stage;
- turn design choices into product invariants;
- turn optional recovery into mandatory capability without evidence;
- use fuzzy states that downstream readers cannot operationally interpret.

#### Requirements

Derive both requirement views from the same behavior:

```text
Confirmed Product Behavior
        │
        ├── Experience Requirements
        └── Engineering Requirements
```

Experience Requirements state what must be understandable, possible, visible, or distinguishable.

Engineering Requirements state what the delivered product must preserve.

Neither side owns implementation architecture.

#### Durable Handoff

A fresh engineering reader should be able to answer:

- what must remain true;
- what behavior is confirmed;
- what requirements follow;
- what remains open / out of scope;
- what design may decide;
- what engineering may decide;
- which evidence / constraints materially matter.

Original chat must not be required.

#### Decision loop

For a substantive blocker:

```text
frame
→ verify relevant authority
→ challenge strongest risk / hidden assumption
→ present bounded alternatives
→ recommend one direction when evidence is sufficient
→ human confirms / refines
→ persist the decision
→ verify persisted state
→ continue
```

Do not reopen a settled decision without materially new evidence.

#### Exit discipline

Do not polish a stage indefinitely.

Move when the next stage can proceed without inventing a material decision.

If a later stage discovers a material upstream product gap, stop and return it upstream rather than resolving it silently.

### 6. Add `pre-engineering/kickoff-prompt.md`

Proposed fresh-session invocation contract:

```text
You are taking one bounded product commitment through the pre-engineering route.

Read, in order:
1. target project's current Product / Domain Authority;
2. the current progress dashboard if one exists (navigation only, not authority);
3. the owning representative scenario / commitment definition;
4. the commitment's eligibility decision and material dependencies;
5. the current state of every material prerequisite actually required for this commitment, distinguishing:
   - pre-engineering definition / handoff state; and
   - real product implementation / delivery state when known.

Do not rely on previous chat memory.

First report:
- active commitment and product claim;
- current route position;
- authority already settled;
- material dependencies, including whether each is merely defined / handed off versus actually real / delivered;
- whether any minimum prerequisite behavior must travel inside this commitment for truthful dependency closure;
- what is explicitly open / parked;
- the next stage exit question.

Then work depth-first on this commitment.

Rules:
- challenge first, then commit;
- human is final authority for substantive product decisions;
- checkpoint each material approved decision in its owning durable artifact;
- verify persistence before continuing;
- do not resolve unrelated blocked future commitments;
- do not treat a prerequisite Stage 7 / handoff-complete state as proof that its real product behavior is delivered;
- include minimum prerequisite behavior only when required for dependency closure and still bounded;
- do not cross into architecture / implementation;
- update the progress dashboard only after owning artifacts change;
- stop at durable engineering handoff.
```

This prompt intentionally makes separate chat / agent sessions safe by reconstructing state from durable artifacts.

### 7. Add `pre-engineering/control-tower.md`

Proposed principle:

> A Control Tower is a derived navigation / progress dashboard. It is never Product Authority.

Suggested grammar:

```text
STATION / AREA = stage / maturity area
NODE           = tracked product-work pointer
COMMITMENT     = work item that travels the depth-first route
RAIL           = derivation / progression / dependency
SIGNAL         = readiness / progress state
```

Minimum useful signals:

```text
COMPLETE
ACTIVE
ELIGIBLE
BLOCKED
WAITING
ROUTE COMPLETE
```

Key rules:

- an ELIGIBLE commitment remains at its current station until the next stage actually begins;
- “ready to move” must not visually imply “already moved”;
- blocked future commitments may remain parked while another commitment progresses;
- the dashboard updates **after** the owning artifact changes;
- route completion means pre-engineering completion, not real implementation / delivery;
- downstream dependencies are not satisfied merely because an upstream commitment reached handoff;
- when useful, show prerequisite definition / handoff state separately from real delivery state so the dashboard does not create fake dependency closure.

### 8. Keep project retrospectives out of runtime guidance

Kencleng's detailed C1 history remains in the Kencleng repository as COLD project evidence.

Harscode guidance should carry only the generic behavior required to reproduce the quality floor.

Examples / retros may be linked conditionally for calibration, but must not become mandatory startup context.

## Rationale

This is generic because the observed problem is not donation-specific:

- product truth can exist while observable behavior is still underspecified;
- downstream engineering can accidentally invent missing semantics;
- full-product specification can become a waterfall bottleneck;
- multiple commitments can have partial-order dependencies;
- interaction evidence can expose semantic gaps before requirement writing;
- separate fresh sessions require durable reconstruction;
- progress dashboards are useful but dangerous if promoted into authority.

The proposal also preserves existing Harscode boundaries:

- target project owns product/domain truth;
- `product-design/` continues to own reusable product-brand/UI/UX authority-building;
- `pre-engineering/` would own product-behavior concretization and handoff discipline;
- `pre-engineering/` and `product-design/` are sibling conditional routes, not a fixed sequence;
- `workflow/` continues to own engineering Exploration onward;
- engineering keeps architecture / implementation mechanics.

The Kencleng C1 route is sufficient evidence for a **proposal and experimental guidance**, but not sufficient evidence to freeze every Pilot #3 stage label as permanent Harscode policy.

C2 / C3 and later materially different product commitments should serve as further Continuous Real-Task Validation runs before declaring the model mature.

---

*After human review: update the Status above. If Accepted, create the new `pre-engineering/` guidance and apply the root routing changes. Leave this proposal in place as changelog evidence.*
