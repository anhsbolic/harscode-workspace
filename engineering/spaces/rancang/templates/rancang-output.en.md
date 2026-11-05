# Template — Rancang Engineering Solution Output & Consumer Handoff (English)

> **Standing:** A4 RESEARCH AUTHORING TEMPLATE / DRAFT FOR HUMAN REVIEW (2026-11-05). Optional reusable authoring aid; **not** approved Space formation, a project-accepted Engineering Solution, canonical API/database schema, runtime evidence, or write permission.
> **Contract:** [Rancang I/P/O/O](../contracts.md) · [Coordination & independent concerns](../coordination.md) · [Artifact representation](../artifacts/README.md). Other language: [Bahasa Indonesia](rancang-output.id.md).
> **Semantic basis:** [Approved Rancang experiment (immutable)](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/rancang-engineering-solution.md): **13 inputs, 10 iterative processes, 8 logical outputs, 6 desired qualities**.
> **Use:** One bounded solution artifact **or a navigable index of actual project-owned sources**. O01–O08 are semantic coverage, **not eight mandatory files or empty sections**. The receiving project's effective standards and consumer-required formats take precedence.

## How to use and quality floor

- **Start from real consumers:** identify the exact assignment, accepted Product/UX/Engineering authority, technical constraints, intended frontend/backend/data/integration implementers, delegated freedoms and acceptance. Do not duplicate binding upstream information into a competing master source.
- **Check sufficiency before binding:** inspect relevant I01–I13. Accepted UX Flow O2 is required by default for new/material UX; accepted Lo-Fi O6 is required by default for new/material screen/surface UX, with legitimate exact-revision equivalents or scoped evidenced exceptions. **Hi-Fi is not a default Rancang input.**
- **Coverage is not a paperwork quota:** use `N/A — scoped reason` for genuinely irrelevant meaning and `OPEN/BLOCKED — owner and affected decision/consumer` for material gaps. Bounded technical hypotheses may support exploration but not binding consumer claims.
- **Architect owns substantive O01–O07**, Requirements Analyst protects original-source fidelity, UX/Experience and Security independently inspect the originals relevant to their concerns and own their own findings, and an independent Solution Reviewer assesses whole-solution fitness. **Coordinator owns O08** and cannot rewrite producer decisions or independent findings.
- **Keep proof claims distinct:** `PROPOSED`, `HUMAN-ACCEPTED (separate exact-revision evidence)`, `CANONICAL ADOPTED`, `NOT RUN`, `CHECKED` and `INDEPENDENCE UNVERIFIED` are different states of evidence. Filling this template never constitutes approval.
- **Choose representation by consumer:** Markdown and tables for decision meaning; diagrams (e.g., Mermaid) for material components/ordering/states; **complete proposed OpenAPI/AsyncAPI/schema/other effective project format** when a real consumer needs machine-readable O03. No mandatory REST/ORM/database/diagram choice.
- **Keep accepted bytes intact:** record Human acceptance separately against the exact reviewed blob/commit and scope. Do not insert SHA/APPROVED into an accepted artifact and infer the earlier approval transferred.

## 0. Identity, authority, scope & input sufficiency — required for binding consumption

| Field | Actual value and exact source |
| --- | --- |
| Target project / repository / branch / inspected baseline | `<actual project-owned path + immutable revision>` |
| Distinct Rancang assignment ID and bounded intended outcome | `<...>` |
| Actual Human instruction, authorized scope and output destination | `<reference; actions/tool writes separately authorized>` |
| Legitimate Engineering Solution decision owner / delegation | `<...>` |
| Intended implementers/consumers and decisions they must make | `<functional owners, scope, actual input contract>` |
| Effective Product Contract and exact approval | `<source/revision/scope or explicitly NON-BINDING hypothesis>` |
| Effective UX O2 Flow, O6 Lo-Fi and relevant O3/O4/O5/O7 | `<accepted source/equivalent, owner-backed scoped exception, or BLOCKED>` |
| Engineering Project Standards and actual stack | `<effective project sources, material owner gap; no mandatory formal catalog>` |
| Security/privacy, material NFRs and current technical baseline | `<effective project source/revision and observed code>` |
| Existing API/database/provider contracts and implementation baseline | `<canonical vs proposed standing, exact revisions, real availability>` |
| Exclusions, delegated Engineering freedom and material unknowns | `<...>` |
| Solution artifact/index and substantive revision(s) | `<exact persisted revision or NOT YET PERSISTED>` |
| Solution standing | `PROPOSED / HUMAN-ACCEPTED only with separate exact-reviewed content evidence` |
| Binding information sufficiency | `SUFFICIENT / CONDITIONAL / BLOCKED + affected decision and owner` |

