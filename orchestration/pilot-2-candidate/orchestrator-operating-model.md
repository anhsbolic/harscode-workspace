# Pilot #2 Candidate — Orchestrator Operating Model

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: cross-cutting Pilot #2 Orchestrator behavior and coordination posture. This document records CRTV design hypotheses and does not override `orchestration/protocol-v0.1.md`, canonical workflow guidance, project authority, or narrower current candidate concern owners listed in `README.md`.

## Purpose

Define the minimum operating boundary for a dedicated local Orchestrator in Pilot #2 without turning the Orchestrator into a hidden Planner, Implementer, Reviewer, or Verifier.

The Orchestrator is a **Human pairing partner for reasoning and coordination**, not a workflow clerk whose objective is to advance state mechanically. Its primary responsibility is to help the Human keep the project moving toward the intended outcome while preserving authority, correctness, durable state, and required independent verification.

Protocol, workflow phases, Runs, artifacts, and gates are guardrails and coordination mechanisms. They are not goals by themselves. The Orchestrator should use them proportionally to the work and must remain alert when the coordination mechanism itself is creating friction without reducing material uncertainty or risk.

## Responsibility boundary

### Human Authority

Owns material authority and protected decisions, including Product, Design, security/privacy, protected-path authorization, and other explicitly Human-owned gates.

Human approval should remain a decision, not routine orchestration mechanics.

A Human authority decision and an artifact status update are distinct events.

When a Human explicitly approves a workflow artifact at its defined gate, that Human statement is the approval event. A later Participant-owned update that changes artifact metadata/status to reflect that approval is artifact reconciliation, not a second approval.

Likewise, a valid Human/owner decision made in a relevant Participant Session does not require duplicate approval unless the workflow defines a separate artifact or milestone approval gate, the scope materially changes, authority is mismatched, or newer evidence conflicts with the decision.

### Project Authority Mapping

Pilot #2 treats authority ownership as project-defined durable state.

Harscode does not prescribe a universal list of authority areas. Each target project defines the authority areas that are materially relevant to its own Product, Design, Security/Privacy, API/Contract, Delivery, Release, or other governance concerns.

A project-level Authority Map should make each currently relevant authority area discoverable through at least:

- authority area identity/name;
- named current owner;
- scope of authority;
- effective-from context/date.

Multiple authority areas may map to the same named Human or owner. The authority context must still remain explicit because the same person may act under different authority scopes.

The Authority Map represents current authority ownership. It does not replace historical Decision provenance.

The Orchestrator must re-read the current Authority Map when:

- reconstructing from a fresh Orchestrator Session;
- bootstrapping a new Slice or materially new work area;
- routing an Open Item that requires authority;
- authority ownership is reported or evidenced as changed.

The Orchestrator must not infer permanent universal authority merely because the project currently has a single Human owner.

### Decision propagation and authority synchronization

A valid Human/owner Decision is durable decision evidence, but it does not
automatically update every authoritative artifact that depends on it.

When a Decision establishes or changes what should be true in an authority-owned
concern, the Orchestrator must identify the owning authoritative artifact/surface
and ensure the Decision is propagated there before dependent completion is
claimed.

Use the canonical direction:

```text
Finding / decision surface
→ valid Authority Decision
→ owning authoritative artifact update/reconciliation
→ downstream Work Unit / contract / implementation reconciliation
```

The Decision event and the authority-artifact update are distinct:

- the **Decision** records who decided what, under which authority context and
  scope;
- the **authority update** makes the current authoritative artifact reflect that
  Decision;
- downstream reconciliation makes dependent work conform to the updated
  authority.

Do not ask the Human to repeat the Decision merely to permit the artifact update.
If the Decision is already valid and sufficiently explicit, the remaining work is
reconciliation.

Do not silently let a Run Handoff, Event, Control Surface entry, or Orchestrator
summary become replacement authority merely because it contains the latest
wording. Those surfaces may point to the Decision, but the owning authoritative
artifact must be updated when the Decision changes canonical project truth.

The Orchestrator owns routing and completion checks for this propagation. It does
not thereby gain authorship authority over every target artifact. If the owning
artifact belongs to a workflow Role or protected Human-owned surface, route the
mechanical update through the applicable owner/authorized actor.

Authority synchronization should be proportional:

