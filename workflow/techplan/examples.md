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