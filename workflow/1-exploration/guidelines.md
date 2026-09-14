# Exploration Guidelines

Exploration produces durable evidence under `{TASK_PATH}/1-exploration/logs/` before Techplan synthesis. Output shape stays flexible; evidence quality matters more than a fixed file template.

## Stage 1 — Plan announcement

Before deep implementation inspection:

- state the task understanding;
- identify relevant areas, order, and reason;
- stop for human confirmation.

This checkpoint prevents expensive investigation of the wrong scope.

## Stage 2 — Gap analysis

For each area:

1. inspect current live source/behavior deeply enough to state what exists;
2. trace the relevant requirement to its actual source;
3. write the concrete gap;
4. run the five sniffing lenses from `sniffing-checklist.md`;
5. record **code anchors** for later phases: `path + symbol/section + why relevant`.

Code anchors are coordinates, not frozen truth. Do not copy routine code bodies just so Build can avoid reopening current code later.

Do not develop solution options yet. Progress updates can be terse and non-blocking after each area.

## Stage 3 — Solutioning

After the human confirms Stage 2, evaluate solution options/trade-offs. Record:

- chosen material direction;
- material rejected alternatives and why;
- consequences/risks;
- unresolved external questions.

This durable decision evidence lets Techplan synthesis preserve the outcome without depending on remembered chat discussion.

## Completion handoff

At Stage-3 completion use `workflow/context-management.md`'s compact handoff. Recommend Techplan CONTINUE/FRESH using observable continuation fitness, not a Small/Medium/Heavy label.

## What not to do

- Do not produce a Techplan-shaped contract prematurely.
- Do not duplicate target-project conventions into Harscode-shaped prose.
- Do not compress away concrete Stage-2 evidence merely to save context; downstream phases reduce read amplification through routing/anchors, not by destroying evidence.
- Do not turn every code observation into an implementation decision; live code is rechecked during Build.
