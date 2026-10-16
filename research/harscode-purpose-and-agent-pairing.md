# Harscode Purpose & LLM-Fit Retrospective — Working State

**Status:** Active research / retrospective; non-operational.
**Started:** 2026-10-15 (Asia/Jakarta).
**Human decision-maker:** Anhar.
**Purpose of this file:** One durable, lightweight checkpoint for the Station 0–6 retrospective. Update when there is a material finding, decision, or station transition; do not maintain a second tracker or create Runs for this research by default.
**Authority boundary:** This is current retrospective working context, **not** canonical Harscode policy, an implementation mandate, or a promotion of experimental Orchestrator/Space semantics. Harscode main remains operational baseline until explicitly changed through applicable authority.

## 1. Destination (working, not yet canonical)

**Effective AI Engineering Partnership:** Anhar can bring a concrete engineering task or an ambiguous problem to AI Agent(s), obtain useful challenge and feasibility assessment, identify a fit-for-purpose solution, use suitable specialized expertise/tools, and reach trustworthy verified engineering outcomes with clear visibility and proportionate Human intervention.

Quality, authority, safety, and reconstructable state remain important; orchestration/automation, fixed stages, Space, and parallel execution are not goals in themselves.

## 1A. Station 1 — Rediscover Purpose (Anhar-approved retrospective baseline)

**Progress:** COMPLETE — Anhar approved Station 1 on 2026-10-16 (Asia/Jakarta), including purpose, boundaries/non-goals and all six success dimensions. This approval settles the **research/retrospective working baseline**, not operational Harscode policy or a change to main.

**Approved retrospective purpose (not operational/canonical Harscode policy):**

> Harscode is a foundation for Anhar to work with AI agents as competent, adaptive, trustworthy engineering partners. It should help understand and solve software engineering problems—whether bounded and clear or still ambiguous—through fit-for-purpose solutions, proportionate engineering rigor, visible reasoning and evidence, reliable continuity, and appropriate Human authority. Workflow, knowledge, specialization, state, and tools serve outcomes rather than constituting goals.

**Six approved retrospective success dimensions (qualitative; effectiveness remains to be validated):**

1. **Engineering quality:** correct, secure, maintainable, risk-appropriate outcomes with honest evidence.
2. **Fit and feasibility:** evaluate solution and execution feasibility; choose no more complexity than actual constraints demand.
3. **Effective pairing:** Anhar gains useful reasoning, challenge, practical execution, and judgment without becoming the perpetual dispatcher, prompt engineer, or process clerk.
4. **Visibility and trust:** clarify what is being done, why, what is proven/unproven, relevant risks, and precise Human decision points.
5. **Continuity and efficiency:** important settled intent/decisions/evidence reconstruct across agents/sessions while avoiding unnecessary rediscovery, rereading, and ceremony; current source still checked when material.
6. **Process health and proportionality:** engineering outcomes must be achieved without unjustified artifact proliferation, Runs/re-entries, redundant verification/context work, repetitive Human coordination, or non-converging loops. Judge cost against meaningful progress, new evidence, risk reduction, and necessary assurance—not raw activity counts. Harscode should be able to recognize and surface unhealthy patterns before reflexively continuing.

**Approved retrospective boundaries and non-goals:**

- Applicable to a narrow backend task, ambiguous investigation, or larger development effort; **no required end-to-end product pipeline**.
- Explore/Plan/Build/Review/Testing/PR is a useful engineering heuristic; **not a mandatory global phase sequence**.
- Orchestrator, Space, strict Work Unit/Run lifecycle, parallelism, workflow automation, dashboard, and particular storage layout are **optional hypotheses/implementation mechanisms**, not intrinsic purpose. A problem with no matching Space remains valid Agent Pairing input.
- Specialist profiles and non-LLM tools may help when task needs them; neither is mandatory or yet proven as a universal mechanism.
- Simplicity is constrained by real correctness, security, authority, independent verification where warranted, and reconstructability. Less documentation or fewer Runs alone are **not** success metrics. Conversely, an eventually correct result does **not** automatically excuse disproportionate process cost.
- **Process-health diagnostic is a desired capability, not an agreed dedicated workflow, dashboard, scoring system, mandatory audit Run, or monitoring platform.** Relevant signals include duplicative artifacts, repeated low-informational-delta Runs, recurring causal loops, excessive Human interventions, and unnecessary rediscovery/reverification. Interpret them with task context and risk; avoid treating a high count as proof of failure.
- Harscode owns reusable collaboration/engineering guidance; the target project retains its own product/design/security/implementation truth.

