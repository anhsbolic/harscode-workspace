# Proposal: Workflow v2 context efficiency and phase handoff

> Status: Proposed
> Date: 2026-09-14
> Protection Tier: techplan-protected
> Triggered by: Kencleng Codex frontend dogfood — quality was satisfactory, but Exploration + Techplan + independent review consumed disproportionate context/usage and exposed broad mandatory reads, recursive re-reading, and stale Techplan guidance.
> Target: cross-workspace workflow/context routing, including `AGENTS.md`, `workflow/`, protected `workflow/2-techplan/` guidance, `best-practices/` routing, and harness translations.

> **Experimental-branch note:** the human owner explicitly authorized implementation of this proposal on `workflow-v2` for dogfood. That authorization does **not** mean this proposal is Accepted for `main`. `main` remains the proven quality baseline until workflow-v2 demonstrates same-or-better correctness in real tasks.

## Friction Found

The current workflow produces code quality the human owner is satisfied with. That quality is the floor for this experiment. The problem is not that the workflow is wrong; it is that agents are often told to load or re-load more context than the active decision requires.

The audit found four structural sources of avoidable context cost:

1. **Router files trigger broad reads.** Root `AGENTS.md` says to read the full root `README.md`; `workflow/AGENTS.md` says to read the full `workflow/README.md`; `best-practices/AGENTS.md` says to read the full `best-practices/index.md`. Those documents are useful authorities, but together they can add tens of kilobytes before phase-specific work begins.
2. **Techplan synthesis loads cold references by default.** `2-1-techplan-synthesis-prompt.md` requires `examples.md` and `retro.md` in the initial read set. `retro.md` is historical evidence and `examples.md` is calibration material; neither should be mandatory when the core rules already answer the active question.
3. **Cross-phase re-reading is too broad.** Testing can need the reason behind a Test Focus Pointer entry, but currently it is directed back to the raw Exploration corpus rather than to the exact evidence that created the pointer.
4. **Stale protected guidance creates contradictory context.** Proposal 0012 removed the embedded Techplan Summary in favor of a separate post-Approval report, but `rules.md`, `guidelines.md`, and `guardrails.md` still contain old Summary/section-14 rules. Proposal 0023 already documented this recurring defect; it remains unapplied at this baseline.

The same dogfood also showed that review-loop over-convergence can consume substantial effort after material correctness issues are resolved. Proposal 0028 added the stopping rule; workflow-v2 extends the same proportionality principle to context loading and handoff.

## Quality Preservation Constraint

Context reduction is not success by itself. Workflow-v2 is acceptable only if real dogfood shows that:

1. no material rule or authority is lost;
2. Build can execute without inventing product/domain, authority/security, architecture/ownership, or verification decisions;
3. Code Review and Testing retain the same defect-finding responsibilities;
4. material clarification/re-litigation does not increase;
5. decision, risk, contract, and unresolved-item history remains durable;
6. implementation quality is at least baseline-equivalent; and
7. unnecessary context loading or repeated reasoning is observably lower.

If efficiency improves while any of 1–6 regresses, the experiment fails and the relevant v2 change should be reverted or revised.

## Proposed Change

### A. Add a guidance-authoring standard

Add a root authoring guide for people/agents changing Harscode itself:

- optimize **correctness density**, not shortest-file size;
- default to direct prose: no filler, repeated conclusions, or rationale that cannot change behavior;
- keep one semantic source of truth and link rather than restate;
- keep examples/history separate from runtime rules;
- treat document length as a review signal, not a correctness rule;
- for frequently loaded runtime guidance, roughly 250–300 lines or 16–20 KB is a soft prompt to review cohesion, not a hard split threshold;
- split only when independent topics have independent readers/triggers;
- long cold/reference material is acceptable when it is not mandatory runtime context and is addressable by headings/indexes.

### B. Make routing progressive rather than broad-read by default

`AGENTS.md` files remain the first hard-rule/router layer, but stop requiring full rationale documents merely to route ordinary work.

Use four context classes:

- **Required** — needed to execute the current phase correctly;
- **Routing/clue** — cheap locator used to find relevant authority;
- **Conditional** — opened only when its trigger applies;
- **Cold/reference** — examples, history, retro, long rationale; opened only for a concrete need.

Best-practice discovery continues to use the existing index, but agents should target the relevant concern/category rows instead of treating the whole index as prose that must be absorbed every run.

### C. Define durable phase handoff and session transition rules

Correctness must depend on durable artifacts and live source-of-truth reads, never on chat memory alone. Same-session continuation may reuse context that is still active and unchanged; fresh sessions re-ground from the smallest sufficient durable state.

Default transition intent:

| Transition | Intent |
|---|---|
| Exploration → Techplan | Adaptive: continue or fresh based on observable continuation fitness |
| Techplan → Build | Fresh preferred |
| Build iteration → Build iteration | Continue while focused |
| Build → Code Review | Fresh for independence |
| Code Review → Patch | Return to Build authority; reuse or fresh Build based on context fitness |
| Build/Patch → Testing | Fresh for independence |
| Testing → Patch | Return to Build authority |
| Testing → PR | Flexible; ground on final repository state and durable evidence |

