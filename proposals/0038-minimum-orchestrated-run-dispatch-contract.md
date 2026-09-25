# Add minimum Orchestrated Run dispatch contract for Pilot #2

**Status:** Proposed
**Date:** 2026-09-25
**Protection Tier:** general
**Triggered by:** Kencleng Orchestrator Pilot #1 CRTV review found the Run contract insufficient for dedicated-Orchestrator dispatch, authorization routing, model rationale, and same-Run Session recovery
**Target area:** orchestration
**Target file(s):**
- orchestration/run-contract.md — add minimum dispatch/recovery contract fields and ownership boundaries
- orchestration/AGENTS.md — route execution-envelope and recovery concerns through the Run contract without duplicating policy

## Gap found

The current `orchestration/run-contract.md` correctly carries identity, artifact paths, Role/Participant/Session, model, reasoning effort, and approval evidence.

Pilot #1 and the Pilot #2 design review exposed four missing contract surfaces:

1. a Participant Run does not receive a durable semantic execution/authorization envelope, so routine in-scope commands can still become ad-hoc Human permission prompts;
2. model selection is recorded as a model/effort value but not why that choice is sufficient for the concrete Run;
3. a Session may be replaced inside the same Run, but the Run contract does not name a continuation/reconstruction checkpoint;
4. phase applicability/routing may be decided by the Orchestrator, but the dispatched Run has no explicit field for the concrete applicability/routing decision that led to this Run.

Without these hooks, a dedicated Orchestrator would need to recreate critical dispatch semantics in free-form prompts, which would make Pilot #2 dependent on hidden operator behavior instead of durable contract data.

## Proposed change

### 1. Keep policy ownership outside run-contract.md

`run-contract.md` should expose dispatch values/pointers only.

Policy ownership remains:

```text
workflow phase behavior
→ workflow/

session continuation fitness
→ workflow/context-management.md

model availability/selection
→ orchestration/local-runtime-config.md

sandbox/tool permission translation
→ harness-optimization/<harness>/

product/security/protected authority
→ target project / Human Authority
```

The Run contract must not duplicate those policies.

### 2. Add concrete routing/applicability input

Add an optional/required-when-applicable dispatch field:

```text
PHASE_ROUTE
```

Semantics:

- identifies the concrete workflow phase/re-entry being dispatched and, when a normally independent phase was evaluated as not applicable, points to the durable rationale;
- does not let a Participant self-waive later phases;
- does not replace the canonical phase prompt.

For a normal Run this may be as small as:

```text
PHASE_ROUTE: Build — REQUIRED
```

or:

```text
PHASE_ROUTE: Code Review confirmation — REQUIRED
```

A NOT_APPLICABLE decision remains an Orchestrator-owned coordination fact and is recorded outside the skipped phase's nonexistent Run.

### 3. Add Run Execution Envelope

Add:

```text
EXECUTION_ENVELOPE
```

The envelope is a small semantic dispatch block or pointer that makes these concerns discoverable:

- authorized write scope;
- routine reversible capabilities already authorized by settled project/workflow authority;
- known required repository commands;
- specialized verification already justified by current plan/finding;
- actions that must route to the Orchestrator;
- Human/protected actions that still require explicit approval.

Minimum authorization classes:

```text
PREAUTHORIZED
ORCHESTRATOR_DECISION
HUMAN_REQUIRED
```

Semantics:

- PREAUTHORIZED — routine, reversible, in-scope execution already justified by settled authority;
- ORCHESTRATOR_DECISION — coordination/scope-expansion choice within settled authority;
- HUMAN_REQUIRED — protected, destructive, gated, authority-changing, or risk-acceptance boundary owned by the Human/project authority.

The envelope is semantic. Pilot #2 does not require a permission DSL or exact command whitelist.

Harness sandbox/approval settings translate this envelope; they do not create or expand authority.

### 4. Add short model-routing rationale

Keep existing:

- `SELECTED_MODEL`;
- `REASONING_EFFORT`;
- `MODEL_APPROVAL`.

