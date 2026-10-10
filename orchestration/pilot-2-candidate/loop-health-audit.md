# Pilot #2 Candidate — Loop Health Audit v0

> Status: EXPERIMENTAL / PILOT #2 CANDIDATE / NON-AUTHORITATIVE  
> Scope: Human-gated diagnosis of suspected non-converging orchestration loops.  
> Validation posture: first real validation target is Kencleng Pilot #3 C1/T2.  
> This guidance does not override `orchestration/protocol-v0.1.md`, canonical `workflow/` guidance, target-project authority, or Human-owned runtime policy.

## Purpose

Harscode already requires meaningful delta for phase re-entry and says repeated unresolved causes should stop mechanical repetition and use `STALLED` handling where applicable.

The missing capability is earlier and narrower:

> detect when a sequence of individually valid Runs/reconciliations may be forming an unhealthy causal loop, then ask the Human for permission to run an independent diagnostic before another ordinary execution cycle is dispatched.

This document defines an experimental **Loop Health Audit** for that purpose.

It is not a workflow phase that every Work Unit collects. It is not continuous monitoring, a scheduler, a scoring engine, or a replacement for Orchestrator judgment. It is a Human-gated diagnostic route used only after objective trigger evidence crosses a bounded threshold.

The intended shape is:

```text
normal orchestration
        ↓
Orchestrator observes objective loop-health trigger evidence
        ↓
no audit yet; no state mutation
        ↓
Human approves diagnostic route
        ↓
fresh independent Reviewer Run
Specialization: Orchestration / Loop Health
        ↓
read-only diagnostic evidence
        ↓
HEALTHY_CONVERGENCE | LOOP_RISK | STALLED_RECOMMENDED
        ↓
Orchestrator reconciles and chooses the next route
```

## Concern ownership and relationship to existing guidance

`workflow-topology-and-applicability.md` remains the candidate owner for ordinary phase applicability, patch/re-entry routing, and normal loop interpretation such as:

```text
implementation defect → patch/re-entry
plan gap             → Techplan reconciliation
authority gap        → owning authority
same unresolved cause repeatedly → canonical STALLED handling
```

This document owns only the **escalated diagnostic mechanism** when normal loop interpretation itself is no longer sufficient to justify another ordinary route with confidence.

`orchestrator-operating-model.md` remains the cross-cutting owner of Orchestrator behavior. The Orchestrator detects candidate anomalies and recommends this audit; it does not perform the independent audit itself.

`orchestration/protocol-v0.1.md` remains authoritative for `BLOCKED`, `STALLED`, Decisions, Blockers, Runs, Events, and current-state semantics. The verdicts in this document are diagnostic outputs, not new protocol states.

## Roles

### Orchestrator — detector and router

The Orchestrator may perform lightweight trigger detection while reconstructing or reconciling normal durable state.

It may:

- group repeated Runs/Blockers by causal concern;
- compare material outcomes across re-entry cycles;
- detect durable-state contradictions or repeated recovery incidents;
- identify that the audit threshold may have been reached;
- explain the trigger evidence to the Human;
- recommend a bounded Loop Health Audit;
- after Human approval, prepare the fresh Reviewer Run;
- after the Reviewer returns, reconcile the diagnostic evidence and determine the next route.

It must not:

- declare `LOOP_RISK` or `STALLED_RECOMMENDED` as an independent verdict before the audit;
- silently set a Work Unit to `STALLED` merely because the audit threshold fired;
- diagnose the full causal loop as a substitute for an independent Reviewer;
- mutate Product, Solution, Techplan, implementation, dependency, blocker, or workflow authority while merely detecting a trigger.

### Reviewer — independent diagnostic

Use the canonical Role `Reviewer` with a bounded specialization such as:

```text
Specialization: Orchestration / Loop Health
```

Do not introduce a new canonical Role for v0.

The Reviewer performs one fresh, read-only diagnostic Run from durable evidence. It does not fix the loop, author a replacement plan, make a Product decision, accept risk, or mutate orchestration state.

### Human Authority — audit gate

The audit requires explicit Human approval before the diagnostic Run is created/dispatched.

Before approval:

- do not create an active Loop Health Audit Run;
- do not create audit verdict evidence;
- do not change Work Unit status merely because the trigger fired;
- present the bounded concern, objective trigger evidence, proposed audit scope, model/effort route if known, and no-mutation boundary.

