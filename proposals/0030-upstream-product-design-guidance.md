# Upstream Product Design Guidance

**Status:** Accepted — approved by Anhar
**Date:** 2026-09-16
**Protection Tier:** general
**Triggered by:** A full upstream product-brand/UI-design cycle exposed a repeatable gap: Harscode had strong engineering workflow and frontend implementation guidance, but no generic guidance for deliberately turning product truth, user trust needs, brand intent, visual exploration, and UI/UX decisions into implementation-ready design authority before engineering begins.
**Target area:** root `product-design/`
**Target file(s):**
- `product-design/README.md` — define scope, authority boundary, and routing for upstream product-design work.
- `product-design/AGENTS.md` — provide concise routing and hard rules.
- `product-design/product-brand-and-ui-exploration.md` — generic upstream exploration guidance for product brand + UI direction.
- `product-design/discussion-facilitation.md` — guidance for conducting adaptive human/AI product-design discussions.
- `product-design/kickoff-prompt.md` — reusable non-rigid kickoff prompt for collaborative upstream product-design work.
- `product-design/design-authority-and-canonicalization.md` — rules for separating exploration evidence from canonical design authority and preventing multiple active sources of truth.
- `product-design/design-to-engineering-handoff.md` — readiness and handoff guidance for moving from approved design authority into engineering exploration/techplanning without accidentally redesigning inside implementation.
- `AGENTS.md` — route product-design work to the new first-class area.

## Gap found

Harscode previously reached product work mostly through engineering-facing concerns: feature exploration, frontend implementation, prototype translation, responsive behavior, rendered verification, component abstraction, and testing boundaries.

That left two upstream gaps.

The first was **design decision discipline**: no shared guidance covered product posture, trust requirements, creative-direction exploration, visual proofs, canonicalization, or design-readiness handoff.

The second was **discussion facilitation**: even with the right design topics, an AI agent could still behave like a questionnaire bot, passive note-taker, or option generator instead of a useful design-thinking partner.

Without explicit guidance, predictable failure modes include:

1. Implementation becomes accidental design authority.
2. Prototype or generated-visual gravity overrides product truth.
3. Teams choose visual tokens before resolving product posture and trust needs.
4. Multiple active sources of design truth coexist.
5. Visual proofs are over-read as product or route specifications.
6. Brand color silently acquires semantic meaning.
7. Different kinds of progress collapse into one generic progress treatment.
8. Unresolved product/design decisions are silently invented in code.
9. Canonicalization happens too early or too late.
10. Design-to-engineering handoff lacks an explicit boundary.
11. Product-design discussion becomes a long static questionnaire.
12. Agents record answers without interpreting their implications.
13. Agents list options without recommending a direction.
14. Agents either agree automatically or challenge performatively.
15. Long discussions accumulate context without explicit decision-state tracking.

## Accepted change

Create `product-design/` as a first-class upstream area beside `workflow/` and `best-practices/`.

The final architecture is:

```text
product/domain truth
→ product-design/
→ workflow/1-exploration
→ workflow/2-techplan
→ build / review / testing / PR
```

`product-design/` is deliberately **not** a mandatory workflow phase. Product-design authority is durable upstream context and is not recreated for every engineering task.

The area contains three kinds of guidance:

### Design reasoning

`product-brand-and-ui-exploration.md` covers product truth → posture → creative directions → synthesis → visual proofs → concrete visual-system decisions.

### Human/AI facilitation

`discussion-facilitation.md` defines how an AI agent should collaborate with the human:

```text
orient
→ find the highest-leverage unresolved question
→ ask a small number of questions
→ interpret the answer
→ challenge where meaningful
→ recommend when evidence is sufficient
→ human confirms/refines
→ update LOCKED / WORKING / OPEN / REJECTED state
→ prove visually when useful
→ canonicalize only after approval
```

`kickoff-prompt.md` packages that interaction model as a reusable starting prompt without turning it into a rigid staged workflow.

### Authority and handoff

`design-authority-and-canonicalization.md` defines how approved exploration becomes one clean source of truth.

`design-to-engineering-handoff.md` defines READY/PARTIAL/OPEN readiness, design invariants vs engineering freedoms, migration/reset reconciliation, calibration, rendered verification, and human acceptance.

## Rationale

This belongs in shared Harscode guidance because the pattern is not tied to one brand, UI stack, visual style, or product domain.

The reusable insight is the decision discipline:

```text
product truth
→ product/design reasoning
→ adaptive human/AI discussion
→ selected direction
→ representative proof
→ canonical authority
→ engineering interpretation
```

Project-specific aesthetics remain in each target project's own documentation.

The root location is intentional. Product design is neither technology-specific best-practice knowledge nor an engineering execution phase. It is upstream authority-building work that feeds the engineering workflow.

---

*Accepted by Anhar on 2026-09-16 and implemented in the same PR. This proposal remains as changelog evidence for the guidance change.*
