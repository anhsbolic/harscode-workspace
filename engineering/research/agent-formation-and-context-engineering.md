# Engineering Agent Formation & Context Engineering — Research Notes

> Standing: WORKING RESEARCH NOTES / NON-NORMATIVE (2026-11-25).
> Scope: Cross-Engineering Space design research, initiated during A5 Go Backend Builder Vertical Depth V1.
> Baseline: research/cross-stage-mapping @ `162aec59abc710a4f28e3b2924810ae1192b7c95`.
> Persistence records discussion and research, not exact-content formation approval, operational policy, a runtime design, or authorization to execute.

## 1. Research question and authority

How should reusable Engineering Spaces allocate responsibilities, knowledge and working contexts so AI Agents deliver sufficiently correct, demonstrable outcomes at justified total cost? A multi-Agent AI system is not a human multi-role team: execution contexts are finite, replaceable and potentially biased; adding Agents may help or harm both correctness and efficiency.

Applicable existing authority: [Engineering Principles V1](../principles.md) (Human-content-accepted research, especially but not limited to P02, P03, P04, P07, P12–P20), [Space Formation](../space-formation.md), [Production and Verification](../production-and-verification.md), [Engineering Project Standards](../project-standard/README.md) and [Engineering routing](../AGENTS.md). These remain controlling within their standing. This note does not supersede them, existing formed definitions or the A5 horizontal ownership model. Do not treat its illustrative categories as a mandatory decomposition.

## 2. Objective and trade-offs

Working direction agreed in discussion: authority, security and evidence integrity are non-negotiable; correct, secure, reliable, fit-for-purpose and evidence-qualified outcomes are the objective. Context efficiency, tokens, latency and cost are optimization dimensions, not substitutes for correctness. Pursue sufficient rather than absolute proof; apply rigor proportionally to consequence. Accept justified coordination or reconstruction costs when needed to preserve quality. Do not optimize token counts at the expense of Human burden or downstream defects.

Assess total cost: source acquisition, reasoning, implementation, coordination, context transfer, verification, assurance, recovery, rework and Human intervention. Local savings may increase total cost. No universal optimal Agent count, token budget, effort scale, context threshold or quality/cost exchange rate is established.

## 3. Four complementary design perspectives

- Responsibility: coherent result, accountable subject, authority, integration and independent judgment.
- Competency: necessary expertise, foundational versus conditional knowledge, actual capability gaps.
- Working context: relevance, sufficiency, source authority, freshness, continuity, isolation, reasoning orientation and transferability.
- Execution continuity: preservation and reconstruction of material state when contexts change or sessions end.

These are analytical lenses, not subsystems. Space boundary (reusable coherent capability), Agent definition boundary (responsibility/competency/authority), assignment boundary (authorized objective) and session boundary (execution context lifetime) need not coincide. Separate execution contexts do not necessarily require additional permanent Agent definitions; separate Agent names do not prove independence. How instances, isolation, context loading and continuation are realized is a runtime concern. Formation must still declare required capabilities and safeguards; an unavailable runtime primitive cannot be assumed.

## 4. Technical characteristics and failure modes

| Concern | Potential benefit of separation | Countervailing risk / safeguard |
| --- | --- | --- |
| Context capacity and effective use | Smaller relevant working set | Lost material constraints; capacity is not effective attention |
| Context pollution | Isolate verbose exploration, logs, failed attempts | Preserve source pointers, unresolved clues and limitations |
| Concern switching | Focus reasoning on a bounded purpose | Excessive switching and duplicated reconstruction |
| Anchoring and confirmation bias | Fresh contract-grounded test design or critique | Shared summaries/models can propagate bias; independence requires real evidence |
| Hallucination | Independent checks of material claims | More Agents can amplify unsupported claims; ground in actual source, tools and observations |
| Instruction overload | Conditional acquisition of relevant knowledge | Never omit applicable authority or critical safeguards |
| Long execution horizon | Restart or compact to recover useful capacity | Information loss, stale state and repeated side effects |
| Task coupling | Keep related reasoning together | Fragmentation of shared invariants and repeated synchronization |
| Parallel work | Independent contributions may reduce elapsed time | Shared mutable resources, overlapping writes, incompatible decisions |
| Coordination and handoff | Bounded results can be transferred | Lost meaning, repeated reads, reconciliation and resource amplification |

