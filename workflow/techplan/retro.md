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