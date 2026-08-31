# Proposal 0004 — Standalone Report Artifact, Generated Post-Approval

**Status:** Draft (pending owner review/merge) · **Date:** 2026-08-27 · **Triggered by:** GMRT-51542 (single story/task — see caveat below)

---

## Friction found

`techplan.md`'s existing Summary section (proposal 0001) solves quick human orientation at the top of the same file, but two gaps showed up working through GMRT-51542:

1. A reviewer who only needs to sign off (not implement) still has to open the full execution-grade techplan to see even a simplified flow or the API shape — Summary intentionally excludes Architecture/Plan and Interface Contract detail, so there's no compact place a non-implementing stakeholder can see "how it roughly works" or "what the request/response looks like" without wading into code-adjacent sections.
2. When a techplan needs to go to someone outside the immediate dev loop (e.g. attaching to a ticket for a lead who won't open the repo), there was no single exportable file — only the option of forwarding the entire technical document.

Ad hoc fix tried during GMRT-51542: two independently-maintained files (`*-AGENT.md` full detail, `*-REPORT.md` compact). This worked for one story/task but reproduces the exact risk **Proposal 0001 already rejected** ("two independent documents... creates two sources of truth that can drift silently") if the two files are edited in parallel.

## Decision

Add a new artifact type, **Report**, with a hard sequencing rule that avoids the drift problem 0001 already solved for Summary:

- Report is a **separate file**, not a section inside `techplan.md`.
- Report is **only generated once `techplan.md` reaches `Approved` status** — never drafted in parallel with an in-progress techplan.
- Report is **always regenerated in full** from the current approved `techplan.md`, never hand-patched independently. If `techplan.md` is revised after a Report was generated (including the Approved→Implemented loop, or a reopened Draft), the Report must be regenerated before it's considered current.
- Report content = existing Summary content (per `rules.md` §7) **plus two new sections**, both validated during GMRT-51542:
  - **Architecture/Plan (simplified)** — a diagram only if the flow is genuinely non-trivial (same "diagram only for genuine branching/multi-step flow" rule already in `guidelines.md` from proposal 0001); otherwise a short prose flow + a plain-language component/purpose table. No file/line references, no code.
  - **Interface Contract (simplified)** — request/response fields described in plain language via a table, **plus a representative JSON example** for request, success response, and error responses. No internal function names, no line numbers.
- New guardrail: agent must not generate or hand-edit a Report while the source techplan is still Draft/In Review, and must not patch an existing Report in place when the source techplan changes — regenerate instead.

## Rejected alternative

**Two independently authored and maintained files from the start** (what was actually done ad hoc in GMRT-51542) — rejected as the durable pattern. It reproduces Proposal 0001's rejected risk if either file is edited without regenerating the other. Only acceptable as a one-off, explicitly risk-accepted choice for a single story/task — not as standing guidance.

## Caveat — evidence strength

This proposal is based on **one story/task**, not the 2+ stories/tasks (or clearly independent structural gap) that proposals 0001-0003 were grounded in before being accepted. Owner (Anhar) chose to formalize anyway rather than wait for a second occurrence. Recorded here so a future retro pass can revisit this proposal specifically if the pattern turns out not to hold up on the next story/task that needs a Report (e.g., if "generate only post-Approval" proves impractical because reviewers actually want to see architecture *before* approving, which would undercut the whole sequencing premise).

## Targets

- New file `workflow/techplan/report-template.md` (protected, sibling to `template.md`) — see companion draft.
- `guidelines.md` — new step: "After `techplan.md` reaches Approved, and only then, generate `report.md` from `report-template.md`, sourced entirely from the approved techplan. Do not generate earlier. If the techplan changes post-approval, regenerate the Report — do not patch it."
- `guardrails.md` — new guardrail: Report generation/regeneration timing (no pre-Approval generation, no independent hand-editing, full regeneration on source change).
- `rules.md` — no change to §7 (Summary) itself; Report is additive/superset, not a redefinition of Summary.