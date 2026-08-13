# Retro

Living log. Each entry: what happened, why it was a problem, how it was
mitigated. Keep appending, don't delete (even once "solved" — the
history still has value).

---

## 2026-07-30 — Duplicate content across raw docs (GMRT-50941)

**What happened:** `implementation-plan.md` and
`registrar-migration-plan.md` both rewrote the same migration SQL, model
field, and service mapping. `registrar-migration-plan.md` was more
detailed (had specific line numbers, a current-state ✓/❌ checklist).

**Why it was a problem:** If content is taken from whichever file was
read first without comparison, you can end up with the less precise
version without realizing it.

**Mitigation:** Added `rules.md` § 2 (Dedup & Reconciliation) —
prioritize the most specific and most recent version, note it as an open
question if it's a genuine conflict (not just a difference in level of
detail).

---

## 2026-07-30 — Sub-component with a different-genre operational lifecycle (GMRT-50941)

**What happened:** `registrar-backfill-plan.md` had its own rollback,
cleanup checklist, execution order, and duration estimate — a different
genre from a techplan (it's a runbook, not a system-behavior spec).

**Why it was a problem:** If forced into a section of the main
techplan, the document gets bloated and mixes two genres (behavior
contract vs one-time execution procedure) into one file.

**Mitigation:** Added `rules.md` § 3 (Runbook vs Techplan) + an example
in `examples.md`.

---

## 2026-08-13 — Sections 1-7 weren't actually "human-readable" despite the label (GMRT-51524)

**What happened:** `template.md`'s own note claimed sections 1-7 are for
"the lead/team audience (no need to open code)." In practice, section 4
(Rules & Validation) for GMRT-51524 had 18 given/when/then rules with
exact boundary conditions and `TransactionID` formats — execution-grade
detail, not something a tech lead skims to approve scope.

**Why it was a problem:** the audience boundary comment existed but was
placed in the wrong spot (between 7 and 8) — the actual density gap
starts around section 3-4, not section 8. A tech lead reviewing the
plan for approval had to wade through rule-by-rule detail meant for the
execution agent.

**Mitigation:** added a Human Digest section at the very top of
`template.md` (`rules.md` § 7, `guardrails.md` § 8), generated last by
condensing sections 1, 2, 5, 7, and Open Items. The audience boundary
moved to sit between the digest and section 1. Sections 1-13 stay
exactly as detailed as before — nothing lost, just no longer mistaken
for the human-facing part. See `proposals/0001-human-digest-section.md`
for the full rationale.

---

## 2026-08-13 — First real-world digest from another model surfaced three gaps (GMRT-51524, second pass)

**What happened:** A different model regenerated the GMRT-51524
techplan under the new Human Digest guidance. Review found: (1) the
digest's Mermaid diagram used single-dash edges (`->`) on three lines —
invalid syntax, fails to render silently; (2) the digest included a
handful of parenthetical rule-ID references (e.g. "(R18)"), which
`rules.md` § 7 said to exclude entirely, but on review these read as
genuinely useful, not noisy; (3) the digest's Top Risks table included
one Medium-severity row alongside High-severity ones, against the
"High-severity only" instruction.

**Why it was a problem:** (1) is a silent failure mode — nothing in the
guidance would have caught a broken diagram before it shipped. (2)
revealed the original rule was stricter than useful once tested against
a real generated example. (3) was a plain compliance gap, not a sign
the rule was wrong.

**Mitigation:** added `diagram-guidelines.md` (Mermaid syntax reference
+ mandatory pre-finalize checklist) and `guardrails.md` § 9 to make
diagram syntax a hard-checked guardrail. Relaxed `rules.md` § 7's
rule-ID exclusion to allow parenthetical cross-references while still
banning full rule-by-rule tables. Left the severity-filtering
instruction as strict as written — that gap gets fixed by enforcement,
not by changing the rule. See
`proposals/0002-digest-diagram-and-rule-id-refinement.md`.

---

## 2026-08-13 — Same gaps recurred a third time; enforcement needed a checklist, not just prose (GMRT-51524, third pass)

**What happened:** A third pass at the GMRT-51524 techplan (a manual
edit by the workspace owner, after two model-generated passes) still
had: the testing checklist missing R18 (the same gap as pass one, which
pass two had actually caught and fixed); two Medium-severity risks in
Top Risks instead of High-only; a diagram branch with an inverted range
condition (`today+14 < expiry < today`, which can never be true) that
passed Mermaid syntax validation cleanly. Separately, during review the
owner confirmed 3 of 4 Open Items were already resolved, but the
Summary at the top of the same file still listed all 4 as active — the
full plan and the Summary had drifted out of sync mid-edit.

**Why it was a problem:** the rules already existed for all four issues
(severity filter, testing checklist traceability, diagram syntax
validation, Summary-is-derived-one-directionally) — restating them in
prose a third time wasn't going to fix a compliance gap that survived
two prior passes. The Open Items desync also exposed a real hole: the
existing guardrail for "don't silently change a locked contract" only
covered Approved/Implemented status, not a Draft being edited
iteratively.

**Mitigation:** converted the relevant rules into an explicit
self-check list in `rules.md` § 7 (run before calling the Summary
done) instead of leaving them as prose to remember. Added
`rules.md` § 8 (Open Items Lifecycle) and `guardrails.md` § 10-11 to
cover resolution/sync at any status, not just Approved/Implemented.
Extended the diagram guardrail (`guardrails.md` § 9,
`diagram-guidelines.md`) to require a semantic check against the
source table, not just Mermaid syntax. Also renamed "Human Digest" to
"Summary" throughout (owner preference, confirmed intentional) and
formalized Open Items as `template.md` section 14 — it had been an
informal, undocumented convention until now. See
`proposals/0003-summary-rename-and-open-items-lifecycle.md`.