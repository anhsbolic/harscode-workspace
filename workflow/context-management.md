# Context Management and Phase Handoff

This file defines the portable workflow rule for loading context, crossing phase/session boundaries, and handing durable state to the next phase. Harness-specific files translate these rules; they do not redefine them.

## Objective

Use the **smallest sufficient context that preserves correctness**.

Context efficiency is not permission to omit material authority. A run is efficient only when it avoids irrelevant/repeated reads while still preserving product/domain behavior, authority/security boundaries, architecture/ownership decisions, interface contracts, risks, verification obligations, and unresolved items.

## Context classes

For the active phase, classify potential inputs as:

- **Required** — must be read/verified to execute this phase correctly.
- **Routing / clue** — used to locate relevant authority; scan/search only the portion needed to route.
- **Conditional** — read when its explicit trigger applies.
- **Cold / reference** — examples, retros, history, deep rationale; read only for a concrete need.

“Important” does not mean “required on every run.”

## Durable state beats chat memory

Correctness must be reconstructable from durable artifacts plus current source-of-truth files. A phase may reuse context already loaded in the same healthy session when the same execution occurrence is still active, or in a non-orchestrated flow where no Run boundary has been crossed. A required decision cannot exist only in remembered conversation.

A fresh session re-grounds on the smallest sufficient durable state:

```text
target-repo applicable instructions/authority
+ current phase canonical prompt
+ current task's authoritative prior-phase artifact(s)
+ relevant live source/code/spec
+ a specific finding/patch plan when re-entering Build
```

Do not paste or re-read an entire earlier phase merely because it exists.

Durable workflow-generated artifacts should also carry compact execution provenance when the phase controls their format: phase/stage, author, created/updated time, and — when the harness exposes them and it is safe/useful to persist — model, reasoning effort, session/thread id, target revision, and workflow revision. Do not invent unknown values or persist account/credential metadata. Git history remains the default version history.

## Orchestrated Run identity

When Orchestrator Protocol v0.1 dispatches the phase, also apply `workflow/orchestrated-run-overlay.md`.

Keep these identities separate:

```text
Work Unit = bounded delivery outcome
Run       = one workflow execution occurrence
Participant = assigned executor
Session   = bounded execution context
```

A fresh Session does not create a new Work Unit.

In orchestrated mode, keep two continuation paths distinct:

- **same active Run** — immediate Session replacement may preserve the same Run and Participant when the execution occurrence is still continuing;
- **new phase / later phase re-entry after a completed occurrence** — create a new Run, new Participant identity, and fresh Participant Session/context. Reconstruct from durable artifacts; do not resume the prior Participant's conversation as hidden execution state.

For fresh-session grounding, prefer current-effective artifacts named by orchestration state over scanning historical Run folders. Deep history is conditional context for regression, loop diagnosis, decision audit, or another concrete need.

## Same session vs fresh session

Use **continuation fitness**, not a fuzzy task-size label.

The rules in this section apply to Session replacement inside the same active execution occurrence and to non-orchestrated workflow usage. They must not be used to carry one Participant/Session across an orchestrated Run boundary.

### CONTINUE when

- the next concern shares the same authority/posture;
- relevant source material is still active and unchanged;
- the session has not accumulated substantial dead ends or unrelated investigation;
- no independence benefit is lost;
- required durable artifacts already exist so a later fresh start remains possible.

### FRESH when

- independence is part of the next phase's value (Code Review, Testing);
- the next phase has different write/tool authority;
- the session has been compacted/reset or has substantial exploratory dead ends;
- major human redirection invalidated earlier reasoning;
- the agent can no longer name the current authoritative artifacts without reconstructing the conversation;
- carrying the current transcript would add more stale/noisy context than useful working state.

Do not invent a context-window percentage as an automatic cutoff. Context occupancy is a signal, not a substitute for these observable conditions.

## Default transition intent

| Transition | Default |
|---|---|
| Exploration → Techplan | **Non-orchestrated:** adaptive from continuation fitness. **Orchestrated:** new Techplan Run/Participant with fresh Session context. |
| Techplan → Build | **Fresh** in orchestrated mode; fresh preferred otherwise. Build needs the approved contract + live code, not exploratory reasoning. |
| Build iteration → Build iteration | **Continue** only while it remains the same active Build Run/execution occurrence. |
| Build → Code Review | **Fresh** for independent inspection; orchestrated mode uses a new Review Run/Participant. |
| Code Review → Patch | **Build authority. Orchestrated:** new Build/Patch Run/Participant with fresh Session context re-grounded on the patch plan. **Non-orchestrated:** continuation fitness may reuse a healthy Build session. |
| Build/Patch → Testing | **Fresh** for independent verification; orchestrated mode uses a new Testing Run/Participant. |
| Testing → Patch | **Build authority. Orchestrated:** new Build/Patch Run/Participant with fresh Session context re-grounded on the patch plan. **Non-orchestrated:** continuation fitness may reuse a healthy Build session. |
| Testing → PR | **Orchestrated:** new PR Run/Participant when PR work is dispatched as a Run. **Non-orchestrated:** flexible; ground on final repository state + durable evidence. |

