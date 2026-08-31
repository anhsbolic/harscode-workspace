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

**Count-check before finalizing:** count the distinct rule IDs in
section 4 (R1, R2, ... Rn) and confirm every single one has at least
one corresponding line in section 12. A missing rule ID is an
incomplete checklist, not a minor omission — this has been the single
most common gap found in practice (see `retro.md`), so treat the count
match as a mandatory check, not a nice-to-have.

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

## 7. Summary

The Summary (top of `template.md`, above the audience boundary) is
written LAST, after sections 1-13 are complete. It is a condensation,
not an independent draft — every sentence in it must trace back to
something already decided in sections 1-13.

**Include, condensed:**
- What & why — from section 1 (Background), 2-4 sentences.
- Scope — from section 2, short bullets, no file/line references.
- Key decisions — from section 5, the *chosen* option only, one line
  each. Not the full option-comparison table.
- Top risks — from section 7, **High-severity rows only**. Check each
  row's Severity column in section 7 before including it — a
  Medium/Low-severity risk doesn't belong in the digest even if it's
  an interesting mitigation. If section 7 has zero High-severity rows,
  the digest's Top Risks can say so ("no High-severity risks
  identified") instead of including a Medium row to avoid an empty
  section.
- Open items needing human input — copied from Open Items as-is.

**Exclude:** line numbers, function signatures, full rule-by-rule
tables (R1, R2... walked through as a structured list), full
option-comparison tables, anything that isn't already written somewhere
in sections 1-13. A parenthetical rule-ID cross-reference is fine —
e.g. "boundary `== today` included per PRD re-read (R18)" is a pointer
for a reader who wants to jump to the detail, not a restatement of the
rule. What's not fine: turning Key Decisions or Top Risks into an
R1-R18 walkthrough. If more than roughly 1 in 3 lines carries a rule-ID,
that's a sign the digest is drifting back into rule-by-rule detail
instead of condensing it.

**Diagram criteria:** include a Mermaid diagram in the digest only if
the plan has at least one of:
- Genuine branching/decision logic (3+ conditions, not a simple
  if/else)
- A state transition (e.g. a status lifecycle)
- A multi-step data/control flow across components where the order
  matters

Skip the diagram for linear or CRUD-shaped plans — a diagram added out
of habit is noise, not signal. Before finalizing a diagram, follow the
syntax checklist in `diagram-guidelines.md` — a diagram with invalid
Mermaid syntax (e.g. single-dash `->` edges) fails to render silently
and is worse than no diagram at all.

**One-directional:** the Summary is derived FROM sections 1-13 (and
§8's Open Items, section 14 in `template.md`), never the other way. If
the Summary and the full plan ever disagree, the full plan is the
source of truth — regenerate the Summary, don't edit the full plan to
match a stale Summary.

**Self-check before calling the Summary done** — this has caught real
recurring gaps in practice (see `retro.md`), don't skip it:
- [ ] Every Top Risks row is genuinely High severity in section 7 —
  re-check the Severity column, don't rely on memory of which risks
  "felt" important.
- [ ] If a diagram is included, every branch condition in it matches
  section 4 / the timeline table exactly — not just valid Mermaid
  syntax (`diagram-guidelines.md`), but the actual logic. An inverted
  or impossible condition (e.g. a range that can never be true) is a
  correctness bug, not a style issue.
- [ ] The Open Items list in the Summary has the exact same items, in
  the same resolved/active state, as section 14's Active list in the
  full plan. If they don't match, section 14 is the source of truth —
  sync it first (§8), then regenerate the Summary.
- [ ] Testing Checklist count-check has been run (see § 4) if section 4
  changed since the last Summary was written.

## 8. Open Items Lifecycle

An Open Item lives in exactly one of two states at any time: **Active**
(needs external input or verification) or **Resolved** (kept for
reference, with the resolution recorded). It moves from Active to
Resolved the moment it's genuinely resolved — this applies at ANY
techplan status, including Draft, not just Approved/Implemented
(contrast with `guardrails.md` § 3, which is specifically about not
silently overwriting a locked contract).

**When an item resolves:**
- Move it out of Active into Resolved in the same edit — don't leave
  it dangling in Active with stale text, and don't just delete the
  line.
- Record the resolution: what was decided, who decided it (if known),
  and any consequence that falls out of it. A one-line resolution is
  fine; a resolution with no content ("resolved") is not — a future
  reader needs to know *what* it resolved to, not just that it did.
- Regenerate the Summary immediately after (see § 7's self-check) —
  a Summary that still lists a resolved item as needing human input is
  actively misleading, worse than an out-of-date Decision Log entry
  because it asks a human to act on something that's already settled.

**Never:** delete an Open Item outright once it's been raised, whether
Active or Resolved. The Resolved list is the permanent record of what
was asked and what was decided — same rationale as `retro.md` and
`proposals/` being append-only logs elsewhere in this workspace.

## 9. Test Focus Pointer Is Carried From Exploration, Not Invented

Section 12's Test Focus Pointer table sources from the raw exploration
docs' Sniffing Checklist § Risk findings for that task — never
invented fresh during synthesis. If synthesis surfaces a new
concurrency/perf/security concern that wasn't flagged during
exploration, that's a missed area in exploration, not something to
quietly add here without flagging it (see `guardrails.md` § 12).

**What qualifies for the pointer:** a Risk-lens finding from exploration
that is genuinely about shared state, race conditions, expensive
primitives under load, or a security-sensitive boundary (auth, payment,
PII) — not every risk finding qualifies. A risk already fully covered
by section 4's ordinary rules (a plain validation edge case, for
instance) doesn't need a pointer row; the pointer exists specifically
for test *classes* the default build-loop suite (unit + mocked + API
contract) does not cover.

**Condensation, not restatement:** only areas that survived synthesis
and remain relevant belong in the table — same condensation discipline
this workspace already applies elsewhere (derived from earlier
material, never an independent draft; the full plan wins if it ever
disagrees with what exploration originally flagged).

**Default is off:** the build/patch implementation loop runs unit +
mocked-service + API-contract tests only, regardless of what this table
says. A row here is an instruction for the testing phase
(`workflow/5-testing/`) to schedule additional test classes there — it
is never an instruction to run race/perf/security tests inside the
tight build-loop iteration.