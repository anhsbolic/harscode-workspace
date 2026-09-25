# Pilot #2 Candidate — Model Routing & Escalation

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group F checkpoint only. This document records CRTV conclusions about model and reasoning-effort routing. It does not override Human-owned runtime configuration or canonical orchestration/workflow authority.

## Purpose

Make model choice explainable and proportional without turning Harscode into a model-ranking system.

Core principles:

> Model selection is a Run-level execution routing decision, not workflow authority.

> Choose the least costly model and lowest reasoning effort that are jointly sufficient for the concrete Run.

> A stronger model must not be used to hide missing context, missing authority, bad guidance, or environment limitations.

## Runtime ownership

The model registry remains Human-owned and Orchestrator-read-only.

Generic Harscode semantics depend only on runtime metadata such as:

- available model identifier;
- coarse capability tags;
- supported reasoning efforts;
- relative cost tier;
- approval requirement.

Exact model names are target/local runtime data.

Harscode must not encode assumptions tied to a particular model generation or vendor naming scheme.

## Selection order

Model routing should happen after the Run is defined.

~~~text
determine next applicable phase
→ define Run purpose and scope
→ assign Role / Specialization
→ assess minimum capability needs
→ select sufficient available model
→ select lowest sufficient supported reasoning effort
→ check approval requirement
→ dispatch
~~~

Do not choose a model first and then shape the work around it.

## Fit-for-purpose sufficiency

Selection should consider the concrete combination of:

- Role;
- task complexity;
- uncertainty;
- material risk;
- repository breadth;
- cross-cutting reasoning needs;
- whether the Run executes a settled plan or must diagnose/reconcile harder contradictions.

Do not hardcode phase-to-model mappings.

A routine Build may need less capability than a cross-cutting Review, while a difficult Build may need more capability than a mechanical Testing Run.

## Coarse capabilities

Keep runtime capability tags coarse.

Useful classes may include:

- general;
- coding;
- repository-work;
- reasoning;
- strong-reasoning;
- architecture;
- cross-cutting-analysis.

Do not turn the registry into a specialist taxonomy for every language/framework/domain.

Run Specialization owns project/stack-specific execution identity.

## Reasoning effort is separate

Model and reasoning-effort selection are independent decisions.

Do not assume one model always runs at one fixed effort.

Use the lowest supported effort that remains sufficient for the Run.

A stronger reasoning effort does not itself create a new approval gate unless Human-owned runtime policy says so.

## Short routing rationale

Pilot #2 should preserve a brief dispatch rationale when model choice is not self-evident.

Candidate shape:

~~~text
Selected model:
<model>

Reasoning effort:
<effort>

Capability need:
<coarse capability set>

Why sufficient:
<short Run-specific reason>

Approval:
<not required | Human approval reference>
~~~

The rationale should be concise; it is dispatch evidence, not a planning essay.

## Escalation triggers

Stronger model escalation should be justified by concrete execution complexity, for example:

- cross-authority contradiction;
- complex dependency/decomposition reasoning;
- repeated STALLED diagnosis;
- material architecture ambiguity;
- high-risk cross-cutting review;
- multiple interacting unresolved constraints.

“Important task” or “stronger model is available” is not sufficient rationale.

## Diagnose before escalating

When a Run struggles, classify the cause before selecting a stronger model.

### Capability insufficiency

The Run is correctly scoped and grounded, but the current model cannot reliably handle the required reasoning/coding complexity.

→ model/effort escalation may be appropriate.

### Missing context

Required current authority/artifact/code was not supplied or discovered.

→ fix invocation/retrieval; do not mask with a stronger model.

### Guidance/routing gap

Canonical workflow/invocation semantics are ambiguous or insufficient.

→ treat as workflow/orchestration CRTV evidence.

### Authority gap

A material Product/security/interface/other Human-owned decision is unresolved.

→ route to authority; model strength cannot create missing authority.

### Environment/harness gap

Required runtime/tool capability is unavailable or misconfigured.

→ fix/route environment capability; model escalation does not solve it.

Core invariant:

~~~text
missing decision
≠
insufficient intelligence
~~~

## Escalation routing

A Participant must not silently switch to a gated/stronger model.

~~~text
Participant signal/finding
→ Orchestrator diagnosis
→ decide whether stronger model is actually the remedy
→ obtain Human approval when runtime policy requires it
→ continue/restart using the smallest sufficient route
~~~

Escalation does not automatically imply a new Work Unit.

Whether it creates a new Session or Run depends on normal Session/Run semantics and the nature of the re-entry.

## Run-scoped approval

Approval for a gated model is scoped to the concrete Run/model/effort being dispatched unless Human policy explicitly says otherwise.

Do not convert one approval into a permanent project-wide default.

A future Run performs a fresh routing decision.

## Non-sticky escalation

Stronger model use should not remain active by inertia.

After the difficult concern is resolved:

- future Participant Runs return to normal fit-for-purpose selection;
- Orchestrator pairing returns to its default model unless another current orchestration concern still justifies escalation.

Pairing escalation and Participant Run escalation remain independent.

## Orchestrator pairing vs Participant execution

Keep these separate:

~~~text
Human ↔ Orchestrator pairing model
≠
Explorer/Planner/Implementer/Reviewer/Verifier Run model
~~~

A stronger Orchestrator pairing does not upgrade Participant Runs automatically.

A stronger Participant Run does not upgrade the pairing automatically.

## Independence does not imply stronger model

A fresh Code Review or Testing Session may be required for independence while using the same ordinary-capability model.

These are different decisions: fresh Session for independence versus stronger model for capability need.

## Routine low-cost Runs

Pilot #2 may test lower-cost models on genuinely bounded routine Runs, for example:

- narrow mechanical reconciliation;
- derived report generation;
- straightforward projection/artifact update;
- small targeted confirmation;
- clearly scoped low-complexity patch.

Do not force low-cost routing merely to produce savings evidence.

Correctness remains the floor.

## Model-routing observability

When practical, retain:

- selected model;
- reasoning effort;
- capability need/rationale;
- approval evidence;
- escalation trigger;
- outcome.

If escalation occurs, preserve the original attempt/trigger rather than rewriting history as though the stronger model was selected from the start.

## No synthetic score

Pilot #2 does not introduce:

- numeric capability scores;
- model rankings;
- phase-specific mandatory models;
- automatic strongest-model fallback.

Qualitative capability matching is sufficient until real execution demonstrates otherwise.

## Reverification of fast-moving model availability

Before Pilot #2 execution, the Human/operator should verify the actual models currently available in the selected harness/runtime and update the Human-owned local registry when needed.

This is runtime maintenance, not a Harscode protocol change.

## Pilot #2 success signals

This model is working when:

- routing choices are explainable from concrete Run needs;
- lower-cost models succeed on appropriately bounded work;
- stronger models are used only when justified;
- model escalation does not hide authority/context/guidance/environment defects;
- gated-model Human prompts remain focused and Run-scoped;
- pairing and Participant model choices remain independent;
- stronger-model use does not become sticky after the difficult concern ends.
