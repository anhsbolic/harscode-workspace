# Template: techplan.md

This skeleton's structure MUST be followed. Fill in each section
following `rules.md` and `guardrails.md`. The Summary is written
LAST, after sections 1-13 are complete — it's a condensation of what's
already decided, not an independent draft. Everything from section 1
onward is written for execution precision; the digest is the only part
calibrated for a quick human read.

```markdown
# Tech Plan: {Feature Name}

> Ticket    : {ticket code}
> Author    : {name}
> Date      : {YYYY-MM-DD}
> Updated   : {fill in if there's a significant revision to section 1-7}
> Status    : Draft / In Review / Approved / Implemented
> Approach  : {optional — one-line summary, omit if section 1/2 already covers it}
> Refs      : {optional — AGENTS.md that was read, PRD link, related story docs}

---

## 📋 Summary — start here

*Derived from sections 1, 2, 5, 7, and 14 (Open Items) below —
condensed, not reinterpreted. No line numbers, no full rule-by-rule
tables, no full option comparisons. See `rules.md` § 7 (Summary) for
what to include and `guardrails.md` § Digest Must Not Introduce New
Decisions.*

**What & why** — 2-4 sentences, from section 1.

**Scope** — short bullets, from section 2, no file/line references.

**Decision flow diagram** — a Mermaid diagram, ONLY if this plan has
genuine branching logic, a state transition, or a multi-step
cross-component flow (see `rules.md` § 7 for the criteria). Skip
entirely for linear/CRUD plans — don't add a diagram just because the
template has a slot for one.

**Key decisions** — chosen option only, one line each, from section 5.
Not the full option-comparison table.

**Top risks** — High-severity rows only, from section 7.

**Open items needing human input** — copy the Active list from section
14 as-is. If section 14 has zero Active items, this line reads "none
open" instead of being omitted silently.

---
<!-- Audience boundary: above is the human-readable digest for
review/approval. Below is the full execution-grade plan — same
decisions, same scope, expanded to file/line precision, rule IDs, and
full option comparisons. Nothing below contradicts the digest above;
it's the same source of truth at higher resolution. -->
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

---
<!-- Secondary marker: sections 1-7 above still favor narrative/table
form; 8-13 below are file/line-precise implementation detail. Both
halves are inside the executor-facing part of the document — the only
audience split that matters for review purposes is the one above,
between the Summary and section 1. -->
---

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

High-level flow / pseudocode. Migration strategy if relevant.

## 10. Implementation Details

Reference file:function + signature. Full snippet ONLY for what's
genuinely novel/non-obvious.

**File**: `path/to/file`
- Change: ...

## 11. Files Changed / Files NOT Changed

| File | Change Type | Description |
|---|---|---|

| File | Reason untouched |
|---|---|

## 12. Testing Checklist

Derived directly from section 4, written concurrently — not afterward.

- [ ] ...

## 13. Testing Examples & Common Mistakes

| Mistake | Error/Behavior | Fix |
|---|---|---|

## 14. Open Items

Lifecycle rules in `rules.md` § 8. An item lives in exactly one of the
two lists below at any time — never both, never neither once raised.

### Active — need external input or verification

1. ...

### Resolved (kept for reference)

1. ~~**{short title}**~~ **RESOLVED — {one-line resolution}.** {who
   resolved it, when, and the consequence if any}.
```

## Structural Note

- The Summary is generated, not authored independently — see
  `rules.md` § 7. If section 1, 2, 5, 7, or 14 (Open Items) changes,
  regenerate the Summary; don't hand-patch it out of sync with the rest
  of the plan. See `rules.md` § 7's self-check before calling any
  revision done.
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