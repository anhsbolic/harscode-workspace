# Station 4 — Space-Oriented Research Frontier and Human Corrections (2026-10-18)

**Status:** CURRENT-EFFECTIVE WORKING RESEARCH CHECKPOINT; Anhar's corrections are explicit current-session design constraints, **not** an approved final architecture, operational Harscode policy, pilot authorization, or Station 4 exit.  
**Branch scope:** `research/harscode-purpose-llm-fit` only; authoritative operational Harscode remains `main`.  
**Lineage:** [2026-10-17 Station 3 closeout / Station 4 ABEE frontier](station3-closeout-station4-active-2026-10-17.md) and [owning retrospective](../harscode-purpose-and-agent-pairing.md). Preserve prior Station 1–3 research approval/history; do not rewrite it as if Space had been selected then.

## 1. Why the frontier changed

The 2026-10-17 ABEE v0.1 candidate used one capable Engineering Agent as default with adaptive work and conditional specialist/coordinator support. Human/assistant tabletop walkthroughs first used a narrow bugfix, then a hypothetical alternative C1 engineering entry against Kencleng's approved pre-engineering handoff. These were **conceptual exercises only**, not coding-Agent execution, independent review, runtime benchmarking or Station 5 piloting.

Anhar challenged ABEE's single-Agent organizing model because of session context-window pressure, generalist capability/bias, and weak standardized production responsibility across commitments. Discussion returned to the earlier *Space-Oriented Work Model* research hypothesis (proposal 0041 in historical experimental lineage). Current main Harscode workflow remains unchanged. Space is now the **leading working conceptual candidate**, not a proven or selected replacement for ABEE or workflow-v2.

## 2. Five connected conceptual dimensions (working v0)

1. **Agent formation:** A reusable Specific Agent Profile describes capability, specialization, expected work outputs and operating boundaries. An executable Agent binds suitable LLM/reasoning, knowledge, tools, guardrails, project authority and assignment scope. Profile wording does not prove actual competence. Reuse/refine/create by demonstrated need rather than producing a universal catalog upfront.
2. **Space formation:** A Space owns one coherent bounded production outcome with strict external contracts; one or several capability-matched Agents can work internally, sequentially/iteratively/in parallel. Scope uses outcome/contract cohesion, capability fit, context containment and useful separation—not necessarily one Agent, task, Stage or Run.
3. **Contracts:** An input contract specifies checkable conformance (types, required inputs, declared state/authorization provenance and interface compatibility where relevant). An output contract specifies deliverables, evidence, truthful completion/limitations. **Conformance is not a guarantee of substantive upstream content quality.**
4. **Composition:** A Space may be invoked standalone; its output can be considered for a next Space when the next input contract and applicable permission/quality acceptance conditions are satisfied. Human + Agent Pairing recommends or chooses next action, and may use bounded/risk-based delegation. No globally mandatory phase chain, coordinator or engine.
5. **Durable state:** Harscode definition, operational Harscode state and target-project authority are different owners. Candidate sibling paths: `/harscode-workspace`, `/harscode-state`, `/repo-project`. These are candidate layout, not mandatory physical semantics. Project-owned contracts, accepted specifications, code and actual evidence remain with owning project.

## 3. Explicit Anhar corrections to preliminary audit F1–F4

- **F1 — Input/version drift:** The Space is **upstream-blind** once given a conformant assignment. It need not continuously watch upstream versions or audit changed upstream semantics. Effective input/version coordination, revocation/reassignment and the consequence of a missed change are owned by **Human + Agent Pairing**. Risk consciously accepted to keep Space bounded. Space must still obey its own received assignment and local operating constraints; pairing must send an explicit changed assignment when needed.
- **F2 — Internal review:** A Space can contain Builder, Reviewer and API Tester. Reviewer/tester checks the Space's **produced work** against its accepted input, capability and output contract; no universal audit of upstream quality. Where a claim requires independent assurance, the verifier must actually be independent as required; a Builder cannot silently self-waive externally binding security/acceptance conditions.
- **F3 — Lost state:** For initial piloting, **assume local operational state is available**, not an obligation to build automated remote backup, recovery engine, ledger or alternate storage. If state is lost, Human + Agent Pairing inspects extant project/state evidence, reconstructs what is supportable and manually defines a new effective state if needed. Lost approvals, missing verification and uncertain partial writes are explicitly **unknown/not verified/not authorized**, never fabricated as accepted/PASS. Future stronger durability may use mechanisms beyond files/directories only if real evidence justifies them.
- **F4 — Human involvement:** Space remains upstream-blind. Human + Agent Pairing evaluates risk and outcome, recommends ordinary delegated continuation when safe, or asks Human for consequential decisions. No universal approval before each Space; however legitimately binding project permissions and independent assurance are not bypassed by a pairing recommendation.

