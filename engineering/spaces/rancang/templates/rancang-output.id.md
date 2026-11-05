# Template — Rancang Engineering Solution Output & Consumer Handoff (Bahasa Indonesia)

> **Standing:** A4 RESEARCH AUTHORING TEMPLATE / DRAFT FOR HUMAN REVIEW (2026-11-05). Template opsional untuk menghasilkan dan mengevaluasi keluaran Rancang; **bukan** formed Space approval, accepted target-project Engineering Solution, canonical feature API/schema, bukti runtime, atau izin write.
> **Contract:** [Rancang I/P/O/O](../contracts.md) · [Coordination & independent concerns](../coordination.md) · [Artifact representation](../artifacts/README.md). Versi bahasa lain: [English](rancang-output.en.md).
> **Semantic basis:** [Approved Rancang experiment (immutable)](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/rancang-engineering-solution.md): **13 input, 10 proses iteratif, 8 logical output, 6 outcome kualitas**.
> **Use:** Satu bounded solution artifact **atau index ke actual project-owned sources**. O01–O08 adalah coverage yang perlu ditelusuri, **bukan delapan file wajib atau delapan section kosong**. Actual project standards dan declared consumer format menang.

## Cara menggunakan dan quality floor

- **Mulai dari real consumer**: assignment, Product/UX/Engineering authority, accepted revisions, constraints, intended FE/BE/data/integration implementers, delegated freedoms dan acceptance. Jangan mengganti Product, UX atau Engineering Project Standards dengan salinan yang menjadi authority tandingan.
- **Sufficiency sebelum binding**: nilai input I01–I13 sesuai keputusan yang material. Untuk UX baru/material, UX Flow O2 default; untuk material screen UX, Lo-Fi O6 default. Accepted equivalent atau exception memerlukan legitimate UX owner, scope dan evidence. **Hi-Fi bukan input default Rancang.**
- **Cakupan bukan pengisian ritual**: gunakan `N/A — alasan dan scope` untuk benar-benar tidak berlaku; `OPEN/BLOCKED — owner, affected decision/consumer` untuk gap material. Provisional Engineering hypotheses boleh membantu exploratory design tetapi **bukan** sumber binding output.
- **Architect owns substantive O01–O07**; Requirements Analyst memeriksa original-source fidelity; UX/Experience dan Security membaca original yang relevan secara independen dan mengembalikan findings milik mereka; independent Solution Reviewer memeriksa keseluruhan. **Coordinator owns O08**, tidak boleh menulis ulang keputusan producer atau temuan reviewer.
- **Bukti bukan klaim**: `PROPOSED`, `HUMAN-ACCEPTED (separate exact-revision evidence)`, `CANONICAL ADOPTED`, `NOT RUN`, `CHECKED` dan `INDEPENDENCE UNVERIFIED` berarti hal berbeda. Approval tidak tercipta karena template selesai diisi.
- **Pilih representasi berdasarkan konsumsi**: Markdown/tabel untuk informasi keputusan; diagram (mis. Mermaid) jika material untuk komponen/sequence/state; **complete proposed OpenAPI/AsyncAPI/schema/other project format** jika actual consumer membutuhkan machine-readable O03. Tidak ada REST, ORM, database atau diagram default.
- **Jaga accepted bytes**: simpan Human acceptance pada record terpisah dengan reviewed exact blob/commit. Jangan mengedit accepted artifact untuk menyisipkan SHA/APPROVED lalu menganggap prior approval masih berlaku.

## 0. Identity, authority, scope & input sufficiency — wajib untuk binding consumer

