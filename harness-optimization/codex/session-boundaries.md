# Session Boundaries (Codex)

## What this translates

Portable authority: `workflow/context-management.md`.

Codex sessions/subagents implement that policy; they do not create a second lifecycle.

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

Do not carry raw Exploration by default. Review/Testing patch requests return to Build authority; reuse a healthy Build session or start a fresh one with the durable patch plan.

## Code Review

Fresh context preferred for independence. Read current diff + current Techplan contract + applicable target-repo authority + routed matching best practices. Do not edit production code in review.

## Testing

Fresh context preferred for independent verification. Read current Techplan + latest build evidence + target repo's real verification authority. Follow exact Test Focus evidence anchors rather than loading the whole Exploration corpus.

## Pull Request

Use final repository state + durable review/testing evidence. Same/fresh session is flexible; do not reconstruct truth from stale Build memory.

## Native subagents / multi-agent tools

Optional execution optimization. Use when it creates real isolation/parallelism without violating Harscode/project authority. Never require it merely because Codex exposes it.

Parallelism does not override write-scope conflicts, dependencies, protected paths, shared contracts, or human gates.
