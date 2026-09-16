# Upstream Product Design Guidance

**Status:** Proposed
**Date:** 2026-09-16
**Protection Tier:** general
**Triggered by:** A full upstream product-brand/UI-design cycle in Kencleng exposed a repeatable gap: Harscode has strong engineering workflow and frontend implementation guidance, but no generic guidance for deliberately turning product truth, user trust needs, brand intent, visual exploration, and UI/UX decisions into implementation-ready design authority before engineering begins.
**Target area:** best-practices
**Target file(s):**
- `best-practices/index.md` — add routing entries for a new `product-design` category.
- `best-practices/product-design/product-brand-and-ui-exploration.md` — add generic upstream exploration guidance for product brand + UI direction.
- `best-practices/product-design/design-authority-and-canonicalization.md` — add rules for separating exploration evidence from canonical design authority and preventing multiple active sources of truth.
- `best-practices/product-design/design-to-engineering-handoff.md` — add readiness and handoff guidance for moving from approved design authority into engineering exploration/techplanning without accidentally redesigning inside implementation.

## Gap found

Harscode currently reaches product work mostly through engineering-facing concerns: feature exploration, frontend implementation, prototype translation, responsive behavior, rendered verification, component abstraction, and testing boundaries.

That leaves a material upstream gap.

When a product does not yet have sufficiently explicit brand, visual, and UI/UX authority, engineering exploration is too late to decide questions such as:

- what the product should emotionally and visually communicate;
- which trust or persuasion strategy is acceptable;
- what visual language is selected versus merely explored;
- which information classes must be visually distinct;
- what is product truth versus organizer/user claims versus system state;
- which visual decisions are brand identity and therefore human-authority decisions;
- whether an existing prototype is still authoritative;
- when generated visual studies are evidence of direction versus pixel-level specifications;
- when a design system is ready enough for implementation;
- when old design generations should be removed rather than kept as competing active guidance.

Without explicit upstream guidance, common failure modes are predictable:

1. **Implementation becomes accidental design authority.** Existing CSS, tokens, or components are treated as truth simply because they exist.
2. **Prototype gravity.** A prototype or generated UI becomes the de facto product specification even when its semantics, visual system, or mock data are stale.
3. **Taste-first design.** Teams choose colors, fonts, cards, or illustration style before resolving product posture, trust requirements, evidence semantics, and user hesitation.
4. **Multiple active sources of truth.** New design direction is added while old guidelines/prototypes remain active, leaving engineers to choose whichever artifact is easiest.
5. **Visual proof overreach.** A screenshot or generated study is treated as a route contract or pixel-perfect implementation spec.
6. **Semantic color leakage.** Brand colors silently acquire product meanings such as trusted, verified, successful, urgent, or safe.
7. **Progress conflation.** Funding progress, operational progress, and reported outcomes are represented as one generic progress concept, producing misleading product meaning.
8. **Unresolved decisions silently invented in code.** Engineering fills material product/design gaps inside JSX/CSS rather than routing them back upstream.
9. **Canonicalization too early or too late.** Either weak exploration gets prematurely frozen, or approved decisions remain scattered in chat/prototypes and never become durable authority.
10. **Design-to-engineering handoff lacks an explicit boundary.** Teams continue reopening approved brand decisions during Build, or conversely treat implementation details as if design should dictate exact component/DOM structure.

The Kencleng cycle produced a useful generic pattern: move from domain/product truth to product posture, to competing creative directions, to human-selected direction, to visual proofs, to concrete visual-system authority, then hand off to engineering interpretation. The project-specific aesthetic choices are not reusable; the decision discipline is.

## Proposed change

Add a new `product-design` category under `best-practices/` with three focused files. The category is deliberately upstream of React/frontend implementation guidance. It should be applicable whether the implementation is React, native mobile, server-rendered web, or another UI stack.

### 1. Add index routing entries

Add rows equivalent to:

```markdown
| product-design | [product-design/product-brand-and-ui-exploration.md](product-design/product-brand-and-ui-exploration.md) | product design, brand direction, visual direction, UI direction, creative direction, design exploration, product posture, brand attributes, visual language | no | Derive product-brand/UI direction from product truth and user needs before choosing concrete visual tokens; compare real alternatives; use visual proofs as evidence, not authority by default |
| product-design | [product-design/design-authority-and-canonicalization.md](product-design/design-authority-and-canonicalization.md) | design authority, canonical design, design source of truth, prototype authority, visual reference, design guidelines, canonicalization, legacy design docs | no | Separate exploration evidence from active authority; promote approved decisions deliberately; remove or demote superseded active guidance so engineers do not choose among conflicting design generations |
| product-design | [product-design/design-to-engineering-handoff.md](product-design/design-to-engineering-handoff.md) | design handoff, design readiness, implementation readiness, engineering interpretation, design system implementation, visual system implementation, frontend foundation | no | Hand off approved design intent as constraints and invariants, not pixel cloning; classify unresolved design gaps before Build; let engineering own implementation mechanics without reopening approved product intent |
```

Suggested trigger-keyword additions should remain broad enough to catch upstream design work but should not cause ordinary React styling tasks to preload all three files.

---

## Proposed new file: `best-practices/product-design/product-brand-and-ui-exploration.md`

```markdown
# Product Brand + UI Exploration

Use this when the product needs a deliberate brand/product-UI direction before implementation can safely establish visual precedent.

This is not a styling checklist. The job is to move from product truth and user needs to a coherent, testable design thesis.

## Start from product truth, not aesthetics

Before choosing color, typography, illustration, card shape, or layout style, identify the product realities that visual design must not distort.

Examples of upstream truth include:

- who the users are and what decisions they are making;
- what information is known, reported, inferred, pending, or unavailable;
- what the product itself guarantees versus what another actor claims;
- irreversible or high-consequence actions;
- trust, safety, privacy, money, access, or identity constraints;
- the main hesitation or confidence gap users bring into the experience.

Design may frame truth. It must not upgrade truth.

Rule of thumb:

> **Resolve what the product must communicate before deciding how it should look.**

## Define experience posture before visual tokens

Capture the intended product posture in behavioral language first.

Useful questions:

- What should a skeptical but reasonable user feel after understanding the product?
- What should the product never do to persuade someone?
- Which qualities should remain visible even when content is difficult, incomplete, or negative?
- Should public/acquisition surfaces and operational/authenticated surfaces have different expressive intensity?
- Which attributes must survive a future logo/name refresh?

Prefer a compact thesis and a small set of attributes over a long mood-word list.

A good thesis has operational consequences.

Weak:

> modern, friendly, clean

Stronger:

> confidence before conversion

because it constrains hierarchy, CTA pressure, information ordering, and copy behavior.

## Challenge the emotional strategy

For products involving trust, money, health, identity, vulnerability, public claims, or social impact, explicitly challenge persuasive shortcuts.

Examples:

- urgency can become coercion;
- sadness can become exploitation;
- celebration can imply an outcome not yet proven;
- institutional visual language can create unearned credibility;
- playful language can trivialize consequential states;
- strong success color can imply verification where only a report exists.

Do not ask only, “does this feel good?” Ask:

> **What could this visual treatment cause a user to believe that the product cannot actually prove?**

## Explore multiple real directions

Do not jump from discovery directly to one polished moodboard.

Create 2–4 meaningfully different directions with clear trade-offs.

A direction should vary a coherent system, not just swap colors.

Compare dimensions such as:

- emotional temperature;
- editorial vs product-system expression;
- photography vs illustration balance;
- typography personality;
- surface density;
- trust expression;
- motion energy;
- public vs authenticated relationship.

Each direction should state:

- what it optimizes;
- why it fits the product;
- what can go wrong if pushed too far.

If every option is acceptable and visually similar, the exploration is not creating a meaningful decision.

## Synthesize instead of averaging

The selected result does not have to be one direction unchanged.

A strong synthesis may take:

- emotional character from one direction;
- trust discipline from another;
- operational restraint from a third.

But synthesis must still produce one coherent thesis. Do not preserve contradictory directions as permanent “flexibility.”

## Separate evidence structure from expressive style

In trust-sensitive products, identify which design elements carry product meaning and which carry brand expression.

Example split:

```text
truth / provenance / chronology / state
→ structural responsibility