| Field | Isian dan exact source |
| --- | --- |
| Target project / repository / branch / inspected baseline | `<actual project-owned path + immutable revision>` |
| Distinct Rancang assignment ID dan bounded outcome | `<...>` |
| Actual Human instruction, authorized scope and output destination | `<reference; tool/write authorization distinct from design acceptance>` |
| Legitimate Engineering Solution decision owner / delegation | `<...>` |
| Intended implementers/consumers and actual decisions they need | `<functional owner, scoped work, actual consumer contract>` |
| Effective Product Contract and exact approval | `<source + revision + decision scope, or explicitly NON-BINDING hypothesis>` |
| Effective UX O2 Flow, O6 Lo-Fi and O3/O4/O5/O7 when relevant | `<exact accepted sources/equivalents, scoped exception with owner/evidence, or BLOCKED>` |
| Engineering Project Standards and stack | `<actual project-owned effective source/standing; material gap owner; absence ≠ automatic blockage>` |
| Security/privacy, applicable NFRs, technical baseline | `<owning sources/versions, real code, project-level requirements>` |
| Existing API/DB/provider contracts and implementation baselines | `<canonical/proposed standing, exact revision, environments as actually observed>` |
| Exclusions, delegated technical freedoms, material unknowns | `<...>` |
| Solution artifact/index and substantive output revision(s) | `<project path + exact persisted revision, or NOT YET PERSISTED>` |
| Current solution standing | `PROPOSED / HUMAN-ACCEPTED only with separate reviewed exact-content evidence` |
| Overall binding sufficiency | `SUFFICIENT / CONDITIONAL / BLOCKED + exact affected decision and owner` |

### Input coverage register — I01–I13 (decision-specific, bukan 13 dokumen)

| Input ID | Source / revision / standing, or N/A evidence | Material consequence or affected O-ID | Open decision / rightful owner |
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
| **I13 Technical Research / PoC** | `<existing evidence / targeted investigation / N/A>` | `<...>` | `<...>` |

Jangan menjadikan N/A jalan pintas untuk input material yang belum diterima. Product hypothesis tidak boleh diam-diam mengunci konsekuensi domain. Project UX menentukan webpage navigation; Rancang menentukan delegated technical/API mechanisms.

## O01 — Engineering Solution Blueprint

**Bounded system outcome dan relevant invariants:** `<accepted Product requirement refs, bukan Product rule baru>`

| Component / system boundary | Responsibility dan authoritative data/state | Input/output, integration dan data-flow dependencies | Deployment/operational constraints | Decision source / standing |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