**Material tensions to test later, not decide at Station 1:** guidance depth versus LLM cognitive load; agent autonomy versus authority/safety; durable continuity versus artifact proliferation; collaboration benefit versus coordination cost; outcome correctness versus process burden. Diagnose process health proportionately **without creating a self-defeating diagnostic ceremony**. Existing main guidance and pilot ideas must be evaluated by actual results, not protected by sunk cost or discarded based only on impressions.

**Station 1 exit:** Approved by Anhar, 2026-10-16. Purpose, six evaluation dimensions and boundaries are agreed for this retrospective. No architecture, implementation mechanism or operational Harscode guidance has been approved by this decision.

## 1B. Station 2 — Understand Human–Agent Pairing (scope proposal, not yet approved)

**Started:** 2026-10-16. **Progress:** IN DISCUSSION — scope clarification. This is a requirements/experience inquiry, not design of a new workflow or architecture.

**Core question:** Given a bounded or ambiguous engineering concern, what collaboration and Agent behavior would genuinely help Anhar reach a trustworthy, feasible outcome with proportionate process cost?

**Proposed inquiry boundaries:** (1) starting interaction/task ambiguity; (2) reasoning, challenge and fit-solution discovery; (3) Agent autonomy, Human authority, specialists and non-LLM tools; (4) visibility, durable continuity and process-health awareness; (5) useful completion, evidence and handoff.

**Representative situations, not mandatory phases:** (A) well-defined backend task; (B) ambiguous engineering investigation; (C) work requiring additional specialist/independent verification. Cases are probes for behavior, not full end-to-end implementation tests at this station.

**Expected minimal exit evidence:** One compact account of desired Agent behaviors across the representative cases, Human–Agent authority/intervention boundaries, visibility/continuity needs, and material unresolved questions. Avoid additional documents, run structures and fixed process stages unless demonstrated necessary.

**Explicit exclusions:** No audit of whether current main/pilot already satisfies the needs (Station 3); no Space, Orchestrator, Profile architecture or tool design (Station 4); no validation experiments (Station 5). No assumption that collaboration must involve coordination, parallelism or a predefined Space.

**Additional pairing concerns from Anhar (2026-10-16; research observations, not approved policy):**

- Communication should be natural but use a concise, readable and sufficiently consistent decision-summary format when discussing material problems. Preserve problem, relevant evidence, tradeoffs, recommendation, decisions and next actions without ceremonial headings on every message.
- Human should supply task-appropriate inputs and prerequisites (requirements, bug symptoms, constraints and material approvals). Agent should challenge insufficient or contradictory inputs before execution. An unclear problem remains a valid starting point for investigation.
- Avoid material planning or redesign during an execution assignment. Distinguish ordinary implementation judgment from discovery of an unresolved material contract, authority, security, or architectural choice. The latter warrants a scoped stop and owner decision; it should not be resolved silently within execution.
- Need to investigate whether communication and readiness expectations should differ by task type, without prescribing one universal form, session split or new workflow mechanism.

**Scope status:** Proposed by assistant for Anhar review; not yet an Anhar-approved Station 2 scope.

## 2. Starting point — evidence and limits