### Input coverage register — I01–I13 (decision-specific; not 13 documents)

| Input ID | Actual source / revision / standing or N/A evidence | Material affected O-ID/consumer | Missing owner decision |
| --- | --- | --- | --- |
| **I01 Product Contract** | `<...>` | `<...>` | `<...>` |
| **I02 UX Flow Diagram** | `<accepted UX O2/equivalent/exception>` | `<...>` | `<...>` |
| **I03 Lo-Fi Wireframes** | `<accepted UX O6/equivalent/exception>` | `<...>` | `<...>` |
| **I04 IA & Navigation** | `<...>` | `<...>` | `<...>` |
| **I05 Interaction & UI States** | `<...>` | `<...>` | `<...>` |
| **I06 Existing Codebase & Architecture** | `<...>` | `<...>` | `<...>` |
| **I07 Engineering Standards & Stack** | `<...>` | `<...>` | `<...>` |
| **I08 Security & Privacy Requirements** | `<...>` | `<...>` | `<...>` |
| **I09 Existing API & DB Schema** | `<...>` | `<...>` | `<...>` |
| **I10 Integration Requirements** | `<...>` | `<...>` | `<...>` |
| **I11 Material Non-Functional Requirements** | `<...>` | `<...>` | `<...>` |
| **I12 Test & Acceptance Scenarios** | `<...>` | `<...>` | `<...>` |
| **I13 Technical Research / PoC** | `<existing evidence / bounded research / N/A>` | `<...>` | `<...>` |

Do not call a required but unresolved input N/A. Hypothesized Product meaning cannot become an approved business rule. UX owns webpage navigation; Rancang owns delegated technical/API design.

## O01 — Engineering Solution Blueprint

**Bounded technical outcome and relevant invariants:** `<accepted Product requirement references, not invented policy>`.

| Component / system boundary | Responsibility and authoritative data/state | Input/output, integration and data-flow dependencies | Deployment and operational constraints | Decision source / standing |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

