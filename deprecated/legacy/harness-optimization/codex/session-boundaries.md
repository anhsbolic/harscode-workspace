# Session Boundaries (Codex)

## What this translates

Portable authority: `workflow/context-management.md`.

Codex sessions/subagents implement that policy; they do not create a second lifecycle.

Human-facing handoffs should say the action to take, not only the portable enum. `CONTINUE`, `FRESH`, and `BUILD authority` remain useful internal semantics, but the operator should see wording such as:

```text
Continue Techplan synthesis in this session because the Exploration context remains focused and current.
Start a fresh Code Review session because reviewer independence is part of the phase's value.
Return to the existing Build session because the patch is narrow and implementation context remains focused.
Start a fresh Build/Patch session re-grounded on the patch plan because the previous Build context is stale/compacted.
```

## Exploration → Techplan

Adaptive:

- CONTINUE when Exploration context is focused, relevant sources remain active/unchanged, durable artifacts exist, and no independence benefit is lost.
- FRESH when compaction/reset, substantial dead ends, major redirection, or context ambiguity makes re-grounding cheaper/safer.

The same canonical Techplan prompt works in both cases. A fresh session reads durable Exploration evidence; a continuing healthy session may reuse active evidence and selectively reopen exact source sections.

## Build / Patch

Fresh from planning is preferred. Re-ground on:

```text
target repo AGENTS/authority
+ Approved Techplan spine
+ current task slice when decomposed
+ live code/spec at anchors
+ specific patch plan when re-entering
```

Do not carry raw Exploration by default. Review/Testing patch requests return to Build authority.

When re-entering after a patch request:

- return to the existing Build session when it is still healthy/focused and the patch is narrow;
- start a fresh Build/Patch session when the prior Build context is stale, compacted, materially redirected, or no longer cheaper than re-grounding on the durable patch plan.

The Review/Testing handoff should state which one it recommends and why so the operator does not have to infer the session destination from `BUILD authority` alone.

## Code Review

Fresh context preferred for independence. Read current diff + current Techplan contract + applicable target-repo authority + routed matching best practices. Do not edit production code in review.

Review does not require a blanket full-suite replay. Run targeted reproduction/verification when a suspected finding needs objective evidence; broad final verification normally belongs to Testing according to the approved Techplan/target repo.

## Testing

Fresh context preferred for independent verification. Read current Techplan + latest build evidence + target repo's real verification authority. Follow exact Test Focus evidence anchors rather than loading the whole Exploration corpus.

On a Testing re-entry after a narrow patch, keep the same independent Testing session only while it remains focused and the affected verification is clear; a fresh Testing session is justified when independence/context hygiene has been lost. Do not create a fresh session solely to make benchmark accounting cleaner.

## Pull Request

Use final repository state + durable review/testing evidence. Same/fresh session is flexible; do not reconstruct truth from stale Build memory.

## Native subagents / multi-agent tools

Optional execution optimization. Use when it creates real isolation/parallelism without violating Harscode/project authority. Never require it merely because Codex exposes it.

Parallelism does not override write-scope conflicts, dependencies, protected paths, shared contracts, or human gates.
