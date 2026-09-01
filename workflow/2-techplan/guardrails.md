# Guardrails

Hard stops. If any of these conditions are hit, the agent STOPS and asks
a human — it does not assume and proceed.

## 1. Don't Edit This Guidance Directly

`template.md`, `rules.md`, `guardrails.md`, `guidelines.md`, and
`diagram-guidelines.md` must not be edited directly by the agent. If a
gap is found, write a new proposal in `proposals/` (format in
`proposals/_proposal-template-techplan-tier.md`, Protection Tier:
`techplan-protected`). See `README.md` § Fundamental Rules for when a
proposal is warranted.

## 2. Don't Modify or Delete Raw Docs in the Task's Exploration Output

Files in `{TASK_PATH}/1-exploration/logs/` (exploration doc, risk doc,
plan doc, whatever they're named) are historical input, read-only. If
there's duplication/conflict between files, resolve it in the resulting
techplan.md (see rules.md § Dedup & Reconciliation), not by editing the
source raw docs.

## 3. Don't Overwrite an Approved/Implemented techplan.md

If `techplan.md` in `{TASK_PATH}/2-techplan/` is already Approved or
Implemented,
and a new synthesis produces changes in section 1-7 (the contract part)
— STOP. Explicitly flag to the reviewer that the contract has changed,
don't overwrite silently. Changes in section 8-13 (derived) may be
updated without special flagging since that content is expected to be
volatile. The Summary is regenerated whenever section 1, 2, 5, or
7 changes — treat that regeneration as part of the same flagged change,
not a separate silent edit.

## 4. Read the Target Convention First, Don't Assume

Before filling in section 8 (Interface Contract), read the AGENTS.md /
README / convention file that exists in the target repo (not in this
guidance folder). Minimal coverage, naming convention, error handling
pattern — all of that is specific per project/service, and this
guidance folder is deliberately generic so it stays portable across
projects.

## 5. Don't Invent Technical Facts

Line numbers, function signatures, file names — all of these must come
from the raw docs OR from a direct cross-check against the codebase. If
unsure, write `TBD — verify` explicitly in the techplan, don't write it
as if it were certain.

## 6. Stop on Breaking Changes or Data Risk Not Already Made Explicit

If, during synthesis, the agent finds a potential breaking change, a
risky data migration, or an impact on existing clients that is NOT
mentioned in the raw docs — stop and ask. Don't quietly write it into
Edge Cases as "low risk" without human validation.

## 7. Full Code Snippets Only for What's Non-Obvious

Section 10 (Implementation Details) references file:function +
signature. Full function bodies only when the logic is genuinely
new/non-obvious. Reason: implementation detail is the part most likely
to change during iteration — full snippets go stale fast and add
maintenance burden to the document without adding value (the code/PR is
already the source of truth for exact detail).

## 8. Summary Must Not Introduce New Decisions

The Summary step (rules.md § 7) is condensation, not synthesis. If,
while writing it, sections 1-13 don't actually contain a clear answer
to "why," "what's in scope," or "what's the risk" — that's a gap in the
full plan, not something to improvise in the Summary. Fix the relevant
section (1, 2, 5, or 7) first, then condense.

## 9. Diagram Must Be Validated — Syntax AND Semantics — Before Finalizing

If the Summary includes a Mermaid diagram, re-check it on two axes
before writing the final file:
- **Syntax**: every edge uses a double-dash arrow (`-->`), never a
  single-dash (`->`) — see `diagram-guidelines.md`.
- **Semantics**: every branch condition shown in the diagram matches
  section 4 / the timeline table exactly. An inverted range, a
  boundary drawn on the wrong side, or a condition that can never be
  true (e.g. `today+14 < expiry < today`) is a correctness bug, not a
  rendering issue — syntax-only validation will not catch it.

Treat both checks with the same seriousness as § 5 (Don't Invent
Technical Facts): an unrendered, broken, or logically-wrong diagram is
a shipped defect, not a style nitpick. If you can't confirm both, either
fix the diagram or simplify it — don't ship it unverified.

## 10. Resolved Open Items Must Be Recorded, Not Deleted

Regardless of the techplan's status (Draft, In Review, Approved,
Implemented), when an Active Open Item is resolved, move it to the
Resolved list with the resolution written out (`rules.md` § 8). Don't
silently delete the line. A future reviewer needs to know what was
asked and what it resolved to — the same reason `retro.md` and
`proposals/` are append-only elsewhere in this workspace.

## 11. Summary Must Stay in Sync With the Full Plan

Before treating any edit to sections 1, 2, 5, 7, or 14 (Open Items) as
done — including a mid-Draft Open Item resolution, not just a full
resynthesis — regenerate the Summary (`rules.md` § 7 self-check). A
stale Summary that still lists a resolved item as needing human input,
or a Top Risk that's since been mitigated, is actively misleading: it
asks a reviewer to act on something that's already settled.

## 12. Don't Silently Drop a Flagged Risk Area

If exploration's Sniffing Checklist § Risk flagged an area as
concurrency/perf/security-sensitive, and that area survives synthesis
in some form, it must appear in section 12's Test Focus Pointer table —
even if the answer is "no longer relevant, see § 5." Silently omitting
it (rather than marking it N/A with a reason) reproduces the same class
of gap as § 11 (Summary drifting out of sync): a reviewer or the
testing phase has no way to tell "deliberately scoped out" from
"forgotten."

If you're unsure whether a Risk-lens finding rises to Test Focus
Pointer relevance or is just an ordinary section 4 edge case — ask,
don't guess. Over-including borderline cases is low-cost (worst case,
the testing phase spends a few extra minutes confirming N/A); silently
under-including one is what lets an untested race condition or
security gap ship.