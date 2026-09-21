# Proposal 0036 — Human Techplan Review Report Before Approval

Status: Proposed
Date: 2026-09-21
Protection Tier: techplan-protected
Triggered by: Kencleng `WU-S1-002 / TP-001` (human review friction after synthesis, independent review, and resolution)
Target:
- `workflow/2-techplan/report-template.md` — Purpose, Generation rule, report sections
- `workflow/2-techplan/rules.md` — Human Report lifecycle
- `workflow/2-techplan/template.md` — Report rule
- `workflow/2-1-techplan-synthesis-prompt.md` — report timing/handoff wording

## Friction Found

The current Techplan split correctly optimizes `techplan.md` as an execution-grade contract for agents and keeps the human-facing digest separate.

However, the current report lifecycle is internally awkward for the Human Techplan gate:

- `report-template.md` says the audience is a reviewer/lead/stakeholder who needs to understand or sign off;
- the same file says `report-techplan.md` may be generated only after the Techplan is already Approved;
- `rules.md`, `template.md`, and the synthesis prompt repeat that post-Approval rule.

During Kencleng `TP-001`, the execution-grade Techplan remained intentionally detailed and agent-oriented. The Human Authority wanted to perform conscious approval without reading the full execution contract line by line. The existing human report would have been the natural review surface, but policy prohibited generating it until after the decision it was meant to help inform.

Generating the report during every Draft mutation would also be wasteful and would create avoidable synchronization churn. `TP-001` passed through synthesis, independent review, and a focused resolution pass before becoming ready for Human approval.

This exposes a structural lifecycle gap rather than a one-off formatting preference:

```text
current:
Draft/In Review Techplan
→ Human approval
→ report-techplan generated

needed:
Draft/In Review Techplan
→ review/resolution convergence
→ human-review-ready report generated
→ Human approval/revision
```

The report remains derived and non-authoritative in both models.

## Proposed Change

### 1. Introduce a REVIEW-READY generation point

Do not generate `report-techplan.md` in parallel with active synthesis/review churn.

Generate it when the current-effective Techplan is ready for the Human gate:

- synthesis is complete;
- any invoked independent review has completed;
- blocking review findings have been resolved;
- mandatory re-review, when required, has completed;
- no unresolved material item prevents a meaningful Human approval decision.

This is a lifecycle condition, not a new Techplan status enum requirement. Existing `Draft / In Review / Approved / Implemented` statuses may remain unchanged unless separate evidence later justifies a status-model change.

A simple non-Complex plan that goes directly from synthesis to Human gate may generate the report immediately before that gate.

### 2. Keep regeneration proportional

Do not regenerate the report for every intermediate Draft change.

Regenerate it only when:

- the Techplan returns to a Human approval gate after a material revision; or
- an already Approved Techplan materially changes and the existing report becomes stale.

Mechanical/non-material changes that do not alter the Human decision surface do not require churn unless the report would otherwise become factually inaccurate.

### 3. Preserve authority boundary

Keep these invariants unchanged:

```text
techplan.md
= execution-grade authoritative planning spine

report-techplan.md
= derived human-facing review/sign-off view
```

If the two disagree, the Techplan wins and the report is stale.

The report MUST NOT become a second place to decide product/domain/security/interface semantics.

### 4. Refine report content for pre-approval review

Retain the existing compact sections where useful:

- What & why
- Scope
- Architecture / Plan
- Interface Contract when reviewer-relevant
- Key decisions

Adjust/add the following reviewer concerns.

#### Material risks / trade-offs requiring Human awareness

Replace the rigid `Risk requiring sign-off — High-severity only` rule with a decision-oriented filter:

Include only risks/trade-offs that are material to conscious Human approval or acceptance.

Severity remains evidence, but severity alone is not the inclusion rule. Do not dump Medium/Low risks merely for completeness.

#### Review & resolution history

Add a compact section that states, when applicable:

- whether independent review ran and why;
- material/blocking findings raised;
- how those findings were resolved;
- whether the resolution materially changed scope, architecture/ownership, business/security/interface semantics, or verification strategy;
- whether re-review ran, was not required, or was explicitly waived.

