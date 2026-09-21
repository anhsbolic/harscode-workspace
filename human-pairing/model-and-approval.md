# Model Selection and Human Approval

This document explains how a Human should understand model selection while pairing with the Orchestrator.

Canonical runtime-selection rules remain in `../orchestration/local-runtime-config.md` and the active Run contract.

## Keep two model concerns separate

```text
Human ↔ Orchestrator pairing model
!=
per-Run execution model
```

The pairing model supports routine coordination between the Human and the Orchestrator.

The per-Run execution model is selected for a specific Explorer, Planner, Implementer, Reviewer, Verifier, or other dispatched Role.

Changing one MUST NOT silently change the other.

## Pairing model

A project may define a default pairing model plus an escalation model.

Use the default for routine orchestration work such as:

- reading current state;
- routing the next action;
- updating durable orchestration artifacts;
- normal dependency/blocker reasoning;
- ordinary checkpoint handling.

Escalate only when orchestration complexity or risk materially requires it, such as:

- cross-authority conflict;
- complex dependency/decomposition reasoning;
- repeated `STALLED` diagnosis;
- material concurrency/routing decisions;
- protocol/state consistency audit.

If pairing escalation requires Human approval, do not switch silently.

## Per-Run model selection

The Orchestrator should select for **fit-for-purpose sufficiency**, not maximum intelligence.

Preferred rule:

```text
minimum justified capability need
+ Human-owned available model registry
→ sufficiently capable model
→ lowest sufficient reasoning effort
→ approval gate when required
```

Do not choose the strongest model merely because it is available.

## Human-owned registry

The available-model registry is Human-owned and Orchestrator-read-only.

The Human controls:

- which models are allowed for the project;
- capability tags;
- supported reasoning efforts;
- cost tier;
- approval-required flags.

The Orchestrator may select from the registry, but must not mutate or reinterpret it to make dispatch easier.

If a model entry appears stale or insufficient, surface that to the Human.

## Approval scope

When a selected model requires approval, approval should be scoped to the relevant Run unless the Human explicitly grants a broader policy.

Example:

```text
Model: gpt-x
Approval: APPROVED_BY_HUMAN
Scope: EXP-001 only
```

Do not carry that approval forward automatically to another Run.

## Reasoning effort

Model choice and reasoning effort are separate runtime decisions.

Use the lowest supported reasoning effort that is sufficient for the Run.

A stronger model does not imply maximum reasoning effort, and a higher reasoning effort does not automatically create a new approval gate unless project policy says so.

## Human operating pattern

When the Orchestrator proposes a gated model, the Human response can remain simple:

```text
Approve <model> untuk <Run>.
```

The Human should not need to rewrite the Run prompt or restate the capability rationale unless correcting a real mistake.

If model selection repeatedly needs Human micromanagement, treat that as orchestration/runtime-policy evidence rather than normal operation.