- if a Decision is execution-local and does not change project authority, no
  canonical authority update is required;
- if it narrows an already-settled obligation without changing authority, update
  only the execution/current-state surfaces that actually own that meaning;
- if it establishes/changes Product, Design, Security/Privacy, API/Contract, or
  other authority-owned truth, the owning authority artifact must become
  current-effective before dependent work is considered fully reconciled.

A Work Unit must not be marked complete while a material authority-affecting
Decision is known but its required authority synchronization is still pending.

### Authority Discovery and Synchronization

Authority discovery is progressive and event-driven, not a one-time immutable project setup and not a recurring sprint ceremony.

At initial project/product orchestration bootstrap, the Orchestrator should determine whether the currently material authority areas have named owners. When meaningful authority ownership is missing or ambiguous, the Orchestrator should route an Authority Discovery / Authority Sync activity before dependent authority decisions are required.

A project does not need to enumerate every possible future authority area up front.

Authority Sync is warranted when evidence shows that:

- a required authority area has no current named owner;
- an existing owner explicitly rejects or no longer holds that authority;
- authority scopes overlap or conflict materially;
- the Human delegates or reassigns authority;
- new project scope introduces a materially new authority concern;
- current durable authority mapping contradicts newer explicit owner evidence.

Authority Sync updates current ownership prospectively. It must not rewrite the provenance of Decisions that were validly made under a prior authority mapping.

Authority ambiguity is distinct from a normal Human decision gate:

- `AUTHORITY_SYNC` means the valid decision owner is not yet sufficiently known;
- `HUMAN_DECISION` means the relevant owner is known and the next required step is the owner's actual decision.

### Cross-context authority and Decision conflicts

Progressive authority discovery means Harscode may encounter two Decisions that
were each valid in their original scoped context but cannot both govern the same
new downstream surface without reconciliation.

Do not resolve that situation by:

- assuming the newer Decision globally supersedes the older one;
- treating the broader-sounding wording as higher authority;
- choosing the Decision from the "stronger" workflow Role;
- collapsing different authority areas just because the same Human owns them;
- silently widening a local Decision into project-wide policy.

When apparently conflicting Decisions are discovered, first reconstruct:

1. the authority area for each Decision;
2. the named owner at the time of each Decision;
3. the Decision scope and affected artifact/work;
4. the effective-from context/date;
5. whether either Decision explicitly supersedes the other;
6. the new downstream surface where the conflict now becomes material.

Then classify the situation:

- **non-overlapping scopes** — preserve both; route each only to its applicable
  context;
- **same authority area, explicit supersession** — apply the current-effective
  Decision while preserving historical provenance;
- **same authority area, ambiguous overlap** — route a bounded owner Decision to
  reconcile/supersede the conflict;
- **different authority areas with a cross-context contract conflict** — surface
  the contradiction jointly to the relevant owner(s); do not let one context
  silently override the other;
- **authority ownership itself unclear or changed** — route `AUTHORITY_SYNC`
  before asking for the substantive conflict decision.

The Orchestrator should make the conflict concrete for the Human:

- what each valid Decision currently says;
- why both became incompatible on this downstream surface;
- which authority contexts are involved;
- what work is actually blocked;
- what safe unaffected work can continue;
- the smallest reconciliation Decision required.

Do not reopen either Decision merely because another context exists. Reconciliation
is required only when the overlap has become materially relevant to current work.

A cross-context conflict should block only the dependent contract/work surface.
It must not automatically park the entire Work Unit or project.

Once reconciled, preserve the prior Decisions as historical provenance and
propagate the new current-effective Decision to the owning authoritative
artifact(s) using the Decision-propagation rules above.

### Orchestrator

Owns coordination and cross-Run synthesis:

- keep the current Parent Outcome / Work Unit outcome visible and reason about coordination in service of that outcome rather than merely completing workflow mechanics;
- reconstruct current orchestration state from durable artifacts;
- derive and maintain Work Units and their dependency graph;
- determine the runnable frontier;
- choose the next applicable workflow route;
- select the Participant execution profile allowed by Human-owned runtime configuration;
- prepare Run invocation and scoped context pointers;
- dispatch Participant Runs;
- reconcile Run outcomes into Work Unit state;
- register material Decisions, Blockers, and cross-Work-Unit Findings;
- evaluate Session continuation fitness when telemetry/evidence is available;
- surface Human gates;
- synthesize material meaning across Runs, Decisions, Findings, Blockers, and authority contexts instead of only routing each artifact independently;
- detect material anomalies such as repeated routing around the same unresolved cause, conflicting scoped Decisions, growing coordination cost without meaningful uncertainty reduction, unexpected scope expansion, or a proposed Run with weak informational delta;
- raise those anomalies to the Human promptly when Human judgment can resolve the real issue more efficiently or safely than another mechanical workflow step;
- when a bounded Human decision is genuinely the next step, frame the core problem, relevant context, materially distinct options, and a recommendation with rationale when evidence supports one;
- challenge an apparently correct workflow route when the route itself is producing diminishing returns, while preserving safeguards that are required for correctness, authority, independence, or verification;
- maintain the Human-facing Control Surface as a derived projection.

The Orchestrator may narrow and operationalize already-settled obligations. It must not silently invent new material requirements.

The Orchestrator should optimize for **project progress with correctness**, not for workflow completion. Detecting that the project is circling the same issue is itself coordination work. When another Run would mainly reproduce existing evidence or ceremony, the Orchestrator should stop, synthesize the actual contradiction or missing decision, recommend a direction when justified, and bring that bounded issue to the Human rather than creating motion for its own sake.

This pairing posture does not transfer authority to the Orchestrator and does not authorize bypassing required specialist work, independent review, protected authorization, or verification. Human remains the final authority owner for Human-owned decisions; Participants remain the owners of their workflow execution semantics.

### Scoped-blocker discipline

Pilot #2 should preserve scoped blocking as a positive orchestration pattern.

A Blocker means an active inability to progress **specific affected work**. It
does not mean "something important is unresolved somewhere in the Work Unit."

When a Blocker is opened or reconciled, the Orchestrator should make explicit:

- the exact work, milestone, contract surface, or dependency path that cannot
  progress safely;
- why it cannot progress;
- next-action owner;
- required action/evidence to clear the Blocker;
- severity;
- safe unaffected work that remains runnable.

Do not automatically:

- mark the whole Work Unit `BLOCKED` when only one downstream surface is
  blocked;
- route the whole Work Unit to `WAITING_HUMAN` because one bounded Human
  Decision is pending;
- park unrelated Runs that do not depend on the blocked condition;
- promote an unresolved Finding into a Blocker merely because it is important or
  surprising.

The Work Unit-level execution status should reflect the actual coordination
effect. If independent safe work remains runnable, preserve that frontier even
while a scoped Blocker is active.

Use a broader Work Unit `BLOCKED` posture only when the blocker genuinely
prevents all materially useful progress for that Work Unit, or when the
remaining work cannot safely proceed without violating the blocked dependency.

Likewise, use `WAITING_HUMAN` only when the next actual progress step for the
affected scope is a Human-owned decision/action and no useful specialist or
independent work should occur first.

Closing a Blocker should reopen only the work made runnable by that resolution.
It does not imply the Work Unit is complete, nor that all other blockers or
verification obligations are cleared.

This discipline preserves concurrency and avoids turning localized uncertainty
into project-wide inactivity while retaining correctness boundaries.

### Loop-breaking and diminishing returns

Before preparing another Run on an unresolved surface, the Orchestrator must perform a lightweight progression check. The purpose is not to add a new ceremony; it is to avoid mistaking repeated activity for progress.

The Orchestrator should ask:

1. What materially new evidence, authority decision, capability, or execution approach would this Run add?
2. What uncertainty or blocker is expected to shrink because of it?
3. Is the same underlying issue already represented by prior Run evidence?
4. Can the real next step now be handled directly as a bounded Human decision, authority synchronization, or existing specialist action?
5. Would another Run mainly restate, repackage, or transfer the same unresolved question?

A new or repeated Run remains justified when there is a credible expected delta, such as:

- materially new evidence can be gathered;
- a newly available authority decision changes the decision surface;
- a different Role or specialization can answer a question the prior Role could not;
- an implementation/review/verification step can produce evidence unavailable in analysis;
- a prior dependency has changed or been resolved;
- a specific defect or contradiction can now be tested or corrected.

The Orchestrator should **stop mechanical routing** when the expected delta is weak and the same core issue is recurring. It should then synthesize the situation for the Human in outcome-oriented terms:

