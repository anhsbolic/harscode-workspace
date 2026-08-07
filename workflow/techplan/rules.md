# Rules

Rules that determine WHAT must be present and how content from raw docs
gets mapped to techplan sections. This is generic — don't hardcode a
single project's specific conventions here (see guardrails.md for that).

## 1. Content → Section Mapping (by FUNCTION, not by file name)

Raw docs in `docs/story/<story-code>/` vary in count and name. Never
assume 1 file = 1 section. A single file can hold content for many
sections at once, and content for one section can be scattered across
many files. Classify each piece of content by asking what question it
answers:

| Content answers the question... | Goes into section |
|---|---|
| Why does this need to exist? What's the problem? | 1. Background |
| What's in/out of scope? | 2. Scope |
| Business rules / conditions that must be met? | 3. Requirements |
| Detailed per-scenario conditions, testable? | 4. Rules & Validation |
| What options were considered, why was this chosen? | 5. Decision Log |
| Are old data/clients affected or not? | 6. Backward Compatibility |
| What could go wrong, how severe, what's the mitigation? | 7. Edge Cases & Risks |
| DB schema / API / contract between layers? | 8. Interface Contract |
| High-level execution flow? | 9. Architecture/Plan |
| Specific file/function that changes? | 10. Implementation Details |
| List of files touched/not touched? | 11. Files Changed/NOT Changed |
| Test scenarios that must be run? | 12. Testing Checklist |
| Example request/response, common mistakes? | 13. Testing Examples |

## 2. Dedup & Reconciliation

If 2+ raw docs cover the same ground (real case: a migration plan doc and
an implementation plan doc both rewriting the same migration SQL) — do
NOT just pick one arbitrarily. Prioritize the version that is:
1. Most specific (has line numbers, exact paths, current-state check)
2. Most recent (created/updated date is more recent)

If there's information that genuinely conflicts (not just a difference
in level of detail), note it as an open question in the techplan — don't
silently pick one.

## 3. Runbook vs Techplan

If there's a sub-component with an independent operational lifecycle —
one-time script/cron, its own rollback, its own cleanup checklist,
executable separately from the main feature — evaluate whether it's:
- An **inseparable part** of the main feature (fold it in as an
  additional section in the same techplan), or
- A **separate techplan/runbook** linked from the main techplan (if it
  can "finish" and be removed/re-run independently of the parent feature)

Signals leaning toward "separate": it has its own execution order, its
own cleanup/rollback, its own monitoring/verification.

## 4. Testing Checklist Is Derived, Not Written From Scratch

Section 12 (Testing Checklist) must be 1:1 traceable back to section 4
(Rules & Validation). If there's a checklist item that can't be traced
back to a rule in section 4 — that means section 4 is incomplete; fix
that first, don't just add the checklist item on its own.

## 5. Decision Log Is Mandatory Whenever >1 Option Was Considered

If the raw docs show more than one approach was explored (even if it
ends up as a single paragraph "why X, not Y"), it MUST become a separate
Decision Log section — not mixed into section 1 (Background) prose.
Reviewers should be able to scan the trade-off without re-reading the
whole background.

## 6. Minimal Interface Contract Coverage

Section 8 must at minimum cover: changes at the persistence layer (DB
Schema), changes at the API layer, and business logic flow — UNLESS the
target repo's convention says otherwise (see guardrails.md § Read the
Target Convention First). This is a floor, not a ceiling — Backward
Compatibility and Edge Cases remain mandatory even once section 8's
"minimal coverage" is satisfied.