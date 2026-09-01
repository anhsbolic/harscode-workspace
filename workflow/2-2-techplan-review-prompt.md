# Techplan Review Prompt (Draft)

> Status: DRAFT — not yet a protected file. Proposed location: `workflow/techplan-review-prompt.md` (sibling to `techplan-synthesis-prompt.md` and `techplan-decomposition-prompt.md`, not nested inside `techplan/`).
> Trigger for formalizing into a proposal: run this against 2+ real Complex-tier techplans first. If it reliably surfaces gaps the primary pass missed, propose it into the repo. If it mostly finds nothing new, keep it informal.

## Purpose

An independent second-pass review of a synthesized `techplan.md`, run by a **different model** than the one that produced it. This is not re-synthesis and not a rewrite — it is adversarial verification against the source material and the plan's own internal consistency.

This exists because the driving story's three review passes (2026-08-13) showed that a model checking its own output against a self-check list is not equivalent to an independent check. Proposal 0002's diagram-syntax and severity gaps, and proposal 0003's R18 recurrence and Summary/Open-Items desync, were all found specifically because a *different* actor (model or human) looked at the same artifact with fresh eyes.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}` — path to this harscode-workspace's content
  relative to (or as an absolute path from) your project. Set once per
  project; see `workflow/README.md` § Path Variables Convention.
- The synthesized `techplan.md` (the artifact under review).
- The raw exploration docs it was synthesized from
  (`{TASK_PATH}/1-exploration/logs/`) — required for Check 1 (Rule
  fidelity) and Check 6 (Test Focus Pointer completeness), both of
  which trace claims back to source material, not to the reviewer's
  judgment.
- `rules.md`, `guardrails.md`, `diagram-guidelines.md`, `template.md` — the review runs against these, not against the reviewer's own general sense of what a techplan should look like.

## Prompt

