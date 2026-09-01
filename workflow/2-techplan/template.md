# Template: techplan.md

This skeleton's structure MUST be followed. Fill in each section
following `rules.md` and `guardrails.md`. This document is
execution-grade throughout — for the implementing agent, the engineer,
and code review. It has no reviewer-facing summary.

Once this techplan reaches **Approved** status, generate
`report-techplan.md` from `report-template.md` — that file is the sole
human-facing artifact (see Proposal 0012, which supersedes the older
embedded-Summary design). Do not add a summary or condensed section
back into this file; if a reviewer needs an update after Approved,
regenerate `report-techplan.md` in full, don't patch either file
piecemeal.

```markdown
# Tech Plan: {Feature Name}

> Ticket    : {ticket code}
> Author    : {name}
> Date      : {YYYY-MM-DD}
> Updated   : {fill in if there's a significant revision to any section}
> Status    : Draft / In Review / Approved / Implemented
> Approach  : {optional — one-line summary, omit if section 1/2 already covers it}
> Refs      : {optional — AGENTS.md that was read, PRD link, related story docs}

---

## 1. Background

Why this change needs to exist. Current behavior / problem statement.
2-3 paragraphs max.

## 2. Scope

**In scope:**
- ...

**Out of scope (explicit):**
- ...

## 3. Requirements

| Condition | Requirement | Source/Note |
|---|---|---|

## 4. Rules & Validation

Testable, given/when/then style.

- Scenario A: ...
- Scenario B (error case): ... → error `{ErrMsgXxx}`

## 5. Decision Log

| Option considered | Why rejected/accepted |
|---|---|
| Option A | ... |
| Option B (chosen) | ... |

## 6. Backward Compatibility

- Database: how existing data is handled
- API: additive vs breaking
- Existing clients/data: affected or not
- Deprecation path if applicable

## 7. Edge Cases & Risks

| Risk | Likelihood | Severity | Mitigation |
|---|---|---|---|

## 8. Interface Contract

Check the target repo's convention first (see `guardrails.md`) to know
what's mandatory to cover here — it can differ per project/service.

**DB Schema changes:**
```sql
```

**API changes:**
```graphql
```

**Business logic flow (concise, not full code):**
```
```

## 9. Architecture / Plan

High-level flow / pseudocode. Migration strategy if relevant. Include
a diagram only if the flow has genuine branching, a state transition,
or a multi-step cross-component sequence — skip it for a linear/CRUD
plan and describe the flow in one line instead (`guidelines.md`'s
diagram criteria apply here, not just in `report-template.md`).

## 10. Implementation Details

Reference file:function + signature. Full snippet ONLY for what's
genuinely novel/non-obvious; for logic that mirrors an existing
precedent, point at the precedent (file:line) instead of duplicating
its code.

**File**: `path/to/file`
- Change: ...

## 11. Files Changed / Files NOT Changed

| File | Change Type | Description |
|---|---|---|

| File | Reason untouched |
|---|---|

## 12. Testing Checklist

Derived directly from section 4, written concurrently — not afterward.
Mark a line with ⚠️ if it's a non-obvious gotcha worth flagging during
review, instead of maintaining a separate mistakes table.

- [ ] ...

### Test Focus Pointer (carry-over from exploration Risk lens)

Areas flagged as concurrency/perf/security-sensitive during exploration
Stage 2 (`sniffing-checklist.md` § Risk) that are still relevant after
synthesis — a pointer for the testing phase, not a full test plan.

| Area | Why sensitive | Still relevant post-synthesis? |
|---|---|---|

Only list areas that survived synthesis and remain relevant — an area
flagged during exploration but dropped/changed during synthesis is
implicitly "N/A, see § 5 Decision Log for why," not restated here. This
is a pointer, not a test plan: race/perf/security execution detail
(scope, tooling, thresholds) is decided in the testing phase
(`workflow/5-testing/`), not here.

## 13. Open Items

Lifecycle rules in `rules.md` § 8. An item lives in exactly one of the
two lists below at any time — never both, never neither once raised.

### Active — need external input or verification

1. ...

### Resolved (kept for reference)

1. ~~**{short title}**~~ **RESOLVED — {one-line resolution}.** {who
   resolved it, when, and the consequence if any}.
```

## Structural Note

- This file has no Summary/digest section and no audience boundary —
  see Proposal 0012. Every section is written at execution precision
  for the agent and reviewing engineer.
- Once this techplan reaches **Approved**, generate
  `report-techplan.md` from `report-template.md`. That file draws from
  sections 1, 2, 5, 7, and 13 (Open Items) here, condensed for a
  reviewer, plus its own Architecture/Plan and Interface Contract
  sections. Never generate it before Approved, and never hand-patch it
  — if this techplan changes afterward (including the
  Approved→Implemented loop or a reopened Draft), regenerate
  `report-techplan.md` in full. See `report-template.md`'s generation
  checklist (relocated from the old `rules.md` § 7) before treating a
  regenerated report as done.
- When an Active Open Item gets resolved — including mid-Draft, not
  just at Approved/Implemented — move it to Resolved with the
  resolution written out (`rules.md` § 8, `guardrails.md` § 10). Don't
  delete the line; a silently-vanished item loses the "why" a reviewer
  may need later.
- If this feature has a sub-component with an independent operational
  lifecycle (one-time script, cron job, separate migration with its own
  rollback/cleanup) — evaluate first whether that's an extra section
  here or a separate linked techplan. See `rules.md` § Runbook vs
  Techplan.