| Material architectural decision | Feasibility evidence (actual code/stack/NFR/PoC) | Alternative dan cost/failure trade-off | Chosen/deferred rationale | Affected O-ID / consumer |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<PROPOSED / owner decision required>` | `<...>` |

**Diagram/sequence/dependency evidence (conditional):** `<actual source + revision + what is represented; N/A with reason>`.

**Material feasibility constraints and unresolved gaps:** `<performance/reliability/availability/scale/operability/integration, owner and affected implementation decision>`.

## O02 — Authentication & Authorization Design

**Applicability:** `APPLICABLE / N/A — reason and scope`.

| Principal / credential / session context | Identity and attribution source | Resource and permission decision, grant/revoke lifecycle | Trusted enforcement point / trust boundary | Denied, expired, replay or compromised path | Accepted Product/Security source |
| --- | --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Session, token, identity-provider and service-to-service trust (when material):** `<mechanism, validation, lifetime/rotation and assumptions; no invented platform guarantee>`.

**Separation of authority:** Product owns domain role/eligibility semantics; Engineering owns technical enforcement. UI hiding a control does **not** enforce authorization. Security Analyst's independent findings are linked under O08, not substituted for O02 design.

## O03 — API Contract / shared interface design

**Actual consumer(s) & accepted project contract format:** `<HTTP/OpenAPI, event/AsyncAPI, RPC, internal typed interface, other; exact version>`.

| Operation/event ID and owner | Endpoint/topic/operation (if applicable) | Request: fields, types, requiredness, validation | Response/success, errors, denied/unknown/partial | Principal/auth, concurrency/idempotency/side-effect guarantees | Compatibility/version and consumer |
| --- | --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Conditional complete machine-readable artifact:** `<exact proposed typed contract path + immutable revision / NOT REQUIRED with actual consumer-specific reason / BLOCKED + owner>`.

- When a **known shared consumer** requires typed contract, the referenced proposal must be *deterministic and complete for the scoped operations*: actual field/type/requiredness, result variants, auth, response/status/error semantics and project format. A table of endpoints alone does not satisfy that consumer.
- Define guarantees a schema cannot encode as **normative, checkable rules** linked to O05/O07: ordering, atomicity, replay/idempotency, unauthorized results, ambiguous network failure, state ownership and version compatibility where relevant.
- API route/operation design belongs to Engineering; UX owns accepted **webpage** routes. A proposed API schema is not the canonical adopted API/DB contract or proof of a live provider.

**Unresolved producer/provider joins and ownership:** `<...>`.

## O04 — Data Model & Database Design

**Applicability:** `APPLICABLE / N/A — reason and scope`.

| Entity/resource and source of truth | Relationships, ownership and lifecycle | Fields/constraints/uniqueness and invariants | Persistence/access boundary | Existing schema / migration & compatibility |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

| Material state mutation / Product invariant | Transaction/atomicity and isolation/consistency guarantee | Concurrency, uniqueness and duplicate protection | Recovery/partial-failure consequence | O03/O05/O07 links |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Schema/model diagram or typed representation (conditional):** `<exact source/revision or N/A>`. Preserve effective project data conventions. A Rancang proposal does not authorize actual migrations or canonical schema updates.

## O05 — State & Error Handling Design

| Technical state / trigger and authoritative owner | Preconditions and transition / side effects | Success, denied, error, partial or **unknown** result semantics | Retry/idempotency/concurrency and recovery | Truthful actor-facing UX O7/O03/O07 link |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Result-loss / uncertain completion contract:** `<how a caller distinguishes observed confirmation from unknown; supported reconciliation/retry if actually provided; otherwise explicit gap>`.

**Time-order or state diagram (conditional):** `<path + exact revision / N/A>`. Do not invent UX screen decisions, successful actions or live backend recovery endpoints to complete the table.

## O06 — Security Design (Architect-authored)

**Effective security/privacy floor:** `<actual applicable sources/revisions and threat boundaries>`.

| Asset/principal, trust boundary, threat or abuse path | Architect-owned protection mechanism and enforcement owner | Data/privacy/logging/caching/secret requirements | Failure/negative case and O07 check | Residual assumption/risk and independent Security finding ref |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

Security Analyst must independently inspect applicable originals and authored design, raise separately owned findings and recheck changed edges. **Do not author Security findings in Architect's voice**. Feasibility can choose between compliant controls; it cannot waive the binding security floor. Risk acceptance requires legitimate owner/Human authority.

**Independent Security Findings source and exact revision:** `<separately owned record, NOT CHECKED / INDEPENDENCE UNVERIFIED if actual separation not proven>`.

## O07 — Technical Verification Specification

**This is a verification *specification*, not a claim that Engineering tests already ran.**

| Case ID + accepted SC/REQ/AC | Tested O-ID / invariant / security/NFR guarantee | Trigger, setup, positive/negative/concurrent or unknown path | Observable expected result **and falsifier** | Future verification owner/method/environment | Actual executed evidence or `NOT RUN` |
| --- | --- | --- | --- | --- | --- |
| `VER-01` | `<...>` | `<...>` | `<...>` | `<...>` | `NOT RUN / executed command + revision + observed result` |

**Coverage challenge:** `<material success, denied, resource-crossing, permission/session failure, data integrity/atomicity, duplicate/retry, lost response, concurrency, recovery, interoperability and NFR cases as applicable; explicit N/A/gaps>`.

Test/tool invocation follows actual target-project SOP and Human permission. A written scenario is **not** test execution, security penetration evidence, production reliability or manual QA acceptance.

## O08 — Engineering Solution Handoff (Coordinator-owned)

**One effective consumer-facing entrypoint:** `<actual target-project path/index, exact revision when persisted, no rival authoritative copy>`.

| Output/source | Producer and original effective revision | Applicability and standing | Independent finding/disposition link | Consumer-specific gap / approval dependency |
| --- | --- | --- | --- | --- |
| O01 Blueprint | `<Architect revision>` | `<...>` | `<...>` | `<...>` |
| O02 AuthN/AuthZ | `<Architect revision>` | `<...>` | `<...>` | `<...>` |
| O03 API | `<Architect + typed contract ref if needed>` | `<...>` | `<...>` | `<...>` |
| O04 Data/DB | `<Architect revision or justified N/A>` | `<...>` | `<...>` | `<...>` |
| O05 State/Error | `<Architect revision>` | `<...>` | `<...>` | `<...>` |
| O06 Security Design | `<Architect revision>` | `<...>` | `<separate Security-owned exact findings>` | `<...>` |
| O07 Verification Spec | `<Architect revision>` | `<...>` | `<...>` | `<...>` |

**Separately owned review records (do not rewrite their conclusions):**

| Concern | Reviewer identity / original-source access and independence evidence | Exact findings revision, severity and affected O-ID | Producer disposition / changed-edge re-review | Evidence limits |
| --- | --- | --- | --- | --- |
| Requirements/authority fidelity | `<...>` | `<...>` | `<...>` | `<...>` |
| UX / Experience integrity | `<...>` | `<...>` | `<...>` | `<...>` |
| Independent Security assessment | `<...>` | `<...>` | `<...>` | `<...>` |
| Independent Solution review | `<...>` | `<...>` | `<...>` | `<...>` |

**Human-facing decision summary:** `<bounded solution result; major choices and cost/security/experience consequences; what has been resolved; what needs exact Human decision>`.

**Unresolved binding decisions, risks or dependencies:**

| Affected output/consumer | Missing decision/evidence or conflicting original | Legitimate owner | Safe independent work / held claim | Next exact action |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Human acceptance of exact substantive handoff:** `PENDING / real separate decision record + reviewed immutable revision + exact accepted scope`. Do not write `APPROVED` solely because Coordinator or an Agent completed a form.

## Six quality outcomes — decision-specific design assessment

| Quality from experiment | Material evidence at exact O-ID/source | Risk, unverified proof or blocked consumer |
| --- | --- | --- |
| **Feasible** | `<actual technical/NFR/cost/dependency basis, O01>` | `<...>` |
| **Secure** | `<O02/O06 controls + separate Security findings>` | `<...>` |
| **Consistent** | `<accepted invariant + O03/O04/O05 + O07>` | `<...>` |
| **Reliable** | `<O05 failure/retry/unknown + O07, material operational NFR>` | `<...>` |
| **Implementable** | `<real consumer-critical O01–O07 semantics, exact artifacts>` | `<...>` |
| **Verifiable** | `<O07 observable conditions and future test owner>` | `<...>` |

These are **desired design qualities**, not observed deployment, provider conformance, security audit certification or delivered actor value.

## Consumer handoff & decision-specific sufficiency — wajib

| Actual intended functional consumer / implementation decision | Applicable O-ID and **exact effective project originals** | Typed interface/DB/verification format required | Generic receiving contract check (if declared) | Real project-bound compatibility, standing and blocked edge |
| --- | --- | --- | --- | --- |
| `<frontend, backend, data, integration, independent verification, etc. only when real>` | `<...>` | `<...>` | `<SUFFICIENT / CONDITIONAL / BLOCKED / NOT APPLICABLE>` | `<SUFFICIENT / CONDITIONAL / BLOCKED / UNVERIFIED + evidence>` |

**Assignment/documentary completion:** `COMPLETE / PARTIAL / BLOCKED / FAILED — exact scope and why`.

**Evidence not actually checked:** `<original-source limits, independence limitations, actual consumer review not run, API provider/environment unavailable, runtime/tool constraints>`.

**What this does NOT authorize or prove:** `<Human acceptance, canonical spec adoption, backend/DB implementation, protected writes, real API integration, executed tests, deployment, security certification, delivered Product outcome>`.

**Next legitimate action and owning Human/consumer:** `<...>`.

**Final consumer-readiness rule:** An elegant prose handoff is **insufficient** if an actual implementer must invent a material API field, permission, database invariant, transaction boundary, error/unknown meaning, security control or verification condition. Fix/hold that specific edge rather than marking all eight sections complete.
