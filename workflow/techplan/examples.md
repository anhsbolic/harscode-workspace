# Examples

This file is growing — append new examples whenever you find a piece of
a techplan that's genuinely good for calibrating tone/level of detail.
Not a template, just a "here's what a good one looks like" reference.

---

## Example: a good Decision Log

Source: GMRT-50941 (KFA FARMASI curation skip list)

```markdown
## 5. Decision Log

| Option | Why rejected/accepted |
|---|---|
| A. Single env var, no code change | **Chosen.** Real data validation shows near-zero risk (4 shared fields are empty HTML placeholders in ALKES, 1 field uses a sentinel value). No code change, backward compatible. |
| B. Two env vars + code change (type-aware) | Rejected for now — clean separation but overkill given the real risk already validated as near-zero. Kept as a future improvement if ALKES needs different behavior. |
| C. Tagged selector syntax (`[FARMASI]field`) | Rejected — more complex parsing logic, overkill for a risk that's already near-zero. |
```

Why this is good: each option has a short conclusion (not just a long
pro/con list), the chosen decision is clear, and rejecting the other
options isn't just "not as good" but references concrete data (real API
validation results).

---

## Example: a good Edge Cases & Risks table

Source: GMRT-50941

```markdown
| Risk | Likelihood | Severity | Mitigation |
|---|---|---|---|
| ALKES `warning` content changes from the Kemenkes API | Very low — currently empty | Low — warning change stays ACTIVE instead of IN_REVIEW | Rollback: remove `warning` from the env var |
| All shared fields change simultaneously | Extremely low | Medium — product stays ACTIVE when it should re-curate | Rollback: remove all 7 shared selectors |
```

Why this is good: Likelihood and Severity are separated (not merged into
one ambiguous "risk level" column), and the mitigation is actionable
(a concrete step, not "monitor closely").

---

## Example: when a sub-component becomes a separate document

Source: GMRT-50941, `registrar-backfill-plan.md`

The backfill document has its own execution order, its own rollback
SQL, its own cleanup checklist, and its own duration estimate — all
signals that it can genuinely "finish" and be run independently of the
main migration. This became a separate document, linked from the main
techplan, rather than an extra section.

---

## Example: a good Summary (with diagram)

Source: GMRT-51524 (Daily NIE Expiration Check)

The full plan had 18 numbered rules (R1-R18) covering three reminder
milestones, a take-down boundary condition, and an idempotency
guarantee — genuine branching logic, not a linear CRUD change. The
digest condensed all of that into:

- A 3-sentence "what & why"
- Six scope bullets (no file/line references)
- A Mermaid flowchart showing the milestone/take-down decision tree
- Four one-line "key decisions" (vs. the full plan's ~13-row option
  comparison table in section 5)
- The 3 High-severity risks (of 12 total rows in section 7)
- The 4 open items needing human input

Why this is good: a tech lead can read the digest in under 2 minutes
and know exactly what to approve and what to push back on (in this
case, a take-down boundary that reverses the tech lead's original
direction), without reading R1-R18 first. The diagram earned its place
because the branching (3 reminder milestones + a take-down boundary +
an idempotent no-op) is genuinely hard to hold in your head from a
table alone.

## Example: when to skip the diagram

A techplan that just adds one new column and wires it through one
upsert path, with no branching beyond a single if/else, does not need
a diagram in its digest — a two-sentence description is faster to read
than a two-node flowchart would be to render and scan. Don't add a
diagram out of habit; see `rules.md` § 7 for the criteria.

---

## Example: recurring Summary mistakes to self-check for

Source: GMRT-51524, across three separate synthesis passes (two
different models, plus a manual edit). These are worth calibrating
against because they happened more than once despite the guidance
already covering them — the fix wasn't a new rule, it was making the
existing rule an explicit checklist item (see `rules.md` § 7's
self-check).

1. **Testing checklist missing a rule ID.** Two out of three passes had
   an 18-rule section 4 (R1-R18) but a section 12 checklist that
   stopped at R17 — R18 (a boundary condition added late in review) was
   simply never added to the checklist. Neither pass "decided" to skip
   it; it just fell through the cracks of writing the checklist by
   feel instead of by counting.
2. **Top Risks including a Medium-severity row.** Two out of three
   passes put a Medium-severity risk from section 7 into the digest's
   Top Risks (which is supposed to be High-only), while a genuinely
   High-severity row (a UTC-vs-local-timezone bug that could misfire a
   whole day) sat unselected in the same pass. The selection read as
   "which risks feel most interesting to summarize," not "which rows
   are actually marked High."
3. **Diagram with an inverted condition.** A flowchart branch was
   labeled `today+14 < expiry < today` — impossible, since `today+14`
   is always greater than `today`. The actual condition (per the plan's
   own timeline table) was `today < expiry < today+14`. The diagram was
   syntactically valid Mermaid and rendered fine; it was just wrong.
   Syntax validation alone (`diagram-guidelines.md`) would not have
   caught this — it needed a line-by-line check against the source
   table.
4. **Summary and full plan drifting out of sync mid-Draft.** An Open
   Item got resolved during a manual edit of the full plan, but the
   Summary at the top of the same file still listed it as needing
   human input — because the Summary wasn't regenerated after the edit.
   The rule ("Summary is derived FROM the full plan, one-directional")
   already existed; what was missing was a trigger to actually re-run
   it after a partial edit, not just after a full resynthesis.