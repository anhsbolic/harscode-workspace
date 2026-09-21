# Techplan Synthesis Prompt

Canonical entrypoint for turning completed Exploration evidence into an execution-grade `techplan.md`.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}` — path to this Harscode workspace. Project-level; used to resolve Techplan and best-practice authorities.
- `{TASK_PATH}` — root working directory for this task. This phase reads `{TASK_PATH}/1-exploration/logs/` and writes `{TASK_PATH}/2-techplan/techplan.md`.
- Completed durable Exploration artifacts in `{TASK_PATH}/1-exploration/logs/`. This phase synthesizes them; it does not silently redo missing Exploration.
- Applicable target-repo authority/specs — the repo instructions, product/spec sources, and live code/contracts needed to verify project-specific facts must be reachable.
- Existing `{TASK_PATH}/2-techplan/techplan.md`, if this is a revision rather than first synthesis. Its lifecycle/status controls whether material changes need an explicit gate.

## Prompt

```text
You are synthesizing the execution-grade Techplan for this task.

Read these Techplan authorities in full:
- {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/template.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/rules.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/guardrails.md

Use {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/guidelines.md only when
you need deeper process clarification; this canonical prompt already owns
the normal execution sequence. Do not default-load examples.md, retro.md,
techplan-example.md, report-template.md, or diagram-guidelines.md. Open them
only when their documented trigger applies.

Output quality: complete, unambiguous, execution-grade, non-redundant.
A fresh Build agent must be able to execute without inventing a material
product/domain, authority/security, architecture/ownership, interface/data,
risk, or verification decision. Do not pad the Techplan with duplicated
source prose, historical narrative, generic framework knowledge, or exact
mechanical detail Build can safely derive from current code.

PROPORTIONAL PLANNING / FAIL-FAST BOUNDARY
Plan enough to make Build safe and directionally correct; use execution to
learn the rest.

Resolve before Build any material ambiguity that Build must not invent,
including product/domain semantics, authority/security, meaningful
architecture/ownership, interface/data contracts, irreversible/destructive
operations, material risk/verification strategy, and human decisions that
block the implementation direction.

Do not pre-solve ordinary details Build can derive safely and cheaply from
current code/convention — local naming, routine mechanical shape, small visual
tuning, or test implementation mechanics — unless they affect a material
contract. This is not permission to defer a material ambiguity to Build.

EXPLORATION COVERAGE
- Fresh/compacted Techplan session: enumerate and read every durable file in
  {TASK_PATH}/1-exploration/logs/ once.
- Same healthy session that completed Exploration: enumerate the durable files,
  reuse evidence still active/unchanged, and open anything not already covered
  or whose exact wording is material. Do not mechanically reread unchanged
  evidence merely for ceremony.
- Correctness must remain reconstructable from durable artifacts. Do not place
  a decision in the Techplan if it exists only in remembered chat context.

SYNTHESIS
- Classify evidence by function per rules.md §1.
- Reconcile overlaps/conflicts per rules.md §2. Genuine contradictions become
  Open Items; do not silently choose the convenient source.
- Evaluate any independently operable migration/script/cron/runbook concern per
  rules.md §3 rather than forcing it into the feature plan.
- Preserve material rejected alternatives in the Decision Log with enough
  rationale that a later agent does not re-litigate settled choices.

PROJECT / PORTABLE AUTHORITY
Read the target repo's applicable AGENTS/README/spec/convention sources for any
project-specific contract or implementation assumption. Paths, symbols,
signatures, schema/API facts, UI/design requirements, and current behavior must
come from durable sources or direct live-code/spec checks.

For stack/security concerns that materially affect this plan, route through
{HARSCODE_WORKSPACE_ROOT}/best-practices/AGENTS.md: search/scan only matching
clue/index entries, then open the matching best-practice files. Do not read the
whole index or best-practices tree by default. If Exploration already cites a
matching best-practice, verify the current authoritative file rather than
copying the Exploration paraphrase as policy.

IMPLEMENTATION DETAIL
In Implementation Details, record code anchors as path + symbol/section + why
relevant + intended change/precedent. Prefer anchors over copied code. Recheck
non-obvious current facts against live code/spec before presenting them as
executable instructions.

VERIFICATION ECONOMICS / OWNERSHIP
For every Rules & Validation rule, preserve verification coverage in the
Testing Checklist. For non-trivial verification, record:
- the evidence/tool/observable check;
- the primary owner of authoritative evidence (Build, Testing, or Human);
- why the check/tool is worth running;
- the meaningful risk if it is skipped.

Build may still run a newly added/changed test enough to establish that the
artifact it authored is executable even when Testing is the primary final
owner. Code Review is normally a reasoning phase; it may run a targeted repro
when needed to substantiate a suspected finding, but do not assign it a broad
final suite merely for ceremony.

BEFORE FINALIZING
- every Rules & Validation rule ID has Testing Checklist verification coverage,
  primary ownership, and enough rationale to judge non-trivial verification
  cost/risk;
- every surviving concurrency/perf/security-sensitive Exploration risk has a
  Test Focus Pointer row with its exact Exploration evidence anchor;
- a scoped-out sensitive risk is N/A with a reason/Decision Log pointer, not
  silently absent;
- unresolved material uncertainty is in Open Items rather than guessed;
- an existing Approved/Implemented Techplan has not been materially changed
  without the guardrail/human gate required for a contract revision.

EARLY ROUTING RECOMMENDATIONS
Before handoff, recommend whether the human should consider the optional
planning mechanisms without invoking them merely to discover they are useless:

Independent Techplan review:
- Skip — normal for a cohesive/comprehensible non-Complex plan the human can
  consciously review/approve.
- Recommend — when independent fidelity checking is likely to catch material
  contract loss or cross-boundary ambiguity. Use the current independent-review
  prompt's Complex signals as the primary clue.
- Required by project policy — only when an external authoritative source says
  review is mandatory.

This recommendation does not replace the independent review prompt's own gate
if that prompt is invoked.

Decomposition:
- Skip — cohesive/linear plan with no meaningful context/review split.
- Consider — when there are genuinely independently useful execution/review/
  context chunks. Length alone is not a reason.

The decomposition prompt remains responsible for the actual post-Approval gate
and exact split if invoked.

There is NO embedded Summary in techplan.md. Do not generate report-techplan.md
during active synthesis/review churn. Generate it only when the current-effective
Techplan is ready to enter the Human approval gate, after any invoked review/
resolution path has converged.

Write the result to {TASK_PATH}/2-techplan/techplan.md using template.md.
Populate the template's provenance fields only with values actually known or
exposed; do not invent model/session/revision metadata or persist account/
credential identifiers. Git history is the default version history.

Treat the written Techplan as a Draft/In-Review checkpoint until the human gate
approves it; do not automatically continue into Build merely because synthesis
completed.

At completion, report:

## Phase handoff
- Completed: Techplan synthesized and self-checked (or state what remains)
- Artifacts: {TASK_PATH}/2-techplan/techplan.md
- Human decision: approve/revise the Techplan and resolve any material Active Open Item that blocks the implementation direction
- Open / deferred: <non-blocking unresolved/deferred items or "none">
- Independent Techplan review: Skip | Recommend | Required by project policy — <reason>
- Decomposition: Skip | Consider — <reason>
- Recommended next step: human Techplan gate; invoke independent review/decomposition only when the recommendation/human judgement warrants it
- Session transition: <plain-language continue/fresh action + reason; Build is fresh-preferred after Approval>
- Context pointers: techplan path + only source anchors needed for unresolved follow-up
```

## Notes

- `techplan.md` remains agent-executable; context optimization must not reduce contract precision.
- Runtime instructions refer to evolving Techplan sections by semantic name rather than remembered ordinal number.
- Examples/retro are calibration/history, not mandatory runtime authority.
- Matching best-practice files are conditional correctness authorities, not cold examples; open them when the task actually triggers them.
- Generate `report-techplan.md` from `report-template.md` when the current-effective Techplan reaches the Human approval gate after applicable review/resolution convergence; run optional decomposition only when its own gate says it adds value.
- Independent review is a correctness tool for plans that justify its cost, not a ritual substitute for conscious human approval.
