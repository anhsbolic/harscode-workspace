# Rancang — Coordination and Continuity (Agent-aware Revision Candidate)

> **Status:** WORKING REVISION PROPOSAL / NOT APPROVED FOR THIS REVISION / NOT RUNTIME READY. Declarative Agent composition only; no Agent is installed or invoked by this file.
> **Owner:** `feature-solution-design` internal accountability. [External I/O](contracts.md) remains the contract authority; [Engineering Space formation](../../space-formation.md) owns general formation and Human approval rules.

## Human-direct Coordinator boundary

The **Human directly addresses and authorizes** the named [Space Coordinator Agent](agents/space-coordinator.md) for an exact, bounded assignment (I4); Balad may advise the Human but has no dispatch, instruction or supervision channel to this Agent. Coordinator is an **explicit actor with its own contract**, not merely an abstract responsibility; its native runtime process/session topology remains unbound. It must:

- Check the exact **formed definition revision**, original I1–I3 provenance, I4 authorization, consumer expectations, output/state destinations and applicable actual harness readiness **before production**. A Human may request preflight within the same Coordinator interaction; preflight permission is not production authorization. If a material prerequisite fails, do not launch production responsibilities.
- Assign only scoped work; name each logical responsibility's authorized inputs, output owner, destination, source/output revisions and stop conditions. Coordinate corrections and inspect revision joins, without changing Product/Design authority or self-approving protected actions.
- Preserve independent Reviewer ownership, reconcile applicable findings with producers, check affected revisions again, assemble actual versioned output and return result, limits and decisions **to the Human directly**.

Default mode is Human-direct `supervised`: agreed material progress observations allow `continue / revise / stop` within existing scope; `continue` never means approval of Product meaning or downstream acceptance. `autonomous` requires a separate explicit Human selection for that invocation and never waives mandatory gates. Internal sequencing and number of runtime agents/sessions are harness choices, not this definition.

## Defined Agent composition and functional ownership

Rancang defines five Agent roles, including Coordinator. Each has its own [Agent-facing contract](README.md) and may be selected/combined per authorized invocation; they are not five mandatory native instances. Coordinator records exactly **which defined Agent responsibilities are assigned to which real actor/session**, each required source/permission and artifact owner, and which role combinations were made. Independent review requires meaningfully independent context and original-source access; a shared producer context cannot be labeled independent. Unselected responsibilities remain owned and must be fulfilled or explicitly marked blocked/not applicable; do not silently omit their outputs.

| Responsibility | Consumes | Owns / delivers | Does not decide |
| --- | --- | --- | --- |
| [Requirements Analyst](agents/requirements-analyst.md) | Original I1–I3 plus I4 scope | X1 original-source obligation, invariant, constraint and open-decision map | Product/Design approval or architecture |
| [Solution Architect](agents/solution-architect.md) | X1, original applicable I2/I3 and current O3 where relevant | O1 shared decisions, O2 interface/state/security/invariant contracts, and producer-owned O4 jointly with experience alignment | Product meaning or protected writes |
| [Experience Specialist](agents/experience-specialist.md) | X1, original Product/Design sources and current O1/O2 | O3 truthful actions, consequences, error/uncertain states and relevant accessibility contracts; producer-owned O4 jointly with solution production | New Product commitments, visual implementation or backend auth enforcement |
| [Solution Reviewer](agents/solution-reviewer.md) | **Original** I1–I4 plus current X1/O1–O4 revisions | Independent O5 findings on source conformance, acceptance and negative-path coverage, O4 adequacy, cross-contract consistency and consumer compatibility | Producer-owned X1/O1–O4 edits or Human acceptance |
| [Space Coordinator](agents/space-coordinator.md) | Authorized input, outputs, review findings and Human decisions | Assignments, revisioned bundle assembly, gate/state evidence and Human-facing O5 handoff metadata | Reviewer findings, solution content or invocation approval |

**O4 remains a producer deliverable** co-authored by Architect and Experience roles as applicable, with one concrete accountable artifact owner. Five **defined Agent actors** do not imply five native sessions; a justified runtime combination preserves every named responsibility and write boundary. Review independence is required; if not evidenced, report `UNVERIFIED` and do not claim completed independent review. Reviewer must inspect original sources, not only producer narratives; findings belong solely to Reviewer, return to owning producers, and materially changed edges must be re-reviewed. Technical knowledge is scoped within each Agent document, never a competing Product/Design authority.

## Consequence-based Human gates

| Boundary | Trigger and held action | Exact decision/resume evidence |
| --- | --- | --- |
| Formation (**external**) | This Agent-aware revision has no exact-revision formation approval; no invocation under this revision | Human approval of this exact revised definition, scope and owner; current v1 approval is pinned to `06371fad...` and does not transfer |
| Invocation (**external**) | No valid I4 or material preflight readiness; hold production | Human-direct project/definition refs, scope, mode, tools, writes, consumers, output/state owner and required gate authority |
| Material owner decision (**conditional**) | Unresolved Product/Design meaning, non-delegated cross-consumer contract or consequential risk changes a dependent solution; hold only that dependent work | Named owning Human, original source and affected proposed decision/output revision, explicit choice and allowed continuation |
| Protected/scope change (**conditional**) | Security, protected specification/path, privilege or authorized action scope would expand; hold that action | Exact path/action/subject revision, authorized Human and permitted tool/write scope; separate actual tool enforcement required |
| Downstream acceptance (**external**) | Bundle produced but not accepted; hold use as binding accepted solution | Human acceptance of **exact output revision** and scope, or request-changes/defer standing; no implementation authorization implied |

Routine Specialist handoffs or supervised `continue` are **not** mandatory approval gates. Missing, denied, ambiguous, stale or out-of-scope permission remains `BLOCKED` for the affected action. Independent authorized work may proceed if it does not depend on the blocked decision. A material change to input, definition, objective, protected boundary or reviewed output invalidates only affected approval/review edges; recheck the new revision and seek a new Human decision where necessary. The Coordinator may not invent approval, widen scope or bypass a gate in either mode.

## Durable state, interruption and resumption

For every authorized production invocation, the **target project** owns a minimum reconstructable record at an approved location, not a central Rancang/Harscode registry. It must identify:

- Exact formed Space definition revision; project repository/ref/SHA and original I1–I3 source revisions; I4 Human authorization, bounded scope, selected mode, allowed tools/writes and output/state owner.
- Current X1/O1–O5 artifact refs/revisions, accountable producers, executed versus proposed checks, review independence evidence/limitations, intended consumers and bundle standing.
- Each material gate's subject revision, owning decision authority, decision/absence, action held, allowed resume scope; current blocker, affected consumer, next safe action/owner, and last validated inputs.

On interruption or new session, read that record **and re-open current originals/artifact revisions**; compare against pinned inputs, approval scope and current runner readiness. Resume only unaffected authorized work from actually existing outputs; changed dependencies, missing evidence or invalidated approval block dependent work until revalidated or reauthorized. If state is missing or unreadable, report the gap—do not recreate decisions from chat memory. A record may be one concise artifact or references in existing project state; no mandated directory, status engine, scheduler or background orchestration.

Report `PARTIAL` for genuinely incomplete deliverables, `BLOCKED` for unmet authority/permission/consumer-critical preconditions and `FAILED` for unsuccessful attempted production; describe interruptions without assuming they are failures. Mark checks and reviewer independence `UNVERIFIED` when not observed. None of these declares output Human-accepted or runtime-verified. For native isolation, permissions and source access use [Harness runtime binding](../../../harness/runtime-binding.md); a written stop rule is not enforced containment.
