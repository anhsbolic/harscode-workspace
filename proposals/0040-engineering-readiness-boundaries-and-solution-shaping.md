# Define engineering readiness boundaries between pre-engineering handoff and execution-grade Techplan

**Status:** Draft
**Date:** 2026-10-09
**Protection Tier:** general
**Triggered by:** Kencleng Pilot #3 C1 first cold-start engineering run and first Techplan synthesis
**Target area:** pre-engineering / workflow boundary
**Current validation branch:** `pilot/orchestrator-v0.1-c1`

## Problem

Kencleng C1 produced a Human-approved pre-engineering handoff that a fresh engineering reader successfully consumed without reconstructing the original Product conversation.

That validates the handoff as sufficient to **begin engineering discovery**.

However, the first C1 Techplan synthesis also exposed that the current transition model can be read as though:

```text
PRE-ENGINEERING ROUTE COMPLETE
≈
ready for execution-grade Techplan synthesis
```

The C1 evidence does not support that equivalence.

The current pre-engineering contract intentionally stops before architecture, API shape, schema, transaction strategy, implementation strategy, detailed Organization field schema, and other engineering/design choices. That boundary is correct.

The current Techplan contract, by contrast, requires an execution-grade plan from which a fresh Build agent can proceed without inventing material product/domain, authority/security, architecture/ownership, interface/data, risk, or verification decisions.

For net-new cross-layer capabilities, there can therefore be a real transformation gap between:

```text
Behavioral Contract / Durable Engineering Handoff
```

and:

```text
Execution-grade Techplan
```

When that gap is not explicit, Techplan synthesis can become a mixed discovery + architecture + interface/data + security-decision + planning phase. That increases the risk of unnecessary Human/Orchestrator loops and of deliberately open engineering/design freedom being misclassified as missing Product authority.

## C1 evidence

### What succeeded

The C1 fresh engineering reader was able to reconstruct from durable artifacts:

- the bounded commitment;
- Stage 5 binding confirmed behavior;
- Stage 6 binding Experience + Engineering Requirements;
- explicit exclusions;
- engineering/design decision space;
- upstream read-only boundary;
- the fact that C1 was not yet implemented.

This supports:

```text
C1 handoff
→ ENGINEERING ENTRY READY
```

### What became unstable during Techplan synthesis

The first Techplan draft attempted to make Build executable while several solution-level concerns were still materially open.

Examples included:

- trusted person attribution / authentication implementation;
- privileged initial Owner grant boundary;
- persistence / transaction strategy;
- API and data contract;
- exact cross-layer ownership and implementation shape.

The draft also treated some deliberately open downstream choices as if they might require upstream Product resolution, including minimum Organization information / field-set concerns, even though current Stage 5/6 authority explicitly preserves detailed Organization field/form choices as design freedom and records no missing observable requirement blocking handoff.

This suggests a phase-boundary problem rather than evidence that pre-engineering should absorb technical design.

## Working conclusion

Use three distinct readiness boundaries.

### 1. Engineering Entry Ready

Owned by the upstream handoff boundary.

Meaning:

> A fresh engineering reader can understand the bounded product claim, binding behavior/requirements, authority boundaries, exclusions, and engineering/design decision space well enough to begin technical discovery without inventing Product Truth.

This is the quality target of the pre-engineering durable handoff.

It does **not** mean:

- architecture is selected;
- interface/data contracts are executable;
- security/auth implementation is decided;
- a Techplan can already be approved;
- Build can start.

### 2. Planning Ready

Owned by engineering discovery/shaping evidence, not pre-engineering.

Meaning:

> The live system, technical gaps, ownership boundaries, and material solution decisions are sufficiently understood that Techplan synthesis can produce an execution-grade contract without using the Planner as the primary architecture/interface/security discovery mechanism.

Before this boundary, material technical choices may still need bounded discovery or shaping.

The boundary should not require ordinary implementation details that Build can safely derive.

### 3. Build Ready

Owned by the approved engineering execution contract and its applicable gates.

Meaning:

> The exact current-effective Techplan is approved, applicable independent review or protected Human decisions have been satisfied, and a Build agent can execute without inventing a material product/domain, authority/security, architecture/ownership, interface/data, risk, or verification decision.

This remains distinct from overall delivery completion.

## Candidate engineering transformation model

Do not adopt these as mandatory stages yet.

Use them as candidate mechanisms to validate against real work:

