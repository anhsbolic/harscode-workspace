# Harscode Foundation Refactor

> **Status: RECONSTRUCTED FOUNDATION / PENDING INTEGRATED VERIFICATION.** This branch is **not an operational replacement for `main`**. One bounded exception is the historically Human-accepted [Local Development Environment Preparation Agent](engineering/agents/local-development-environment-preparation/agent.md) for scoped local use at its **original exact revision**; the current editorial edition is **not separately exact-content reapproved** (see [Engineering standing](engineering/README.md#standing)). The broader foundation remains research-only.

## Start here

- [Architecture Blueprint](ARCHITECTURE.md) — proposed domain ownership, boundaries and migration rules.
- [Refactor Checklist](REFACTOR-CHECKLIST.md) — verified progress and remaining work.
- [Integrated Verification](FOUNDATION-VERIFICATION.md) — source-level results, open validation and authority findings.
- [Authoring Rules](AUTHORING.md) — temporary refactor writing safeguards.
- [Deprecated Reference](deprecated/README.md) — archived pre-refactor materials; **reference only**.

## Root domains

| Domain | Responsibility | Readiness |
| --- | --- | --- |
| [Product](product/README.md) | Experiment-led Product Definition I/P/O/O, Product authority/approval and subject-independent information handoff; three optional templates accepted as research authoring aids (not target-project authority) | RESEARCH REDESIGN — NOT OPERATIONAL MAIN |
| Design — [UX direct entry](design/ux/README.md) · [UI direct entry](design/ui/README.md) · [Project Standards direct entry](design/project-standard/README.md) | UX/UI and independent project-neutral standards research guidance | UX + UI SETTLED_FOR_RESEARCH; PROJECT STANDARDS EXACT GUIDANCE ACCEPTED_FOR_RESEARCH — NOT OPERATIONAL MAIN; [research standing](experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md) |
| [Engineering](engineering/README.md) | Solution, implementation, Engineering Spaces and Specialist-local knowledge | WORKING — RESEARCH ONLY |
| [Collaboration](collaboration/README.md) | Human–AI advisory collaboration and authority-aware decisions | WORKING — RESEARCH ONLY |
| [Harness](harness/README.md) | Runtime-specific execution/permission translation | WORKING — RESEARCH ONLY |
| [Deprecated](deprecated/README.md) | Frozen legacy references for selective migration | REFERENCE ONLY |

**Routing:** The five foundation domains remain research guidance, not an approved operational replacement. The accepted standalone local-environment Agent is a scoped Human-direct local-use exception **on this branch only**; its acceptance does not authorize other Engineering Spaces or promote the foundation. Historical/archived material is reference only; current operational baseline remains `main`. For **current A1–A6 research direction** (A5 horizontal **closed for conceptual research**, Go vertical depth **deferred**, A6 Part 1 **conceptually accepted**, Part 2 routing reconciled, and **full foundation closure pending**), consult the [single owning research tracker](experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md) and its [A5 scope/vertical closure criteria](experiments/org-01-reverse-lifecycle/a5-engineering-builder-horizontal-coherence-and-vertical-depth-debt.md); this root README is navigation, **not a parallel tracker**.

## Project-agnostic current-tree verification

The [project-agnosticity audit](PROJECT-AGNOSTICITY-AUDIT.md) records source-level cleanup scope, immutable provenance/approval safeguards, and the explicit exclusion of the frozen `deprecated/` archive. Historical experiment references do **not** create reusable target-project policy.

## Source and constraints

Refactor source: `research/harscode-purpose-llm-fit@d972f9c4ec3470b0611da4286629a8659d96ab3d`. Original research files remain accessible at that exact Git revision. Rancang's **original historical** formation pin `1f20cf6584dba54dee17d8183c7069d7c99eafe6` did not transfer through archival relocation; the **later formed research v3** was approved separately at `4b49d0dd0db74cf34a927cadc938ae724676a75a`. The **vNext definition** at `9663a3fa73ac0101e66764d63af8711f291a66ab` received a separate **FORMATION APPROVED / RESEARCH-ONLY** Human decision on 2026-10-25, recorded in [historical vNext exact formation approval](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/engineering/spaces/feature-solution-design/formation-approval-2026-10-25.md). The revised vNext definition `47297c6f369dad4d4e4c4f90f0e81eb0310be7cf` received separate **FORMATION APPROVED / RESEARCH-ONLY** on 2026-10-27; see [historical revised approval](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/engineering/spaces/feature-solution-design/formation-approval-2026-10-27.md). For current standing follow [Engineering routing](engineering/README.md), not root navigation as separate approval authority.

Domain reconstruction is complete **at the documentation-foundation level**, with integrated independent verification and live runtime evidence still pending. A clean source tree is not proof of an accepted Engineering Space, harness readiness, or downstream delivery.
