# 0024 — Claude Code backend track: slash commands + subagent phase mapping

**Status:** Accepted
**Date:** 2026-09-10
**Protection Tier:** general
**Triggered by:** Real usage gap on a live project (koperasiqu-web-app, backend track) — every phase prompt in `workflow/` was being copy-pasted by hand into a fresh Claude Code session, and all four to five phases of one feature (exploration, techplan, build, patches) were being run inside a single session, contrary to this workspace's own context-isolation framing
**Target area:** harness-optimization
**Target file(s):**
- New: `harness-optimization/claude-code/backend/slash-commands.md`
- New: `harness-optimization/claude-code/backend/subagents.md`
- Depends on 0009/0010 (frontend track, same mechanisms) already being Accepted

## Gap found

0009 and 0010 translated `workflow/`'s phase prompts and the "amnesiac
contractor" framing into Claude Code slash commands and subagents, but
scoped to the frontend track only (`claude-code/frontend/`). Backend
track had no equivalent — in practice this meant:

1. No native way to kick off a phase other than opening the relevant
   `*-prompt.md` file and pasting its contents by hand into a new
   session, every single time.
2. No structural boundary between phases within a feature — a real
   task on koperasiqu-web-app (`D01-01-registrasi-dan-verifikasi-email`)
   ran exploration (12 log files), techplan synthesis, decomposition,
   the initial build, and 9 rounds of patches all inside one
   continuously-growing session, which is exactly the failure mode
   `subagents.md`'s Tier 2 rationale (0010) already names: a planning-
   type phase's full reasoning trail has no reason to still be resident
   in context once an execution-loop phase (build) begins.

## Proposed change

**`backend/slash-commands.md`**: same pattern as `frontend/
slash-commands.md` (0009) — one command per phase (`/explore`,
`/techplan`, `/build`, `/code-review`, `/test`), plus one additional
command, `/domain-sequence`, for the new pre-exploration domain-level
sequencing pass added by Proposal 0026.
Command bodies stay pointers into `workflow/`'s files, same discipline.

**`backend/subagents.md`**: same pattern as `frontend/subagents.md`
(0010) — one subagent per phase (`explorer`, `techplan-writer`,
`builder`, `code-reviewer`, `tester`), each scoped to the minimum tool
list that phase needs. This is where the backend translation genuinely
differs from frontend, justifying a separate file per
`harness-optimization/README.md`'s track-split rule rather than reusing
frontend's file verbatim:

- Backend's `builder` subagent needs `Bash` for framework-specific
  commands (migrations, artisan-equivalent tooling, running the test
  suite as part of the build loop) that frontend's build subagent may
  not need in the same way.
- Backend carries a project-specific hard constraint frontend does not:
  koperasiqu-web-app's `AGENTS.md` § 3 File-Path Fencing (Tier 0) names
  specific backend paths (PII encryption trait, blind-index mechanism,
  permission seeder, incentive/bonus ledger locking logic) that no
  subagent should touch without an explicit, session-specific ask from
  Anhar. `backend/subagents.md` states this as a generic *pattern*
  (every backend subagent's system prompt must reference whatever its
  target repo's own `AGENTS.md` § File-Path Fencing section declares,
  the same "translate an existing rule, don't invent a new one"
  discipline `hooks-protected-files.md` already uses for
  harness-optimization's own protected paths) — it does not hardcode
  koperasiqu-web-app's specific fenced paths, keeping the file
  project-agnostic per this tree's own construction rule.
- Model routing differs: `best-practices/model-routing.md`'s "Backend
  build" row is scoped to Go and explicitly flagged in that same table's
  fallback-mapping section as not directly validated for other backend
  languages. `backend/subagents.md` inherits that caveat explicitly
  rather than silently presenting a Go-benchmarked pick as
  language-neutral.

## Rationale

This is a replication of an already-Accepted mechanism (0009/0010) to a
second track, not a new mechanism — the risk profile is lower than the
original frontend adoption, since the pattern itself (pointer-only
command bodies, tool-scoped subagents, explicit context handoff via file
path) is already validated. It's proposed as one combined Tier 1+Tier 2
change rather than split across two proposals (as 0009/0010 were)
because the original tiered rollout was about sequencing risk for a
*first-time* adoption of these mechanisms; replicating a proven pattern
to a second track doesn't carry that same first-time risk.

Both files stay project-agnostic by construction: neither references
koperasiqu-web-app by name in its reusable pattern content, only in this
proposal's own "Gap found" framing (which is allowed to be concrete,
per 0008/0009/0010's own precedent).