These are candidate causal mechanisms and design considerations, not measured Harscode results. Prefer the minimum sufficient trustworthy working context, not the smallest context. Keep highly coupled reasoning together where justified; isolate expensive context when results can be transferred safely. Distinguish actual source evidence from assumptions and summaries; direct access to effective authority matters.

## 5. Competency and knowledge placement

Working direction: Core + Conditional Competency Model. Agent identity is not a technology catalog. All Engineering Agents need role-appropriate engineering judgment, authority awareness, security and evidence reasoning. Required competency, available capability and demonstrated competency are distinct. A guidance file does not create expertise.

Specialization may extend an existing consuming responsibility without a separate permanent Agent. Use responsibility-local knowledge consistent with P19; selective duplication is acceptable when purposes differ or essential safeguards need explicit presence. Do not create a centralized global engineering knowledge library or exhaustive framework catalog. Physical skills/guidance layout and retrieval mechanism remain open.

Progressive disclosure: keep mission, authority, essential guardrails and discovery guidance available; acquire assignment-relevant contracts, standards and actual stack; load specialized references only when applicable. Specialists can discover additional needs during work; Coordinator can indicate known requirements. Critical applicable restrictions must be known before affected action, not treated as optional knowledge. Missing material competence requires legitimate assistance, containment or qualified results.

Illustrative transaction knowledge consumption: producer needs correct transaction construction; verifier needs observable atomicity/rollback evidence; independent reviewer needs counterexamples and invalid isolation assumptions; Coordinator needs consequence and assurance literacy. These are different consumption purposes, not four mandatory Agents.

## 6. Candidate working-context areas

| Area | Characteristic context | Potential design implication |
| --- | --- | --- |
| Coordination and outcome | Broad but concise objective, authority, dependencies, findings and claims | Preserve global view without low-level logs |
| Exploration and investigation | Large, temporary repository/dependency discovery | Isolate when bounded findings and original references suffice |
| Construction and integration | Interdependent code, domain invariants, decisions and corrections | Preserve continuity; avoid splitting tightly coupled technology concerns |
| Verification and evidence | Contract-derived scenarios, observations, test code and failure diagnosis | Consider separate reasoning context to reduce producer confirmation bias |
| Independent assurance | Original authority, exact subject revision, evidence and critical judgment | Require meaningful independence, not merely another persona |

These five areas are hypotheses for analysis, not a five-Agent formation or stages. Exploration/planning separation may duplicate source comprehension. Verification/construction separation may reduce bias but impede tightly coupled debugging; producer verification remains necessary and a test producer cannot independently assure its own tests merely by role label. Actual independent assurance evaluates the coherent delegated outcome, not the activity list.

## 7. Related working decisions from Go Builder discussion

The following were agreed as working design direction in the originating discussion; their wider applicability is a research candidate, not new policy:

- Runtime-agnostic formation: do not prescribe model, Harness, tools or runtime parameter mapping. Specify capabilities, source access, scoped permissions, isolation and evidence requirements as needed.
- Coordinator allocates applicable responsibilities, recommends effort and reconciles overall result. No mandatory Agent-level pre-execution effort negotiation. Use available runtime effort vocabulary if known, otherwise describe reasoning demand. Provider labels (max, xhigh, ultra, etc.) do not imply equivalent capability. Runtime owner realizes configuration; Specialists surface material capability gaps. Initial Coordinator runtime configuration is external.
- Agent participation is conditional; order follows actual dependencies, not formation layout. Parallelism must be safe and supported. Every applicable obligation still has a legitimate accountable subject.
- Internal task decomposition does not fragment overall accountability. A subtask may end with code change, focused test or finding; no universal per-subtask verification/review cycle. Verify where meaningful; reuse evidence only while revision, scope, environment and claim remain applicable. Binding project rules still apply.
- Independent technical assurance focuses on coherent assignment outcome when required by risk or binding rules. Coordinator determines handoff readiness. Exceptional early scrutiny is legitimate for consequential risk or required gates; it does not substitute for overall assessment. Corrections return to implementation ownership; re-verification may focus on affected changes and regression risks. End-to-end is bounded by delegated capability, not automatically whole-product acceptance or E2E Testing Space ownership.
- Consume effective project-owned standards; assess sufficiency against actual assignment. Follow sufficient existing standards. Missing formal documentation is not automatic blockage; use legitimate discretion where safe, without promoting local choices to project policy. Surface material gaps/conflicts to owning authority and contain affected work. Do not add a Standards Agent or mandatory standards preparation phase. Restrictions on testing do not authorize claims that prohibited/unperformed testing succeeded.
- Go Builder working accountability decisions: dedicated Coordinator, single accountable implementation owner, dedicated independent technical assurance subject. The prior three-Agent final composition recommendation was withdrawn pending technical analysis; no final count or additional Agent definitions approved. Core + conditional competencies retained. These decisions do not revise other Spaces or A5 I/P/O/O.

## 8. Session continuity and context transformation

Context capacity, effective context, context quality and productive session lifetime are different. Long contexts may degrade before capacity is exhausted; a small context can also be insufficient. Compaction transforms accumulated context, sometimes by summarization, sometimes via opaque provider-specific representation. It may lose constraints, uncertainty, evidence or progress; repeated compaction may compound drift. Neither compaction nor a fresh session automatically fixes a wrong premise. Fresh sessions also incur reconstruction cost.

| Condition | Candidate judgment |
| --- | --- |
| Healthy context and tightly coupled work | Continue |
| Stable reconstructable state, mostly irrelevant accumulated history | Compact if supported and adequate |
| Verbose tool output | Selectively prune/retrieve relevant evidence where supported |
| Forgotten requirements or stale assumptions | Re-ground against original sources; consider reset |
| Repeated failed reasoning or disproven premise persists | Consider fresh context with corrected framing |
| Independent assessment needed | Separate working context with direct authority/evidence access |
| Unresolved investigation, competing hypotheses, uncertain side effects or unreconstructable state | Preserve/recover material evidence and reconcile actual state before continuation; avoid blind replay |

These are judgment aids, not thresholds, mandated checkpoint cadence or a session-management engine. A forced compaction may occur at an inconvenient point; reconstruct and verify affected state rather than assume retention. Context refresh supports continuity; reasoning reset seeks fresh evaluation without inheriting unsupported conclusions.

Durable engineering state should survive session replacement: authorized objective and restrictions, effective source/revision pointers, actual implementation/worktree state, material decisions and their standing, verification evidence and applicability, unresolved findings, dependencies and uncertain side effects. Preserve investigation clues if material. Ephemeral reads, superseded hypotheses, redundant logs and scratch work need not all survive. Existing repository/contracts/diffs/evidence may already suffice; no mandatory new file per category or transcript persistence. On resume, reconstruct only sufficient context, recheck current state and authoritative sources, and do not repeat side-effecting operations blindly. Harscode correctness must not depend on conversational memory or the opaque compaction item alone.

## 9. External research basis and limitations

Selected references rechecked on 2026-11-25:

