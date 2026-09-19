# AGENTS.md — workflow/

This is the workflow hard-rule/router layer. Do **not** read all of `README.md` by default. Start ordinary phase work from the applicable canonical root `*-prompt.md`; read `README.md` or `context-management.md` when their cross-phase/governance detail is actually needed.

## Hard rules

- `2-techplan/` protected files (`template.md`, `rules.md`, `guardrails.md`, `guidelines.md`, `diagram-guidelines.md`, `report-template.md`): proposal-gated. `examples.md` and `retro.md` remain the documented append-only exceptions.
- `1-exploration/`, `3-build/`, `4-code-review/`, `5-testing/`, `6-pull-request/` are lightweight and have no protected core today.
- Start each phase from its root `*-prompt.md` where one exists. Harness/project wrappers route to it; they do not re-author or fork lifecycle policy by stack.
- When a phase is dispatched as an orchestrated Run, also load `orchestrated-run-overlay.md`. The overlay changes identity/read-write path semantics only; the canonical phase prompt remains phase authority.
- Use `context-management.md` for phase/session transitions: durable artifacts over chat memory, progressive disclosure, compact handoff, and Build ownership of patches.
- Stop polishing when the next phase can proceed without inventing a material decision. If a later phase hits one anyway, stop/report instead of inventing it.
- Domain-level prompts apply only to projects that group work by domain; otherwise skip them without ceremony.

## Routing

- Orchestrated Run path/identity compatibility → `orchestrated-run-overlay.md`
- Exploration → `1-exploration-kickoff-prompt.md`
- Techplan synthesis → `2-1-techplan-synthesis-prompt.md`
- Independent Techplan review → `2-2-techplan-review-prompt.md` only when its gate applies
- Techplan decomposition → `2-3-techplan-decomposition-prompt.md` only when its gate applies
- Build/Patch → `3-build-prompt.md`
- Code Review → `4-code-review-prompt.md`
- Testing → `5-testing-prompt.md`
- Pull Request → `6-pull-request/` (no root prompt today)