A meaningful phase/stage completion reports a compact handoff: completed work, artifacts, blockers/open items, recommended next step, session recommendation with reason, and context pointers needed by the next phase. This is not repeated on every progress message.

### D. Transfer code coordinates, not stale implementation facts

Exploration and Techplan may record **code anchors**: file path + symbol/section + why it matters. Build re-opens current code at those anchors before editing. Earlier prose about current implementation is evidence from that time, not a substitute for the live codebase.

Build is not a second product/domain exploration phase. If live code invalidates a material contract assumption, Build stops and reports rather than silently redesigning.

### E. Keep Techplan execution-grade while reducing non-authoritative reads

Techplan remains the agent-executable contract. Replace "full detail, no compression" as a blanket writing signal with **complete, unambiguous, execution-grade, non-redundant**.

Default synthesis reads the protected core authority it needs. `examples.md`, `retro.md`, finished examples, and diagram guidance become conditional/cold references rather than mandatory initial reads.

Apply the already-evidenced Proposal 0023 correction on workflow-v2: remove stale embedded-Summary instructions and stale section-14 references. The separate Approved human report remains the only reviewer digest.

### F. Strengthen the Techplan spine + existing decomposition mechanism

Do not create arbitrary Techplan shards. Keep `techplan.md` as the always-authoritative spine. Existing decomposition may create executable task slices after approval.

Invariant: **no material decision, risk, interface/behavior contract, verification obligation, or unresolved item may exist only in a child task file.** Child tasks may carry scoped implementation detail and point back to the spine.

A Build using decomposition reads the Techplan spine plus the current task slice; it need not load unrelated task files unless a declared dependency requires them.

### G. Make Testing follow exact evidence pointers

Extend Test Focus Pointer rows with a source/evidence anchor to the Exploration finding that justified the row. Testing follows that anchor instead of scanning the entire Exploration corpus merely to recover the reason.

Keep Testing's fresh end-to-end Techplan contradiction check during the first workflow-v2 dogfoods; independence is a correctness feature and should not be removed until evidence supports doing so.

### H. Keep patch ownership in Build

Code Review and Testing identify findings and produce patch plans. Production-code fixes are executed through Build/Patch authority. Returning to Build may continue a focused Build session or start a fresh Build session re-grounded on the approved Techplan, specific patch plan, relevant current code/diff, and latest necessary build evidence.

### I. Separate output terseness from context efficiency

Keep the existing principle: process narration is terse; required artifacts remain complete. Remove stale embedded-Summary examples from token-optimization guidance.

Context efficiency is a separate concern: load only what the active phase needs, but never use compaction or selective reading to omit material durable state.

### J. Do not mandate usage telemetry in workflow-v2

Token/model/allowance telemetry remains operator/harness observability, not a phase artifact requirement. If later useful, document how individual harnesses expose usage data without making every task report carry benchmark metadata.

## Explicit Non-Goals

Workflow-v2 does **not**:

- optimize for minimum token count at the expense of correctness;
- aggressively shorten or delete proven guidance merely because it is long;
- change project-specific Kencleng documentation in this experiment;
- redesign model routing (handled separately);
- require token telemetry in phase reports;
- turn every checkpoint into a verbose status ritual;
- let Review or Testing fix production code in their own authority lane;
- let Build rely on stale Exploration descriptions instead of live code;
- split Techplans by file size alone;
- change `main` until dogfood evidence supports adoption.

## Dogfood / Exit Criteria

Run workflow-v2 on real features while `main` stays untouched as the baseline. After each run, evaluate:

- Did any agent miss or re-litigate a material decision?
- Did Build need information that selective context loading hid?
- Did Review/Testing lose defect-finding signal?
- Did agents ask materially more clarification questions?
- Were phase handoffs sufficient for fresh sessions?
- Was context loading/re-reading observably lower?
- Was the resulting code at least as good as the established baseline?

Do not promote workflow-v2 to `main` from one successful run. Use multiple real tasks and revise this branch in place until the quality/efficiency tradeoff is credible.

## Rationale

The current workflow already produces satisfactory outcomes, so a risky "make everything shorter" rewrite would optimize the wrong metric. The safer target is knowledge delivery: keep the same durable authority, but make agents discover and load it proportionally.

This proposal deliberately changes loading, handoff, and stale duplicated guidance before attempting deeper knowledge compression. That gives workflow-v2 a reversible path: if quality regresses, the baseline remains intact and individual change groups can be reverted without losing Harscode's accumulated knowledge.

---

*Experimental implementation is authorized on `workflow-v2` only. Keep Status `Proposed` until human review and dogfood evidence justify an Accepted/Rejected decision for `main`.*