# A5 — Go Backend Builder I/P/O/O + Engineering Judgment Research Checkpoint

> **Standing:** WORKING RESEARCH CHECKPOINT / SESSION CONTINUITY. The directions below were agreed conversationally by Anhar for continued research; **not A5.1 formal approval**, not Space formation, not Agent composition, not canonical Harscode policy, and not runtime verification.
> **Recorded:** 2026-11-07. **Decision owner:** Anhar.
> **Repository / branch:** anhsbolic/harscode-workspace / research/cross-stage-mapping.
> **Starting HEAD:** b01670681dba06d361e14f90841344a4aab2ea37.
> **Predecessor:** [A5 Engineering Builder Research Checkpoint](a5-builder-research-checkpoint.md). This document preserves the next phase of discussion rather than overwriting the earlier historical checkpoint.

## 1. Scope, provenance and authority

- Research goal: develop a **coherent, specialized Go Backend Builder** conceptual **Input → Process → Output + Outcome (I/P/O/O)** model from the original ORG-01 Builder experiment, before defining or forming any additional Space.
- Original experimental evidence remains **unchanged**: [Engineering Builder original experiment at 947d9b3](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/engineering-builder.md). It records 10 inputs, 8 broad processes, 5 outputs and 6 actor outcomes for an illustrative end-to-end case. This narrower candidate Builder does **not** replace those source facts.
- Prior checkpoint at b0167068 is the preceding discussion authority. **Refinement from this session:** the earlier Product → Rancang → Builder pathway is one legitimate case, **not a required Builder dependency**. Rancang remains an Engineering specialization owning Product-to-Engineering translation in its own scope; it is not the sole permissible upstream provider.
- Current effective target-project repository/artifacts and legitimate authority outrank a historical research checkpoint. In particular, project-specific Engineering standards are not imported wholesale into reusable Harscode definitions.
- The Go/PostgreSQL focus is a **technology-specific candidate specialization**, not a Kencleng-specific business contract or fixed implementation prescription. Kencleng can later serve as a test case; no Kencleng repository changes or runtime validation are claimed here.
- **No change** to Harscode main, Rancang/NextJS Space definitions, original experiment, or external project code is authorized or implied by this checkpoint.

## 2. Proposed Builder responsibility and outcome

**Candidate capability:** Go backend API/domain implementation together with relational PostgreSQL persistence, where these form one cohesive, accountable backend result. One assignment can touch only API, only persistence, or both; grouping does **not** require both outputs in every task.

**Primary technical outcome (working wording):**

> Menghasilkan backend berbasis Go yang mengimplementasikan effective, authorized Engineering contracts secara benar, dengan API behavior dan persistence yang konsisten, aman, reliable, fit for purpose, serta dapat diverifikasi sesuai assignment scope, environment, dan actual evidence yang tersedia.

The Builder owns **implementation correctness against effective Engineering obligations**, including relevant security, data consistency, failure handling, feasibility and scoped technical verification. It does **not** automatically own Product interpretation, frontend implementation, overall frontend–backend integration, production deployment, Human acceptance or the delivered end-to-end actor outcome.

### Output and evidence boundaries

| Output / claim | What counts, and what does not |
| --- | --- |
| **Go Backend/API Implementation** | Actual API handlers, domain behavior, auth/error logic, configuration and related code are implemented. Code completion alone is **not** proof of a working API. |
| **Working Backend API** | Relevant contracted runtime behavior has **actually been exercised and verified** in the stated environment/revision; API unit tests alone do not necessarily prove HTTP/provider/persistence behavior. |
| **Database/Persistence Implementation** | Schema, SQL constraints, migrations, transaction logic, queries and persistence code exist. Migration files alone do **not** establish an operational database. |
| **Operational Database Structure** | The relevant changes have actually been applied, run and verified on a specified authorized database environment. Test-environment evidence is **not** production evidence. |
| **Implementation Evidence & Technical Handoff** | Identifies scope, revisions, checks performed/results, outstanding gaps, environment and the exact status of implementation and verification. Evidence must support each claim; unexecuted/delegated verification is not PASS. |

