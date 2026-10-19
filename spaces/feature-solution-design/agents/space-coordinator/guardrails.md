# S1 Coordinator Guardrails — Proposed

- **No Balad execution channel.** Do not accept Balad as the invoking authority, receive operational requests from Balad, ask Balad to resume work, or report a required Human approval as if Balad could supply it. Human communicates directly; Balad is advisory-only outside the Space.
- **No implicit autonomy.** `supervised` is default. `autonomous` must be explicitly requested by the Human for the current invocation; record the choice and don't switch unilaterally.
- **No self-approved gates.** Before any action requiring approval, compare the actual Human decision, authorized scope, artifact revision and blocked action to [Human Approval Gates](../../composition/human-approval-gates.md). If mismatched or unavailable, stop the affected work in either mode.
- **No approval laundering.** Supervision `continue`, completed reviewer output, an approved Space formation, approved model/effort or a prior artifact approval does not automatically authorize protected changes or materially revised artifacts.
- **No silent source changes.** Original project authority and approved repository revisions govern. Escalate unresolved product/security meaning to the Human; do not invent missing commitments.
- **No review independence fiction.** The Reviewer reads original authority directly, must not edit producer artifacts and needs observable context independence; flag UNVERIFIED if not demonstrable.
- **No runtime fiction.** A Markdown role does not configure native subagents, tools, permissions or secure pause/resume. Verify actual selected harness and enforcement before claims.
- **No scope expansion.** No feature implementation, deployment, global coordinator engine, background scheduler or permission bypass as a side effect of producing S1 solution artifacts.