```
You are running an independent second-pass review of a synthesized
techplan.md — you did not write this plan, and you are not rewriting
it. Your job is adversarial verification: check every claim against
the actual source material and the plan's own internal consistency,
not against your general sense of what a techplan should contain.

Guidance folder for this phase: {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan
— rules.md, guardrails.md, diagram-guidelines.md referenced below
resolve relative to this. The techplan under review is at
{HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/template.md for structure
reference, but read the actual task's techplan.md (given below) for
content.

Response style: your process can be terse and checklist-driven, but
every reported finding must be complete — location, what's wrong, what
the source says instead. The findings report is the deliverable
({HARSCODE_WORKSPACE_ROOT}/workflow/README.md § Response Style By Phase).

Step -1 — Resolve section numbers first (mandatory, do this before
anything else): read the current template.md and identify the actual
section number for each of the following named sections in THIS
version of the template: Rules & Validation, Testing Checklist (and
its Test Focus Pointer subsection, if present), Open Items, Decision
Log, Edge Cases & Risks, and Summary (if the template still has one —
some versions moved this to a separate report-template.md instead).
Use the section names below, resolved to whatever number they
actually have in the template you're reviewing against — do not
assume fixed numbers from memory or from a previous review. Template
section numbers change as this workspace's guidance evolves via its
own proposal process; a check written against a stale number silently
checks the wrong thing.

Step 0 — Gate question (mandatory, answer explicitly before
proceeding): Is this techplan Complex-tier? (Rules & Validation has
≥15 rules, cross-service, breaking-change trigger, or touches
auth/payment/PII/Kafka-pubsub contract)
- If no — stop here. State why review isn't warranted at this tier
  and exit. Don't review "on autopilot" just because this prompt was
  invoked.
- If yes — proceed, and state which Complex-tier criteria applied.

Run every check below against the actual techplan and actual source
docs — not from memory of what a typical techplan contains. Don't skip
a check because an earlier one found nothing; each looks for a
different class of drift. Cite the resolved section number from Step
-1 whenever you reference a section, not an assumed one.

1. Rule fidelity (Rules & Validation section): count rule IDs there.
   Confirm every rule ID has a corresponding line in the Testing
   Checklist section. Flag any missing. For each rule, re-derive it
   from the raw exploration doc it claims to come from — flag any rule
   that doesn't trace back, or that paraphrases the source in a way
   that changes meaning.

2. Diagram validation (if the plan includes a Mermaid diagram, wherever
   it lives in the template):
   - Syntax: every edge uses `-->`, no single-dash edges.
   - Semantic: for every branch condition, re-check against the source
     table or rule it claims to represent. Confirm the direction of
     any inequality is correct and the range is actually satisfiable
     (watch for impossible-range bugs, e.g. a condition that can never
     be true given the variables involved). Confirm no gaps or
     overlaps between branches.

3. Human-facing summary accuracy (only if the template has a
   human-facing summary/digest section, under whatever name it
   currently uses): confirm any "top risks" or equivalent list only
   includes the severity tier the template defines as inclusion
   criteria — flag anything below that bar. Confirm every item in any
   condensed Open-Items-style list matches the current state of the
   full Open Items section exactly. Confirm the summary introduces no
   decision that isn't traceable to the full plan's body.

4. Open Items lifecycle (Open Items section): every item is in exactly
   one defined lifecycle state — flag ambiguous or dual-state items,
   whatever the state names are called in this version of the
   template. Every resolved item has its resolution recorded, not
   deleted.

5. Guardrail compliance spot-check: no invented facts — spot-check 2-3
   non-obvious technical claims against source docs. No silent
   overwrite of a locked/approved contract, or of draft-status content
   mid-edit without a dependent summary/derived section being
   resynced.

6. Test Focus Pointer completeness (Testing Checklist section's Test
   Focus Pointer subsection, if the template you're reviewing against
   has one — some earlier techplans predate this and won't): read the
   raw exploration docs' risk-lens findings from its sniffing/gap
   analysis. For each finding genuinely about shared state,
   concurrency, an expensive primitive under load, or a
   security-sensitive boundary — confirm it appears in the pointer
   table, either as a relevant row or explicitly marked not-applicable
   with a reason. Flag any such finding that's simply absent with no
   trace — the same class of silent-drop gap as Open Items desync
   (Check 4), just on a different section. Don't flag ordinary
   rule-level edge cases that don't rise to pointer relevance —
   over-flagging noise defeats the check.

Explicitly out of scope: re-litigating architectural decisions already
made in the Decision Log section — this is a compliance/consistency
review, not a second design review. Style or wording nitpicks are not
worth reporting on their own.

Techplan under review:
[PASTE PATH OR CONTENT HERE]

Raw exploration docs it was synthesized from:
[PASTE PATH OR CONTENT HERE]

---

Do NOT output a rewritten techplan. Output a findings report in this
exact format:

## Review findings — <task-code>

**Section numbers resolved (this techplan's version):** [Rules &
Validation = §_, Testing Checklist = §_, Open Items = §_, ...]

**Gate check:** [Complex-tier criteria that applied]

### Blocking (must fix before Approved)
- [finding] — [location in techplan, using the resolved section number] — [what's wrong] — [what source says instead]

### Non-blocking (worth a look, doesn't block approval)
- [finding]

### Clean
- [checklist items that passed, briefly — confirms the check was actually run, not skipped]
```

## What happens with findings

Findings go back to the primary model (or the human lead) for resolution — this prompt does not auto-fix the techplan. If the same category of finding recurs across 2+ stories/tasks, that's the proposal threshold (`guidelines.md`) — write a proposal to fold it into `rules.md`/`guardrails.md`/`diagram-guidelines.md` as a permanent self-check item, the same way proposal 0003 converted recurring prose instructions into checklist items.

## Notes

- This prompt does not decide which model runs it — see `best-practices/model-routing.md` (draft): the mandatory dual-model row for Techplan Complex synthesis is what this review formalizes into a repeatable step.
- Explicitly out of scope is also stated inside the prompt block itself (not just here) so the model sees the boundary at review time, not only in this file's documentation.
- **Why section numbers are resolved at runtime instead of hardcoded:** the previous version of this prompt hardcoded `§4`/`§12`/`§14` etc. directly, copied from `template.md`'s numbering at the time it was written. `template.md` has since evolved (its Open Items section is now `§13`, not `§14`) and this prompt's checks 3-4 kept citing the stale `§14` without anyone noticing — a review prompt silently checking the wrong section number is exactly the kind of drift this prompt exists to catch elsewhere. Naming sections instead of numbering them makes this prompt resilient to future `template.md` renumbering without needing a matching edit here every time.
- This same fragility likely affects `2-1-techplan-synthesis-prompt.md` and `2-3-techplan-decomposition-prompt.md` too, wherever they reference section numbers directly — worth an audit pass, but out of scope for this fix.
