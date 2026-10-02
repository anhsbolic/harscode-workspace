# Pilot #2 Candidate — Model Routing & Escalation

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group F checkpoint only. This document records CRTV conclusions about model and reasoning-effort routing. It does not override Human-owned runtime configuration or canonical orchestration/workflow authority.

## Purpose

Make model choice explainable and proportional without turning Harscode into a model-ranking system.

Core principles:

> Model selection is a Run-level execution routing decision, not workflow authority.

> Choose the least costly model and lowest reasoning effort that are jointly sufficient for the concrete Run.

> A stronger model must not be used to hide missing context, missing authority, bad guidance, or environment limitations.

> Fully deterministic coordination mechanics do not become low-cost AI Runs merely because a model can perform them.

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

## Run qualification precedes model routing

Model routing applies only after coordination has established that the next action
is genuinely a Participant Run.

Do not create a Run merely because an action changes durable state. Before model
selection, distinguish workflow execution that needs Role-specific capability,
material synthesis, implementation judgment, new evidence, or independent
review/verification from a deterministic reconciliation whose result already
follows completely from settled durable inputs.

A deterministic reconciliation stays outside Participant model routing when all
of the following are true:

- the governing inputs/Decision are already settled and explicit;
- there is one materially valid outcome;
- preconditions can be checked objectively;
- the allowed mutation is bounded and mechanically describable;
- a precondition mismatch can fail closed without guessing intent; and
- no Human authority, specialist judgment, independent review, or independent
  verification boundary is being replaced.

Examples include verifying an exact approved artifact revision before a permitted
lifecycle-status update, promoting an exact Human-approved candidate through a
bounded lifecycle transition, or rebuilding a genuinely derived projection from
settled owning state.

When any of the conditions above is false, do not force the action into a
mechanical path merely to avoid AI cost. Route the smallest appropriate Human,
Orchestrator-reasoning, or Participant path instead.

Deterministic mechanics remain project-defined implementation choices. This
guidance does not introduce a new canonical orchestration object, autonomous
state machine, or workflow engine.

### Deterministic coordination execution boundary

Passing Run qualification into the deterministic path authorizes only a bounded
mechanical consequence of already-settled truth. It does not transfer semantic
authorship to the Orchestrator.

The deterministic path must preserve these invariants:

1. **No new canonical object** — do not represent the action as a mechanical Run,
   reconciliation Run, synthetic Participant, new status family, or operation
   registry merely because a durable mutation occurs.
2. **Settled inputs** — all inputs that determine the result are durable,
   explicit, current-effective, and authority-valid before mutation begins.
3. **Single valid result** — one materially valid outcome follows from those
   inputs; if multiple interpretations/outputs remain materially plausible, the
   action requires reasoning/authority rather than mechanical execution.
4. **Check → mutate → verify → fail closed** — objective preconditions are checked
   before mutation, only the allowed delta is applied, objective postconditions
   are checked afterward, and mismatch stops the path without guessing intent.
5. **Bounded write authority** — only the exact surface/fields already authorized
   by settled authority/workflow lifecycle may change. A settled Decision does
   not grant broad authorship over the owning artifact.
6. **No semantic synthesis** — lifecycle metadata reconciliation, exact candidate
   promotion, mechanically entailed pointer changes, and genuinely derived
   projection refreshes may qualify; drafting requirements, choosing API/data
   semantics, deciding materiality, making implementation choices, or accepting
   risk do not.
7. **Existing provenance surfaces** — do not create a Run package, Invocation,
   Handoff, default reconciliation report, or operation log. Use Git/content
   revisions and existing authority evidence; record a normal Event/current-state
   consequence only when materially needed for reconstruction/routing.
8. **Failure routes upward** — stale/mismatched input, unexpected target revision,
   wider-than-permitted delta, ambiguity, conflicting authority, or failed
   postcondition stops mechanical execution. The Orchestrator then chooses the
   smallest appropriate Human, Orchestrator-reasoning, or Participant route; it
   must not improvise a semantic answer or auto-create a Run solely because the
   mechanical attempt failed.

A deterministic result also does not bypass protected-path/action authorization.
If a required Human/protected authorization applies, obtain it first; then perform
only the mechanically entailed mutation inside that authorized boundary.

`orchestration/run-contract.md` owns the concrete non-Run execution shape and
provenance expectations for this path. Do not build a universal reconciliation
CLI/state machine until repeated CRTV evidence shows a stable recurring
mechanism worth extracting.

## Selection order

Model routing should happen only after Run qualification succeeds.

~~~text
determine next applicable action
→ decide whether a Participant Run is actually required
   → if fully deterministic settled reconciliation: no Participant model route
   → otherwise continue
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

A routine Build may need less capability than a cross-cutting Review, while a difficult Build may need more capability than a bounded Testing Run. Work that is fully deterministic should have been removed from the Participant Run path before this comparison occurs.

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

### Human-facing escalation approval

