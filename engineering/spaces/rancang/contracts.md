# Rancang — External Input / Process / Output / Outcome Contract

> **Standing:** A4 ZERO-BASED NEW FORMATION CANDIDATE / NOT FORMATION APPROVED (2026-11-05). The [approved experiment](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/rancang-engineering-solution.md) is the semantic target, not runtime or target-project authority.
> **Owners:** Architect produces technical solution; Coordinator owns external contract/joins; Requirements, UX and Security retain independent concern lenses, and Solution Reviewer assesses cross-output fitness.

## 1. INPUT — 13 information obligations, not thirteen required files

| ID | Input from approved experiment | Decision-specific sufficiency / legitimate source |
| --- | --- | --- |
| **I01** | Product Contract | Accepted consequential Product invariants, permissions/roles, behavior and observable acceptance at exact owned revision. Product hypotheses support only labeled exploration, not binding decisions. |
| **I02** | UX Flow Diagram | Relevant accepted UX O2 flow for new/material UX by default; exact accepted equivalent or justified owning UX exception permitted. |
| **I03** | Lo-Fi Wireframes | Relevant accepted UX O6 structural evidence for new/material screen/surface UX by default; inspect, do **not author** as Rancang. Equivalent/non-applicability must be legitimate and evidenced. |
| **I04** | Information Architecture & Navigation | Effective UX IA, navigation, page/path versus UI state and relevant web route decisions; Design owns webpage paths, not Architect. |
| **I05** | Interaction & UI State Requirements | Effective UX O7 interaction, validation, loading, denial, error, unknown and recovery obligations, with accepted Product truth. |
| **I06** | Existing Codebase & System Architecture | Relevant actual code, stack, deployed boundaries and technical constraints for an existing project; label freshness/limits. |
| **I07** | Engineering Standards & Technology Stack | Effective and sufficiently specified project-level stack/technical rules; use [Engineering Project Standards concern](../../project-standard/README.md) to resolve material reusable gaps, not create an empty catalog. |
| **I08** | Security & Privacy Requirements | Independently inspected owning security/privacy/trust constraints, privileges, protection floors and actual risks; Engineering cost does not weaken binding safeguards. |
| **I09** | Existing API Contracts & Database Schema | Current canonical/proposed API/data contracts, persistence/schema, compatibility and ownership evidence **when available/material**. |
| **I10** | Integration Requirements | Actual external identity/services, provider/consumer semantics, failures, dependencies and versions when relevant. |
| **I11** | Non-Functional Requirements | Material performance, availability, reliability, scalability, operability, observability and cost constraints; no invented thresholds. |
| **I12** | Test & Acceptance Scenarios | Current accepted positive, negative, security, concurrency, recovery and edge obligations; differentiate proposed verification from performed results. |
| **I13** | Technical Research / PoC | Existing feasibility evidence or proportionate investigation when material technical uncertainty exists; never a universal PoC gate. |

**Acquisition:** Original project/Human/Design/technical sources can supply multiple inputs. No mandatory named upstream Space, fixed PRD/TRD, file count or sequential stage. Technical-only/non-screen work may legitimately omit screen UX with evidence; new/material UX has accepted O2 and O6 required-by-default coverage (or accepted equivalents/evidence-backed exceptions). **Hi-Fi is not a required/default Rancang input**. When actual accepted Hi-Fi constraints materially affect the solution, consume the relevant explicit requirements; do not require Figma/image/browser tooling.

**Input disposition:** `SUFFICIENT` for the decision, `CONDITIONAL` for bounded explicitly provisional technical exploration, `BLOCKED` where missing external authority would be invented, `NOT APPLICABLE` for genuinely irrelevant inputs. Coordinator and Requirements Analyst cite exact project source/standing; independent UX and Security specialists re-read originals relevant to their concerns. A work ID permits authorized discovery only. Missing Engineering mechanisms require investigation, not reflexive upstream refusal; only affected binding decisions are held.

## 2. PROCESS — 10 iterative Engineering activities

