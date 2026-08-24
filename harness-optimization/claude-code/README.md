# claude-code/ — Claude Code harness translations

**Effective as of:** Claude Code CLI, native installer (`claude --version`
reporting 2.1.x line), August 2026
**Last verified:** 2026-08-23
**Re-verify:** recommended every ~2-3 months, or immediately if Claude
Code ships a major change to how hooks, subagents, or skills work —
these mechanics have already changed within single-digit-week windows
during 2026 (see e.g. corrections to hook-blocking behavior documented in
third-party hook guides current as of this writing).

## What lives here

Translations of `workflow/`, `best-practices/`, and
`harness-optimization/token-optimization.md` into Claude Code's native
mechanisms: slash commands, skills, subagents, hooks. See
`../README.md` for the translation-only discipline this all follows.

## Files

- `token-optimization.md` — how the root token-optimization rule is
  enforced in Claude Code, plus dated verdicts on third-party
  token-compression tools evaluated so far
- `frontend/` — track-specific translations (subagents, hooks, skill
  wrapping) where the translation genuinely differs by track; nothing
  track-agnostic is duplicated here — see `frontend/README.md` if present,
  or the individual files' own scope notes