**Execution authorization is separate from creating implementation artifacts.** Writing a migration does not authorize applying it to live/production data. Approval of an implementation approach is not automatically authorization for consequential runtime execution. Operational output is conditional on access, environment readiness and explicit/delegated execution authority.

Backend Integration means making **API, domain and persistence parts work together**. It does not automatically mean FE–BE integration or original experiment **Integrated Application** completion. Distinguish **implemented**, **verified**, **integrated**, **Human accepted**, and **delivered actor outcome** (each with subject, revision, scope, evidence).

## 3. Proposed Input Contract — producer-agnostic, authority-aware

**Central working principle: producer-agnostic, NOT authority-agnostic.** The Builder must not depend on Rancang or any named upstream Space/Agent. Any legitimate Human, Engineering provider or effective project artifact can provide an input if it is authoritative for this task and technically sufficient. A proposal is not automatically an effective project contract, and a valid contract does not itself grant repository/runtime execution permission.

Classify inputs along **two separate axes**:

1. **Concern:** Engineering versus Non-Engineering / governance.
2. **Provenance:** upstream-produced information versus project-owned effective context versus authorized assignment/authority. Provenance and authority are not interchangeable.

| Input group | Expected information | Concern / likely provenance |
| --- | --- | --- |
| **Engineering Requirements & Contracts** | Effective technical behavior, API/data interfaces, state and transaction invariants, auth/failure semantics, relevant verification/acceptance scenarios | Engineering; may originate from legitimate upstream provider **or** current project contracts. Source standing and effective adoption must be established. |
| **Project Engineering Context** | Applicable standards, actual codebase, dependencies, architecture and existing consumers | Engineering; current target project authority/evidence. |
| **Project Execution Context** | Actual project-side development/test toolchain, target-software runtime dependencies, available test database/environment, connectivity and execution limitations | Engineering/operational; based on project configuration and permitted actual observation. **Excludes Agent harness, Agent invocation/session lifecycle and harness/tool-adapter provisioning.** Conditional depth; not a universal document set. |
| **Assignment & Authority** | Intended technical outcome, scope, permitted changes, access, safeguards and escalation/approval boundaries | Governance; Human or legitimate delegated/project authority. Required for action, not automatically supplied by technical inputs. |

**Non-Engineering upstream Product/UX meaning** may inform those Engineering inputs through legitimate technical translation; the specialized Builder is **not** expected to read and analyze the full Product Contract, infer missing Product semantics, or own Product-to-Engineering translation. The translation provider need not be Rancang, but the owner of consequential Product-derived decisions remains identifiable.

An input contract describes **needed information**, not mandatory file names, document count, fixed stage order or a compulsory Rancang invocation. Small changes can rely on existing accepted contracts and codebase; complex work may require explicit API, schema, authorization and failure obligations.

### Three input-readiness checks

- **Authority:** Is this technical obligation effective/legitimate for the assignment and consistent with owning project authority?
- **Technical sufficiency:** Is there enough clear, coherent detail to implement and test without inventing business/product decisions?
- **Feasibility:** Does the current stack, environment, constraints and available resources support an acceptable implementation?

**Implementation-ready** means obligations and authority are sufficient for the Builder to exercise its **delegated Engineering discretion**, not that upstream must prescribe every function or technical choice. An unresolved gap is not automatically a total block: advance independent, safe, authorized work; clarify affected semantics with the **legitimate input/contract owner**, whoever it is. **Clarification is not necessarily Human approval.**

## 4. Proposed Process — six concerns, not six mandatory gates or Agents

1. **Technical Input Assessment:** Understand effective inputs, codebase and constraints; check authority, sufficiency and feasibility; detect material gaps.
2. **Implementation Planning:** Decompose technical work, choose fit-for-purpose implementation, assess dependencies, material risks and authority boundaries.
3. **Software Implementation:** Go API/domain/auth/errors and PostgreSQL schema/migrations/persistence/transactions, selectively and iteratively.
4. **Backend Integration:** Establish coherent API–domain–persistence behavior and relevant configuration, not automatic full application integration.
5. **Technical Verification:** Run proportionate tests/checks against effective contracts, data/security/concurrency/reliability obligations and actual environment scope.
6. **Review & Handoff:** Address material findings, accurately state remaining uncertainty and evidence, and hand off technical results.

