# Project Design Standards — Definition & Evolution

> **Standing:** A3 PROJECT STANDARD RESEARCH GUIDANCE — **CONTENT REVIEW PENDING** (2026-11-04). The independent `design/project-standard/` concern is a proposed Harscode research model; these newly drafted semantics are **not Human-accepted, not operational `main`, and not target-project Design Authority**.
> **Owner:** Reusable guidance for determining whether a target project should adopt, clarify, revise, supersede, or simply reuse **its own** cross-feature Design Standards. Decisions are owned and approved at the actual project scope.

## Direct entrypoint

This directory stands on its own for the Project Design Standards concern. It does **not** require `design/README.md`, parent `design/AGENTS.md`, sibling Harscode UX/UI instructions, an Orchestrator, or a formed Design Space.

| Decision need | Local owning guide |
| --- | --- |
| When to reuse or revise a project-wide Design rule, evidence/decisions/outputs and scope | [Project Standard Definition](definition.md) |
| Agent source selection, conflict handling and write/evidence constraints | [Project Standard AGENTS](AGENTS.md) |
| Project rule ownership, approval, supersession and downstream information | [Project Standard Authority & Handoff](authority-and-handoff.md) |

**Read the effective originals in the actual project** (relevant Product authority, accepted UX/UI, brand/visual/pattern/asset rules, owning project Design index, working guidance, and consumer implementation evidence), not a Harscode-generated copy of them. An index only routes; the owning original defines the real rule and standing.

## When this concern matters

Enter when a **material cross-feature / cross-surface design decision** lacks adequate accepted project rules, a real conflict/stale OPEN claim misleads a consumer, an accepted rule needs an evidence-backed change, or a repeated feature/UI pattern is a credible **candidate for project-wide precedent**.

**Skip new standardization** when accepted rules already suffice, or when the design is one bounded feature's UX flow, screen hierarchy, Hi-Fi component candidate, copy or implementation choice with no proven wider obligation. A project need not have a required minimum number of Design Standard categories, files, token tables, or component libraries.

## What is owned — and not

This concern guides **rule governance**, not a second Design Standard repository. Target projects may choose their own structure. Responsibilities may include reusable Product Design principles, UX interaction patterns, Brand/Product UI direction, visual systems, writing conventions and asset governance **when those needs actually exist**.

It **does not** select Product domain truth, feature UX flows/pages/states, feature-specific UI visual acceptance, production component APIs or CSS/framework, release scope, or technical/runtime readiness. Feature work can **propose** reusable rules but cannot silently **promote** them. Existing code, a polished screenshot, a selected-direction reference, and a working draft are different evidence types—not automatic project standards.

## Actual example, not universal policy

[Kencleng Design Standards source audit](../../experiments/org-01-reverse-lifecycle/a3-project-design-standards-kencleng-gap-matrix.md) found that the pilot project's existing five canonical Design concerns were already sufficiently structured. A stale “OPEN” list was reconciled to later accepted Visual Guidelines; a subsequent **Human-approved exact pilot revision** clarified the Design authority map and five `Owns / Does not own` boundaries. These are **project-specific observations**, not a mandate to copy Kencleng's files, visual language or branch choices to other projects.

No project Standard file, folder, template, brand system or agent is produced by using this Harscode research guide. Actual target-project writes require separate legitimate scope/permissions and approval evidence.
