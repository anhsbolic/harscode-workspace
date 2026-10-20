# Station 5 — S1 Formation Candidate and First-Use Test Plan (2026-10-19)

> Status: **FORMED / DEFINITION APPROVED** at immutable Harscode SHA `1f20cf6584dba54dee17d8183c7069d7c99eafe6` by Anhar; see [S1 formation approval](station5-s1-formation-approval-2026-10-19.md). No project invocation, Codex readiness proof, Specialist execution, or C1 engineering approval has occurred. Coordinator/mode/gate guidance: [decision checkpoint](station5-human-direct-coordinator-gates-2026-10-19.md).
> Owner and decision-maker: Anhar.

## Scope

This is the first-use test plan for the [formed S1 definition pinned at its approved commit](https://github.com/anhsbolic/harscode-workspace/tree/1f20cf6584dba54dee17d8183c7069d7c99eafe6/spaces/feature-solution-design), prompted by the [accepted Balad C1 Formation Request trial](station5-balad-formation-request-closeout-2026-10-19.md). Harscode definitions are on research branch `research/harscode-purpose-llm-fit`. Formation approval is recorded separately in the [owning approval checkpoint](station5-s1-formation-approval-2026-10-19.md); the branch HEAD is not a substitute for the approved definition commit.

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

1. **Formation approval (COMPLETE, declarative only):** Anhar approved immutable S1 definition SHA `1f20cf6584dba54dee17d8183c7069d7c99eafe6` in the [recorded decision](station5-s1-formation-approval-2026-10-19.md). No Codex runtime readiness or project invocation follows automatically.
2. **Codex readiness (within the ordinary Coordinator session if suitable):** Confirm actual CLI and Agent/context mechanics, model+effort eligibility, Reviewer isolation, effective write boundaries, **Human-direct Coordinator conversation, supervised checkpoint behavior and gate pause/resume enforcement**. Autonomous remains unproven unless separately tested. Unavailable material capability is NOT READY; a role profile does not dispatch anything.
3. **Human-direct invocation authorization:** Human may start a Coordinator session for discovery/readiness from a short intent-only kickoff; starting the session does **not** authorize production. Coordinator reconstructs current approved sources and proposes C1-specific input SHA, concrete artifact/state locations, allowed writes, output expectations and mode (`supervised` default; `autonomous` only when explicitly chosen), plus conditional material/protected gates. Human explicitly approves the concrete production scope **before** Specialist execution/writes. **Balad cannot request or coordinate execution.** This is separate from formation and may continue in the same Coordinator session.
4. **Real-use evidence:** In a separately authorized Human-direct S1 execution, capture X1 and O1–O5 with original-source trace, Coordinator/Specialist provenance, supervision observations, triggered gate decisions and revision-bound resume, conformance, costs and real failure modes. Review a consumer-style cold-start reading of the resulting bundle and pin artifact refs.
5. **Review and revise:** Compare actual output with matrix; classify deficiencies as reusable contract, Agent knowledge, harness, project binding or authorization defects. Revise only evidenced gaps and review compatibility. **Do not form S2/S3/S4/S5 as prerequisite** to assess S1's first output.

## Remaining decisions before invocation

**Already settled:** formed definition SHA `1f20cf6584dba54dee17d8183c7069d7c99eafe6`. **Still needed:** Human-direct invocation/selected mode, output/artifact location within Kencleng or another legitimate project-owned place; current-effective invocation state owner; Coordinator/Specialist model+effort and context mechanisms; observable Reviewer isolation, Human gate pause/resume behavior, sandbox/write permissions and evidence owner. C1-specific protected/security approvals stay Human-owned. Balad is advisory-only, not a dispatcher. No values are preauthorized by this plan.

The approved definition's `invocation/kickoff-prompt.md` and Coordinator prompt are **informational templates**, not mandatory Human prompt text, Codex launchers or grants of first invocation. A read-only smoke test is optional when explicitly requested or needed to resolve a material readiness risk; do not silently substitute one for the Human's intent to start real S1 work. Readiness checks and the later explicitly authorized execution can share one Coordinator session. Unverified runtime safeguards still block affected production.
