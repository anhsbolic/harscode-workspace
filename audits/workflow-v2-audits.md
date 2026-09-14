# Audit Report — `workflow-v2` vs `main`

**Repo:** anhsbolic/harscode-workspace
**Branch under audit:** `workflow-v2` (dogfood-frozen baseline `6edc1a6`)
**Compared against:** `main` (`fbeb2e6`), merge-base `fbeb2e6`
**Related proposal:** `proposals/0030-workflow-v2-context-efficiency-and-handoff.md` (Status: Proposed, Experimental)
**Audit date:** 2026-09-14
**Auditor:** Claude, at Anhar's request
**Status:** CLOSED — 6 findings confirmed (2 critical, 2 moderate, 2 low-moderate); see Final verdict at the end

## Scope & method

`workflow-v2` is a large context-efficiency/handoff rewrite: 41 files changed,
+2536/-3272 lines vs `main`. Given the blast radius, this audit does not assume
"shorter = safe" or "shorter = broken" — each file is diffed line-by-line
against `main`, and every removed passage is checked for whether its *meaning*
survived somewhere else (not just whether its words survived). Special
attention goes to internal self-contradictions (a file's own instructions
disagreeing with each other), since that is a defect class specific to a
heavy compression pass and not something a stat count (`+X/-Y`) can surface.

Severity scale used below:
- **Critical** — reintroduces a previously-fixed, previously-incident-causing
  defect class, or removes a hard stop with no equivalent left anywhere.
- **Moderate** — real loss of robustness/auditability, but not tied to a
  known past incident and not a silent hard-stop removal.
- **Low** — wording/rationale compression with no behavior change identified.
- **Note** — observation worth tracking during dogfood, not a defect.

## Summary of file size deltas (protected Techplan files)

| File | `main` lines | `workflow-v2` lines | Δ |
|---|---|---|---|
| `workflow/2-techplan/rules.md` | 212 | 107 | -50% |
| `workflow/2-techplan/guardrails.md` | 125 | 57 | -54% |
| `workflow/2-techplan/template.md` | 178 | 132 | -26% |

## Findings

### F1 — [CRITICAL] Hardcoded section numbers reintroduced in the independent review prompt, contradicting the file's own runtime-resolution instruction

**File:** `workflow/2-2-techplan-review-prompt.md`

**What `main` does:** Contains an explicit, mandatory "Step -1 — Resolve
section numbers first," with a documented incident in its own Notes section:
a prior version of this same prompt hardcoded `§4`/`§12`/`§14`, `template.md`
later moved Open Items from `§14` to `§13`, and the prompt kept silently
checking the stale section — undetected until this fix. The fix deliberately
uses section **names**, resolved at runtime, everywhere in the checks.

**What `workflow-v2` does:** Compresses "Step -1" into one line — "Resolve
current template section names/numbers before checking; do not rely on
numbers remembered from an older template" — then, in the very next block
(Check 1, "Rule fidelity"), writes:

```
- Every §4 rule traces to real requirement/Exploration evidence...
- Every §4 rule has §12 verification coverage.
```

This hardcodes `§4`/`§12` directly in the check body, in the same file that
just instructed the reader not to rely on remembered numbers. It happens to
be correct today (current `template.md`: §4 = Rules & Validation, §12 =
Testing Checklist), so the defect is latent, not yet observable in output.

**Why this matters:** This is not a generic "numbers might drift" risk — it
is the exact defect class this file was already bitten by and fixed once.
The rationale paragraph that explained *why* hardcoding is dangerous here was
also the paragraph removed in the compression pass, which is plausibly why
the regression was reintroduced unnoticed.

**Correction after further review (see F2):** `main` was not actually clean
everywhere — `5-testing-prompt.md` on `main` already hardcodes `§ 4`/`§ 12`
for the same techplan sections, and its own note in `2-2-...` explicitly
flagged `2-1-techplan-synthesis-prompt.md` and `2-3-...` as "same fragility,
... out of scope for this fix." So the fragility class was known and already
present elsewhere on `main`. What makes this specific instance still the
most serious finding: `2-2-techplan-review-prompt.md` is the **one file
that had already been fixed** against exactly this bug, with the fix's own
rationale on record — and `workflow-v2` is the change that undid it, in the
same compression pass that deleted the rationale explaining why it mattered.