If the Human declines, continue only through another route that remains justified by current authority/evidence. A declined audit is not itself evidence that normal execution is healthy.

## Trigger evaluation unit

Evaluate triggers against one **bounded concern**, not against the entire project and not by raw Run count.

A bounded concern should identify:

```text
affected Work Unit / task or boundary
+ causal family
+ owning concern
```

Examples:

```text
WU-C1-ENG-001 / T2 dependency acceptance / security-dependency gate
WU-X / payment retry correctness / implementation defect
WU-Y / Organization duplicate semantics / Product authority gap
```

Do not group events merely because filenames, advisory IDs, error strings, or phases look similar. Group by the reason progress cannot safely cross the same boundary.

## Trigger threshold

Recommend a Loop Health Audit when either:

```text
one HARD trigger is satisfied
```

or:

```text
at least two WARNING triggers are satisfied
for the same bounded concern
```

The threshold authorizes a recommendation to the Human. It does not prove an unhealthy loop.

### HARD H1 — repeated causal blocker after owning reconciliation

Satisfied when all are true:

1. a bounded concern ends a Run in `BLOCKED` or `STALLED`;
2. an owning reconciliation/Decision/plan change intended to address that causal concern occurs;
3. a later distinct Run again ends `BLOCKED` or `STALLED` at the same dependent boundary; and
4. the later blocker belongs to the same causal family, even if its exact error/advisory/finding identifier differs.

Example:

```text
dependency acceptance blocked
→ dependency baseline reconciled
→ fresh Build
→ dependency acceptance blocked again
```

Different advisory IDs do not make the cause different if the unresolved boundary remains “selected dependency baseline cannot yet be safely accepted.”

Do not fire H1 when the second blocker is materially unrelated to the first causal family.

### HARD H2 — routing-relevant durable current-state contradiction

Satisfied when current durable evidence cannot support one unambiguous runnable frontier because either:

- two owning current-state/authority artifacts materially disagree; or
- a previously reconciled routing-relevant contradiction recurs and again blocks safe routing.

A single stale derived projection with an obvious owning source does not by itself satisfy H2; repair it deterministically when canonical guidance permits. The trigger is for ambiguity or recurring state drift that makes another normal Run unsafe or unreliable.

Routing-relevant contradictions include disagreement about:

- current-effective authority/revision;
- active blocker;
- current Run/outcome;
- dependency satisfaction;
- current runnable frontier;
- whether a material implementation/decision is committed, accepted, or still provisional.

### HARD H3 — repeated materially equivalent Human decision request

Satisfied when:

1. a Human decision was already explicitly answered and durably recorded;
2. the same or materially equivalent question is requested again;
3. no new evidence makes the prior decision stale, out-of-scope, or inapplicable.

Do not treat normal Run-specific model approvals or genuinely new protected actions as the same decision merely because the wording resembles an earlier approval.

## Warning triggers

### WARNING W1 — planning churn around one causal family

Satisfied when the same bounded concern causes at least two material successor planning reconciliations after the original approved plan, without durable evidence that the causal family is closed.

This does not mean the revisions were wrong. It means the next ordinary cycle deserves diagnostic scrutiny before another plan/build bounce.

### WARNING W2 — repeated phase bounce

Satisfied when the same bounded concern forms at least two full alternations such as:

```text
Build → Planning → Build → Planning
Review → Build → Review → Build
Authority → Engineering → Authority → Engineering
```

and the later transition does not clearly represent a different causal class.

A normal single `Review → Patch → Review` cycle is not a warning by itself.

### WARNING W3 — repeated orchestration-recovery incidents

Satisfied when at least two distinct recovery incidents for the same bounded concern materially delay or block routing, such as:

- missing required terminal handoff;
- stale/contradictory Work Unit current state;
- stale Control Surface projection that materially misroutes work;
- current-effective artifact pointer/revision drift;
- Run lifecycle state that cannot be reconciled from required durable evidence.

Incidental documentation cleanup that does not affect routing does not count.

### WARNING W4 — repeated low-informational-delta re-entry

Satisfied when two consecutive re-entry Runs for the same bounded concern terminate without materially new implementation, verification result, authority decision, root-cause evidence, or changed premise, and still recommend returning to substantially the same unresolved route.

