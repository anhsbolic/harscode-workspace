# 0034 — Workflow-v2 proportional Techplan and verification ownership refinement

**Status:** Accepted - Anhar
**Date:** 2026-09-15
**Protection Tier:** techplan-protected
**Triggered by:** `audits/workflow-v2-validation-01-retrospective.md`; structurally, the first workflow-v2 real-task validation showed that the Techplan contract can preserve correctness while still leaving the operator to discover too late whether independent review/decomposition are worth invoking, and can over-prescribe verification without explaining economics/phase ownership.
**Target area:** Techplan contract + synthesis routing + Build/Review/Testing verification boundaries
**Target file(s):**
- `workflow/2-techplan/template.md` — provenance metadata and verification rationale/primary-owner structure.
- `workflow/2-techplan/report-template.md` — derived-report provenance alignment.
- `workflow/2-1-techplan-synthesis-prompt.md` — proportional/fail-fast planning language plus early review/decomposition recommendations.
- `workflow/3-build-prompt.md` and `workflow/3-build/guidelines.md` — focused edit-loop verification only.
- `workflow/4-code-review-prompt.md` and `workflow/4-code-review/guidelines.md` — targeted repro only when needed to substantiate review findings; no broad final-suite replay by default.
- `workflow/5-testing-prompt.md` and `workflow/5-testing/guidelines.md` — independent final/broad verification owns the final evidence while sweeping rather than blindly replaying Build.

> Renumbering note: this proposal was `0033` on the isolated experimental branch and became final proposal `0034` when current `main` was reconciled before promotion.

## Friction Found

### 1. Optional Techplan mechanisms are discoverable too late

Validation #1 did not warrant independent Techplan review under the current Complex gate and did not benefit from decomposition. The human nevertheless had to think about invoking those mechanisms separately to learn whether they were useful.

The problem is not that the gates are wrong. The problem is routing latency: the synthesis actor has the full plan in context and can cheaply recommend `skip` versus `consider`, while the dedicated review/decomposition prompts remain responsible for the actual gate/execution if invoked.

### 2. Planning can drift toward exhaustive certainty instead of safe directional correctness

The human owner prefers fail-fast execution: settle decisions that Build must not invent, then let live implementation/review/testing expose cheap mechanical or behavioral details. A Techplan should prevent material wrong-direction work, not prove every local implementation detail before code exists.

Without an explicit proportionality reminder, synthesis/review can spend too long on details that are cheaper and safer to learn during Build.

### 3. Verification obligations lack economics and primary ownership

The Techplan currently maps Rules & Validation to a Testing Checklist but does not require a reason for a non-trivial verification method, the risk if it is skipped, or the phase/human primarily responsible for final evidence.

In Validation #1, browser/component/full verification was repeatedly executed across Build, Review, patches, and Testing. Some repetition was justified and found real defects; some broad reruns after narrow patches were not proportional.

A named tool such as Playwright can therefore become ceremonial simply because it appears in the plan, even when later phase boundaries would make one focused authoring run plus one independent final run sufficient.

## Proposed Change

### A. Proportional planning / fail-fast boundary

Techplan synthesis must resolve material decisions that Build cannot safely invent:

- product/domain semantics;
- authority/security boundaries;
- architecture/ownership decisions with meaningful blast radius;
- interface/data contracts;
- irreversible/destructive migration or operational choices;
- material risk/verification strategy;
- unresolved human decisions that block the implementation direction.

Do not pre-solve ordinary details that Build can derive safely and cheaply from current code/convention, such as local naming, routine mechanical shape, small CSS tuning, or test implementation mechanics, unless they affect a material contract.

Operational principle:

> Plan enough to make Build safe and directionally correct; use execution to learn the rest.

This is not permission to defer a material ambiguity to Build.

### B. Early independent-review recommendation from synthesis

At Techplan synthesis handoff, include:

```text
Independent Techplan review: Skip | Recommend | Required by project policy — <reason>
```

