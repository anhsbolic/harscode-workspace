# harscode-workspace

A portable, project-agnostic work manual for moving product intent into reliable software with AI agents. It separates **pre-engineering product-behavior discipline**, **product-design authority**, **delivery orchestration**, **engineering workflow**, **engineering knowledge**, and **harness translation** so agents can load the smallest relevant authority instead of carrying one giant prompt.

## Mental model

AI agents do not reliably compound context across sessions. Durable quality comes from controlling:

- **knowledge** — what authority is available;
- **durable state** — what survives session boundaries;
- **scope/authority** — what the active area/phase may decide or change;
- **verification** — what proves the result;
- **human gates** — where unresolved material decisions stop.

A useful routing model is:

```text
                         ┌─ pre-engineering/
                         │  when product behavior /
product/domain truth ────┤  requirement meaning is materially open
                         │
                         ├─ product-design/
                         │  when product-brand / UI / UX
                         │  authority is materially open
                         │
                         └─ engineering exploration
                            when upstream meaning is ready enough
                                  ↓
                               techplan
                                  ↓
                        build / review / testing / PR
```

`pre-engineering/` and `product-design/` are conditional sibling upstream routes, not mandatory sequential phases. Use the route that owns the unresolved question so engineering does not become accidental product or design authority.

## Structure

```text
AGENTS.md                  lightweight root router + hard rules
AUTHORING.md               standard for writing Harscode guidance itself
pre-engineering/           upstream product-behavior concretization + handoff discipline
  AGENTS.md                pre-engineering router + hard rules
  README.md                scope, authority, usage model
  commitment-route.md      depth-first commitment route
  kickoff-prompt.md        fresh-session commitment bootstrap
  control-tower.md         optional non-authoritative progress dashboard guidance
product-design/            upstream product-brand/UI/UX authority-building guidance
  AGENTS.md                product-design router + hard rules
  kickoff-prompt.md        collaborative design-discussion entrypoint
  README.md                scope, authority, usage model
  ...                      exploration/canonicalization/handoff guidance
orchestration/             pilot coordination protocol / Work Unit + Run semantics
  AGENTS.md                lightweight orchestration router
  protocol-v0.1.md         pilot-candidate coordination semantics
  run-contract.md          Work Unit / Run / Participant / Session invocation contract
workflow/                  engineering lifecycle / phase authority
  AGENTS.md                phase router
  orchestrated-run-overlay.md path/identity compatibility for orchestrated Runs
  context-management.md    context classes, handoff, session transitions
  *-prompt.md              canonical phase entrypoints
  <phase>/                 deeper phase rules/checklists/examples
best-practices/            technology/correctness knowledge base
  AGENTS.md                targeted discovery rules
  index.md                 clue map → matching best-practice files
harness-optimization/      translation into Codex/Claude/etc mechanisms
human-pairing/             Human-facing operator handbook for pairing, approvals, and session hygiene
proposals/                 one protected-guidance proposal log
```

### `pre-engineering/`

Owns reusable upstream discipline for turning project-owned Product / Domain Truth into bounded confirmed product behavior, traceable Experience + Engineering Requirements, and a durable engineering handoff.

Use it when product semantics are directionally clear but engineering would still have to invent material product behavior, state meaning, consequences, or requirements. It is conditional, does not own project Product Truth, and stops before architecture / implementation.

### `product-design/`

Owns reusable upstream decision discipline for turning product/domain truth into implementation-ready product-brand/UI/UX authority. Use it when product-brand/UI direction is materially open, design generations conflict, visual references/prototypes have unclear authority, or design readiness is uncertain.

It is **not** a mandatory per-feature engineering phase. If the target project already has sufficiently clear canonical design authority, skip product-design work and begin engineering Exploration.

### `orchestration/`

