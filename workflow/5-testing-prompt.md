# Testing Prompt

Manual-invoke prompt for the testing phase. One-shot: the sweep (Step
0) and the four coverage categories run in a single invocation, against
the same story.

## Inputs required before running

- Path to the techplan (`docs/story/<story-code>/techplan.md`) — § 4
  (Rules & Validation) is the source of truth for what must be covered,
  and § 12's Test Focus Pointer (if present) is the source of truth for
  which areas need race/perf/security-class coverage beyond the four
  standard categories below.
- Path to the raw exploration docs (`docs/story/<story-code>/` raw
  material, pre-techplan) — required to cross-check the *why* behind
  any Test Focus Pointer entry (its Sniffing Checklist Risk-lens
  finding). Without this, a Test Focus Pointer row is a label with no
  detail to build a concrete test plan from.
- Path to the latest implementation report (`3-build/report.md`, or the
  most recent report if the story looped back through the
  implementation after code review — e.g. a patch/rebuild report).
  Required for Step 0 — without it the agent has no claims to spot-check
  and will default to a full redo.
- The real interface entry point(s) to exercise (API base URL + routes,
  CLI command, UI flow) — not just "read the code and reason about it."
- Path to the target repo's own build/lint/test commands (README or
  Makefile) — required for Final Verification, don't assume
  `go build`/`npm test`/etc.

## Prompt

```
You are running the testing phase for a story that has already been
through implementation and code review. Follow this process, in order:

Step 0 — Sweep, don't redo:
{file:workflow/5-testing/guidelines.md#process} (item 0 specifically).
Read the implementation report below. For every rule/scenario it claims
is covered by a named test, spot-check it (run the existing test, don't
rewrite it). Then read its "what is not tested, and why" section (or
equivalent) — that is your priority list, not a fresh read of techplan
§ 4 from zero.

Also as part of Step 0: read techplan § 12's Test Focus Pointer table.
For every row still marked relevant, cross-check the raw exploration
docs below for the concrete Sniffing Checklist Risk-lens finding behind
it, then build a Test Execution Plan (scope, tooling, threshold) for
that area — this is a distinct deliverable from the four-category
coverage in Step 1, and covers race/concurrency/perf/security-class
tests that Step 1 does not. If the pointer table is empty or missing
but you notice a genuinely concurrency/perf/security-sensitive area in
the exploration docs or code, flag it back as a possible techplan gap —
don't silently add the test yourself without noting the gap.

Step 1 — Coverage per techplan § 4:
{file:workflow/5-testing/guidelines.md#process} (items 1-3). Test every
rule in the techplan's Rules & Validation section using the real
interface. For rules already spot-checked in Step 0 as genuinely
covered, don't re-derive a new test — note it as confirmed. Spend actual
effort only on: rules with no named test, rules whose named test you
could not confirm still passes, and the four categories below.

Cover all four categories, not just the happy path:
- Happy path
- Negative cases (missing fields, invalid input, dependency failures)
- Edge cases (empty/null/boundary values)
- Backward compatibility (old clients, existing data)

Verify error responses precisely — category, actionable message,
correct propagation through the app's error-handling layer, not just
"an error happened."

Full checklist: {file:workflow/5-testing/checklist.md}
Known recurring bug patterns worth specifically hunting for:
{file:workflow/5-testing/examples.md}

Techplan:
[PASTE TECHPLAN PATH OR CONTENT HERE]

Raw exploration docs:
[PASTE PATH OR CONTENT HERE]

Latest implementation report (build or most recent patch/rebuild):
[PASTE REPORT PATH OR CONTENT HERE]

Real interface entry point(s):
[PASTE API ROUTES / CLI COMMANDS / UI FLOW HERE]

Target repo build/lint/test commands:
[PASTE COMMANDS OR PATH TO README/MAKEFILE HERE]

---

Output format:

## 0. Sweep Summary
- Confirmed (spot-checked, still passing): [rule/scenario → test name]
- Closed from report's own gap list: [gap → what was added/verified]
- Not carried over — required fresh testing: [what, and why the report
  didn't cover it]

## 0a. Test Focus Pointer Execution
[Area (from techplan § 12) | Why sensitive (from exploration) | Test
executed (scope/tooling/threshold) | Result] per row. If the pointer
table was empty/missing and you suspect a genuinely sensitive area was
scoped out silently, state that here as a flagged item, not a finding
buried elsewhere — this is a techplan-drift signal
(`workflow/2-techplan/guardrails.md` § 12), report it back rather than
resolving it unilaterally.

## 1. Test Coverage
[Rule/Scenario | Category (happy/negative/edge/backward-compat) |
Real-interface test performed | Result] per item. Cite § 4 rule IDs
where applicable. If a § 4 scenario can't be exercised through the real
interface, flag it explicitly — don't skip silently.

## 2. Error Verification
[Error case | Expected category | Actual category | Message
actionable? | Propagation correct?] per case, or "No error paths
exercised beyond §1" if genuinely none apply.

## 3. Final Verification
- [ ] Target repo build/lint/test commands: pass/fail (paste output)
- [ ] Migration/schema version collision check: result
- [ ] Backward compatibility: explicitly verified, not assumed
- [ ] Fresh end-to-end techplan read: gaps/contradictions found, or none

## 4. New Bug Patterns
Only include entries that meet the threshold in
{file:workflow/5-testing/guidelines.md#threshold-for-adding-to-examplesmd}
(a category of mistake, not a one-off). Otherwise state "No new pattern
— see workflow/5-testing/examples.md for handling this ticket-specific
bug directly."

## Verdict
One of: Pass / Pass with flagged follow-ups / Fail — send back to
implementation.
If "Fail" or flagged follow-ups, list which findings are blocking vs.
optional, and whether they trace to a genuinely new gap or a
Step-0-confirmed area that regressed.
```

## Notes

- This prompt does not decide which model runs it — see
  `best-practices/model-routing.md` (draft) for tier × stage routing.
  Testing is currently flat/DeepSeek-routed (Flash for Simple/Medium,
  Pro for Complex) — no dual-model requirement at this stage today.
- Step 0 exists specifically so this phase doesn't silently re-verify
  everything from a blank slate (token cost with no new signal) and
  doesn't silently trust an implementation report's claims without
  spot-checking. If Step 0 consistently gets skipped in practice (the
  agent defaults straight to a full redo, or defaults to blind trust),
  log it in `workflow/5-testing/examples.md` — that would mirror the
  exact "prose instruction doesn't survive" pattern already documented
  in `workflow/2-techplan/retro.md`, and would be a candidate for
  converting Step 0 into a harder-gated checklist item instead of prose.
- If a specific pass (coverage, error verification, final check)
  consistently produces weak findings across multiple real runs, note
  the pattern in `workflow/5-testing/examples.md` before restructuring
  this prompt — don't split it into per-step invocations preemptively.