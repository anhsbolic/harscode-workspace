# Pilot #2 Candidate — Participant Execution and Continuation

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Run invocation, ephemeral Participant execution, Session renewal, execution handoff, and artifact ownership for Human-Assisted Orchestration. This guide does not override project authority, canonical workflow guidance, or `orchestration/protocol-v0.1.md`.

## Purpose

Define the minimum durable contract for executing a Run through ephemeral Participants and disposable Sessions without relying on hidden conversational memory.

Core principles:

> The Run is the durable record and assignment binding for one execution occurrence of a workflow activity. The Participant is ephemeral execution capacity. The Session is a disposable runtime context.

> A Session may be disposable; an active assignment must be reconstructable.

> Assignment truth flows from Orchestrator to Participant; execution truth flows from Participant back to Orchestrator.

## Semantic boundary

- **Participant Profile** — reusable execution blueprint: capability, operating boundaries, guidance routing, and expected handoff behavior.
- **Run** — durable record and assignment binding for one execution occurrence of a workflow activity.
- **Participant** — concrete ephemeral executor identity for a Run.
- **Session** — temporary runtime/context container used by that Participant.
- **Run Invocation** — Orchestrator-owned binding artifact that tells a Participant what Run to execute.
- **Continuation Checkpoint** — Participant-owned execution-state artifact used when the same Run/Participant continues in a replacement Session.
- **Participant Execution Handoff** — Participant-owned terminal execution-outcome evidence. It may be a standalone Handoff artifact or be carried by a canonical immutable phase-owned result artifact when that artifact already contains the complete terminal outcome.

A Run is one execution occurrence of a workflow activity, consistent with the canonical protocol.

A Run may span multiple Sessions only when the same active execution occurrence continues through immediate context/runtime renewal.

A Run must not span multiple separated execution occurrences.

## Run Invocation

The Orchestrator owns the Run Invocation.

The Invocation defines the assignment; it does not duplicate durable project truth or become a giant prompt.

A minimal Invocation should make discoverable:

- **Identity** — Run ID, Work Unit ID, workflow route;
- **Assignment** — bounded objective, Run-specific scope, Run-level completion condition;
- **Execution binding** — Role, Specialization when useful, Participant ID, Participant Profile ID, pinned Profile revision;
- **Effective inputs** — current-effective input pointers, assignment-defining revisions when drift detection matters, and material resolved-guidance provenance when needed for reconstruction;
- **Repeated-Run provenance when applicable** — prior relevant execution evidence, meaningful delta, and newly effective Decision/Finding/dependency evidence;
- **Runtime route** — model, reasoning effort, routing rationale, working directory/runtime route;
- **Session posture** — initial Session identity/posture;
- **Expected handoff** — required Participant-owned completion evidence.

Run-specific scope is narrower than, and cannot override, project/profile guardrails.

Conceptually:

```text
effective execution scope
=
Profile/project boundary
∩ Run-specific scope
∩ applicable project guardrails
```

The Invocation routes to current-effective truth rather than copying Product, Techplan, contract, or guidance content unnecessarily.

Use three distinct input postures rather than treating every pointer as either
"pinned" or "latest":

1. **Assignment-defining pinned input** — exact revision/provenance that defines
   what this Run was asked to execute. Changing it materially may change the Run
   meaning.
2. **Execution baseline reference** — target repository / working-state revision
   used to detect drift or establish the starting point. It is evidence of the
   baseline, not a universal freeze of every file for the entire Run.
3. **Current-effective guidance** — ordinary project/workflow guidance resolved
   from the applicable current route unless its exact revision is itself part of
   the assignment contract.

Pin what defines what the Run means; baseline what helps detect execution drift;
resolve ordinary guidance as current-effective.

Assignment-defining material commonly includes:

- the pinned Participant Profile revision;
- approved Techplan / contract / spec revisions whose exact content defines the
  bounded assignment;
- authority Decisions whose provenance materially determines what must be true;
- a specific patch plan / review Finding / test focus when the Run exists
  specifically to act on that exact evidence.