Fresh for **independence** and fresh for **context hygiene** are different reasons. Record the actual reason.

`CONTINUE`, `FRESH`, and `BUILD authority` are portable routing semantics. Human-facing handoffs should translate them into an explicit action sentence instead of exposing only the enum. Examples:

```text
Continue Techplan synthesis in this session because Exploration context remains focused and current. (Non-orchestrated flow.)
Start a fresh Techplan Participant Session from the new Run Invocation because orchestrated phase transition creates a new Run/Participant.
Start a fresh Code Review session because reviewer independence is part of the next phase's value.
Start a fresh Build/Patch Participant Session from the new Run Invocation and patch plan because orchestrated re-entry is a new Run/Participant.
Return to the existing Build session only in a non-orchestrated flow when continuation fitness remains healthy.
```

## Code knowledge across phases

Transfer **coordinates, not cached facts**.

Exploration/Techplan may record a code anchor:

```text
path/to/file.ext — SymbolName / heading / relevant block — why it matters
```

A later Build re-opens current code at that anchor before editing. Earlier prose about code is evidence from when it was inspected, not a replacement for the live repository.

Build is not expected to re-explore product/domain intent. If live code makes a material contract assumption false, stop and report back instead of silently redesigning.

## Patch authority

Code Review and Testing may identify a finding and write a patch plan. Production-code fixes execute through Build/Patch authority.

A Build re-entry needs only the smallest sufficient set:

```text
approved techplan (and current task slice if decomposed)
+ specific patch plan/finding
+ relevant current code/diff
+ latest build report when it contains needed verification state
```

Do not carry the whole Review/Testing conversation into Build.

In orchestrated mode, a handoff back to Build starts a new Build/Patch Run with a new Participant and fresh Session context, re-grounded from the new Invocation plus the smallest sufficient durable inputs. Do not route back by resuming the prior Build Participant's conversation.

In non-orchestrated mode, continuation fitness may still determine whether an existing healthy Build session is reused. `BUILD authority` alone is not a complete human instruction.

## Human-visible blocker signal

When a phase/Participant concludes that an **active Blocker** exists and surfaces
it to the Human, make the signal immediately noticeable:

```text
[SCOPED BLOCKER DETECTED]

Blocks: <exact affected work / milestone / contract surface>
Does not block: <safe unaffected work, or "none materially useful">
Next route: <smallest concrete resolution route>
Owner: <next-action owner>
```

Keep it simple:

- use the signal only for a real active Blocker, not for every Finding, risk,
  warning, unresolved question, or deferred item;
- the blocker may affect a narrow surface or the whole Work Unit; always state
  the exact scope;
- if safe unaffected work can continue, say so explicitly;
- do not require a matching `[NO BLOCKER]` signal when none exists;
- this is a Human-facing visibility convention, not a new protocol enum, state,
  severity, or artifact requirement.

A response may continue with normal explanation after this compact signal.

## Phase completion handoff

At a **meaningful stage/phase completion** (not every progress message), finish with a compact handoff:

```markdown
## Phase handoff
- Completed: <what reached the phase/stage exit condition>
- Artifacts: <paths written/updated; "none" if none>
- Human decision: <decision needed now; "none" if no human decision is currently required>
- Open / deferred: <non-blocking unresolved/deferred items; "none" if none>
- Recommended next step: <one concrete next action/phase>
- Session transition: <plain-language action + reason; in orchestrated mode, distinguish same-Run Session replacement from new-Run/new-Participant dispatch>
- Context pointers: <only paths/anchors the next phase is likely to need>
```

Keep **Human decision** separate from **Open / deferred**. A durable unresolved item is not enough if a person must make a decision before the next meaningful step; surface that decision explicitly at the boundary.

Keep the handoff operational. Do not repeat the phase report inside it.

If the phase already owns a structured report, the handoff points to it instead of duplicating its contents.

## Progressive disclosure rule

Before opening a reference, ask what decision/check requires it.

Good flow:

```text
canonical phase prompt
→ required phase authority
→ routing/clue map
→ matching conditional authority
→ cold reference only when a concrete ambiguity remains
```

Bad flow:

```text
enter phase
→ recursively read every README/example/retro in nearby folders
→ decide later which parts mattered
```

## Quality guardrail

Selective loading has failed if a later phase has to invent or re-litigate a material decision that the previous phase already resolved. Fix the handoff/authority path; do not normalize the re-litigation as the cost of saving context.