Do not infer low delta from small diff size. A one-line observation can be material; a large generated artifact can have almost no diagnostic value.

### WARNING W5 — owner bounce without new evidence

Satisfied when the same material question moves between ownership classes at least twice, for example:

```text
Engineering → Product/Human → Engineering → Product/Human
```

without new evidence that changes the question or makes the prior owning answer insufficient.

This is distinct from a healthy authority round-trip where a real Product Decision is made once and downstream engineering then reconciles it.

### WARNING W6 — unresolved cause disguised by identifier churn

Satisfied when successive Runs create new Finding/Blocker IDs but the audit-relevant dependent boundary and causal reason remain materially unchanged, and no durable evidence explains why the prior cause should be considered closed.

This warning exists to prevent identifier churn from hiding a repeated causal loop.

## Explicit non-triggers

Do not recommend Loop Health Audit merely because any one of these occurs:

- a single Code Review `Request changes` followed by a bounded patch;
- one Techplan revision caused by genuinely new implementation/runtime evidence;
- multiple Runs created by valid Techplan decomposition;
- fresh Sessions or Participants required by normal re-entry/independence;
- repeated Run-specific model approvals where each Run independently requires approval;
- independent Review/Testing finding a defect after Build self-check passed;
- several different blockers affecting the same task but belonging to different causal families;
- a long Work Unit history by itself;
- a large number of files or evidence artifacts by itself.

Loop count alone is not a quality metric.

## Diagnostic causal classes

The Reviewer should classify the dominant cause using the smallest useful label. These are diagnostic labels, not protocol enums.

Use existing workflow-topology meanings where applicable and extend only for audit clarity:

- `IMPLEMENTATION_DEFECT` — settled contract exists; implementation is wrong/incomplete;
- `EVIDENCE_GAP` — behavior may be correct, but required proof/harness/evidence is missing;
- `PLAN_GAP` — execution-grade planning omitted or misstated a material decision/obligation;
- `SOLUTION_GAP` — Product/domain meaning is sufficient, but a material engineering architecture/interface/data/security solution is unresolved or invalidated;
- `AUTHORITY_GAP` — material Product/domain/security/other authority meaning is missing or conflicting;
- `ENVIRONMENT_GAP` — runtime/toolchain/provider/infrastructure capability prevents credible progress;
- `ORCHESTRATION_STATE_DEBT` — durable current-state/revision/handoff/reconciliation defects are materially impairing routing;
- `PROTOCOL_GUIDANCE_GAP` — current Harscode guidance cannot route the observed case without ad-hoc invention;
- `MIXED` — two or more causes are genuinely co-dominant; explain the boundary rather than forcing one label.

Do not classify based on which phase emitted the Finding. Classify based on what must change or become known before the blocked boundary can be crossed safely.

## Audit Run qualification

After Human approval, create a new Run because the audit is a distinct independent diagnostic execution occurrence with new purpose and output evidence.

Recommended binding:

```text
PHASE_ROUTE: Orchestration Diagnostic / Loop Health Audit (experimental)
ROLE: Reviewer
SPECIALIZATION: Orchestration / Loop Health
ARTIFACT_TARGET: none
SESSION_TRANSITION: FRESH
```

The Run writes only its own evidence under `RUN_PATH`.

The audit does not create or mutate a stable workflow artifact. Its output is diagnostic evidence for Orchestrator/Human routing.

## Audit input boundary

Start from the smallest durable set sufficient to reconstruct the suspected loop.

Normally include:

1. Work Unit current state;
2. material Events for the bounded concern;
3. terminal handoffs/reports for the Runs that form the suspected cycle;
4. relevant Blocker/Decision evidence;
5. current-effective authority/plan/task/dependency artifacts directly implicated by the concern;
6. live repository evidence only when needed to resolve a state/evidence contradiction;
7. applicable Harscode loop/re-entry/current-state guidance.

Do not load by default:

- the entire repository;
- raw chat history;
- unrelated Work Units;
- all Exploration logs;
- all Product/pre-engineering artifacts;
- every historical Run merely because it exists.

If the evidence points to a possible Product/authority gap, the audit may inspect the smallest owning authority needed to determine whether the gap is real. It must not reconstruct or rewrite Product meaning from conversation history.

