# NextJS Builder — Coordination, Internal Handoffs, Human Gates and Runtime

> **Standing:** Formation candidate, NOT FORMATION APPROVED; does not assign native runner/model or independent isolation. [External contract](contracts.md) owns I1–I5/O1–O4 semantics.

## 1. Human-direct Coordinator: entry, start and resume

A Human may say “implement frontend for work X” (for an API-dependent task, `MOCK_DEVELOPMENT` by default), or explicitly “integrate work X against actual backend” (`REAL_API_INTEGRATION`). Coordinator resolves project/repo/ref, effective accepted work/defect, relevant SOP, accepted interfaces, design/asset standards, prior assignment/handoff, actual runtime/tool permission and intended consumers from **durable originals**. Human need not enumerate document paths. Do not derive critical status from conversation memory.

An identifier permits authorized discovery, not blanket code, testing, service activation, commit/push or protected writes. Before production, record bounded work identity, exact selected mode, source/definition revisions, exclusions, producer responsibilities, target code paths/outputs, permissions, consequential gates and consumer acceptance expectations. Do not assume one Product Outcome = one invocation.

For **resume**, match the exact assignment and persisted mode, reopen latest authoritative sources and actual implementation revisions, identify changed compatibility edges/authorization, and continue only within still-valid permission. A new real integration session after mock handoff is a **new assignment or explicitly reauthorized re-scope**, not a mode transition triggered by provider news.

## 2. Internal Agent I/O edges and ownership

| Edge | Producer → consumer | Minimum return/acceptance and hard boundary |
| --- | --- | --- |
| **A** | Coordinator → Engineer/Craft/Reviewer | Bounded, source-pinned, *mode-bound*, SOP-aware assignment; allowed actions and outputs, actual evidence/independence capability. Each recipient confirms own scope and source access. |
| **B** | Craft → Engineer | Purposeful user-facing priorities, ordinary composition/copy/asset recommendations and observed actionable findings with authority, affected surface, consequence, proposed correction and evidence limits. **Not binding Design policy**. |
| **C** | Engineer → Craft | Exact rendered/code revision and relevant states/viewports/content/technical constraints for actual visual assessment; source-only look is **not** rendered review. |
| **D** | Engineer → Independent Reviewer | Effective original inputs, exact implementation/diff, test/inspection results with env and run/not-run status, craft findings, unresolved decisions and mode/provider standing. Reviewer inspects originals independently, not summaries only. |
| **E** | Engineer/Craft/Reviewer → Coordinator | Engineer owns O1/O2 and assigned checks, Craft owns its guidance/findings, Reviewer owns independent findings; Coordinator checks consistency, evidence/versions, remaining gates and assembles O4 without rewriting owners' conclusions. |

**Single implementation owner:** Next.js Engineer is accountable for all production source changes including CSS, copy, icons and implementation integration. Craft may create candidate copy, exploratory assets, mockups/briefs or other explicitly permitted auxiliary content, but not a rival production-code authority. Avoid separate mandatory plan or report per edge; one anchored comment/section can suffice when useful.

**Early bidirectional collaboration:** material new UI engages Craft while material implementation choices remain revisable. Engineer can challenge technical feasibility, accessibility, performance or cost; Craft can challenge misleading or generic expression. No fixed Craft-first sequence, consensus gate or recurring approval meeting. Minor non-visual changes need no artificial Craft session. Material disagreement: compare binding meaning first, then observable user benefit, feasibility, project standards, total cost, reversibility and evidence; ask independent Reviewer for a recommendation when needed. Consequential unresolved Product/Design choices return to Human/owner. Reviewer never self-approves producer-owned output.

**Reviewer selection:** for material UX, security/privacy, cross-boundary or assigned assurance work, provide genuinely independent context and original-source access; otherwise justify proportionate lighter review. If review is required but isolation/capability is unavailable, mark UNVERIFIED/BLOCKED for that claim. Security specialty beyond the four roles is requested through Human only when real risks justify it.

## 3. Per-mode execution and failure behavior

**Mock mode:** Check whether source contracts permit meaningful faithful simulated API behavior. Keep dev/test mocks outside production behavior; mock states cover applicable success, denial, failed/unknown, stale and invalid responses. No requirement to wait for backend. If a material interface rule is unresolved, don't invent a request shape; do permitted independent work and record the exact dependency. Provider readiness received mid-task is information, **not** mode-switch authority.