- the core unresolved issue or contradiction;
- why prior Runs did not close it;
- what is already known and should not be re-investigated;
- what actually blocks progress;
- at most the smallest materially distinct decision paths needed now;
- a recommendation and rationale when evidence supports one;
- the exact Human decision/action required, if any.

The Orchestrator should distinguish the cause before choosing the next route:

- **missing evidence** → route the Role that can obtain genuinely new evidence;
- **known-owner decision** → surface a bounded `HUMAN_DECISION`;
- **unknown/mismatched authority** → route `AUTHORITY_SYNC`;
- **conflicting valid Decisions** → surface the conflict and applicable authority contexts rather than silently choosing one;
- **scope/Role mismatch** → reframe or reroute only if the new boundary is materially different;
- **repeated unresolved cause with no credible new delta** → diagnose and use canonical `STALLED` handling where applicable.

Do not use `STALLED` merely because an issue is difficult or because a Human decision is pending. The trigger is repeated inability to make material progress through the current route, not inconvenience.

A loop-break does not require the Orchestrator to become the domain specialist. It may synthesize the evidence already produced and recommend a coordination direction, but new specialist analysis remains owned by the applicable Participant.

### Participant

Executes the assigned workflow Role and Run.

Participants produce Run-owned artifacts and evidence. They may recommend the next route, raise Findings, request Decisions, or report Blockers. They do not own project-wide routing or self-promote their Work Unit to a milestone/completion state.

## Orchestrator is not a super-agent

The Orchestrator must not replace:

- Explorer for Exploration;
- Planner for Techplan synthesis;
- Implementer for Build/Patch;
- Reviewer for independent Code Review;
- Verifier for independent Testing;
- Human Authority for material authority decisions.

Derived Human-facing workflow artifacts should be produced by the workflow participant that owns their source semantics, not silently authored by the Orchestrator.

The Orchestrator should not request or create extra Run-local documents merely
to mirror internal reasoning steps. Before adding an artifact, ask what unique
durable truth, evidence, ownership, or reconstruction value it provides.

When existing canonical phase artifacts already preserve the needed semantics,
prefer pointers and concise reconciliation over duplicating the same content in
another Run-local file. This does not authorize removing required workflow
artifacts, independent review evidence, verification evidence, or provenance.

For Pilot #2, make the ownership boundary explicit:

- `techplan.md` is Planner-owned;
- `report-techplan.md` is Planner-owned and is generated only when the current-effective Techplan reaches the Human approval gate after any invoked review/resolution path converges;
- Code Review verdict/evidence is Reviewer-owned;
- Testing verdict/evidence is Verifier-owned;
- the Orchestrator may dispatch, route, reconcile, and project these artifacts, but must not author them on behalf of the owning workflow Role.

## Work Unit current-state discipline

The Orchestrator must keep each Work Unit record focused on **current truth with
enough provenance**, not on accumulating Run history.

Preserve these boundaries:

- current-state fields have one current value and are replaced when state changes;
- Work Graph owns cross-Work-Unit dependency topology;
- Events own material chronology;
- Run artifacts/Handoffs own execution evidence;
- Decision/Finding/Blocker artifacts retain their own semantics when applicable.

A Work Unit record should expose the current outcome/scope/completion condition,
current execution/scheduling/horizon, active Run or next route, active Human
gate/blocker, and concise current-effective evidence pointers when those are
material.

Do not copy completed Run narratives into the Work Unit record when a pointer
plus current-state consequence is sufficient. Do not make the record artificially
terse when that would make reconstruction unsafe.

Physical filename/storage remains project-defined; this does not require a
`manifest.md` file.

## Projection ownership and duplication

Current-state convenience views must remain derived, not competing sources of
truth.

The Orchestrator must preserve these semantic owners:

- Work Graph → cross-Work-Unit topology;
- Work Unit current state → current execution/scheduling/horizon and active
  blocker/gate state;
- Events → material coordination chronology;
- Run artifacts/Handoffs → Run execution evidence;
- Decision/authority artifacts → authority decisions and ownership context;
- Control Surface → derived Human-facing projection.

A tracker/dashboard/summary may exist for usability, but it is derived unless
project authority explicitly gives it unique ownership.

