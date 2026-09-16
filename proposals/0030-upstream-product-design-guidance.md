# Upstream Product Design Guidance

**Status:** Accepted — approved by Anhar
**Date:** 2026-09-16
**Protection Tier:** general
**Triggered by:** A completed upstream product-brand/UI-design cycle exposed a reusable gap: Harscode had strong engineering workflow and frontend implementation guidance, but no first-class shared guidance for moving product truth, user needs, brand intent, visual exploration, and UI/UX decisions into implementation-ready design authority.
**Target area:** root `product-design/`
**Human approval:** Anhar explicitly approved the proposal and authorized implementation in this session.
**Target file(s):**
- `product-design/README.md` — first-class upstream product-design entrypoint and boundary with domain truth, workflow, and technical best practices.
- `product-design/AGENTS.md` — routing and hard rules for the new area.
- `product-design/product-brand-and-ui-exploration.md` — reusable guidance for product-brand/UI exploration, creative directions, truth/provenance discipline, and visual proofs.
- `product-design/design-authority-and-canonicalization.md` — reusable guidance for authority ownership, legacy harvesting, one active source of truth, visual-reference boundaries, and canonicalization.
- `product-design/design-to-engineering-handoff.md` — reusable readiness, reconciliation, calibration, reset-vs-migration, and implementation-handoff guidance.
- `AGENTS.md` — route upstream product-design work to the new first-class area and protect shared guidance through the proposal mechanism.

## Gap found

Before this change, Harscode covered engineering exploration, techplanning, frontend implementation, prototype translation, responsive behavior, component boundaries, rendered verification, and testing well, but had no durable upstream discipline for questions such as:

- what product truth visual design must preserve;
- how to define product posture before choosing tokens;
- how to compare real creative directions instead of polishing one arbitrary moodboard;
- how trust/provenance/unknown states should constrain visual expression;
- when generated visual studies are useful evidence versus accidental product specifications;
- how to promote approved design work into one active source of truth;
- how to remove legacy design generations without losing reusable knowledge;
- how to distinguish design invariants from engineering implementation freedom;
- when design is READY, PARTIAL, or materially OPEN for engineering;
- when to calibrate one representative implementation slice before broad rollout.

Without this layer, implementation tends to become accidental design authority, stale prototypes retain gravity, multiple design generations remain active, and engineering silently fills material product/design gaps inside code.

## Accepted direction

The human reviewer chose a **root `product-design/` area** instead of the originally proposed `best-practices/product-design/` category.

Rationale:

- this discipline is upstream of implementation and not technology-specific;
- it owns a distinct product-to-engineering concern rather than reusable code knowledge;
- it should be discoverable alongside `workflow/` and `best-practices/`, not nested under either;
- it may later gain executable prompts or workflow integration if real usage demonstrates the need, without forcing every engineering task through a product-design phase today.

## Accepted principles

The implementation promotes these reusable rules:

- product truth before aesthetics;
- product posture before tokens;
- challenge persuasive/emotional shortcuts explicitly;
- explore multiple meaningful directions with trade-offs;
- synthesize deliberately rather than averaging contradictory directions;
- separate structural meaning from expressive style;
- treat provenance and unknown states as first-class design concerns;
- brand color is not automatically semantic color;
- progress visualizations must represent a specific kind of progress;
- visual proofs should answer decision questions and be capable of failing the direction;
- generated visuals are only as authoritative as explicitly approved;
- one active source of truth per design concern;
- harvest reusable legacy knowledge before deleting superseded authority;
- prefer Git history/archive over competing active design generations;
- canonical docs may keep material decisions explicitly OPEN rather than inventing precision;
- human approval is required where brand/product precedent is durable;
- design readiness should be classified before Build;
- design hands off invariants, engineering owns mechanics;
- existing code is evidence, not automatic design authority;
- choose reset vs migration from current implementation evidence, not aesthetic preference;
- calibrate before proliferating a new visual system;
- shared primitive changes require downstream impact analysis;
- implementation reuse must not erase semantic distinctions;
- material visual implementation requires rendered verification and, where required, human acceptance;
- reopen approved design only when implementation produces material evidence.

## Implementation note

This accepted proposal is implemented on the same branch/PR that originally carried the proposal. It remains in `proposals/` as changelog evidence after merge.

No Kencleng-specific palette, typography, brand name, UI copy, or domain semantics are promoted into Harscode. Only the reusable decision discipline is retained.