**Recommendation:** Replace `§4`/`§12` in Check 1 (and audit Checks 2–6 for
the same pattern) with resolved section **names**, matching Step 0's own
instruction. Consider keeping a one-line version of the original incident
note — it is exactly the kind of rationale `AUTHORING.md` itself says earns
its space ("records a non-obvious trade-off... explains a proven failure
mode").

**Status:** Confirmed, unresolved as of this audit.

---

### F2 — [MODERATE] Hardcoded-section-number fragility widened, not narrowed, by the rewrite

**Files:** `workflow/2-1-techplan-synthesis-prompt.md` (primarily); pattern
also present pre-existing in `workflow/5-testing-prompt.md` on both branches.

**Measurement:** counted literal `§<number>` references to `techplan.md`
sections in each phase prompt:

| File | `main` | `workflow-v2` |
|---|---|---|
| `2-1-techplan-synthesis-prompt.md` | 1 (`§12`, with an explicit "verify the actual number against this template.md, don't assume" caveat right next to it) | 6 (`§4`, `§5`, `§10`, `§12`, `§13` — no caveat) |
| `2-2-techplan-review-prompt.md` | 0 live checks (names only; historical numbers appear only in the Notes narrative explaining the past bug) | 2 (`§4`, `§12`, live in Check 1 — see F1) |
| `5-testing-prompt.md` | 4 (`§ 4`, `§ 12` repeated) — pre-existing, not introduced by v2 | 3 (`§4`, `§12`) — carried forward, not worsened |

**What this means:** `main` was already inconsistent about this (it fixed
the bug in one file and left the same risk in `5-testing-prompt.md`, as its
own notes admit). `workflow-v2` does not close that gap — it goes the other
direction, adding five new hardcoded template-section references to
`2-1-techplan-synthesis-prompt.md` (the file that *writes* `techplan.md` in
the first place) with no "verify, don't assume" caveat anywhere, on top of
un-fixing `2-2`. Net effect of the rewrite on this specific defect class:
worse, not better, even though nothing in proposal 0030's stated goals
targeted this area at all — it is a side effect of the compression pass,
not a deliberate design choice.

**Why this matters beyond the individual instances:** this is exactly the
"correctness density" failure mode `AUTHORING.md` itself warns about —
rationale that "cannot change behavior" is a fine thing to cut, but the
`2-2` Notes paragraph is rationale that *did* change behavior (it's the
reason a fix exists at all). Cutting it looks safe by the file's own
authoring heuristics and wasn't.

**Recommendation:** Treat this as one fix, not two — do a single pass across
every canonical phase prompt (`2-1`, `2-2`, `2-3`, `5-testing`) that resolves
`techplan.md` section references by name/anchor at runtime, consistently,
and re-add one line of rationale (not the full historical narrative) so a
future compression pass doesn't repeat this.

**Status:** Confirmed, unresolved as of this audit.

---

## Positive findings (not defects — noted for balance)

- `template.md`: added stable IDs (`Q1` requirements, `R1`/`R2` rules, `D1`
  decisions, `RISK-1` risks) and an explicit evidence-anchor column in the
  Test Focus Pointer table. This is a genuine traceability improvement over
  `main`, independent of the context-efficiency goal, and directly supports
  fixing F1/F2 (IDs are more drift-resistant than bare section numbers).
- `2-3-techplan-decomposition-prompt.md`: added an explicit STOP rule when
  decomposition exposes a material decision/risk/contract missing from the
  parent spine ("the Techplan needs revision/human gate... not a hidden
  child-task fix") — this did not exist in `main` and closes a real gap.
- `guardrails.md` and `rules.md`: despite ~50% line reduction each, a
  full read-through found all 12 guardrails and all 11 rules present with
  intact meaning, just denser wording. The compression methodology itself
  is largely sound; F1/F2 are localized regressions, not evidence the whole
  approach is unsafe.

---

### F3 — [LOW-MODERATE] `workflow-v2`'s rewrite of `workflow/README.md` drops a heading that an accepted proposal cites by name

**Files:** `workflow/README.md` (v2 rewrite); `proposals/0029-domain-grouped-projects-and-closure-review.md` (unchanged, cites the old heading).

**What happened:** `main`'s `workflow/README.md` has a short standalone
section `## What's Explicitly Out of Scope Here` (3 lines: project-specific
conventions belong in the target repo, not here). `workflow-v2`'s rewrite
folds that idea into the intro paragraph instead of keeping it as an
addressable heading. The *meaning* survives, but the **heading is gone**.

`proposals/0029-...md` — an already-Accepted, still-governing proposal,
copied unchanged onto `workflow-v2` — cites this exact heading as its
justification for why domain-level guidance must be conditional:

> "`workflow/` is meant to be generic and portable across projects
> (`workflow/README.md` § What's Explicitly Out of Scope Here)."

On `workflow-v2`, that citation now points at a heading that doesn't exist.

**Wider pattern:** the same rewrite also renamed `## Session Boundaries` →
`## Context and session boundaries` and `## Response Style By Phase` →
`## Response style`. Several proposals (0024, 0025, 0028) cite the old
names. These are lower-stakes than F3 because the citing documents are
`proposals/` history (Cold reference, not a runtime-loaded authority), but
it's the same defect class: **a rewrite pass changed headings without a
pass to update or verify inbound citations.**

**Why this matters:** the whole point of this workspace's link-instead-of-restate
convention (`AUTHORING.md` § One semantic source of truth) is that a link stays
valid. A rewrite that changes headings without grepping for inbound `§ <Heading
Name>` citations quietly breaks that convention's own precondition — ironic
given this rewrite is the one that formalized the convention in `AUTHORING.md`.

**Recommendation:** before merge, grep every `*.md` in the repo for `§ <heading>`
citation patterns pointing at `workflow/README.md`, `2-techplan/*.md`, and
`context-management.md`, and fix or intentionally accept each stale one.
Cheap to do, easy to skip, and exactly the kind of thing that's invisible
until someone follows the link mid-task.

**Status:** Confirmed, unresolved as of this audit.

---

### F4 — [CRITICAL] Mandatory build-report self-confirmation for race/perf/security tests removed, with no equivalent left anywhere

**File:** `workflow/3-build-prompt.md`

**What `main` does:** the Build report's **Output format** contains a fixed,
mandatory line the agent must fill in every single iteration:

> "Confirm explicitly: no `-race`, perf/load, or security-class test was
> run in this iteration."

This is a forcing function, not a reminder — it makes the agent produce an
affirmative statement every time, rather than relying on it having read and
remembered a prose rule earlier in the session. Per this workspace's own
recorded history (`principles-and-workflow.md` / this workspace's retro),
this exists because of a **real incident**: a bcrypt + race-detector test
accidentally pulled into the Build loop caused a ~2 hour stall. That incident
is why tiered testing (unit/mocked/API-contract in Build; race/perf/security
exclusively in Testing) became a hard rule in the first place.

**What `workflow-v2` does:** the equivalent report field is now:

```
## Deferred / not tested here
[verification deliberately left for independent Testing, with reason; "none" if none]
```

This is free text, optional in effect ("none" if none), and framed as *what
was deferred* rather than a forced *affirmative confirmation that heavyweight
tests were not run*. The prose rule survives (`3-build-prompt.md`'s
VERIFICATION section: "Do not pull heavyweight race/perf/security-class
verification into this tight loop..."; `3-build/guidelines.md`: "Race/
concurrency, performance/load, and security-class sweeps belong to
independent Testing..."), but the **mechanical forcing function is gone**,
and it is not relocated to `guidelines.md` or `checklist.md` either — grepped
both, no equivalent exists anywhere in `workflow-v2`.

**Why this is Critical, not Moderate:** this is the one instance in the audit
so far where a rule that exists *specifically because prose alone already
failed once* (that's the whole reason the mandatory confirmation line was
added instead of just stating the rule) had its enforcement mechanism
removed and downgraded back to prose plus an optional-shaped field. This is
the same failure shape as F1 — a fix that exists because of a documented
incident gets compressed away because, read in isolation, it looks like
redundant reinforcement of a rule stated elsewhere.

**Recommendation:** restore a mandatory, non-omittable confirmation line in
the Build report format — e.g. `## Verification scope confirmation` +
`Confirm: no race/perf/security-class test executed in this iteration
(Y/N + reason if Y)`. This is cheap (one line) and directly closes the gap
without reverting any of the surrounding context-efficiency changes.

**Status:** Confirmed, unresolved as of this audit.

---

### F5 — [MODERATE] `model-routing.md` pointer removed workspace-wide, and the review prompt's "different model" requirement softened to "when practical" with its incident rationale deleted

**Files:** `workflow/2-2-techplan-review-prompt.md`, `2-3-techplan-decomposition-prompt.md`, `3-build-prompt.md`, `4-code-review-prompt.md`, `5-testing-prompt.md`, `workflow/README.md`.

**Measurement:** `git grep model-routing` inside `workflow/` on `main` returns
8 hits across 6 files. The same search on `workflow-v2` returns **zero**.
Every phase prompt that used to point at `best-practices/model-routing.md`
for tier×stage routing — including the note that Testing is currently
flat-routed with "no dual-model requirement at this stage today," which is
itself useful information — no longer points anywhere.

The more specific loss is in `2-2-techplan-review-prompt.md`'s own framing.
`main`'s Purpose section:

> "An independent second-pass review of a synthesized `techplan.md`, run by
> a **different model** than the one that produced it... This exists because
> the driving story's three review passes (2026-08-13) showed that a model
> checking its own output against a self-check list is not equivalent to an
> independent check. Proposal 0002's diagram-syntax and severity gaps, and
> proposal 0003's R18 recurrence... were all found specifically because a
> *different* actor... looked at the same artifact with fresh eyes."

`workflow-v2`'s version:

> "Independent adversarial verification of a synthesized Techplan. Use a
> different reviewer/model/actor from the primary synthesis **when
> practical**; this is review, not re-synthesis."

The categorical requirement became a soft preference, and the two-incident
citation that justified the requirement is gone along with the pointer to
where the "mandatory dual-model row" was recorded.

**Why Moderate and not Critical:** `2-2-techplan-review-prompt.md` is
explicitly Draft on both branches — it was never a protected, enforced gate
to begin with, so this isn't un-doing a locked rule the way F1/F4 are. It's
also consistent with proposal 0028's deliberate, previously-recorded choice
(R6) to keep model-routing decisions out of generic phase prompts. But 0028
said it would *not edit* `model-routing.md` and leave it as "the generic
routing reference for its rows" — it did not say every pointer *to* it should
disappear from the phases that need to know it exists. The workspace's own
memory calls dual-model review at Expert tier "non-negotiable... validated by
real incidents" — that context is what's now missing from the one file whose
entire purpose is to be that dual-model check.

**Recommendation:** keep the "when practical" softening if that's an
intentional execution-profile decision (per 0028's layering principle), but
restore one pointer per phase prompt to wherever routing tier/model
requirements now live, so the requirement doesn't silently become
undiscoverable. Consider re-adding a compressed one-line version of the
incident citation in `2-2-...`'s Notes.

**Status:** Confirmed, unresolved as of this audit.

---

### F6 — [LOW-MODERATE] "Never merge your own proposal" self-approval guardrail dropped, no equivalent anywhere

**Files:** `best-practices/AGENTS.md`, `harness-optimization/AGENTS.md`.

**What `main` does:** both files end their proposal-routing bullet with an
explicit, categorical rule: *"...using the template in `../proposals/README.md`.
**Never merge your own proposal.**"* — a separation-of-duties guardrail so
the actor writing a proposal isn't also the one approving/merging it into a
proposal-gated protected tree.

**What `workflow-v2` does:** both files were rewritten; neither retains this
sentence in any form. `proposals/README.md` — the file both bullets point to
— is byte-for-byte unchanged between `main` and `workflow-v2` and doesn't
contain the rule either. Grepped the full `workflow-v2` tree for `merge your
own`, `self-merge`, `self-approv`: zero hits anywhere.

**Why lower severity than F1/F4/F5:** not tied to a documented incident, and
Anhar works largely solo with AI agents rather than a multi-committer team,
so practical exposure is lower. Still worth flagging: it's a categorical
"Never" rule that silently vanished rather than being consciously kept,
moved, or retired — the same compression-pass pattern as the other findings.

**Recommendation:** restore the line in both `AGENTS.md` files, or move it
once into `proposals/README.md` (the more correct single source of truth,
since both callers already point there) and let both bullets rely on that.

**Status:** Confirmed, unresolved as of this audit.

---

## Pre-merge checklist (derived from all findings)

- [ ] F4 — restore a mandatory, non-omittable race/perf/security confirmation
      line in `3-build-prompt.md`'s report format (**highest priority** — tied
      to a real ~2h incident, currently no equivalent exists anywhere)
- [ ] F1 — fix hardcoded `§4`/`§12` in `2-2-techplan-review-prompt.md` Check 1
- [ ] F2 — do one consistent pass across `2-1`, `2-2`, `2-3`, `5-testing` for
      section-reference resolution (name/anchor at runtime, not hardcoded number)
- [ ] F5 — decide deliberately whether dual-model independent review is still
      a requirement or now a preference, and restore at least one pointer per
      phase prompt to wherever that decision now lives
- [ ] F3 — grep-audit all `§ <Heading Name>` citations repo-wide against the
      renamed/removed headings in the rewritten `workflow/README.md`
- [ ] F6 — restore or relocate "never merge your own proposal" into
      `proposals/README.md` or both `AGENTS.md` files
- [ ] Re-add a short (1-line) version of the "why runtime-resolution matters"
      rationale that F1/F2 identify as removed — a `AUTHORING.md`-compliant
      compression, not a restoration of the full paragraph

## Audit coverage — final

**Line-by-line diffed and read in full:** every canonical phase prompt
(`1-exploration-kickoff-prompt.md`, `2-1`, `2-2`, `2-3`, `3-build-prompt.md`,
`4-code-review-prompt.md`, `5-testing-prompt.md`), every protected Techplan
file (`rules.md`, `guardrails.md`, `template.md`), both new files
(`context-management.md`, `AUTHORING.md`), root `README.md` + `AGENTS.md`,
`workflow/README.md` + `AGENTS.md`, `best-practices/AGENTS.md`,
`harness-optimization/AGENTS.md`, `harness-optimization/codex/session-boundaries.md`,
`harness-optimization/claude-code/backend/slash-commands.md` + `subagents.md`,
`harness-optimization/token-optimization.md`.

**Checked by targeted grep/diff (removed-line scan, not full re-read):**
`4-code-review/checklist.md` + `guidelines.md`, `5-testing/checklist.md` +
`guidelines.md`, `1-exploration/guidelines.md`, `model-routing.md`
cross-reference count workspace-wide, `harness-optimization/codex/skills.md` +
`instruction-loading.md` + `token-optimization.md`,
`best-practices/react/testing-automation-boundary.md`.

**Not individually audited (lower-risk translation mirrors of already-checked
backend equivalents, same rewrite author/pass, no new defect *type* expected):**
none remaining — see final spot-check note below.

**Final spot-check (done after initial close):** `harness-optimization/claude-code/frontend/slash-commands.md`,
`subagents.md`, and `claude-code/token-optimization.md` were diffed for the
same six patterns. Result: canonical-prompt routing language ("never copies
content inline," "never the phase folder directly") survives, just reworded
("the body points to the canonical Harscode prompt"). The only drops found
are more `model-routing.md` pointers disappearing — already covered by F5,
not a new finding. No 7th finding from this pass.

## Final verdict

**Do not merge `workflow-v2` to `main` as-is.** Not because the underlying
idea is bad — the context-efficiency direction is sound, the compression
methodology is mostly disciplined (`rules.md`/`guardrails.md` full reads
confirmed no material meaning loss), and several changes are genuine
improvements over `main` (stable IDs in `template.md`, the shadow-contract
STOP rule in decomposition, the codex session-boundaries file collapsing
~90 lines of duplication into a clean pointer to `context-management.md`).

The reason to hold: **six findings, and four of them (F1, F4, F5, F6) share
one root cause** — categorical/mandatory language ("never," "must," "confirm
explicitly," "run by a different model") that exists *specifically because
softer prose already failed once* gets read as safely compressible by a
pass optimizing for "correctness density," and isn't. That is a systematic
blind spot in how this rewrite was done, not six unrelated typos. Proposal
0030's own Quality Preservation Constraint #1 ("no material rule or
authority is lost") is not yet satisfied by the evidence in this report.

**Path forward:** fix F4 and F1 first (cheapest, highest-consequence, both
map to real incidents already paid for once). Then do one targeted pass
across the whole branch searching specifically for categorical language
(`never`, `must`, `always`, `confirm explicitly`, `stop and`) that existed
on `main` and checking each instance survived intact — that single targeted
pass would likely catch F1/F4/F5/F6 as one class of fix rather than four
separate ones, and is far cheaper than re-reading all 41 files diff-by-diff
the way this audit did. Once that pass is done and re-verified, the dogfood
plan proposal 0030 already lays out (2+ real Complex-tier runs, `main`
untouched as baseline) is the right next gate — this report is a pre-dogfood
correctness check, not a substitute for it.

---

*(Audit closed. Re-open with new findings if `workflow-v2` changes further.)*

---

*(Further findings appended below as the audit continues.)*