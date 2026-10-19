# Station 5 — Human-Direct Space Coordinator and Approval Gates (2026-10-19)

> **Authority:** Anhar's explicit working decisions in the 2026-10-19 design conversation. **Status:** accepted research design direction, applied to experimental candidate guidance; not an approved S1 formation, native Codex configuration, actual invocation, empirical runtime result or promotion to Harscode `main`.
> **Owning changes:** [Space formation contract floor](../../space-formation/contract-and-readiness.md), [S1 definition](../../spaces/feature-solution-design/SPACE.md), [S1 gate map](../../spaces/feature-solution-design/composition/human-approval-gates.md), and [Balad boundary](../../pairing/AGENTS.md).

## Decision and reason

- **Human-direct execution:** Balad is Human-facing advisory for project authority, chain/compatibility assessment, Formation Request drafting and requested output interpretation. Balad **may not invoke, request dispatch from, communicate with, coordinate, resume or control Space Coordinator Agents**. Human directly chooses, authorizes and communicates with a Space Coordinator in its execution context.
- **Coordinator Agent role:** Each prospective Space formation defines a bounded **Space Coordinator Agent** responsibility for internal assignments, handoffs, evidence, gate checks and final Human-facing delivery. Defining the role **does not prove** a distinct configured native Agent/process. Physical model/harness topology remains a tested implementation decision.
- **Two execution modes:** `supervised` is **default**. `autonomous` requires Human-explicit mode selection for a concrete authorized invocation; Coordinator cannot switch to it itself. Modes control routine operational delegation and optional Human-visible progress/continuation checkpoints; **neither** grants additional product/write authority.
- **Consequence-based Human Approval Gates:** define during formation for material decisions/operations, not routinely at every Specialist handoff. Exact trigger, required evidence, subject artifact revision, Human authority, downstream action held and valid resume/invalidation rule must be inspectable. Gates apply **in both modes**; stale/denied/missing approval blocks affected downstream action.
- **Human acceptance separated:** formation approval, invocation authorization, conditional protected/product decisions and final downstream acceptance are distinct. Routine supervised `continue` is **not** binding Product Authority approval.

## Worked distinction

A future **Builder Space** (not formed here) should require Human approval of a reviewed **Techplan's exact version before Build implementation** in supervised *and* autonomous mode. A consequential revision invalidates the affected approval. S1 is solution design only and does **not** inherit that Builder gate; it has conditional Human owner/security decision gates plus final output acceptance.

## Current pilot posture and falsification

For first S1 use in Codex CLI, propose a directly Human-opened Coordinator context using supervised mode and visible milestones (after X1 and after O1/O2/O3) before review, with real artifact paths and independent Reviewer evidence. This is **not an invocation instruction**. Validate actual subagent/session mechanisms, model/effort policy, permissions, enforcement of pause/resume and Human gate revision checks. Autonomous remains a selectable design mode, not a capability already demonstrated.

**S1 remains PROPOSED / UNFORMED.** Current repository research changes are not proof of operability. No Kencleng feature code, runtime config, protected workflow policy or `main` promotion is authorized by this working decision.

## Next legitimate frontier

Review the revised candidate's Coordinator and gate contract for formation approval on an exact immutable SHA. Only after distinct Human formation approval: test Codex/runtime readiness, direct Human invocation scope and credible gate enforcement, then execute the bounded C1 real-use experiment.
