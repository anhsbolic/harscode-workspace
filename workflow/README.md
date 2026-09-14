# Workflow

Portable guidance for moving one piece of work from understanding → executable plan → implementation → independent review/testing → delivery. Generated task artifacts live in the target project, not this workspace.

Use `AGENTS.md` as the lightweight router. Use this README for cross-phase/governance rationale; ordinary phase execution starts from the canonical phase prompt.

## Lifecycle

```text
(optional domain sequencing)
Exploration
→ Techplan synthesis
→ optional independent Techplan review
→ optional Techplan decomposition
→ Build / Patch
→ Code Review
→ Build / Patch when findings require code changes
→ Testing
→ Build / Patch when testing finds code defects
→ Pull Request
(optional domain closure)
```

Phase weight is intentionally uneven. Techplan is a high-stakes execution contract; Build is a tight execution loop; Review/Testing are independent verification concerns. Do not copy ceremony from one phase into another merely for symmetry.

## Context and session boundaries

`context-management.md` is the source of truth for:

- Required / routing / conditional / cold context;
- durable artifacts vs chat memory;
- same-session vs fresh-session continuation fitness;
- default phase-transition intent;
- code anchors;
- Build ownership of patches;
- compact phase-completion handoff.

Key principle: **smallest sufficient context that preserves correctness**. A fresh session re-grounds from durable state; a same session may reuse active, unchanged context without mechanically rereading it.

The default transition intent is not “one session per phase” and not “one session for the feature.” Exploration → Techplan is adaptive; Build, Review, and Testing retain authority/independence boundaries. See `context-management.md` instead of duplicating the matrix here.

## Domain-grouped projects (optional)

Projects that explicitly group planned work by domain may use:

- `0-domain-sequencing-prompt.md` before choosing the first feature;
- `7-domain-closure-prompt.md` after the domain's feature work completes testing.

Feature-by-feature projects skip both. “Domain” describes planning/work grouping, not Domain-Driven Design.

## Governance

### Protected Techplan guidance

These `2-techplan/` files are proposal-gated:

- `template.md`
- `rules.md`
- `guardrails.md`
- `guidelines.md`
- `diagram-guidelines.md`
- `report-template.md`

`examples.md` and `retro.md` are append-only exceptions. Stable recurring lessons should graduate into protected rules instead of becoming required historical reading.

### Lightweight phases

`1-exploration/`, `3-build/`, `4-code-review/`, `5-testing/`, and `6-pull-request/` have no protected core today. Correct small issues in place; use the root proposal process only when a structural/recurring change warrants it.

### Proposal system

All proposals live under root `proposals/` with one numbering sequence and the applicable protection tier. See `proposals/README.md`.

### Authoring Harscode itself

Use root `AUTHORING.md`: correctness density, one source of truth, direct prose, progressive disclosure, explicit invocation semantics, and soft—not hard—document-size review thresholds.

## Cross-stage source of truth

Later phases consume earlier durable artifacts selectively. They do not copy them wholesale and do not treat remembered chat context as authority.

Examples:

- Build executes the Approved Techplan + current task slice (when decomposed) and reopens live code at recorded anchors.
- Code Review judges the current diff against the contract/current repo, not the Build session's memory.
- Testing starts from the current Techplan + latest build evidence and follows exact Test Focus evidence anchors when specialized context is needed.
- PR truth comes from final repository state + final evidence, not planned changes that never landed.

## What's Explicitly Out of Scope Here

Project-specific codebase conventions and product/domain truth belong in the target repo, not Harscode. This heading is retained as an addressable compatibility anchor for accepted historical proposals; current layering details live under `Canonical phase prompts` below.

## Phase convergence

A phase is sufficient when the next phase can proceed without inventing a material product/domain, authority/security, architecture/ownership, interface/data, risk, or verification decision.

Once that holds, stop polishing mechanical detail. If a later phase encounters such a missing decision anyway, it stops/reports back rather than inventing the answer.

Techplan independent review applies the concrete convergence rule in `2-2-techplan-review-prompt.md`.

## Canonical phase prompts

Where a root `*-prompt.md` exists, it is the default invocation surface:

| Concern | Canonical entry |
|---|---|
| Domain sequencing (optional) | `0-domain-sequencing-prompt.md` |
| Exploration | `1-exploration-kickoff-prompt.md` |
| Techplan synthesis | `2-1-techplan-synthesis-prompt.md` |
| Techplan independent review | `2-2-techplan-review-prompt.md` when its gate applies |
| Techplan decomposition | `2-3-techplan-decomposition-prompt.md` when its gate applies |
| Build / Patch | `3-build-prompt.md` |
| Code Review | `4-code-review-prompt.md` |
| Testing | `5-testing-prompt.md` |
| Pull Request | `6-pull-request/` guidance (no root prompt today) |
| Domain closure (optional) | `7-domain-closure-prompt.md` |

Harness wrappers route to these prompts; they do not maintain stack/project copies of lifecycle policy. Stack correctness comes from matching `best-practices/`; project truth comes from the target repo; model/client/tool selection belongs to execution profiles/harness configuration.

## Path variables

- **Project-level:** `{HARSCODE_WORKSPACE_ROOT}`, `{CODEBASE_CONTEXT}`, target convention path. Set/reuse these per target project without restating the project into Harscode.
- **Task/run-level:** `{TASK_PATH}`, `{TASK}`, ticket/area, diff, entry point, etc.

Deep project understanding comes from reading target-repo authority, not from expanding `{CODEBASE_CONTEXT}` into a copied project description.

## Response style

Two independent axes:

1. **Process narration** — default direct/terse. Explain reasoning where a human gate or material trade-off needs it; do not narrate routine reads/tool calls/obvious execution.
2. **Deliverable completeness** — stays high. A terse process can still owe a complete Techplan, finding, build report, test report, or PR description.

Planning artifacts are not licenses for verbose narrative. They preserve decisions, evidence, rationale that controls execution, and unresolved material questions. See `context-management.md` for the compact phase handoff.

## Prompt file shape

Canonical prompts use a predictable shape without forcing filler headings:

1. title + short purpose;
2. `## Inputs required before running` — an invocation contract, not a placeholder inventory. For each non-obvious input, state what it represents, its valid source/form, relevant project/task/round scope, and any precondition/authority limitation needed to avoid guessing. Bare variable names are not a brevity target;
3. `## Prompt` with the runnable instruction;
4. phase-specific output/rules only when needed;
5. `## Notes` last.

A prompt should route to deeper authority rather than copying it, but routing must not make the prompt skeletal: a fresh agent still needs enough local semantics to invoke the phase safely. When adding or revising a prompt, follow this shape and root `AUTHORING.md` rather than copying the nearest sibling's historical quirks.
