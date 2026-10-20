# Harscode Foundation Refactor — Architecture Blueprint

> **Status:** RECONSTRUCTED RESEARCH FOUNDATION — integrated verification pending; not operational policy or a validated runtime.
> **Date:** 2026-10-20
> **Source:** `research/harscode-purpose-llm-fit@d972f9c4ec3470b0611da4286629a8659d96ab3d`
> **Operational baseline (unchanged):** `main@c762a27aee622c247c2a408d932e762076e3588c`
> **Refactor branch:** `refactor/harscode-foundation`
> **Companion:** [Foundation Refactor Checklist](REFACTOR-CHECKLIST.md)

## Objective

Rebuild Harscode's reusable guidance around clear domain ownership, experience-led product reasoning, bounded engineering capabilities, durable state, and verifiable human/agent authority. Preserve valid semantics; do not transplant legacy workflows merely because they exist.

This blueprint describes **guidance ownership**, not a mandatory linear delivery pipeline. Project-specific product truth, accepted designs, engineering contracts, and execution evidence remain in the owning project.

## Proposed root

```text
harscode-workspace/
├── README.md
├── AGENTS.md
├── AUTHORING.md
├── product/
├── design/
├── engineering/
├── collaboration/
├── harness/
└── deprecated/
```

Create subdirectories only for proven distinct responsibilities. Do not create an empty folder taxonomy for appearance. Root files should provide a compact entrypoint, authority routing, and authoring discipline without duplicating domain contracts.

## Domain ownership

| Root | Owns | Does not own |
| --- | --- | --- |
| `product/` | Reusable guidance for product authority formation, actor/experience discovery, meaningful commitments, commitment-scoped experiences, truthful product outcomes, and acceptance meaning | Target-project product facts, UI presentation mechanisms, solution architecture |
| `design/` | Experience expression: interaction design, UI/visual/brand systems, accessibility/design principles, design evidence and design handoff | Product-semantic authority, engineering implementation |
| `engineering/` | Solution design, implementation, integration, verification, engineering Space formation/definitions, Specialist-local technical knowledge | Product decisions, cross-domain Human advisory ownership, harness-native tooling mechanics |
| `collaboration/` | Human–AI pairing, source/authority verification, advisory composition, decision continuity, scoped Human approvals across domains | Space execution/dispatch, engineering production, autonomous orchestration |
| `harness/` | Harness-specific runtime translation: model/tool inventory, instructions, sandbox/permissions, session/subagent mechanics, runtime evidence | Product truth, Space capability contracts, authority to expand writes |
| `deprecated/` | Legacy material and historical evidence for controlled migration | Current authority, implicit fallback instructions, active startup guidance |

### Product / Design boundary

Product experience specifies **what a person experiences, understands, can do, and can truthfully conclude**. Design specifies **how that experience is expressed and made usable**. Experience reasoning occurs both before commitment selection (discovery) and within a selected commitment (concrete journeys, negative paths, and acceptance). A narrative must not replace binding invariants and acceptance evidence; requirement lists must not erase the narrative.

### Collaboration / Engineering / Harness boundary

Balad is the Human-facing, cross-domain **advisory** pairing role, not an Engineering Space or Orchestrator. The Human directly authorizes/invokes Engineering Spaces. Engineering owns reusable capability contracts and Specialist responsibilities. Harness owns verified execution mechanisms. Native write permission never substitutes for scoped Human authorization.

### Engineering knowledge locality

Do **not** recreate a centralized engineering best-practices repository. Selectively place relevant technical knowledge in the owning Space/Specialist package. Intentional duplication across Specialists is acceptable when it lowers routing ambiguity and irrelevant context. Track revisions by the consuming package; do not invent a shared global version requirement. Keep cross-cutting **security and authorization safeguards** at the applicable hard-rule/contract boundary so locality cannot weaken protection. Unmigrated guidance remains historical reference, not automatically effective.

### Space scope

For this research refactor, Space formation and execution target **engineering work only**, including solution design and assurance. Product and Design use Human–AI collaboration by default. This is a bounded experimental scope, **not** a permanent assertion that product/design work cannot use agent harnesses.

## Authority, approvals and evidence

