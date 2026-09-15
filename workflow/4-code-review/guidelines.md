# Guidelines

Runs after implementation exists, before it is considered done. Four review
passes run in order against the same current diff:

1. Safety
2. Quality
3. Stack-Specific Best Practices
4. Consistency

## Verification posture

Code Review is primarily independent reasoning against the current diff and contract, not a second final Testing phase.

Run a command/reproduction when it is needed to prove or disprove a suspected finding, validate a concrete behavior the diff makes uncertain, or distinguish a real defect from speculation. Keep that execution targeted to the question being reviewed.

Do **not** replay the full target-repo test/build/browser matrix by default merely because Review is independent. Broad final verification remains Testing-owned when the Techplan/target repo assigns it there. If Review runs a broad suite, state the concrete review question/risk that required it.

A failing targeted reproduction is evidence for a finding/patch plan; Review still does not edit production code.

## 1. Safety Review

Review specifically for:

- nil/null dereference where absence is legitimate;
- race/shared-state or lifecycle hazards in concurrent/async code;
- swallowed errors or errors that do not reach the caller that needs them;
- missing cancellation/timeout propagation for external calls;
- resource leaks on success/error/early-return paths.

If Safety reveals a genuinely concurrency/perf/security-sensitive area, check
the current Techplan Test Focus Pointer. If specialized coverage is warranted
but absent, report **Techplan drift** separately from the code-level finding.
Review does not silently retrofit planning history.

## 2. Quality Review

Review for maintainability/readability issues that materially affect the
change, including:

- duplicated logic that deserves a shared abstraction;
- misleading names/signatures;
- missing observability at meaningful decision/failure points;
- dead/leftover code from refactoring;
- unnecessary complexity with a simpler local shape already established in
  the target repo.

Do not invent style findings merely to populate the section.

## 3. Stack-Specific Best Practices Review

This pass requires routed external knowledge, but **not a blanket full-index
read**.

1. Use `best-practices/index.md` as a clue map. Search/scan only trigger rows
   relevant to the technologies/areas touched by the diff. For a security
   concern, also target the matching Security Concern Map row(s).
2. Open only the matching best-practice files.
3. Apply those files' actual checklists/rules to the diff.
4. Cite the matching best-practice source for each finding.

If no trigger/security concern matches, this pass is explicitly clean/no-op;
do not force a nearby best practice merely to have something to report.

Best-practice guidance is portable engineering knowledge, not target-project
convention. Do not substitute a different project's pattern for the routed
Harscode source.

## 4. Consistency Check

Read the target repo's applicable convention/instruction source; do not infer
project conventions from Harscode or another repository.

Check applicable concerns such as:

- error construction/wrapping/category convention;
- logging/observability convention;
- validation placement/shape;
- naming and local architectural precedent;
- project-specific frontend/backend/design/test conventions relevant to this
  diff.

Cite the target-repo source/precedent behind a consistency finding.

## Order matters

Safety comes first because correctness/safety defects dominate local quality.
Stack-specific correctness and project consistency are separate checks: one
asks "is this correct for the technology/concern?"; the other asks "does this
fit this repository's actual conventions?"

Use the current diff as review scope. The Build report is evidence/context, not
a substitute for inspecting the code change itself.