| ID | Experiment process | Accountability and necessary reasoning |
| --- | --- | --- |
| **P01** | Requirements Analysis | Requirements & Authority Analyst traces accepted original → binding Engineering obligation, negative cases, constraints, freedom and gaps; Architect checks consumer impact. |
| **P02** | Technical Feasibility Analysis | Architect inspects stack/code/NFR/operations, compares materially different mechanisms and records evidence-backed feasibility, cost, residual uncertainty and fallbacks. |
| **P03** | Solution Architecture Design | Architect resolves components, boundaries, state/data owners, integration and data flows without inventing Product or UX choices. |
| **P04** | Authentication & Authorization Design | Architect specifies actual identity/session/attribution/permissions and enforcement where material; Security independently establishes trust and misuse risks, challenges early. |
| **P05** | API & Data Design | Architect authors implementable operations, API representation, model/constraints, transaction/invariant guarantees and compatibility; does not adopt canonical contracts. |
| **P06** | State, Failure & Recovery Design | Architect decides positive/negative/unknown, concurrency/retry/idempotency/recovery; UX independently validates actor-visible truth early. |
| **P07** | Security & Risk Analysis | Architect **authors security controls**; independent Security Analyst investigates threats and issues separately owned findings; producer remedies, assessor rechecks. |
| **P08** | Verification Planning | Architect creates checkable specs; Requirements, UX and Security independently challenge relevant gaps and negative paths; planned checks are not PASS. |
| **P09** | Solution Review & Refinement | Independent Solution Reviewer inspects originals, applicable O01–O07 and Security/UX findings; Architect repairs; material changed edges re-reviewed. |
| **P10** | Engineering Handoff & Human Acceptance | Coordinator joins exact effective sources, outputs, reviews, intended consumer fit and Human decision request; Human accepts only explicitly reviewed exact bundle. |

The order is **not linear**. UX/Experience and Security concern knowledge must inform decisions before architecture selection hardens. Security can challenge feasibility framing; Architect must supply a safe viable alternative or precise unresolved blocker. No required consensus vote or process state machine.

## 3. OUTPUT — eight logical Engineering Solution results

| ID | Logical output | Required implementation-consumable meaning and owner |
| --- | --- | --- |
| **O01** | Engineering Solution Blueprint | **Architect:** relevant components, architecture, deployment/data flow, integrations, feasibility rationale, NFR/operational constraints and significant alternatives. |
| **O02** | Authentication & Authorization Design | **Architect:** principals/identity/session, attribution, permissions/resource ownership, grants/revocation, trusted enforcement points and material denied/replay/expired-session paths. Independently challenged by Security. |
| **O03** | API Contract | **Architect:** consumer-critical operations/events, request/response and requiredness, authorization, success/error/denied/unknown, idempotency, version/compatibility. If actual shared consumers need machine-readable, deliver a **complete deterministic proposed typed contract** in their effective project format plus normative non-schema guarantees; prose-only may be used only if sufficient for real consumers. Canonical adoption belongs downstream. |
| **O04** | Data Model & Database Design | **Architect:** material entities/relations, ownership, uniqueness/integrity constraints, persistence lifecycle, transactions, atomicity/concurrency, migration/compatibility, and explicit N/A for non-persistent work. |
| **O05** | State & Error Handling Design | **Architect:** authoritative state/transition owners, validation, errors, denial, unknown/partial, retries, idempotency, recovery/observability, and user-visible implications consistent with UX/Product. |
| **O06** | Security Design | **Architect authors** implementable trust/protection/authorization/data safeguards and threat-linked controls. **Security Analyst separately assesses** them with risk, limitations and required change. Assessment is not the security design. |
| **O07** | Technical Verification Specification | **Architect is accountable:** observable positive/negative/security/concurrency/reliability/recovery cases, falsifiers, future verification owner/environment, trace to accepted obligations and evidence state `NOT RUN` unless actually performed with permission. |
| **O08** | Engineering Solution Handoff | **Coordinator:** one effective exact-revision solution package/index containing O01–O07, legitimate sources/standing, separately owned UX/Security/Solution findings and dispositions, limits, known consumer checks, exact Human approval status and next permitted action. |

