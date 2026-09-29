# Pilot #2 Candidate — Participant Profile Discovery

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: project-level Participant Profile discovery for Orchestrated Runs. This guide does not override canonical workflow guidance, project authority, or `orchestration/protocol-v0.1.md`.

## Purpose

Define how the Orchestrator discovers the smallest reusable Participant Profiles needed by a target project without inventing capabilities, authority, or hidden persistent agent state.

A Participant Profile is a reusable execution blueprint.

It is not:

- a persistent agent;
- a memory container;
- an authority grant;
- a current-work record;
- a replacement for Run invocation or workflow guidance.

Core principle:

> Discover capabilities, not personalities.

## Core rules

- profile discovery is progressive;
- project bootstrap should seed the minimum evidence-backed baseline Profile set justified by the near-term project shape, including stable recurring Roles when their need is already clear;
- existing suitable Profiles should be reused directly during normal Runs without a mandatory profile-readiness ceremony;
- later capability gaps may reuse, refine, or create Profiles through bounded Slice reconciliation or just-in-time completion when real evidence requires it;
- no profile may be more specific than the durable evidence supporting it;
- profile readiness is scoped to the capability needed now, not to project-wide documentation completeness;
- missing guidance that is not currently applicable MUST NOT block profile creation;
- when evidence does not justify a narrow specialization, prefer the least-specific safely supported profile rather than blocking unnecessarily;
- profile discovery never grants material decision authority;
- current Run state, prior Session history, and hidden agent memory do not belong in profiles.

## Discovery and reconciliation triggers

Participant Profile work has three normal entry points:

- **Project bootstrap** — establish the initial reusable baseline team justified by durable near-term project evidence;
- **Slice readiness reconciliation** — at a new Slice/material work area, reuse the baseline by default and refine/create only when the Slice introduces a materially new capability or boundary;
- **Just-in-time gap completion** — during real work, resolve a specific capability/profile gap discovered by the Orchestrator or explicitly surfaced by the Human.

Profile creation or re-evaluation is warranted when:

- runnable work requires capability not covered by current Profiles;
- an existing Profile is materially too broad or too narrow;
- a new stack, domain, risk area, or execution boundary materially changes the capability need;
- repeated Run friction indicates specialization mismatch;
- project guidance or guardrails materially change;
- an independence requirement requires a distinct execution blueprint;
- a Human requests a missing specialist/capability and durable evidence supports that need.

A new Work Unit, a normal Run dispatch, or a narrower Run scope does not by itself justify profile discovery or a visible readiness check.

Core rule:

> Profile suitability is an orchestration invariant, not a mandatory ceremony before every Run.

## Evidence sufficiency gate

Before creating or refining a profile, the Orchestrator should have enough durable project evidence to answer only what is material for the near-term capability:

1. What capability is actually needed?
2. What project/repository scope does it operate in?
3. What stack/domain context materially shapes the work?
4. What minimum durable guidance or project boundary is necessary for this profile to operate safely on the near-term work?
5. What guardrails or protected boundaries apply?
6. Is there near-term work that justifies a reusable profile rather than Run-local specialization alone?

The objective is minimum sufficient evidence, not complete project documentation.

Rule:

> No Participant Profile should be more specific than the durable evidence supporting it.

Examples:

- durable evidence proves a Go backend, applicable backend scope, and relevant project guardrails → a `Go Backend Implementer` profile may be justified;
- durable evidence proves only a backend execution need but not the stack → prefer a broader `Backend Implementer` profile if that is still safe and useful;
- missing future caching, concurrency, email, or other guidance that is irrelevant to current work must not block creation of an otherwise justified backend profile.

## Evidence sources

Use the smallest applicable set of durable project sources, such as:

- Product / Design authority;
- repository structure;
- root or scoped `AGENTS.md` guidance;
- approved architecture or tech-stack documentation;
- workflow routing;
- current Work Graph / near-term runnable frontier;
- security or protected-path guidance;
- promoted Project Learning;
- prior valid profile-discovery evidence.

Do not use chat memory, assumptions, or one-off Participant recollection as project evidence.

## Required vs routed guidance

A Participant Profile should distinguish:

- **required guidance** — minimum stable guidance that must be discoverable for the profile to operate safely in its normal project scope;
- **routed / optional guidance** — concern-specific or Run-specific guidance that is pulled only when the current Run makes it applicable.

Required guidance should normally include the stable entrypoints that define how
the Profile's Role executes under Harscode, when those entrypoints apply. In an
orchestrated project this may include, for example:

- the applicable canonical workflow phase entrypoint/guidelines for the Role;
- `workflow/orchestrated-run-overlay.md` for orchestrated identity/path semantics;
- the current Orchestrator/Pilot guidance that materially changes Participant
  execution or handoff behavior;
- project-local root/scoped guidance such as applicable `AGENTS.md` files.

The Profile should point to these sources; it should not copy their contents.

Run-specific invocation remains responsible for naming the exact current-effective
phase inputs, task scope, current authority/decision evidence, and any additional
guidance needed for that occurrence. A Profile is therefore a reusable guidance
router, not a frozen bundle of every document a future Run might need.

Use stable logical/current-effective pointers by default. Pin a guidance revision
in the Profile only when the Profile's meaning genuinely depends on that exact
revision; otherwise the Run Invocation may pin assignment-defining inputs when
drift detection matters.