color / type personality / imagery / illustration / composition
→ expressive responsibility
```

This prevents brand styling from silently becoming semantic authority.

## Distinguish information classes before styling them

Where product truth has multiple provenance classes, model them explicitly before choosing badges or colors.

Possible classes include:

- platform/system fact;
- user- or organizer-provided information;
- externally reported information;
- pending/not-yet-available information;
- confirmed system state;
- reported outcome.

Prefer label + source + context + chronology over color-only distinction.

The exact classes belong to the product domain; the generic rule is:

> **Different certainty/provenance should not collapse into one visual “trusted” treatment.**

## Treat unknown as a first-class state

A design system is more trustworthy when it can represent:

- not yet reported;
- unavailable;
- delayed;
- under review;
- changed;
- partially known.

Do not force every state into positive/negative semantics merely because the visual system has success/warning/error colors.

## Use visual proofs at the right moment

Textual direction alone is not enough to validate typography, color balance, spacing, surface behavior, and visual hierarchy.

After selecting a direction, create representative visual proofs that exercise the risky decisions.

Useful proof types:

- public/acquisition composition;
- operational/authenticated surface;
- typography/color/surface foundation board;
- truth/provenance grammar board;
- progress/state grammar board;
- representative mobile composition.

A proof should answer a decision question.

Bad reason:

> make a beautiful mockup

Better reason:

> verify that the expressive brand direction remains credible on a dense operational surface

## Do not let generated visuals become accidental product specs

AI-generated or manually composed visual studies may prove:

- character;
- hierarchy;
- composition principles;
- palette relationship;
- public/product expressive relationship.

They do not automatically prove:

- business semantics;
- API shape;
- exact copy;
- exact route content;
- component architecture;
- exact responsive behavior;
- pixel-level production geometry.

Document their authority level explicitly.

## Approve in layers

A useful sequence is:

```text
product/design principles
→ creative direction
→ representative visual proofs
→ concrete visual-system decisions
→ implementation readiness
```

Human approval should happen at the points where a decision creates durable brand/product precedent.

Do not make engineering wait for every decorative detail. Do not send engineering forward while foundational product/brand intent is still materially open.

## Rule of thumbs

- One strong thesis beats twenty adjectives.
- Product truth outranks visual references.
- Brand color is not automatically semantic color.
- Trust is usually better carried by structure than by badges.
- Unknown is a valid state.
- Public surfaces may be more expressive than operational surfaces without becoming a different brand.
- Photography can be evidence; illustration usually cannot.
- A progress visualization must represent a specific kind of progress.
- If two progress concepts have different meanings, do not make them look identical merely for component reuse.
- If a visual proof cannot fail the direction, it is decoration, not proof.
- Do not optimize for implementation convenience during upstream design exploration.
- Do not specify implementation mechanics unless they materially affect product/design intent.
```

---

## Proposed new file: `best-practices/product-design/design-authority-and-canonicalization.md`

```markdown
# Design Authority and Canonicalization

Use this when exploration has produced approved design decisions and the project needs one clear active source of truth.

## Exploration evidence and canonical authority are different

Exploration may contain:

- discarded directions;
- alternative palettes;
- visual studies;
- prototype screenshots;
- rationale;
- generated images;
- unresolved questions.

Canonical authority should contain only decisions intended to guide future work.

Do not ask engineers to infer which exploration artifact “won.”

## Define authority by concern

Avoid one giant design document that owns everything.

A healthy design knowledge architecture separates concerns such as:

```text
product/domain truth
→ product/domain specs

