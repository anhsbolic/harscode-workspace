# instruction-loading.md (Codex)

## What this translates

Harscode separates three kinds of truth:

```text
project-specific rules and routing
→ target repo

portable lifecycle/process guidance
→ workflow/

portable engineering correctness
→ best-practices/
```

Codex already has a native hierarchical instruction mechanism. The translation goal is therefore **not** to create another Codex policy document; it is to use the hierarchy without collapsing those source boundaries.

## Current Codex behavior this pattern relies on

As verified 2026-09-13, Codex aggregates instruction sources including:

- user/Codex-home `AGENTS.override.md` and `AGENTS.md`;
- project instruction files from the Git/project root toward the current working directory;
- configured fallback project-document filenames;
- configured skill metadata.

More-specific project instructions are layered later. The project-document path is bounded by a default context budget, so always-loaded instruction size is not free.

## Target-repo pattern

Use root `AGENTS.md` for only the material that must always govern work in the repository:

- hard safety/correctness rules;
- write/protected-path fencing;
- authoritative local commands;
- directory/scope boundaries;
- concise routing to project canonical docs;
- concise routing to Harscode lifecycle/best-practice sources.

Use nested `AGENTS.md` only where a subtree genuinely needs additional or more-specific rules.

Move rationale, long examples, detailed architecture, visual-system explanation, and full workflow procedures into the source that owns them, then route to that source.

A useful test is:

> Would Codex need this sentence before almost every task in this scope, or only when a specific concern is active?

If it is concern-specific, prefer routing/progressive disclosure over always-loaded prose.

## Harscode integration

Do not paste Harscode workflow files wholesale into project `AGENTS.md`.

A target repo should be able to say, in compact form:

```text
feature lifecycle / generic phase responsibilities
→ {HARSCODE_WORKSPACE_ROOT}/workflow/README.md

portable engineering guidance
→ {HARSCODE_WORKSPACE_ROOT}/best-practices/index.md
```

Then the active phase/task loads only the smallest relevant Harscode material.

The target repo remains authoritative for its own domain/product/architecture rules. Harscode remains authoritative for the portable concern it owns.

## `AGENTS.override.md`

Treat `AGENTS.override.md` as an explicit override mechanism, not the normal home for baseline project governance.

Good uses are genuinely temporary/local/operator-specific overrides where overriding the normal hierarchy is intentional and visible.

Do not use an override file merely because the root `AGENTS.md` became too large. If the root file is bloated, compact it and move detail to canonical/on-demand sources instead.

## `project_doc_fallback_filenames`

Codex can be configured to recognize additional project-document filenames.

Use this as a compatibility bridge for a repository that already has a legitimate instruction file under another name. Do not introduce a new `CODEX.md` (or similar) solely because the option exists.

A fallback filename that duplicates `AGENTS.md` creates two independent sources that can drift.

## Conflict handling

When two instruction sources appear to conflict on the same concern:

1. apply Codex's normal instruction precedence;
2. identify whether the conflict is actually between two legitimate owners;
3. surface a real source-of-truth contradiction instead of silently choosing whichever rule makes the current task easier.

Harness translation must not be used to override project/domain authority.

## Context-budget check

Before adding always-loaded instruction text, ask:

- Is this already stated in `workflow/`, `best-practices/`, or a target-repo canonical doc?
- Can the root/nested `AGENTS.md` point there instead?
- Is this rule scoped to only one subtree?
- Could a Skill load this only when relevant?

The goal is not the smallest possible `AGENTS.md`; it is the smallest **complete always-needed** instruction surface.
