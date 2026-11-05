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
| Engineering Project Standards (direct research concern) | [Project Standard](project-standard/README.md) · [Definition](project-standard/definition.md) · [Authority and handoff](project-standard/authority-and-handoff.md). **HUMAN CONTENT REVIEW PENDING**, not a Space. |
| Rancang Engineering Solution (zero-based research candidate) | [New Rancang entrypoint](spaces/rancang/README.md) · [13→10→8→6 contract](spaces/rancang/contracts.md) · [formation lineage](spaces/rancang/formation-lineage.md). **NOT FORMATION APPROVED / NOT RUNTIME VERIFIED**. |
| Mandatory routing and authorization rules | [Engineering AGENTS](AGENTS.md) |

**No centralized knowledge library.** A Specialist owns technical rules it needs to execute its bounded responsibility. Duplication across Specialists is acceptable when it reduces discovery and irrelevant-context costs; critical security requirements remain explicit at applicable contracts and protected-path boundaries.

Archived legacy workflows and best practices are **not** active engineering instructions. Migrate knowledge selectively into a consuming capability when it is concretely required. There is no assumption that every legacy technology guide has a currently formed Specialist consumer.

## Standing

NextJS Builder four-Agent definition is **FORMATION APPROVED / RESEARCH-ONLY** for exact immutable revision `323d8c4a19eb1ae497066ff47ce092ee19f0ab94`, by Anhar's Human decision on 2026-11-02; see [the approval record](spaces/nextjs-builder/formation-approval-2026-11-02.md). Subsequent status/navigation changes are administrative only. Its native runtime, isolation, scoped execution, mock-first delivery and real API integration remain **NOT VERIFIED / NOT RUN**; per-invocation authorization and project-owned acceptance are separate. Material definition changes require new exact-revision formation review and Human decision.

The **prior** Rancang FR-01–FR-04 formation was **FORMATION APPROVED / RESEARCH-ONLY** only for exact old-path immutable revision `6dfc4be790c526026529ed7ef397c61567809de4` (earlier revisions separately historical); see [pinned formation lineage](spaces/rancang/formation-lineage.md). The rewritten [Rancang target](spaces/rancang/README.md) and new [Project Engineering Standards concern](project-standard/README.md) do **not** inherit that approval. New Rancang formation and Harness/runtime execution remain **NOT APPROVED / NOT VERIFIED**. Research design acceptance is distinct from a new exact formation decision and from any authorized project task.

[Architecture](../ARCHITECTURE.md) · [Checklist](../REFACTOR-CHECKLIST.md)