stable product-design principles
→ decision principles and readiness rules

selected brand/product UI direction
→ thesis, character, public/product relationship

concrete visual system
→ typography, color roles, spacing, surfaces, iconography

recurring UX patterns
→ interaction behavior and feedback conventions

asset governance
→ asset truthfulness, approval, lifecycle

route/persona map
→ surface inventory and information architecture

visual references
→ approved evidence of direction, with bounded authority
```

Exact filenames are project-specific. The separation of concerns is the reusable part.

## Prefer one active source of truth per concern

When a new design generation supersedes an old one, choose an explicit disposition:

```text
KEEP
REWRITE / ABSORB
DEMOTE TO EXPLORATION EVIDENCE
DELETE FROM ACTIVE TREE
```

Do not leave contradictory generations active and rely on readers to understand chronology.

Git history is often the correct archive for superseded canonical guidance.

Rule of thumb:

> **History is an archive; the active tree is current truth.**

## Harvest before deleting legacy guidance

Removing stale design documents is correct only after useful knowledge has been classified.

Harvest reusable principles such as:

- trust before persuasion;
- consequence clarity;
- progressive disclosure;
- loading/empty/error semantics;
- responsive information priority;
- asset truthfulness;
- non-color-only state communication.

Drop generation-specific assumptions such as:

- old brand colors;
- old exact fonts;
- prototype-specific card layout;
- obsolete shell composition;
- stale component architecture;
- temporary mock behavior.

The test is not “is this old?”

The test is:

> **Does this still express current product/design truth independent of the superseded visual generation?**

## Canonicalize only after decision evidence exists

Do not freeze exact palette, typeface, radius, icon family, or motion values merely because a document needs to feel complete.

If a decision is still materially uncertain, mark it OPEN.

Canonical documents can contain explicit open decisions. False precision is worse than a visible gap.

## Keep visual references subordinate to semantic authority

Every selected visual reference should state what it proves and what it does not prove.

Example:

```text
PROVES
- visual character
- hierarchy
- expressive intensity
- relationship between brand and product surfaces

DOES NOT PROVE
- domain semantics
- API fields
- permissions
- exact copy
- component contracts
- pixel-perfect production layout
```

This prevents reference images from overriding better semantic sources later.

## Make human authority explicit

Brand-defining decisions often require human approval because they create durable identity and product precedent.

Typical human-gate decisions include:

- selected creative direction;
- logo/wordmark;
- brand-defining palette;
- typography identity;
- key illustration/photography language;
- material changes to trust/provenance presentation;
- replacement of an established design authority generation.

An AI agent may explore, compare, synthesize, and document. It should not silently approve its own brand-defining output when the project requires human authority.

## Update routers when authority changes

Canonicalization is incomplete if the new document exists but project routers still point to old guidance.

Check:

- root agent/convention files;
- frontend/mobile scoped agent files;
- architecture docs;
- design README/authority map;
- prototype/reference guidance;
- task templates that name removed paths.

A stale router can resurrect a deleted design generation operationally.

## Do not preserve competing authority for sentimental reasons

Keeping every prior design artifact in the active tree feels safe but shifts ambiguity onto future engineers and agents.

If history is available in version control, duplication often reduces safety rather than increasing it.

## Canonicalization checklist

Before declaring a design generation ready:

```text
[ ] selected thesis/direction is human-approved where required
[ ] semantic/product truth remains owned outside visual artifacts
[ ] stable principles are separated from concrete visual tokens
[ ] concrete visual decisions have evidence, not just textual preference
[ ] selected references have bounded authority
[ ] OPEN decisions are explicit
[ ] legacy active guidance has an explicit disposition
[ ] routers point to current authorities
[ ] stale prototype/visual references are removed or demoted
[ ] engineering invariants are stated
[ ] engineering freedoms are stated
```

The last two prevent design from either under-specifying intent or over-specifying implementation.
```

---

## Proposed new file: `best-practices/product-design/design-to-engineering-handoff.md`

