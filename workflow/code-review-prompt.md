# Code Review Prompt

Manual-invoke prompt for the code-review phase. One-shot: all four
passes run in a single invocation, in order, against the same diff.

## Inputs required before running

- The diff or set of changed files to review (scope must be explicit —
  don't let the agent guess "the whole repo since last commit").
- Path to the target repo's own convention file (AGENTS.md / README /
  CONTRIBUTING) — required for Pass 4, must be read, not assumed.

## Prompt

```
You are reviewing a code change. Run four passes, in this exact order,
against the diff below. Do not skip a pass because an earlier pass
found nothing — each pass looks for a different class of problem, and
a clean Safety pass says nothing about Consistency.

Guidance for each pass — read before judging, don't rely on general
knowledge alone:
- Pass 1 (Safety): {file:workflow/code-review/guidelines.md#1-safety-review}
- Pass 2 (Quality): {file:workflow/code-review/guidelines.md#2-quality-review}
- Pass 3 (Stack-Specific Best Practices): {file:workflow/code-review/guidelines.md#3-stack-specific-best-practices-review}
  — match against {file:best-practices/index.md}, open only the files
  that match this diff's technology, apply their checklists.
- Pass 4 (Consistency): {file:workflow/code-review/guidelines.md#4-consistency-check}
  — read [TARGET REPO CONVENTION FILE PATH] first, do not assume a
  pattern from a different project applies here.

Full checklist (all four passes): {file:workflow/code-review/checklist.md}
Known recurring finding patterns worth specifically hunting for:
{file:workflow/code-review/examples.md}

Diff to review:
[PASTE DIFF OR LIST OF CHANGED FILES HERE]

Target repo convention file:
[PASTE PATH OR CONTENT OF AGENTS.md / README / CONTRIBUTING HERE]

---

Output format — one section per pass, in the same order as run:

## 1. Safety
[Finding | Location | Why it matters | Suggested fix] per item, or
"No findings" if genuinely clean — do not pad with non-issues to look
thorough.

## 2. Quality
(same format)

## 3. Stack-Specific Best Practices
(same format — cite which best-practices file each finding came from,
e.g. "kafka/consumer-and-offset-management.md". If no keyword in
best-practices/index.md matched this diff's technology, say so
explicitly instead of skipping the section silently.)

## 4. Consistency
(same format — cite which existing convention was violated, and where
in the target repo that convention is established.)

## Verdict
One of: Approve / Approve with minor comments / Request changes.
If "Request changes," list which findings are blocking vs. optional.
```

## Notes

- This prompt does not decide which model runs it — see
  `best-practices/model-routing.md` (draft) for tier × stage routing,
  including the Complex-tier dual-model Safety pass. Keep that decision
  out of this file to avoid duplicating source of truth.
- If a pass consistently produces weak or skipped findings across
  multiple real reviews, log it in `workflow/code-review/examples.md`
  (agent-appendable) or note the pattern for a future proposal — don't
  restructure this prompt into per-pass invocations preemptively.