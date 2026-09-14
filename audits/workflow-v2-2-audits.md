# Audit Report #2 — `workflow-v2` remediation verification

**Repo:** anhsbolic/harscode-workspace
**Branch under audit:** `workflow-v2` @ `4bbc283` ("Remediate workflow-v2 pre-dogfood audit findings")
**Prior baseline audited (Report #1):** `6edc1a6` ("Freeze workflow v2 dogfood baseline")
**Compared against:** `main` @ `fbeb2e6` (unchanged since Report #1 — confirmed below)
**Related documents:** `audits/workflow-v2-audits.md` (Report #1, now committed to the repo verbatim), `proposals/0031-workflow-v2-pre-dogfood-audit-remediation.md` (Accepted)
**Audit date:** 2026-09-14
**Auditor:** Claude, at Anhar's request
**Status:** CLOSED — this is an independent re-verification, not a fresh full-branch audit; scope is the remediation diff (`6edc1a6..4bbc283`, 14 files) plus a check that nothing outside that scope moved.

## Method

Report #1 raised 6 findings (F1–F6). Proposal 0031 claims to remediate all
six. This report does not re-trust that claim — it re-diffs every file the
remediation touched, checks each fix against the specific defect described
in Report #1 (not just "does something look different here"), and separately
confirms proposal 0031's own stated non-goals were honored (no scope creep,
`main` untouched, no unrelated architecture change).

Verdict scale per finding: **Fixed** / **Partially fixed** / **Not fixed** /
**Fixed differently than recommended, and why that's acceptable**.

## Finding-by-finding verification

### F1 — Hardcoded `§4`/`§12` in `2-2-techplan-review-prompt.md` → **Fixed**

Diff confirms:
- Check 1 now reads "Rules & Validation" / "Testing Checklist" instead of `§4`/`§12`.
- Check 2 now reads "the Decision Log" instead of `§5`.
- Step 0 rewritten: "Resolve current template section names before checking.
  If the report needs section numbers for human location, map those names to
  the current numbers from `template.md` at runtime; never encode remembered
  ordinal numbers in the checks." — this is stricter than Report #1's own
  recommendation (which only asked to restore name-based checks); it also
  explicitly separates "numbers for human display" from "numbers as a
  runtime check locator," which is a more precise fix than what existed even
  on `main`.
- The deleted incident rationale is back, compressed to one line in Notes:
  *"A prior version hardcoded Techplan section numbers, the template later
  renumbered, and the review silently checked stale locations; keep this
  failure-mode rationale when compressing the prompt."* — this is a direct
  instruction to future compression passes, addressing the actual root cause
  Report #1 identified, not just the symptom.

**No residual concern.**

### F2 — Hardcoding widened in `2-1-techplan-synthesis-prompt.md` (and spread) → **Fixed, and generalized**

This is the strongest fix in the remediation. Proposal 0031 did not treat F1
and F2 as two separate patches — it correctly recognized them as one defect
class and fixed it everywhere:

- `2-1-techplan-synthesis-prompt.md`: `§5`, `§10`, `§4`, `§12`, `§13` all
  converted to semantic names.
- `5-testing-prompt.md`: `§4`, `§12` (both instances) converted.
- `5-testing/checklist.md`, `5-testing/guidelines.md`: same conversions.
- `4-code-review/checklist.md`, `4-code-review/guidelines.md`: the `§12`
  reference in the Techplan-drift check converted.

Re-ran the same measurement Report #1 used (`§<number>` reference count per
phase prompt, techplan.md sections only):

| File | Report #1 (`main` / `workflow-v2` pre-fix) | Now |
|---|---|---|
| `2-1-techplan-synthesis-prompt.md` | 1 / 6 | **0** |
| `2-2-techplan-review-prompt.md` | 0 / 2 | **0** |
| `5-testing-prompt.md` | 4 / 3 | **0** |
| `4-code-review/checklist.md` + `guidelines.md` | n/a / 2 | **0** |

**Systemic fix, not local patch:** `AUTHORING.md` gained a new numbered
authoring rule (§ list item 11): *"Prefer semantic anchors over ordinal
section numbers... This rule exists because a Techplan review once silently
checked stale sections after template renumbering."* — and a matching
line was added to `AUTHORING.md`'s own pre-finalization checklist ("Do
cross-document references use stable semantic anchors rather than
drift-prone ordinal numbers?"). This means a *future* compression pass has
an explicit rule to check against, not just tribal memory of this one
incident. This directly satisfies Report #1's closing recommendation
("re-add one line of rationale... so a future compression pass doesn't
repeat this") and goes further than requested.

**No residual concern.**

### F3 — `## What's Explicitly Out of Scope Here` heading dropped, breaking proposal 0029's citation → **Fixed**

`workflow/README.md` now has:

> "## What's Explicitly Out of Scope Here
>
> Project-specific codebase conventions and product/domain truth belong in
> the target repo, not Harscode. This heading is retained as an addressable
> compatibility anchor for accepted historical proposals; current layering
> details live under `Canonical phase prompts` below."

This is the right shape: it restores the addressable anchor (so proposal
0029's citation resolves again) without reverting to the old long-form
prose, and it's explicit about *why* the heading exists in its current
minimal form — future editors won't accidentally delete it again thinking
it's dead weight, because the heading itself says it's a compatibility
anchor.

Verified: `grep -rn "What's Explicitly Out of Scope Here"` now resolves in
both `workflow/README.md` and `proposals/0029-...md`.

**No residual concern.**

### F4 — Build report's mandatory race/perf/security confirmation line removed → **Fixed**

`3-build-prompt.md`'s report format gained back:

> "## Verification scope confirmation
> Confirm explicitly: no race/concurrency, performance/load, or
> security-class test was executed in this Build iteration. If any was run,
> list it here and flag the scope deviation instead of silently treating it
> as ordinary Build verification."

This is not a verbatim revert of `main`'s line — it's an improvement:
`main`'s version only asked for a confirmation; this version also defines
what to do if the confirmation can't be given honestly (name it + flag as a
scope deviation, rather than leaving the agent to improvise). `3-build/checklist.md`
was updated to match ("Build report explicitly confirms the heavyweight
verification boundary..."). Notes now state plainly why this exists: *"an
intentional forcing function: prose/checklist guidance alone is not treated
as sufficient evidence that heavyweight Testing work stayed out of the tight
Build loop."*

This last sentence matters: it's the remediation explicitly naming the
failure mode Report #1 described (prose alone already failed once), rather
than silently re-adding the line without saying why. That's the difference
between a patch and an actual fix.

**No residual concern. This was the highest-priority finding and it's the
most solidly closed.**

### F5 — `model-routing.md` pointers dropped workspace-wide; "different model" softened to "when practical" → **Fixed differently than recommended, and the difference is an improvement**

Report #1 recommended: "restore at least one pointer per phase prompt to
wherever routing tier/model requirements now live." Proposal 0031 did not do
that — and says so explicitly in its non-goals: *"This remediation does not
restore model-routing pointers to every generic phase prompt."*

Instead, `2-2-techplan-review-prompt.md`'s Purpose now reads:

> "Independent adversarial verification of a synthesized Techplan. This
> review must use an independent reviewer/actor context from the primary
> synthesis; it must not be the synthesizer merely self-checking its own
> plan. Exact model/client selection is execution configuration, not phase
> policy."

And a new Note: *"Independence is mandatory at the reviewer/actor-context
level even though exact model/client routing stays outside this phase
prompt."*

**Why this is the right call, not a dodge:** Report #1's own analysis
already separated two different things that had gotten conflated in
`main`'s original wording — (a) the *requirement* that review be independent
of synthesis, which is the thing actually validated by the 0002/0003
incidents, and (b) *which model* satisfies that requirement, which is
proposal 0028's "execution profile" territory and was never meant to live in
generic phase prompts. `main`'s wording bundled both into "run by a
**different model**," so removing the model-routing pointer in `workflow-v2`
accidentally softened (a) along with correctly removing (b). The remediation
un-bundles them cleanly: "must use an independent reviewer/actor context"
(hard requirement, restored) vs. "exact model/client selection is execution
configuration" (correctly kept out). This is arguably a better outcome than
Report #1's own recommendation, because restoring a `model-routing.md`
pointer to every phase prompt would have re-created exactly the coupling
proposal 0028 deliberately removed.

**Residual note, not a defect:** the *other* four files that lost
`model-routing.md` pointers on `main` (`2-3-decomposition`, `3-build`,
`4-code-review`, `5-testing`, `workflow/README.md`) still don't point
anywhere. That's fine **if** none of them ever depended on "different
model," only on "different session/context" (Build/Testing/Code-Review
independence is already handled by `context-management.md`'s session-fresh
defaults, not by a model-routing citation). Spot-checked: none of those four
files used "different model" language on `main` the way `2-2` did — they
only referenced `model-routing.md` for tier/cost routing, which is
legitimately execution-profile territory. So this residual is consistent
with 0031's own explicit non-goal, not an oversight.

**Verdict: Fixed for the part that mattered (independence requirement).
Deliberately not fixed for the part that didn't need fixing (model pointer
proliferation), and that choice is justified.**

### F6 — "Never merge your own proposal" dropped from both `AGENTS.md` files → **Fixed, and correctly centralized**

`proposals/README.md` now owns the rule once:

> "**No self-approval.** The actor that authors a proposal is not the
> approval authority for that proposal. Obtain explicit human-owner or
> independent authorized acceptance before merge. After that approval, an
> authorized implementation actor may perform the mechanical
> application/merge; it does not turn authorship into approval authority."

This is the option Report #1 called "arguably the more correct single
source of truth" over duplicating the line in both `AGENTS.md` files — and
it's meaningfully more precise than `main`'s original one-liner: it now
distinguishes *approval* authority from *mechanical merge* authority, which
`main`'s terse "never merge your own proposal" left ambiguous (does an
approved-by-someone-else proposal still need a different person to click
merge? 0031's wording says no — implementation can be mechanical once
approval exists).

