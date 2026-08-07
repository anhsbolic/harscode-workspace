# Template: techplan.md

This skeleton's structure MUST be followed. Fill in each section
following `rules.md` and `guardrails.md`. Section order is intentional:
1-7 for the lead/team audience (no need to open code), 8-13 for the
executor (precise technical detail).

```markdown
# Tech Plan: {Feature Name}

> Ticket    : {ticket code}
> Author    : {name}
> Date      : {YYYY-MM-DD}
> Updated   : {fill in if there's a significant revision to section 1-7}
> Status    : Draft / In Review / Approved / Implemented
> Approach  : {one-line summary}
> Refs      : {AGENTS.md that was read, PRD link, related story docs}

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
<!-- Audience boundary: above for lead/team, below for the executor -->
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
```

## Structural Note

- If this feature has a sub-component with an independent operational
  lifecycle (one-time script, cron job, separate migration with its own
  rollback/cleanup) — evaluate first whether that's an extra section
  here or a separate linked techplan. See `rules.md` § Runbook vs
  Techplan.