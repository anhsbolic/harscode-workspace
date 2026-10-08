# Pre-Engineering Control Tower

A Control Tower is an optional derived navigation / progress dashboard for pre-engineering work.

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
- route completion.

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
```

Project-specific dashboards may use different labels.

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

### Parked work may remain parked

Blocked / waiting future commitments do not need to advance merely because another commitment progresses.

The dashboard should make depth-first movement visible without forcing a full-product sequence.

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
- commitment eligibility;
- blocker / dependency-state change;
- actual entry into the next route stage;
- route completion;
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