Checked both `best-practices/AGENTS.md` and `harness-optimization/AGENTS.md`
still route to `proposals/README.md` for the proposal process (unchanged,
confirmed no dangling reference — they never restated the rule inline after
this fix, they just point at the one place it now lives).

**No residual concern.**

## Non-goals and scope-creep check (proposal 0031's own verification gate)

Independently re-verified, not just taken on the proposal's word:

- **`main` untouched:** `main` is still at `fbeb2e6`, identical to Report #1. Confirmed.
- **No `model-routing.md` redesign:** file untouched in this diff (not in the 14-file changeset).
- **No reversal of progressive disclosure / context-management.md:** untouched in this diff.
- **`rules.md` / `guardrails.md` not re-expanded:** untouched in this diff — the semantic-anchor fix happened entirely in the *consumers* of section numbers (phase prompts/checklists), not in the protected files that define the numbering. Correct scoping.
- **Kencleng not touched:** N/A to this repo, not applicable/verifiable from here, but no file path in the diff touches anything outside this workspace.
- **No unrelated file touched:** all 14 changed files map directly to one of F1–F6 or to `audits/workflow-v2-audits.md` + `proposals/0031-...md` (the paper trail itself). No stray edits found.

## Overall verdict

**All 6 findings from Report #1 are resolved.** Five are straightforward
fixes verified line-for-line against the original defect. The sixth (F5) was
resolved by a more precise fix than Report #1 itself proposed — separating
"independence is mandatory" from "model choice is execution configuration"
— which is a better outcome than blindly restoring the old coupled wording
would have been.

Two things stand out about the quality of this remediation, worth recording
for future reference on this workspace:

1. It fixed **root causes**, not just instances — the new `AUTHORING.md`
   rule #11 means a future compression pass has an explicit checklist item
   to catch this defect class before it ships, rather than relying on this
   audit finding it by hand again.
2. It **improved on `main`'s original wording** in three places (F1's
   name-vs-number split, F4's "flag the scope deviation" branch, F6's
   approval-vs-merge distinction) rather than mechanically reverting to
   what existed before the context-efficiency pass. This is the outcome
   Report #1 hoped for but didn't require — the remediation used the audit
   as an opportunity to make the rules better, not just to undo damage.

**Recommendation:** treat `4bbc283` as the new dogfood baseline (superseding
`6edc1a6`, exactly as proposal 0031 § Verification gate proposes), and
proceed to the dogfood runs proposal 0030 already specified (2+ real
Complex-tier Techplans) before promoting `workflow-v2` toward `main`. This
audit's job — pre-dogfood correctness verification — is done; dogfood
evidence is the next and only remaining gate.

---

*(This closes the audit thread opened in Report #1. Re-open if `workflow-v2`
changes further before or during dogfood.)*