# 0042 — Claim-scoped verification and phase applicability

**Status:** Accepted - Anhar
**Date:** 2026-10-12
**Protection Tier:** general
**Triggered by:** Kencleng Pilot #3 C1 CRTV after repeated Review/Testing/security-routing work exposed a mismatch between proportional-verification guidance and how downstream phases can still be interpreted as chronology-driven rituals. The concrete evidence includes narrow patch/re-review loops, verification intentionally deferred until faithful FE/backend integration exists, and Human questions about whether required checks may be omitted, deferred, or accepted as residual risk.
**Target area:** orchestration + lightweight Review/Testing workflow routing
**Target file(s):**
- `README.md` — clarify that Build → Review → Testing is the default engineering path, not unconditional ceremony when an independent phase is materially not applicable.
- `orchestration/AGENTS.md` — add hot-path claim/evidence/applicability reasoning before dispatching Review/Testing.
- `orchestration/run-contract.md` — define claim-scoped phase applicability and Human verification-decision boundaries without adding protocol objects/states.
- `workflow/AGENTS.md` — clarify routing of Review/Testing as applicable independent concerns rather than filesystem/chronology obligations.
- `workflow/4-code-review-prompt.md` — state that applicability is decided before invocation; once Review is invoked, all four passes remain mandatory.
- `workflow/5-testing-prompt.md` and `workflow/5-testing/guidelines.md` — make acceptance scope explicit and distinguish evidence reuse, N/A, deferral, Human risk acceptance/waiver, and actual verification results.

## Gap found

Current Harscode already contains most of the required mechanisms:

- Proposal 0034 established proportional verification ownership and the principle that a named tool is not a ritual.
- The Techplan Testing Checklist records rule/evidence, primary owner, and `Why / risk if skipped`.
- Build and Testing already discourage blind broad-suite replay.
- A narrow Review-requested patch does not automatically require another full four-pass Review.
- `PHASE_ROUTE` already permits an independent phase to be recorded N/A without creating a fake skipped-phase Run.
- Testing can reuse current authoritative evidence and supports `Pass with flagged follow-ups`.
- `HUMAN_REQUIRED` already covers authority-changing and material risk-acceptance boundaries.

However, these rules are distributed and do not currently form one explicit decision model.

The default README lifecycle still reads as Build → Code Review → Testing → PR. Review and Testing prompts assume they have already been invoked. The Run Contract says an independent phase can be N/A but does not define the claim/evidence criteria for that decision. Human material risk acceptance exists generically but verification guidance does not explicitly distinguish:

- genuinely not applicable;
- already satisfied by current evidence, so no rerun is needed;
- deferred because faithful evidence belongs to a later integration horizon;
- required evidence intentionally waived/changed by its owning authority;
- residual risk explicitly accepted while the technical claim remains unverified.

This ambiguity can produce two opposite failures:

1. **over-protection:** every Build/re-entry mechanically creates Review/Testing/broad reruns even when no material uncertainty or independent claim remains;
2. **under-protection:** a Human “skip” is interpreted as if missing technical evidence became PASS.

Kencleng C1 exposed both pressures. Some evidence, such as real Google login and full integrated UI/cache/semantic behavior, is more faithfully collected after FE/backend integration. Other backend/security/DB claims remain executable now. Treating all deferred evidence as a common blocker can create artificial sequencing deadlocks; treating a Human defer/waiver as technical PASS would create false assurance.

## Proposed change

### A. Verification is claim-scoped

Add the shared invariant:

> Verification exists to substantiate a declared claim/acceptance boundary. A phase or check is required when the current contract, risk, dependency condition, or unresolved claim requires evidence that the phase/check materially provides. Workflow chronology alone is not sufficient justification.

Before dispatching independent Review or Testing, identify:

```text
claim / acceptance boundary being considered
→ evidence required by current authority/risk
→ current evidence already sufficient and still applicable
→ material evidence still missing/stale/disputed
→ cheapest faithful independent mechanism that closes that gap
```

Do not create Review/Testing merely because the previous phase ended.

This does not remove Review or Testing from the default engineering path. It makes their applicability explicit.

### B. Review applicability before invocation

Before creating a Review Run, ask what material independent reasoning it is expected to add.

Review is normally justified by material production behavior, contract, architecture, security/authority risk, a broad or uncertain diff, a disputed finding, or an explicit project requirement.

A mechanical/narrow delta may be Review N/A when settled authority and existing evidence make independent reasoning materially unnecessary.

If Review is invoked, its canonical contract remains unchanged:

- all four passes run;
- no pass is skipped because an earlier one is clean;
- Review does not silently mutate production code;
- targeted reproduction is used only when it resolves a concrete review question.

Thus:

```text
Review applicability → conditional
Review internal discipline after invocation → mandatory
```

### C. Testing applicability and evidence selection

Testing is not a requirement to recreate every Build check. The obligation is sufficient, current evidence for the claim being accepted.

Testing must distinguish:

- evidence that is already current and can be credibly reused;
- evidence needing independent spot-check/final execution;
- evidence that is materially deferred to a later observable/integration horizon;
- evidence that remains required and blocking for the current claim;
- Human-owned decisions or Human-performed scenarios.

A Testing Run may be N/A when no current acceptance claim requires independent evidence uniquely supplied by Testing, no target-project authority mandates the phase, and all relevant required evidence is already current through authoritative equivalent mechanisms.