1. `main` remains operational. The research branch and this refactor branch are not automatically canonical or project-ready.
2. The active repository/owning artifact and exact revision determine current authority. History, chat, copied documents and `deprecated/` are evidence only.
3. Human approval is required for material product meaning, capability formation/revision, protected writes, and consequential execution gates, subject to scoped authority.
4. **Rancang / `feature-solution-design`** has a historical research formation approval tied to the immutable definition at `1f20cf6584dba54dee17d8183c7069d7c99eafe6`, path `spaces/feature-solution-design/`. Moving or revising its files does not transfer that approval to a new path/revision.
5. C1's interim closeout is partial evidence, **not** accepted solution output, runtime readiness, complete formal closeout, or proof that product-oriented Agents can never work.
6. Every future active guidance source must state ownership, applicability, precedence, and an explicit effective/working status. No downstream consumer may infer approval from directory placement.
7. Critical security boundaries, independent verification, durable reconstructability and truthful partial/blocked results survive migration even if old mechanisms are discarded.
8. New mechanism proposals should solve observed problems. Avoid premature automation, global state machines, four parallel proposal systems, or unnecessary handoff layers.

## Legacy disposition

All legacy top-level directories were archived under `deprecated/legacy/` during **Phase 2** (checkpoint `9f8b6cb898fddce959b812748ebecfcb030efcf7`), retaining their original Git object identities. Preserve relative structure for traceability; moving files may break relative links and must not rewrite historical approval claims.

| Legacy area | Disposition and selective successor |
| --- | --- |
| `audits/` | Historical reference only; retire active copies once evidence links are retained |
| `best-practices/` | Retire central library; selectively distill into relevant Engineering Space/Specialist guidance |
| `harness-optimization/` | Rebuild applicable runtime guidance in `harness/` |
| `pairing/` | Rebuild Balad and collaboration guidance in `collaboration/`; separate CLI details into `harness/` |
| `pre-engineering/` | Reconsider fundamentals and rebuild relevant reusable semantics in `product/` |
| `product-design/` | Rebuild interaction/visual expression in `design/`; product-experience semantics belong in `product/` |
| `proposals/` | Archive old proposal history; use concern-owned changes and proportional review, no automatic per-domain proposal folders |
| `research/` | Preserve dated findings and decisions as research evidence; explicitly promote only validated, owned insights |
| `space-formation/` | Rebuild Engineering Space formation guidance in `engineering/` |
| `spaces/` | Rebuild Engineering Space definitions; maintain historical pinned formation lineage |
| `workflow/` | Curate surviving execution and assurance semantics within `engineering/`; avoid mechanical phase copy |

## Migration and publication rules

- Phase 0–1: establish an isolated branch, pin source revisions, define domain owners and checkpoints. **No legacy moves or behavioral changes.**
- Phase 2: archive the old tree, declare archival content reference-only, update root navigation, preserve links/pins and make unbuilt domains explicitly **NOT READY**. Never silently fall back to legacy.
- Later: rebuild one domain at a time, reviewing exact migrated semantics and downstream consumers. Design/readiness claims require independent evidence where consequence demands it.
- Gate each construction commit on authority/reference correctness, material semantic coverage and negative-path safeguards. Defer **independent fresh-context consumption and effectiveness validation** until after all domains are reconstructed, then test cross-domain reasoning and actual runner properties.
- Promote back to research, and eventually to `main`, **only via separate Human decisions and verified evidence**.

## Current construction standing

All five active areas are **WORKING / RESEARCH-ONLY**. Rancang under `engineering/spaces/feature-solution-design/` is a **new NOT FORMED candidate**, not a replacement approved Space; its historical formation approval remains pinned to the old revision and path. Specialist-local knowledge exists only for the candidate's scoped responsibilities; unused technology best practices remain archived until a real consumer justifies migration. No Product/Design/Collaboration runtime or Engineering Space is authorized by this branch. Independent fresh-reader, actual harness binding, usage effectiveness, and any promotion decision remain untested/deferred.

## Refactor success criteria

- Fresh sessions can locate the effective owner without chat recall or broad tree scans.
- Product guidance remains experience-led, semantically correct, and honest about unknowns.
- Cross-domain outputs have explicit producer, consumer, standing, and revision.
- Engineering Specialists can access relevant local knowledge without a centralized dependency.
- No stale or deprecated artifact is consumed as current authority.
- Material Human gates, security controls, and verification obligations remain enforceable or are marked unproven/blocked.
- Actual project consumption and execution produce reconstructable evidence; a well-organized tree alone is not a PASS.