**Real mode:** Start with exact FE/BE revisions and effective adopted interface; assess provider reachability, auth/test data, safe environment and SOP permissions. Connect actual frontend consumer and verify as authorized. If provider unavailable, wrong, or interface mismatch material: perform **bounded diagnosis only** to distinguish frontend/backend/environment/authority issue; fix frontend-owned bugs inside scope, otherwise **stop the affected real-integration assignment**, preserve evidence and route accountable blocker to Human. No switch to mock to preserve momentum, no unauthorized backend changes, no replacing blocked real tests with mock and claiming PASS. No automatic background watch or resume. Even if other frontend tasks are conceivable, do not silently change scope.

## 4. Human approval gates (consequence-based)

| Gate | Required decision/evidence |
| --- | --- |
| **Formation** | Explicit Human acceptance of exact candidate definition revision; current candidate persistence is NOT approval. |
| **Invocation/mode** | Human-authorized work, selected mode/default recorded, project/ref, permitted actions/paths/tools, output/state owner. |
| **Material external semantics** | Effective owning Product/Design/shared-interface decision; no Engineer/Craft invented rule. |
| **SOP exception** | Exact restricted test/tool/action, project-owning approval, rationale/risks, allowed side effects before execution. |
| **Protected/security/privilege writes** | Human authorization for exact affected operation/path/revision and real tool permission enforcement. |
| **External actions and environment** | Explicit scope for services, test data, paid generation assets, installs, network/provider use, commits, pushes and deployment, when consequential or project policy requires. |
| **Downstream binding acceptance** | Human/project acceptance of exact material output; separate from manual QA, integrated-system and release claims. |

Project SOP that explicitly forbids tests must be respected. Recommending a high-value exception is allowed; actually running forbidden automation is not. Higher-priority security/legal safeguards remain non-negotiable; escalate actual conflicts and hold affected action.

## 5. Runtime binding requirements (external to definition)

Before production, the selected Harness/operator must demonstrate as applicable:

- **Source fidelity:** current originals, code, contracts, asset/Design authority and pinned revisions reachable.
- **Write containment:** effective scoped filesystem/repository permissions or accurately reported unenforced deviation with appropriate Human decision; tools being writable is not sufficient authorization.
- **Mode persistence:** exact mode and assignment identity survive context/session boundaries, without depending on ChatGPT Memory.
- **Specialist access:** Engineer/Craft/Reviewer receive only necessary original source, tools and permissions; collaboration has clear ownership.
- **Independent assessment:** reviewer can access current originals and exact output in meaningfully separate context when required; role labels don't prove independence.
- **Real tooling readiness:** source setup and selected UI/browser/test tools observed, with explicit SOP limitations. Browser or backend runtime availability is not assumed from config.
- **Human gates:** enforceable decisions for protected writes, external operations, SOP exceptions, material scope/mode changes.
- **Executed evidence:** actual command, state/viewport and real-vs-mock provider identity traceable to relevant code revision.
- **Durable handoff:** project-owned recoverable output/working state and a discoverable entrypoint from exact work identity.

Refer to [Harness runtime binding](../../../harness/runtime-binding.md). The Space does not install/certify its own Harness, invent a global run registry, or require scheduler/state engine tooling. No native isolation or security containment is claimed from declarative text.

## 6. Human-facing closure and continuity

Coordinator returns a concise decision-facing outcome: scope and selected mode; exact effective source, project policy and code revision; O1/O2 result; O3 checks performed or deferred/forbidden/manual-owned; material Craft and independent findings; backend/provider/consumer compatibility; specific blockers or residual risks; owning next action and separate Human acceptance/delivery status.

Use the target project's already accepted representation and directory routing. Persist sufficient source/implementation/evidence references for a fresh consumer to reconstruct state; don't demand fixed file-per-output or copy the contracts into handoff. If write/commit was not permitted or source is only an uncommitted working tree, report that truthfully. After corrections, re-review only affected claims and invalidate stale evidence, not unrelated history.

**Stop cleanly:** `COMPLETE`, `PARTIAL`, `BLOCKED` or `FAILED` are scoped claims. In particular, `REAL_API_INTEGRATION` with a material backend blocker must return a durable `BLOCKED` handoff and finish rather than revert to mock or wait for background repair.