Owns **how approved work is coordinated** in the v0.1 pilot: Work Units, Runs, Roles/Specializations, Participants/Sessions, Decisions, Findings, Blockers, state, history, and control-surface semantics. It does not own project product/domain truth or replace workflow phase authority.

### `workflow/`

Owns **what must happen by engineering phase**: Exploration, Techplan, Build/Patch, Code Review, Testing, PR, plus optional domain-level sequencing/closure. When a phase is dispatched as an orchestrated Run, `workflow/orchestrated-run-overlay.md` adapts identity/read-write paths without changing the phase's canonical behavior.

### `best-practices/`

Owns **portable engineering correctness** by technology/concern. `index.md` is a clue map; agents target relevant rows/sections and then open matching authority rather than reading the whole knowledge base.

### `harness-optimization/`

Owns **translation only**: how a harness expresses existing Harscode rules using its native instruction/session/skill/sandbox mechanisms. It does not invent product, lifecycle, or engineering policy.

### `human-pairing/`

Human-facing operating guidance for working with Harscode/Orchestrator without turning the Human into the workflow prompt author. It explains approvals, corrections, Run/Session boundaries, context hygiene, and related operator practices while linking back to the canonical owning guidance.

## Product-to-engineering authority boundary

Harscode deliberately separates these reusable authority areas:

```text
product/domain truth
→ owned by the target project

pre-engineering/
→ how open product behavior becomes bounded confirmed behavior,
  traceable requirements, and durable engineering handoff

product-design/
→ how open product truth becomes coherent product-brand/UI/UX authority

workflow/
→ how engineering interprets, plans, builds, reviews, verifies, and delivers

best-practices/
→ reusable technical correctness knowledge used during that work
```

`pre-engineering/` and `product-design/` are sibling conditional routes. Either may expose a gap owned by the other; neither may silently absorb the other's authority.

This prevents existing code, prototypes, generated visuals, or old implementations from becoming accidental current authority merely because they exist.

A healthy design handoff is asymmetric:

> **Design hands off invariants and intent; engineering owns implementation mechanics.**

## Design principles

- **Quality/correctness is the floor.** Context/token reduction is useful only when outcome quality is preserved or improved.
- **Product truth before implementation convenience.** Shared guidance must not silently invent project semantics or brand decisions.
- **Single source of truth.** Link/routable authority beats repeated hand-maintained copies.
- **Evidence and authority are different.** A prototype, screenshot, generated visual, historical implementation, or prior artifact may be useful evidence without being current authority.
- **Progressive disclosure.** Load required authority first; clue maps locate conditional detail; examples/history stay cold until needed.
- **Durable artifacts over chat memory.** A fresh phase/session can reconstruct required truth from files + current source state.
- **Weight matches stakes.** Product-design work is conditional; Techplan is formal; Build is a tight loop; Review/Testing are independent verification concerns.
- **Calibrate before proliferating.** When establishing a new product/visual system, prove it on a representative slice before spreading it broadly.
- **Terse process, complete artifact.** Avoid narration/filler without weakening execution/review evidence.
- **Project-agnostic by construction.** Project-specific facts/rules belong in the target repo.

See `AUTHORING.md` for documentation-writing rules and `workflow/context-management.md` for runtime context/session rules.

## Governance

| Area | Direct edit on ordinary project task? | Change mechanism |
|---|---|---|
| `pre-engineering/` | No | root `proposals/`, `general` tier |
| `product-design/` | No | root `proposals/`, `general` tier |
| `best-practices/` | No | root `proposals/`, `general` tier |
| protected `workflow/2-techplan/` files | No | root `proposals/`, `techplan-protected` tier |
| `workflow/2-techplan/examples.md`, `retro.md` | append-only exception | direct append |
| lightweight workflow phase guidance | yes, corrected in the moment today | proposal for structural/recurring changes |
| `harness-optimization/` | No | root `proposals/`, `general` tier |

One proposal folder, one numbering sequence. See `proposals/README.md`.

