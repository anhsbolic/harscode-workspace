# Pilot #2 Candidate — Run Execution Envelope & Permission Routing

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group C checkpoint only. This document captures a lightweight semantic authorization model for Pilot #2. It does not replace target-repo authority, protected-path policy, or harness sandbox/approval controls.

## Purpose

Reduce routine Human permission toil without weakening protected boundaries.

Core principle:

> The Human is an authority, not an interactive shell permission broker.

A Run should carry enough execution authority context that ordinary, reversible, in-scope work can proceed without repeated Human approval prompts.

Harness permissions translate this authority; they do not create it.

## Run Execution Envelope

A Run may carry a lightweight **Execution Envelope** describing:

- authorized write scope;
- routine capability classes;
- known required target-repo commands;
- specialized verification already justified by the plan;
- actions requiring Orchestrator routing;
- actions requiring explicit Human/protected authorization.

The envelope is a semantic contract, not necessarily a machine-enforced policy file in Pilot #2.

## Candidate authorization classes

### PREAUTHORIZED

Routine, reversible, in-scope operations already justified by the active phase, approved plan, or target-repo workflow.

Typical examples when target-repo authority allows:

- read/search/list operations;
- ordinary edits inside the authorized write scope;
- `git status`, `git diff`, ordinary inspection;
- targeted unit/component/contract tests;
- target-repo-defined build/lint/test commands;
- known required final verification such as `make verify`;
- specialized verification explicitly justified by the approved Techplan/Test Focus and in scope for the current phase.

PREAUTHORIZED does not override protected paths or destructive-operation rules.

### ORCHESTRATOR_DECISION

Actions that may be valid coordination/execution choices but are not routine Participant autonomy and are not inherently Human-owned.

Candidate examples:

- broader verification than planned where scope/cost meaningfully expands;
- launching an additional Participant Run;
- selecting a different available non-gated model;
- starting an extra local runtime service needed for already-approved work;
- widening the working/verification scope within settled authority.

The Participant should route these to the Orchestrator rather than directly to the Human.

The Orchestrator must still respect project/workflow authority and may not use this class to approve a Human-owned boundary.

### HUMAN_REQUIRED

Operations whose authority remains explicitly Human/protected.

Typical examples:

- target-repo protected/Tier-0 path mutation;
- destructive persistent database/storage operation not already explicitly authorized;
- broad recursive deletion or discard-all-worktree behavior;
- force push or equivalent history-destructive action;
- production-like irreversible external action;
- model use marked as Human-approval-required;
- material new risk acceptance;
- Product/security/interface/authority decisions.

A script/wrapper does not downgrade the risk class of the underlying operation.

## Envelope shape

Pilot #2 may start with a simple human-readable block, for example:

```text
Execution Envelope

Write scope:
- backend/internal/domain/donation/**
- related tests

Routine capabilities:
- read/search/list
- ordinary edits inside write scope
- git status/diff
- target-repo build/test/lint commands
- focused verification for changed scope

Required command:
- make verify-backend

Specialized verification:
- scoped race check only when justified by Techplan Test Focus

Route to Orchestrator:
- broader verification not already planned
- additional Participant Run
- non-gated model change

Human required:
- protected-path mutation
- destructive persistent-data operation
- force push
- gated model
```

Do not expand this into an exhaustive command whitelist unless Pilot evidence shows that the harness cannot reliably operate from capability classes.

## Known required commands

When the target repo explicitly defines a required final command, include it directly.

Example:

```text
Required:
make verify
```

This prevents a Participant from treating a known mandatory routine command as an ad-hoc permission question.

Known required commands complement capability classes; they do not replace them.

## Specialized verification authorization

A specialized command is PREAUTHORIZED when:

- the approved plan/current finding already establishes the verification obligation;
- the current phase owns that evidence;
- the scope is proportional to the stated risk.

If a Participant proposes a materially broader or more expensive verification strategy than the approved obligation implies, route through ORCHESTRATOR_DECISION.

If the expansion changes material risk acceptance/authority, route through HUMAN_REQUIRED.

## Permission routing

Target interaction:

```text
Participant
├── routine/in-scope → execute
├── coordination/scope expansion → Orchestrator
└── protected/authority boundary → Human
```

Avoid:

```text
Participant
→ ask Human for every shell command
```

## Harness boundary

Harness controls such as Codex sandbox/approval settings are implementation translations of the envelope.

They must not silently:

- authorize a protected action;
- erase a required Human gate;
- expand write/network scope beyond project authority;
- reinterpret an unavailable capability as permission to skip evidence.

Pilot #2 uses Ubuntu + Ghostty + Codex CLI mechanics, but these authorization classes are candidate orchestration semantics rather than Codex-specific policy.

For the current Pilot #2 execution posture, visible Ghostty + interactive Codex CLI is the normal Participant dispatch path. If the outer sandbox blocks GUI launch or Codex runtime-local filesystem access, that is harness friction rather than a reason to change workflow authority. Request the narrow managed escalation needed and retry the visible path.

A background/non-visible launcher may be useful as a diagnostic tool, but it is not an equivalent silent fallback for a Pilot #2 Run whose execution target is visible.

## Observability

Record material permission requests and disposition when practical:

```text
Requested action:
Requested by:
Classification:
Disposition:
Reason:
Should this have been preauthorized? yes/no
```

This allows CRTV to distinguish:

- legitimate Human gates;
- useful Orchestrator coordination decisions;
- avoidable harness/agent permission friction.

## Pilot #2 diagnostic signals

Examples:

```text
Permission request:
make verify
Classification:
PREAUTHORIZED
Observed behavior:
Participant still asked Human

Interpretation:
possible invocation/harness/agent conservatism issue
```

```text
Permission request:
modify protected payment authority
Classification:
HUMAN_REQUIRED

Interpretation:
expected stop
```

Raw permission-request counts are not enough; classify the requests.

## Orchestrator boundary

The Orchestrator may:

- resolve PREAUTHORIZED vs ORCHESTRATOR_DECISION within settled authority;
- reject unnecessary scope expansion;
- route genuine Human gates.

The Orchestrator must not:

- approve protected operations reserved for Human authority;
- invent a new security/risk exception;
- become the detailed test designer;
- broaden permissions merely because a Participant is blocked.

## Failure posture

When a Run cannot proceed because of permission/sandbox limits:

1. verify the blocked action is genuinely required;
2. verify the active authority allows it;
3. classify the action;
4. request only the narrowest needed authority/capability;
5. retry the intended execution path after the boundary is resolved.

For Pilot #2 visible dispatch specifically:

- GUI/runtime-local denial may require managed escalation;
- escalation should preserve the intended Ghostty + interactive Codex execution mode;
- do not silently switch to background/non-visible execution merely because it is easier after escalation;
- if the visible path still cannot be established, record a Pilot deviation and return control to Human/Orchestrator routing.

After a visible Run is successfully dispatched, normal supervision is fire-and-forget: the Orchestrator does not poll the Participant transcript or progress. The Human reports a material problem or completion; only then does the Orchestrator diagnose or reconcile from durable artifacts.

Do not weaken verification or silently rewrite scope just to avoid the permission boundary.

## Anti-overengineering rule

Pilot #2 does not require:

- a permission DSL;
- exhaustive command-by-command policy;
- a generic multi-harness authorization engine;
- perfect machine enforcement.

Start with clear semantic classes and a simple Run envelope. Expand only when CRTV evidence shows the current representation is insufficient.
