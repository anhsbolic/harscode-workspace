# Proposal: Rename to "Summary", formalize Open Items lifecycle, convert recurring rules into a self-check

> Status: Accepted
> Date: 2026-08-13
> Triggered by: GMRT-51524, third review pass (manual edit by workspace
> owner, after two model-generated passes under proposals 0001/0002)
> Target: `template.md` (rename, metadata, new § 14), `rules.md`
> (rename § 7, new § 8, self-check in § 7, count-check in § 4),
> `guardrails.md` (rename, new § 10-11, extended § 9), `guidelines.md`
> (step 7 rewrite, new step 10), `examples.md` (rename, new example),
> `diagram-guidelines.md` (new semantic validation section)

## Friction Found

A third independent pass at the same techplan (this time a manual edit,
not model-generated) reproduced gaps that earlier passes had already
hit:

1. Testing checklist missing a rule ID (R18) — same exact gap as the
   first model-generated pass; the second pass had actually caught and
   fixed it, so this wasn't a permanent fix, it was luck.
2. Top Risks including Medium-severity rows instead of High-only — same
   gap as the second pass (see proposal 0002), which was left as "the
   rule is fine, compliance needs to improve" — and compliance didn't
   improve on the next pass either.
3. A new gap: a diagram branch with an inverted, logically-impossible
   condition. It passed Mermaid syntax validation (proposal 0002's
   fix) cleanly — syntax and semantics are genuinely different checks.
4. A new gap: 3 of 4 Open Items were resolved during a manual edit, but
   the Summary at the top of the file wasn't regenerated, so it still
   listed all 4 as active. The existing "don't silently overwrite a
   locked contract" guardrail only applied to Approved/Implemented
   status, leaving iterative Draft edits uncovered.

The pattern across #1 and #2: writing "check the severity column" or
"count the rule IDs" as prose inside a rule's description is not
enough — it gets skipped in practice, twice, regardless of which model
or person is doing the synthesis. This is the actual structural
finding of this proposal: **recurring compliance gaps need to become
explicit self-check items, not restated instructions.**

## Proposed Change

- **Rename "Human Digest" → "Summary"** everywhere (owner preference,
  confirmed intentional) — `template.md` heading, all cross-references
  in `rules.md`, `guardrails.md`, `guidelines.md`, `examples.md`.
- **`template.md`**: `Approach`/`Refs` metadata fields become optional.
  New formal section 14 "Open Items" (Active / Resolved subsections) —
  this had been an undocumented convention in practice, now part of
  the skeleton.
- **`rules.md` § 7 (Summary)**: added an explicit self-check checklist
  to run before calling the Summary done — severity re-check, diagram
  semantic re-check, Open Items sync check, testing-checklist
  count-check. § 4 (Testing Checklist) gained an explicit "count the
  rule IDs, confirm each has a checklist line" instruction.
- **`rules.md` § 8 (new): Open Items Lifecycle** — Active/Resolved
  states, resolution must be recorded not deleted, applies at any
  techplan status (not just Approved/Implemented).
- **`guardrails.md`**: § 9 extended to require semantic diagram
  validation (not just syntax); new § 10 (resolved items must be
  recorded) and § 11 (Summary must stay in sync with the full plan,
  including mid-Draft edits).
- **`diagram-guidelines.md`**: new "Semantic validation" section with
  a worked example of the actual inverted-condition bug found, plus a
  concrete checklist (inequality direction, satisfiability, boundary
  side, no gaps/overlaps).
- **`guidelines.md`**: step 7 rewritten to point at the self-check;
  new step 10 for handling Open Item resolution during iterative
  (non-full-resynthesis) edits.
- **`examples.md`**: new "recurring Summary mistakes" example
  documenting all four gaps found across the three passes, as
  calibration for future synthesis.

## Rationale

Two of these four gaps (testing checklist completeness, risk severity
filtering) were already covered by existing rules and still recurred.
The lesson isn't "add more rules" — it's that a rule stated once in
prose, however clear, doesn't survive being read once and then
forgotten during a long synthesis pass. An explicit, mechanical
self-check list — the same pattern already proven useful in
`diagram-guidelines.md`'s syntax checklist — is a better fit for
"cheap to verify, expensive to get wrong" gaps. The Open Items lifecycle
gap (#4) is structural rather than a compliance issue: the workspace
genuinely didn't have a rule for iterative Draft edits, only for
protecting a locked contract, so that's a real new rule rather than a
stricter enforcement of an old one.

---

*Reviewed and approved directly with the workspace owner in the same
session that surfaced the friction — see `retro.md` 2026-08-13 (third
entry). Builds on proposals 0001 and 0002; does not reverse either.*