A target repository revision such as `TARGET_REVISION` normally establishes the
execution baseline observed at dispatch. It does **not** by itself mean every
repository file is semantically pinned for the duration of the Run. Expected
Participant-owned edits, generated artifacts, or unrelated concurrent changes
must be interpreted according to scope and drift relevance.

Generic project guidance, coding conventions, reusable best practices,
current-effective Harscode workflow guidance, and concern-specific routed
guidance should normally remain current-effective rather than being
indiscriminately pinned.

Pin ordinary guidance only when reproducibility/safety requires the Participant
to execute under that exact guidance revision and changing it would materially
change the assignment meaning. Do not pin guidance merely because a commit SHA is
available.

At dispatch, the Invocation should make the posture discoverable for material
inputs. A reader should be able to tell whether a pointer is assignment-defining,
baseline-only, or current-effective without guessing.

### Current-effective guidance provenance

`current-effective` means **not semantically pinned**. It does not mean
"untracked."

When material workflow/project guidance is resolved for dispatch, capture enough
revision/provenance to reconstruct which guidance the Participant actually relied
on. This may be a repository/workflow revision plus the applicable guidance
pointers rather than a separate snapshot of every file.

Provenance capture and semantic pinning are different:

- **provenance capture** records what revision was observed/used;
- **semantic pinning** requires that exact revision to define the Run assignment.

Ordinary guidance should normally use provenance capture without semantic
pinning.

During an active Run:

- do not silently rewrite the original observed-guidance provenance;
- if a later Session or explicit re-resolution sees a newer guidance revision,
  compare the material delta before continuing;
- if the change does not alter the Run meaning, safety boundary, authority,
  required outputs, or verification obligation, the Run may continue and the
  newly observed revision should be recorded when materially useful;
- if the change materially invalidates or changes the active assignment, stop and
  reconcile before continuing; use an explicit amendment only when the assignment
  meaning remains intact, otherwise end the occurrence and use a new Run;
- a newer guidance revision must not retroactively change what an earlier
  Participant Session was instructed to do.

A replacement Session reconstructing the same Run should therefore know both:

1. the guidance provenance previously relied upon; and
2. the current-effective guidance now available.

It should check for material drift rather than blindly freezing the old guidance
or blindly adopting the new one.

Core rule:

> Semantic pinning preserves assignment meaning; provenance capture preserves
> reconstructability. Use both only where each is actually needed.

## Invocation stability

Before dispatch, the Orchestrator may edit the Invocation normally.

Once a Participant has been dispatched from it, the Invocation has crossed its reliance boundary and becomes effective assignment evidence.

After dispatch:

- non-material cleanup may use normal Git history;
- material changes to objective, scope, Role, workflow route, completion condition, Profile, or authority-relevant inputs must not be silently rewritten;
- if a material change makes the active assignment no longer valid, stop/reconcile the current Run and use a new Run for subsequent execution;
- a narrow clarification that does not change the assignment meaning may be handled as an explicit amendment when justified.

A Run must not silently become a different assignment while retaining the same identity.

## Participant Profile revision

An active Run uses the Participant Profile revision pinned at dispatch.

Profile refinement does not silently mutate an active Participant.

Future Runs/Participants may use the newer current-effective Profile.

If a Profile change is safety-critical or materially invalidates an active assignment, the Orchestrator must explicitly reconcile the active Run rather than injecting the new Profile silently.

## Participant lifecycle

A Participant is ephemeral.

Typical execution:

```text
Run becomes dispatchable
→ Orchestrator selects Profile/model/runtime
→ Orchestrator creates Invocation
→ Participant executes the Run through one or more Sessions
→ Participant writes Checkpoint when immediate Session renewal is needed
→ Participant persists terminal execution-outcome evidence when the Run occurrence ends
→ Participant terminates
→ Orchestrator reconciles Work Unit / next route
```

A Participant must not retain hidden memory across future Runs.

### Immediate Session renewal

When only the Session/runtime context changes and substantive execution is continuing immediately:

```text
Run            SAME
Participant    SAME
Profile rev    SAME
Session        NEW
```