If Testing is invoked, its declared scope/claim must be explicit. `Pass` and `Pass with flagged follow-ups` apply only to that declared scope; they must not imply broader acceptance whose required evidence remains deferred/unestablished.

### D. Do not use bare “skip” as durable semantics

When a Human or Orchestrator says a Review/check/test should not run, translate the intent into its actual semantic class rather than recording ambiguous `skip`.

Use ordinary prose/Decision evidence, not a new enum/state machine:

```text
Not applicable
→ this phase/check does not materially apply to the current claim.

Satisfied by current evidence
→ no rerun; cite the authoritative current evidence and why it remains applicable.

Deferred
→ obligation remains; evidence will be collected at a later declared boundary.
   The deferred item is not PASS and blocks only claims/dependencies that actually require it.

Authority waiver / contract change
→ the owning authority removes or changes a previously required verification obligation.
   Reconcile the owning authority artifact when the change is material.

Residual-risk acceptance
→ the owning Human/project authority knowingly permits progression despite absent/failing evidence.
   Record the risk/decision and affected boundary; do not report the technical behavior as verified.
```

If the exact meaning is unclear, ask the owner rather than guessing which class was intended.

### E. Human authority cannot manufacture evidence

Add the invariant:

> Human authority may change requirements, defer evidence, waive an obligation within its authority, or accept residual risk. It cannot convert verification that was not performed into technical evidence that the behavior passed.

Examples:

```text
Human: defer real Google login until integrated UI exists
→ legitimate scheduling/evidence-horizon Decision
→ real-provider behavior remains unverified

Human: accept release risk without concurrency verification
→ legitimate only for the owner of that risk/acceptance boundary
→ concurrency behavior remains NOT ESTABLISHED unless independently proven

Human: remove the concurrency-verification requirement
→ material authority change
→ update/reconcile the owning contract before downstream agents treat it as no longer required
```

A Human-owned decision does not override an external/regulatory/project authority that the Human does not own.

### F. Preserve dependency semantics

A missing verification item blocks only the declared dependent boundary whose satisfaction condition requires it.

For a HARD dependency:

- do not cross the declared boundary while required evidence is absent;
- if the semantic owner validly changes the condition/requirement, reconcile that authority first;
- Human risk acceptance does not silently mark the old evidence condition satisfied.

This prevents broad deferred integration evidence from freezing unrelated backend or downstream work.

### G. Acceptance and verdict scope

Testing/Orchestrator reports must avoid whole-system language when verification is bounded.

A clean or conditional verdict answers:

```text
What exact claim/scope is supported by this evidence?
What remains deferred/unverified?
Does any remaining item block this claim, or only a later claim?
Was any missing evidence explicitly accepted as risk rather than technically verified?
```

`Pass with flagged follow-ups` is valid only when those follow-ups are non-blocking for the declared accepted scope.

### H. No protocol expansion

Do not add:

- a `WAIVED`, `DEFERRED`, or `SKIPPED` execution status;
- a new Review/Testing state machine;
- a universal risk score;
- mandatory cost scoring;
- a new verification object/registry.

Use existing Decisions, authority artifacts, dependency conditions, Run applicability, and durable evidence.

## Rationale

This proposal extends rather than reverses Proposal 0034.

0034 established verification economics and primary ownership:

- Build owns focused edit-loop evidence;
- Review reasons independently without broad-suite ritual;
- Testing owns independent final/broad evidence;
- non-trivial checks carry a reason and risk if skipped.

C1 CRTV exposed the next ambiguity: even with proportional execution inside phases, the system still needs a clear rule for whether the phase/check is applicable to the claim being made and what a Human decision to omit it actually means.

Claim-scoped verification preserves the correctness floor while reducing ceremony:

- required claims still need sufficient evidence;
- existing current evidence can be reused;
- deferred integration evidence stays visible without becoming a false failure or false PASS;
- independent phases run when they provide material value;
- Human authority remains strong without becoming fictional technical evidence;
- HARD dependency conditions continue to fail closed unless their owning semantics are legitimately changed.

The Techplan protected template does not need an initial change. It already carries rule-level verification, primary owner, and `Why / risk if skipped`. The proposed first implementation should clarify routing/acceptance semantics around that existing contract. Change protected Techplan guidance later only if CRTV shows the current fields are insufficient.

## Explicit non-goals

This proposal does **not**:

- make Review or Testing opt-out by default;
- eliminate independent verification;
- let Orchestrator waive project/security requirements;
- let Human approval relabel missing/failing technical evidence as PASS;
- make every open follow-up non-blocking;
- weaken target-repository required final commands;
- permit crossing a HARD dependency without evidence or a legitimate owning-authority change;
- require all verification to wait for end-to-end integration;
- create a new phase/status/registry/scoring system.

## Validation expectation

Validate on the remainder of Kencleng C1 before wider promotion.

Useful evidence would include:

- whether the Orchestrator can decide Review/Testing applicability from claim + risk rather than chronology;
- whether backend-only verification can progress while integrated/UI/provider evidence is explicitly deferred;
- whether narrow patch loops stop when additional independent evidence has no material value;
- whether Human defer/waive/risk decisions remain reconstructable without false PASS claims;
- whether T2→T3 dependency routing respects the exact observable satisfaction condition rather than requiring whole-T2 final acceptance.

Do not promote this proposal to operational `main` from discussion alone.

---

*After human review: update the Status above. If Accepted, apply the approved change to the target documents and leave this proposal in place as changelog evidence. See `proposals/README.md` for the general-tier proposal process.*