Use the existing review prompt's Complex signals as the primary clue. `Skip` is normal for a comprehensible, cohesive non-Complex plan that the human can review consciously. `Recommend` is appropriate when independent fidelity checking is likely to catch material contract loss or cross-boundary ambiguity. `Required by project policy` is reserved for an external authoritative requirement.

This is a recommendation, not a new gate. If the review prompt is invoked, its own current Complex gate remains authoritative.

### C. Early decomposition recommendation from synthesis

At Techplan synthesis handoff, include:

```text
Decomposition: Skip | Consider — <reason>
```

Recommend `Consider` only when the approved plan appears to contain genuinely independently useful execution/review/context chunks. Do not recommend decomposition because the Techplan is long.

The dedicated decomposition prompt remains responsible for the actual post-Approval decomposition gate and exact split.

### D. Verification contract records reason, risk, and primary owner

Replace the bare Techplan Testing Checklist shape with a compact table or equivalent structure that preserves 1:1 Rules & Validation coverage and records:

```text
Rule
Verification / evidence
Primary owner
Why / risk if skipped
```

Primary owner examples:

- `Build` — fast/focused edit-loop confidence;
- `Testing` — independent final/broad verification;
- `Human` — subjective/product acceptance automation cannot decide.

Code Review is normally a reasoning phase rather than the primary owner of a planned test suite. It may run a targeted repro/check when necessary to substantiate a suspected finding.

A newly added/changed automated test may still be run in Build even when Testing is the primary final-verification owner; Build must establish that the artifact it authored is executable. This does not make Build the final broad-verification phase.

### E. Sharpen phase verification ownership

#### Build

Run ordinary fast verification that gives credible edit-loop feedback for changed behavior. Run newly added/changed tests enough to prove they work. Do not replay broad Testing-owned suites merely for extra confidence unless target-repo authority explicitly requires them at that point or the current patch materially changes the relevant risk.

After a narrow patch, rerun affected verification. Broaden only when the patch changes scope/risk or a broader suite is the only credible way to prove the patch.

#### Code Review

Review the current diff through Safety, Quality, Stack-Specific, and Consistency reasoning. Execute a targeted reproduction/check when it is needed to prove or disprove a suspected finding. Do not run the final full test matrix by default simply because Review is independent.

#### Testing

Own independent final/broad verification according to the Techplan and target-repo authority. Continue to `SWEEP, DON'T REDO`: spot-check Build claims, close deferred gaps first, execute Testing-owned evidence, and avoid rewriting/replaying equivalent tests without a verification reason.

### F. Verification tool rationale

When a non-trivial tool/technique is named — e.g. browser automation, production build, race detector, load test, security scan, human rendered acceptance — the Techplan must make clear why it is appropriate and what meaningful risk remains if omitted.

This allows the human to judge verification economics before approving the plan instead of discovering the cost only during Build/Testing.

## Rationale

This change is genuinely structural despite originating from one validation run because it changes the contract boundary shared by every downstream phase: what is resolved before Build, how optional planning mechanisms are routed, and which phase owns verification evidence.

It preserves the correctness floor demonstrated by Validation #1:

- independent Review/Testing remain;
- Build still verifies what it changes;
- specialized/final verification is not removed;
- human acceptance remains required when the contract says automation cannot decide the outcome.

The change targets duplicated verification and operator uncertainty, not minimum token count.

## Explicit non-goals

This proposal does **not**:

- make Techplan review mandatory;
- eliminate Techplan review;
- make decomposition mandatory;
- weaken material Techplan completeness;
- create a separate Patch phase;
- prohibit Playwright/browser automation;
- move all tests out of Build;
- let Code Review or Testing edit production code;
- replace human judgement with a cost heuristic.

## Validation expectation

Apply only on `workflow-v2`, freeze a new candidate checkpoint, then validate on a different real task. Success means same-or-better correctness with clearer human routing and less unjustified repeated verification. Do not promote to `main` from Validation #1 alone.

---

*Accepted by the human owner after Validation #1 discussion. The proposal is techplan-protected because it changes `workflow/2-techplan/template.md` / `report-template.md`; the structural cross-phase verification issue justifies the protected-tier change.*
