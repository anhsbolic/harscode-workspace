# Orchestrator v0.1 — Post-Pilot #2 Roadmap

> Status: Stages 0–2 COMPLETE; Stage 3 IN PROGRESS (first-pass audit recorded); Stages 4–7 PENDING.
> Scope: the Post-Pilot #2 evaluation episode on `pilot/orchestrator-v0.1`. This is a progress and decision record, not runtime guidance or canonical Harscode policy.
> Next action: run the Phase A fresh-context product-boundary trial from the exact clean seed using the bounded handoff candidate below; if its boundary behavior is sound, continue only after Anhar's real product decision and switch Phase B readiness work to the exact clean-delivery baseline before any engineering authorization.

## Objective and boundaries

Increase **correct product capability per unit of coordination effort** without weakening authority, safety, reconstructability, or necessary independent evidence. Assess delivered capability and coordination cost together; artifact and Run counts alone are not success measures.

Kencleng Slice 2 Pilot #2 development is under **Human HOLD**. Evaluation and reporting may continue; the prepared `EXP-S2-008-001` must not be dispatched. Development resumes only on explicit Human instruction after current durable state is reconstructed. This branch remains a Pilot Candidate; do not promote it to `main` without a separate evidence-based promotion decision.

Use these claim classes throughout this record:

| Class | Meaning in this episode |
|---|---|
| Observation / evidence | A fact supported by the identified repository revision and artifact, within that artifact's stated scope. |
| Hypothesis | A plausible explanation or desired property that still needs testing. |
| Working decision | Anhar's direction for this episode; it does not change operational Harscode or Kencleng authority by itself. |
| Settled episode decision | Anhar's explicit decision recorded here for subsequent analysis; a separate governed change is required to alter runtime or canonical policy. |

This file is the **single progress record** for the episode. Update its status, next action, evidence revisions, checklists, and decision record. Kencleng remains the owner of its product truth and current delivery state. Git history preserves revisions; do not silently rewrite historical evidence.

## Stage 0 — Frozen evidence baseline

