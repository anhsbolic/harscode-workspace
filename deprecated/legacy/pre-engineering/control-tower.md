# Pre-Engineering Control Tower

A Control Tower is an optional derived navigation / progress dashboard for pre-engineering work. A project may also keep observing the same commitment after handoff through engineering and verification, provided those lifecycle states are owned by downstream artifacts / evidence.

> **A Control Tower is never Product Authority.**

If it conflicts with an owning artifact, the owning artifact wins.

## Purpose

Use a Control Tower when visualizing current state materially improves orientation across:

- whole-product understanding;
- actor outcomes;
- representative scenarios;
- commitment frontier;
- active commitment routes;
- blockers / dependency waits;
- route completion;
- optional end-to-end commitment lifecycle state after handoff.

It should answer quickly:

- Where is the active work?
- What is complete?
- What is blocked?
- What depends on what?
- Which commitment is eligible?
- Which commitment is active?
- Which routes have reached handoff?

## Suggested visual grammar

```text
STATION / AREA
= stage / maturity area

NODE
= tracked product-work pointer

COMMITMENT
= node that can travel through the depth-first route

RAIL
= derivation / progression / dependency

SIGNAL
= readiness / progress state
```

Not every node is a commitment.

Upstream nodes may represent value loops, actor outcomes, scenarios, or other project-specific discovery artifacts.

## Suggested signals

Keep the set small unless the project proves a need for more:

```text
COMPLETE
ACTIVE
ELIGIBLE
BLOCKED
WAITING
ROUTE COMPLETE
PARKED / UNRESOLVED
```

Project-specific dashboards may use different labels. Use stronger signals only when an owning artifact / evidence source actually establishes them.

## Position rules

### Ready is not moved

An ELIGIBLE commitment remains at its current station until the next stage actually begins.

Do not visually imply:

```text
ready to move
=
already moved
```

### Route complete is not delivered

```text
ROUTE COMPLETE
= pre-engineering handoff complete

ROUTE COMPLETE
≠ implemented
≠ delivered
```

Downstream dependencies are not satisfied merely because an upstream commitment reached handoff.

When useful, show prerequisite definition / handoff state separately from real implementation / delivery state so the dashboard cannot create fake dependency closure.

### Status ownership before display

The dashboard may only reflect a readiness / dependency state that has an owning artifact or evidence source.

```text
owning artifact / evidence
→ persisted state
→ Control Tower reflects
```

Therefore:

- ELIGIBLE requires an owning readiness decision;
- BLOCKED requires an owning blocker;
- WAITING requires an owning dependency state;
- dependency rails require an owning dependency relation;
- if future work has not been re-gated / sequenced, use PARKED / UNRESOLVED or omit the stronger claim.

Do not let dashboard convenience create product sequencing truth.

### Parked work may remain parked

Future commitments do not need to advance merely because another commitment progresses.

The dashboard should make depth-first movement visible without forcing a full-product sequence.

## End-to-end lifecycle observation

A project may keep the same commitment visible after its pre-engineering route completes.

This does **not** extend the pre-engineering route or create artificial post-engineering stages.

Useful lifecycle fields may include:

```text
overall commitment
pre-engineering route
engineering
cold-start handoff validation
verified real-product behavior
overall completion
```

Rules:

- `ROUTE COMPLETE` means pre-engineering handoff complete only;
- an overall commitment may be `IN PROGRESS / NOT COMPLETE` even when no phase is currently `ACTIVE`;
- `ACTIVE` should mean work is actually being executed, not merely that the overall commitment remains unfinished;
- engineering state must come from owning engineering workflow artifacts / evidence;
- cold-start validation state must come from the independent engineering consumption attempt;
- verified real-product behavior must come from testing / delivery / real-product evidence;
- the Control Tower reflects these lifecycle facts but never creates them.

## Rail semantics

At minimum distinguish:

- derivation / lineage;
- actual progression;
- product dependency.

A dashboard may add a “ready” visual hint, but it must not look like actual progression.

## Update discipline

The correct flow is:

```text
discussion / owning artifact
→ durable decision
→ Control Tower reflects the new state
```

Never:

```text
dashboard edit
→ new Product Truth
```

Update the dashboard after meaningful state changes such as:

- stage / output completion;
- commitment eligibility or parked state established by an owner;
- blocker / dependency-state change established by an owner;
- actual entry into the next route stage;
- route completion;
- engineering lifecycle changes recorded by owning engineering artifacts;
- cold-start validation results;
- verification / real-product evidence changes;
- materially new evidence that reopens prior state.

## Content discipline

Keep the dashboard compact.

Prefer:

- node ID / short name;
- current station;
- signal;
- concise blocker / dependency reason;
- links to owning artifacts.

Keep detailed product reasoning in the owning artifact.

The dashboard is a control-tower view, not a second hand-maintained specification.
