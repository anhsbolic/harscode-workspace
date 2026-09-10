# 0026 — Domain-level sequencing pre-flight (new phase 0, before exploration)

**Status:** Accepted
**Date:** 2026-09-10
**Protection Tier:** general
**Triggered by:** Real usage gap on koperasiqu-web-app's backend track — every feature within a domain (e.g. `D01-01` through `D01-09`) was being worked strictly serially, one full exploration-through-testing cycle at a time, with no point in the process where cross-feature parallel-safety was ever actually evaluated. The one existing mechanism that answers a similar question — `2-3-techplan-decomposition-prompt.md`'s dependency graph — only runs *after* a single feature's techplan is already locked, so it can say "these two tasks inside this one feature are parallel-safe" but has no scope to say "these two *features* in the same domain are parallel-safe"
**Target area:** workflow (lightweight — see 0025's note on why this is proposed anyway)
**Target file(s):**
- New: `workflow/0-domain-sequencing-prompt.md`
- `workflow/AGENTS.md` — one new hard-rule bullet
- `README.md` (root) — new step in `## Usage` (before the current step 3), `### Task Working Directory Structure` gets a new `{DOMAIN_PATH}` subsection. (`## Structure`'s top-level tree already omits every other root-level `*-prompt.md` file for brevity — left as-is, not made inconsistent by singling this one out.)

## Gap found

Two mechanisms already exist that are adjacent to this but don't cover
it:

1. **Per-task decomposition** (`2-3-techplan-decomposition-prompt.md`)
   — runs after one feature's techplan is `Approved`, splits *that
   feature's* work into parallel-safe vs. sequential task files. Scope
   is one `{TASK_PATH}`, never crosses into a sibling feature.
2. **Per-task shared-infra exploration** (an existing exploration lens,
   evidenced in practice by files like a task's `1-exploration/logs/
   02-fenced-shared-infra.md`) — surfaces shared/fenced infrastructure
   concerns, but scoped to justifying *that one feature's* design
   against already-fenced infra, not to comparing it against a sibling
   feature that hasn't been explored yet.

Neither answers "given a domain with N planned features, which of them
can be explored/built in parallel sessions, and which must wait on
another" — a question that has to be answered *before* picking which
feature to start next, not after any of them have a techplan.

## Proposed change

New file, `workflow/0-domain-sequencing-prompt.md`, numbered `0` to
signal it runs before `1-exploration/`. Follows the standard prompt-file
shape (`workflow/README.md` § Prompt File Shape).

Key points of its content:

- **When to use:** once per domain, before the first feature in that
  domain gets its first exploration session — not once per feature. If
  the domain's manifest already exists and no new feature has been
  added to the domain's planned scope since, skip re-running this.
- **What it reads:** whatever enumerates the domain's planned features
  (a roadmap/spec doc, or existing placeholder task folders) —
  generalized as `{DOMAIN_SPEC}` alongside the existing `{TASK_PATH}`-
  style variables.
- **What it must not do:** does not replace per-feature decomposition —
  it reasons at the shared-resource/fencing grain (same table, same
  service, same file-path-fencing-tier path touched by more than one
  planned feature), not at rule-level implementation detail, since most
  features in scope won't have an exploration or techplan yet at this
  point.
- **Explicit lower-confidence caveat:** unlike the post-techplan
  decomposition graph, this pass runs before any of the domain's
  features have been explored, so its dependency graph is necessarily
  coarser and more provisional. States this directly rather than
  presenting the same confidence level as the decomposition manifest.
  Revisit/regenerate it if a feature's own exploration later surfaces a
  cross-feature dependency this pass missed.
- **Splitting/grouping vocabulary:** reuses the same axis options and
  "hard dependency" vs. "no hard dependency" language as
  `2-3-techplan-decomposition-prompt.md` § 2, for consistency between
  the two manifests rather than inventing new terms for the same kind
  of graph at a different grain.
- **Output:** `{DOMAIN_PATH}/_domain-manifest.md` (new convention, see
  below) — the domain's feature list, the dependency/parallel-safety
  graph between them, and explicit call-outs of any target repo's
  File-Path-Fencing-Tier-0-class overlaps between features (referenced
  generically — this file doesn't invent or hardcode any specific
  repo's fenced paths, same discipline `harness-optimization/claude-
  code/backend/subagents.md`, Proposal 0024, already follows for the
  same reason).

Root `README.md` changes:

- `## Usage` gets a new step inserted before the current step 3
  ("Start a task in `1-exploration/`..."), the rest renumbered:
  > Before the first feature in a new domain, run
  > `workflow/0-domain-sequencing-prompt.md` once to produce that
  > domain's `_domain-manifest.md` — it tells you which of the domain's
  > planned features can run in parallel sessions and which must wait on
  > another. Skip this for a domain's 2nd+ feature once the manifest
  > already exists and nothing new has been added to scope.
- `### Task Working Directory Structure` gets a preceding
  `{DOMAIN_PATH}` note: `{DOMAIN_PATH}` is the parent directory holding
  every feature's `{TASK_PATH}` within one domain; `_domain-manifest.md`
  (leading underscore, sorts before every feature folder) is the only
  file that lives directly under `{DOMAIN_PATH}` rather than inside a
  specific feature's `{TASK_PATH}`.

`workflow/AGENTS.md` gets one new bullet under Hard rules:

```markdown
- Before the first feature session in a new domain, run
  `0-domain-sequencing-prompt.md` and produce `{DOMAIN_PATH}/
  _domain-manifest.md` before picking which feature to start. Don't
  default to strict serial order across a domain's features without
  having checked this.
```

## Rationale

Generic across any project using this workflow — "which of a domain's
planned features are parallel-safe" is a question every multi-feature
domain eventually needs answered, not something specific to
koperasiqu-web-app. Deliberately modeled on
`2-3-techplan-decomposition-prompt.md`'s already-proven shape
(gate question, dependency-graph vocabulary, snapshot-not-living-
document caveat) rather than inventing new structure, for the same
reason 0025 generalizes 0010's subagent reasoning instead of restating
it differently.

Proposed (rather than a direct "corrected in the moment" edit) for the
same reason given in 0025: the change is structural — a new prompt
file, a new step in the root `README.md`'s numbered list, a new
directory-structure convention — not a single guideline correction.
