# Template — UX Output & Consumer Handoff (Bahasa Indonesia)

> **Standing:** DRAFT FOR HUMAN REVIEW, reusable **research authoring aid** only (A2, 2026-11-04). Not an approved target-project UX artifact, Design Standard, formed Space contract, Human decision or write authorization.
> **Contract references:** [UX Definition](../definition.md) · [UX Authority & Handoff](../authority-and-handoff.md).
> **Use:** One bounded UX artifact (or an index of actual project-owned sources) for the **information and decisions needed by a real consumer**. Nine logical output types (O1–O9) are coverage prompts, **not nine mandatory files or nine obligatory sections**.

## Cara menggunakan

- Isi **identitas, source/standing, scoped UX decisions, material interaction states, unresolved gaps, dan consumption needs** pada tingkat yang cukup untuk keputusan sebenarnya.
- Gunakan **referensi exact project-owned source** jika output sudah ada dan valid; jangan menduplikasi authoritative Product, UX, atau Project Standard menjadi spesifikasi tandingan.
- Untuk output yang tidak relevan, tulis **N/A — alasan** singkat. Untuk output yang belum diputuskan tetapi material, tulis **OPEN — owner dan affected decision**. Jangan mengisi placeholder dengan asumsi lalu mengklaim READY.
- Jika prototype, UX Flow, wireframe, atau route map adalah file terpisah, tautkan exact revisions dan nyatakan authority/proof limits. **O2 dan O6 wajib secara default untuk UX baru/material**, tetapi bukan kewajiban memanggil UX Space atau menjalankan fase Lo-Fi sebelum UI/Engineering.
- Template yang sudah terisi **belum approved**. Approval Human terhadap exact artifact revision dicatat terpisah agar accepted bytes tidak berubah hanya untuk mengisi status atau SHA.

## Format artefak & batas pembuktian (conditional)