- Harscode operational main at branch creation: c762a27aee622c247c2a408d932e762076e3588c. Main has portable pre-engineering, optional product-design, engineering phase guidance, best practices, harness translation, durable context and verification semantics. Anhar reports positive practical results using it on bounded backend tasks; this does not prove all tasks or all LLM configurations.
- Harscode experimental Orchestrator pilot baseline inspected: 651ce57f044bff23fba99082322cee6c066d25a6 on pilot/orchestrator-v0.1-c1. It contains Work Unit/Run protocol, Profiles/Specializations and other mechanisms; none become canonical simply because they exist.
- Kencleng C1 offers real verification wins as well as coordination, environment and stale-state friction. The observed 57 Run directories are **not** a measured count of actual Participant executions; no reliable exact avoidable-cost attribution has been established.
- Proposal 0041 (Space-Oriented Work Model) is **Research Hypothesis — Deferred**, explicitly non-operational; it must not be treated as a chosen architecture.
- Repository truth may evolve. Recheck current refs and relevant live evidence before decisions; the commits above describe this starting checkpoint, not permanent current heads.

## 3. Human intent and constraints captured in retrospective

1. Prioritize intention, intended outcome, feasibility, and fit solution; technical detail remains appropriate when material, not the default center of gravity.
2. Desired experience is **Agent Pairing** (human–AI engineering partnership), not a mandatory dedicated Orchestrator product or workflow coordination engine. Multiple agents/parallelism are optional when useful.
3. No intent to build workflow automation or a strict engineering factory. Explore → Plan → Build → Review → Testing → PR is a useful heuristic, not an unconditional required chronology.
4. Fit-for-purpose, simplest sufficient robust solution; avoid fancy architecture and unnecessary ceremony, while retaining essential correctness/security safeguards.
5. Strong concern for **visibility** (what is happening, why, evidence, Human decisions) and **feasibility** (can the problem/solution actually be executed under current constraints).
6. Reconstructable durable state should reduce unnecessary cross-session/agent rediscovery and redundant document/codebase learning, without replacing necessary inspection of live source and authority.
7. Harscode should work for a single backend task, ambiguous investigation, or broader work as needed; full product lifecycle is not compulsory.
8. Existing orchestration implementation may prove entirely unnecessary; do not preserve it for sunk-cost reasons. Still assess its individual useful capabilities on their own merits.
9. Existing main guidance and best practices may themselves impose excess LLM context/process load; their effectiveness needs comparative real-use evidence, not assumption.
10. Specialized Agent Profiles are a promising preference: find appropriate capabilities for a problem without mandating persistent personalities, premature Space fitting, or a readiness ceremony.
11. Non-LLM tools may be useful where they are simpler or more reliable; avoid building a tooling platform without evidence.
12. A Space, if ever useful, should arise from a genuine bounded input/output responsibility. **An ambiguous or unmatched problem must still be serviceable by Agent Pairing without a pre-existing Space.**
13. (2026-10-16 clarification) Correct engineering outcomes must be **balanced with healthy, proportionate execution**. Harscode should recognize potentially excessive artifacts, Runs, re-entry, redundant verification, repetitive Human coordination, and similar process overhead; do not mistake raw activity counts for diagnosis or assume the existing experimental Loop Health Audit mechanism is required.

## 4. Station map and progress

These are retrospective learning checkpoints, **not** Harscode runtime workflow phases or a new process engine.

| Station | Focus | Progress | Exit evidence |
| --- | --- | --- | --- |
| 0 — Current Reality | Establish honest starting baseline | BASELINE RECORDED | main/pilot distinction, known evidence and uncertainty captured here |
| 1 — Rediscover Purpose | Purpose, user needs, boundaries, non-goals | COMPLETE — Anhar approved 2026-10-16 | Reviewed purpose statement and evaluation criteria, no mandatory architecture |
| 2 — Understand Human–Agent Pairing | Actual desired interactions and capabilities | IN DISCUSSION — scope draft | Clear behavioral needs across bounded and ambiguous cases |
| 3 — Reality Check Harscode | Audit value and burden of main guidance, pilot, research | NOT STARTED | Evidence map: working, uncertain, costly, redundant, unnecessary |
| 4 — Smallest Sufficient Model | Compare ways to satisfy established needs | NOT STARTED | One testable working hypothesis with trade-offs, not a complete new framework |
| 5 — Real-Usage Validation | Limited representative engineering tasks | NOT STARTED | Evidence on quality, Human burden, feasibility, visibility, rediscovery and cost |
| 6 — Evidence-Based Commitment | Decide what belongs in operational Harscode | NOT STARTED | Anhar-approved decision grounded in real results; changes only with explicit authorization |