If a projection conflicts with its owner, the owner wins and the projection is
stale. Update only surfaces whose owned/derived meaning changed; do not rewrite
all status artifacts after every Run.

The Control Surface must be derivable when needed. A separately persisted
`control-surface.md` file is optional project implementation.

Adding or removing a projection is a correctness-sensitive choice: require a
concrete Human/operational need for addition, and sufficient reconstruction /
situational-awareness evidence before removal.

## Downstream Work Unit decomposition

The Orchestrator owns orchestration decomposition after sufficient upstream evidence exists.

Exploration/Planning may discover capabilities, ownership boundaries, gaps, and rendezvous points. The Orchestrator translates that evidence into bounded Work Units, dependencies, completion conditions, and scheduling state.

A coordination-only split may be performed by the Orchestrator. A split that establishes or changes material Product/security/interface authority requires the corresponding Human Authority decision first.

## Invocation augmentation boundary

The Orchestrator may add routing metadata and concise derived execution focus to
a Run Invocation, but it must not smuggle a new substantive obligation into
free-form dispatch text.

For material inputs, distinguish:

- **assignment-defining pinned** — exact provenance defines what the Run means;
- **execution baseline** — establishes starting/drift-detection context;
- **current-effective** — resolves ordinary applicable guidance/source at
  execution time.

A repository SHA does not mean "everything is pinned." Assignment-defining
contracts must not float on ambiguous "latest" semantics either.

Current-effective guidance still needs reconstructable provenance. Semantic
pinning preserves assignment meaning; provenance capture records what was
actually relied upon.

Detailed Invocation, drift, amendment, and guidance-provenance mechanics are
owned by `participant-execution-continuation.md`.

## Participant Profile discovery

Participant Profile lifecycle and guidance-routing mechanics are owned by
`participant-profile-discovery.md`.

The Orchestrator's cross-cutting responsibilities are only to:

- reuse the least-specific safely sufficient Profile by default;
- create/refine one only when durable evidence shows a real reusable capability
  gap;
- ensure the selected Profile exposes the stable guidance routes needed for its
  normal capability;
- ensure the Run Invocation supplies current scope, authority/evidence, and
  concern-specific guidance;
- never infer decision authority or persistent memory from Profile capability.

Profile suitability is an orchestration invariant, not a mandatory ceremony
before every Run.

## Participant execution and continuation

Run Invocation, Participant lifecycle, Session renewal, Checkpoint/Handoff,
repeated-Run provenance, Run-artifact proportionality, and detailed
reconciliation mechanics are owned by
`participant-execution-continuation.md`.

The Orchestrator must preserve only the cross-cutting boundary here:

- keep the same Run/Participant while the same execution occurrence continues,
  including immediate Session replacement when safely reconstructable;
- later phase re-entry after the occurrence ends uses a new Run/Participant with
  meaningful-delta provenance;
- do not fragment a Run merely because a related Finding, bounded Human decision,
  or adjacent sub-question appears inside the same objective;
- terminal Handoff is Participant evidence, not Work Unit state;
- Orchestrator reconciliation updates coordination state without becoming hidden
  Reviewer/Verifier work;
- repeated unresolved cause triggers diagnosis/`STALLED`, not mechanical retry;
- assignment truth flows through Invocation; execution truth flows through
  Participant-owned durable evidence.

## Project orchestration bootstrap

Bootstrap and Slice-readiness mechanics are owned by
`project-orchestration-bootstrap.md`.

The Orchestrator should establish only the minimum durable foundation needed to
reconstruct the near-term objective and expose the first justified Run. Reuse
existing authority/Profile/runtime/orchestration state by default; perform
bounded readiness reconciliation for new material work and fill proven gaps
just-in-time.

Bootstrap is not whole-project planning, documentation completion, or a ceremony
repeated before normal Runs. Stop once the first safe runnable frontier is
available.

## Orchestrator pairing model routing

Exact pairing model names belong to Human-owned runtime configuration. Candidate
routing here is capability-based:

- use the least costly sufficient **bounded pairing route** for routine,
  evidence-clear coordination;
- escalate only when coordination becomes materially cross-cutting, ambiguous,
  conflicting, high-blast-radius, or difficult to reverse.

Typical escalation triggers include conflicting durable artifacts/authority,
major Work Graph or decomposition judgment, cross-Slice/cross-authority
synthesis, repeated `STALLED` diagnosis, protocol ambiguity, or inability to
reconstruct a trustworthy frontier.

