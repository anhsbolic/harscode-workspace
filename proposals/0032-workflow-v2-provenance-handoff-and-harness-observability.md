# 0032 — Workflow-v2 provenance, handoff, and harness observability refinement

**Status:** Accepted - Anhar
**Date:** 2026-09-15
**Protection Tier:** general
**Triggered by:** `audits/workflow-v2-validation-01-retrospective.md` from the first Kencleng workflow-v2 Continuous Real-Task Validation run.
**Target area:** lightweight workflow phases, context handoff, guidance authoring, Codex harness translation
**Target file(s):**
- `AUTHORING.md` — define compact provenance expectations for workflow-generated artifacts.
- `workflow/context-management.md` — standardize human-facing phase handoff semantics.
- `workflow/1-exploration-kickoff-prompt.md` — provenance + improved handoff wording.
- `workflow/2-1-techplan-synthesis-prompt.md` — handoff/provenance alignment; proposal 0033 owns Techplan-specific routing semantics.
- `workflow/2-2-techplan-review-prompt.md` — provenance + human-readable handoff.
- `workflow/2-3-techplan-decomposition-prompt.md` — provenance + human-readable handoff.
- `workflow/3-build-prompt.md` — provenance + explicit Build/Patch re-entry/session wording.
- `workflow/4-code-review-prompt.md` — provenance + explicit Build/Patch destination/session wording.
- `workflow/5-testing-prompt.md` — provenance + explicit Build/Patch destination/session wording.
- `harness-optimization/codex/benchmarking.md` — session-level benchmark/usage capture guidance.
- `harness-optimization/codex/README.md` — route to benchmark guidance.
- `harness-optimization/codex/permissions-and-sandbox.md` — proportional destructive-command approval guidance.
- `harness-optimization/codex/session-boundaries.md` — human-readable transition examples.

## Gap found

Validation #1 showed that the underlying workflow state was mostly preserved correctly, but the operator experience was weaker than the durable artifacts:

1. workflow artifacts did not consistently say who/what authored them, when, model/reasoning/session identity when agent-authored, or which workflow/target revision they describe;
2. `Session recommendation: CONTINUE | FRESH` is useful internally but too enum-like for a human deciding what to do next;
3. `Open / blocked` mixes external human decisions with ordinary deferred/non-blocking items, so an important decision can survive in the artifact without being surfaced strongly enough at the phase boundary;
4. Review/Testing → Patch handoffs identify Build authority but do not always tell the operator whether to return to the existing Build session or start a fresh one;
5. the first CRTV benchmark started too late and combined multiple phases in one session, making per-phase/session comparison weaker than intended;
6. Codex approval/sandbox guidance explains phase capability boundaries but lacks an operator-friendly rule for ordinary Git/file commands versus destructive operations.

These are traceability/operator-routing gaps, not reasons to add a new lifecycle phase.

## Proposed change

### A. Compact provenance for workflow-generated artifacts

Every durable workflow-generated artifact should record a compact provenance header when the producing phase controls its format:

```text
Phase: <phase/stage>
Author: <human/agent identity>
Created: <date/time when useful>
Updated: <date/time when materially revised>
Model: <exact model if agent-authored and exposed by harness>
Reasoning: <if exposed>
Session: <session/thread id if useful and safe to persist>
Target revision: <commit/ref if known>
Workflow revision: <commit/ref if known>
```

Do not invent unavailable values. Do not persist credentials/account identifiers/secrets. Git history remains the primary version history; add a manual semantic version only when the artifact itself has a versioned contract.

### B. Human-facing Phase Handoff

Replace the operator-facing enum-only shape with:

```text
## Phase handoff
- Completed: ...
- Artifacts: ...
- Human decision: <decision needed now or None>
- Open / deferred: <non-blocking unresolved/deferred items or None>
- Recommended next step: ...
- Session transition: <plain-language action + reason>
- Context pointers: ...
```

Examples:

- `Continue Techplan synthesis in this session because Exploration context remains focused and current.`
- `Start a fresh Code Review session because reviewer independence is part of the next phase's value.`
- `Return to the existing Build session because the patch is narrow and the implementation context remains focused.`
- `Start a fresh Build/Patch session re-grounded on the patch plan because the previous Build session is stale/compacted.`

`CONTINUE`, `FRESH`, and `BUILD authority` remain useful semantics in portable context-management guidance, but they should not be the only human-facing instruction.

### C. Benchmarking stays harness observability

Add a Codex benchmark guide that treats one agent session as the primary measurement unit and records a before/after snapshot when the client exposes it.

Minimum useful fields:

```text
run/task
phase(s)
session id
model + reasoning
fresh/continued
before snapshot
after snapshot
input/cached/output usage when exposed
allowance deltas when exposed
human prompts
rescue prompts
clarifications
outcome/verdict
notes
```

Do not use a usage reset in the middle of a measured session; if a reset occurs between sessions, record the boundary. Do not compare cached and uncached input as if they have identical cost semantics. Do not require telemetry inside every phase report.

### D. Proportional Codex approvals

Do not solve safety by blanket-blocking useful Git/workspace operations. Prefer normal workspace execution with approval required for materially destructive/irreversible operations.

Ordinary examples that normally should not need special escalation when project authority allows them:

```text
git status
git diff
git log
read/search commands
target-repo test/lint/build commands
ordinary authorized file edits inside the task scope
```

Examples that should normally require explicit approval or be blocked by project policy when not specifically authorized:

```text
rm -rf / broad recursive deletion
git reset --hard
git clean -fd / -fdx
git push --force / --force-with-lease
discard-all-worktree operations
destructive database/storage commands
writes outside the authorized workspace/protected paths
```

Concrete Codex config syntax remains fast-moving and must be re-verified before copying into a real configuration.

## Rationale

These refinements are generic because they concern reconstructability, phase/session routing, and harness observability rather than Kencleng product semantics.

They preserve the successful parts of workflow-v2:

- durable state over chat memory;
- fresh Review/Testing independence;
- Build ownership of production patches;
- progressive disclosure;
- optional rather than ritualized planning mechanisms.

The proposal deliberately does not introduce a new patch phase, new stage artifact, or mandatory benchmark payload in phase outputs.

---

*Accepted by the human owner after Validation #1 discussion. Apply on `workflow-v2` only and validate on a different real task before considering promotion to `main`.*