```markdown
# Design to Engineering Handoff

Use this after upstream product/design decisions are sufficiently approved and the next question is how to implement them safely.

The handoff boundary is:

> **Design decisions are ready; implementation strategy is not yet decided.**

Do not collapse those into one step.

## Separate design intent from implementation strategy

Upstream design should hand off:

- experience thesis;
- product/design principles;
- selected visual direction;
- concrete visual-system decisions where approved;
- behavior/pattern authority;
- asset rules;
- visual references with bounded authority;
- explicit OPEN items;
- non-negotiable semantic distinctions.

Engineering should determine:

- component decomposition;
- token representation;
- CSS/framework mechanics;
- migration sequencing;
- route-local vs shared boundaries;
- DOM structure;
- responsive mechanics;
- test architecture;
- performance strategy;
- implementation-specific loading behavior.

Design may constrain outcomes without prescribing mechanics.

## Classify design readiness before Build

For a material surface, classify:

### READY

Existing authority sufficiently defines the product/design intent.
Engineering may implement and make local mechanical choices.

### PARTIAL

The overall intent is established, but small local gaps remain.
Engineering may resolve low-consequence gaps using established principles, while surfacing any choice that creates broad precedent.

### OPEN

Material interaction, information architecture, brand, trust, or visual-system intent is unresolved.
Return upstream before canonical Build.

Rule of thumb:

> **Do not design materially OPEN product intent accidentally inside implementation code.**

## Reconcile existing implementation before migration

When applying a new design generation to an existing product, first inspect what the current implementation actually encodes.

Classify existing implementation elements:

```text
STRUCTURALLY VALUABLE
- accessibility behavior
- component semantics
- state handling
- robust layout mechanics
- tests

VISUALLY STALE
- old palette
- old typography
- old radii/shadows
- obsolete brand assets

SEMANTICALLY STALE
- outdated trust/status meaning
- prototype-driven assumptions
- invalid CTA hierarchy

UNKNOWN / NEEDS REVIEW
```

Do not preserve code merely because it exists.
Do not reset code merely because the design changed.

The correct strategy may be selective migration, targeted replacement, or aggressive reset depending on the actual coupling.

## Audit authority conflicts before coding

Architecture and agent docs may still contain assumptions from the previous design generation.

Before Build, reconcile stale references such as:

- removed design guideline paths;
- obsolete prototype authority;
- old brand colors described as canonical;
- prior action hierarchy;
- old font/token assumptions;
- component rules derived from a superseded prototype.

Treat these as documentation/authority conflicts, not as implementation precedent.

## Establish the smallest calibration surface

For broad visual-system migrations, do not redesign the entire product first.

Choose a representative slice that exercises enough of the system to expose bad assumptions.

A useful calibration slice may cover:

- shell/navigation;
- primary typography relationship;
- core surfaces and spacing;
- primary/secondary actions;
- representative content/card treatment;
- one trust/provenance state;
- responsive desktop + mobile behavior.

The slice should be large enough to judge the system and small enough to revise cheaply.

Rule of thumb:

> **Calibrate before proliferating.**

## Treat shared primitives as migration multipliers

A visual-system migration often touches broad primitives such as:

- Button;
- Input;
- Badge/status treatment;
- Progress;
- Surface/Card;
- typography tokens.

Before changing a broad primitive:

```text
classify the change
→ discover real consumers/wrappers
→ identify representative risk cases
→ change the primitive
→ verify the primitive
→ verify representative downstream consumers
```

Do not assume a foundation task grants permission to rewrite every primitive globally.

## Preserve semantic distinctions through components

A generic visual primitive should not erase product meaning.

Example:

```text
FundingProgress
OperationalMilestoneTimeline
ReportedOutcomeBlock
```

may share lower-level layout primitives while remaining semantically distinct concepts.

Do not force them into one `Progress` abstraction merely because they are all “progress-ish.”

## Implement tokens from roles, not screenshots

Translate design-system roles into implementation tokens.

Prefer:

```text
canvas
surface-warm
text-primary
text-muted
border-subtle
brand-energy
semantic-success
semantic-warning
```

over screenshot-derived names such as:

```text
yellow-from-homepage
pink-card-background
```

But token naming remains implementation-specific; projects may choose another convention.

## Verify rendered behavior, not just compilation

Material visual implementation requires real rendered feedback.

Use representative states and viewports capable of disproving the implementation.

Check:

- hierarchy;
- responsive reading order;
- long content;
- realistic numbers/data;
- state legibility;
- clipping/overflow;
- focus/keyboard behavior where relevant;
- brand consistency;
- whether semantic distinctions remain understandable without relying only on color.

Automated checks and human acceptance serve different purposes.

## Keep visual references as comparison evidence

During implementation, use approved references to evaluate:

- character;
- hierarchy;
- composition;
- expressive intensity;
- relationship between public and operational surfaces.

Do not clone incidental details when the implementation context differs.

## Do not reopen approved design casually

Engineering exploration may discover that an approved design decision is infeasible, inaccessible, inconsistent, or unexpectedly expensive.

That is valid evidence for reopening a decision.

But implementation preference alone is not sufficient reason.

Route material conflicts back to the authority owner with concrete evidence.

## Handoff checklist

Before moving from upstream design into implementation planning:

```text
[ ] active design authorities are canonical and discoverable
[ ] legacy active design authority is removed/demoted
[ ] design readiness is READY or appropriately PARTIAL
[ ] material OPEN design decisions are not hidden
[ ] visual references have bounded authority
[ ] existing architecture/docs are checked for stale design assumptions
[ ] representative calibration surface is identified
[ ] broad primitive blast radius is understood
[ ] engineering invariants are known
[ ] engineering freedoms are known
[ ] rendered + human acceptance expectations are explicit
```

If these conditions are not met, engineering may still explore implementation constraints, but should not pretend the product/design contract is settled.
```