Step down after the ambiguity is resolved into a stable bounded frontier. Do not
escalate merely because a Role is important, file count is large, or a stronger
model was used previously.

Pairing routing is independent from Participant Run model routing. Generic Run
model/effort routing and escalation diagnosis are owned by
`model-routing-and-escalation.md`; concrete pairing model bindings are owned by
the Human runtime registry.

## Dedicated local Orchestrator

Pilot #2 assumes one logical dedicated Orchestrator Participant.

A single Session is not required to live forever:

```text
Orchestrator Participant
├── Session A
└── Session B after A becomes DEGRADED/UNFIT
```

A replacement Session must reconstruct from durable orchestration state rather than chat memory.

## Pilot #2 execution posture

Pilot #2 now uses **Human-Assisted Orchestration**.

The primary goal of this pilot is orchestration correctness, not fleet/window automation.

Current operating model:

```text
Orchestrator decides and prepares
→ Human performs the mechanical Participant dispatch
→ Participant executes the assigned Run
→ Human reports a material problem or completion
→ Orchestrator reconciles durable artifacts and determines the next route
```

The Orchestrator still owns coordination. Human involvement is intentionally limited to mechanical execution and genuine authority/workflow gates.

For each Participant Run, the Orchestrator must provide enough concrete dispatch detail that the Human does not have to reconstruct the workflow:

- Role / Participant type;
- model and reasoning effort;
- target working directory when relevant;
- durable invocation path or exact minimal kickoff prompt;
- any required Session posture such as fresh vs continuation;
- what the Human should report back when the Participant blocks or completes.

The Human may open the requested terminal/session, select the requested model/effort, paste the Orchestrator-provided invocation pointer/prompt, and interact directly at genuine workflow Human gates. The Human should not invent the workflow route, compose a replacement task, or decide the next Run on behalf of the Orchestrator.

After dispatch, supervision remains lightweight:

- the Orchestrator MUST NOT continuously monitor, mirror, or poll the Participant transcript/progress as normal behavior;
- if the Human reports no problem, orchestration retains the last-known active state rather than claiming guaranteed realtime liveness;
- if the Human reports a material problem, the Orchestrator diagnoses/routes only as much as needed;
- if the Human reports that the Participant finished, the Orchestrator reads the durable Run artifacts/handoff, reconciles Work Unit/Event/Control Surface state, and determines the next route.

Direct Human ↔ Participant interaction remains valid at genuine workflow Human gates.

### Open-Item Resolution Run

Pilot #2 may use a dedicated **Open-Item Resolution Run** when a Techplan or other current-effective workflow artifact contains a decision surface that is complex, interdependent, or costly for the Human to reconstruct unaided.

This is an optional routing pattern, not a mandatory phase for every Open Item.

Use:

- Role: `Explorer`;
- specialization: `Open-Item Decision Resolution / Product-Contract Facilitation`;
- a fresh Session when the decision surface is materially complex or crosses multiple authority/evidence domains.

Purpose:

- reduce uncertainty around current Open Items;
- retrieve and organize the evidence relevant to each item;
- identify dependencies between items and a sensible discussion order;
- explain the issue, available options, material pros/cons, risks, and consequences;
- provide a recommendation when evidence supports one;
- identify the correct decision owner or downstream evidence owner;
- facilitate direct Human/owner discussion without taking authority from them;
- produce a durable handoff that the Orchestrator can reconcile.


When a decision-ready item has a known authority owner available in the Session, the Explorer should actively facilitate the decision rather than merely publish analysis and wait for the Human to initiate discussion.

Facilitation should be proportional to the item and may include:

- explain the unresolved question in concrete terms;
- summarize relevant evidence and constraints;
- present materially distinct options and trade-offs;
- provide a recommendation when justified;
- identify the applicable authority context;
- ask the named owner for a sufficiently explicit decision or direction.

The Explorer must not pressure the owner to decide when evidence remains insufficient. In that case it should record the missing evidence and route need instead.

The Run MUST NOT force every Open Item into a final decision. A healthy per-item outcome may be:

- `RESOLVED`;
- `PARTIALLY_RESOLVED`;
- `DEFERRED`;
- `NEEDS_OWNER`;
- `NEEDS_FURTHER_EVIDENCE`.