- [Liu et al., Lost in the Middle: How Language Models Use Long Contexts (TACL 2024)](https://aclanthology.org/2024.tacl-1.9/): retrieval and multi-document QA experiments show sensitivity to location of relevant information within long inputs. Not a Go engineering benchmark or universal degradation curve.
- [Anthropic, Effective Context Engineering for AI Agents (2025)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents): context curation, just-in-time retrieval and long-horizon strategies including compaction and subagents. Practitioner guidance, not proof of Harscode effectiveness.
- [Anthropic, When to Use Multi-Agent Systems (and When Not To)](https://claude.com/resources/articles/building-multi-agent-systems-when-and-how-to-use-them): context isolation and independent work may justify multiple Agents; duplicated context and coordination are costs. Vendor observations do not establish optimal topology here.
- [Anthropic, Effective Harnesses for Long-Running Agents](https://www.anthropic.com/research/effective-harnesses-for-long-running-agents): experiments use persistent progress artifacts and incremental work across context windows. Example mechanisms, not required Harscode artifacts.
- [OpenAI API, Compaction](https://developers.openai.com/api/docs/guides/compaction): documents an opaque compaction representation for continuation, illustrating that compaction is not universally a human-readable summary. No provider-specific binding follows.

Discussion also considered cumulative information loss and constraint drift under repeated compaction. Treat those as plausible failure modes to test, not quantitative claims; earlier illustrative percentages/curves and unpinned paper references are intentionally not carried forward as evidence. No Harscode-specific comparative runtime experiment has been conducted in this episode.

## 10. Next research and validation

Before concrete Go Builder analysis, resolve only the cross-Engineering semantic questions listed in the bounded discussion tracker below. Concrete design questions remain with the Go Builder case. Then analyze A5 Go Backend Builder P1 Technical Input Assessment, P2 Implementation Planning, P3 Software Implementation, P4 Backend Integration, P5 Technical Verification, P6 Review & Handoff against responsibility, authority, competency, context footprint/lifetime, reasoning orientation, bias, grounding, coupling, independence, transfer/reconstruction cost and verification quality. Keep settled external I/P/O/O intact. Evaluate alternatives before choosing permanent Agent composition; distinguish context isolation from definition separation.

For later separately authorized V2/CRTV, observe actual outcome correctness, meaningful evidence and defects, forgotten constraints or stale assumptions, reconstruction/coordination cost, repeated reads and checks, rework, Human burden, token/time/cost where available, and actual isolation/permission/readiness evidence. Compare like-for-like tasks and source revisions where feasible; do not turn these into metric targets or imply a mandatory dashboard. Test continuation and fresh-context assurance against material failure modes. No runtime authorization, HI-004 closure or formation approval follows from this note.

Open questions: which work benefits from independent test design/implementation; when exploration isolation pays off; how much context can be transferred without losing invariants; which runtime mechanisms support safe continuation; whether extra Agents improve sufficient outcome quality relative to total cost. Revisit on material evidence. Promote only justified findings through the owning artifact and applicable Human review, not through repetition of these notes.

## 11. Bounded formation research discussion tracker

> Working discussion scope agreed 2026-11-25. This is a local research question/decision tracker, not a second cross-stage status tracker, mandatory execution workflow, or approval ledger. A5, A6 and HI-004 standing remain owned by the [cross-stage research tracker](../../experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md). Record agreed decisions here with their scope and limitations; do not infer canonical policy or formation approval.

| ID | Cross-Engineering question to settle | Concrete questions deferred to Go Builder | Discussion disposition |
| --- | --- | --- | --- |
| E1 | Formation decision discipline: when to consolidate, isolate execution, or separate Agent definitions; preserve coherent accountability and justify cost | Actual P1–P6 decomposition and Agent composition | AGREED WORKING DECISION |
| E2 | Information integrity: preserve authority, provenance, uncertainty, material meaning and independent access to evidence | Actual handoff content, collaboration and source reads | AGREED WORKING DECISION |
| E3 | Knowledge semantics: responsibility-local ownership, discovery, applicability, freshness, precedence and safeguards availability | Actual Go competencies, guidance organization and consumption | AGREED WORKING DECISION |
| E4 | Continuity accountability: identify who preserves material state and reconstructability without prescribing runtime mechanisms | Actual durable state, recovery and revision/evidence joins | IN DISCUSSION |
| E5 | Coordinator limits: coherent outcome, allocation, authority, reconciliation; no assumption of detailed technical production or runtime control | Concrete coordination behavior, dependencies and assurance readiness | OPEN |

Exit boundary: the five semantic questions have sufficiently clear working decisions to support concrete formation analysis; no universal Agent topology, handoff schema, knowledge loader, session manager, or Coordinator workflow is required. Transfer unresolved concrete questions to P1–P6; return only justified cross-Engineering findings to this note. Real execution evidence and any applicable Human approval remain separate.

### E1 — agreed working decision (2026-11-25)

Existing P02/P03/P04/P12/P17/P19 and Space Formation already justify necessary separation and coherent accountability. The remaining question is how to distinguish a separate Agent definition from conditional knowledge or a separate execution context. Agreed decision discipline: preserve binding authority and independence first; then assess shared invariants, distinct reasoning purpose, material context interference, transferable outputs, available competence and total coordination/reconstruction cost. Prefer consolidation for tightly coupled reasoning, conditional knowledge for expertise alone, isolated execution for bounded context-heavy work, and distinct Agent definitions when stable differentiated responsibilities, authority, independent judgment or a recurring materially different execution contract justify them. These are alternatives to compare, not a mandatory escalation sequence or numeric scoring rule. No final Go Agent count is implied.

Human agreed that separate Agent definitions may be justified by material execution effectiveness even without separation of overall outcome accountability, provided the bounded contribution, ownership and authority are clear. Form Agents around meaningful reusable responsibilities or bounded contributions whose separation materially improves accountability, authority containment, independent judgment, outcome quality or execution effectiveness. Compare consolidation, conditional specialization, isolated execution and separate definitions; do not create Agents merely for technologies, activities, stages, artifacts or context capacity limitations. Assess accountability, authority, independence, reasoning orientation, context characteristics, semantic coupling and total engineering cost. Preserve binding safeguards and coherent outcome accountability; no numeric scoring rule, mandatory decomposition sequence, final Go Agent count or formation approval follows. This is a Human-agreed working research decision, not operational policy or runtime evidence.

### E2 — agreed working decision

Information exchange is a correctness boundary: preserve meaning and standing across contexts. An observation must not become policy, an assumption must not become fact, and a recommendation must not become authorization through repetition. Multi-Agent agreement is not independent evidence. Agreed decision: exchange minimum sufficient information for the receiving responsibility, retaining material source/revision/authority, observations versus derived findings, assumptions, uncertainty, decisions and their standing, relevant evidence/limitations and unresolved dependencies. Prefer original source references over unnecessary transcripts where the recipient can access them; do not substitute references or summaries for essential content or direct grounding where required. Producers own accuracy and consumer fit of their contribution; consumers own contextual sufficiency and proportionate validation of material premises; Coordinator owns reconciliation of material contradictions and gaps in the overall Space result, not every message or repeated full review. Preserve independent source access and judgment where required, restrict sensitive information to legitimate need/access, and recheck affected references/claims after material changes. No universal message schema, broker, mandatory handoff artifact or full source reread per exchange is proposed. Concrete information exchange remains for Go P1–P6 analysis.

Human accepted Information Integrity & Consumer-Sufficient Exchange, including shared producer/consumer accountability and proportionate validation without mandatory repeated verification. This is a working research decision, not runtime evidence or operational policy.

### E3 — agreed working decision

Agreed decision: distinguish required competency (ability to fulfill responsibility), available capability (actual execution conditions), demonstrated competency (observed results), knowledge (technical information), guidance (application aids), and guardrails (applicable constraints). A skill or other packaging mechanism does not itself establish competence or authority. Preserve P19 responsibility-local knowledge and conditional specialization, with project-owned standards taking precedence over reusable defaults within higher safeguards. Formation should identify required core competencies, applicable specialized knowledge discovery and essential safeguards; avoid exhaustive catalogs. A consuming Agent must be able to discover relevant knowledge without reading all modules: use concise purpose/applicability cues and accessible source references, acquire only needed depth, and inspect applicable versions/assumptions against actual stack and project context. Coordinator may communicate known constraints and needs but need not select every knowledge item; the consumer owns selection, applicability and technical grounding. The legitimate owner of the reusable Agent/Space definition owns maintenance of its guidance; consumers surface material stale/conflicting guidance rather than silently rewriting it. External or project-owned sources retain their own authority; verify consequential version-sensitive claims proportionally and use current authoritative references when needed. Critical safeguards and applicable restrictions must be discoverable and known before affected actions; do not hide them in optional modules. Distinguish missing knowledge (acquire legitimate information) from missing capability or authority (seek authorized support, contain affected work or qualify the result). No mandatory skill format, directory topology, knowledge loader, global catalog, scheduled maintenance or universal loading sequence. Concrete Go competency depth, routing and packaging remain for P1–P6 and formation design; discovery reliability and demonstrated competency remain unverified.

Human agreed to three-level knowledge ownership (Engineering, Space, Agent), narrowest sufficient legitimate ownership scope, distributed knowledge with scoped discovery, and progressive retrieval complexity. Engineering owns cross-Space semantics and justified shared guidance; Space may own genuinely shared technical knowledge for its bounded responsibilities; Agent owns responsibility-specific guidance. Target-project rules and original technical sources retain their respective authority. Shared knowledge is not automatically loaded, and reuse alone does not justify promotion to a broader scope. Discovery considers scope, responsibility, actual applicability, version and legitimate access; direct references, concise descriptive indexes and repository-native search are candidate initial mechanisms. More sophisticated keyword, semantic or hybrid retrieval requires demonstrated need. Search relevance is not authority, correctness or permission; essential safeguards must not depend on optional retrieval success.

Human also raised the possibility that the existing "No centralized knowledge library" restriction may no longer be sufficient or valid. Open authority-reconciliation question: distinguish centralized storage/indexing from centralized semantic ownership, unconditional context loading and global technical policy. Evaluate against concrete Go Builder needs before proposing any change to P19, Engineering README or AGENTS guidance. Existing accepted exact content and research authority remain unchanged; E3 agreement is not permission to silently override them or adopt a global library. No physical layout or retrieval service is approved.

### E4 — current discussion framing

Candidate decision (pending Human agreement): session-independent accountability with distributed material-state ownership and coherent assignment-level reconstruction. Each participating Agent is accountable for preserving enough material state of its delegated contribution to support legitimate continuation and consumption; Coordinator is accountable for coherent reconstructability of the overall assignment, including authority/scope, allocations and outstanding dependencies, actual contribution standing and evidence applicability. Coordinator does not own every Specialist's internal scratch context or manage compaction. Human retains consequential authority and acceptance; Harness provides actual execution, persistence/access and containment mechanisms, not engineering judgment or authorization. Formation identifies necessary continuity properties and actual invocation uses authorized destinations under existing workspace routing. Reuse owning artifacts rather than duplicate state; record material decisions and their standing, actual changed state, relevant evidence/revision/conditions, unresolved findings and uncertain effects before relying on them downstream, and at meaningful safe boundaries proportionate to risk. Preserve material clues during unresolved investigation. Do not require a checkpoint per action or transcript persistence. Unexpected interruption can occur before an Agent records progress: absence of a record is not proof of no effect; reconcile actual repository/environment/operation state and legitimate authority before retrying affected actions. On resume, recover minimum sufficient context from current authority and durable evidence, revalidate changed/uncertain dependencies and qualify unsupported claims. Do not assume pending work is completed or replay uncertain side effects; contain only affected work and seek owner decision if safe reconstruction is unavailable. Separate session continuity from independent assurance; a resumed producer remains a producer. No mandatory run registry, checkpoint interval, session manager, scheduler, universal state schema or guaranteed crash recovery. Concrete state, ownership joins and runtime feasibility remain for Go Builder P1–P6 and separately authorized execution evidence.
