# Pre-Engineering

`pre-engineering/` is Harscode's reusable upstream discipline for turning project-owned Product / Domain Truth into bounded confirmed product behavior, traceable requirements, and a durable engineering handoff.

It does **not** own project semantics. Product / Domain Truth remains in the target project.

It does **not** own technical architecture, API/database design, implementation strategy, or code.

It does **not** replace `product-design/`. The two are conditional sibling routes:

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

If pre-engineering exposes a material product-brand / UI / UX ambiguity, route that concern to `product-design/`.

If product-design exposes missing product / behavioral semantics, return that concern to project Product Authority / pre-engineering.

Neither route may silently take authority owned by the other.

## When to use this area

Use pre-engineering when current project Product Truth is directionally correct but engineering would still have to invent material product meaning, for example:

- actor outcome / responsibility is unclear;
- a representative workflow cannot yet be described truthfully;
- product states / consequences are underspecified;
- dependency meaning is unclear;
- a capability is being prematurely treated as a UI feature;
- requirements would otherwise be two independent interpretations by design and engineering;
- the engineering handoff would require reconstructing the original product conversation.

Skip this area when product behavior is already sufficiently concrete and durable for engineering Exploration.

## Starting model

The default model is:

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

This is a starting model, not a mandatory fixed taxonomy.

Projects may use different labels or artifact shapes. Preserve the quality floor rather than the exact names.

## Whole-enough before depth-first

Do not fully specify the whole product before useful commitment work can begin.

Understand enough of the surrounding product to avoid local semantic mistakes, expose major actors / dependencies, and identify representative scenarios.

Then move depth-first on a bounded commitment once it is ready.

## Representative scenarios before feature matrices

Use scenarios / workflows as the primary requirement-discovery unit.

A representative scenario should make clear enough of:

- actor situation;
- responsibility / action;
- product consequence;
- dependency;
- relevant uncertainty / failure.

Do not default to persona × feature matrices or premature surface decomposition.

## Commitment frontier

A commitment is a bounded product claim / actor outcome that can be taken through the depth-first pre-engineering route.

A commitment is **ELIGIBLE** when it is:

- meaningful;
- semantically ready enough;
- dependency-closed enough for its product claim;
- truthful;
- bounded.

`ELIGIBLE` is sufficient readiness to enter the commitment route. Do not add a redundant readiness state after eligibility.

If multiple independent items are ELIGIBLE, choosing execution order among them is not another readiness state.

Blocked future commitments do not need to be resolved merely to make a full-product sequence look complete.

## Dependency semantics

Dependency closure is about the **real product behavior required for the active commitment's claim**, not merely the existence of an upstream specification / handoff.

```text
prerequisite reaches durable pre-engineering handoff
≠ prerequisite is implemented
≠ prerequisite is delivered / real in the product
≠ downstream dependency automatically satisfied
```

A completed prerequisite handoff proves that the prerequisite behavior is sufficiently defined for engineering; it does not prove that the behavior exists in delivery.

For an active commitment whose prerequisite is not yet real:

```text
WAIT
→ keep the commitment dependency-blocked until the prerequisite becomes real

or

INCLUDE
→ carry only the minimum required prerequisite behavior inside the active commitment
   when the combined claim remains meaningful, semantically ready enough,
   dependency-closed enough, truthful, and bounded
```

Do not use INCLUDE to pull unrelated future scope into the commitment.

## Depth-first commitment route

Once ELIGIBLE, run one commitment depth-first:

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

See `commitment-route.md` for the execution discipline.

## Decision classifications

Use classifications only when they help preserve ownership and avoid silent guessing:

- **OBSERVATION / EVIDENCE** — useful fact or finding, not a decision.
- **OPEN PRODUCT DECISION** — missing product meaning required before truthful progression.
- **OPEN EXPERIENCE / DESIGN DECISION** — presentation / interaction choice that can remain open without changing product truth.
- **OPEN ENGINEERING CONSTRAINT** — technical fact that may materially constrain behavior but belongs to engineering to resolve or report.
- **WORKING DECISION** — human-approved for the active route but not necessarily canonical project authority.
- **PARKED — NOT NEEDED YET** — intentionally unresolved because it does not block the active commitment.

Use the target project's own authority vocabulary when one already exists.

## Stage movement

Do not polish a stage indefinitely.

Move when the next stage can proceed without inventing a material decision.

If a later stage discovers a material upstream product gap, stop and return the question upstream rather than resolving it silently.

## Fresh-session quality

A new session must reconstruct required truth from durable artifacts.

Do not rely on remembered chat context.

Use `kickoff-prompt.md` to start a fresh commitment session.

## Authority and persistence

Durable project correctness should remain reconstructable from project-owned authority + current pre-engineering artifacts.

Checkpoint substantive approved product decisions in their owning target-project artifact.

Verify the persisted state before continuing when the decision materially changes the active commitment.

A derived progress dashboard may improve navigation but does not become authority. See `control-tower.md`.

## Maturity

This guidance is under Continuous Real-Task Validation.

Do not freeze project-specific stage labels, templates, or artifact shapes into universal policy merely because one validation run used them successfully.

Preserve the reusable semantics; revise the guidance when materially different real tasks expose a stronger model.