Context renewal changes the Session, not the Run.

The replacement Session reconstructs from the base Run Invocation, the pinned Participant Profile revision, the latest Continuation Checkpoint, and current durable working state.

### Meaningful pause and workflow re-entry

A Human/authority decision made while the Participant remains actively executing does not by itself end the Run. The same Run may continue when the decision is durably recorded and the execution occurrence remains active.

When a Human decision, external dependency, blocker, or another meaningful pause causes the current execution occurrence to end:

```text
Participant persists terminal execution-outcome evidence
→ current Run execution occurrence ends
→ Orchestrator reconciles Work Unit state
→ Work Unit may become WAITING / WAITING_HUMAN / BLOCKED / PARKED as applicable
→ meaningful delta occurs
→ later workflow re-entry creates a NEW Run
```

Examples of meaningful delta include the canonical protocol cases:

- new evidence;
- authority decision;
- material plan amendment;
- different implementation approach;
- resolved dependency;
- specific defect correction.

Do not keep the old Run open across a separated execution occurrence.

Core rule:

> A Run may span multiple Sessions, but it does not span multiple execution occurrences.

> Session renewal preserves a Run; workflow re-entry creates a new Run.

### Run-boundary proportionality

A semantic distinction does not automatically require a new Run.

Within one active execution occurrence, the Participant may handle multiple
closely related Findings, questions, or Human decisions when all of the
following remain true:

- the Run objective and completion condition still mean the same thing;
- the Role and Specialization remain fit for the work;
- the Run-specific scope has not materially expanded;
- applicable authority ownership is known and Human-owned decisions remain with
  the proper owner;
- no independent review/verification boundary requires a different Participant;
- assignment-defining inputs have not changed in a way that invalidates the
  active assignment;
- the Participant/Session remains fit to continue safely.

Examples of changes that do **not** by themselves require a new Run:

- a Finding reveals a related sub-question already inside the Run objective;
- the Human resolves a bounded decision while the Participant is still actively
  executing;
- several related decision surfaces are discussed together because they share
  the same evidence and authority context;
- the Participant refines analysis within the existing objective without
  changing the workflow Role.

Create a new Run when the execution occurrence truly ends or the assignment
meaning changes materially, including when:

- objective or completion condition changes materially;
- the work crosses into a different Role or required independent Participant;
- scope expands beyond the bounded assignment;
- a meaningful pause ends the occurrence and later re-entry is required;
- new authority/evidence materially invalidates the active assignment;
- a different execution approach constitutes a meaningful new occurrence.

Do not create a new Run merely to reflect every conceptual distinction,
intermediate Finding, or Human interaction. Run boundaries exist to preserve
execution meaning and provenance, not to maximize procedural separation.

This rule does not weaken canonical re-entry semantics: once an occurrence has
ended, later re-entry is a new Run with meaningful-delta provenance.

## Repeated Run provenance

A repeated/new Run created after workflow re-entry should preserve concise provenance to the prior relevant execution evidence.

Make discoverable when applicable:

- prior relevant Run(s) and terminal execution-outcome evidence, including a standalone Handoff when one was required;
- relevant review/finding/decision/dependency evidence;
- meaningful delta that justifies re-entry;
- newly effective Decision/evidence;
- current-effective assignment inputs.

Repeated-Run provenance follows causal relevance, not merely chronological adjacency. A later Build/Patch Run may, for example, depend on an earlier Build terminal outcome plus a Reviewer Finding produced by an intervening Review Run.

The new Run receives a new Run Invocation, Participant identity, and applicable current Profile revision.

Do not introduce a cross-execution Resume Invocation for this path. The canonical repeated-Run semantics already represent the new execution occurrence.

## Session fitness and context renewal

Use the existing semantic Session fitness states:

- `HEALTHY` — substantive execution may continue normally;
- `DEGRADED` — the Session can still land safely but should not begin substantial new work;
- `UNFIT` — substantive execution should stop; recover from durable state.

Do not bind these states to a universal token percentage or runtime-specific threshold.