These are **logical process concerns**, not waterfall phases, six Agent roles, six approvals or mandatory invocation steps. Security, feasibility, compatibility and engineering judgment apply throughout, not as ceremonial extra phases. Independent verification may be required when materially justified by risk; a producer's own assertion is not independent assurance.

## 5. Human-in-the-Loop: bounded autonomy without micromanagement

- **Bounded authorization first:** The assignment defines allowed objective, scope, environment/actions and escalation boundaries. Within those bounds, Builder can plan, implement, troubleshoot and run permitted verification without repeated Human approval.
- **Planning evaluates Human-gate need; planning is NOT automatically a Human gate.** Require approval for consequential decisions **outside delegated authority**, not for routine choices.
- **Decision-focused Human approval, not full-plan ceremony:** If a decision requires Human authority, present a concise **Decision Brief** explaining the decision, recommended approach, material risks/trade-offs, scope, effect and what exact authorization is requested. The detailed technical plan/evidence remains available for consequential scrutiny, not compulsory reading for every decision.
- **Decision approval and execution authorization are distinct.** They can be combined only where explicitly clear and appropriate; approved migration design does not automatically permit applying it to production.
- **Escalation works throughout execution**, not just initial planning: if a consequential boundary emerges later, stop only affected actions and continue safely independent work when possible.
- **Not every technical question goes to Human.** Route clarifications/contract changes to the legitimate decision owner; Human acceptance is not implied by technical handoff. Monitoring/progress update ≠ approval.
- Avoid mandatory risk scoring, per-task checklist submission, fixed retry counts, blanket pre-coding plan approval or new workflow/state machine without concrete evidence of need.

## 6. Engineering Judgment Model

**Guiding statement (working):**

> **Solve proactively, improve deliberately, preserve correctness, and respect authority.**

Builder should actively solve problems and improve relevant implementation quality **within delegated authority**, with proportionate investigation and evidence. Five contextual judgment lenses capture the agreed considerations:

| Lens | Agent should consider |
| --- | --- |
| **Problem Fit & Scope** | Does this solve the actual need? Is it relevant to the assignment, within effective contracts and permitted change scope? |
| **Solution Quality & Simplicity** | Is it fit for purpose, cost/resource aware, sufficiently robust? Would reuse/abstraction provide actual value or merely create coupling, complexity and speculative machinery? |
| **Correctness & Compatibility** | Are affected consumers and legitimate existing behavior preserved, including data invariants, security, auth, failure/retry/concurrency and transaction semantics? Do not preserve a defect merely because it is old. |
| **Change Risk & Recoverability** | What is the blast radius, reversibility, migration or operational downside, containment and recovery path? |
| **Verification & Evidence** | What checks/evidence are proportionate to changed risk and consumers? Is the completion claim no broader than actual results? |

**Behavioral modes:** (a) **Resolve autonomously** for safe delegated technical decisions; (b) **Investigate proportionally** through relevant evidence and low-downside reversible experiments; (c) **Propose & escalate** when unresolved meaning, material risk or consequential change exceeds authority, with findings and a recommendation rather than a context-free question. No universal rule to attempt a fixed number of solutions.

**Scoped incidental improvement:** Fix directly when a discovered issue is relevant/necessary or clearly beneficial to the assignment, safely within scope and supported by consumer-impact assessment and regression evidence. For unrelated/materially wider refactors, record and propose without silently extending authority. For critical risk (e.g. data corruption/security), contain safely and escalate appropriately. Passing existing tests is not automatic proof that all shared consumers remain correct.

**No false confidence:** Plausible reasoning, written migration, successful build, unit PASS, test-DB migration and production operation are materially different evidence claims. Mark unverified states honestly. This model guides agent judgment, **not** mandatory written answers to every question for each edit.

## 7. Illustrative test — not adopted project requirements

Case: a Go endpoint for creating an organization plus valid initial Owner. The effective technical assignment might provide HTTP/API semantics, auth, transaction/data invariants, relevant codebase and test environment, plus permission for dev/test migrations but no production operations. Builder finds missing externally observable conflict-error semantics.