## Audit questions

The Reviewer must answer all of these from durable evidence:

1. **Observed cycle** — What exact sequence of Runs/Decisions/reconciliations forms the suspected loop?
2. **Causal grouping** — Which repetitions are the same causal family, and which are materially different?
3. **Net progress** — What materially new evidence, implementation, authority, or verification result did each cycle add?
4. **Prior intervention effectiveness** — Did each owning reconciliation actually address the cause it claimed to address?
5. **State coherence** — Do current durable artifacts agree on current authority, blocker, implementation acceptance, and runnable frontier?
6. **Ownership** — What class owns the remaining cause: implementation, evidence, plan, solution, authority, environment, orchestration state, or protocol guidance?
7. **Next-attempt premise** — If the currently proposed next ordinary Run executes, what premise is materially different from the previous failed cycle?
8. **Convergence expectation** — Is there an evidence-based reason to expect the next ordinary cycle to converge?
9. **Smallest intervention** — What is the least invasive action that materially improves convergence probability?
10. **Resume condition** — What observable durable condition should be established before normal execution resumes?
11. **Unaffected work** — What work can safely continue without waiting for this concern, if any?

## Net-progress discipline

The audit must distinguish activity from progress.

Potential material progress includes:

- new runtime/implementation evidence that narrows the cause;
- a new verified dependency/environment fact;
- a settled Human/authority Decision;
- a materially improved solution/plan that addresses the observed failure mode;
- an implementation correction proven against the requesting finding;
- a previously ambiguous current state becoming reconstructable;
- elimination of one causal branch so the next attempt has a narrower premise.

The following do not automatically count as material progress:

- creating a new Run ID;
- changing Participant/Session;
- regenerating a projection/report with no new semantic/evidentiary result;
- renaming the Finding/Blocker;
- restating the same recommendation;
- increasing document length;
- repeating the same failed command without a changed premise.

## Verdict contract

The Reviewer must return exactly one diagnostic verdict.

### `HEALTHY_CONVERGENCE`

Use when repetition exists but the evidence shows the process is still converging.

Expected characteristics:

- each material cycle adds genuinely new evidence or closes a causal branch;
- the unresolved cause is becoming narrower or more concrete;
- current state is coherent enough to route safely;
- the next ordinary Run has a materially changed premise;
- no repeated owner/authority bounce remains unexplained.

Typical recommendation: continue the smallest normal route already justified by current authority/evidence.

### `LOOP_RISK`

Use when the trigger is real and current evidence suggests another ordinary cycle has meaningful probability of repeating the same causal pattern, but canonical `STALLED` is not yet clearly justified.

The Reviewer must identify:

- the repeated causal pattern;
- why prior interventions did not fully address it;
- the smallest intervention before the next ordinary Run;
- the observable resume condition.

Possible interventions include, only when evidence supports them:

- bounded current-state repair;
- broader one-time dependency/environment diagnostic;
- Techplan reconciliation;
- conditional Solution Shaping re-entry for a true `SOLUTION_GAP`;
- owning Product/authority Decision;
- verification-strategy correction;
- decomposition/routing correction;
- Harscode guidance proposal when current protocol itself is the blocker.

The audit does not perform these interventions.

### `STALLED_RECOMMENDED`

Use when:

- the same root cause has survived meaningful attempts to resolve it;
- another ordinary Run lacks a materially changed premise or credible informational gain;
- continuing normal routing is likely to repeat work rather than reduce uncertainty.

This verdict is a recommendation only.

The Reviewer does not mutate Work Unit status to `STALLED`. The Orchestrator reconciles the verdict against canonical protocol/current authority and surfaces any required Human decision before changing project state.

## Required audit output

Write one Run-owned artifact, recommended path:

```text
RUN_PATH/evidence/loop-health-audit.md
```

Use this structure:

```text
# Loop Health Audit

## Scope and provenance
- Work Unit / bounded concern
- Run / Reviewer / Session
- target + workflow revision
- Human approval evidence
- inputs inspected

## Trigger evaluation
- HARD triggers satisfied
- WARNING triggers satisfied
- non-triggers explicitly excluded where relevant

## Observed cycle
- chronological causal sequence

## Causal grouping
- same-family repetitions
- materially different causes

## Net progress by cycle
- cycle
- new evidence / decision / implementation / verification
- what remained unresolved

## Current-state coherence
- current authority/revision
- blocker(s)
- accepted vs provisional implementation
- runnable frontier
- contradictions/drift

## Root-cause classification
- primary diagnostic class
- supporting reasoning/evidence

## Next-attempt premise
- what would actually be different if the proposed next normal Run executes

## Verdict
HEALTHY_CONVERGENCE | LOOP_RISK | STALLED_RECOMMENDED

## Recommended intervention
- smallest intervention only
- owner
- why this is smaller/better than another ordinary loop

## Unaffected work
- safe independent work or `none`

## Resume condition
- observable durable condition for normal routing

## Limits
- what was not inspected/proven

## Phase handoff
- Completed: Loop Health Audit
- Artifacts: this audit artifact
- Human decision: exact decision needed now or `none`
- Open / deferred: remaining concern
- Recommended next step: advisory only; Orchestrator determines project route
- Session transition: audit Run ends; any intervention is a new owning Run/Decision path
- Context pointers: smallest relevant current artifacts
```

Do not create a patch plan from the audit. Patch plans remain owned by phases that identify implementation corrections such as Code Review/Testing.

## No-mutation boundary

The Loop Health Audit is read-only with respect to project/workflow authority and implementation.

It must not:

- edit Product/pre-engineering authority;
- edit Solution Contract or promote Solution Shaping conclusions;
- edit Techplan/candidate/report;
- edit decomposition task snapshots or manifest;
- edit source code, dependencies, configuration, migrations, tests, or runtime state;
- close/open/reclassify Blockers as project truth;
- change Work Unit status/scheduling/horizon;
- mutate Work Graph dependencies;
- accept residual risk;
- grant protected implementation authorization;
- mark a dependency satisfied;
- dispatch the recommended intervention;
- declare C1/Work Unit complete.

If the audit discovers a factual contradiction in an owning artifact, report it. Do not repair it inside the audit Run.

## Human-facing recommendation contract

When the threshold is met, the Orchestrator should present a concise recommendation before any audit Run is created/dispatched.

Recommended shape:

> Aku mendeteksi Loop Health trigger pada `<bounded concern>`.
>
> Evidence: `<objective trigger evidence>`.
>
> Ini belum berarti Work Unit `STALLED` atau workflow salah. Threshold diagnostic sudah terpenuhi karena `<HARD trigger or warning combination>`.
>
> Aku merekomendasikan fresh **Loop Health Audit** yang read-only untuk membedakan healthy convergence dari repeated causal loop dan menentukan smallest intervention. Audit tidak akan mengubah Product authority, Solution Contract, Techplan, implementation, blocker state, atau acceptance.
>
> Proposed Reviewer route: `<role/specialization/model-effort if resolved>`.
>
> Approve Loop Health Audit?

Do not use alarmist language such as “workflow rusak” or “loop hell confirmed” before independent diagnosis.

## Model-routing posture

Do not hardcode a concrete model in this guidance.

Select the least costly model/effort that is sufficient for:

- cross-Run causal reconstruction;
- distinguishing authority/solution/plan/implementation/environment causes;
- detecting subtle current-state contradictions;
- evaluating meaningful delta and convergence probability.

Because the audit is cross-cutting and independent, stronger reasoning capability may be justified more often than for routine coordination. Resolve the concrete model from Human-owned runtime configuration. Any `approval_required` rule remains effective.

Human approval of the audit purpose does not silently approve an approval-required model unless the same Human response clearly approves both presented decisions.

## Orchestrator handling after verdict

The audit verdict is evidence, not routing authority.

### After `HEALTHY_CONVERGENCE`

Orchestrator:

- reconcile that the suspected loop was audited;
- keep current authority/Blockers unchanged unless separate evidence changes them;
- proceed with the smallest already-justified normal route;
- avoid repeating the audit unless materially new trigger evidence appears.

### After `LOOP_RISK`

Orchestrator:

- preserve the audit evidence;
- identify the owner of the recommended intervention;
- ask the Human only for decisions/approvals actually required;
- route the smallest intervention;
- do not continue the same ordinary cycle until the resume condition is established when the audit says doing so would repeat the cause.

