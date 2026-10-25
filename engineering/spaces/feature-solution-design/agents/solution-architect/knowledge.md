# Solution Architect — Architecture Decision Reference

> **Type:** Agent-owned, non-binding decision knowledge, **not** a default technology stack or prescribed architecture. **Current effective project architecture, ADRs, code standards, platform constraints and accepted technical decisions take precedence**, even when they differ from the patterns below. Material Product/security/privilege contradictions go to the owning authority, not to Space preference. See [Space-wide project precedence](../../../../space-formation.md#project-standards-take-precedence-over-space-base-knowledge).

## Selection order — problem before pattern

1. Inspect the *existing* project architecture and effective standards; identify the required product outcome, consumers, latency/reliability, scale, deployment/team constraints, security/privacy, persistence and migration limits.
2. Define invariants and who owns each state/action. Separate cross-consumer commitments from local implementation freedom. Evaluate real failure modes and reversibility before selecting structures.
3. Prefer **least additional complexity that meets actual constraints**; maintain required isolation, authorization, transactional correctness and reliability. Record alternatives only where they change a material decision.
4. When selecting a new mechanism, account for operational load, observability, consistency semantics, incident recovery, data ownership and team ability to maintain it. Follow current effective standards; challenge them only for evidenced material deficiency in the assigned solution and through bounded, independently reviewed, Human-approved standards evolution.

## Structural options — alternatives at different levels

| Option | Useful when | Cost / warning |
| --- | --- | --- |
| Existing monolith | Single release boundary, shared transactional consistency, limited operational capacity | Avoid tangled dependencies and arbitrary global state |
| Modular monolith | Distinct bounded responsibilities with one deployment and explicit module interfaces | Modules are real ownership boundaries, not folders or premature plugin systems |
| Separately deployable services | Independent operational scaling, lifecycle or security boundaries justify separation | Distribution adds network failures, version compatibility, data coordination and monitoring |
| Microservices | Several independently evolving/scaling bounded domains **and** supporting operations/team capability exist | Avoid by default for a small bounded feature; eventual consistency and deployment complexity have real costs |

These are **deployment/decomposition choices**. Hexagonal, ports-and-adapters, layered, clean architecture, event-driven flows and DDD modeling address different concerns (code dependency direction, integration seams or domain modeling); they can exist *inside* a monolith or service. Never treat them as a competing single-choice menu. Select only patterns that solve an observable coupling, testability or operational problem.

## Contract and risk checks

- Specify producer/consumer operations, error/result categories, authorization decision owner, data model meaning, state transitions, consistency and version compatibility to the required implementation depth.
- Authentication does not prove resource permission; client visibility is not enforcement. Treat retries, duplicates, concurrency, lost responses, partial commits and stale reads when required by the operation.
- For atomic multi-step outcomes, identify the invariant first, then compare project-supported transaction, idempotency, compensating action or coordination alternatives. Do not invent distributed processing for a local invariant.
- Shared API source and canonical feature schema are **project-owned** by downstream concerns; Rancang O2 is proposed handoff, not authority to edit those files. A bounded, exact Human-approved Engineering *standard* change may be persisted by Architect only with separate scoped permission, re-opened effective revision and affected review.
- Surface unresolved owner choices and unsupported consumer-critical contracts instead of inventing defaults.

## Detect overengineering

Ask: What concrete requirement fails without this layer/service/event bus/abstraction? Is the risk observed or only hypothetical? What additional coordination, failure surface and migration cost does it create? Can a smaller reversible implementation meet the same invariant? If the proposed mechanism adds complexity without justified benefit, prefer the simpler project-compatible design. Do not weaken critical safeguards just to appear lean.

[Actor contract](agent.md) · [Architecture decision template](../../artifacts/templates.md#o1--shared-solution-decision)
