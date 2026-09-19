# harscode-workspace

A portable, project-agnostic work manual for moving product intent into reliable software with AI agents. It separates **product-design authority**, **delivery orchestration**, **engineering workflow**, **engineering knowledge**, and **harness translation** so agents can load the smallest relevant authority instead of carrying one giant prompt.

## Mental model

AI agents do not reliably compound context across sessions. Durable quality comes from controlling:

- **knowledge** — what authority is available;
- **durable state** — what survives session boundaries;
- **scope/authority** — what the active area/phase may decide or change;
- **verification** — what proves the result;
- **human gates** — where unresolved material decisions stop.

A useful shorthand is:

```text
product/domain truth
→ product design when materially open
→ engineering exploration
→ techplan
→ build / patch
→ code review
→ testing
→ pull request
```

Not every task needs upstream product-design work. The point is to make that boundary explicit so implementation does not become accidental product or design authority.

## Structure

```text
AGENTS.md                  lightweight root router + hard rules
AUTHORING.md               standard for writing Harscode guidance itself
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
proposals/                 one protected-guidance proposal log
```

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

## Product-to-engineering authority boundary

Harscode deliberately separates four kinds of reusable authority:

```text
product/domain truth
→ owned by the target project

product-design/
→ how open product truth becomes coherent product-brand/UI/UX authority

workflow/
→ how engineering interprets, plans, builds, reviews, verifies, and delivers

best-practices/
→ reusable technical correctness knowledge used during that work
```

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
3. If product/design authority is materially open, use `product-design/kickoff-prompt.md` and the product-design guidance until the needed authority is implementation-ready. If design authority is already sufficiently clear, skip this step.
4. If the target project is using Orchestrator Protocol v0.1, route through `orchestration/AGENTS.md` and dispatch a Run using `workflow/orchestrated-run-overlay.md`; otherwise start the engineering task directly from the active canonical prompt under `workflow/`.
5. Optional domain-grouped projects may run domain sequencing before the first feature.
6. Run Exploration before Techplan. At Exploration completion, follow its CONTINUE/FRESH recommendation for Techplan based on observable continuation fitness; the same canonical Techplan prompt supports either.
7. Techplan synthesis produces the execution-grade contract; independent review/decomposition run only when their gates apply.
8. Build executes the Approved Techplan (plus current decomposed task when applicable) and reopens live code at recorded anchors.
9. Code Review runs independently. Findings needing code changes create a patch plan and return to Build authority.
10. Testing runs independently. It confirms existing evidence, follows exact specialized-risk evidence anchors, and returns code fixes to Build authority.
11. Create the PR from final repository state + durable evidence.
12. Optional domain-grouped projects may run domain closure after feature testing completes.

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

This branch adds **Orchestrator Protocol v0.1 as a Pilot Candidate**. It is not promoted operational authority yet. Validate it through a real Kencleng delivery slice, record protocol friction/outcome evidence, remediate from evidence, and only then decide whether it should replace or extend the current `main` behavior.

## License

_(TBD)_
