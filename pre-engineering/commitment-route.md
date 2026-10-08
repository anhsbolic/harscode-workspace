# Commitment Route

Use this guidance to take one ELIGIBLE product commitment depth-first from interaction evidence to durable engineering handoff.

## Entry conditions

Before starting, the commitment should already be:

- meaningful;
- semantically ready enough;
- dependency-closed enough for its current product claim;
- truthful;
- bounded.

If one of these is materially false, return to the commitment frontier instead of pretending the route has started.

Default to one active commitment route at a time.

This is not rigid isolation. A minimum prerequisite behavior may travel inside the active commitment only when it is materially required for dependency closure and the combined commitment still passes the readiness / boundedness gates.

## Route

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

## Collaboration loop for substantive decisions

For a material blocker:

```text
frame the blocked commitment / behavior
→ verify relevant current authority
→ challenge the strongest risk / hidden assumption
→ present bounded alternatives
→ recommend one direction when evidence is sufficient
→ human confirms / refines
→ persist the approved decision
→ verify persisted state
→ continue
```

Do not reopen a settled decision without materially new evidence.

Do not resolve unrelated future commitments merely because they are visible.

## Interaction Exploration

Make the product concrete without jumping directly to a predetermined form, screen, API, or implementation.

For each material scene, ask:

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

Useful outputs include:

- scene / state progression;
- consequential meaning before commitment;
- observable state transitions;
- valid unknown / pending / incomplete states;
- material failure / recovery behavior;
- surfaced product / design / engineering questions.

Classify ambiguity rather than silently solving it.

Resolve only blockers required for the active commitment to remain truthful.

### Interaction Exploration exit

Move forward when:

- the commitment can be experienced end-to-end at the product-behavior level;
- material consequences are understandable before consequential actions;
- success, incomplete, failure, and relevant uncertainty are distinguishable enough;
- material exception behavior is bounded;
- design freedom can be distinguished from product semantics;
- no unresolved product decision is required to confirm the behavior.

A prototype or visual proof may be useful evidence, but it is not automatic authority.

## Confirmed Product Behavior

Promote sufficiently tested interaction evidence into confirmed product behavior / invariants.

Do not invent a new scenario here.

Challenge candidate behavior for:

- hidden contradictions;
- accidental expansion into another commitment;
- behavior that is actually only a design choice;
- optional recovery / convenience being promoted into mandatory capability;
- fuzzy states downstream readers cannot operationally interpret;
- unresolved product decisions hidden inside apparently complete wording.

### Confirmed Behavior exit

Move forward when:

- behavior and invariants are explicit;
- product semantics are separated from design freedom;
- open / parked scope is explicit;
- no material unresolved product decision blocks requirement derivation.

## Requirements

Derive both requirement views from the same confirmed behavior:

```text
Confirmed Product Behavior
        │
        ├── Experience Requirements
        └── Engineering Requirements
```

### Experience Requirements

State what the experience must make:

- understandable;
- possible;
- visible / inspectable;
- distinguishable;
- recoverable, when recovery is actually required.

Do not prescribe exact screens, copy, interaction pattern, or visual treatment unless those are themselves confirmed product / design requirements.

### Engineering Requirements

State what the delivered product must preserve so the confirmed behavior can remain true.

Do not prescribe:

- architecture;
- API shape;
- database schema;
- transaction mechanism;
- service / component decomposition;
- implementation strategy;

unless the target project's engineering authority has already established one of those as a real constraint.

Prefer observable semantic requirements over implementation-shaped wording.

### Requirements exit

Audit:

- every requirement traces to confirmed behavior;
- XR and ER preserve one product meaning;
- neither side invents Product Truth;
- no unnecessary solution-lock has been introduced;
- engineering decision space remains explicit.

## Durable Engineering Handoff

Stage / route completion packages; it does not reinterpret.

If the target project has explicitly approved commitment-specific behavior / requirements as binding within this commitment, the handoff must identify that scoped authority clearly. “Not whole-product canonical” must not be treated as permission for downstream engineering to ignore it.

A fresh engineering reader should be able to answer from durable artifacts:

- What product claim is being handed off?
- What must remain true?
- What product behavior is confirmed?
- What Experience Requirements apply?
- What Engineering Requirements apply?
- What remains open / out of scope?
- What may design decide?
- What may engineering decide?
- Which interaction evidence / constraints materially matter?
- Is the original product conversation unnecessary to begin?

A useful read order is usually:

```text
current Product / Domain Authority
→ confirmed behavior
→ requirements
→ interaction evidence when context is needed
→ commitment / dependency context when needed
```

### Handoff exit

The pre-engineering route is complete when the durable handoff is:

- sufficiently complete by inspection to support a fresh engineering reader without requiring the original chat;
- explicit about binding scoped authority, open / parked scope, and engineering decision space;
- Human-approved when the project requires that gate.

```text
handoff prepared + Human-approved
→ PRE-ENGINEERING ROUTE COMPLETE

route complete
≠ independent cold-start consumption already observed
≠ implemented
≠ delivered
≠ prerequisite automatically real for downstream commitments
```

### Cold-start handoff validation

The first independent fresh engineering session provides a separate validation result:

```text
fresh engineering reader
+ durable handoff
→ can / cannot begin without reconstructing the original conversation
```

This is **validation evidence**, not another pre-engineering stage.

If cold-start consumption reveals a material missing decision, authority ambiguity, or unusable handoff gap, feed that evidence upstream and reopen only the affected concern.

A successful pre-engineering route by itself demonstrates route execution and handoff preparation. It does not by itself prove implementation / delivery correctness, preservation of the behavior in the real product, or universal validity of the exact artifact / stage mechanism.

If implementation later reveals a material product-semantic gap, return it upstream rather than silently redefining behavior downstream.

## Session boundary

A commitment may use one or several sessions.

Quality must not depend on session continuity.

For a fresh session, use `kickoff-prompt.md` and reconstruct the current state from durable authority / artifacts.
