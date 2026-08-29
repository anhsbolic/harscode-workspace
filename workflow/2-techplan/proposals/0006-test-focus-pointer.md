# Proposal: Test Focus Pointer — carry concurrency/perf/security test scope from exploration into the techplan, without turning techplan into a test plan

> Status: Proposed
> Date: 2026-08-27
> Triggered by: Real incident — a build/patch loop stalled ~2 hours
> running a full race-detector pass (with production-cost bcrypt) that
> should never have run in that phase at all. Root discussion concluded
> the missing piece isn't just "tier the testing phases" (already fixed
> at the best-practices level, see root `proposals/0008`) but that
> nothing currently tells the *testing* phase which areas of a given
> story actually need race/perf/security-class tests versus the default
> build-loop set (unit/mocked/API-contract).
> Target: `template.md` § 12 (new subsection), `rules.md` (new § 9),
> `guardrails.md` (new § 12), `guidelines.md` (new step), `examples.md`
> (new example, directly appendable — included here for review
> convenience, not gated on this proposal's acceptance)

## Friction Found

Two options were considered for where "which test classes does this
story need" should live:

1. Techplan gets a full test-plan section (scope, tooling, thresholds
   per area).
2. Techplan stays clean of test-plan detail; testing phase derives
   everything fresh from raw exploration docs.

Option 1 was rejected — it duplicates decision-making that's cheaper
and more accurate done once, in the testing phase, with full context.
Option 2 was also rejected on its own: raw exploration docs are a
point-in-time snapshot from Stage 2, before techplan review/synthesis
can cut scope, merge areas, or change the implementation approach. If
the testing phase reads exploration docs directly and techplan diverges
from what exploration originally flagged, there's no way to tell
"deliberately scoped out during synthesis" from "just never carried
forward" — the same class of drift this workspace already formalized a
fix for once, between the Summary and the full plan (§ 11,
`proposals/0003`).

The concrete failure mode this proposal targets: an area gets flagged
as concurrency-sensitive during exploration's Sniffing Checklist (Risk
lens), techplan synthesis doesn't carry that forward in any form, and
by the testing phase there's no trace of it left anywhere in the
techplan artifact — the testing phase either misses it entirely or has
to re-derive it from scratch by re-reading raw docs and hoping nothing
changed since.

## Proposed Change

A thin **pointer**, not a test plan — added inside the existing § 12
Testing Checklist section (no renumbering of the rest of the template).

**`template.md` § 12** — add a subsection after the existing checklist:

```markdown
### Test Focus Pointer (carry-over from exploration Risk lens)

Areas flagged as concurrency/perf/security-sensitive during exploration
Stage 2 (`sniffing-checklist.md` § Risk) that are still relevant after
synthesis — a pointer for the testing phase, not a full test plan.

| Area | Why sensitive | Still relevant post-synthesis? |
|---|---|---|

Only list areas that survived synthesis and remain relevant — an area
flagged during exploration but dropped/changed during synthesis is
implicitly "N/A, see § 5 Decision Log for why," not restated here. This
is a pointer, not a test plan: race/perf/security execution detail
(scope, tooling, thresholds) is decided in the testing phase
(`workflow/5-testing/`), not here.
```

**`rules.md`** — new § 9:

```markdown
## 9. Test Focus Pointer Is Carried From Exploration, Not Invented

Section 12's Test Focus Pointer table sources from the raw exploration
docs' Sniffing Checklist § Risk findings for that story — never
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
```

**`guardrails.md`** — new § 12:

```markdown
## 12. Don't Silently Drop a Flagged Risk Area

If exploration's Sniffing Checklist § Risk flagged an area as
concurrency/perf/security-sensitive, and that area survives synthesis
in some form, it must appear in section 12's Test Focus Pointer table —
even if the answer is "no longer relevant, see § 5." Silently omitting
it (rather than marking it N/A with a reason) reproduces the same class
of gap as § 11 (Summary drifting out of sync): a reviewer or the
testing phase has no way to tell "deliberately scoped out" from
"forgotten."

If you're unsure whether a Risk-lens finding rises to Test Focus
Pointer relevance or is just an ordinary section 4 edge case — ask,
don't guess. Over-including borderline cases is low-cost (worst case,
the testing phase spends a few extra minutes confirming N/A); silently
under-including one is what lets an untested race condition or
security gap ship.
```

**`guidelines.md`** — new step (appended, doesn't renumber the existing
steps 1-10):

```markdown
11. **When populating section 12 (Testing Checklist), also populate the
    Test Focus Pointer table** (`rules.md` § 9) by cross-referencing the
    raw exploration docs' Sniffing Checklist Risk findings for this
    story. Don't silently drop a flagged area — mark it N/A with a
    reason if it didn't survive synthesis (`guardrails.md` § 12).
```

**`examples.md`** — new worked example (agent-appendable directly per
`README.md` § Governance — included here for context, not gated on this
proposal):

```markdown
## Example: a Test Focus Pointer table

Source: illustrative, modeled on the incident that triggered this
proposal (Kencleng auth story).

| Area | Why sensitive | Still relevant post-synthesis? |
|---|---|---|
| Login handler (`internal/auth/login.go`) | Shared session store, concurrent login attempts for the same account — exploration Risk lens flagged possible race on session invalidation | Y |
| Password reset token generation | Exploration flagged as security-sensitive (token entropy, reuse) — synthesis moved this to a separate, already-shipped techplan (§5), out of scope here | N — see § 5 |
| Get profile (`internal/user/profile.go`) | No shared state, read-only, single-row lookup — not flagged during exploration | (not listed — doesn't qualify per `rules.md` § 9) |

Why this is good: only two rows needed a decision at all — the profile
handler was never flagged, so it correctly doesn't appear (a table
padded with every touched file would defeat the pointer's purpose). The
reset-token row shows the "N — see § 5" pattern: still visible, not
silently dropped, with a pointer to *why* instead of the detail
repeated here.
```

## Rationale

This is the same shape of fix this workspace has already validated
twice — first for Summary/Open-Items drift (`proposals/0003`, § 11),
now applied to a different kind of carry-over (exploration → testing
scope). The alternative of skipping techplan and reading exploration
docs directly in the testing phase reintroduces exactly the
two-sources-of-truth risk `proposals/0001` already rejected once for a
different reason (human digest vs full plan as separate documents).

Genuinely structural, not a one-off: any story with a concurrency,
performance, or security-sensitive area will hit this same gap absent
a pointer mechanism — and the triggering incident (a 2-hour stalled
build loop) is exactly the kind of real, costly friction this
workspace's proposal threshold is meant to catch, even from a single
occurrence.

---

*Companion change: `proposals/0008` (root-level) fixes the
best-practices-level cause (`testing-concurrency.md`'s missing
lifecycle scoping, and the missing expensive-primitive-cost guidance).
This proposal fixes the process-level cause (nothing told the testing
phase which areas needed that tier of test). Both are needed — 0008
alone doesn't tell the testing phase *which* areas to scope
race/perf/security tests to; this proposal alone doesn't fix the
default behavior of `testing-concurrency.md` itself.*