**Current location:** Station 1 complete and approved; Station 2 active (scope under discussion, not approved). Continue with human–agent interaction needs before evaluating solutions.

## 5. Working decisions and unresolved hypotheses

**Working agreements (2026-10-15, Anhar approved):**
- Use Station 0 → 6 as the *retrospective roadmap*, not a workflow that every task must follow.
- Keep the research isolated from operational main and experimental C1 Orchestrator execution.
- Do not choose Agent Pairing, Space, Orchestrator, fixed phases, automation, or any artifact model as the new canonical architecture yet.
- Evaluate proportionally to real consequence. Protect safeguards, avoid premature complexity and speculation; use real Kencleng usage as evidence, not automatic project-agnostic policy.

**Station 1 approval (2026-10-16, Anhar):** Approved the purpose, boundaries/non-goals and all six success dimensions (Engineering Quality; Fit & Feasibility; Effective Pairing; Visibility & Trust; Continuity & Efficiency; Process Health & Proportionality) as the **retrospective evaluation baseline**. Station 1 is closed; proceed to Station 2. No promotion into operational main or commitment to an implementation architecture.

**Still open:**
- What concrete Human–Agent Pairing behavior best serves different classes of problem?
- How much existing main guidance helps or burdens specific LLM agents in real tasks?
- Which pilot capabilities have separable value without its orchestration protocol?
- Whether Space has any necessary semantic value beyond direct Agent Pairing and explicit bounded outputs.
- What evidence is sufficient to assess improvement without creating a monitoring bureaucracy?
- What is the minimum viable way to **notice and diagnose unhealthy process cost** without mandating an additional Run, report, scoring service, or ceremony? Existing experimental `orchestration/pilot-2-candidate/loop-health-audit.md` covers a narrower repeated-loop case; it is research material, not a selected solution.

## 6. Source pointers

- Operational main: https://github.com/anhsbolic/harscode-workspace/tree/main
- Main workflow: https://github.com/anhsbolic/harscode-workspace/blob/main/workflow/README.md
- Main context management: https://github.com/anhsbolic/harscode-workspace/blob/main/workflow/context-management.md
- Pilot Orchestrator: https://github.com/anhsbolic/harscode-workspace/tree/pilot/orchestrator-v0.1-c1
- Pilot Participant Profiles: https://github.com/anhsbolic/harscode-workspace/blob/pilot/orchestrator-v0.1-c1/orchestration/pilot-2-candidate/participant-profile-discovery.md
- Pilot Loop Health Audit (experimental, narrow scope): https://github.com/anhsbolic/harscode-workspace/blob/pilot/orchestrator-v0.1-c1/orchestration/pilot-2-candidate/loop-health-audit.md
- Space research: https://github.com/anhsbolic/harscode-workspace/blob/pilot/orchestrator-v0.1-c1/proposals/0041-space-oriented-work-model-research-hypothesis.md
- Kencleng C1: https://github.com/anhsbolic/kencleng/tree/pilot/3-c1-engineering

## 7. Continuation rule

At the next session, read **this file** as the current retrospective checkpoint, verify live repository authority where material, and continue from the indicated station. Update only material findings/agreements/transitions in this file. Keep observations, hypotheses, Anhar working decisions, and durable canonical Harscode changes explicitly distinct.

**Immediate next action:** Confirm or adjust Station 2 scope, then examine the first representative pairing situation (a bounded engineering task). Do not design or implement a new architecture yet.
