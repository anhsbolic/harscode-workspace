# token-optimization.md (Codex)

## What this translates

The authoritative cross-harness rule remains:

```text
harness-optimization/token-optimization.md
```

This file only explains where that already-decided rule should live in Codex so it applies consistently without being duplicated across every skill or project document.

## Codex placement

Use **one persistent instruction surface** for the rule, chosen according to the intended scope.

### Harness-wide / dedicated Harscode Codex profile

When a dedicated Codex profile is used for Harscode-driven development, place the rule once in that profile's persistent developer-instruction configuration.

Current Codex configuration exposes `developer_instructions` for additional persistent instructions. Re-verify the concrete config key/placement against the current Codex version before copying an example into a real machine config.

### User-wide

If the rule should apply to all Codex work for one user, a user-level `$CODEX_HOME/AGENTS.md` is an appropriate instruction surface.

### Project-only

If the rule should apply only inside one target repository, place the translation once in the appropriate project `AGENTS.md` scope.

Do not install the same token rule in `developer_instructions`, user `AGENTS.md`, project `AGENTS.md`, and skills simultaneously. Duplicate persistent copies create drift and spend context budget without adding authority.

## Translation snippet

Use the following as a compact translation of the root Harscode rule:

```md
Default explanatory/process narration is terse:
- no filler, hedging, restating the request, or sign-off;
- this does not compress code, diffs, configuration, or structured artifact content itself.

Full completeness is required whenever output:
1. crosses an audience boundary into human-facing/reviewer-facing content
   such as a Summary/Digest, risk note, PR description, or equivalent
   substitute for the full underlying detail; or
2. is inside a section governed by a formal named Harscode self-check
   checklist.

When uncertain whether an exception applies, read the current
`harness-optimization/token-optimization.md`; this instruction translates
that rule but does not replace it.
```

If the underlying Harscode rule changes through its own proposal process, update this translation instead of independently editing the snippet's semantics.

## Why this is not a Skill

The token rule is a cross-cutting default behavior with structural exceptions. It is not a task that should trigger only when a semantic description matches.

Putting it in a Skill risks the exact failure the root rule is meant to avoid: the rule would be absent until the skill happens to trigger.

Skills may themselves follow this rule, but they are not its authority or primary enforcement surface.

## Why not globally force minimal deliverables

Codex may expose model/output/reasoning controls that can reduce verbosity or cost. Those controls are not a substitute for Harscode's distinction between **process narration** and **deliverable completeness**.

A terse Build loop can still owe a complete build report. A concise session can still owe a complete PR description or self-check-guarded section.

Do not configure a global response/output constraint so aggressively that it causes required human-facing or self-check-guarded content to omit material detail.

## Third-party compression tools

This file makes no recommendation to install a third-party output/context compression tool.

Such a tool is an empirical, fast-moving harness decision and should be evaluated separately for:

- measured token/cost effect;
- task-quality impact;
- which Codex inputs/outputs it actually intercepts;
- supply-chain/security cost;
- whether it understands Harscode's completeness exceptions.

Do not infer a Codex recommendation from the dated Claude Code tool verdicts in the sibling harness directory.

## Context compaction is a different concern

Codex may compact/summarize long-running context as part of its own agent loop. That mechanism helps manage context growth; it does not change the Harscode rule about what the final artifact/output must contain.

A compacted internal context is acceptable only if the durable task artifacts and final deliverables still preserve the information the active Harscode phase requires.

## Verification checklist

- [ ] The root Harscode token rule is still the semantic source of truth.
- [ ] Exactly one persistent Codex instruction surface owns this translation for the intended scope.
- [ ] The rule does not depend on a Skill triggering.
- [ ] Code/diff/config/artifact content is not mechanically shortened by the narration rule.
- [ ] Human-facing and self-check-guarded outputs remain complete.
- [ ] Any concrete Codex config key used in a target setup has been re-verified against the current Codex release.
