# Benchmarking and Usage Observability (Codex)

## Scope

This file translates Continuous Real-Task Validation observability into Codex session-level practice.

It is **harness observability, not workflow policy**. Harscode phases must remain correct without token telemetry, allowance percentages, or a benchmark file.

Use this guidance when a human/operator wants to compare workflow/context efficiency across real tasks or candidate workflow revisions.

## Measurement unit

Treat **one Codex agent session/thread as the primary measurement unit**.

A phase may share a healthy session with an adjacent phase when Harscode context-management says continuation is fit. Record that honestly instead of fabricating per-phase token numbers the client does not expose.

Example:

```text
session-1
→ Exploration + Techplan synthesis

session-2
→ Build + Build/Patch rounds

session-3
→ Code Review

session-4
→ Testing + Testing re-check
```

When phase-level comparison matters, prefer a fresh session boundary that is already justified by workflow/context policy. Do not create artificial fresh sessions merely to improve benchmark granularity if that changes the workflow being measured.

## Before/after capture

When the current Codex client exposes status/usage information, capture a snapshot **before the first prompt/work of the measured session** and again at session completion.

The exact command/UI changes over time. Use the current client's supported status/usage surface; `/status` or `/usage` may be examples when available, but re-verify current Codex mechanics before relying on a concrete command.

Do not use a usage-limit reset in the middle of a measured session. If a reset is intentionally used between sessions, record the reset boundary so allowance deltas are not misread as session cost.

Avoid running unrelated Codex work against the same allowance pool while using before/after allowance percentages as a benchmark proxy.

## Recommended record

A compact benchmark entry should capture what the harness actually exposes:

```markdown
### <session label>

- Run / task: <id/path>
- Phase(s): <phase(s) executed in this session>
- Session/thread id: <id if useful/safe to persist>
- Model: <exact model>
- Reasoning: <effort if exposed>
- Transition: fresh | continued from <phase/session>
- Start snapshot: <context / allowance / usage state>
- End snapshot: <context / allowance / usage state>
- Token usage:
  - input: <value if exposed>
  - cached input: <value if exposed>
  - output: <value if exposed>
  - reasoning: <value if exposed>
- Human prompts: <count or concise description>
- Rescue prompts: <count>
- Clarification prompts: <count>
- Outcome: <phase verdict/accepted/blocked/etc.>
- Notes: <compaction, reset, unrelated activity, harness anomaly, etc.>
```

Do not persist account email, credentials, secret values, or other authentication identifiers from a status screen.

## Interpret usage carefully

Token count is evidence, not the goal.

Do not add cached input and uncached input as though they have identical economic/performance semantics. Keep the categories separate when the client exposes them.

Allowance percentage is a coarse proxy, not a precise per-session bill. It may be affected by:

- another Codex session/process using the same pool;
- model/reasoning differences;
- product-side accounting changes;
- reset timing;
- cached-input treatment.

Record those confounders rather than manufacturing precision.

## Quality pairings

A context-efficient session is useful only if correctness is preserved. Pair usage with outcome evidence such as:

- phase accepted / requested changes / failed;
- material authority or decision missed;
- later phase had to re-litigate a settled decision;
- rescue prompts required because routing/guidance was insufficient;
- human clarification count;
- Review/Testing defects attributable to missing prior-phase context versus ordinary implementation bugs;
- final outcome quality.

A useful comparison is therefore closer to:

```text
usage/context/turns
+
correctness/outcome/rescue evidence
```

not `lowest tokens wins`.

## Rescue prompt definition

Count a **rescue prompt** when the operator supplies extra workflow/project guidance that the agent should reasonably have discovered from canonical prompt/routing/authority, solely to keep the run succeeding.

Do not count ordinary required human decisions, Stage gates, approval decisions, or a correction to a genuinely new fact as rescue prompts.

If a rescue was caused by deficient guidance/routing, preserve it as validation evidence instead of silently normalizing the extra coaching.

## Benchmark file placement

The benchmark record may live with task-local validation evidence when the project chooses to persist it, but it must not become an input that later workflow agents are required to read.

Example project-local shape:

```text
<TASK_PATH>/benchmarks.md
```

The exact path remains target-project/operator choice.

## Validation comparison posture

Prefer comparing different real tasks **directionally** after each candidate workflow checkpoint rather than replaying a solved task whose solution/defects are already known.

Use exact controlled replay only when the question specifically requires it — for example, proving whether a controversial verification reduction loses a known signal.

Across different tasks, compare trends rather than claiming false token equivalence:

- did correctness remain?
- did rescue/clarification decrease or stay low?
- did handoff become easier to follow?
- did repeated verification decrease when not justified?
- did context/usage remain proportional to task complexity?
- was the final result still acceptable?
