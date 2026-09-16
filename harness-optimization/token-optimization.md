# Token / Output Efficiency (Harness-Agnostic)

## Scope

This file governs **output/process verbosity**. `workflow/context-management.md` separately governs what context should be loaded. Do not conflate the two.

Harness translations may enforce these rules through their own instruction mechanisms; they do not redefine them.

## Rule

Default explanatory/process narration is direct and terse:

- no filler, hedging, repeated request restatement, routine tool narration, or sign-off;
- explain material trade-offs/human gates when the explanation affects a decision;
- do not mechanically shorten code, diffs, configuration, or required structured artifacts.

Deliverables remain complete enough for their audience/next phase. Examples:

- `techplan.md` remains execution-grade for Build;
- `report-techplan.md` remains complete for human sign-off;
- review/testing findings contain enough evidence to act on;
- PR descriptions accurately reflect final diff/evidence.

**Terse process ≠ incomplete artifact.**

## Context efficiency is different

A short response does not compensate for loading irrelevant context. Likewise context compaction is not permission to lose durable decisions.

For context loading, phase handoff, same/fresh session choice, and progressive disclosure, follow `workflow/context-management.md`.

## Third-party compression tools

No generic recommendation. Evaluate per harness for measured quality/cost effect, what inputs/outputs are transformed, security/supply-chain cost, and whether required durable artifacts remain intact.
