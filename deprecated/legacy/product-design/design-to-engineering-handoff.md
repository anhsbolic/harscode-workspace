# Design to Engineering Handoff

Use this guidance when upstream product/design work is approved enough to move into engineering exploration and planning.

The goal is not to make engineering copy screenshots. The goal is to preserve design intent while giving engineering clear ownership of implementation mechanics.

## 1. Handoff is a boundary, not a file transfer

A useful handoff answers three questions:

```text
What must remain true?
What is still open?
What may engineering decide?
```

Without that distinction, one of two failures usually occurs:

- engineering accidentally redesigns the product while coding; or
- design over-specifies implementation mechanics and blocks healthy engineering decisions.

## 2. Classify design readiness

Before Build, classify the relevant surface or feature.

### READY

The product/design intent is sufficiently established for implementation.

Engineering may still make local implementation decisions, but should not reopen the selected design thesis without material evidence.

### PARTIAL

The core intent is established, but limited local gaps remain.

Engineering may resolve small gaps using current principles and patterns if the decision does not create significant new precedent.

Surface assumptions when they may become reusable precedent.

### OPEN

Material product/design intent is unresolved.

Examples:

- information hierarchy is unknown;
- trust/provenance semantics are unresolved;
- main interaction model is undecided;
- brand expression is still being selected;
- a consequential state has no approved behavior.

Do not make an OPEN surface canonical accidentally inside implementation.

## 3. Separate invariants from engineering freedom

A good handoff defines design invariants rather than prescribing code structure.

Design invariants may include:

- information priority;
- semantic distinctions;
- interaction intent;
- public vs operational expressive intensity;
- brand color roles;
- provenance visibility;
- progress meaning;
- accessibility behavior;
- responsive priority;
- asset truthfulness.

Engineering normally owns:

- component APIs;
- DOM structure;
- CSS/Tailwind representation;
- token naming;
- state ownership mechanics;
- data-fetching implementation;
- performance strategy;
- test implementation;
- exact breakpoint mechanics unless design requires a specific behavior.

Rule of thumb:

> Design hands off meaning and constraints; engineering owns mechanics.

## 4. Reconcile the existing implementation before Build

When implementation already exists, do not assume it should either be preserved or reset.

Perform an explicit reconciliation against current design authority.

Classify implementation elements as:

```text
STRUCTURALLY VALUABLE
→ keep or adapt

VISUALLY STALE BUT STRUCTURALLY SOUND
→ restyle/migrate

SEMANTICALLY STALE
→ redesign/rewrite

ACCIDENTAL LEGACY AUTHORITY
→ remove or stop treating as precedent
```

Existing code is current-state evidence, not design authority merely because it exists.

## 5. Reset vs migration is an engineering strategy decision

Do not decide “rewrite everything” or “preserve everything” from design taste alone.

Evaluate:

- whether structure matches current product semantics;
- whether existing component boundaries remain healthy;
- how deeply stale design assumptions are embedded;
- shared-component blast radius;
- test coverage and migration risk;
- cost of translating versus replacing;
- whether the old implementation would keep influencing future work if partially retained.

A hard reset can be safer when stale assumptions are pervasive.

Selective migration is safer when structure remains valid and the gap is primarily visual.

The correct choice depends on current code evidence.

## 6. Reconcile documentation before implementation if it conflicts

If architecture docs, agent instructions, or implementation notes still encode superseded design assumptions, resolve or explicitly record the conflict before Build.

Examples:

- old brand color still described as primary action;
- removed prototype still named as authority;
- old font/token system still described as canonical;
- documentation still says a visual system does not exist after one has been approved.

Engineering should not be asked to choose between contradictory instructions.

## 7. Calibrate before proliferating

When a new visual/product system is entering implementation, prefer one representative calibration slice before converting every route.

A good calibration surface exercises enough of the system to expose problems such as:

- typography hierarchy;
- brand color restraint;
- action hierarchy;
- surface grouping;
- responsive behavior;
- imagery/placeholder treatment;
- representative shared primitives;
- public vs product expression.

The calibration slice is not necessarily the whole page or feature.

Its job is to generate trustworthy implementation evidence before broad rollout.

Rule of thumb:

> Establish one coherent precedent before multiplying it across the product.

## 8. Choose the smallest representative slice that can fail

Do not make the calibration slice so small that every direction looks acceptable.

A useful slice should include enough realistic content and interaction to expose likely failure.

Examples:

- real heading/body hierarchy;
- a meaningful CTA relationship;
- one representative content/card/surface pattern;
- realistic long content;
- desktop and mobile composition;
- at least one state where semantic color or provenance matters if relevant.

## 9. Do not complete unrelated product semantics for visual polish

A foundation/calibration task may need placeholder or provisional content from domains that are not yet ready.

Do not invent canonical business meaning to make the mock look complete.

Keep unresolved semantics visibly provisional, or omit them from the calibration surface.

Visual completeness is not worth product-semantic drift.

## 10. Translate design tokens deliberately

Approved visual-system values still need engineering representation.

Translate them into the project's actual styling system while preserving semantic roles.

Prefer semantic roles such as:

```text
canvas
surface-subtle
text-primary
text-muted
border-default
brand-energy
semantic-success
semantic-warning
semantic-error
```

over exposing only raw color names everywhere.

But do not create global tokens merely because one isolated value exists.

A design token should represent a stable reusable role, not just centralize arbitrary numbers.

## 11. Do not overfit implementation to visual proofs

Approved proofs may contain incidental details:

- arbitrary mock copy;
- generated metrics;
- convenient spacing;
- accidental card geometry;
- one viewport's composition;
- prototype-only controls.

Engineering should preserve approved system behavior and hierarchy, not clone incidental pixels.

When uncertain, ask:

> Is this detail part of the approved rule, or only visible in the proof?

## 12. Shared primitive changes require blast-radius analysis

Implementing a new design generation often touches broad UI primitives.

Before materially changing shared primitives:

```text
classify the change
→ discover actual consumers and wrappers
→ identify representative risk cases
→ implement
→ verify primitive contract
→ verify representative downstream consumers
```

Do not assume a visual-system migration makes breaking primitive changes safe.

A tiny primitive can have a larger product blast radius than a large route-local component.

## 13. Semantic components should not be created from visual similarity alone

Two surfaces looking similar does not prove they share a semantic contract.

For example, funding progress and operational progress may both involve horizontal space, but different meanings may justify different components or compositions.

Prefer semantic ownership over visual deduplication.

Implementation reuse must not erase product distinctions.

## 14. Preserve source/provenance semantics through implementation

If upstream design distinguishes system facts, reported information, pending information, or outcomes, engineering must not collapse them into one generic badge/state component for convenience.

A generic primitive may still be used underneath, but feature-level composition must preserve the distinction.

## 15. Accessibility is part of intent, not post-processing

Design handoff should preserve requirements such as:

- state is not color-only;
- meaningful labels remain visible;
- keyboard/focus behavior remains understandable;
- content priority survives responsive collapse;
- contrast is adequate in actual implementation;
- imagery alternatives and controls are accessible.

Engineering may choose the implementation mechanism, but cannot treat these as decorative polish.

## 16. Responsive design preserves priority, not screenshots

Responsive implementation should preserve:

1. the user's current task;
2. trust-critical information;
3. consequences;
4. provenance/chronology where relevant;
5. accessible actions;
6. content dignity.

Decorative composition may simplify or disappear.

Do not force desktop composition into smaller widths merely to preserve visual similarity.

## 17. Rendered verification is required for material visual work

Compilation and component tests cannot prove:

- hierarchy;
- spacing;
- clipping/overflow;
- typography feel;
- responsive behavior;
- visual density;
- whether the brand/product relationship survives implementation.

Use actual rendered inspection during implementation.

Choose representative states, content conditions, and viewports based on risk.

## 18. Human acceptance remains distinct from agent inspection

Agent-driven render → inspect → fix is valuable implementation feedback.

It is not automatically final product acceptance.

Material brand/product UI implementation should receive human rendered acceptance at representative scope when the project requires it.

Human review should focus on:

- visual hierarchy;
- comprehension;
- responsive usability;
- preservation of approved product/design intent;
- asset appropriateness;
- obvious state behavior.

## 19. Reopen approved design only with material evidence

Implementation can expose problems that upstream proofs missed.

Examples:

- contrast failure;
- unrealistic density;
- localization/content growth breakage;
- semantic ambiguity;
- inaccessible interaction;
- a token that behaves poorly across contexts.

These are valid reasons to route a decision back upstream.

Do not reopen approved choices merely because an engineer prefers another aesthetic.

When reopening, describe the concrete implementation evidence and the affected invariant.

## 20. New implementation precedent should be intentional

Before establishing a new pattern not explicitly covered by current design authority, ask:

```text
Is this local implementation detail?
→ engineering may decide locally

Will this likely be copied across multiple surfaces?
→ evaluate as reusable precedent

Does it change product meaning, trust, hierarchy, or brand identity?
→ route upstream for design/product authority
```

A one-off can reveal a meaningful boundary; repeated occurrences are evidence worth evaluating, not automatic proof of abstraction.

## 21. Handoff packet

A lightweight implementation-ready handoff should make discoverable:

- current product/domain authority;
- active design authority map;
- selected visual references and their limits;
- relevant OPEN decisions;
- applicable readiness classification;
- engineering invariants;
- engineering freedoms;
- representative calibration target if a new system is being introduced;
- required human/rendered acceptance.

Do not duplicate every upstream document into the task. Route to the owners.

## Rule of thumbs

- Design decisions can be complete while implementation strategy remains open.
- Existing code is evidence, not automatic authority.
- Do not redesign materially OPEN questions inside JSX/CSS.
- Do not preserve stale implementation solely because it exists.
- Do not reset healthy structure solely because the aesthetic changed.
- Calibrate before proliferating.
- Choose a representative slice that can actually expose failure.
- Design hands off invariants; engineering owns mechanics.
- Shared primitives require downstream impact analysis.
- Reuse must not collapse semantic distinctions.
- Responsive implementation preserves priority, not screenshot geometry.
- Rendered verification is part of material UI engineering.
- Human acceptance and agent inspection are different gates.
- Reopen approved design only when implementation produces material evidence.