Gunakan format sesuai [UX Definition — Artifact Representation & Tooling Constraints](../definition.md#7-artifact-representation--tooling-constraints--ux-lo-fi). **Markdown** adalah default; gunakan **Mermaid di dalam Markdown** jika hubungan/flow perlu diagram, **HTML + CSS** jika komposisi Lo-Fi perlu diperiksa, dan **minimal JavaScript** hanya jika interaksi yang disimulasikan perlu diuji serta tool/runtime diizinkan. Untuk UX baru/material, **O2 diagram dan O6 Lo-Fi wajib secara default**; task lain boleh memakai sumber existing yang cukup, dan prototype interaktif tidak wajib secara universal.

Jangan menganggap source Mermaid otomatis sudah dirender, file HTML otomatis sudah diperiksa di browser, atau clickable prototype otomatis membuktikan backend/real-user usability. Gunakan Markdown fallback jika rendering tidak tersedia; catat limitasi. Diagram/visual harus merujuk owning UX/Product decisions, **bukan menjadi competing authority**.

**Baseline wajib untuk UX baru/material:** O2 UX Flow Diagram dan O6 Lo-Fi Wireframes harus tersedia sebagai default; Mermaid dan HTML/CSS menjadi format authoring baru. Accepted existing exact-revision artifact boleh digunakan tanpa dibuat ulang. Exception harus mencatat O-ID/scope, evidence, UX owner/delegation, dan akibat terhadap consumer. Ketiadaan renderer tidak otomatis menjadi exception; tandai NOT RENDERED / NOT CHECKED.

## 0. Identity, scope & effective sources — required for binding consumption

| Field | Actual value / source |
| --- | --- |
| Project / bounded outcome / UX question | `<...>` |
| Intended functional consumer and decision | `<e.g. visual interface design deciding navigation/state expression>` |
| Legitimate UX decision owner | `<actual project authority / delegation source>` |
| Product authority and bounded scope | `<path + immutable revision + standing, or HYPOTHESIS / not binding>` |
| Applicable project Design Standards | `<effective paths + exact revisions / N/A with reason>` |
| Other material input and constraints | `<a11y, device, security/privacy, verified technical facts, research, etc.>` |
| This UX artifact / referenced output revisions | `<path + immutable revision when available>` |
| Logical UX output(s) dan pertanyaan yang dibuktikan | `<O1–O9 yang relevan + pertanyaan konkret; N/A jika tanpa visual>` |
| Artifact representation / format | `<Markdown / Mermaid-in-Markdown / HTML+CSS / conditional JS / supporting reference>` |
| Diagram/Lo-Fi/prototype exact source | `<Git path + immutable revision atau NONE / NOT YET PERSISTED>` |
| Render / interaction verification | `<CHECKED + actual tool/evidence ref / NOT CHECKED; source inspection != rendering>` |
| Simulation / observed evidence / proof limits | `<yang disimulasikan, yang benar-benar diperiksa, yang tidak dibuktikan>` |
| O2/O6 baseline fulfillment / exception | `<new actual proof / accepted exact-revision equivalent / O-ID + scope + evidence + legitimate owner/delegation + consumer impact>` |
| Decision standing | `EXPLORATORY / PROPOSED / ACCEPTED only with separate exact-revision evidence` |
| Material exclusions / non-claims | `<...>` |

The current effective status is established by **actual project-owned approval evidence**, not by editing this table. Where approval has not happened, keep proposed meaning explicitly provisional.

## O1 — Actor Scenario & UX Journey

**Bounded actor goal and entry context:** `<...>`

| UX moment / actor goal | Relevant information encountered and understood | Decision/action | Consequence and accepted Product source | Alternate / recovery |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<reference, not invented policy>` | `<...>` |

Actor scenario and UX Journey concern **interaction experience**, not new Product domain rules or legal/role standing.

## O2 — UX Flow

**O2 required-baseline coverage (new/material UX):** `<Mermaid source + exact revision / accepted equivalent revision / evidence-backed exception with scope and owner>`

| Flow ID | Trigger / precondition | Interaction decision and branch | Exit / failure / unknown / recovery | Decision standing |
| --- | --- | --- | --- | --- |
| FLOW-01 | `<...>` | `<...>` | `<...>` | `<proposed/accepted ref>` |

Do not invent backend ordering, APIs or success semantics to make the flow look complete.

## O3 — Information Architecture (IA)

| IA ID | Person's current question / decision | Needed-now information / timing | Additional accessible detail and placement | Product/Design source |
| --- | --- | --- | --- | --- |
| IA-01 | `<...>` | `<...>` | `<...>` | `<...>` |

Distinguish mandatory pre-effect disclosures, information discoverable on demand, and nonessential repetition. UX selects priority/structure; Product owns consequential information meaning.

## O4 — Navigation Structure

| Surface / navigation node | Entry and destination / return | Purpose and information access | Relevant alternate/error states | Standing |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Scope:** `<web / native / service / other>`. Not every interaction requires page-to-page navigation.

## O5 — Webpage Map & Route Specification (conditional)

**Applicability:** `APPLICABLE / N/A — reason`

| Web path / page | Purpose and actor entry | Navigation to/from | Page vs in-page state | Accepted/proposed revision |
| --- | --- | --- | --- | --- |
| `<route if genuinely applicable>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Web page paths are UX navigation decisions; not backend API endpoints or mandatory router/Next.js implementation details.** Do not invent paths for a non-web scope.

## O6 — Structural Lo-Fi Proofs (required baseline for new/material UX)

**Baseline disposition:** `NEW PROOF / ACCEPTED EXACT-REVISION EQUIVALENT / JUSTIFIED NON-APPLICABILITY` — include source, evidence, UX owner and consumer consequence. Render verification remains separately stated.

| Wireframe / structural artifact | UX question tested | Covered surface/state | Actual inspection/evidence and exact ref | Limitations |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

A low-fidelity image or mock is not itself an accepted UX decision; its scope, source and standing matter.

## O7 — Interaction & UI State Requirements

| STATE ID | Actor action / situation | User-visible meaning and allowed action | Error / denied / partial / unknown handling and recovery | Accessibility / UX requirement | Product source / standing |
| --- | --- | --- | --- | --- | --- |
| STATE-01 | `<...>` | `<...>` | `<...>` | `<focus, keyboard, screen-reader, device, responsive priority>` | `<...>` |

Include only **material** states, such as empty, loading, validation, permission, failure, unknown result, recovery and legitimate success. A timeout is not evidence of confirmed success or confirmed failure. Do not invent Product or backend states.

## O8 — Interactive Prototype & UX Evaluation (conditional)

**Applicability:** `APPLICABLE / N/A — reason`

| Prototype / evaluation evidence | Real UX question | Actually inspected flows/states | Method and finding | Not proven |
| --- | --- | --- | --- | --- |
| `<path + revision, or NONE>` | `<...>` | `<...>` | `<walkthrough / heuristic / independent user check / a11y check>` | `<runtime / usability / accessibility / etc.>` |

A synthetic clickable demo may substantiate **interaction feasibility at that fidelity**; it cannot prove real user comprehension, API success, security, or implemented accessibility without performed evidence.

## O9 — UX Review & Decision References

| Decision ID / affected output | Proposed decision or question | Real Human disposition / standing | Evidence / trade-off | Immutable reviewed artifact or pending reference | Remaining scope |
| --- | --- | --- | --- | --- | --- |
| UX-DEC-01 | `<...>` | `<PROPOSED / HUMAN-ACCEPTED only if actual evidence>` | `<...>` | `<...>` | `<...>` |

**Approval evidence is external to approved artifact bytes.** Do not fill an APPROVED label or SHA inside an already accepted UX artifact and claim an earlier decision still covers the revised bytes. If acceptance predates persistence, preserve the immutable reviewed snapshot and check exact persisted equivalence.

## Consumer Handoff & Decision-Specific Sufficiency — required

| Consumer responsibility / intended decision | Required approved UX meaning and exact source | UX/other-concern delegated freedom | Material gap / owner | Compatibility / evidence standing |
| --- | --- | --- | --- | --- |
| `<visual interface / engineering solution / implementation / verification / standard proposal>` | `<...>` | `<...>` | `<...>` | `<SUFFICIENT / CONDITIONAL / BLOCKED / UNVERIFIED + reason>` |

**Generic receiving contract check:** `<actual declared contract result, or NOT APPLICABLE>`

**Project-bound consumer check:** `<actual scope, source/approval/security/standard checks, or NOT CHECKED>`

**What is not being claimed:** `<e.g. rendered fidelity, independent user test, implementation/runtime verification>`

**Next legitimate decision and owner:** `<...>`

Do not create a second authoritative Product/Design Standard master or hide mandatory obligations in unapproved prototype files. This UX output is a bounded information/decision vehicle, **not permission** to invoke a Space, modify protected files, approve UI, adopt a project-wide standard, deploy code, or claim a delivered actor outcome.