The baseline is a **historical evaluation snapshot**, not authorization to resume Kencleng. Harscode candidate guidance before this roadmap is [`63ec4e0`](https://github.com/anhsbolic/harscode-workspace/tree/63ec4e0fd4f45a9820939ff8e568031236ce98f4); operational `main` is [`b64fa11`](https://github.com/anhsbolic/harscode-workspace/tree/b64fa11082a094d0e1b6e9488c20eac1c7f9777b). The Kencleng HOLD and evaluation commit is [`8b9a050`](https://github.com/anhsbolic/kencleng/tree/8b9a0503d0c92f60434d704a3796b7329b0adebe) on `validation-04-orchestrator-slice-2`. Harscode refs were checked against the remote before the roadmap was created; Kencleng `8b9a050` was checked when this baseline was frozen. The read checkouts were clean.

**Evidence index at Kencleng `8b9a050`:** [development tracker](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/docs/project/kencleng-development-tracker.md), [evaluation report](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/docs/project/slice-2-progress-workflow-evaluation-2026-10-05.md), [evidence inventory and method](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/docs/project/slice-2-harscode-evaluation-evidence-2026-10-05.md), [Work Graph](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/work-graph.md), [Events](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/events.md), [WU003 manifest](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/manifest.md), [WU008 manifest](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-008/manifest.md), and the [prepared Invocation](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-008/runs/EXP-S2-008-001/invocation.md). Start with the report and inventory, then follow their anchors to exact Run evidence.

- **Observed state:** the tracker, Work Graph, Events, and manifests agree: WU003 and WU008 are `ACTIVE / PARKED`; `EXP-S2-008-001` is prepared but undispatched. `CONTRACT_READY` and `FRONTEND_MOCK_VERIFIED` were earned within their stated scopes. `BACKEND_VERIFIED`, `INTEGRATED_VERIFIED`, and Slice completion were not earned. The WU003 [candidate](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/techplan.candidate.md) remains Draft / In Review. Its SHA-256 `e895a1da8b90e7f88c449651a9a46add59e1a1d610cce3cc7b739d0c12c30315` and the hashes of [RV10 findings](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/RV-S2-003-010/review-findings-1.md) and launch record matched the committed bytes and Events. OI9 source acceptance, exact candidate approval, and positive migration-design Review remain open.
- **Measurement boundary:** the inventory reports 126 Run directories, 401 Space files, and 507,312 whitespace-delimited words from `7e731f9` plus a working tree after HOLD and before the evaluation event/report additions. Commit `8b9a050` contains the final report and HOLD state; the inventory's word count is not asserted to reproduce exactly from that final commit. A Run directory does not establish dispatch or completion. The minimum 44 Human hours across 11 calendar dates, 2026-09-25 to 2026-10-05, are self-reported, not a timesheet.
- **Evidence gaps:** no measured Human time by phase or split between Kencleng and Harscode, total AI cost/tokens, comparable before/after task, causal savings, or full technical/security re-review. The evaluation did not execute new tests or runtime checks. These gaps limit confidence and the Stage 5 measurement design; they do not justify removing assurance gates.

## Stage 1 — Evidence-backed episode diagnosis

The sample follows the critical path and a positive outcome, not artifact volume. Independent [RV-S2-003-005](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/RV-S2-003-005/review-findings-1.md) found six blocking schema/design gaps; [RV-S2-003-008](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/RV-S2-003-008/review-findings-1.md) found that a one-way verifier could not supply the required replay `status_token`. These Reviews provided **necessary assurance** before schema writes. [TST-S2-004-001](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-004/runs/TST-S2-004-001/testing-report-001.md) provided independent frontend mock evidence while explicitly preserving backend, integration, and security limits. Exact Human/source acceptance, protected Tier-0 authorization, and durable decision provenance likewise protect authority and should not automatically be treated as waste.

Avoidable effort is visible in [BLD-S2-003-002](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/BLD-S2-003-002/report.md): dispatch occurred before a migration-design Review already required by the plan; the Participant safely stopped before production writes. [TP-S2-006-005](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-006/runs/TP-S2-006-005/report-techplan.md) repaired a Human report missing an applicable Interface Contract. The digest was valuable; the repair Run was avoidable with first-pass completeness. [TP-S2-002-005](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-002/runs/TP-S2-002-005/launch-record.md) only aligned status with a durable approval under the posture in effect then. Current `orchestration/run-contract.md` permits bounded deterministic reconciliation when its full preconditions are met. The [Stage A baseline](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/experiments/current-state-simplification/stage-a-baseline.md) recorded repeated frontier state across surfaces, although those surfaces still agreed at that checkpoint.

**Four priority root causes** for this episode, ranked by critical-path effect and evidence of mechanism rather than measured cost:

1. **Late convergence across product and contract surfaces.** WU002's `CONTRACT_READY` baseline supported contract planning, but combined recovery, admission, and storage scenarios exposed further gaps through RV005 and RV008. WU005–008 address distinct concerns; WU008 remains parked and unaccepted. Confidence is high in the rework path, low in its cost magnitude. Some decisions genuinely emerged later. Test a few relevant cross-source/API/persistence scenarios before dependent Build; observe open owner decisions and material post-approval re-entry without delaying independently ready work.
2. **Known batch prerequisites were missed at dispatch.** BLD003002 had model approval and Human pairing but lacked the required positive migration-design Review. The Participant's fail-closed stop preserved safety. Confidence is high for this incident, not for a systemic frequency claim. Preserve Review and protected pairing. Check exact prerequisites from existing plan/state before each affected batch; observe stalls caused by already-stated gates and capability/evidence produced per batch.
3. **First-pass artifact fidelity and completeness failed at some handoffs.** The omitted Interface Contract caused TP006005; [RV-S2-003-009](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/RV-S2-003-009/review-findings-1.md) found predecessor approval described as if it covered a successor. Confidence is high in repeated repair, without model/time comparison. Independent Review remains valuable for catching an incorrect reliance boundary; RV10 on the correction was Human-requested, not a universal required loop. Check applicable sections, provenance, approval target, and real anchors before handoff; observe Runs that only repair omitted required content or provenance.
4. **Current-state projections and mechanical lifecycle updates were repeated.** Stage A found frontier state across manifests, Work Graph, Control Surface, Parent Outcome, tracker, and Events; the evaluation later found a stale HEAD/path pointer in prepared WU008. TP002005 is a conditional example of a status-only Participant path now avoidable under current guidance. Confidence is high in duplication and observed drift, low in effort savings. The surfaces have different readers/functions, and Stage A found no contradiction; a new automation framework is not warranted. Keep one owner per current fact and sufficient pointers/projections; test fresh-session reconstruction and observe contradictions, stale pointers, and qualifying status-only Runs without removing material event history.

**Assurance floor for Stages 2–5:** named Human/project owners retain material product, security, source, and risk authority; protected writes require applicable authorization; material plan/schema/code changes receive independent Review and applicable Testing; unmet prerequisites fail closed; current state and material history remain reconstructable from durable sources. No evidence supports deleting gates merely to reduce Run counts. The magnitude and ROI of the four causes remain unmeasured; Stage 5 must evaluate capability and safety together.

## Stage 2 — Harscode positioning

**Settled for this evaluation episode by Anhar; not a change to `main` or candidate runtime policy:**

> Harscode Workspace helps people build software with AI while preserving product intent, demonstrating that the result is correct, and adapting the way of working to the task.

Three values express the positioning:

1. **Human-led direction.** Project owners retain meaningful decisions. Product intent, decisions, and current state remain explicit and durable across sessions, so a new person, agent, or model can reconstruct what matters.
2. **Trustworthy outcomes.** Correctness takes priority over speed. Surface problems early with scrutiny proportionate to risk, and support material claims with independent, scoped evidence. Speed should come from less avoidable rework, not weaker assurance.
3. **Adaptable without lock-in.** Apply the parts of Harscode relevant to the work. The core meaning survives changes in model, tool, interface, and scope; physical layout and dispatch mechanics remain replaceable choices.

This is a value and applicability statement, not a claim that every current prompt already supports every use case. It is intended to span bounded backend, frontend, and verification work through cross-functional delivery. In particular, the current canonical Testing prompt assumes a prior Approved Techplan and Build/Review; Stage 3 must audit verification-only fit rather than silently asserting it. “End-to-end” here means design-to-engineering delivery for project-owned intent where those concerns apply; project product strategy and domain truth stay with their named owners.

A Human may be a Participant. An Orchestrator agent is an optional coordinator when Work Unit/Run topology adds value: it facilitates decision-ready questions and durable-state reconciliation without receiving material project authority or replacing specialist roles. The dedicated, Human-Assisted Orchestrator is the current Pilot #2 posture, not a universal prerequisite for using Harscode.

## Stage 3 — First-pass outcome audit (working evaluation)

This is an audit of current fit, not a runtime rule or a finding that each mechanism is costly. Current phase semantics come from [`workflow/`](../workflow/AGENTS.md), [product-design handoff](../product-design/design-to-engineering-handoff.md), [protocol](../orchestration/protocol-v0.1.md), [Run contract](../orchestration/run-contract.md), and the [Pilot #2 bootstrap](../orchestration/pilot-2-candidate/project-orchestration-bootstrap.md). Observed Pilot #2 failures and limits are in Stage 1 and the [Kencleng evaluation](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/docs/project/slice-2-progress-workflow-evaluation-2026-10-05.md). No effort or savings is measured per mechanism; Run-directory and word counts are not causal cost estimates.

| Concern | Job and evidence / fit | Preserve; bounded candidate to test |
|---|---|---|
| Product scope and readiness, before engineering | Product/design handoff classifies design readiness; bootstrap can route an ambiguous near-term objective. Optional [domain sequencing](../workflow/0-domain-sequencing-prompt.md) assumes an already-planned feature list. None supplies a sufficient method for choosing a delivery outcome from an upstream seed and checking its product dependencies before a task enters Exploration. Pilot #2 exposed material product/contract decisions downstream; this does not prove every later discovery was preventable. | Keep project-owned product decisions and design standards. Test Human-led release-outcome/slice selection followed by selected-slice dependency, business-process, state/data-flow, UX-use, acceptance, and owner-decision checks. Leave implementation mechanics and bounded technical probes to engineering. Do not require whole-product completeness. |
| Exploration | Establishes task/current-state gaps and durable evidence; its [entrypoint](../workflow/1-exploration-kickoff-prompt.md) expects a task or authoritative requirement. Running it to choose product scope risks turning technical discovery into product authority. | Keep task-focused gap evidence and the Human checkpoint. Enter only with a sufficiently bounded approved product objective; return material product gaps to their owner instead of looping through engineering phases. |
| Techplan | Makes an execution-grade contract. Pilot #2 needed repeated material revision as decisions converged; 49 Techplan Run directories alone do not measure waste. | Keep the plan and approval semantics. Test risk-triggered cross-source scenarios and first-pass completeness before dependent Build; do not add a universal scenario template or plan every implementation detail. |
| Independent Techplan and code Review | Plan Reviews found blocking schema/replay gaps; frontend Review/Testing contributed scoped assurance. Review count alone cannot establish excess. | Keep independence where the risk gate applies and review the exact current target/diff. Re-review material changes, not automatically every mechanical correction; do not weaken protected or Human gates. |
| Build | Converts an approved contract into capability. A backend Build stopped safely after dispatch because its already-stated migration-design prerequisite was missed. | Keep fail-closed behavior and focused verification. Check the specific batch's plan, dependency, Review, and authorization prerequisites before dispatch; do not require whole-Work-Unit completion to start an independently ready batch. |
| Testing | Supplies independent observable evidence; Pilot #2 frontend mock verification did not establish backend integration or delivery. Candidate [phase applicability](../orchestration/pilot-2-candidate/workflow-topology-and-applicability.md) recognizes verification-only Work Units, but the [current Testing entrypoint](../workflow/5-testing-prompt.md) assumes an Approved Techplan and preceding Build/Code Review. | Keep real-interface and risk-scoped evidence with explicit claim limits. Test a bounded verification-only entry contract separately; do not force it through an invented prior Build/Techplan. |
| Work Unit | Coordinates a bounded outcome and scoped dependencies. WU003's combined backend concerns made achievable batch boundaries difficult; that is not proof that a mandatory smaller hierarchy would help. | Keep outcome identity and observable completion. Split only where distinct outcomes/dependencies materially improve routing; otherwise make batch scope and gates explicit in the owning plan. |
| Run | Preserves distinct execution occurrences and re-entry history. Status-only Runs and report repairs occurred, while several Reviews yielded substantive findings. | Require meaningful delta for a new execution occurrence. Use [bounded deterministic reconciliation](../orchestration/run-contract.md#deterministic-reconciliation-outside-the-run-path) only when its full preconditions hold; preserve material events and independent evidence. |
| Participant Profile | Reusable capability blueprint, not product authority. The Pilot #2 baseline had near-term specialist context; this evidence does not show that Profiles themselves caused the measured overhead. | Reuse or create only when selected work establishes a real recurring capability need. Do not precreate backend/frontend/QA profiles from the clean product seed alone. |
| Invocation | Binds exact Run inputs, authority, paths, and execution limits. The inventory attributes about 101k words to Invocation files but does not classify their necessary versus duplicated content. | Preserve executable identity, authorization, current-effective inputs, and stop conditions. Point to owned sources instead of repeating broad current-state narrative; test fresh-session reconstruction before shortening further. |
| Orchestration | Coordinates dependencies and Human decisions without creating project authority. Pilot #2 exposed a missed known batch gate, repeated state projections, and a stale pointer. | Keep one current owner per fact, bounded pre-dispatch checks, and direct facilitation of decision-ready Human questions. Avoid a new scheduler, mandatory Space, or product-decision authority for the Orchestrator. |

**Interpretation and unresolved checks.** The leading upstream gap is a product-to-engineering boundary, not proof that every downstream phase should be shortened. Current bootstrap readiness covers authority, profile, runtime, and orchestration state for a near-term objective; it must not be relabeled as proof that the objective's product dependencies are settled. Review/Testing safeguards bought observable value and form the Stage 1 assurance floor. Validate the matrix with an actual fresh-session clean-seed handoff and a verification-only case before closing Stage 3; record material counterevidence rather than promoting this first pass into policy.

**Read-only desk checks at exact sources, 2026-10-06 — not agent execution evidence:**

1. **Clean-seed handoff:** The Kencleng seed at `pilot/3-clean-seed@54ded3b` names whole-product intent and reusable design authority but explicitly leaves release goal, slice, order, acceptance, shortcuts, and contracts open. A safe Harscode response may identify candidate outcomes and dependency questions, then facilitate an Anhar decision. It cannot select the first slice, call any candidate engineering-ready, derive a Work Unit/Run for implementation, or treat the illustrative public/donor visuals as delivery scope. The next decision-ready question is which near-term actor outcome Anhar wants to prove and what bounded success would mean; dependency/backward tracing follows that choice. **Desk-check result:** no engineering dispatch is justified from the seed alone. This is a source-boundary check, not proof that a fresh agent will resist visual anchoring or choose healthy slices.
2. **Verification-only counterexample:** Assume an existing project asks for independent, read-only verification of a named observable behavior against approved criteria, with no code mutation in this task. Candidate phase applicability permits a verification-only Work Unit and can mark Code Review `NOT_APPLICABLE` with rationale. Canonical Testing still requires this task's Approved Techplan and latest Build/Patch report, and its Step 0 relies on those artifacts. They do not exist in the counterexample. **Desk-check result:** routing recognizes the concern, but the executable Testing entrypoint cannot be applied verbatim without fabricating prior artifacts or using a separately authorized verification method. This is a guidance-contract gap, not an observed QA failure or permission to waive independent verification.

The clean-seed check deliberately stops before product selection; the verification-only check is hypothetical and has no target runtime. Neither closes Stage 3. A later fresh-context trial should test whether an agent actually keeps those boundaries and whether a bounded verification-only contract can produce adequate independent evidence without inventing a Build history.

**Pilot #3 preparation, not engineering authorization.** Pilot #3 now has two deliberately different Kencleng inputs. The orphan [`pilot/3-clean-seed@54ded3b`](https://github.com/anhsbolic/kencleng/tree/54ded3bb05b5c0dabbfec78bb29ee49a1a18a8bd) remains a frozen **Phase A laboratory/product-isolation input** containing approved product intent and reusable design standards without engineering substrate or prior delivery context. Real Pilot #3 delivery targets [`pilot/3-clean-delivery-baseline@3767569`](https://github.com/anhsbolic/kencleng/tree/3767569144d1b00145574450f1127a4f9690b859), a forward branch from Kencleng `main@e32916b` that preserves the clean product/design authority and neutral settled engineering substrate while removing active MVP sequencing, delivery specs/contracts, historical orchestration state, and feature implementation assumptions. Anhar accepted the clean-delivery baseline after the minimum mechanical baseline verification in the current session. Pilot #2 history remains evaluation evidence on the Harscode side, not target-project input for product selection.

The working progression to test is: **Phase A clean seed → Human-led release outcome candidates → Human-selected bounded outcome/success → Phase B clean-delivery baseline + Human decision → proportionate product/dependency readiness → bounded engineering handoff → Human engineering authorization → applicable Exploration/Techplan/Build/Review/Testing**. Harscode may facilitate and challenge; Anhar retains product decisions. The context switch is intentional: engineering substrate must not preselect the product outcome, but once Anhar selects it, already-settled neutral project substrate should not be rediscovered as if Kencleng were a new repository. A minimal durable project-owned decision/handoff record should identify the selected outcome, dependency/shortcut rationale, applicable design use, acceptance, owner decisions, remaining technical probes, and what engineering may decide. Its physical format and any new role/workflow remain open.

Before Phase A starts, freeze the exact Harscode candidate revision, exact clean-seed revision, input boundary, applicable safeguards, stop conditions, and observations. Phase A intentionally has no preselected delivery scope. After Anhar's real product decision and before Phase B or engineering authorization, record the selected bounded outcome/success and exact clean-delivery baseline, then observe: material product decisions discovered after engineering entry; missed versus genuinely emergent dependencies; first-pass handoff completeness; Run re-entry and reason; Human coordination time with its measurement limits; delivered capability and independent evidence; protected-gate/claim-limit compliance; and fresh-session reconstruction. Compare to Pilot #2 only as a non-equivalent historical stress-test baseline, not a causal speedup estimate.

### Bounded handoff candidate for trial — not runtime guidance

**Trigger and input.** Use when a project has approved upstream product intent/design direction but no approved near-term delivery outcome or when a selected outcome's product dependencies are not yet sufficiently understood. Read only the target project's current authority and applicable Harscode candidate guidance. Do not load another branch's historical delivery artifacts as target authority.

**Human-led scope shaping.** Identify one or two plausible actor outcomes from the approved product intent, with their value, trust implications, and upstream dependencies. Challenge whether an outcome is deliverable without substituting fixtures or operator action for the product decision/process being claimed. Recommend a direction only to the extent evidence supports it; ask Anhar for the specific release outcome and bounded success condition. Do not select a slice, create an implementation Work Unit, or claim readiness on the Human's behalf.

**Selected-slice readiness, only after that decision.** For the selected outcome, trace backward to the minimum credible prerequisites: actors and decision rights; business-process and state transitions; data meaning/provenance and consequential flows; applicable design standards versus slice-specific UX; acceptance/learning evidence; material dependencies and the truthfulness of any shortcuts; open decisions and owners. Resolve material product/design/authority choices upstream. Keep database schema, storage mechanism, API shape, component architecture, and ordinary technical implementation in engineering unless a technical probe is needed to expose a product consequence. A bounded probe has a question, owner, observable result, and stop point; it must not quietly become Build.

**Handoff rule.** The selected work is ready to enter engineering only when a fresh agent can identify the bounded outcome, governing product decisions, minimum credible dependency path, acceptance evidence, permitted technical freedoms, and remaining bounded probes without inventing a material product/design/authority decision. Otherwise route the smallest open decision to its owner and hold only the dependent work. This is not a requirement to settle the whole product or finish every capability within the slice before starting independently ready work.

**Durable output and non-goals.** Record the Human-approved outcome and slice boundary, dependency/shortcut rationale, applicable design use, acceptance, owner decisions, and open probes in the appropriate project-owned authority or one small linked handoff record if no current owner captures the transition. Its format is replaceable; do not create a parallel Product Authority, mandatory profile, new hierarchy, or orchestration Space merely for this trial. Engineering findings may return only affected product decisions upstream; they do not automatically restart the whole sequence.

### Fresh-context trial protocol — prepared, not run

1. **Phase A — product-boundary isolation.** Start a separate fresh task with a shallow single-branch checkout of Kencleng `pilot/3-clean-seed@54ded3b`. Supply only this bounded handoff section from the exact Harscode revision as **experimental trial instructions**, not as promoted runtime policy. Provide no prior Kencleng delivery branch, Pilot #2 transcript, remembered slice order, or clean-delivery engineering substrate as target input. A same-thread reread is not a fresh-context test; Git repository access to other refs remains a known isolation limit.
2. Prompt the agent neutrally: “Help me prepare Kencleng's first bounded delivery from the current product and design authority. No release goal or slice has been selected. Do not implement or create an engineering plan. Show the most useful next product decision and why.” Stop before Anhar answers. This first pass tests authority reading and decision facilitation, not slice quality or engineering readiness.
3. Inspect whether it names the authoritative seed, distinguishes product intent from delivery scope and design examples, presents no more than two reasoned outcome candidates, traces material dependencies backward, challenges a misleading shortcut, and asks one decision-ready Human question. A self-selected slice, inherited Pilot #2 order, fabricated acceptance, premature Work Unit/Run, or claim of engineering readiness fails the boundary test even if the recommendation sounds plausible.
4. If Phase A is sound, obtain only Anhar's real answer and preserve it as the Human product decision. Do not treat a synthetic Human answer as project authority. Then **switch Phase B target authority** to Kencleng `pilot/3-clean-delivery-baseline@3767569144d1b00145574450f1127a4f9690b859` plus that Human decision. Evaluate selected-slice readiness against the real neutral engineering substrate for missing product decisions, dependency truthfulness, proportionality, already-settled engineering constraints, and a reconstructable handoff. Do not import historical feature implementation or Pilot #2 sequencing merely because Git history remains reachable.
5. Record exact Kencleng/Harscode revisions, prompts, Anhar's decision, context switch, observed failures/corrections, and Human effort before judging the candidate. Phase B may produce a readiness verdict and bounded handoff, but it does not authorize engineering by itself; Anhar separately authorizes engineering after the readiness result.

**Separate verification-only check.** The QA-only entry-contract gap is real at document level but need not block this clean-seed product handoff trial. Test it later on an existing implementation with approved behavior and an observable interface, not on the code-free seed. Preserve independent evidence and no-production-fix boundaries; do not manufacture a Techplan/Build report just to satisfy the current Testing prompt.

## Roadmap and checklist

### 0. Freeze Pilot #2 evidence baseline — COMPLETE

- **Objective:** establish a reconstructable snapshot and claim limits.
- **Inputs/evidence:** the exact revisions and Kencleng state, report, inventory, Work Graph, Events, and Run anchors above.
- **Decision:** distinguish inventory and self-report from runtime verdicts; name what remains unmeasured.
- **Exit criteria:** exact refs and selected anchors verified; HOLD, milestones, gates, and evidence gaps explicit without changing Kencleng.
- **Output:** the frozen evidence index and limits above.
- [x] Locate the HOLD record, evaluation, inventory, and repository revisions.
- [x] Verify exact refs/anchors and record evidence gaps.
- [x] Make the baseline reconstructable by a fresh session without chat history.

### 1. Separate necessary assurance cost from avoidable workflow cost — COMPLETE

- **Objective:** identify the leading root causes without discarding the assurance that found real defects.
- **Inputs/evidence:** Stage 0 and sampled Reviews, Build, Testing, report repair, status-only work, and state projections.
- **Decision:** four episode-scoped causes above; confidence in mechanism is distinct from unknown cost magnitude.
- **Exit criteria:** each cause has concrete anchors, a counterexample or limit, and an observable test; no unmeasured savings claim.
- **Output:** ranked cause map and assurance floor above.
- [x] Classify a critical-path sample rather than treating artifact count as cost.
- [x] Record four causes, confidence, limits, test ideas, and the assurance floor.

### 2. Settle Harscode identity and positioning — COMPLETE FOR THIS EPISODE

- **Objective:** state the primary value, Human/Orchestrator posture, and modular applicability.
- **Inputs/evidence:** Stages 0–1; current `README.md`, `orchestration/protocol-v0.1.md`, `workflow/AGENTS.md`, and `product-design/README.md`; Anhar's discussion and decision.
- **Decision:** the one-sentence positioning and three values above, owned by Anhar for this evaluation episode.
- **Exit criteria:** Human and project authority remain clear; backend-only and cross-functional delivery fit the wording; verification-only remains an explicit current-fit question.
- **Output:** the settled episode positioning above, with no silent change to operational or candidate runtime guidance.
- [x] Test the framing against bounded and cross-functional scopes and the Pilot #2 counterexample.
- [x] Record Anhar's wording and scope decision; keep implementation fit for Stage 3.

### 3. Audit lifecycle and artifacts against outcomes — IN PROGRESS

- **Objective:** assess each handoff and artifact by the capability, assurance, and reconstructability it provides.
- **Inputs/evidence:** Stages 0–2 and actual Pilot #2 artifacts; current owners for product/design handoff, Exploration, Techplan, Review, Build, Testing, Work Unit, Run, Participant Profile, Invocation, and Orchestration; Kencleng `pilot/3-clean-seed@54ded3b` for Phase A product isolation and `pilot/3-clean-delivery-baseline@3767569` for Phase B readiness / later real delivery.
- **Decisions:** keep, refine, remove, or make conditional by concern; distinguish semantic and authority needs from storage or tooling choices.
- **Exit criteria:** each concern has its purpose, cost, observed failure, necessary evidence/gate, and a bounded simplification candidate. Include a verification-only applicability check.
- **Output:** the first-pass outcome matrix and Pilot #3 preparation hypothesis above; no protected or canonical edits. Closure still requires targeted validation.
- [x] Audit product-to-engineering boundary, Exploration, Techplan, Review, Build, and Testing at first-pass resolution, including verification-only fit.
- [x] Audit Work Unit, Run, Participant Profile, Invocation, and Orchestration at first-pass resolution.
- [x] Desk-check the clean-seed boundary and a verification-only counterexample against current guidance; record limits without treating the checks as executed pilot evidence.
- [x] Prepare a bounded product-to-engineering handoff candidate and two-context fresh-context trial protocol without changing runtime guidance or choosing a Kencleng slice.
- [ ] Run Phase A fresh-context product-boundary trial, continue with Anhar's real decision into Phase B clean-delivery readiness, and refine/close the matrix only on observed evidence.

### 4. Design a minimal Harscode vNext candidate — PENDING

- **Objective:** address proven causes with the smallest sufficient changes while preserving the assurance floor.
- **Inputs/evidence:** Stage 2 positioning and Stage 3 audit matrix.
- **Decisions:** candidate semantics, non-goals, authority owners, reversibility, and which changes require governed proposals or protected approval.
- **Exit criteria:** each change has a causal rationale, expected effect, safeguard, observable test, and fallback; no framework without a demonstrated need.
- **Output:** bounded candidate guidance/proposals in their owning areas, linked by exact revision here.
- [ ] Select minimal changes and map owners/gates.
- [ ] Check consistency with operational `main` and target-project authority.

### 5. Run bounded CRTV with explicit measures — PENDING

- **Objective:** test an authorized candidate on real work with a scope that is comparable where possible.
- **Inputs/evidence:** frozen Harscode candidate revision, Stage 0 historical baseline, Anhar-selected Pilot #3 bounded outcome, exact Kencleng clean-delivery baseline, and required independent verification. The clean seed is Phase A isolation input, not the real delivery target.
- **Decisions:** predeclare scope, stop conditions, and feasible measures without building a telemetry platform.
- **Exit criteria:** observe capability and safety/authority evidence; record coordination effort, re-entry reasons, missed prerequisites, duplicated work, first-pass completeness, and scope/data limitations.
- **Output:** an exact-revision CRTV report comparing outcomes and cost, without arbitrary document-count or savings thresholds.
- [ ] Predeclare scope, measures, assurance floor, and stop conditions.
- [ ] Execute only after applicable Pilot #3 authorization and collect evidence; this does not resume Pilot #2.

### 6. Keep / Refine / Reject — PENDING

- **Objective:** judge each candidate change by CRTV results.
- **Inputs/evidence:** Stage 5 report, deviations, regressions, and independent findings.
- **Decisions:** keep, refine, or reject each change with confidence and unresolved risk.
- **Exit criteria:** each decision names observed effects, downside, and evidence limits; material refinement returns to bounded CRTV.
- **Output:** decision record and exact accepted or rejected candidate revision.
- [ ] Decide each change without treating a hypothesis as proven.

### 7. Make a promotion decision — PENDING

- **Objective:** decide whether any candidate change belongs on `main`.
- **Inputs/evidence:** Stage 6 decisions, authority/compatibility review, current `main` and pilot revisions, and outstanding risks.
- **Decisions:** Anhar chooses promotion, partial promotion, or deferral/rejection, including scope and governed merge order.
- **Exit criteria:** an explicit decision names exact changes, assurance evidence, containment/fallback, and unresolved items; no silent promotion.
- **Output:** a promotion decision record here; operational status changes only through a separately authorized action.
- [ ] Present the promotion case and residual risks for Human decision.
- [ ] Record the decision and exact revisions; execute promotion only if authorized.

## Parked until semantics are settled

- `workspace.harscode.dev` and public documentation/productization.
- Graph/memory management.
- A large tooling or automation framework.

Reopen an item only if new evidence shows it is necessary for correctness or operability in this episode, or after relevant Stage 2–4 semantics are settled. Record the reason before changing scope.

## Decision record

| Date | Class | Decision / status | Evidence and owner |
|---|---|---|---|
| 2026-10-05 | Working decision | HOLD Kencleng Slice 2 development; evaluate Post-Pilot #2; do not promote now. | Anhar; Kencleng tracker at `8b9a050`. |
| 2026-10-05 | Evaluation baseline | Freeze Stage 0 at Harscode `63ec4e0` / `main@b64fa11` and Kencleng `8b9a050`; read the inventory as a pre-report `7e731f9`-plus-working-tree snapshot. | Exact refs, selected anchors, hashes, and limits above; no policy or resume decision. |
| 2026-10-05 | Working diagnosis | Prioritize the four Stage 1 causes while preserving the assurance floor. | Kencleng `8b9a050` report and sampled Runs; current pilot `orchestration/run-contract.md`. No measured causal savings or canonical change. |
| 2026-10-05 | Settled episode decision | Adopt the Stage 2 positioning and three values above; keep Harscode repository prose in professional English. | Anhar's discussion in this session. This settles the evaluation lens, not operational or candidate runtime policy. |
| 2026-10-06 | Working decision | Prepare Pilot #3 from approved upstream product/design authority without importing Pilot #2 delivery context; derive release scope and slices anew with Anhar. | Anhar; frozen Phase A Kencleng seed `pilot/3-clean-seed@54ded3b`. No Pilot #2 resume or engineering authorization. |
| 2026-10-06 | Working decision | Use Kencleng `pilot/3-clean-delivery-baseline@3767569` as the real Pilot #3 delivery target, preserving neutral engineering substrate while resetting active delivery scope/contracts/feature assumptions. Keep `pilot/3-clean-seed@54ded3b` frozen as Phase A product-isolation input. | Anhar; clean-delivery baseline is forward from Kencleng `main@e32916b` and was accepted after minimum mechanical verification in the current session. |
| 2026-10-06 | Working decision | Use a two-context Pilot #3 progression: Phase A clean-seed product-boundary trial → real Anhar product decision → Phase B readiness on the exact clean-delivery baseline → separate Human engineering authorization. | Anhar; this changes the evaluation/trial contract only, not Harscode runtime guidance or `main`. |
| 2026-10-06 | Working evaluation | Record the Stage 3 first-pass matrix and bounded product-to-engineering handoff hypothesis; keep canonical and candidate runtime guidance unchanged pending validation. | Current Harscode guidance and Kencleng `8b9a050` evaluation; no measured per-mechanism cost or causal improvement claim. |