Model approval is a Human-facing runtime decision, not a new workflow artifact or authority object. Keep Participant Run escalation distinct from Human ↔ Orchestrator pairing escalation.

For a gated Participant Run route, render a compact approval request equivalent to:

```text
[MODEL APPROVAL REQUIRED]

Run:
<RUN_ID> — <Role / Profile>

Requested:
<model> / <reasoning effort>

Why:
<bounded capability reason current approved route is insufficient>

Diagnosed as:
capability insufficiency

Not caused by:
<context / authority / guidance / environment gaps ruled out>

Scope:
this Run only

Trigger:
<material escalation trigger when applicable>

Decision:
Approve requested model/effort?
```

For Human ↔ Orchestrator pairing escalation, use a distinct request without inventing a Run:

```text
[PAIRING ESCALATION APPROVAL REQUIRED]

Concern:
<bounded coordination problem>

Current:
<default pairing model>

Requested:
<escalation model / effort when applicable>

Why:
<cross-Work-Unit / cross-authority / dependency / repeated-STALLED synthesis reason>

Scope:
this concern only

Step-down:
return to default after the concern is resolved

Decision:
Approve temporary pairing escalation?
```

Apply these invariants:

- request escalation only after diagnosis shows capability insufficiency for a Participant Run or materially harder coordination synthesis for the pairing; missing context, authority, guidance, or environment capability must be routed as their own problem;
- name the exact requested model and reasoning effort plus the bounded justification and scope; do not use model rankings, synthetic scores, speculative quality percentages, or “stronger is better” as rationale;
- if a sufficient non-gated route exists, use it rather than asking for a gated model merely as a preference;
- Participant approval is scoped to the concrete Run/model/effort use; pairing approval is scoped to the concrete coordination concern;
- approval does not mutate the Human-owned registry, remove future approval requirements, or establish a future default;
- bind Participant approval through the existing durable assignment provenance such as `MODEL_APPROVAL`; do not create `model-approval.md`, escalation receipts, or parallel approval state;
- pairing approval normally remains runtime coordination context; persist an Event/experimental evidence only when materially useful for CRTV/reconstruction;
- a rejected escalation must not silently fall back to another gated model/effort. Re-route explicitly: continue with an already-sufficient approved route, rescope/decompose, repair context/guidance/environment, or surface that no sufficient approved route currently exists;
- approval of a stronger model does not decide Session/Run identity. Continue/re-enter according to normal occurrence semantics;
- escalation is non-sticky. Future Runs perform normal fresh routing; pairing returns to its default route after the bounded concern is resolved unless another current concern independently justifies escalation.

A Human-facing `[RUN READY]` rendering is valid only after every required gated-model approval has been obtained and bound to the assignment. Do not combine “approval pending” with a card that claims dispatch readiness.

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

The Orchestrator pairing may request a concern-scoped model and/or reasoning-effort
escalation when the coordination problem itself requires materially stronger
cross-Work-Unit synthesis, cross-authority reconciliation, dependency reasoning,
repeated-STALLED diagnosis, or analysis of multiple interacting constraints.
This is appropriate when the needed evidence already exists and the hard part is
coordination synthesis; missing domain evidence should still be routed to the
appropriate Participant instead.

Any pairing escalation follows the Human-owned runtime registry and requires
explicit Human approval when that registry marks the requested route as gated.
The escalation is non-sticky: once the difficult coordination concern is
resolved, return to the default pairing route unless another current concern
independently justifies escalation.

## Independence does not imply stronger model

A fresh Code Review or Testing Session may be required for independence while using the same ordinary-capability model.

These are different decisions: fresh Session for independence versus stronger model for capability need.

## Bounded low-cost Runs after qualification

Pilot #2 may test lower-cost models on genuinely bounded Runs that still require
Participant capability or judgment, for example:

- a small targeted confirmation that requires interpretation rather than a pure
  mechanical check;
- a clearly scoped low-complexity patch;
- bounded repository analysis where current evidence must still be interpreted;
- a simple workflow-role task whose correct outcome is not mechanically
  predetermined.

Do not route fully deterministic status propagation, exact-hash reconciliation,
derived projection refresh, or similarly predetermined bookkeeping through a
Participant merely to use a cheap model. Those actions should leave the AI Run
path when their preconditions and allowed mutation are fully mechanical.

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

- deterministic settled mechanics are removed from Participant model routing rather than merely assigned a cheaper model;
- deterministic reconciliation is fail-closed, bounded to already-authorized mutation, and does not gain semantic authorship by convenience;
- routing choices are explainable from concrete Run needs;
- lower-cost models succeed on appropriately bounded judgment-requiring work;
- stronger models are used only when justified;
- model escalation does not hide authority/context/guidance/environment defects;
- gated-model Human prompts remain focused and Run-scoped;
- pairing and Participant model choices remain independent;
- pairing/Participant escalation remains concern-scoped and non-sticky after the difficult concern ends.