**Ownership rule:** Human + Agent Pairing owns **cross-Space quality, version/routing coordination and consequential judgment**. Space owns **input contract conformance, scoped execution, output contract fidelity and its own operational guardrails**. The Space's successful output does not prove the whole project is correct.

## 4. Latest-state-first continuity; minimal history

**Current-Effective Snapshot** is the proposed default recovery/read surface for Human + Agent Pairing. Normal fresh-session entry starts by reading the current authoritative/effective commitment position, **not replaying the chain of historical Runs, Sessions, Events or handoffs**. It must point to effective objective, current material decisions, effective input/output and authority references, active/blocked work, acceptance/verification limits and next safe action to the extent needed. It is a *thin index/current view*, not a second owner of project truth.

Inside an active **concrete Space execution**, keep only the working state needed for safe continuation: accepted assignment reference, relevant partial artifacts, actual focused check results, unresolved work and next step. This may survive multiple replaceable Agent sessions. Old routine checkpoints need not be separately retained as permanent history. At terminal handoff, retain material output, evidence and unresolved obligations in appropriate owning sources, then retire redundant internal working material when safe.

**History-on-demand, not history-by-default:** Do not create immutable per-session/per-Run archives, universal audit logs, giant state projections or multiple synchronized registries merely to feel durable. Retain history/provenance only when materially necessary for project authority, approved decisions, protected operations, actual test/review evidence, diagnosis, legal/compliance, security, or known rollback/recovery concerns. Existing Git history and owning project artifacts may be sufficient. If no evidence survives, do not reconstruct a historical approval or claim a past test passed from memory.

**Guard against a false shortcut:** 'Read the latest' means **read the latest *valid current-effective state***, not trust the most recently edited file regardless of source or completeness. A compact snapshot must be enough to locate the owning evidence and distinguish accepted, unverified, blocked and superseded claims. Fresh-session reconstruction adequacy is a piloting hypothesis, not already validated.

## 5. Boundaries and unresolved empirical questions

- No specific Kencleng or Go Space/Agent contracts, file schemas, state machine, registry, orchestration code, mandatory storage engine or automation will be designed here.
- Space scope fragmentation versus bloat, reviewer independence in shared Space, conformance without semantic quality re-audit, risk-based routing, stale pairing coordination, and fresh-session recovery are **pilot test targets**, not accomplished results.
- Sibling `harscode-state` is a user-accepted **working directory name/location candidate**, not a physically created directory or durability guarantee. State-loss tolerance is accepted **for initial piloting only**, not automatic approval for sensitive production operation.
- Previous ABEE fixture/oracle/pre-exit evaluation materials were proposed **drafts** and have not been executed. The pre-exit audit requested by Anhar has now been discussed conceptually with corrections, but its exit evidence policy (empirical testing before exit versus Station 5 pilot) remains to be **explicitly reconciled**, not silently treated as passed or deleted.
- Material approvals and protected actions remain governed by their owning authority; normal risk-based Human autonomy cannot transform unverified evidence into PASS.

## 6. Current decisions, status and next step

**Current-session working direction:** Space-oriented candidate; specialized Agents compose bounded Space outcomes; strict input/output, upstream quality owned by Human + Agent Pairing; upstream-blind Space; internal output-focused reviewer; minimal latest-state-first operational continuity; candidate `harscode-state` external sibling directory; no overbuilt historical audit or automatic backup prerequisite for initial pilot.

**Not settled:** Selecting/promoting Space architecture; exact contract format, number of Space types, concrete Profile assignments, independent-assurance mechanism, retention mechanism, automated orchestration, or complete Station 4 exit policy.

**Station 4:** OPEN; conceptual pre-exit audit discussion occurred, **final Human exit approval not given**. **Station 5:** NOT STARTED/GATED by relevant product-driven handoff and authorization. **Station 6:** NOT STARTED. Nothing in this checkpoint amends `main` or target-project truth.

**Next research action:** Verify whether one current-effective Human–Agent Pairing snapshot plus active Space working state is sufficient for an ordinary fresh-session continuation, using a **conceptual** test first and reserving actual recovery/cost evidence for piloting. Then explicitly reconcile pre-exit scope and obtain Anhar's Station 4 decision; no automatic closure.
