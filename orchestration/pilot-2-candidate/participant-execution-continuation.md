# Pilot #2 Candidate — Participant Execution and Continuation

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Run invocation, ephemeral Participant execution, Session renewal, execution handoff, and artifact ownership for Human-Assisted Orchestration. This guide does not override project authority, canonical workflow guidance, or `orchestration/protocol-v0.1.md`.

## Purpose

Define the minimum durable contract for executing a Run through ephemeral Participants and disposable Sessions without relying on hidden conversational memory.

Core principles:

> The Run is durable assignment state. The Participant is ephemeral execution capacity. The Session is a disposable runtime context.

> A Session may be disposable; an active assignment must be reconstructable.

> Assignment truth flows from Orchestrator to Participant; execution truth flows from Participant back to Orchestrator.

## Semantic boundary

- **Participant Profile** — reusable execution blueprint: capability, operating boundaries, guidance routing, and expected handoff behavior.
- **Run** — durable bounded assignment and workflow execution route.
- **Participant** — concrete ephemeral executor identity for a Run.
- **Session** — temporary runtime/context container used by that Participant.
- **Run Invocation** — Orchestrator-owned binding artifact that tells a Participant what Run to execute.
- **Continuation Checkpoint** — Participant-owned execution-state artifact used when the same Run/Participant continues in a replacement Session.
- **Participant Execution Handoff** — Participant-owned result/handoff artifact produced when the Run execution occurrence ends.

A Run is one execution occurrence of a workflow activity, consistent with the canonical protocol.

A Run may span multiple Sessions only when the same active execution occurrence continues through immediate context/runtime renewal.

A Run must not span multiple separated execution occurrences.

## Run Invocation

The Orchestrator owns the Run Invocation.

The Invocation defines the assignment; it does not duplicate durable project truth or become a giant prompt.

A minimal Invocation should make discoverable:

- Run ID;
- Work Unit ID;
- workflow route;
- Role;
- Participant Profile ID and pinned revision;
- Participant ID for the initial execution episode;
- bounded Run objective;
- Run-specific scope;
- Run-level completion condition;
- current-effective input pointers;
- material input revision-at-dispatch when drift detection is useful;
- model/reasoning route and rationale;
- working directory/runtime route;
- Session posture;
- expected Participant-owned outputs/handoff behavior.

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

## Invocation stability

Before dispatch, the Orchestrator may edit the Invocation normally.

Once a Participant has been dispatched from it, the Invocation has crossed its reliance boundary and becomes effective assignment evidence.

After dispatch:

- non-material cleanup may use normal Git history;
- material changes to objective, scope, Role, workflow route, completion condition, Profile, or authority-relevant inputs must not be silently rewritten;
- a material semantic assignment change should normally create a new Run;
- a narrow clarification that does not change the assignment may be handled as an explicit amendment when justified.

A Run must not silently become a different assignment while retaining the same identity.

## Participant Profile revision

An active execution episode uses the Participant Profile revision pinned at dispatch.

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
→ Participant execution episode instantiated
→ Session executes
→ Participant writes Checkpoint when immediate Session renewal is needed
→ Participant writes Execution Handoff when the execution episode ends
→ Participant terminates
→ Orchestrator reconciles Run / Work Unit / next route
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

When execution stops for a Human decision, external dependency, blocker, or another meaningful pause that ends the current execution occurrence:

```text
Participant writes Execution Handoff
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

## Repeated Run provenance

A repeated/new Run created after workflow re-entry should preserve concise provenance to the prior execution.

Make discoverable when applicable:

- prior Run ID;
- prior Participant Execution Handoff;
- meaningful delta that justifies re-entry;
- newly effective Decision/evidence;
- current-effective assignment inputs.

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

## Replacement Session reconstruction

A replacement Session should perform a short reconstruction procedure before substantive continuation:

1. read the base Run Invocation;
2. read the exact pinned Participant Profile revision;
3. read the latest Continuation Checkpoint;
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

The Participant owns the Participant Execution Handoff.

The Handoff ends the current Run execution occurrence. The Orchestrator then reconciles the Work Unit and determines whether the Work Unit is complete, waiting/blocked, or later requires a repeated/new Run.

A minimal Handoff should make discoverable:

- execution outcome;
- durable outputs;
- Findings;
- Human/owner Decisions observed, with provenance when applicable;
- Blockers;
- remaining concerns/work;
- recommended continuation;
- Learning Proposal pointer or `None`.

The Participant may recommend a next route but must not create the next Run, mark a Work Unit complete, or self-promote a milestone.

Useful execution-outcome semantics may include:

- assigned work completed;
- partial execution;
- blocked;
- waiting on external/Human decision.

These are Participant execution results, not canonical orchestration-state enums.

## Human decisions during Participant execution

A Human/authority decision made inside a Participant Session is valid decision evidence when it is explicit enough and recorded durably with appropriate provenance.

The Participant records the decision as observed evidence; it does not become the authority owner.

The Orchestrator later reconciles the decision into durable project/orchestration state without requiring duplicate approval merely because the decision occurred inside a Participant Session.

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

When the Participant produces the terminal Execution Handoff for the occurrence, that Run ends.

If the Work Unit is not yet complete because it is waiting on a Human/owner decision, blocked by a dependency, or requires later re-entry, the Orchestrator updates canonical Work Unit execution/scheduling state rather than keeping the Run alive.

Later execution uses a new Run with meaningful-delta provenance.

Run result/reconciliation remains Orchestrator-owned; Participants do not self-promote Work Unit or milestone state.

## Artifact ownership

Semantic ownership for this candidate model:

- Run Invocation — Orchestrator;
- Continuation Checkpoint — Participant;
- Participant Execution Handoff — Participant;
- Session Transition / recovery record — Orchestrator;
- Run dispatch/result chronology — Orchestrator;
- Work Unit execution/scheduling state / Work Graph / Control Surface — Orchestrator;
- Human Decision — Human/authority owner; evidence may be recorded by Participant;
- Learning Proposal — proposer/Participant;
- Project Learning promotion — applicable Human/review authority.

One durable artifact should have one semantic owner. Avoid shared-write artifacts whose provenance becomes ambiguous.

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
- Handoff reliance boundary — Orchestrator reconciliation;
- Decision reliance boundary — downstream work acts on it;
- Learning Proposal reliance boundary — review/promotion begins.

Do not create correction artifacts for trivial formatting/typo changes unless they affect material interpretation.

Material corrections may use simple relations such as:

- `AMENDS`;
- `SUPERSEDES`.

Do not build a heavyweight artifact-versioning system unless repeated CRTV evidence requires it.

## Human-Assisted dispatch

The Human remains a mechanical dispatcher in Pilot #2.

For a new assignment, the Orchestrator should provide:

- Run;
- Participant/Profile;
- model/reasoning;
- working directory;
- Invocation pointer or minimal kickoff prompt.

For immediate Session renewal, the Orchestrator should provide:

- same Run;
- same Participant;
- same pinned Profile revision;
- replacement Session posture;
- base Invocation pointer;
- latest Continuation Checkpoint.

After a meaningful pause has ended the Run occurrence, later execution must be dispatched as a new Run with concise provenance to the prior Run/Handoff and the meaningful delta.

The Human should not author the handoff, reconstruct workflow routing, or invent the continuation task.

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
