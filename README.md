# harscode-workspace

A portable, project-agnostic work manual for AI-assisted software delivery. It separates **workflow**, **engineering knowledge**, and **harness translation** so agents can load the smallest relevant authority instead of carrying one giant prompt.

## Mental model

AI coding agents do not reliably compound context across sessions. Durable quality comes from controlling:

- **knowledge** — what authority is available;
- **durable state** — what survives session boundaries;
- **scope/authority** — what the active phase may decide/change;
- **verification** — what proves the result;
- **human gates** — where unresolved material decisions stop.

Harscode is the portable manual around those controls. Target-project truth still belongs in the target repo.

## Structure

```text
AGENTS.md                  lightweight root router + hard rules
AUTHORING.md               standard for writing Harscode guidance itself
workflow/                  lifecycle / phase authority
  AGENTS.md                phase router
  context-management.md    context classes, handoff, session transitions
  *-prompt.md              canonical phase entrypoints
  <phase>/                 deeper phase rules/checklists/examples
best-practices/            technology/correctness knowledge base
  AGENTS.md                targeted discovery rules
  index.md                 clue map → matching best-practice files
harness-optimization/      translation into Codex/Claude/etc mechanisms
proposals/                 one protected-guidance proposal log
```

### `workflow/`

Owns **what must happen by phase**: Exploration, Techplan, Build/Patch, Code Review, Testing, PR, plus optional domain-level sequencing/closure.

### `best-practices/`

Owns **portable engineering correctness** by technology/concern. `index.md` is a clue map; agents target relevant rows/sections and then open matching authority rather than reading the whole knowledge base.

### `harness-optimization/`

Owns **translation only**: how a harness expresses existing Harscode rules using its native instruction/session/skill/sandbox mechanisms. It does not invent lifecycle or engineering policy.

## Design principles

- **Quality/correctness is the floor.** Context/token reduction is useful only when outcome quality is preserved or improved.
- **Single source of truth.** Link/routable authority beats repeated hand-maintained copies.
- **Progressive disclosure.** Load required authority first; clue maps locate conditional detail; examples/history stay cold until needed.
- **Durable artifacts over chat memory.** A fresh phase/session can reconstruct required truth from files + current source state.
- **Weight matches stakes.** Techplan is formal; Build is a tight loop; Review/Testing are independent verification concerns.
- **Terse process, complete artifact.** Avoid narration/filler without weakening execution/review evidence.
- **Project-agnostic by construction.** Project-specific facts/rules belong in the target repo.

See `AUTHORING.md` for documentation-writing rules and `workflow/context-management.md` for runtime context/session rules.

## Governance

| Area | Direct edit on ordinary task? | Change mechanism |
|---|---|---|
| `best-practices/` | No | root `proposals/`, `general` tier |
| protected `workflow/2-techplan/` files | No | root `proposals/`, `techplan-protected` tier |
| `workflow/2-techplan/examples.md`, `retro.md` | append-only exception | direct append |
| lightweight workflow phase guidance | yes, corrected in the moment today | proposal only for structural/recurring changes |
| `harness-optimization/` | No | root `proposals/` |

One proposal folder, one numbering sequence. See `proposals/README.md`.

`AGENTS.md` files are intentionally small routing/hard-rule surfaces. Full README/index documents are **not mandatory startup reads merely because they exist**; load their relevant sections when the active concern requires them.

## Usage

1. Make Harscode reachable from the target project and set `{HARSCODE_WORKSPACE_ROOT}`.
2. Use `{HARSCODE_WORKSPACE_ROOT}/AGENTS.md` as the routing entrypoint.
3. Start the active phase from its canonical prompt under `workflow/`.
4. Optional domain-grouped projects may run domain sequencing before the first feature.
5. Run Exploration before Techplan. At Exploration completion, follow its CONTINUE/FRESH recommendation for Techplan based on observable continuation fitness; the same canonical Techplan prompt supports either.
6. Techplan synthesis produces the execution-grade contract; independent review/decomposition run only when their gates apply.
7. Build executes the Approved Techplan (plus current decomposed task when applicable) and reopens live code at recorded anchors.
8. Code Review runs independently. Findings needing code changes create a patch plan and return to Build authority.
9. Testing runs independently. It confirms existing evidence, follows exact specialized-risk evidence anchors, and returns code fixes to Build authority.
10. Create the PR from final repository state + durable evidence.
11. Optional domain-grouped projects may run domain closure after feature testing completes.

Session/context details live in `workflow/context-management.md`; do not infer “same session” or “fresh session” solely from task size.

## Task working directory

Each task uses one `{TASK_PATH}` in the target repo:

```text
{TASK_PATH}/
├── 1-exploration/
│   └── logs/                       durable raw evidence / code anchors / solutioning
├── 2-techplan/
│   ├── techplan.md                 authoritative execution-grade spine
│   ├── report-techplan.md          generated after Approval; human-facing digest
│   └── tasks/                      optional decomposition task files + manifest
├── 3-build/
│   ├── report.md
│   └── patch-report-<n>.md
├── 4-code-review/
│   ├── review-findings-<n>.md
│   └── patch-plan-<n>.md
├── 5-testing/
│   ├── testing-report-<n>.md
│   └── patch-plan-<n>.md
└── 6-pull-request/
    └── pr-description.md
```

Patch rule: **production patches are executed/reported in `3-build/` regardless of which independent phase requested them.** Review/Testing keep the finding/patch-plan request, preserving authority separation.

For domain-grouped projects, `{DOMAIN_PATH}` may additionally contain `_domain-manifest.md` and `_domain-closure-review.md`; feature-by-feature projects have no domain-level artifacts.

## Status

Active personal system. Harscode uses **Continuous Real-Task Validation**: changes are evaluated through real engineering tasks, individual executions are **validation runs**, and evidence from those runs drives revisions while proven quality remains the floor.

## License

_(TBD)_