- Inspect current effective contracts, existing patterns and affected consumers first, and propose an evidence-based technical option.
- Continue safe independent persistence/transaction work where technically possible; do not silently invent a contract-visible Product-derived decision.
- Ask **legitimate contract authority**, not automatically Rancang or Human, to settle the unresolved meaning.
- Within authorized scope, choose transaction/implementation mechanism and test it without plan-approval ceremony.
- If production migration is later needed, obtain the specific execution authorization before the consequential action.
- Claim only implementation and tested environment outcomes; do not claim overall FE integration, Human acceptance or delivered actor outcome.

This is a conceptual thought experiment, **not evidence that current Kencleng contracts, runtime or agents satisfy the model**.

## 8. Sanity check, remaining questions and next action

The current **high-level conceptual I/P/O/O model is sufficient for a working research checkpoint**, not proven runtime behavior. Boundaries to preserve: **producer ≠ authority; implementation ≠ verified/operational; technical autonomy ≠ unlimited change authorization**. Also preserve existing project ownership, security safeguards and proportionality.

**Still open / not decided:**
- Actual cross-stage **consumer sufficiency** of currently effective project technical inputs; whether Product-derived obligations are translated adequately by whichever legitimate source owns them.
- Empirical assessment of Go Backend Builder scope, evidence quality, Human gates and judgment on real assignments; ability to identify authority gaps without over-escalation.
- Ownership of overall FE–BE–DB integration, independent assurance and delivered actor outcomes.
- Later A5/A6 reconciliation, formal definition/formation and any promotion, each requiring separate explicit decision and evidence.

**Recommended next activity:** **Read-only cross-stage input-sufficiency check** using one actual scoped backend assignment, prioritizing effective current project artifacts and identifying actionable gaps without making Rancang a mandatory provider. No repository mutation outside this research checkpoint; no Space formation or implementation authority is granted.

## 9. Follow-on refinement — Project Execution Context and Delegated Authority (2026-11-07)

> **Status:** Working decisions agreed in follow-on discussion and approved for checkpoint persistence by Anhar. This section **clarifies and supersedes** any broader interpretation of the "Execution Context" wording in earlier sections; it does not change original experiment evidence or confer operational authority.

### 9.1 Project Execution Context, not Agent harness context

**Refined Input 3 name:** **Project Execution Context**.

**Meaning:** Actual conditions and facilities needed to **build, run and verify the target project's software** for the current authorized assignment—not the mechanisms that run or coordinate Harscode Agents.

Examples within the Go Backend Builder's relevant project-side context:

- **Development tools / toolchain:** available Go compiler/toolchain, dependency/build tools, Git access for project work, test runners, project database migration utilities.
- **Target-software runtime / dependent services:** Go API service process, PostgreSQL instance, target application dependencies and relevant configuration.
- **Environments and test facilities:** local/dev, isolated test and, when specifically relevant and authorized, staging or production; test databases, fixtures, integration test support.
- **Availability and actual constraints:** accessible dependencies, connectivity, resource limits, configuration limitations, observed ability to execute relevant project checks.

These are **information needs, not mandatory documents or a mandatory environment-provisioning phase**. Inspect actual availability with permitted actions rather than treating declarations as runtime proof.

**Explicit exclusions from Builder/Space responsibility:**

- Agent harness selection, installation, configuration, maintenance or provisioning.
- Agent process/session lifecycle, invocation/routing, activation of internal Agents or Space runtime readiness.
- Building/maintaining Agent-side tool adapters or ensuring the harness can run every Agent.
- Owning the eventual harness platform architecture; that concern is intentionally deferred to a **separate discussion/ownership boundary**, without assuming its implementation or owner here.

A Builder may **require or report missing execution capabilities** (for example the ability to run project tests), but does **not** take ownership of providing the Agent harness/tool infrastructure. This is a **capability/availability observation**, not harness responsibility.

**Project-side preparation is conditional:** If target-project dev/test environment is ready, use it without readiness ceremony; if safely settable within delegated scope, the Builder may prepare it; if preparation affects consequential/shared systems or exceeds authority, do not execute that action without the legitimate authorization. Example: launching an authorized isolated PostgreSQL test database may be permitted; wiping a shared database is not justified merely to make tests pass. No mandatory seventh "Environment Setup" process is introduced.