`AGENTS.md` files are intentionally small routing/hard-rule surfaces. Full README/index documents are **not mandatory startup reads merely because they exist**; load their relevant sections when the active concern requires them.

## Usage

1. Make Harscode reachable from the target project and set `{HARSCODE_WORKSPACE_ROOT}`.
2. Use `{HARSCODE_WORKSPACE_ROOT}/AGENTS.md` as the routing entrypoint.
3. If product behavior / requirement meaning is materially open, use `pre-engineering/AGENTS.md` and the applicable pre-engineering guidance until a bounded commitment has a durable engineering handoff. Skip this route when product behavior is already sufficiently concrete.
4. If product-brand / UI / UX authority is materially open, use `product-design/kickoff-prompt.md` and the product-design guidance until the needed authority is implementation-ready. Pre-engineering and product-design are sibling routes; use either or both only when their owning ambiguity exists.
5. If the target project is using Orchestrator Protocol v0.1 for engineering delivery, route through `orchestration/AGENTS.md` and dispatch a Run using `workflow/orchestrated-run-overlay.md`; otherwise start the engineering task directly from the active canonical prompt under `workflow/`.
6. Optional domain-grouped projects may run domain sequencing before the first feature.
7. Run Exploration before Techplan. At Exploration completion, follow its CONTINUE/FRESH recommendation for Techplan based on observable continuation fitness; the same canonical Techplan prompt supports either.
8. Techplan synthesis produces the execution-grade contract; independent review/decomposition run only when their gates apply.
9. Build executes the Approved Techplan (plus current decomposed task when applicable) and reopens live code at recorded anchors.
10. Code Review runs independently. Findings needing code changes create a patch plan and return to Build authority.
11. Testing runs independently. It confirms existing evidence, follows exact specialized-risk evidence anchors, and returns code fixes to Build authority.
12. Create the PR from final repository state + durable evidence.
13. Optional domain-grouped projects may run domain closure after feature testing completes.

Session/context details live in `workflow/context-management.md`; do not infer same/fresh session solely from task size.

## Working-state modes

### Legacy task-path mode

Existing projects may continue using one `{TASK_PATH}` with ordinal phase folders. That structure remains supported for non-orchestrated runs.

### Orchestrated Run mode — v0.1 pilot

Projects using Orchestrator Protocol v0.1 provide explicit `WORK_UNIT_ID`, `RUN_ID`, `RUN_PATH`, and `PRIOR_ARTIFACTS` according to `orchestration/run-contract.md` and `workflow/orchestrated-run-overlay.md`.

In this mode:

```text
Work Unit identity
≠ filesystem path
≠ workflow phase
≠ Session
```

Each workflow re-entry creates a new Run and preserves earlier evidence. Filesystem ordering is not execution chronology. A dedicated Harscode Space is optional and project-defined; tiny work may rely on a lightweight Work Unit record plus commit/PR/test evidence.

Patch authority still belongs to Build/Patch even when Review or Testing discovered the finding. The requesting phase preserves its finding/patch request; the new Build Run records the production fix.

## Status

Active personal system. Harscode uses **Continuous Real-Task Validation (CRTV)**: changes are evaluated through real product/engineering work, individual executions are validation runs, and evidence from those runs drives revisions while proven quality remains the floor.

The workflow-v2 line on `main` remains the current **operational default** after two materially different real Kencleng validation runs with positive correctness/outcome evidence.

This branch adds **Orchestrator Protocol v0.1 as a Pilot Candidate**. It is not promoted operational authority yet. Kencleng Slice 2 Pilot #2 development is on Human HOLD while Post-Pilot #2 evaluation proceeds. The [Post-Pilot #2 roadmap](audits/orchestrator-v0.1-post-pilot-2-roadmap.md) owns this episode's progress, evidence, and next action; promotion to `main` awaits an explicit evidence-based decision.

## License

_(TBD)_