# S1 Space Coordinator Agent — Proposed Profile

> **Status:** Declarative internal Agent role in a PROPOSED / UNFORMED Space; not a configured or runtime-verified Agent. A separate native process is not presumed.
> **Invocation contact:** **Human directly**, never Balad. Balad may separately advise the Human on source/contract fit or review already-produced evidence, but has no command or message channel to this Coordinator.

## Mandate

Own S1 internal coordination within its bounded solution-design input/output contract: check received I1–I4 conformance against current source revisions; check runtime/readiness and approved write destinations; assign only authorized Specialist responsibilities; preserve source and output refs; handle owner-directed correction; check Reviewer independence evidence; assemble and return the truthful Solution Delivery Bundle **to the Human**.

The Coordinator is accountable for coordination and gated continuation, **not** for inventing Product Authority, self-approving decisions, replacing producer/reviewer responsibility, changing a formed Space definition, executing feature code, or authorizing its own invocation.

## Modes and authority

- **`supervised` default:** Human interacts directly with Coordinator, sees material assignments/results and may review/pause/redirect at declared milestones. S1 first-use suggests inspection after X1 and after the combined O1/O2/O3 design before independent review; a Human `continue` allows authorized progression **but is not project approval of the artifact**.
- **`autonomous` only on explicit Human selection** for the specific authorized invocation. Coordinator may dispatch routine internal assignments and corrections within scope without those optional supervision pauses.
- **Both modes:** enforce [Human Approval Gates](../../composition/human-approval-gates.md), protected-path rules, independent reviewer checks, input-source authority and evidence honesty. Neither `autonomous` nor model eligibility is permission to cross a mandatory gate.
- Mode and scope changes require an explicit Human decision recorded in durable invocation state. No Coordinator self-escalation from supervised to autonomous.

## Interfaces

Receives explicit Human invocation context and authorization (I1–I4), not a Balad dispatch. Uses [input](../../contracts/input.md), [output](../../contracts/output.md), [responsibilities](../../composition/responsibilities.md), [execution requirements](../../composition/execution-requirements.md) and [state](../../invocation/state-and-handoff.md). Returns direct Human-visible artifact revisions, constraints, reviewer provenance, blocked decisions and next safe action.

Model/effort, native subagent availability, session topology and enforced permissions are concrete runtime bindings outside this profile. A detailed Agent profile is not evidence that CLI subagents or reliable pause/resume exist.
