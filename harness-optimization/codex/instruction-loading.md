# Instruction Loading (Codex)

## Authority mapping

```text
target-repo product/domain/project rules
→ target repo hierarchical AGENTS.md + canonical project sources

portable lifecycle/process
→ Harscode workflow/ canonical phase prompt + routed context

portable engineering correctness
→ Harscode best-practices clue map → matching authority
```

Codex's hierarchical project instructions make another giant always-loaded policy file unnecessary.

## Always-loaded project instructions

Keep target-repo `AGENTS.md` focused on what must govern nearly every task in that scope:

- hard safety/write/protected-path rules;
- authoritative local commands;
- directory/scope boundaries;
- concise routes to project canonical sources and Harscode entrypoints.

Move rationale, long examples, architecture/design explanation, and full workflow procedures to their owners and load them on demand.

Useful test:

> Does Codex need this before almost every task in this scope, or only when a specific concern is active?

If concern-specific, route/progressively disclose it.

## Harscode integration

Do not put a blanket instruction such as “read the whole Harscode README/index first.” Route by concern:

```text
workflow task
→ {HARSCODE_WORKSPACE_ROOT}/workflow/AGENTS.md
→ applicable canonical workflow/*-prompt.md
→ only context the prompt/trigger requires

engineering best practice
→ {HARSCODE_WORKSPACE_ROOT}/best-practices/AGENTS.md
→ targeted search/scan of index.md for active stack/concern
→ matching best-practice file(s)
```

For same/fresh sessions and re-grounding, follow `workflow/context-management.md` via `session-boundaries.md`.

## Overrides / fallback filenames

Use `AGENTS.override.md` only for intentional local/operator overrides, not as an overflow file for a bloated baseline.

Use additional project-document fallback filenames only to recognize an existing legitimate instruction surface. Do not create `CODEX.md` simply because configuration allows it.

## Conflict handling

When instruction sources conflict:

1. apply normal Codex instruction precedence;
2. identify the legitimate semantic owners;
3. surface a real source-of-truth contradiction instead of choosing whichever rule makes the task easier.

Harness translation never overrides target project/domain authority.

## Context-budget check

Before adding persistent instruction text, ask whether it is already owned elsewhere, whether it can be routed conditionally, and whether its scope can be narrower. Goal: smallest **complete always-needed** instruction surface, not smallest file at any cost.
