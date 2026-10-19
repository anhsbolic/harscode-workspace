# Station 5 — S1 Formation Candidate and First-Use Test Plan (2026-10-19)

> Status: **PROPOSED / UNFORMED**. No S1 formation approval, invocation, runtime proof or C1 engineering has occurred. Coordinator/mode/gate working decision: [2026-10-19 checkpoint](station5-human-direct-coordinator-gates-2026-10-19.md).
> Owner and decision-maker: Anhar.

## Scope

This is the first-use test plan for the [Feature Solution Design Space candidate](../../spaces/feature-solution-design/SPACE.md), prompted by the [accepted Balad C1 Formation Request trial](station5-balad-formation-request-closeout-2026-10-19.md). Harscode definitions are on research branch `research/harscode-purpose-llm-fit`. Formation approval must identify the exact immutable definition commit, not just a branch.

Target project to revalidate at preflight: `anhsbolic/kencleng`, `pilot/station5-c1-space-only@63c86e8f7bc9f61380e17dd393c81c0dd184dcd2`. Stage 5 approved behavior and Stage 6 requirements own C1 commitment-specific Product Authority; Stage 7 is a navigation handoff. Pilot entry, root/scoped instructions, relevant project technical and UI/UX authority also apply.

Do not preload historical C1 Solution Contract, old Techplans/API/auth selections, Orchestrator artifacts or previous C1 implementation as design authority. The C1 pilot explicitly excludes inherited old-workflow routing. Current OpenAPI is an empty operational baseline; it is not automatic permission to edit `api/`.

## Falsification tests for live S1 output

| Original C1 obligation | Reject design output when… | Required trace |
| --- | --- | --- |
| B1/B3 attribution and Organization+Owner single success | Owner attribution is missing, or one half can claim success independently | I1 → X1 → O1/O2 invariant → O3 success/failure meaning → O4 negative test → O5 original-source review |
| B2 consequence before effect | Internal Owner consequence is disclosed only after effect or implied external legal proof | I1 → O2 action/effect contract → O3 pre-effect experience → O4 observable test |
| B4 durable reinspection | Only a transient success message preserves meaning | I1 → O2 durable inspection owner → O3 later inspection surface → O4 check |
| B5 provenance | Organization-provided information silently becomes independently verified or curated | I1 → O1 trust distinction → O2/O3 expression → O5 review |
| B6 incomplete processing | Partial/failed/unattributed operation is indistinguishable from success | I1 → O2 result semantics → O3 incomplete states → O4 tests |
| B7 known unresolved representation conflict | Solution ignores a known conflict or invents mandatory conflict detection/adjudication outside C1 | I1 → O2 known-conflict input semantics → O3 non-success behavior → O5 source check |
| Consumer compatibility | Go Backend and Next.js Frontend must invent contradictory shared decisions | O1/O2/O3 with named producers, consumers, revisions, decisions and blocking unknowns |

This matrix tests **solution contract quality**, not C1 implementation. A strong S1 output may still be waiting for Human acceptance and downstream contract checks.

## Formation and first-use gates

1. **Formation approval:** Human reviews candidate external I/O, both diagrams, **Coordinator Agent**, Specialist ownership, **S1 consequence-based Human Approval Gates**, agent-owned knowledge, permissions and failure semantics. Only explicit approval of a pinned commit establishes a **FORMED** definition.
2. **Codex readiness:** Confirm actual CLI and Agent/context mechanics, model+effort eligibility, Reviewer isolation, effective write boundaries, **Human-direct Coordinator conversation, supervised checkpoint behavior and gate pause/resume enforcement**. Autonomous remains unproven unless separately tested. Unavailable material capability is NOT READY; a role profile does not dispatch anything.
3. **Human-direct invocation authorization:** Human directly starts the Coordinator and approves C1-specific input SHA, concrete artifact/state locations, allowed writes, output expectations and mode (`supervised` default; `autonomous` only when explicitly chosen), plus conditional material/protected gates. **Balad cannot request or coordinate execution.** This is separate from formation.
4. **Real-use evidence:** In a separately authorized Human-direct S1 execution, capture X1 and O1–O5 with original-source trace, Coordinator/Specialist provenance, supervision observations, triggered gate decisions and revision-bound resume, conformance, costs and real failure modes. Review a consumer-style cold-start reading of the resulting bundle and pin artifact refs.
5. **Review and revise:** Compare actual output with matrix; classify deficiencies as reusable contract, Agent knowledge, harness, project binding or authorization defects. Revise only evidenced gaps and review compatibility. **Do not form S2/S3/S4/S5 as prerequisite** to assess S1's first output.

## Remaining decisions before invocation

Exact definition SHA to approve; Human-direct invocation/selected mode, output/artifact location within Kencleng or another legitimate project-owned place; current-effective invocation state owner; Coordinator/Specialist model+effort and context mechanisms; observable Reviewer isolation, Human gate pause/resume behavior, sandbox/write permissions and evidence owner. C1-specific protected/security approvals stay Human-owned. Balad is advisory-only, not a dispatcher. No values are preauthorized by this plan.

The candidate's `invocation/kickoff-prompt.md` and Coordinator prompt are informational templates before formation and preflight; do not use them as a launcher today.
