# Techplan Independent Review Prompt (Draft)

> **Status:** DRAFT — dogfood on 2+ real Complex-tier Techplans before proposing formalization as a stable gate.

Independent adversarial verification of a synthesized Techplan. This review must use an independent reviewer/actor context from the primary synthesis; it must not be the synthesizer merely self-checking its own plan. Exact model/client selection is execution configuration, not phase policy.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}` — path to this Harscode workspace, used to resolve current Techplan authority.
- `{TASK_PATH}` — root working directory for the task under review.
- `{TASK_PATH}/2-techplan/techplan.md` — the actual synthesized Techplan; this prompt reviews it and does not replace it.
- `{TASK_PATH}/1-exploration/logs/` — all durable Exploration evidence for independent fidelity checking. Broad rereading is intentional here when the Complex gate applies.
- Applicable target-repo source/spec/live-code authority — required for technical-fact spot checks; Exploration prose is not a substitute for current source truth.
- `diagram-guidelines.md` is conditional and is opened only when the Techplan actually contains a diagram.

Unlike ordinary cross-phase progressive disclosure, this review intentionally re-grounds broadly on Exploration evidence for **independent fidelity checking**. That cost is justified only when the Complex gate below applies.

## Prompt

```text
You are independently reviewing a synthesized techplan.md. Do not rewrite it.
Verify it against the actual durable source evidence and current Techplan
and target-repo authority, not against your memory or general preference.

Read:
- {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/template.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/rules.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/guardrails.md
- {TASK_PATH}/2-techplan/techplan.md
- every durable Exploration artifact under {TASK_PATH}/1-exploration/logs/
- diagram-guidelines.md only if the Techplan includes a diagram
- target-repo source/spec/live code only where a claim needs independent fact
  verification

Process narration may be terse/checklist-driven; every finding must include
location, defect, source evidence, and materiality.

STEP 0 — COMPLEX GATE
Is independent review warranted? Treat as Complex when the plan has ≥15
Rules & Validation entries, crosses services/contracts, carries a breaking
change, or touches high-stakes auth/payment/PII/event-contract boundaries.

If NO: stop, state why this review is not warranted, and do not review on
autopilot.
If YES: state the criteria and continue.

Resolve current template section names before checking. If the report needs
section numbers for human location, map those names to the current numbers from
template.md at runtime; never encode remembered ordinal numbers in the checks.

CHECKS

1. Rule fidelity
   - Every Rules & Validation rule traces to real requirement/Exploration
     evidence without meaning-changing paraphrase.
   - Every Rules & Validation rule has Testing Checklist verification coverage.
   - Flag invented or silently dropped material rules.

2. Decision fidelity
   - Material chosen/rejected alternatives in the Decision Log match
     Exploration solutioning.
   - Do not re-litigate a correctly recorded choice; flag only missing,
     contradictory, or meaning-changing decision history.

3. Diagram validation (only if present)
   - valid Mermaid syntax;
   - branch/state/control-flow semantics match the relevant rules/contracts;
   - no impossible, gapped, or overlapping conditions.

4. Open Items lifecycle
   - each item is Active or Resolved, never ambiguous/duplicated;
   - resolved items retain the actual resolution/consequence.

5. Technical-fact / guardrail spot-check
   - verify 2–3 non-obvious paths/symbols/signatures/contracts against current
     target-repo source/spec/live code, not only against Exploration wording;
   - no invented technical fact;
   - no silent material overwrite of an already locked contract.

6. Test Focus Pointer completeness
   - every surviving concurrency/perf/security-sensitive Exploration finding
     is `Yes` or explicit `N/A` with reason;
   - every row has the correct exact Exploration evidence anchor;
   - no ordinary rule-level edge case is inflated into specialized testing
     without reason.

Classify findings:

MATERIAL / BLOCKING — Build would otherwise need to invent or cross a material
product/domain, authority/security, architecture/ownership, interface/data,
risk/meaning, or verification decision; or the Techplan contract is unusable.
Tag the concern.

MECHANICAL / NON-BLOCKING — wording/formatting/exact command/local shape or
other unambiguous correction that can be resolved without changing material
meaning.

Do not hunt for polish after the material checks are complete.

Output only:

## Review findings — <task-code>
**Gate:** <Complex criteria>
**Sections resolved:** <current mapping from semantic section names to current template numbers>

### Blocking
- <finding — location — source evidence — material concern>

### Non-blocking
- <finding>

### Clean
- <checks that passed, briefly>

## Phase handoff
- Completed: independent review
- Artifacts: <review findings path if one was written; otherwise "review output in current session">
- Open / blocked: <blocking findings or none>
- Recommended next step: one resolution pass, then human gate
- Session recommendation: CONTINUE only for the planning resolution/human gate while context is focused; FRESH for Build after Approval
- Context pointers: Techplan + exact source anchors for blocking findings only
```

## What happens with findings

Default shape:

```text
synthesis
→ one independent review (Complex only)
→ one resolution pass
→ human gate
```

The resolver declares whether the resolution changed material scope, architecture/ownership, business/security/interface semantics, or verification strategy. If yes, re-review runs unless the human gate waives it. If no, the human may still order re-review.

Non-blocking/mechanical corrections never trigger re-review by themselves. If Build later discovers a material gap, it returns to the Techplan/human gate rather than inventing the decision.

## Notes

- This Draft prompt does not choose named models; model routing is a separate execution concern.
- Independence is mandatory at the reviewer/actor-context level even though exact model/client routing stays outside this phase prompt.
- Use semantic section names in checks. A prior version hardcoded Techplan section numbers, the template later renumbered, and the review silently checked stale locations; keep this failure-mode rationale when compressing the prompt.
- Broad Exploration rereading here is deliberate independent verification, not the default pattern for Build/Testing.
- The reviewer's job is fidelity/correctness, not a second architecture contest after a decision is correctly recorded.
- Re-evaluate the prompt after 2+ real Complex runs before making it a stable mandatory mechanism.
