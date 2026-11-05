# A4 — Rancang Zero-Based Target Design v1

> **Standing:** TARGET DESIGN PROPOSAL / HUMAN DESIGN REVIEW PENDING (2026-11-05). Not an amended or formed Rancang definition, not Human exact-content acceptance, not an invoked Space, not runtime proof and not operational `main`.
> **Scope:** Harscode-Workspace, `research/cross-stage-mapping`; project-agnostic reusable research.
> **Decision owner:** Anhar. This document records the approved **direction to redesign** Rancang, separate Engineering Project Standards, rename the target directory, and preserve independent UX/Engineering/Security concern lenses. Those directional approvals do **not** approve this newly authored exact target text or a new formation.
> **Target paths (not created by this document):** `engineering/spaces/rancang/` and `engineering/project-standard/`.

## 0. Source authority and audit method

1. **Binding target semantic reference for research:** [Human-approved Rancang reverse-lifecycle experiment, immutable snapshot](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/rancang-engineering-solution.md), blob `e78812cc2b67ba4b87a7e17eff271649899df0f3`: **13 logical inputs, 10 logical processes, 8 logical outputs, 6 desired outcomes**, plus Hi-Fi exclusion and UX-web-route versus Engineering-API-route boundary. This approved model is an **experimental design target**, not yet current operational policy.
2. **Supporting experimental authority principles:** [Cross-stage candidate reference](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/candidate-reference-model.md). Approval/standing lives at original project-owned sources, not an artifact's existence or a producer label.
3. **Existing subject of comparison, not a constraint:** [Rancang current entry](https://github.com/anhsbolic/harscode-workspace/blob/8ac5c49eb14b1713989be66f75d2382fcfb81c2f/engineering/spaces/feature-solution-design/README.md), [candidate contract](https://github.com/anhsbolic/harscode-workspace/blob/8ac5c49eb14b1713989be66f75d2382fcfb81c2f/engineering/spaces/feature-solution-design/contracts.md), [coordination](https://github.com/anhsbolic/harscode-workspace/blob/8ac5c49eb14b1713989be66f75d2382fcfb81c2f/engineering/spaces/feature-solution-design/coordination.md), six Agent profiles and knowledge references, artifact representations, and exact formation lineage `6dfc4be790c526026529ed7ef397c61567809de4` (2026-10-30).
4. **Project Standards analogy, not copied Design semantics:** [Design Project Standards](../../design/project-standard/definition.md), plus current [Engineering formation discipline](../../engineering/space-formation.md). Specific project rule sources and project-level approvals remain the target project's authority.
5. **Current read-only audit checkpoint:** `8ac5c49eb14b1713989be66f75d2382fcfb81c2f`. No current Rancang rename/rewrite or Engineering Project Standards files are performed by this proposal.

**Method:** Design the bounded capability from the experimental I/P/O/O first; select internal responsibilities for source fidelity, concern independence, production quality and reasonable total cost; then decide what existing machinery earns retention. Matching Agent count, output labels, file layout or historical approval is not an acceptance criterion.

## 1. Capability boundary and primary result

**Rancang** transforms an authorized, bounded Engineering design question and sufficient effective project information into **one coherent, implementation-consumable Engineering Solution**, with material risks, verification specifications and exact-revision Human handoff. It must solve delegated technical questions; it is not merely an input validator, orchestrator, Product/UX designer, project standards owner, code producer or implementation/runtime certifier.

- **Material source authority:** Product owns accepted actor/domain semantics, invariants and consequential acceptance. UX owns interaction flow, IA, navigation/webpage routes, representative Lo-Fi and state interaction requirements. UI owns visual/content expression. Project Engineering Standards owns reusable project technical rules and their change authority. Rancang owns delegated technical architecture, auth/API/data/state/security *mechanism designs* and verification specifications. Actual API/schema adoption, feature implementation, runtime tests and deployment have distinct downstream owners.
- **Execution scope:** One bounded assignment may cover cross-cutting frontend/backend/data/integration solution design as material, without becoming a full-stack implementation Space. Small, local technical decisions may use a simpler authorized path.
- **No mandatory stage sequence:** Product, UX, Engineering Standards, current code and Human decisions are **information sources**, not automatic named-Space dependencies. Conditional accepted equivalents and justified inapplicability are first-class.
- **Project-neutral definition:** No project-specific architecture, web path, technology, role system, screen count, API style, schema package or approval packet is imposed.

## 2. External INPUT — the 13 experiment meanings

Each row is a **logical information requirement**, NOT a required file or upstream invocation. The Coordinator and Requirements/Authority Analyst record exact source/owner/standing, relevant sufficiency, consumer impact and gaps. An approved Product source is required for **consequential binding Product decisions**, while clearly marked hypotheses may support technical exploration only.

| Experimental input | Sufficiency and legitimate source |
| --- | --- |
| **I01 Product Contract** | Effective scoped Product meaning, invariants, actor/Domain Role rights, acceptance and exact acceptance revision; do not recreate Product policy. |
| **I02 UX Flow Diagram** | Accepted relevant flow and branches; for new/material UX, UX O2 is required by default, or an actual accepted equivalent or legitimate evidence-backed exception. |
| **I03 Lo-Fi Wireframes** | For material screen/surface UX, accepted relevant structural UX O6 by default (equivalent/exception permitted). **Consume** it; do not require Rancang to **author** new Lo-Fi. |
| **I04 Information Architecture & Navigation** | Accepted UX IA/navigation and web page/path/page-vs-state meaning where material; UX owns webpage routes. |
| **I05 Interaction & UI State Requirements** | Accepted interaction/validation/loading/denied/failed/unknown/recovery truth traced to Product and UX; reconcile conflicts with owning Design authority. |
| **I06 Existing Codebase & Architecture** | Actual scoped code, architecture, deployment/evolution constraints when the project exists; evidence is not automatic Product/Design authority. |
| **I07 Engineering Standards & Technology Stack** | Discover **effective, sufficiently defined** technical project constraints/conventions and legitimate exceptions. No presumed mandatory documentation catalog. Missing material reusable rules are handled by `engineering/project-standard/` owner. |
| **I08 Security & Privacy Requirements** | Independent security-source discovery of applicable obligations, principals, trust boundaries, data sensitivity and higher-priority protections. Engineering feasibility does not dilute minimum binding safeguards. |
| **I09 Existing API & Database Schema** | Exact effective shared interfaces, API/data contracts, database constraints and migration/compatibility facts if available and relevant; distinguish proposed from canonical. |
| **I10 Integration Requirements** | Actual producer/consumer boundaries, external providers, dependencies, failure/availability contracts and versions as relevant; missing real integration prerequisites are explicit. |
| **I11 Non-Functional Requirements** | Material performance, availability, reliability, operability, scale, observability, cost and migration constraints with source/standing; no blanket numerical targets without project evidence. |
| **I12 Test & Acceptance Scenarios** | Accepted positive/negative/security/recovery/edge acceptance from owning sources; design verification obligations are derived, not claimed executed. |
| **I13 Technical Research / PoC** | Existing evidence or proportionate targeted investigation **only where** unresolved technical feasibility would materially alter the decision; never a ritual PoC. |

**Input gate:** Sufficient effective source information for the *affected binding technical decision* OR a visibly bounded hypothesis for exploration. Missing Product/UX/standards authority blocks only dependent binding decisions; delegated Engineering unknowns require substantive technical work, not automatic escalation. For technical-only/non-screen work, UX O2/O6 may be genuinely inapplicable with reason. **Hi-Fi is not a default input**; relevant visual/content constraints can arrive as explicit approved requirements, with optional source inspection when genuinely helpful.

**Invocation envelope (not a new 14th experimental input):** actual Human-authorized assignment identity, intended consumers, source/project revisions, permitted tools/read/write scope, output/state destination, supervision and consequential gates. A work ID authorizes permitted discovery, not writes.

## 3. PROCESS — 10 experiment activities, iterative

| Process | Primary accountable role and feedback | Required tangible decision/evidence |
| --- | --- | --- |
| **P01 Requirements Analysis** | Requirements/Authority Analyst; Coordinator joins source refs | Trace binding Product/UX/standards obligations, invariants, exclusions, delegated technical freedoms and unresolved owning authority. |
| **P02 Technical Feasibility Analysis** | Engineering Solution Architect; independent UX/Security challenge as applicable | Actual constraints, material alternatives, costs/risks, unresolved feasibility evidence/PoC need. |
| **P03 Solution Architecture Design** | Engineering Solution Architect | Components, boundaries, data flows, integrations, state ownership, mechanism rationale. |
| **P04 Authentication & Authorization Design** | Architect designs; **Independent Security Analyst** establishes binding threat/permission constraints and challenges proposed controls | Identity/session, attribution, resource permissions, grants/revocation, enforcement points and trusted decision makers when material. |
| **P05 API & Data Design** | Architect; Requirements and UX independently verify source constraints | Implementable shared operations and error/result semantics; entity/model/constraints, schema adoption dependencies and transactional guarantees when applicable. |
| **P06 State, Failure & Recovery Design** | Architect, with independent UX/Experience integrity challenge | State transitions, error/unknown, idempotency, concurrency, recovery, consistency, actor-visible truth. |
| **P07 Security & Risk Analysis** | **Independent Security Analyst** separately owns threat assessment and findings; Architect owns mechanism corrections | Source-grounded threats, safeguards, severity, mitigation/acceptance authority, changed-edge review. |
| **P08 Verification Planning** | Architect authors material checkable specs; Requirements/UX/Security contribute obligation checks | Observable success/failure/security/recovery cases, producer and future evidence owner, no fabricated execution. |
| **P09 Solution Review & Refinement** | **Independent Solution Reviewer** checks original sources, whole eight-output coherence and evidence; owning producers correct | Findings, severity, consumer-specific completeness, targeted re-review, unresolved consequential trade-offs. |
| **P10 Engineering Handoff & Human Acceptance** | Coordinator assembles; Human alone accepts exact binding solution revision | Revisioned navigable solution, clear limits, review standing, actual known consumer fit, required Human decisions. |

**Non-linear:** P02–P08 iterate while mechanisms are still revisable. UX and Security challenge **before** irreversible/expensive solution selection, not solely as after-the-fact formal review. Independent findings remain separately owned. The table is neither a ten-stage workflow engine nor a requirement for ten Agents.

## 4. OUTPUT — the eight experiment meanings are the external contract

**Recommendation:** Replace legacy `X1/O1–O5` as the **primary external taxonomy** with `O01–O08` matching the approved experiment. A source/obligation map is a useful internal aid, not an extra obligatory output or sixth external output family.

| Logical output | Accountable substantive owner | Actual consumer acceptance obligation |
| --- | --- | --- |
| **O01 Engineering Solution Blueprint** | Architect | Relevant architecture/components, data flow, interfaces, integration boundaries, rationale and material feasibility/operational constraints sufficiently specified for intended implementers. |
| **O02 Authentication & Authorization Design** | Architect; Security independently challenges | Applicable principal/session identity and trust, authentication/attribution, permission/resource-owner decisions, role/grant/revoke lifecycle, enforcement points, negative/failure behavior. No assumed mechanism. |
| **O03 API Contract** | Architect | Relevant operations/events, identifiers, typed inputs/outputs when required, auth and success/denied/error/unknown semantics, versions/compatibility. A project-required shared machine-readable format yields a **complete proposed typed contract** plus normative guarantees and checkable tests; prose-only is allowed only when actual consumers can implement unambiguously. Canonical adoption remains external. |
| **O04 Data Model & Database Design** | Architect | Applicable entities/relations, ownership, constraints/uniqueness, lifecycle, persistence, transaction/atomicity/concurrency and migration/compatibility implications. No required schema file or DB decisions when not applicable. |
| **O05 State & Error Handling Design** | Architect; UX/Experience independently challenges user-visible integrity | Relevant authoritative state owners/transitions, validation, retries/idempotency, denial, partial/unknown, recovery and observability; align visible claims with accepted Product/UX. |
| **O06 Security Design** | **Architect authors proposed technical controls**; **Security Analyst independently derives risks/requirements and assesses** | Actual trust boundaries, protection/enforcement mechanisms, data/privacy safeguards, threat-linked controls, security assumptions and residual risks. Independent findings are distinct assurance, not a substitute for the design. |
| **O07 Technical Verification Specification** | Architect, with named source-obligation contributors | Checkable material positive/negative/security/reliability/recovery conditions, falsifiers, future test owners/environments as needed and evidence gaps. **Planning is not performed testing.** |
| **O08 Engineering Solution Handoff** | Coordinator, retaining independent authorship of findings | One effective revision-pinned bundle/index linking O01–O07, original sources/standing, independent UX/Security/Solution findings and their disposition, material unresolved edges, per-known-consumer compatibility, actual Human acceptance and next permitted action. |

Outputs can share a single target-project artifact; there are **not eight mandatory files**. A concrete applicable output cannot be omitted merely because the output section is absent. Clearly reasoned `NOT APPLICABLE` is valid only for truly irrelevant portions; `PROPOSED`, `BLOCKED`, `NOT CHECKED` and `UNVERIFIED` do not count as accepted production or runtime success. Each output must identify its accountable **producer**, exact source/output revision and linked material verification coverage.

**Webpage navigation vs API ownership:** UX owns webpage route/navigation/IA meaning; Rancang owns delegated backend API contracts and technical routing/integration mechanisms. Technical infeasibility triggers owning UX reconciliation; Rancang must not silently rewrite accepted webpage paths.

## 5. OUTCOME — six desired qualities with observable design evidence

| Experiment outcome | Evidence needed to make a bounded *design* quality claim | Not implied |
| --- | --- | --- |
| **Feasible** | Fits actual stack/dependencies, meaningful NFR, implementation/operations cost and risk; unresolved technical unknowns surfaced with evidence and next investigation. | PoC passed or deployable runtime. |
| **Secure** | Binding security/privacy floor preserved; O02/O06 specify controls; independent Security findings corrected or explicitly and legitimately dispositioned. | Pen-test, independent runtime containment or blanket certification. |
| **Consistent** | Product invariants trace to API/data/state ownership, transaction boundaries and verifiable checks; cross-output contradiction absent for material cases. | Database transaction actually executed. |
| **Reliable** | Material retry/concurrency/unknown/recovery and availability/operational risks covered by design and O07 scenarios. | Real failure injection or production SLO achievement. |
| **Implementable** | Two independently authorized consumers would not need to invent materially incompatible interface, data, permission, state or security meaning. | Downstream adopted canonical contracts or delivered code. |
| **Verifiable** | Material guarantees have checkable expected/negative cases, owners and actual evidence status; independent reviewers assess completeness. | Tests performed, PASS or Human final acceptance. |

**Completion principle:** A document having eight headings is not enough. A material, unresolved implementer-critical technical choice defeats a `consumer-ready` claim even if listed as a risk. A legitimate `PARTIAL` or `BLOCKED` handoff may still be valuable for Human decision, but cannot be laundered into accepted implementation readiness.

## 6. Agent concern and knowledge architecture — proposed SIX distinct responsibilities

**Zero-based decision:** Six *logical responsibility and knowledge boundaries* are justified by distinct incentives and error modes; this is **not a claim that the earlier six-Agent arrangement is correct**, nor a universal mandate to run six native sessions for every assignment.

| Responsibility | Owns / receives | Must not own; bias protected |
| --- | --- | --- |
| **A. Space Coordinator** | Invocation identity, sufficient inputs, assignments, permission/Human gates, durable state, O08 assembly and revision/consumer joins. | Cannot produce substantive O01–O07, change project authority or rewrite independent findings. Operational throughput must not turn BLOCKED into PASS. |
| **B. Requirements & Authority Analyst** | Independently reads accepted Product/UX/Engineering Standards originals; derives decision-specific obligation/invariant trace, exclusions, and owner gaps. | Cannot infer Product truth from convenient technical mechanisms or select architecture; analysis is internal evidence, not a second canonical requirements source. |
| **C. Engineering Solution Architect** | Single substantive accountable technical producer for O01–O07, delegating scoped technical subproblems only where justified. | Cannot approve Product/UX/project standards or self-certify security/independent review. Feasibility is a design constraint, **not** permission to weaken accepted experience/security guarantees. |
| **D. UX / Experience Integrity Specialist** | Distinct Design-origin knowledge: UX O2/O6, IA/navigation, action/state truth, accessibility and relevant accepted UI constraints; proactively challenges O01/O02/O03/O05 **before** mechanism choice hardens. | No Engineer-owned API/data design, no new Product/UX/UI decision, no project Design Standard promotion, no mandatory UI/Hi-Fi authoring. Independence from Architect's preferred solution is important. |
| **E. Independent Security Analyst** | Independently reads security/privacy originals, threats, trust/permission/data boundaries and material abuse cases; establishes binding security sufficiency and critically assesses O02/O04/O05/O06/O07, independently owned findings and recheck. | Does **not** start from Architect's budget/feasibility framing, author Architect's production design, accept material security risk for Human, or self-approve controls. Engineering feasibility can influence **choice among safe solutions**, never silently redefine the security floor. |
| **F. Independent Solution Reviewer** | Independently checks original sources and all applicable O01–O08, reconciles UX/Security findings, feasibility, outcome/consumer completeness and evidence standing. | Cannot replace independent Security assessment, alter producer-owned decisions or issue Human acceptance. |

### Knowledge isolation / anti-bias guarantees (design requirements)

1. **Separate owning knowledge:** Engineering patterns/techniques in Architect package; accepted UX/interaction/visual constraints and usability expertise in UX/Experience package; threat modeling/security/privacy controls and mandatory protection references in Security package. A common authoritative project-source reference is permitted; **do not make specialist conclusions depend on one Engineering-authored condensed brief**.
2. **Original-source access:** Requirements, UX and Security must read *their own relevant effective originals*, revision and actual limits; the Architect's summary is supplemental. Critical security and source-authority hard requirements remain accessible across role boundaries.
3. **Early independent challenge:** UX can reject unsupported user-visible assumptions; Security can expose unacceptable threats **before** Architect closes a decision. Neither independently changes owning Product/Design/project standards. Architect replies with a technically feasible solution or a precise blocked decision.
4. **Do not disguise context reuse as independence:** When separate independent context/tool access is not demonstrated, label `INDEPENDENCE UNVERIFIED`. A two-role conversation in one shared context may still improve reasoning but cannot claim independent assurance. For material independent Security or Solution review, actual isolation/evidence is required before the corresponding claim.
5. **Proportionality without bias erasure:** Low-risk, narrow tasks may omit irrelevant deep-dive or use fewer physical sessions if no applicable assurance rule is compromised; the **roles/knowledge/decision ownership** cannot be silently merged where material risk or required independent review makes separation necessary. A co-located agent is never authorized to self-approve material security findings.
6. **Disagreement routing:** UX concern raises accepted-meaning mismatch to UX owner; Security concern raises binding protection/risk to authorized security/Human owner; Architect solves delegated Engineering alternatives; Reviewer independently tests trade-offs; Coordinator records exact scope/decision and held consumer edges. No consensus vote or default pro-Engineer tie-break.

**Rationale for keeping a distinct Requirements & Authority Analyst:** prevents architecture feasibility from quietly redefining the binding problem before the solution is designed, and allows trace of consequential decisions from original sources. Its execution overhead should be tested in bounded pilots; do not retain merely because this role existed historically.

## 7. Engineering Project Standards — separate direct concern

**Target:** `engineering/project-standard/`, analogous in *authority pattern* to `design/project-standard/` but **not** a new Space by default. It is Harscode reusable **guidance about a target project's owning technical standards**, never a universal repository of canonical project rules.

**Owns:** finding actual project-wide Engineering standards and authority; judging fit/adequacy for identified work; deciding with the legitimate owner whether to **REUSE / NO CHANGE**, clarify a conflict/stale claim, propose a justified first project-wide rule, revise/supersede an accepted reusable rule, and reconcile affected consumers with exact standing/approval and source proof.

**Possible technical rule topics only if needed:** tech-stack/architecture conventions, API/event/data conventions, persistence/migration compatibility, security/privacy engineering baseline, reliability/operability constraints, coding/testing/SOP practices. A topic list is not mandatory document taxonomy.

**Boundary to Rancang:** Rancang consumes **effective** standards as I07/I08/I11 constraints and may report a material gap or a concrete scoped candidate. **The project standards concern/legitimate target-project owner** governs proposal review, approval and effective project-owned persistence. Rancang does **not** automatically carry standards-write privileges or a built-in governance subworkflow. A feature-specific architecture or API proposal is not automatically a project-wide rule.

**No empty-project deadlock:** I07 is mandatory *sufficient technical decision context*, **not** mandatory prior existence of formal standard documents. For a new project, an actual cross-feature stack/security/API choice may require project-level authority before binding consumers; for delegated local choices, a coherent project-conformant solution is enough. If no material project-wide rule needs changing, return `REUSE / NO CHANGE` with existing source/standing (or justified absence and remaining scoped freedom). Do not invent full standards sets.

**Security integrity:** A project security standard cannot grant exception to higher-priority laws or required protections; security-impacting standards proposals need independently grounded security scrutiny and legitimate risk owner decision. The standards concern should not become a general workflow engine, Orchestrator, automatic registry, or hidden mutation authority.

**Initial owning guidance draft shape, not a binding file count:** `README.md` (entry/standing), `definition.md` (decision/semantic coverage), `AGENTS.md` (source/authority/change safety), `authority-and-handoff.md` (owner, supersession, consumers). Make only useful files, not empty ceremony.

## 8. External handoffs, failures, stopping and approval

- **Project source → Rancang:** current original Product/UX/Design/Engineering/security authority, standing and exact revision, actual code and external consumer needs. Neither project standards concern nor Rancang duplicates owning canonical truth.
- **Rancang → known implementers:** O01–O08 information at usable depth; enough direct access to authoritative originals; proposed vs accepted vs canonical adoption clearly separated. A project may have frontend, backend, data and integration consumers; **no assumption that one Builder Space owns the complete actor outcome**.
- **Known consumers:** check generic declared input compatibility when applicable, then project-bound source/approval/format/security fit. Unknown future consumers = `NOT CHECKED`, not hypothetical certification.
- **`COMPLETE`:** scoped design outputs and required independent findings are coherently authored, corrected/dispositioned, and accurate for supported documentary consumer claims. It is not automatically Human-approved, implementation-ready for every project, or runtime-tested.
- **`PARTIAL`:** usable bounded work exists but a materially required owner output/review is incomplete. **`BLOCKED`:** missing binding owner decision/authorization/security floor/consumer-critical contract defeats affected work. **`FAILED`:** attempted scoped design production did not yield meaningful required result. **`UNVERIFIED`:** qualifier on evidence or independence, not a way to pass an unperformed obligation.
- **Hard stop:** lack of accepted Product meaning, missing material UX baseline/exception, unsafe security mechanism, unauthorized standard change, non-reconstructable handoff, conflicting binding API/data obligations, or absent reviewer independence where mandatory. Hold affected claim/actions, preserve independent progress and name exact owner/next condition.
- **Separate gates:** formation approval for exact reusable definition; Human invocation and actual tool scope; project Standard owner decision; protected/security/privilege exception; exact Engineering Solution Human acceptance; project-owned canonical feature API/schema adoption; implementation; integration/QA; runtime delivery. Do not conflate these.
- **Durability:** exact project/assignment identity, effective source and output revisions, responsible producer/assessor, Human gate/permissions, risks, acceptance standing and recoverable next action survive a fresh session without conversational recall. No universal registry/scheduler/state engine.

## 9. Source-level acceptance scenarios for design review (NOT executed runtime tests)

| Scenario | Required discriminating result |
| --- | --- |
| **S1 New/material screen experience** | Read accepted UX O2/O6 (or legitimate equivalents/exceptions) and O3/O4/O7, conditional web O5; UX Specialist challenges Architect before user-visible solution is called binding. Hi-Fi remains optional. |
| **S2 Technical-only / API-independent design** | No invented UX journeys, wireframes, Hi-Fi or DB schema; still read material Engineering/security constraints and provide correct N/A reasons. |
| **S3 Security-critical identity/resource grant** | Security independently derives trust/resource protection and tests O02/O06 before accepting Architect feasibility argument; unresolved material risk blocks affected design. No security self-review. |
| **S4 Shared API with independent frontend/backend consumers** | Consumer-complete O03 proposed typed contract when required; errors, auth, unknown and versions unambiguous, with normative non-schema guarantees and O07 checks; canonical adoption external. |
| **S5 Atomic multi-record operation with lost response** | Accepted invariant maps to O04 constraints and transaction boundary, O05 idempotency/unknown/recovery, O02 permission, O06 controls and O07 negative/concurrency tests; no fake successful runtime claim. |
| **S6 Missing/conflicting project-wide Engineering standard** | Rancang may choose delegated local mechanism; material cross-feature gap goes to `engineering/project-standard/` owning decision. No automatic standard write, and no deadlock on empty formal standards inventory. |
| **S7 Cross-stage route disagreement** | UX owns webpage route/IA decision, Architect supplies feasibility and API constraints, legitimate owner reconciles exact change; no silent UX overwrite. |
| **S8 Resume / approval lineage** | New session can recover exact assignment, original source revisions, approved-vs-proposed design, separate security/solution findings, owner decisions and next permitted action, with prior formed definition not inherited by rewritten/new-path version. |

Source-level scenario walkthrough is necessary before new formation review. Actual native reviewer independence, tool permission, consumed project proofs, runtime output quality and cold resumption remain **NOT RUN/UNVERIFIED** until directly observed.

## 10. Disposition of existing 23 Rancang files and migration

**New active target:** `engineering/spaces/rancang/`, with newly authored content chosen by real responsibility/consumer needs. Do **not** treat a mechanical directory move as exact formation approval; original approved `6dfc4be` and earlier commits remain immutable historical authority.

| Existing source | Proposed disposition after target review |
| --- | --- |
| `README.md` | **REWRITE** compact Rancang mission, new semantic entrypoints, new formation standing and project-standard boundary. |
| `contracts.md` | **REPLACE** legacy X1/O1–O5 primary external contract with approved experiment I01–I13 / P01–P10 / O01–O08 / 6 qualities, applicability and failure contracts. |
| `coordination.md` | **REDESIGN** durable identity, independent role/source joins, Human gates and short real handoffs, removing old Agent assumptions. |
| `agents/space-coordinator/agent.md` | **REAUTHOR** under new coordination/approval/consumer semantics. |
| `agents/space-coordinator/knowledge.md` | **SELECTIVELY REUSE** bounded durable-state and precise Human question practice. |
| `agents/requirements-analyst/agent.md` | **REAUTHOR** as independent Requirements & Authority Analyst; keep clear source/provenance boundaries. |
| `agents/requirements-analyst/knowledge.md` | **REUSE/REFINE** source fidelity and negative-path trace knowledge; no second canonical Product brief. |
| `agents/solution-architect/agent.md` | **REWRITE** for O01–O07 substantive technical ownership, independent challenge and non-governance boundary. |
| `agents/solution-architect/knowledge.md` | **REUSE SELECTIVELY** feasible mechanism/trade-off guidance; exclude standards-write subworkflow as default. |
| `agents/experience-specialist/agent.md` | **REWRITE** as independently grounded UX/Experience Integrity specialist; required UX consumption is not new UX authoring. |
| `agents/experience-specialist/knowledge.md` | **REUSE/REFINE** UX state truth/accessibility and source checks, with distinct Design-grounded expertise/context. |
| `agents/security-analyst/agent.md` | **REWRITE** early independent security obligations/assessment and precise risk escalation; independent from feasibility framing. |
| `agents/security-analyst/knowledge.md` | **REUSE/REFINE** source-led threats/controls, distinct from solution architecture knowledge. |
| `agents/solution-reviewer/agent.md` | **REWRITE** for 8-output/6-quality coherence and independently checked Security/UX claims. |
| `agents/solution-reviewer/knowledge.md` | **REUSE/REFINE** original-source critique and actionable consumer-fit review; no self-approval. |
| `artifacts/README.md` | **SIMPLIFY** into minimal representation/provenance requirements only when useful. |
| `artifacts/templates.md` | **REPLACE/OPTIONAL** with consumer-driven 8-output prompts, no eight-file mandate. |
| `artifacts/examples.md` | **RETAIN SELECTIVELY** only neutral examples adding consumer value; otherwise retire from active tree, original Git remains. |
| `formation-approval-2026-10-20.md` | **HISTORICAL ONLY**; keep exact immutable Git lineage with a short new-path provenance pointer. |
| `formation-approval-2026-10-21.md` | **HISTORICAL ONLY**, same. |
| `formation-approval-2026-10-25.md` | **HISTORICAL ONLY**, same. |
| `formation-approval-2026-10-27.md` | **HISTORICAL ONLY**, same. |
| `formation-approval-2026-10-30.md` | **HISTORICAL ONLY**; latest old-path formation approval does not form new path/content. |

**No mandatory 23→23 migration.** Do not leave the old path as a competing active definition. Before deletion/move, preserve immutable Git URLs and a discoverable historical lineage index; update **all live current-tree references** including `engineering/README.md`, root `AGENTS.md`, `ARCHITECTURE.md`, `AUTHORING.md`, research tracking and appropriate harness routing. Protect genuinely historical text from silent rewriting. A complete current-tree relative-link/heading/reference audit is required before claiming path migration DONE.

**Engineering Standards split:** delete/retire existing Rancang-owned standards evolution procedure in the *new* active Rancang contract; preserve only source discovery, project-wide gap reporting, and legitimate owner escalation. Do not clone the procedure into a new Space uncritically.

## 11. Review decisions and next bounded execution

**Recommended design direction:** (a) explicit 13→10→8→6 semantic coverage; (b) six *justified* concern/knowledge boundaries with standalone UX/Experience and Security perspectives **before** architecture closure; (c) project-owned Engineering Standards governance moved to `engineering/project-standard/` as direct research concern, not automatically a Space; (d) rename/rewrite into `engineering/spaces/rancang/`; (e) retain exact-revision, independent assurance, durable continuity and truthful claim safeguards; (f) no schema/file/Agent-session-count mandate.

**Material trade-off still to validate:** independent knowledge and findings improve bias resistance but add context/coordination cost. Measure source fidelity, missed material risks, response quality and unnecessary overhead in bounded real tasks rather than claim superiority based on the definition alone. Security independence is non-negotiable **when** material independent security assessment is required; physical topology and selected harness remain separate implementation decisions.

**Review order after Anhar approves this target text:** produce a **scoped rewrite** and new Project Standards concern on the *same research branch*; run source-level eight-scenario contract walkthrough, all-link/authority checks and security/consumer review; get fresh-context independent formation review for the new `engineering/spaces/rancang/` exact definition; then request a distinct **Human exact-revision formation decision**. Do not silently promote to `main` or claim runtime readiness. A5 Builder remains on hold until A4 design review and formation boundaries settle.
