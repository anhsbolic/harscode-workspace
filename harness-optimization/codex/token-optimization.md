# Token / Output Efficiency (Codex)

## Authority

- Output/process rule: `harness-optimization/token-optimization.md`
- Context-loading/session rule: `workflow/context-management.md`

This file only translates those rules into Codex placement/behavior.

## Placement

Install the compact output rule once at the intended scope (dedicated Codex profile developer instructions, user-level instruction surface, or target-project `AGENTS.md`). Do not duplicate it across profile + user + project + skills.

Compact translation:

```md
Default process/explanatory narration is direct and terse: no filler,
hedging, repeated request restatement, routine tool narration, or sign-off.
Do not compress required code/diff/config/artifact content. Techplans,
review/testing findings, human reports, and PR descriptions remain complete
for their audience/next phase.
```

## Context behavior

Codex compaction can manage long sessions, but it does not change durable-state requirements. When continuation fitness is poor, prefer a fresh session re-grounded from the smallest sufficient artifacts instead of relying on an opaque compacted summary.

Skills/wrappers should route to canonical Harscode prompts and conditional sources; they should not preload every related README/example/retro.

## What not to do

- Do not globally force minimal deliverables.
- Do not treat output verbosity controls as a substitute for context routing.
- Do not install third-party compression tools without measuring quality/cost/security impact.
- Do not duplicate the same persistent instruction across multiple Codex surfaces.
