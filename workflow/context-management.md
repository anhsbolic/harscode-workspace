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

Correctness must be reconstructable from durable artifacts plus current source-of-truth files. A phase may reuse context already loaded in the same healthy session, but a required decision cannot exist only in remembered conversation.

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

## Same session vs fresh session

Use **continuation fitness**, not a fuzzy task-size label.

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
| Exploration → Techplan | **Adaptive** — continue or fresh based on continuation fitness |
| Techplan → Build | **Fresh preferred** — Build needs the locked contract + live code, not exploratory reasoning |
| Build iteration → Build iteration | **Continue** while focused |
| Build → Code Review | **Fresh** for independent inspection |
| Code Review → Patch | **Build authority**; continue prior Build if healthy, otherwise fresh Build re-grounded on the patch plan |
| Build/Patch → Testing | **Fresh** for independent verification |
| Testing → Patch | **Build authority**; continue prior Build if healthy, otherwise fresh Build re-grounded on the patch plan |
| Testing → PR | **Flexible**; ground on final repository state + durable evidence |

Fresh for **independence** and fresh for **context hygiene** are different reasons. Record the actual reason.

`CONTINUE`, `FRESH`, and `BUILD authority` are portable routing semantics. Human-facing handoffs should translate them into an explicit action sentence instead of exposing only the enum. Examples:

```text
Continue Techplan synthesis in this session because Exploration context remains focused and current.
Start a fresh Code Review session because reviewer independence is part of the next phase's value.
Return to the existing Build session because the patch is narrow and implementation context remains focused.
Start a fresh Build/Patch session re-grounded on the patch plan because the previous Build session is stale/compacted.
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

The handoff back to Build should tell the operator whether to reuse the existing Build session or start a fresh Build/Patch session, based on continuation fitness. `BUILD authority` alone is not a complete human instruction.

## Phase completion handoff

At a **meaningful stage/phase completion** (not every progress message), finish with a compact handoff:

```markdown
## Phase handoff
- Completed: <what reached the phase/stage exit condition>
- Artifacts: <paths written/updated; "none" if none>
- Human decision: <decision needed now; "none" if no human decision is currently required>
- Open / deferred: <non-blocking unresolved/deferred items; "none" if none>
- Recommended next step: <one concrete next action/phase>
- Session transition: <plain-language continue/fresh/return-to-Build action + reason>
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
