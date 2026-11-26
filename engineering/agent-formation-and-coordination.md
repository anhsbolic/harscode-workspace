# Engineering Agent Formation & Coordination V1

> **Standing:** PROPOSED CONSOLIDATED RESEARCH GUIDANCE / EXACT-CONTENT HUMAN REVIEW PENDING.
> **Scope:** Reusable Engineering Space and Agent formation design; not operational policy or an executable runtime specification.
> **Decision basis:** Human-agreed E1–E5 working research decisions and bounded conceptual coherence review, 2026-11-25–26, at `research/cross-stage-mapping@5f4bd298845042c391697850e6ffca917ff2178e`.

## 1. Purpose and authority

Design Engineering capabilities that produce correct, secure, fit-for-purpose, evidence-qualified outcomes at justified total engineering cost. Optimize context consumption, coordination, latency, recovery, and rework without weakening authority, security, or evidence integrity.

This document consolidates the agreed working design direction from [Agent Formation & Context Engineering research notes](https://github.com/anhsbolic/harscode-workspace/blob/5f4bd298845042c391697850e6ffca917ff2178e/engineering/research/agent-formation-and-context-engineering.md). The research notes retain decision provenance, alternatives, and limitations. This consolidation does not supersede existing authority or imply approval of its exact content.

Apply [Engineering Principles V1](principles.md) in full, contextually, together with [Space Formation](space-formation.md), [Production and Verification](production-and-verification.md), [Engineering Project Standards](project-standard/README.md), [Engineering routing](AGENTS.md), and [Harness Runtime Binding](../harness/runtime-binding.md), within their respective standing. Effective project-owned requirements and standards govern concrete work within legitimate authority and applicable higher safeguards.

## 2. Agent formation discipline (E1)

Form Agents around meaningful reusable responsibilities or bounded contributions whose separation materially improves accountability, authority containment, independent judgment, outcome quality, or execution effectiveness. Distinct overall outcome ownership is not required for every Agent; distinct bounded contributions must nevertheless have legitimate accountable owners.

Distinguish Space capability, Agent definition, authorized assignment, and execution session. A separate context does not necessarily require a separate Agent definition. A separate Agent name does not establish independence or effective isolation.

Compare four arrangements according to actual work characteristics:

- Consolidate tightly coupled responsibilities where shared invariants and reasoning continuity matter.
- Extend existing responsibilities through conditional specialization where additional expertise is the primary need.
- Isolate execution contexts for bounded, transferable work where context interference is material and the runtime supports it.
- Separate Agent definitions where reusable differentiated contributions, authority, independent judgment, or material execution effectiveness justify the cost.

Assess accountability, authority, independence, reasoning orientation, competency, context characteristics, semantic coupling, and total engineering cost. Include source acquisition, coordination, context transfer, verification, reconstruction, recovery, rework, and Human burden. Preserve required separation of duties and security boundaries before optimizing cost.

Do not create Agents merely to represent technologies, activities, process concerns, artifact types, or context capacity limitations. No universal Agent count, fixed formation sequence, or weighted scoring model is required. Reassess separation or consolidation on material evidence.

## 3. Information integrity and consumer-sufficient exchange (E2)

Preserve material meaning, authority, provenance, evidence, uncertainty, and decision standing across responsibilities and execution contexts. Distinguish binding requirements, authorized decisions, observations, derived findings, assumptions, hypotheses, recommendations, and unresolved concerns. Formal labels are not required where the distinction remains clear.

Repetition, consensus, summarization, and handoff do not transform unsupported claims into truth or recommendations into authorization. Existing implementation is evidence, not automatically adopted policy. Producer verification is not independent assurance.

Exchange the minimum sufficient trustworthy information for the receiving responsibility. Prefer precise references to accessible owning sources over redundant transcripts and summaries; retain essential context, source revisions, findings, limitations, and unresolved dependencies where necessary. Restrict sensitive information to legitimate need and access.

The producer owns accuracy and consumer sufficiency of the contribution. The consumer owns contextual understanding and proportionate validation of material premises. The Coordinator reconciles material contradictions and gaps in the overall assignment, not every message. Consumers must have legitimate access to original authority and evidence wherever required, including meaningful independent judgment.

Reuse trustworthy evidence only while its subject, scope, revision, conditions, and supported claims remain applicable. Recheck consequential premises and changed dependencies proportionately. Neither blind trust nor mandatory full re-verification is the default.

## 4. Competency and knowledge architecture (E3)

### 4.1 Competency model

Distinguish required competency, available execution capability, and demonstrated competency. Knowledge, guidance, examples, and skills support competency but do not establish it or confer authority.

Define role-appropriate core competencies and conditionally applicable specialization. Acquire only the technical depth necessary for the actual work. Missing knowledge calls for legitimate information acquisition; material capability or authority gaps require authorized support, containment, or qualified results.

### 4.2 Knowledge ownership and placement

Use the narrowest sufficient legitimate ownership scope:

| Scope | Responsibility |
| --- | --- |
| Engineering | Cross-Space semantics, principles, safeguards, and justified shared guidance. |
| Space | Genuinely shared technical knowledge for the bounded capability and its consuming responsibilities. |
| Agent | Responsibility-specific technical knowledge, reasoning support, and application guidance. |

Target-project standards and original technical sources retain their respective authority. Shared applicability alone does not justify promotion to a broader scope. Intentional duplication is acceptable where it preserves essential safeguards or materially improves responsibility-specific use.

The legitimate owning definition is responsible for maintenance of reusable guidance. Consumers assess applicability and surface material stale or conflicting guidance; they do not silently rewrite owning definitions. Verify consequential version-sensitive claims against actual technology and relevant authoritative technical sources.

### 4.3 Scoped discovery and progressive retrieval

Make knowledge discoverable by purpose, applicability, and accessible location. Coordinator communicates known capability needs and assignment constraints; consuming Agents select and acquire relevant knowledge. Discovery must not require reading every available module. Shared knowledge is not universally loaded.

Begin with sufficient direct references, concise descriptive indexes, or repository-native discovery. Increase retrieval sophistication only when actual need justifies the added complexity. Physical storage, index structure, skill packaging, and retrieval mechanisms remain replaceable choices. Search relevance is not authority, correctness, or permission.

Mission, authority, essential guardrails, and discovery guidance must be available. Applicable safeguards and restrictions must be known before affected actions and must not depend on successful optional retrieval.

**Open authority boundary:** Existing P19 and Engineering guidance against centralized knowledge libraries remain unchanged. The shared-scope model and potential centralized storage/indexing require explicit reconciliation before any adoption contrary to that guidance. Centralized physical storage or indexing is not inherently centralized semantic ownership, universal context loading, or global technical policy. Evaluate concrete needs before proposing a revision.

## 5. Durable state, reporting, and execution continuity (E4)

### 5.1 Distributed authority and single-writer state

Preserve accountability and work continuity across context transformation, interruption, and session replacement. Session continuity is a mechanism, not the required outcome.

Use shared logical assignment coordination state with the Coordinator as its exclusive active writer. Participating Agents have legitimate scoped read access and retain accountability for their contributions. Exclusive state mutation does not transfer ownership of project contracts, source code, Human decisions, independent findings, or other engineering outputs to the Coordinator.

Maintain one legitimate owning representation per material fact, decision, or claim where sufficient. Reuse existing owning artifacts, reference original sources, and derive consumer-specific views when needed. Persist additional information only where necessary for correctness, continuity, authority, evidence, or downstream consumption. Avoid redundant snapshots and duplicate ledgers.

Distinguish mutable current coordination state from revision-bound evidence and consequential decision history. A historical result can remain true while no longer supporting a current claim. Shared logical state does not require shared working context, a single physical file, or a centralized service.

### 5.2 Transient contribution reporting

Reports communicate material contribution deltas rather than narrating activities or duplicating durable state. Provide compact pointer-first information sufficient to convey producer, subject and revision, result and standing, material findings, evidence references, limitations, and blockers as applicable. Pointer-only reporting is insufficient when it loses meaning or forces unnecessary reinvestigation.

Formation provides reusable Agent reporting guidance. Coordinator supplies assignment-specific reporting direction, including expected contribution, relevant references, material reporting needs, and authorized destination or transport where necessary. Agents own truthful, sufficient reports. Reconcile material contributions at meaningful dependency or consequence boundaries; batch independent reports where safe.

Reporting is communication semantics, not a mandatory file. Prefer reliable native result delivery, such as authorized subagent execution, without a duplicate physical report when material information remains recoverable until durable reconciliation. Use a compact physical report at an authorized accessible destination for separate-session execution without sufficient native delivery, or where native delivery needs a durable fallback.

Normally consume reports once and use reconciled durable state thereafter. Permit recovery rereads when disposition is uncertain. Avoid duplicate material effects on replay. Clean up reports only after durable reconciliation, safe retention of material meaning, provenance, independent findings and evidence, and satisfaction of retention obligations. Unique material evidence is not disposable because it arrived in a temporary report.

### 5.3 Consistency and recovery

Verify effective single-writer containment, including exclusivity of active Coordinator instances. Serialize coordination state updates without unnecessarily serializing independent engineering work. Single-writer state does not solve concurrent source-code changes, shared environment conflicts, or stale contributions; contain those according to actual dependencies and risk.

Preserve material state at meaningful safe boundaries, including effective objective and authority, allocations, dependencies, decisions and standing, actual changed state, applicable evidence, unresolved findings, and uncertain effects. Preserve material investigation clues when needed. Reuse existing owning artifacts and authorized workspace routing.

On interruption or resume, reconstruct minimum sufficient context from current authority, actual state, and durable evidence. Reconcile uncertain effects before replaying work. Absence of a report is not proof of no effect; a stale PASS cannot establish correctness of a newer changed subject. If safe reconstruction is unavailable, contain affected work and qualify the outcome. A resumed producer is not an independent reviewer merely because its session or model changed.

## 6. Outcome-oriented, bounded coordination (E5)

Coordinator is accountable for coherent, evidence-qualified outcome and external handoff within one authorized Space assignment. Responsibilities include:

1. Assignment integrity: understand effective objective, inputs, authority, constraints, and expected outcome; establish actual readiness and authorized destinations.
2. Capability allocation: allocate applicable responsibilities, identify competency needs, and recommend contextual reasoning effort without assuming a universal model-effort scale.
3. Collaboration direction: communicate expected contributions, constraints, dependencies, and reporting direction.
4. Dependency coordination: enable safe supported parallelism, resolve material gaps within delegated authority, and coordinate consequential escalation and applicable assurance.
5. State reconciliation: maintain shared assignment coordination state under E4 and reconcile contributions without altering their originating authority or independent judgment.
6. Outcome and handoff: reconcile evidence applicability, limitations, remaining obligations, and consumer fit; distinguish scoped outcome standing from Human acceptance or delivery.
7. Continuation and stopping judgment: pursue the authorized objective with sufficient proportionate effort and stop when continuation is no longer legitimate, necessary, productive, or justified.

These are responsibility domains, not mandatory phases. Agent participation and order depend on actual obligations and dependencies. Coordinator directs contributions rather than every action; Specialists retain technical judgment, local decomposition, knowledge acquisition, execution, verification, and reporting. Required independent assurance remains independent.

Coordinator may inspect material evidence proportionately, but must not become a substitute for Specialist competency, Human authority, independent assurance, or Harness mechanisms. Do not impose a universal workflow, process every activity, choose every knowledge item, or require Coordinator mediation of all source access. Keep assignment-level context sufficient and obtain detailed technical context on demand.

Human retains reserved authority and acceptance. Harness/operator realizes actual execution, scoped access, isolation, and persistence. Delegation and separate-session execution require applicable Human authorization and actual runtime capability; no automatic dispatch is implied.

### 6.1 Bounded persistence and justified stopping

Both Coordinator and participating Agents have a duty to pursue their legitimate objectives and a duty to stop when justified. Difficulty, unfamiliarity, initial failure, and inconvenience alone do not establish a blocker.

Distinguish four stopping conditions:

| Condition | Required judgment |
| --- | --- |
| Successful stop | Authorized outcome and necessary evidence are sufficient. Avoid unrelated improvement. |
| Mandatory stop | Binding authority, safety, protected-action boundary, or Human stop instruction requires affected work to cease immediately. |
| Material blocker | Proportionate investigation establishes a necessary prerequisite or legitimate path is unavailable. |
| Unproductive or disproportionate continuation | No credible proportionate path remains, or authorized resource limits are exhausted. Report incomplete obligations truthfully. |

**Stopping guardrails**

- **G1 — Mandatory Reasonable Effort:** Investigate material difficulties with proportionate legitimate effort before declaring recoverable work blocked.
- **G2 — Evidence-Based Blockers:** Ground blockers in actual evidence or identifiable binding restrictions, not preference or unsupported assumptions.
- **G3 — Reasonable Alternatives:** Consider materially different feasible, authorized, proportionate alternatives when initial approaches fail.
- **G4 — Exercise Delegated Autonomy:** Resolve routine technical choices within delegated discretion; do not make Human the default fallback for difficulty.
- **G5 — Contain the Stop:** Stop affected work and dependencies while continuing independent safe, authorized, useful work where feasible.
- **G6 — No Forced Progress:** Do not fabricate evidence, weaken safeguards, change contracts without authority, conceal gaps, or repeat unproductive work for apparent progress.

Mandatory stops take immediate precedence; never require an unsafe or unauthorized attempt as proof of effort. Coordinator scrutinizes Specialist blocker claims proportionately before treating them as Space-level blockers. Redirect effort, reframe, acquire legitimate expertise, adjust allocation, or recover context when justified. No fixed retry count, token threshold, or exhaustive alternative search is mandated.

Preserve achieved outcome, remaining obligations, stop reason, material effort and evidence, current changed or uncertain state, and resume conditions where applicable through E4. Do not require a separate stopping artifact where existing state suffices. An ended or paused invocation is not a completed obligation; a paused invocation need not stay active while waiting for an external prerequisite.

## 7. Concrete formation and validation boundary

Apply this working design direction to actual Space responsibilities without assuming a permanent Agent count, one Agent per process, mandatory report schema, universal state representation, knowledge loader, session manager, scheduler, database, message broker, or global run registry. Select physical mechanisms from actual needs and available runtime capabilities.

Evaluate concrete composition, knowledge placement and discovery, reporting sufficiency, state representation, safe parallelism, assurance, stopping behavior, and runtime requirements during Go Backend Builder Vertical Depth V1. Observe actual outcome quality, evidence validity, context and coordination costs, recovery, Human burden, stale contributions, containment, and effort/stop effectiveness in later separately authorized execution. Conceptual coherence is not proof of effectiveness.

Existing research notes retain unresolved questions and decision provenance. A5 and HI-004 standing remain owned by the [cross-stage research tracker](../experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md). This proposed consolidation is not Go V1 formation-ready review, V2 execution evidence, exact Space formation approval, invocation authorization, target-project implementation permission, or promotion to operational `main`.
