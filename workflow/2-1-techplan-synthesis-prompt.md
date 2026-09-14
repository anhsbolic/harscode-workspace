# Techplan Synthesis Prompt

Canonical entrypoint for turning completed Exploration evidence into `techplan.md`.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}` — Harscode workspace path.
- `{TASK_PATH}` — task working directory.
- Completed durable Exploration artifacts in `{TASK_PATH}/1-exploration/logs/`.
- Applicable target-repo authority/specs must be reachable.

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
techplan-example.md, report-template.md, or diagram-guidelines.md.
Open them only when their trigger in the Techplan README/guidelines applies.

Output quality: complete, unambiguous, execution-grade, non-redundant.
A fresh Build agent must be able to execute without inventing a material
product/domain, authority/security, architecture/ownership, interface/data,
risk, or verification decision. Do not pad the Techplan with duplicated
source prose, historical narrative, generic framework knowledge, or exact
mechanical detail Build can safely derive from live code.

Exploration coverage:
- If this is a fresh/compacted session, read every durable file in
  {TASK_PATH}/1-exploration/logs/ once.
- If this is the same healthy session that completed Exploration, enumerate
  the durable files and reuse evidence still active/unchanged. Open anything
  not already covered and reopen exact source sections when wording is
  material. Do not mechanically reread unchanged evidence just for ceremony.
- Correctness must remain reconstructable from durable artifacts; do not
  write a decision that exists only in chat memory.

Classify evidence by function per rules.md §1. Reconcile overlaps/conflicts
per §2. Preserve material rejected alternatives in §5 so later agents do
not re-litigate settled choices.

Read the target repo's applicable AGENTS/README/spec/convention sources for
any project-specific contract or implementation assumption. Technical paths,
symbols, signatures, schema/API facts, and current behavior must come from
those sources or direct live-code/spec checks.

For Implementation Details, record code anchors as path + symbol/section +
why relevant + intended change/precedent. Prefer anchors over copied code.

Before finalizing §12:
- every §4 rule ID has checklist coverage;
- every surviving concurrency/perf/security-sensitive Exploration risk has a
  Test Focus Pointer row with its exact Exploration evidence anchor;
- a scoped-out sensitive risk is N/A with a reason/Decision Log pointer, not
  silently absent.

There is NO embedded Summary in techplan.md. Do not generate the human report
during Draft/In Review; report-techplan.md is generated separately only after
Approval.

Write the result to {TASK_PATH}/2-techplan/techplan.md using template.md.
Carry unresolved material uncertainty into §13 Open Items instead of guessing.

At completion, report:

## Phase handoff
- Completed: Techplan synthesized and self-checked (or state what remains)
- Artifacts: {TASK_PATH}/2-techplan/techplan.md
- Open / blocked: <material unresolved items or none>
- Recommended next step: human Techplan gate; independent review only if its Complex gate applies
- Session recommendation: FRESH for Build after Techplan approval; if review/decomposition remains, CONTINUE only while planning context stays focused
- Context pointers: techplan path + only source anchors needed for unresolved follow-up
```

## Notes

- `techplan.md` remains agent-executable; context optimization must not reduce contract precision.
- Examples/retro are calibration/history, not mandatory runtime authority.
- After human Approval, generate `report-techplan.md` from `report-template.md`; then run optional decomposition only when its own gate says it adds value.