For example, a Go backend profile may require root/backend project guidance plus
the stable Build/orchestrated-run entrypoints, while money, idempotency,
anti-enumeration, concurrency, or email guidance remains routed by Run scope.

Do not turn optional or future-applicable guidance into a profile-readiness prerequisite.

A Profile that names a Role/capability but provides no discoverable route to the
guidance needed to execute that Role safely is incomplete for that capability.

## Evidence-gap classification

When profile discovery cannot proceed safely, classify the material gap rather than inventing specifics.

### Documentation gap

The project likely has a settled truth, but that truth is not durably discoverable.

Route to documentation reconciliation or evidence retrieval.

### Authority gap

The project has not settled a material choice needed to define the profile safely.

Route to the relevant Authority Sync or Human authority decision.

### Exploration gap

The answer likely exists in code, repository state, or runtime evidence but has not been established.

Route to Explorer / technical investigation.

### Runtime or environment gap

A runtime capability needed to instantiate the profile is unknown or unavailable.

Route to runtime preparation or environment handling.

Runtime mechanics must not silently change the semantic profile.

A gap should block only the affected profile refinement/creation and dependent work, not unrelated orchestration.

## Baseline reuse and gap completion

Once a Profile is active and still fit for its intended project capability, normal Runs should reuse it directly.

Do not require the Orchestrator to visibly re-prove Profile readiness before each dispatch. Reconciliation is event-driven: perform it when new Slice context, durable evidence, capability mismatch, Human request, or execution friction gives a concrete reason.

Project bootstrap may create a stable baseline team whose recurring use is already justified by the near-term project shape. Just-in-time creation is for gaps discovered later, not the default way to instantiate every ordinary Role.

The Human may surface a missing capability during real work. The Orchestrator should validate the request against durable evidence and project boundaries, then reuse/refine/create the narrowest justified Profile rather than treating the request itself as authority to invent capability.

## Reuse / refine / create decision

Prefer, in order:

1. reuse an existing suitable profile;
2. refine an existing profile when the capability remains substantially the same;
3. create a new profile only when there is a materially distinct:
   - capability set;
   - operating boundary;
   - required guidance;
   - independence requirement;
   - or handoff expectation.

Do not create a profile merely because:

- a new Work Unit exists;
- a new domain name appears;
- a narrower Run scope is needed;
- another profile name would look cleaner.

Run-specific scope belongs in the invocation.

When evidence is insufficient for a narrow specialization, first evaluate whether a broader profile is safely supported before declaring discovery blocked.

## Minimum profile contract

A project-local profile should identify at least:

### Identity

- profile ID;
- display name.

### Execution semantics

- base Role;
- Specialization;
- capability scope.

### Operating boundaries

- default scope;
- guardrails;
- prohibited actions;
- escalation route.

### Knowledge routing

- required guidance pointers, including applicable Harscode workflow/orchestrated
  execution entrypoints and project-local guidance needed for normal safe operation;
- optional or routed guidance pointers when useful;
- enough separation between stable Profile guidance and Run-specific guidance
  that the Profile does not become a frozen task prompt.

### Handoff contract

- expected workflow-owned outputs;
- material Finding / Decision / Blocker behavior;
- recommended continuation;
- optional Learning Proposal behavior.

## Explicit exclusions

A Participant Profile must not contain:

- prior conversation history;
- private or persistent agent memory;
- current Work Unit state;
- current Techplan or Open-Item state;
- historical decisions as personal knowledge;
- authority grants not present in project authority;
- runtime Session identity;
- model-specific hidden state.

The Profile is a stable operating blueprint, not a durable brain.

## Authority boundary

A Participant Profile answers:

- what this actor is capable of working on;
- how it should operate;
- what execution boundaries apply.

It does not answer:

- what this actor may authoritatively decide.

Decision authority comes from the project Authority Map and applicable workflow/project authority.

## Instantiation semantics

A Profile is reusable.

A Participant is ephemeral.

Typical lifecycle:

```text
Participant Profile
→ Orchestrator assigns the Profile to a Run
→ ephemeral Participant is instantiated
→ one or more Sessions may execute the same Run occurrence if Session replacement is needed
→ Participant produces durable handoff/artifacts
→ Participant terminates when the Run occurrence ends
```

The Participant must not rely on hidden memory across future Runs.

Multiple parallel Participants derived from the same Profile must have distinct Participant identities.

## Learning exit channel

At completion, a Participant may emit a Learning Proposal when material reusable knowledge emerged.

The Participant may:

- record an Observation;
- propose Project Learning;
- nominate possible Harscode-wide relevance.

The Participant must not:

- self-promote Project Learning;
- mutate canonical project authority through a Learning Proposal;
- self-promote Harscode guidance.

Learning is promoted through the applicable review path.

The normal case may simply record:

```text
Learning Proposal: None
```

Do not require a retrospective ceremony for every Run.

## Discovery outcomes

A discovery attempt should end in one of these semantic outcomes:

- existing profile reused;
- existing profile refined;
- new profile created;
- broader safely supported profile used;
- profile creation/refinement deferred because material evidence is insufficient;
- no reusable profile needed because Run-local specialization/scope is sufficient.

When material evidence is insufficient, record:

- candidate capability/profile;
- missing evidence;
- gap classification;
- affected work;
- safe unaffected work;
- recommended next route.

Profile discovery should fail constructively, not generically.