The Participant may detect local Session degradation and request context renewal. The Orchestrator owns reconciliation and continuation routing.

Preferred proactive transition:

```text
Session becomes DEGRADED
→ do not begin a large new atomic step
→ finish/stop at a safe boundary
→ persist meaningful working state
→ write Continuation Checkpoint
→ request replacement Session
→ Orchestrator reconciles
→ Human mechanically opens replacement Session
→ same Participant reconstructs
→ execution continues
```

Do not spend remaining context producing a giant narrative handover.

## Continuation Checkpoint

The Participant owns the Continuation Checkpoint.

The Checkpoint describes execution delta/state, not full project truth.

A minimal Checkpoint should make discoverable:

- Run ID;
- Participant ID;
- Session ID;
- Session fitness and transition reason;
- base Invocation pointer;
- pinned Participant Profile revision;
- completed durable progress;
- current execution position;
- material remaining work;
- important current-effective input pointers when needed;
- material Findings/Decisions/Blockers already affecting continuation;
- durable working-state description;
- any unverified or at-risk progress;
- smallest concrete next execution step.

Particularly important fields are:

- current position;
- unverified/at-risk progress;
- next execution step.

For implementation work, the Checkpoint should describe semantic working-state status such as modified files, partial work, test state, or known unverified changes without duplicating diffs that can be inspected directly.

Checkpoint rule:

> Checkpoint describes execution delta; durable project artifacts describe project truth.

## Checkpoint reliance and immutability

A Checkpoint is editable while being prepared.

Once a replacement Session has been dispatched from it, it has crossed its reliance boundary and becomes historical execution evidence.

After reliance:

- do not silently rewrite material content;
- correct via a later checkpoint/addendum/superseding artifact when material;
- ordinary non-material cleanup may rely on Git history.

Create Checkpoints for actual Session transitions, not on a mandatory clock/token schedule unless future CRTV evidence demonstrates the need.

Do not introduce a separate `latest-checkpoint` mirror. The applicable Checkpoint is identified by the transition/dispatch that relied upon it, not by filename recency or filesystem timestamp.

## Replacement Session reconstruction

A replacement Session should perform a short reconstruction procedure before substantive continuation:

1. read the base Run Invocation;
2. read the exact pinned Participant Profile revision;
3. read the Continuation Checkpoint explicitly relied upon by the replacement transition/dispatch;
4. inspect referenced durable working state;
5. verify that current state still matches checkpoint assumptions;
6. continue from the recorded next execution step.

If the durable state diverges materially from checkpoint assumptions, do not continue blindly.

Report the reconstruction mismatch for Orchestrator reconciliation.

## Emergency recovery

A Session may crash, become hard-exhausted, or disappear before a new Checkpoint can be written.

In that case:

- the Orchestrator must not fabricate a Participant-authored Checkpoint;
- recover from the latest durable Participant artifact and actual repository/runtime state;
- explicitly identify possible unpersisted or unverified progress;
- treat unknown progress as unknown;
- inspect/repeat work only as necessary.

A replacement Session must not reconstruct missing state from assumption.

## Participant Execution Handoff

The Participant owns the terminal execution-outcome evidence for its Run.
`Participant Execution Handoff` is the semantic contract for that terminal
outcome; it is **not** a requirement that every Run create a separate
`handoff.md` file.

When a canonical immutable phase-owned result artifact already contains the
complete terminal outcome — for example a review findings artifact, Build report,
or Testing report whose format includes the phase handoff — that artifact may
satisfy the terminal Handoff obligation directly. Create a standalone Handoff
when the Run otherwise has no natural terminal result carrier, such as a Planner
that mutates a stable Techplan artifact, a decomposition Run that mutates stable
task snapshots, or an Explorer whose durable evidence is split across multiple
files without one terminal result artifact.

For every terminated orchestrated Participant Run, whichever artifact carries
the terminal outcome MUST contain exactly one compact `## Phase handoff` with
these fixed continuation fields:

```markdown
## Phase handoff
- Outcome: ...
- Result refs: ...
- Findings: ...
- Decision requests: ...
- Blockers: ...
- Open / unverified: ...
- Recommended continuation: ...
- Context refs: ...
```

The fields have these semantics:

- **Outcome** — how this Run occurrence ended. It describes execution occurrence
  completion, not Work Unit completion, milestone promotion, or downstream
  authorization. Use concise occurrence semantics such as `COMPLETED`,
  `STALLED`, or `FAILED` when they fit the actual result.
- **Result refs** — materially relevant terminal/stable outputs plus exact
  reconstructable revision/content identity when later reliance requires it.
  This is not a touched-file inventory. Do not copy stable workflow artifacts
  into the Run merely to make the handoff self-contained.
- **Findings** — material observed problems/evidence raised by the Run, preferably
  by pointer to their durable owning evidence when one exists. Use `none` when
  there are no material Findings.
- **Decision requests** — unresolved material authority choices that require an
  identified owner/Human decision. Keep these distinct from Findings and
  Blockers; use concise exact asks or durable Decision pointers rather than a
  narrative restatement.
- **Blockers** — active inability to progress, including the exact affected scope
  and safe unaffected work when known. A scoped blocker must not be silently
  widened to the whole Work Unit.
- **Open / unverified** — material uncertainty, deferred obligations, or evidence
  not yet established. Open or unverified work is not automatically a Blocker.
- **Recommended continuation** — Participant-local advice about the smallest
  useful continuation. It is a routing signal, not routing authority: the
  Participant must not create the next Run, mark a Work Unit complete, promote a
  milestone, or authorize downstream work through this field.
- **Context refs** — only the smallest durable pointers needed to reopen the
  relevant evidence or authority context. Do not reproduce the full source set.

The structured Phase Handoff is an index into durable evidence, not a second
phase report. It should not duplicate detailed test output, full findings, copied
plans, source diffs, complete logs, or the full content of stable workflow
artifacts that already have their own semantic owner.

The Orchestrator may reconcile or route directly from the structured Phase
Handoff when it is sufficient. When it is not sufficient, selectively open the
referenced durable evidence rather than requiring every terminal handoff to
restate it.

Do not add a generic `Session transition` field to this terminal shape. Once the
terminal outcome is persisted, the Run occurrence ends; later Session/Run posture
is Orchestrator routing. This does not remove portable non-orchestrated phase
handoff wording from canonical workflow prompts.

Under normal execution, one Run should produce exactly one durable terminal
execution-outcome carrier. Checkpoints may be multiple, but the terminal outcome
closes the Run occurrence. Do not create both a complete phase-owned terminal
report and a second standalone Handoff that merely repeats the same outcome.
Material corrections after the relied-upon terminal outcome should
amend/supersede rather than silently rewrite it.

Historical Runs and terminal artifacts remain valid evidence and require no
backfill solely to adopt this structured shape.

## Human decisions during Participant execution

A Human/authority decision made inside a Participant Session is valid decision evidence when it is explicit enough and recorded durably with appropriate provenance.

The Participant records the decision as observed evidence; it does not become the authority owner.

The Orchestrator later reconciles the decision into durable project/orchestration state without requiring duplicate approval merely because the decision occurred inside a Participant Session.

If the Decision changes authority-owned project truth, the terminal outcome is
still only decision evidence and routing context. It must not become the
canonical authority artifact by convenience. The Orchestrator must route or
verify the corresponding authority-artifact update before dependent completion
is claimed.


## Orchestrator reconciliation after terminal outcome

A terminal execution outcome is Participant evidence, not the resulting Work Unit state.

The Orchestrator should perform a coordination-level reconciliation before updating canonical Work Unit state:

1. validate Run / Work Unit / Participant identity and provenance;
2. compare the terminal outcome against the Run Invocation objective, scope, completion condition, and expected outputs;
3. resolve material durable evidence rather than relying on narrative claims alone;
4. reconcile Findings, Decisions, Blockers, and their ownership/routing implications, including the exact affected scope and safe unaffected work for each active Blocker;
5. when a Blocker is scoped, preserve unrelated runnable work rather than expanding the Blocker to the whole Work Unit without evidence;
6. when multiple Decisions appear to overlap or conflict, compare their authority
   areas, owners, scopes, effective contexts, and explicit supersession before
   deciding which is current-effective; do not infer global recency precedence;