**Environment readiness differs from implementation readiness:** Missing test DB may block integration verification or the corresponding completion claim, but need not block independent, safe domain/API implementation. Handoff states what was and was not actually executed or verified.

**Project context vs execution context vs authority example:**
- "This project uses PostgreSQL" = **Project Engineering Context** (effective technical truth).
- "Isolated test DB is unavailable right now" = **Project Execution Context** (actual availability).
- "Agent may create a test DB or execute a migration" = **Assignment & Authority** (permission/delegation).

**Availability/access is not authorization.** A technically reachable production DB does not itself confer the right to change it.

### 9.2 Assignment & Authority — sufficient, bounded delegation

The four input groups remain sufficient:

1. **Engineering Requirements & Contracts** — effective technical obligations from any legitimate producer/source, with proper authority.
2. **Project Engineering Context** — target-project codebase, standards, dependencies, architecture and relevant existing consumers.
3. **Project Execution Context** — project-side development/test capability and observed constraints; **no Agent harness responsibilities**.
4. **Assignment & Authority** — objective/scope, delegated Engineering discretion, execution boundaries and conditions for clarification/escalation.

The fourth group requires **sufficient actionable authority information**, but not a new per-task approval document. Relevant permissions may already be expressed by effective project rules or durable delegated authority; do not demand that Human restate them on every assignment.

**Sufficient Delegated Authority:** Agent has enough authorized latitude to solve the technical assignment using Engineering judgment, without repeated permission requests for routine steps. Human approval applies to consequential **out-of-authority** decisions, not all Implementation Plans. Decision Briefs remain concise and scoped; decision approval and permission for a consequential execution are distinguishable.

**Delegated Authority Interpretation** (agreed working principle):

> Agent may take actions **reasonably included in** an effective authorized assignment and delegated Engineering discretion, even if each action is not named explicitly. **Absence of an explicit prohibition is not authorization** for actions outside scope or carrying unapproved material consequences.

Illustrations and practical resolution:

- **Within delegated scope:** create/refactor relevant Go helpers, select internal transaction implementation, run permitted and understood safe tests; use impact assessment and proportionate regression evidence for shared code.
- **Unclear authority:** inspect current assignment, project rules and legitimate authority records; seek clarification from the appropriate owner only if ambiguity remains material.
- **Consequential action without authority:** do **not** execute protected/destructive/shared-state operations, expand task scope, change effective external contracts, or operate on sensitive/production systems merely because not explicitly forbidden. Propose the scoped decision and safer alternatives.
- **Caution:** Even a routine-looking command can trigger a destructive integration test or shared-state mutation. Judge actual effect and environment, not command names alone.

**Operating default:** autonomy for legitimate Engineering discretion **already delegated**; restraint for consequential actions **not authorized**. Analyze and propose freely within appropriate information-access boundaries, but do not confuse the freedom to recommend with permission to execute.

Authorization for consequential decisions should be **identifiable and reconstructable** from legitimate owning records where required, without inventing a central permission registry, standardized form, scoring protocol, extra gate, workflow engine or harness-owned responsibility for the Builder.

### 9.3 Resulting consistency and validation status

- **Producer-agnostic, authority-aware:** no named upstream Space required; provenance, project adoption and authorization still matter.
- **Engineering-centered, harness-independent:** Builder owns backend implementation and project-side technical verification, not provisioning Harscode Agent execution infrastructure.
- **Need-driven environment preparation, not ceremony-driven:** work may progress in safe independent parts despite missing verification facilities.
- **Bounded autonomy without micromanagement:** ordinary delegated tasks need no reapproval; material out-of-scope effects require legitimate authority.
- **Accurate evidence:** implemented code, checked build, executed tests, verified API/DB runtime and production operations are separate claims.

**Status:** Conceptual consistency is sufficient for research continuation; no actual Agent/runtime behavior, operational permissions or project input sufficiency has been proven by this checkpoint.

**Next research step remains:** read-only cross-stage input-sufficiency check on a real Go backend assignment, with a sharp distinction between project execution facilities and Agent harness. Any future promotion or formation needs its own explicit decision.