| Material architecture decision | Actual stack/NFR/PoC feasibility evidence | Alternative and cost/failure trade-off | Selected/deferred rationale | Affected O-ID and consumer |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<PROPOSED / owner decision>` | `<...>` |

**Architecture/sequence/dependency diagram (conditional):** `<actual artifact path and revision, represented question; or N/A with reason>`.

**Unresolved feasibility constraints:** `<material performance/availability/reliability/operations/integration uncertainty, owner, blocked consumer decision>`.

## O02 — Authentication & Authorization Design

**Applicability:** `APPLICABLE / N/A — reason and scope`.

| Principal / credential / session context | Identity and attribution source | Resource permission, grant/revoke lifecycle | Trusted enforcement point / boundary | Denied, expired, replay or compromise behavior | Accepted Product/Security source |
| --- | --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Session/token/identity-provider/service-to-service trust where material:** `<mechanism, validation, expiry/rotation, evidence and assumptions; no invented runtime guarantee>`.

Product retains domain role/eligibility meaning; Engineering defines technical enforcement. Hiding a UI control is not authorization. Separately owned independent Security findings are linked at O08, not substituted for AuthN/AuthZ design.

## O03 — API Contract / shared interface

**Actual consumers and effective project interface format:** `<HTTP/OpenAPI, event/AsyncAPI, RPC, internal typed contract, other + exact effective format version>`.

| Operation/event ID and producer | Endpoint/topic/operation if applicable | Request fields, types, requiredness and validation | Response/success and error/denied/unknown/partial | Principal/auth, concurrency/idempotency/effect guarantees | Compatibility/version and consumers |
| --- | --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Conditional complete machine-readable interface:** `<proposed artifact path + exact revision / NOT REQUIRED with real consumer-based reason / BLOCKED and owner>`.

- When an **actual shared consumer** needs a typed contract, supply a **complete and deterministic scoped proposal**, including actual field names/types/requiredness, status/result variants, auth, errors, and effective project format. A prose endpoint inventory is not enough.
- State guarantees a schema cannot encode as **normative and checkable obligations**, linked to O05/O07: authorization, ordering, atomicity, retries/idempotency, ambiguous network outcomes, state ownership and versions when material.
- Engineering owns proposed technical/API routes; UX owns accepted **webpage** routes. A Rancang API proposal is not canonical adoption or proof of live provider behavior.

**Provider or integration gaps and rightful owner:** `<...>`.

## O04 — Data Model & Database Design

**Applicability:** `APPLICABLE / N/A — scoped reason`.

| Entity/resource and source of truth | Relationships, ownership and lifecycle | Fields, uniqueness/integrity constraints and invariants | Persistence/access boundary | Existing schema and migration/compatibility impact |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

| Material mutation / Product invariant | Transaction/atomicity and isolation/consistency guarantee | Race/duplicate/uniqueness protection | Recovery or partial failure behavior | O03/O05/O07 references |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Typed schema/model/diagram artifact (conditional):** `<exact path/revision or N/A>`. Apply actual project data standards; this proposal does not grant permission to perform migrations or adopt canonical schemas.

## O05 — State & Error Handling Design

| Technical state/trigger and authoritative owner | Preconditions and transition/side effects | Success, denied, error, partial or **unknown** meaning | Retry/idempotency/concurrency and recovery | Truthful UX state and O03/O07 references |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Response-lost / unknown completion contract:** `<how consumer distinguishes confirmed outcome from unknown, supported reconciliation/retry if actually designed, unresolved owner gaps>`.

**Timing/state diagram (conditional):** `<actual source and revision / N/A>`. Do not invent UX screens, backend recovery operations or success proof to complete a diagram.

## O06 — Security Design (Architect-authored)

**Effective protection/security/privacy floor:** `<actual accepted requirements, exact source and trust boundaries>`.

| Asset/principal, trust boundary, threat/abuse path | Architect-owned safeguard, enforcement mechanism and owner | Privacy/data/logging/cache/secrets implications | Negative behavior and O07 check | Residual assumption/risk and independently owned Security finding |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

Security Analyst must independently read applicable originals and assess the exact Architect-authored controls. **Do not write independent Security findings as the Architect**. Feasibility affects the selection among safe controls, never the binding security floor. Legitimate security/Human authority is required for material risk acceptance.

**Independent Security findings and exact revision:** `<separate owner-owned source / NOT CHECKED or INDEPENDENCE UNVERIFIED if applicable>`.

## O07 — Technical Verification Specification

**These are required testable *design obligations*, not evidence that tests have run.**

| Case ID + accepted SC/REQ/AC | O-ID and invariant/security/NFR guarantee | Preconditions, scenario and positive/negative/race/unknown path | Observable expected result **and falsifier** | Future verification owner/method/environment | Actual executed evidence or `NOT RUN` |
| --- | --- | --- | --- | --- | --- |
| `VER-01` | `<...>` | `<...>` | `<...>` | `<...>` | `NOT RUN / actual command, revision and observed result` |

**Coverage challenge:** `<material success/denial/resource-boundary/session/atomicity/duplicate/retry/lost-response/concurrency/recovery/provider/NFR cases, plus evidenced N/A and gaps>`.

Run only tests/tools allowed by the target project's effective SOP and Human permissions. Test planning does not prove implementation, penetration testing, real integration, uptime, or Human QA acceptance.

## O08 — Engineering Solution Handoff (Coordinator-owned)

**Single effective consumer entrypoint:** `<project-owned recoverable path, exact revision; no competing master output>`.

| Output | Original producer and exact effective revision | Applicability and standing | Independently owned finding/disposition link | Consumer restriction / adoption dependency |
| --- | --- | --- | --- | --- |
| O01 Blueprint | `<Architect revision>` | `<...>` | `<...>` | `<...>` |
| O02 AuthN/AuthZ | `<Architect revision>` | `<...>` | `<...>` | `<...>` |
| O03 API | `<Architect and typed contract when required>` | `<...>` | `<...>` | `<...>` |
| O04 Data/DB | `<Architect revision or evidenced N/A>` | `<...>` | `<...>` | `<...>` |
| O05 State/Error | `<Architect revision>` | `<...>` | `<...>` | `<...>` |
| O06 Security Design | `<Architect revision>` | `<...>` | `<separate Security findings>` | `<...>` |
| O07 Verification Spec | `<Architect revision>` | `<...>` | `<...>` | `<...>` |

**Separate owner-controlled assessment artifacts (do not rewrite their conclusions):**

| Concern | Independent/source-access facts and accountable assessor | Exact finding revision, severity and affected O-ID | Producer disposition and changed-edge re-review | Evidence limits |
| --- | --- | --- | --- | --- |
| Requirements/authority fidelity | `<...>` | `<...>` | `<...>` | `<...>` |
| UX / Experience integrity | `<...>` | `<...>` | `<...>` | `<...>` |
| Independent Security | `<...>` | `<...>` | `<...>` | `<...>` |
| Independent Solution review | `<...>` | `<...>` | `<...>` | `<...>` |

**Human-facing decision summary:** `<bounded result, reasons, major technical/UX/security/cost trade-offs, decisions still needed>`.

| Blocked output/consumer | Missing binding evidence/authority or conflicting original | Legitimate owner | Work still safe / held claims | Next exact action |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Human acceptance of exact substantive solution:** `PENDING / separate actual decision record, exact reviewed revision and accepted scope`. A filled template or reviewer endorsement is not Human approval.

## Six quality outcomes — decision-specific design evidence

| Experiment quality | Material evidence with exact O-ID/source | Risk, unverified proof or affected consumer |
| --- | --- | --- |
| **Feasible** | `<real technical/NFR/cost/dependency evidence; O01>` | `<...>` |
| **Secure** | `<O02/O06 authored controls and independent Security findings>` | `<...>` |
| **Consistent** | `<Product invariants, O03/O04/O05 and O07 falsifiers>` | `<...>` |
| **Reliable** | `<O05 failure/retry/unknown, O07, operational NFR>` | `<...>` |
| **Implementable** | `<unambiguous O01–O07 for actual known implementers>` | `<...>` |
| **Verifiable** | `<O07 cases, future verification owner and actual evidence limits>` | `<...>` |

These are **desired design properties**, not measured deployment quality, provider conformance, penetration testing or delivered actor outcomes.

## Consumer handoff & decision-specific sufficiency — required

| Actual functional consumer and implementation decision | Required O-ID and **effective project-owned originals** | Typed interface/DB/verification representation needs | Generic declared receiver contract fit | Real project-bound fit, source standing and blocked edge |
| --- | --- | --- | --- | --- |
| `<actual frontend/backend/data/integration/verification consumer>` | `<...>` | `<...>` | `<SUFFICIENT / CONDITIONAL / BLOCKED / NOT APPLICABLE>` | `<SUFFICIENT / CONDITIONAL / BLOCKED / UNVERIFIED + evidence>` |

**Scoped documentary production completion:** `COMPLETE / PARTIAL / BLOCKED / FAILED — scope and evidence`.

**Checks not actually performed:** `<missing source access, independence, consumer proof, live provider/environment, permitted runtime/testing>`.

**What this does NOT prove or authorize:** `<Human acceptance, canonical API/DB adoption, real code or migrations, protected writes, real provider integration, test PASS, deployment, security certification or delivered Product value>`.

**Next legitimate owner/action:** `<...>`.

**Consumer readiness rule:** A well-written narrative is **insufficient** if an actual implementer must invent a material field, permission, data invariant, transaction boundary, error/unknown behavior, security control or verification condition. Fix/hold that consumer edge; do not claim readiness merely because every section was filled in.