## Rationale

This guidance is intentionally generic.

The reusable lesson is not a specific palette, typography pair, donation UX, trust vocabulary, or Kencleng artifact structure. The reusable lesson is the upstream decision architecture:

```text
product/domain truth
→ product posture and trust constraints
→ multiple creative directions
→ human-selected direction
→ representative visual proofs
→ concrete visual-system authority
→ canonicalization / legacy cleanup
→ engineering interpretation
→ implementation planning
```

This fills a real gap between Harscode's existing exploration workflow and its frontend implementation best practices.

It also complements, rather than replaces, existing React guidance:

- `react/ai-prototype-to-production-translation.md` begins once a prototype/reference already exists; this proposal covers how such references gain or do not gain authority upstream.
- `react/visual-verification.md` covers implementation verification; this proposal covers visual proof as a design-decision tool before implementation.
- `react/component-composition-and-abstraction.md` covers component structure; this proposal explicitly leaves component decomposition as engineering freedom unless product semantics require separation.
- `react/accessibility-fundamentals.md` remains implementation/accessibility authority; upstream design must avoid creating systems that depend on color alone, but does not replace implementation accessibility guidance.
- Harscode Exploration remains the engineering exploration workflow. This proposal adds domain guidance for upstream product-design work and for the boundary where approved design enters engineering exploration.

The proposed category also protects Harscode from becoming frontend-framework-centric. Product-brand and UI authority should be derivable before choosing React-specific mechanics.

A final reason to keep the guidance in three files rather than one large document is progressive disclosure:

- a team creating a new product direction needs the exploration file;
- a team cleaning up conflicting design generations needs canonicalization guidance;
- a team beginning implementation from already-approved design needs only the handoff file.

This matches the workspace's existing trigger-based best-practices routing model.

---

*After human review: update the Status above. If Accepted, merge into the target document and leave this proposal in place (don't delete it) — it serves as this folder's changelog. See `proposals/README.md` for the Protection Tier distinction and numbering convention.*
