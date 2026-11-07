# Engineering — Foundation Research

> **Status:** WORKING / RESEARCH-ONLY. These documents are not operational Harscode `main`, a ready Space catalog, or a permission to execute.
> **Owner:** Reusable Engineering capability and delivery semantics. Concrete implementations and accepted contracts belong to the project.

## Responsibilities

Produce and verify software solutions against current project authority: solution decisions, interfaces, state, implementation, integration, security and tests. Engineering may select mechanisms but cannot change product meaning without the Product owner.

| Concern | Guidance |
| --- | --- |
| Create/revise a reusable engineering production capability | [Space formation](space-formation.md) |
| Prepare bounded work and test that delivered software matches accepted contracts | [Production and verification](production-and-verification.md) |
| Local development environment readiness (standalone Agent) | [Accepted Agent definition](agents/local-development-environment-preparation/agent.md) · [Guidance](agents/local-development-environment-preparation/guidance.md). **Human-direct local use accepted on this research branch**; not promoted to `main`. |
| NextJS Builder implementation capability (research-formed) | [NextJS Builder entrypoint](spaces/nextjs-builder/README.md) · [I/O contract](spaces/nextjs-builder/contracts.md) · [formation approval (2026-11-02)](spaces/nextjs-builder/formation-approval-2026-11-02.md). **FORMATION APPROVED / RESEARCH-ONLY** for `323d8c4a19eb1ae497066ff47ce092ee19f0ab94`; **RUNTIME NOT VERIFIED / NOT READY**. |
| Engineering Project Standards (direct research concern) | [Project Standard](project-standard/README.md) · [Definition](project-standard/definition.md) · [Authority and handoff](project-standard/authority-and-handoff.md). **ACCEPTED FOR RESEARCH** on four exact guidance blobs (A4 D2, 2026-11-05); not a Space or target-project policy. [Standing record](../experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md#a4-human-decisions-d1-and-d2--2026-11-05). |
| Rancang Engineering Solution (zero-based research definition) | [Rancang entrypoint](spaces/rancang/README.md) · [13→10→8→6 contract](spaces/rancang/contracts.md) · [formation lineage](spaces/rancang/formation-lineage.md). **FORMATION APPROVED / RESEARCH-ONLY** at exact commit `5a2964703bfddc3dc06a78091ef0b7f0220a57f0` (A4 D1); **NOT RUNTIME VERIFIED**. [External approval record](../experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md#a4-human-decisions-d1-and-d2--2026-11-05). |
| A5 Engineering Builder research; A6 closure later | [A5 umbrella research checkpoint](../experiments/org-01-reverse-lifecycle/a5-builder-research-checkpoint.md) · [Go Backend Builder I/P/O/O sub-research](../experiments/org-01-reverse-lifecycle/a5-go-backend-builder-unified-ipoo-research-definition.md) · [derivation method](../experiments/org-01-reverse-lifecycle/a5-go-backend-builder-ipoo-derivation-method.md) · [A5 horizontal coherence scope + deferred Go vertical depth](../experiments/org-01-reverse-lifecycle/a5-engineering-builder-horizontal-coherence-and-vertical-depth-debt.md). **A5 horizontal conceptual audit selected; Go vertical design and execution depth deferred, not cancelled. A6 broad cross-stage/foundation closure remains pending.** [Single status tracker](../experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md). No Go Backend Builder Space formed. |
| Mandatory routing and authorization rules | [Engineering AGENTS](AGENTS.md) |

**No centralized knowledge library.** A Specialist owns technical rules it needs to execute its bounded responsibility. Duplication across Specialists is acceptable when it reduces discovery and irrelevant-context costs; critical security requirements remain explicit at applicable contracts and protected-path boundaries.

Archived legacy workflows and best practices are **not** active engineering instructions. Migrate knowledge selectively into a consuming capability when it is concretely required. There is no assumption that every legacy technology guide has a currently formed Specialist consumer.

## Standing

NextJS Builder four-Agent definition is **FORMATION APPROVED / RESEARCH-ONLY** for exact immutable revision `323d8c4a19eb1ae497066ff47ce092ee19f0ab94`, by Anhar's Human decision on 2026-11-02; see [the approval record](spaces/nextjs-builder/formation-approval-2026-11-02.md). Subsequent status/navigation changes are administrative only. Its native runtime, isolation, scoped execution, mock-first delivery and real API integration remain **NOT VERIFIED / NOT RUN**; per-invocation authorization and project-owned acceptance are separate. Material definition changes require new exact-revision formation review and Human decision.

The **prior** Rancang FR-01–FR-04 formation was **FORMATION APPROVED / RESEARCH-ONLY** only for exact old-path immutable revision `6dfc4be790c526026529ed7ef397c61567809de4` (earlier revisions separately historical); see [pinned formation lineage](spaces/rancang/formation-lineage.md). The rewritten [Rancang research definition](spaces/rancang/README.md) received its own **separate Human D1 formation approval**, scoped to exact revision `5a2964703bfddc3dc06a78091ef0b7f0220a57f0`, and does **not** inherit old-path approval. The direct [Engineering Project Standards guidance](project-standard/README.md) separately received **A4 D2 research-content acceptance** of four exact blobs, **not** Space formation. [Both decisions are recorded in the owning research tracker](../experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md#a4-human-decisions-d1-and-d2--2026-11-05); earlier authored DRAFT/NOT APPROVED headers inside pinned guidance are historical text, not proof that subsequent Human approval never occurred. **No Rancang or other Engineering Space runtime execution is verified or implicitly authorized** by those research approvals.

[Architecture](../ARCHITECTURE.md) · [Checklist](../REFACTOR-CHECKLIST.md)
