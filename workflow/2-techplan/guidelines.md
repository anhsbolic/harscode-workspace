# Guidelines

Process reference for synthesizing Exploration evidence into `techplan.md`. The canonical prompt (`../2-1-techplan-synthesis-prompt.md`) is the normal runtime entrypoint; this file is the deeper process authority when needed.

## Process

1. **Establish Exploration coverage.**
   - Fresh/compacted session: read every durable file in `{TASK_PATH}/1-exploration/logs/` once.
   - Same healthy Exploration session: enumerate the durable files, reuse content that is still active/unchanged, and open any file/section not already covered or whose exact wording is material. Do not mechanically reread unchanged evidence merely to satisfy ceremony.
2. **Classify evidence by function** using `rules.md` §1, not by filename.
3. **Reconcile overlap/conflict** per `rules.md` §2. Genuine contradictions become Open Items.
4. **Evaluate independent operational sub-components** per `rules.md` §3.
5. **Read target-repo authority where the plan depends on project-specific convention**, especially interfaces, state/ownership, error semantics, migrations, UI/design, or test/build conventions.
6. **Write `techplan.md` from `template.md`.** Preserve material decisions/risks/contracts once; use cross-references rather than repeated prose.
7. **No embedded Summary step.** Once the Techplan reaches Approved, generate `report-techplan.md` separately from `report-template.md`.
8. **Use conditional references only when triggered:**
   - `diagram-guidelines.md` when a diagram is warranted;
   - `examples.md` / `techplan-example.md` when tone/shape/detail is genuinely ambiguous;
   - `retro.md` when investigating a known historical failure or guidance regression, not as a default pre-finalization read.
9. **Populate §12 concurrently with §4.** Every rule has coverage; every specialized Test Focus Pointer row carries its exact Exploration evidence anchor.
10. **Preserve Open Item history.** Resolution moves the item to Resolved; do not erase it.
11. **If a structural guidance gap is found**, follow the Proposal Threshold rather than silently editing protected guidance during task work.

## Writing standard

Techplan content is **complete, unambiguous, execution-grade, non-redundant**.

That means:

- enough detail for a fresh Build agent to execute without inventing a material decision;
- rejected material alternatives remain in the Decision Log so they are not re-litigated;
- code implementation detail uses live anchors/precedents rather than copied bodies where possible;
- rationale is retained when it controls execution or prevents reopening a decision;
- source prose is not repeated just to make the artifact look comprehensive.

See root `AUTHORING.md` for Harscode guidance-writing standards; that file does not change the execution-grade requirement of the generated Techplan artifact.

## Proposal Threshold

Change protected Techplan guidance only when:

- the same friction occurs across 2+ distinct tasks, or
- the gap is genuinely structural (changes a durable way of working/authority boundary).

One-off wording preferences belong in the current artifact, not a new permanent rule. Small historical/calibration notes may go to `retro.md`/`examples.md`; recurring lessons should graduate into stable guidance instead of forcing every future agent to read history.
