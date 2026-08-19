# proposals/

> Location: `harscode-workspace/proposals/` — root level, sibling to
> `best-practices/` and `workflow/`. Deliberately not nested under either,
> so it can serve both.

## Scope

- **Covers today:** all of `best-practices/` — `index.md` and every file
  under every category folder are fully protected; the agent cannot edit
  any of them directly, not even append.
- **Available for, not yet used by:** `workflow/{exploration,code-review,testing,pull-request}`.
  These currently stay lightweight — no protected files, no proposal
  process, corrected in the moment (see `workflow/AGENTS.md`). If one of
  them ever needs formal protection, it uses this mechanism rather than
  inventing a new one.
- **Does NOT cover:** `workflow/techplan/`. That has its own dedicated
  `proposals/` (`workflow/techplan/proposals/`), already proven across
  three accepted proposals, with its own stricter threshold (2+ stories
  or a genuinely structural gap) appropriate to techplan's contract-level
  stakes. Not migrated or consolidated here — techplan keeps its own.

## Threshold

Looser than `techplan/proposals/`. `best-practices/` is knowledge content
refined over time, not a contract a lead signs off on — so a single
well-evidenced gap is enough to propose. Worst case if a proposal is
weak: it gets reviewed and rejected, no execution risk.

## What warrants a proposal

- A pattern that caused a real bug/incident and isn't covered by any
  existing `best-practices/` file
- A real-world case worth attaching to an existing file (goes in as a
  proposal to append to that file's `examples.md`)
- An existing file's Bad/Good example turns out wrong, outdated, or
  contradicted by a real case
- A new concern that doesn't fit any existing category (e.g. proposing a
  new folder, as happened with this workspace's first `infra/`/`pwa/`
  additions)
- (If ever applicable) a recurring gap in one of the lightweight
  `workflow/` phases that's outgrown "corrected in the moment"

## Proposal file format

`proposals/000X-<short-slug>.md`

```markdown
# 000X — <short title>

**Status:** Proposed
**Date:** YYYY-MM-DD
**Triggered by:** <story/task that surfaced this>
**Target area:** best-practices | workflow/<phase>
**Target file(s):** <path(s) relative to workspace root, or "new file: <path>">

## Gap found
<what's missing, wrong, or outdated — be specific>

## Proposed change
<the actual content to add/change — write it as it should appear in the
target file, not just a description of the change>

## Rationale
<why this belongs where you're proposing it — is it genuinely generic
(for best-practices/), or does it risk being project-specific creeping in?>
```

## After review

Human either:
- Merges the proposed content into the target file(s), updates
  `best-practices/index.md` (row + Security Concern Map entry if
  applicable) if the target is `best-practices/`, then marks the
  proposal `Status: Accepted`
- Marks it `Status: Rejected` with a one-line reason, left in place for
  historical record — never deleted

Proposals are never auto-merged, regardless of how well-evidenced they
appear.