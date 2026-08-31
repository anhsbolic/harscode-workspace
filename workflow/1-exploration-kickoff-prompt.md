# Kickoff Prompt

A starting point for the first message of an exploration session. Fill
in the placeholders, adapt freely — this is a starting shape, not a
rigid form.

```
You are exploring a task in this codebase: {CODEBASE_CONTEXT — a short
one-line label, e.g. "Kencleng — Go backend + Next.js frontend", NOT a
restated description of the repo. Set once per project and reuse
across every task — see {WORKSPACE_ROOT}/workflow/README.md § Path
Variables Convention}. This happens in three stages — do not skip or
merge them.

Working directory for this task: {TASK_PATH} — write all raw output
from every stage below into {TASK_PATH}/1-exploration/logs/ (see root
README.md § Task Working Directory Structure).

Guidance folder for this phase: {WORKSPACE_ROOT}/workflow/1-exploration
— sniffing-checklist.md and guidelines.md referenced below resolve
relative to this.

Response style: Stage 1 stays terse — plan and order only, no detail
yet. Stages 2 and 3 need full, concrete detail per area — this is raw
material a future techplan builds a contract from
({WORKSPACE_ROOT}/workflow/README.md § Response Style By Phase).

**Task:** {paste the task detail directly, or paste the path to a
PRD/TRD/spec document to read instead — either works. If it's a path,
read the file in full before Stage 1, don't summarize from the
filename alone}

**Ticket:** {ticket ID/link, if any}

**Area (if known):** {service/module/component, or "not sure yet —
help me figure out the areas"}

---

STAGE 1 — Plan Announcement (do this first, then STOP and wait for me):

Read this repo's own convention file (AGENTS.md / README / whatever
exists) just enough to identify which areas of the codebase are
relevant to this task. Then tell me:
- Your understanding of the task itself, in your own words — one or
  two sentences, so I can catch a misread before you go further
- Which areas you intend to explore
- In what order, and why that order
- Do NOT read the actual implementation files yet, and do NOT propose
  any solution yet. Wait for my go-ahead before Stage 2.

STAGE 2 — Gap Analysis (after I confirm the plan):

For each area, one at a time, fully before moving to the next:
- Current state: what exists today, concretely — actual function/file
  names, actual behavior, not a vague description
- Requirement: what the task (above) expects here — cite the
  specific line/section it came from if it's a document, don't
  paraphrase from memory of the whole doc
- Gap: the specific difference
- Sniffing: run the five lenses in sniffing-checklist.md (risk, edge
  cases, miscontext, misleading signals, inconsistency) on this area
- Do NOT propose solutions or compare options here. A bare one-line
  observation is fine if something occurs to you, but don't develop it.
- Report after each area so I can redirect if needed, then continue to
  the next area without waiting for explicit approval each time.

STAGE 3 — Solutioning (only after I've reviewed Stage 2's output):

This is where trade-offs, options, and rationale get written. Don't
start this until I explicitly confirm the gap analysis is accurate and
tell you to proceed.

Write whatever form of raw doc best captures what's found at each
stage into {TASK_PATH}/1-exploration/logs/ — the shape should follow
the content, not a preset template.
```

## Notes

- `{TASK_PATH}` — root working directory for this specific task in the
  target repo (e.g. `.local-agents/works/account/06-mfa-totp/`). Every
  later phase's prompt writes into its own numbered subfolder under
  this same root — see root `README.md` § Task Working Directory
  Structure.
- `{WORKSPACE_ROOT}` — path to this harscode-workspace's content relative
  to (or as an absolute path from) your project. Set once per project;
  see `workflow/README.md` § Path Variables Convention.
- `{CODEBASE_CONTEXT}` is a one-line label only (project name + high-
  level stack), not a restated description of the repo — that would
  create a second, independently-drifting source of truth alongside
  the repo's own README/AGENTS.md. Deep repo understanding always
  comes from Stage 1's own instruction to read that file directly;
  this label exists purely so the opening sentence orients the agent
  before that read happens, and so a monorepo with multiple
  services/frontends can disambiguate which one is in play. Set it
  once per project, same tier as `{WORKSPACE_ROOT}`.
- `{TASK}` accepts either pasted content or a document path — one
  field, not a menu of source types to pick from. This is deliberately
  separate from `{CODEBASE_CONTEXT}`: the latter is stable background
  reused across every task on this project, `{TASK}` is the actual
  requirement driving this specific task and changes every time.
- If the task is a file path, the agent reading it is part of Stage 1,
  not assumed to have happened already — Stage 1's own wording ("state
  your understanding of the task in your own words") exists
  specifically to surface a misread here before Stage 2 wastes effort
  on the wrong requirement.
- Stage 1 is a hard stop by default — see
  `guidelines.md` § Why the Split Matters for why this is the cheapest
  point to redirect.
- Stage 2 is not blocking between areas, but the agent should still
  report progress so there's a natural checkpoint if something looks
  off.
- Don't let Stage 3 material creep backward into Stage 2's docs — if a
  Stage 2 doc already reads like a Decision Log, that's a sign the split
  wasn't respected.