Add:

```text
MODEL_ROUTING_RATIONALE
```

A concise rationale should state:

- minimum capability need;
- why selected model/effort is sufficient;
- escalation trigger when this is an escalated/gated choice.

This is dispatch evidence, not a model score or planning essay.

Before escalating to a stronger model, the Orchestrator should distinguish capability insufficiency from:

- missing context;
- guidance/routing gap;
- authority gap;
- environment/harness gap.

A stronger model must not be used as a substitute for fixing one of those other causes.

### 5. Add same-Run Session continuation hook

Add:

```text
CONTINUATION_CHECKPOINT
```

Semantics:

- optional when the Run begins in a fresh normal Session;
- required when a new Session continues an already-active Run and the normal phase handoff is not sufficient;
- points to the smallest sufficient durable state needed to reconstruct continuation.

A checkpoint should make discoverable:

- current Run identity/purpose;
- current stage/checkpoint;
- current-effective artifacts;
- settled findings/decisions relevant to continuation;
- open blockers/questions;
- relevant source anchors;
- next intended action.

A Session replacement does not create a new Run by itself.

### 6. Add Session transition metadata without turning telemetry into policy

Allow the Run record/invocation to preserve, when known:

```text
SESSION_TRANSITION: CONTINUE | FRESH
SESSION_TRANSITION_REASON: INDEPENDENCE | CONTEXT_HYGIENE | HARNESS_RECOVERY | HUMAN_REDIRECTION | other explicit reason
```

These values explain routing; they do not mechanically derive from token percentage, elapsed time, or read count.

The exact enum representation may remain lightweight during Pilot #2; the semantic distinction is the important part.

### 7. Extend durable Run record

Extend the durable Run record, when known/applicable, with:

```text
Phase route / applicability
Execution envelope or pointer
Selected model / reasoning effort
Model routing rationale / approval evidence
Session transition / continuation checkpoint
```

Do not copy the full Human-owned model registry, full permission policy, or full workflow authority into each Run.

### 8. Keep invocation augmentation bounded

Clarify that Orchestrator-generated Run invocation may:

- provide routing metadata;
- point to current-effective artifacts;
- narrow settled obligations into the Run scope;
- provide runtime/authorization/model/session dispatch data.

It may not silently invent new material Product, security, interface, architecture, risk, or verification obligations.

A newly discovered substantive obligation becomes a Finding/Decision/planning reconciliation rather than free-form invocation text.

### 9. Update orchestration/AGENTS.md routing

Add a concise hard/routing rule:

```markdown
- Orchestrated Runs receive their identity, current-effective inputs, execution envelope, model-routing evidence, and Session-continuation hooks through `run-contract.md`. These dispatch fields operationalize settled authority; they do not create new project/workflow authority.
```

## Explicitly Not Proposed

This proposal does not introduce:

- a permission DSL;
- exhaustive command whitelist;
- harness-specific Codex flags into generic Harscode;
- a launcher daemon/process supervisor;
- token/context thresholds;
- numeric model scores;
- phase-to-model mapping;
- mandatory filesystem serialization for the envelope/checkpoint;
- automatic phase skipping;
- a generic multi-harness execution framework.

Exact Pilot #2 launcher and telemetry mechanics remain candidate implementation detail.

## Rationale

A dedicated Orchestrator needs a stable boundary between:

```text
coordination decision
→ durable dispatch contract
→ Participant execution
```

Without that boundary, Human/operator prompt composition remains the hidden integration layer.

The proposed change keeps the Run contract intentionally thin:

```text
run-contract.md
→ what dispatch information must be discoverable

owner guidance
→ how that decision is made
```

This is the minimum canonical promotion needed before Pilot #2 can test automated visible dispatch without turning `run-contract.md` into a second copy of workflow, permission, model, or session policy.

---

*After human review: update the Status above. If Accepted, merge into the target document and leave this proposal in place (don't delete it) — it serves as this folder's changelog. See `proposals/README.md` for the Protection Tier distinction and numbering convention.*