7. for each material Decision, determine whether it is execution-local or
   authority-affecting, and if authority-affecting identify the owning
   authoritative artifact/surface that must be updated;
8. check whether material authority or assignment-defining input drift invalidates the completion claim;
9. verify that required authority synchronization is complete before treating
   dependent work as fully reconciled;
10. evaluate the Work Unit completion/workflow consequence;
11. update canonical Work Unit current state and record material Events;
12. recompute the runnable frontier.

Reconciliation checks coordination sufficiency. It must not turn the Orchestrator into a hidden Reviewer or Verifier. When technical correctness or independent verification remains unresolved, route the appropriate Role.

Do not create a default `reconciliation-report.md` or second reconciliation state store. The durable consequence should be expressed through the existing Work Unit current state, Events, Blockers/Decisions/Work Graph updates, and the next Run Invocation when applicable.

### Repeated Run gate and STALLED

A terminal `PARTIAL` result does not by itself justify a repeated Run.

Before dispatching repeated execution, the Orchestrator should be able to identify the prior relevant execution evidence, the meaningful delta, and why another execution occurrence is now justified.

If work can safely continue as the same execution occurrence, use Session replacement rather than ending the Run.

If the original Run was materially oversized, the runtime route was unfit, or decomposition was wrong, correct that cause before creating the next Run so the correction itself provides meaningful delta.

If a repeated Run intended to resolve cause X ends with materially the same unresolved cause X, treat that as a strong signal for canonical `STALLED`: stop mechanical repetition, diagnose, and reroute. `STALLED` is a loop-breaker, not a synonym for difficult work.

## Session termination, Run end, and Work Unit continuation

Session termination and Run termination are distinct.

```text
Session termination
= runtime context ends

Run termination
= one workflow execution occurrence ends

Work Unit continuation
= Orchestrator reconciles whether the bounded outcome needs more work
```

A Session may terminate while the same Run continues only through immediate Session replacement.

When the Participant persists the terminal execution outcome for the occurrence, that Run ends.

If the Work Unit is not yet complete because it is waiting on a Human/owner decision, blocked by a dependency, or requires later re-entry, the Orchestrator updates canonical Work Unit execution/scheduling state rather than keeping the Run alive.

Later execution uses a new Run with meaningful-delta provenance.

Run result/reconciliation remains Orchestrator-owned; Participants do not self-promote Work Unit or milestone state.

## Artifact ownership

Semantic ownership for this candidate model:

- Run Invocation — Orchestrator;
- Continuation Checkpoint — Participant;
- Participant terminal execution outcome / Handoff evidence — Participant; the carrier may be standalone or embedded in the canonical immutable phase-owned result artifact;
- Session Transition / recovery record — Orchestrator;
- Run dispatch/result chronology — Orchestrator;
- Work Unit execution/scheduling state / Work Graph / Control Surface — Orchestrator;
- Human Decision — Human/authority owner; evidence may be recorded by Participant;
- Learning Proposal — proposer/Participant;
- Project Learning promotion — applicable Human/review authority.

One durable artifact should have one semantic owner. Avoid shared-write artifacts whose provenance becomes ambiguous.

A workflow artifact does not become Run-owned merely because a Run modifies it.
When the orchestrated-run overlay binds a stable `ARTIFACT_TARGET`, that stable
artifact retains its workflow semantic identity while the Run package records
only the occurrence-specific assignment and evidence.

### Run artifact proportionality

Do not create a Run-local artifact merely because a conceptual stage, Finding,
or discussion step occurred.

The durable Run package should contain the **smallest set of artifacts that
preserves the execution meaning and evidence required for correctness**.

The following remain required when applicable:

- a discoverable Run Invocation before dispatch;
- the canonical phase-owned artifact(s) required by the active workflow route,
  stored according to their own lifecycle/ownership semantics rather than copied
  into the Run merely for provenance;
- a Continuation Checkpoint only when an actual Session transition/recovery
  requires one;
- one durable terminal execution-outcome carrier when the occurrence ends; use a
  standalone Handoff only when an existing canonical phase-owned result artifact
  does not already carry the complete terminal outcome;
- additional evidence artifacts when the evidence is materially useful for
  verification, decision provenance, review, reconstruction, or later reuse.

Do not collapse or remove a canonical phase-owned artifact just to reduce file
count. For example, a stable Planner-owned Techplan, Reviewer-owned review
evidence, or Verifier-owned testing evidence keeps its own semantic ownership
when the workflow requires it.

Do not create a default `launch-record.md`. The Invocation owns assignment and
dispatch binding; the terminal outcome owns execution result; material dispatch
chronology belongs in Events/coordination state when needed. Add another durable
Run-local provenance file only when it owns material information that those
surfaces cannot reconstruct.

Do not copy version-controlled source files into a Run-local `baseline/` tree by
default. Prefer the observed target revision plus relevant paths and exact
content revision/hash when needed. Preserve an explicit source snapshot only
when the exact input would otherwise not be durably reconstructable, such as an
ephemeral or non-versioned external source.

Do not persist a `source-delta.patch` or equivalent patch snapshot by default
when the delta is reconstructable from durable source revisions/working state.
Persist an exact patch only when the patch itself becomes a relied-upon object or
when its source state cannot otherwise be reconstructed safely.

Extra Run-local evidence files should earn their existence by owning material
information that would otherwise become ambiguous, hard to verify, or expensive
to reconstruct. Avoid splitting one coherent body of evidence into multiple
files only to mirror internal reasoning stages.

Likewise, do not duplicate the same conclusion across several Run-local files
for convenience. Prefer pointers plus a concise summary when the durable truth
already exists elsewhere.

Artifact count is not a success metric. Reconstructability, provenance,
verification quality, and semantic ownership are.

## Session Transition record

The Participant records why/how execution can safely continue through its Checkpoint.

The Orchestrator records the coordination transition itself.

A minimal Session Transition record may identify:

- prior Session;
- replacement Session;
- reason;
- Continuation Checkpoint;
- Participant;
- Run.

Once the transition has occurred, the transition record is historical event evidence.

## Reliance boundary and mutation rule

Use a lightweight generic reliance-boundary rule:

> If nobody has materially relied on the artifact yet, edit it normally. If execution or reconciliation has materially relied on it, preserve provenance and amend/supersede material changes rather than silently rewriting history.

Examples:

- Invocation reliance boundary — Participant dispatch;
- Checkpoint reliance boundary — replacement Session dispatch;
- terminal outcome/Handoff reliance boundary — Orchestrator reconciliation;
- Decision reliance boundary — downstream work acts on it;
- Learning Proposal reliance boundary — review/promotion begins.

Do not create correction artifacts for trivial formatting/typo changes unless they affect material interpretation.

Material corrections may use simple relations such as:

- `AMENDS`;
- `SUPERSEDES`.

Do not build a heavyweight artifact-versioning system unless repeated CRTV evidence requires it.

## Run evidence discoverability

Storage/layout remains project-defined, but durable resolution must be deterministic.

Candidate invariants:

- given an active Work Unit, its current Run must be discoverable from current orchestration state;
- given a Run ID, its Invocation and available execution evidence must be deterministically resolvable without conversational memory or heuristic repository search;
- workflow chronology comes from Runs and Events, not filesystem ordering;
- repeated-execution lineage comes from durable causal provenance and meaningful delta, not chat recall.

A project-local layout such as:

```text
<orchestration-root>/
  runs/
    <run-id>/
      invocation.md
      checkpoints/          # only when an actual Session transition requires them
      <phase-result>        # when the Run owns a natural immutable result artifact
      handoff.md            # only when terminal outcome is not carried elsewhere
```