### After `STALLED_RECOMMENDED`

Orchestrator:

- reconcile the recommendation against canonical `STALLED` semantics;
- surface the bounded reason and evidence to the Human when Human judgment is required;
- if `STALLED` is established, stop mechanical retries and route root-cause resolution;
- preserve unaffected runnable work when dependencies allow it.

Do not convert every `LOOP_RISK` into `STALLED`.

## Interaction with Product decisions and Solution Shaping

The audit must distinguish at least these downstream cases:

```text
settled contract violated
→ implementation patch / normal phase re-entry

material Techplan execution decision missing/wrong
→ Techplan reconciliation

Product/domain/security authority meaning missing/conflicting
→ owning Authority Decision

Product meaning sufficient but material engineering solution unresolved/invalidated
→ candidate Solution Shaping re-entry / engineering solution reconciliation
```

`Solution Shaping` remains experimental under Proposal 0040. The Loop Health Audit may recommend a bounded shaping re-entry when evidence supports `SOLUTION_GAP`; it does not make Solution Shaping canonical or mandatory.

If a material post-approval Decision changes the Approved Techplan, existing Orchestrator rules still require fresh Planner revision, applicable Review/report/Human approval, and reconciliation of affected task snapshots before dependent Build.

## Interaction with canonical `STALLED`

This audit does not replace the existing rule:

> repeated unresolved cause with no credible new delta should stop mechanical repetition and use canonical `STALLED` handling where applicable.

Instead it provides a bounded independent diagnostic before the Orchestrator/Human conclude that the threshold for `STALLED` has truly been reached.

The audit is especially useful when evidence is ambiguous between:

```text
healthy convergence through new evidence
```

and:

```text
repeated causal loop with diminishing informational return
```

## First validation case — Kencleng C1/T2

The first intended CRTV use is the current Kencleng C1/T2 dependency/security sequence.

Observed trigger candidates include:

- T2-001 terminal dependency/security blocker followed by owning Techplan reconciliation;
- T2-002 terminal dependency/security blocker at the same dependency-acceptance boundary with a different actual graph/advisory set;
- multiple successor dependency planning reconciliations;
- routing-relevant orchestration recovery/state inconsistencies around current T2 evidence and task refresh.

These observations justify the audit recommendation threshold. They do **not** predetermine the verdict.

The Reviewer must independently determine whether:

- T2-001 → T2-002 represents healthy narrowing through materially new graph evidence;
- dependency strategy is reactively rediscovering the same acceptance problem;
- orchestration-state debt is materially amplifying the apparent loop;
- the proposed next T2 attempt has a genuinely changed premise sufficient to expect convergence.

Do not use this C1 example as a permanent trigger template for unrelated tasks.

## Validation success signals

Treat v0 as useful only if real execution shows that it can:

- avoid firing on ordinary healthy Review/Patch cycles;
- detect a repeated causal pattern before another low-value Run;
- distinguish healthy convergence from actual loop risk using durable evidence;
- produce a smaller intervention than “rerun the workflow again”;
- preserve authority boundaries and independence;
- produce a clear observable resume condition;
- remain reconstructable without chat history;
- add enough diagnostic value to justify its ceremony/cost.

## Failure / simplification signals

Reconsider or remove this mechanism if CRTV shows that it:

- fires routinely on normal engineering iteration;
- mostly repeats reasoning the Orchestrator already performs adequately;
- requires broad whole-repository archaeology to be useful;
- creates a second progress/state ledger;
- becomes a mandatory phase before Build/Review/Testing;
- encourages premature `STALLED` classification;
- adds more coordination work than it saves;
- cannot produce a materially different next action from normal causal classification.

## Promotion posture

Do not promote v0 into canonical protocol based on the C1 case alone.

After real uses, evaluate separately:

1. whether trigger precision is acceptable;
2. whether Human gating is necessary/proportional;
3. whether Reviewer independence materially improves diagnosis;
4. whether the verdict vocabulary is sufficient;
5. whether `SOLUTION_GAP` re-entry needs a reusable canonical route;
6. whether any metrics deserve automation or whether human-readable trigger rules are enough.

Do not build a loop score, monitoring daemon, scheduler, state machine, or universal metrics registry until repeated CRTV evidence demonstrates a concrete problem those mechanisms solve.