These are **logical outputs**, not eight mandatory files or a requirement to manufacture irrelevant sections. A meaningful `NOT APPLICABLE` needs reason; material gaps are `BLOCKED`/`PARTIAL` rather than invented designs. A requirements trace can support O01–O07 internally, but legacy `X1/O1–O5` is **not** the current external taxonomy. Every substantive output has one accountable producer and exact version, including Security findings separately authored from proposed controls.

## 4. OUTCOME — six design qualities and evidence floor

| Quality | Minimum defensible *design* evidence (not runtime success) |
| --- | --- |
| **Feasible** | Real technical constraints, NFR/stack/dependency feasibility, proportionate cost/risk/trade-offs and unresolved uncertainty disposition. |
| **Secure** | Binding safeguards preserved in O02/O06, independent material threat review and risk/mitigation record; no security self-approval. |
| **Consistent** | Accepted Product invariants traced to O03/O04/O05 state, permission and transaction boundaries, with O07 falsifiers. Atomicity is required when accepted invariant demands it, not universally. |
| **Reliable** | Material failure/retry/concurrency/unknown/recovery semantics, availability and operational risks addressed with checkable conditions. |
| **Implementable** | Actual known implementers need not invent incompatible interface, identity, data, state, security or integration decisions; proposed vs adopted source status explicit. |
| **Verifiable** | Material guarantees have observable cases, owners, coverage/limits and actual `NOT RUN` vs executed evidence. |

These qualities are **target outcomes**; a coherent design does not prove deployed behavior, independent user research, penetration testing, API provider readiness or release acceptance.

## 5. Known consumer handoff, incompatibility and completion claims

For each actual intended consumer, check (1) **generic input-type/meaning/standing compatibility** if it has a declared contract and (2) **project-bound fit** against real current project source, accepted constraints, security/SOP, expected interface format and scope. Unknown/unformed future consumers are `NOT CHECKED`, not fictional PASS. If a consumer needs typed O03, a readable but incomplete prose list is **not** documentarily ready.

Distinguish `PROPOSED ENGINEERING SOLUTION`, `HUMAN-ACCEPTED exact bundle`, `CANONICAL API/DB CONTRACT ADOPTED`, `IMPLEMENTATION VERIFIED` and `DELIVERED ACTOR OUTCOME`. They are separate events/authorities.

- `COMPLETE` means all **applicable design production** and required independent assessment obligations are satisfactorily fulfilled and no material unresolved decision defeats the scoped known consumer-critical claim; still not automatic Human acceptance or implementation evidence.
- `PARTIAL` means usable bounded design work exists but applicable outputs, reviews or evidence remain incomplete; exact blocked edges and owners are explicit.
- `BLOCKED` means a material external authority/security/permission/consumer-critical contract prevents the dependent binding design; safe independent work can continue.
- `FAILED` means attempted scoped design production did not produce its required meaningful result.
- `UNVERIFIED` qualifies missing actual assurance/permission/runtime evidence; it never converts a missing obligation to PASS.

Human approval of a new Space formation does not grant task invocation; Human acceptance of O08 does not authorize canonical spec edits, protected writes, implementation, tests, migration or deployment. Missing independent security/reviewer context where materially required prohibits the corresponding **independent** assurance claim.

## 6. Hard authority boundaries

- [Engineering Project Standards](../../project-standard/definition.md) owns reusable project-wide technical rule governance. Rancang may identify a concrete gap or candidate but **cannot automatically approve/write** project standards; local delegated solution decisions stay local. Project technical authority never overrides higher-priority privacy/security protection.
- Product owns actor/domain meaning and invariants; UX owns webpage routes, interaction flow, IA, Lo-Fi and states. Rancang may specify backend API paths and implementation constraints but cannot change accepted web navigation or Product semantics unilaterally.
- Security owns independently grounded risk assessment, **not** the Architect's chosen safe mechanism, and does not accept risk without owning Human authority. Engineering feasibility is not a reason to weaken protection.
- No feature code/migrations, canonical feature contract mutation, environment setup, Harness installation/certification, global Orchestration, new schedule/registry, downstream implementation/release or fabricated independent/actual tests.
- For technical unknowns within Engineering authority, investigate with proportional evidence. For missing material Product/UX/project-standard authority, return the exact blocked decision and owning source to Human without sending automatic upstream dispatch.
