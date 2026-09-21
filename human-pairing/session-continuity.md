# Session Continuity and Context Hygiene

This document helps a Human decide whether to continue work in the same Session or start a fresh Session while preserving the same Work Unit and, when applicable, the same Run.

Canonical context rules remain in `../workflow/context-management.md`.

## Keep the identities separate

```text
Work Unit != Run != Session
```

A fresh Session does not automatically create a new Work Unit or a new Run.

Example:

```text
WU-S1-001
└── EXP-001
    ├── Session A — Stage 1 + Stage 2
    └── Session B — Stage 3
```

This is still one Exploration Run when Stage 3 continues the same execution occurrence and purpose.

## Do not use a fixed context-window threshold

Context occupancy is a signal, not a rule.

Do not define policy such as:

```text
80% used -> always start fresh
```

because the right choice depends on continuation fitness and durable state.

## Continue the same Session when

- the next concern shares the same authority and execution posture;
- relevant source material is still focused and current;
- the Session has not accumulated substantial dead ends or unrelated investigation;
- the next step benefits materially from the active working context;
- the agent can still identify the current authoritative artifacts cleanly.

## Prefer a fresh Session when

- the next step is still substantive but the current Session carries substantial context pressure or noise;
- durable artifacts already capture the material findings and decisions needed to continue;
- the Session has been compacted/reset;
- major Human redirection invalidated prior working reasoning;
- the agent can no longer reliably distinguish durable authority from remembered conversation;
- independence is part of the next phase's value, such as Code Review or Testing.

## The key safety condition

A fresh Session is safe only when durable state is sufficient to reconstruct the work.

Before moving fresh, ensure the current Run has durable evidence such as:

- current-effective findings / gap analysis;
- accepted decisions;
- relevant source/code anchors;
- current Run identity and scope;
- unresolved questions/blockers;
- next checkpoint or stage.

If those do not exist, strengthen the durable handoff first instead of depending on chat memory.

## Human operating pattern

When continuation is healthy:

```text
Stage 1 Approved, lanjut ke Stage 2.
```

When moving to a fresh Session within the same Run:

```text
Stage 2 Approved. Stop di sini; Stage 3 dilanjutkan di fresh Session.
```

Then start the new Session by pointing it to the current Run's durable invocation/state rather than reproducing the full prior conversation.

## Why this matters

Same-session continuation preserves warm context but can accumulate stale or distracting history.

Fresh-session continuation improves context hygiene but requires strong durable artifacts.

The goal is not to minimize Session count. The goal is to preserve correctness while keeping working context focused.
