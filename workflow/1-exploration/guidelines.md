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

Before asking to continue to Stage 3, classify the progression effect of every
material Finding in plain language:

- **informational** — useful evidence, but no current decision/progression impact;
- **decision-relevant** — solutioning may continue, but the Finding must shape or
  surface a decision;
- **blocking** — the affected scope cannot safely progress until the stated
  condition/action is resolved;
- **needs further evidence** — the current evidence is insufficient to decide
  whether or how to progress;
- **deferable** — unresolved, but current task/scope can progress safely and the
  deferred trigger/owner is explicit.

These are Exploration progression labels, not new protocol state enums.

A Finding is not a Blocker merely because it is unresolved, surprising, or
important. State the exact affected scope and progression consequence. If only
part of the work is blocked, keep safe unaffected solutioning open.

The Stage-2 boundary summary must tell the human:

1. what was found;
2. what is actually blocked, if anything;
3. whether Stage 3 can proceed safely and why;
4. what must happen next if it cannot;
5. what confirmation or redirection is needed from the human.

## Stage 3 — Solutioning

After the human confirms Stage 2, evaluate solution options/trade-offs.

When Human/owner input is required, do not ask with a bare list such as
"choose A/B/C/DEFER". Frame the decision so the Human does not have to reconstruct
the analysis:

1. state the concrete problem/question;
2. summarize the minimum current context and constraints;
3. present normally no more than two materially distinct viable options;
4. recommend one option when evidence supports it;
5. explain the material rationale, consequence, and risk;
6. ask for the exact decision/direction required.

Use more than two options only when additional paths are genuinely distinct and
decision-relevant. If evidence is not sufficient to recommend or decide, say
what evidence is missing and route that need instead of forcing a premature
choice.

Record:

- chosen material direction;
- material rejected alternatives and why;
- consequences/risks;
- unresolved external questions.

This durable decision evidence lets Techplan synthesis preserve the outcome without depending on remembered chat discussion.

## Completion handoff

At Stage-3 completion use `workflow/context-management.md`'s compact handoff. In orchestrated mode, Techplan starts as a new Run/Participant with a fresh Participant Session/context. Outside orchestrated mode, recommend Techplan CONTINUE/FRESH using observable continuation fitness, not a Small/Medium/Heavy label.

## What not to do

- Do not produce a Techplan-shaped contract prematurely.
- Do not duplicate target-project conventions into Harscode-shaped prose.
- Do not compress away concrete Stage-2 evidence merely to save context; downstream phases reduce read amplification through routing/anchors, not by destroying evidence.
- Do not turn every code observation into an implementation decision; live code is rechecked during Build.