This is routing/confidence information, not a copy of the review artifact.

#### Decision needed before approval

List only current items whose resolution is required for the Human to approve the plan.

If none, say `None.`

#### Deferred / Human-owned follow-up

List current non-blocking Human-owned or externally owned follow-up that remains relevant after approval.

This prevents a non-blocking design/copy/operational follow-up from being misread as an approval blocker.

#### Approval boundary

State plainly what Human approval authorizes and what it does not authorize.

For example:

```text
Approval authorizes Build to execute the reviewed planning contract within scope.
Approval does not assert that runtime implementation, integration, or final verification is complete.
Approval does not authorize explicitly deferred capabilities.
```

Keep this task-specific and derived from the Techplan; do not invent generic permissions that contradict project authority.

### 5. Keep the report intentionally smaller than the Techplan

Do not copy:

- the full Rules & Validation table;
- implementation anchors;
- low-level test mechanics;
- complete rejected-alternative history;
- every risk or edge case.

Reference the Techplan for execution detail.

If condensation exposes a missing material decision, fix/re-review the Techplan before presenting the report for approval.

## Concrete protected-guidance changes

### `report-template.md`

Change Purpose from an Approved-only digest to a human-facing digest of the current Techplan at a Human review/sign-off gate.

Replace the current generation rule:

```text
Generate only after the source Techplan reaches Approved.
```

with semantics equivalent to:

```text
Generate when the current-effective Techplan has converged enough to enter a Human approval gate.
Do not generate during unresolved synthesis/review churn.
After a material revision that returns the Techplan to the Human gate, regenerate in full.
After Approval, the same report remains the derived digest until a material source change makes it stale.
```

Update provenance/status wording so the report identifies the source Techplan status and source revision instead of assuming `Approved`.

Add the reviewer sections described above.

### `rules.md` — Human Report section

Replace the post-Approval-only rule with:

```text
The human report is generated from the current-effective Techplan at the Human approval gate, after applicable planning review/resolution has converged.

It is not generated or maintained in parallel with every Draft mutation.

The report is derived review evidence, never execution authority. If a material Techplan revision changes the Human decision surface, regenerate the report before the next Human approval decision. If an Approved Techplan later changes materially, regenerate it again.
```

### `template.md` — Report rule

Remove wording that says the report is created only after Approved.

Route readers to the Human-gate generation semantics in `rules.md` / `report-template.md`.

Do not add an embedded human summary back into `techplan.md`.

### `2-1-techplan-synthesis-prompt.md`

Replace:

```text
Do not generate the human report during Draft/In Review; report-techplan.md is generated separately only after Approval.
```

with semantics equivalent to:

```text
Do not generate report-techplan.md during active synthesis/review churn.
Generate it only when the current-effective Techplan is ready to enter the Human approval gate, after any invoked review/resolution path has converged.
```

The synthesis phase may therefore recommend/route report generation but should not create it prematurely when independent review or resolution is still pending.

## Rationale

This preserves the original reason for separating Techplan and report:

- agents receive a complete execution-grade planning contract;
- humans receive a comprehensible review surface;
- there is still only one planning authority;
- report maintenance remains proportional.

The proposal fixes an ordering contradiction without making report generation a ritual on every Techplan edit.

It also supports conscious Human approval: the Human can review material scope, decisions, interface/security implications, review findings, risks, unresolved blockers, and the exact approval boundary, while drilling into `techplan.md` only where deeper audit is warranted.

## Validation

Pilot this change first on Kencleng `WU-S1-002 / TP-001`.

Success signals:

- one report is generated only after the current review/resolution cycle has converged;
- the Human can make an informed approve/revise decision primarily from the report;
- material details remain traceable to `techplan.md`;
- no conflicting decision is introduced in the report;
- no unnecessary report regeneration occurs during intermediate planning churn.

Continue observing at least one later Techplan before treating the exact report content balance as fully settled.

---

*After human review: update Status to Accepted / Rejected / Superseded. If Accepted, apply only the approved protected-guidance changes and retain this proposal as changelog evidence.*