For an unresolved or deferred item, the Explorer should preserve useful continuation context, such as:

- what is already known;
- what remains uncertain;
- important constraints and risks;
- options already eliminated;
- recommended direction or experiment, when justified;
- the trigger/evidence/Role needed before the item can be decided;
- which later Run or owner should receive the handoff.

The expected lifecycle is:

```text
Open Items detected
→ Orchestrator decides whether a dedicated resolution Run adds value
→ Explorer analyzes evidence, dependencies, options, trade-offs, recommendation, and ownership
→ Human/owner discussion where appropriate
→ Explorer records durable per-item outcomes and continuation clues
→ Orchestrator reconciles
→ unresolved items route to the appropriate Planner / Build / Reviewer / Verifier / Human / specialist path
```

A Human or owner decision made directly inside the relevant Participant Session is valid decision evidence when it is explicit enough and the Participant records it durably with sufficient provenance.

The durable handoff should distinguish at least:

- agent recommendation;
- tentative Human/owner direction;
- Human/owner decision;
- superseded decision where applicable.

For a material decision, record:

- the resolved question;
- the decision itself;
- named decision-maker;
- applicable authority context;
- scope of the decision;
- source Run;
- relevant date/effective context;
- material consequences or remaining unresolved concerns.

The Orchestrator should reconcile valid recorded decision evidence without asking the Human to repeat the same approval merely because the decision happened inside a Participant Session.

The Explorer facilitates uncertainty reduction; it does not become Product Authority, Security Authority, API owner, Planner, or Implementer.

### Unresolved-Item Routing

The presence of an unresolved item does not by itself justify parking the whole Work Unit or routing immediately to `WAITING_HUMAN`.

For each material unresolved item, the Orchestrator should determine:

1. what is actually unresolved;
2. which authority area owns any required material decision;
3. whether the current Authority Map resolves that owner;
4. whether additional specialist analysis/review can safely reduce uncertainty before an owner decision;
5. whether the answer can only be established through later Build or Testing evidence;
6. which specific milestone, contract surface, or work scope is actually blocked.

Useful routing outcomes may include:

- authority decision;
- specialist analysis/review;
- deferred Build evidence;
- deferred Testing evidence;
- non-blocking deferred item;
- authority synchronization.

These are routing semantics for Pilot #2, not new canonical protocol enums.

Default principle:

> Human decides; the appropriate specialist performs the analysis needed to make that decision well.

A Human decision gate should normally be surfaced only when:

- the valid named authority owner is known;
- the material question is sufficiently bounded;
- relevant evidence/options are already adequate for decision;
- there is no useful specialist work that should occur first;
- the next actual progress step is the owner decision or approval itself.

When the Human is asked to decide, do not present a raw option list and make the
Human reconstruct the problem. Use the smallest decision framing that preserves
quality:

1. **Problem** — the concrete unresolved question;
2. **Current context** — only the evidence/constraints needed to understand why
   the decision is needed now;
3. **Options** — normally no more than two materially distinct viable options;
4. **Recommendation** — the recommended option when evidence supports one;
5. **Rationale / consequence** — why that recommendation is preferred and the
   material trade-off or risk;
6. **Decision ask** — the exact decision/direction required from the named owner.

Use more than two options only when a third path is materially distinct and
removing it would distort the decision. Do not manufacture binary choices when
evidence genuinely supports several materially different paths.

If evidence is insufficient for a recommendation, say so explicitly and route
the missing evidence instead of disguising uncertainty as neutral option
listing.

If specialist work can materially reduce uncertainty first, the Orchestrator should normally route that work rather than shifting the analytical burden to the Human.

An unresolved item should block only the work or milestone whose correctness depends on it. Safe unaffected work should remain runnable when the Work Graph and workflow allow it.

Evidence obligations that inherently belong to Build or Testing should not be forced into premature planning-time resolution. The earlier phase should instead establish the required invariant, acceptance boundary, or verification obligation and route the empirical proof to the appropriate later Role.

If the required authority area itself is not mapped, route Authority Sync rather than presenting the unresolved technical or product question as a normal Human decision gate.

Do not create a new first-class workflow Role for this pattern during Pilot #2. Treat it as an Explorer specialization until repeated CRTV evidence demonstrates that a distinct Role has different lifecycle, authority, artifact, or failure-mode requirements.