is a valid candidate implementation pattern, not a universal Harscode filesystem law. A stable workflow artifact bound through `ARTIFACT_TARGET` may live outside the Run package entirely.

Do not introduce a Run Registry merely because a Participant Profile Registry exists. A separate Run Registry is justified only if deterministic Run-ID resolution cannot be achieved cleanly through the project’s existing orchestration layout/indexing.

## Human-Assisted dispatch

The Human remains a mechanical dispatcher in Pilot #2. Human-facing dispatch is a compact rendering of an already-prepared durable assignment; it is not a new project artifact, orchestration object, or authority surface. The Run Invocation remains the durable assignment contract.

For a new Run that is fully ready for mechanical dispatch, the Orchestrator should render a compact Human-facing card equivalent to:

```text
[RUN READY]

Purpose:
<one bounded sentence explaining why this Run exists now>

Run:
<RUN_ID> — <Role / Participant Profile>

Model:
<model> / <reasoning effort>

Cwd:
<working directory>

Invocation:
<durable Invocation pointer>

Kickoff:
<one copy-pasteable instruction>

Report back:
<terminal carrier pointer/result or exact scoped discrepancy to return>
```

Add Session posture only when the Human needs it to dispatch correctly. `Purpose` is orientation, not a second summary of Work Unit history, decisions, source pointers, execution envelope, or completion conditions. Those remain in the durable Invocation.

The Human must be able to recover model/reasoning, cwd, Invocation, kickoff, and expected report-back behavior without opening the Invocation. `Report back` is explicit so the Human does not have to infer what to bring back to the Orchestrator when execution ends or stops on a discrepancy.

A `[RUN READY]` card means all dispatch prerequisites owned outside the Human's mechanical launch action are already satisfied. If the selected model/effort requires explicit Human approval under the runtime registry, obtain that approval first; only then render the Run as ready. Do not combine a still-pending gated-model approval with a card that claims dispatch readiness.

For immediate Session renewal of the same active Run, use a distinct compact rendering equivalent to:

```text
[SESSION REPLACEMENT READY]

Continue:
<RUN_ID> — <same Participant / pinned Profile>

Checkpoint:
<exact Continuation Checkpoint pointer>

Cwd:
<working directory>

Kickoff:
<one reconstruction-and-continue instruction>

Report back:
<next checkpoint or terminal carrier>
```

Do not restate the full assignment in a replacement-Session card. The base Invocation plus relied-upon Checkpoint remain the durable reconstruction sources.

After a meaningful pause has ended the Run occurrence, later execution is a new Run with concise causal provenance; use the new-Run dispatch rendering rather than a replacement-Session card.

Do not create a default `dispatch.md`, `dispatch-receipt.md`, `launch-record.md`, Human-dispatch YAML, or equivalent artifact merely to preserve this rendering. If actual dispatch chronology is materially relevant, record that consequence through existing Events/coordination state rather than duplicating the Invocation.

The Human should not author the handoff, reconstruct workflow routing, inspect the Invocation merely to recover mechanical launch parameters, or invent the continuation task.

Under the current Pilot #2 Human-Assisted posture, Participant dispatch remains a Human mechanical action. The Orchestrator must not silently substitute harness-native agent/subagent spawning for that action. If automatic dispatch is later tested, treat it as an explicit Human-approved execution-mechanism experiment; do not infer it from harness capability alone.

## Thin kickoff semantics

A new-assignment Session can be started with a compact pointer-based instruction equivalent to:

```text
Jalankan Run sesuai Run Invocation yang diberikan.
Gunakan exact Participant Profile revision yang dirujuk.
Ikuti applicable workflow dan scoped project guidance.
Jangan mengasumsikan authority/requirement di luar durable sources.
```

A continuation Session can be started with a compact instruction equivalent to:

```text
Lanjutkan Run/Participant yang sama sebagai replacement Session.
Reconstruct dari base Run Invocation, pinned Participant Profile revision,
dan Continuation Checkpoint yang diberikan.
Verifikasi durable working state sebelum melanjutkan.
```

Exact runtime/prompt mechanics remain implementation choices.