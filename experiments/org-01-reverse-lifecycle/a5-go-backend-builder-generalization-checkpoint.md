# A5 — Generalized Go Backend Builder I/P/O/O — Research Checkpoint

> **Standing:** WORKING RESEARCH / DISCUSSION CONTINUITY (agreed direction, **not** formal A5 approval, Harscode operational policy, formed Space, Agent composition, or runtime-proven behavior).
> **Decision owner:** Anhar. **Recorded:** 2026-11-07.
> **Repository:** \`anhsbolic/harscode-workspace\` · **Branch:** \`research/cross-stage-mapping\` · **Starting HEAD:** \`cadfd2219e88cc8cf9c017a20c9e4dc9942a5403\`.
> **Purpose:** Preserve the material shift from the initial API/PostgreSQL-centered Go Backend Builder candidate to a **general-purpose Go backend engineering specialization**, without losing traceability to the original I/P/O/O experiment or prematurely designing skillsets, Agents, harness mechanisms, or project-specific execution.
>
> **Predecessors:** [Initial A5 research checkpoint](a5-builder-research-checkpoint.md) and [Go Backend Builder I/P/O/O + Engineering Judgment checkpoint](a5-go-backend-builder-ipoo-research-checkpoint.md) (latter at commit \`cadfd2219e88cc8cf9c017a20c9e4dc9942a5403\`). **This follow-on checkpoint refines their generalized-scope interpretation; it does not rewrite their historical decisions.**

## 1. Source authority and methodological boundary

The immutable [ORG-01 Engineering / Builder experiment](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/engineering-builder.md) (commit \`947d9b361bd4cdf07d3aeebffb4a27eaf18da49a\`, blob \`22f88376a1b9912ee54c3a6b462245a7c0f2003f\`) is **WORKING EXPERIMENT SNAPSHOT**, not generalized or runtime-verified policy.

- Original illustrative **10 inputs**: Product Contract; UX Flow/Interaction Spec; Hi-Fi UI Design; Engineering Solution Design; API Contract; Data Model/Database Schema; Existing Codebase & Technical Standards; Test & Acceptance Scenarios; conditional Design System and Web Assets.
- Original **8 processes**: Input Review; Implementation Planning; Frontend Development; Backend Development; Database Implementation; Integration; Testing & Verification; Review & Handoff.
- Original **5 outputs**: Functional Web UI; Working Backend API; Operational Database Structure; Integrated Application; Test & Verification Results.
- Original **6 actor outcomes** are specific to organization formation: start; understand consequences; authenticate/submit; organization and valid first Owner created together; inspect durable relationship; truthful failure/uncertain response.

**Correction to preserve:** the original ORG-01 experiment is **not itself a technology skillset specification**. It is an *end-to-end, case-specific I/P/O/O description* that includes frontend, backend and database. The current research **derives a narrower-responsibility but broader-technology reusable Go backend Builder** from that experimental evidence. Kafka, GraphQL, Redis, S3, etc. were **not validated by the original experiment**; they are proposed generalization domains grounded in recognized backend concerns.

The original actor outcomes are **not replaced** by a specialized Builder outcome; Go Backend Builder contributes only its authorized technical part. No direct full Product analysis requirement is silently reintroduced.

## 2. Key agreed direction: stable responsibility, adaptable competence

**Strong working recommendation accepted in discussion:**

> **Stable responsibility model, adaptable technical competencies.**
>
> I/P/O/O defines **what Go Backend Builder is accountable for**. Technical capabilities and specialized skillsets support **how the Process is performed**, selected for the effective project and bounded assignment; they do not determine the identity of the Space, force a fixed tech stack, or mandate an Agent per technology.

The earlier Go API + PostgreSQL grouping remains a **valid specific example**, not the permanent scope of reusable Go Backend Builder. In particular:

- Go is the defining implementation specialization; **REST is not the only interface**, and **PostgreSQL is not the only database**.
- Relevant backend software can include REST, GraphQL, gRPC, WebSocket, domain/application operations, persistence, caching/ephemeral state, messaging/event processing, background workers, object storage and backend-facing external systems.
- Examples of conditional technologies: PostgreSQL vs MySQL; Redis vs no cache; Kafka, RabbitMQ or no broker; S3-compatible storage such as MinIO. These are **examples, not a mandatory stack, proven capability, or technology catalog that must be implemented now**.
- The effective **target project** establishes stack choices, versions, standards and architectural constraints; the **assignment** determines which of those capabilities actually matter for this work.
- A general Go Builder must continue to grow based on actual project needs, with meaningful competence/quality standards; building the complete speculative catalog up front would add complexity without evidence.
- Specialization of expertise does **not** imply a 1:1 correspondence between skillset, Agent, Space, process, or output. Do not infer one PostgreSQL Agent, Kafka Agent, etc. simply because the technologies differ.
- **Focus/selective applicability** matters: unrelated skillsets should not become obligatory knowledge, work, prompts, steps or approvals for every Agent execution. We have **not chosen a skill-loading/runtime/harness mechanism**.

### Three distinct notions, not three runtime layers

1. **Core Go/backend Engineering competence:** idiomatic Go and cross-cutting technical judgment that support backend work.
2. **Conditional specialized capabilities and technology expertise:** API styles, database engines, messaging, storage, caching, async processing, specialized performance work, etc., only when relevant.
3. **Project/assignment applicability and authority:** effective choices/constraints and exact permitted work; not themselves reusable skills.

A specialized knowledge source teaches mechanisms, trade-offs, failure modes and verification; it must **not override** effective project contracts, standards, or Human authorization.

## 3. Generalized Go Backend Builder I/P/O/O — current working target

This is a **conceptual target**, not a final canonical Space definition. Keep the four already-agreed input groups and six logical process concerns. **Generalize primarily Outputs/Outcome** without weakening technical accountability.

### INPUT — four information groups, not four required documents

| Group | General requirement | Standing / boundary |
| --- | --- | --- |
| **I1. Engineering Requirements & Contracts** | Sufficient effective technical obligations (behavior, interfaces, data/state/invariants, identity/authorization, failure/recovery, acceptance/verification requirements as applicable) | **Producer-agnostic, authority-aware**. Can originate from any legitimate upstream or current project source. An input producer is not automatically the contract authority; Rancang is not a required upstream dependency. |
| **I2. Project Engineering Context** | Actual codebase, effective architecture/standards, dependency and consumer context | Owned by target project; technology and versions are project-specific. No historical/research proposal silently becomes canonical. |
| **I3. Project Execution Context** | Available project-side development/build/test tools, target-app runtime dependencies and environment constraints | May be inspected/prepared **as needed and authorized**. Excludes responsibility for Agent harness, invocation, Agent session lifecycle and harness/tool-adapter provisioning. Availability does not imply authorization. |
| **I4. Assignment & Authority** | Objective, scope, delegated technical discretion, allowed actions/environments and escalation boundaries | Legitimate Human/delegated authority; no universal per-task approval form. Consequential unapproved actions remain disallowed even if not explicitly forbidden. |

Readiness is judged by **authority, technical sufficiency and feasibility**, proportional to the assignment—not a checklist of document titles. The Builder can resolve normal technical ambiguity in delegated discretion; it does not invent Product meaning or silently change accepted cross-boundary contracts. Missing information need not block safe independent work.

### PROCESS — six logical concerns, not six mandatory ordered phases or Agents

1. **Technical Input Assessment:** inspect effective obligations, code/context, applicability, conflicts, gaps and feasibility.
2. **Implementation Planning:** select/decompose adequate Go backend implementation based on actual dependencies, risk, cost, authority and scope; no mandatory Human plan approval.
3. **Software Implementation:** write relevant **Go backend capabilities**—not just REST handlers and PostgreSQL SQL. May encompass backend service interfaces, domain processing, persistence adapters, workers, message handlers, caching integration and storage access as assigned.
4. **Backend Integration:** make relevant backend components and dependencies work coherently (synchronous/asynchronous, local/external); not automatic overall frontend–backend app acceptance, infrastructure/platform operations, or production provisioning.
5. **Technical Verification:** perform risk-proportionate evidence-producing checks of actual contracted behavior, data/security/concurrency/compatibility and relevant integration paths in authorized environments.
6. **Review & Handoff:** account for code/results, regressions, scope, exact checks, material limitations and readiness. Independent assurance is separate when justified.

The processes can be iterative/selective. The previously agreed **Engineering Judgment Model**, **bounded problem-solving autonomy**, **scoped incidental improvement**, **conditional decision-focused Human gates** and **no false evidence claims** remain cross-cutting obligations. They do not become a workflow engine, per-command approval protocol, or fixed Agent sequence.

### OUTPUT — broadened logical categories

| Generalized output | Accountable meaning | Example manifestation (conditional) |
| --- | --- | --- |
| **O1. Implemented Go Backend Capabilities** | Actual authorized backend application/service behavior and technical interfaces that fulfill effective Engineering contracts | HTTP/REST/GraphQL/gRPC handlers, application/domain operations, Go workers or message processors |
| **O2. Relevant Backend Data & System Integrations** | Implemented backend-side interaction with required persistence/storage/cache/message/external capabilities, including consistency, contracts and failure handling | SQL migrations and persistence; Redis integration; S3-compatible object access; Kafka/RabbitMQ clients |
| **O3. Implementation Evidence & Technical Handoff** | Exact scope/revisions, verified checks and outcomes, unverified/blocked items, material findings, applicable environment and remaining risks | Targeted tests, API contract checks, data consistency/integration evidence, honest handoff |

**O1/O2 are logical responsibility groups, not universally required distinct deliverables.** A bounded assignment may deliver only one relevant part, with appropriate evidence. Backend-facing integrations are within Builder scope when assigned; production operation/provisioning of third-party platforms, DB/broker clusters or Agent harness is **not automatic ownership**.

**Output correctness vs claim evidence:** implementation artifacts do not equal tested working services; writing SQL migrations does not equal an operational database; configuring Kafka/S3 clients does not establish working broker/object-store integration; a test environment PASS does not prove production. Original ORG-01 Working Backend API and Operational Database Structure remain **concrete instances** of the broader results. Original end-to-end Integrated Application and actor outcomes require separately accountable integration and acceptance.

### OUTCOME — broadened, still accountable

> **Go Backend Builder menghasilkan Go-based backend capabilities yang mengimplementasikan effective Engineering contracts secara correct, secure, reliable, dan fit for purpose, termasuk relevant backend processing, data/state behavior dan system integrations, dengan verification evidence yang sesuai authorized assignment scope dan actual execution environment.**

The **desired quality** and the **proven completion state** must be separated: an assignment may hand off correct implementation with unperformed verification transparently labeled, but cannot claim verified working or operational outcomes without evidence. This is **technical backend outcome**, not Product meaning translation, Human acceptance, overall integrated-application outcome, or claim of delivered actor journey.

## 4. Initial competency-domain map — subordinate to I/P/O/O

The following is an **initial conceptual audit proposal** (not a final validated industry taxonomy, not a mandatory skillset inventory, not an Agent chart):

**Candidate core foundations (8 areas):**
1. Go language/runtime engineering (idioms, errors, context, concurrency, resource safety).
2. Backend application engineering (domain/application behavior, invariants, validation, ownership boundaries).
3. Service/interface engineering (contracts, request/response and message semantics, compatibility/consumers).
4. Data/state correctness (consistency, atomicity, lifecycle, concurrency and idempotency).
5. Integration and distributed behavior (dependencies, timeout, retry, partial failure and duplicates).
6. Security/trust boundaries (secure coding, authn/authz enforcement, data/secrets protection).
7. Reliability/operability (lifecycle, configuration, observability, performance/resource fit).
8. Testing/verification/maintainability (proportionate evidence, regression safety, maintainable change).

**Candidate conditional domains:** API/communication style; database/persistence; caching/coordination; messaging/event processing; object/file storage; background/async work; advanced backend optimization. Technology-specific knowledge may become applicable when real project requirements call for it.

**Key distinction:** core principles such as consistency, caching trade-offs, or asynchronous failure handling do **not** imply the project must use any database engine, Redis, Kafka or an async worker. Conversely, deep vendor-specific operational/implementation details should not bloat universal core responsibilities.

There is interest in **quality standards for skillsets** (fitness, applicability, failure modes, safeguards, verification and authority), closely related to future Agent competence. However **formal skillset standards, catalog decomposition, loading/selection mechanism, Agent composition and harness design are deliberately postponed**. These are supporting implementation questions, **not the primary structure of the Builder I/P/O/O model**.

## 5. Level-of-abstraction correction

Use the following analytical relationship; this is **not** a stage pipeline or mandatory document chain:

| Level | Purpose | Authority/evidence limit |
| --- | --- | --- |
| **Original ORG-01 experiment** | Concrete end-to-end I/P/O/O example; traceability and inspiration for Builder responsibility | Specific case, research snapshot. Does not prove all generalized tech domains. |
| **Generalized Go Backend Builder I/P/O/O** (**current focus**) | Reusable technical accountability independent of one project's stack or one upstream Space | Working research model; neither Space formation nor runtime proven. |
| **Project + bounded assignment application** | Select relevant standards, technology-specific expertise and permitted work | Future use of the model. Not required to settle the current conceptual contract. |

**Avoid two opposite mistakes:**
- **Too narrow:** define the reusable Builder as permanently "REST API + PostgreSQL Builder", confusing an example project stack with the specialization itself.
- **Too vague:** define the output merely as "some backend software", losing the distinct accountability for implemented behavior, relevant backend integrations, and actual technical verification evidence.

The **I/P/O/O semantic contract is primary**. Skillsets are supporting competencies for Process, **not a competing taxonomy that replaces I/P/O/O**.

## 6. Explicit decisions, unchanged boundaries and deferred work

### Accepted *working direction* (not formal formation approval)

- Maintain a **Go-based backend engineering specialization** broad enough to cover common backend responsibilities and technology variants, selected by relevant project/assignment.
- Keep the **four Input groups and six Process concerns**. Generalize **Output and Outcome** while retaining implementation/evidence and integration accountability.
- Preserve prior safeguards: producer-agnostic but authority-aware inputs; no default Product interpretation; bounded autonomy/HITL; fit-for-purpose Engineering judgment; meaningful verification; no Agent harness responsibility.
- Let expertise expand **on demand**, with future standards of skillset quality, rather than loading/building all possible technology skills upfront.
- Retain original experiment evidence and traceability rather than rewriting its case-specific inputs, process, outputs or actor outcomes.

### Not decided or authorized

- No confirmed exhaustive "common Go backend work" audit, final competency/skillset taxonomy or actual Agent skill-loading design.
- No Agent composition, Space formation, formal A5/A6 finalization, operational promotion or Human approval of an implementable agent runtime model.
- No target-project technology adoption, code modifications, deployment, runtime tests or real-case/cross-stage validation.
- No requirement to execute a Kencleng assignment now; Anhar explicitly paused real-case validation to **focus on conceptual I/P/O/O**.

### Next discussion

**Refine the generalized Go Backend Builder OUTPUT + OUTCOME at the semantic I/P/O/O level first**, checking that categories are broad enough for varied Go backend implementations but specific enough for accountable results. Then perform a concise consistency check against **INPUT + PROCESS**. Only later, in a separate episode, examine detailed skillset quality, Agent composition or real usage evidence.

**No authority conferred by this checkpoint.** It is a durable research discussion record; authoritative project repository decisions and current human-approved scoped constraints remain upstream of implementation permissions.