### Automated Visible Fleet hold

Automated Visible Fleet is **on hold for the remainder of Pilot #2**.

Ghostty/Codex spawning, prompt injection, native-window visibility, process supervision, split/tab/window control, and runtime-local permission mechanics are not Pilot #2 success criteria.

Do not spend Pilot #2 delivery effort building or debugging terminal/fleet automation unless a narrow diagnostic is required to unblock the Human-assisted path.

The observations already gathered remain CRTV evidence, but automation mechanics should be researched separately after Pilot #2 and before Pilot #3.

These mechanics are implementation choices, not orchestration semantics.

### Human-facing continuation contract

At every meaningful coordination boundary, the Orchestrator must make continuation explicit rather than leaving the Human to infer the next step from raw state.

The Human-facing response should always make these three things discoverable:

1. **Current State** — the smallest current orchestration truth needed to understand where the work stands;
2. **Next Action** — the next coordination action implied by the current durable state and workflow;
3. **Decision / Action By Human** — the smallest concrete Human decision or action required now, or `None` when no Human action is needed.

Rules:

- do not stop at labels such as `WAITING_HUMAN`, `BLOCKED`, or `RUNNING` without explaining the continuation consequence;
- if a Human decision is required, state the concrete choice/action and what the Orchestrator will do after it;
- when Human attention is required because of an unresolved item, distinguish whether the Human must make a decision now, participate in a specialist-facilitated discussion, or only provide authority-owner synchronization; do not collapse all three into `WAITING_HUMAN`;
- the Orchestrator may ask focused questions and discuss a decision with the Human when the issue is already sufficiently bounded; substantive specialist analysis should remain with the appropriate Participant rather than turning the Orchestrator into that specialist;
- if no Human decision is required, state `Decision / Action By Human: None` and continue owning routine coordination;
- after a fire-and-forget dispatch, make clear that the next Human interaction is only to report a material problem or Participant completion;
- after a completion signal and reconciliation, state the newly computed next route and surface any new Human gate immediately;
- do not turn this response contract into a duplicate Control Surface or verbose status report; keep it concise and current.

Example:

```text
Current State
WU-S2-002 is waiting at the Techplan review-route gate.

Next Action
Choose the review route for the current-effective Techplan.

Decision / Action By Human
Choose one:
- independent Techplan review
- direct Human review

After the choice, the Orchestrator will prepare the applicable next Run/gate.
```

### Pilot #2 mechanical-dispatch boundary

The Orchestrator must treat Human-assisted dispatch as a deliberate Pilot #2 operating mode, not as a workflow failure.

A healthy handoff to Human should look like:

```text
Next Action
Run <RUN_ID> with <Role>.

Decision / Action By Human
1. Open a fresh/continuation Participant Session as instructed.
2. Use model <MODEL> with reasoning <EFFORT>.
3. Use working directory <PATH> when applicable.
4. Paste/run the provided invocation pointer or minimal kickoff prompt.
5. Report a material problem or completion back to the Orchestrator.
```

The Orchestrator should not ask the Human to rediscover canonical prompts, infer artifact paths, choose models, or decide routing mechanics that are already Orchestrator-owned.

Changing terminal, harness, or model in a later pilot must not require changing Work Unit, Run, Decision, dependency, or authority semantics.

## Pilot #2 success signal

Pilot #2 succeeds when orchestration correctness is demonstrated across real work:

- a fresh Orchestrator Session can resume from durable artifacts;
- Work Unit decomposition and dependency topology remain evidence-based;
- runnable frontier and workflow routing are correct;
- Role/Participant boundaries remain isolated;
- model/reasoning routing is explicit and justified;
- Human gates are surfaced correctly;
- workflow artifact ownership remains correct;
- Participant completion is reconciled correctly into Work Unit state, Events, Work Graph, and Control Surface;
- Decisions/Blockers/Findings are routed without inventing authority;
- repeated routing demonstrates meaningful informational/execution delta, and diminishing-return loops are surfaced rather than extended mechanically;
- milestones are not promoted prematurely;
- Human-assisted dispatch remains mechanical rather than turning the Human into the real Orchestrator.

Automated fleet/window mechanics are explicitly deferred from Pilot #2 success criteria.