```text
Behavioral Contract / Durable Engineering Handoff
        │
        │ ENGINEERING ENTRY READY
        ▼
Engineering Intake
→ frame the engineering problem, ownership, current baseline,
  required discovery, protected boundaries, and material decision classes

Engineering Exploration
→ inspect the live system, capability gaps, constraints, code/contracts,
  and current technical evidence

[Solution Shaping — conditional]
→ resolve only material architecture / interface / data / security /
  cross-layer decisions needed before execution-grade planning

        │
        │ PLANNING READY
        ▼
Techplan synthesis
→ convert sufficiently settled solution evidence into an execution-grade
  implementation / verification contract

[Independent Techplan Review when warranted]
→ fidelity / correctness check

Human approval / applicable protected approvals
        │
        │ BUILD READY
        ▼
Build
→ Code Review
→ Testing
```

## Important distinction: readiness semantics vs stage mechanism

The readiness boundaries are the primary proposal.

The exact workflow mechanism remains open.

Do not assume yet that Harscode needs two new mandatory phases.

Possible outcomes after validation include:

1. existing Exploration can be refined to own enough intake/shaping for many tasks;
2. a lightweight Engineering Intake becomes useful before Exploration;
3. Solution Shaping becomes a conditional phase only for materially under-shaped cross-layer work;
4. some combination of the above.

Choose the smallest mechanism that repeatedly solves the observed problem.

## Candidate contracts

### Engineering Intake candidate output

A bounded **Engineering Problem Frame** may make explicit:

- target commitment/task;
- current engineering baseline;
- required capabilities;
- existing vs missing capabilities;
- relevant Product / Design / Engineering authority;
- protected/security boundaries;
- external/prerequisite capability needs;
- decision ownership;
- discovery scope;
- whether current evidence is already sufficient to proceed directly to ordinary Exploration / Techplan.

It must not prematurely select architecture/API/schema merely to fill a template.

### Solution Shaping candidate output

A bounded **Solution Contract** may make explicit only the material choices Techplan must not invent, such as:

- architecture/ownership direction;
- interface/API contract;
- data/persistence contract;
- identity/authentication integration direction;
- authorization boundary;
- transaction/consistency model;
- cross-layer responsibility;
- migration/compatibility direction;
- material failure model;
- verification implications.

Not every task needs every concern.

## Relationship to current phases

### Pre-engineering

Keep the current boundary.

Do not move architecture, API, database schema, transaction design, auth implementation, or ordinary engineering solutioning upstream merely because Techplan later needs those decisions.

### Exploration

Current Exploration already provides useful technical discovery:

```text
current state
→ requirement
→ gap
→ constraints / risks
→ code anchors
```

The open question is whether its Stage 3 solutioning is sufficient for complex net-new capability shaping or whether a distinct conditional mechanism improves convergence.

### Techplan

Techplan should primarily synthesize a sufficiently settled technical direction into an execution-grade contract.

It may still resolve bounded planning choices.

It should not routinely serve as the first place where broad architecture/interface/security shape is discovered.

### Build

Build remains downstream of an Approved execution-grade contract and applicable protected gates.

Build does not absorb unresolved Planning-Ready work.

## Non-goals

This proposal does not:

- declare C1 pre-engineering incomplete;
- add post-pre-engineering Product stages;
- require more Product specification merely because engineering design is open;
- make Engineering Intake or Solution Shaping mandatory;
- prescribe one universal artifact shape;
- change the current Product / Design / Security authority model;
- weaken protected authorization gates;
- change the Build / Review / Testing correctness floor;
- normalize extra ceremony for small/reversible tasks.

## Validation questions

Use real engineering work to answer:

1. Can a fresh engineering reader distinguish Product gaps from intentionally open Design/Engineering freedom?
2. After technical discovery, can the system state exactly what remains before Planning Ready?
3. Does a conditional shaping step reduce Planner↔Human↔Orchestrator re-entry loops on net-new cross-layer capabilities?
4. Can routine/small work still move directly through existing Exploration → Techplan without extra ceremony?
5. Does Techplan quality improve when architecture/interface/security decisions arrive as durable upstream engineering evidence rather than being first discovered during synthesis?
6. Can a fresh Build agent execute an Approved Techplan without reopening material decisions?
7. Which concerns repeatedly justify a reusable Solution Contract, and which should remain task-specific evidence?

## C1 immediate handling

Treat the current C1 Techplan as validation evidence, not as proof that the proposed model is already correct.

Before continuing C1 toward Build:

- do not send deliberately open Product/design freedom upstream merely because the Draft Techplan wants a concrete implementation contract;
- preserve genuine protected authentication/privileged-authorization gates;
- classify unresolved items into Product gap vs engineering shaping vs protected Human authorization;
- use the smallest bounded engineering mechanism needed to reach Planning Ready;
- only then reconcile/revise the Techplan toward its normal review/approval gate.

## Success signal for this proposal

The refinement is useful if later real tasks can answer three questions independently:

```text
Can engineering begin?
→ Engineering Entry Ready

Can an execution-grade plan be synthesized?
→ Planning Ready

Can implementation begin safely?
→ Build Ready
```

without collapsing those states into one generic “ready for engineering” claim.
