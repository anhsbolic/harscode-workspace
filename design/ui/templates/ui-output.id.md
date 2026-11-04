# Template — UI Output & Consumer Handoff (Bahasa Indonesia)

> **Standing:** A3 RESEARCH AUTHORING TEMPLATE / DRAFT FOR ANHAR REVIEW (2026-11-04). Bukan approved target-project UI Design, project-wide Design Standard, runtime/visual verification, formed Space, atau izin menulis/menjalankan tool.
> **Contract:** [UI Definition](../definition.md) · [UI Authority & Consumer Handoff](../authority-and-handoff.md). Versi bahasa lain: [English](ui-output.en.md).
> **Use:** Satu bounded UI output record, atau navigable index ke artifact project-owned yang sudah tersedia. Sembilan logical outputs **O1–O9 bukan sembilan file wajib**. Template ini **tidak menggantikan visual artifact** untuk desain baru/material.

## Cara menggunakan

- Pertama, lakukan **UI Input Sufficiency Check** terhadap **I01–I13** sebagaimana didefinisikan di [UI Definition](../definition.md#3-ui-input-sufficiency-check). Referensikan owning source yang sebenarnya; jangan membuat ulang Product/UX/Project Design Standard sebagai authority kedua.
- Untuk new/material visual UI, **visual screen proof O1 wajib tersedia secara default**; sertakan affected **O3 responsive, O4 material states, O5 visual/component styles dan O7 final UI copy**. Reuse exact accepted artifacts jika cukup; exception mesti punya scope, evidence, legitimate decision owner/delegation dan dampak consumer.
- O2 prototype diperlukan **ketika interaksi yang material tidak dapat dievaluasi secara memadai lewat static proof**; O6 reusable library dan O8 assets mengikuti kebutuhan nyata, bukan target jumlah file.
- Jika artifact terdapat pada HTML/CSS, images, prototype, existing Figma atau media lain, cantumkan **path, exact revision, decision scope, visual inspection standing dan evidence limits**. Source file/HTML di Git bukan bukti sudah dirender di browser.
- Bedakan **NOT CHECKED**, **CHECKED (actual evidence)** dan **HUMAN ACCEPTED exact revision**. Review atau approval record boleh terpisah agar approved bytes tidak berubah karena menambahkan hash/status ke dalam artifact yang sudah ditinjau.
- Gunakan `N/A — alasan dan scope` untuk output yang benar-benar tidak berlaku, `OPEN — owner dan consumer impact` untuk material gap; jangan pernah mengisi placeholder dengan asumsi lalu menyatakan READY.

## 0. Identity, scope, input sufficiency & standing

| Field | Actual value / exact source |
| --- | --- |
| Project / bounded UI outcome / actor / intended decision | `<...>` |
| Actual UI decision owner / delegation evidence | `<actual target-project owner and reference>` |
| Intended functional consumer and decision | `<Engineering / verification / other, exact decision>` |
| Current project repo, branch and inspected baseline | `<path + immutable revision>` |
| Effective Product sources / accepted scope | `<project-owned paths + revisions + standing>` |
| Effective UX sources: O2 Flow & O6 Lo-Fi baseline | `<accepted paths/revisions, or legitimate evidenced exception>` |
| Applicable UX O1/O3/O4/O7 and web O5 | `<actual accepted source/revision or gap owner>` |
| Effective Brand/Visual/Component/Asset standards | `<project-owned paths/revisions and applicability; N/A if absent>` |
| Other material I01–I13 input decisions and gaps | `<applicable input IDs + source/owner; link source checks>` |
| UI candidate artifact(s) and source revision(s) | `<exact revision(s) when persisted; prior source if proposed>` |
| Binding UI input sufficiency | `SUFFICIENT / CONDITIONAL / BLOCKED / UNVERIFIED + per-decision reason` |
| UI content standing | `PROPOSED / ACCEPTED only with separate actual exact-revision evidence` |
| Exclusions, open decisions, risks | `<...>` |

**No silent UX substitution:** Untuk UX baru/material, UX O2 flow dan O6 structural Lo-Fi default required. Jika kurang, arahkan specific gap ke UX owner. UI boleh exploration yang independen, tetapi keputusan visual yang bergantung pada UX belum boleh diklaim accepted.

## 1. Visual evidence register — required for new/material UI

| Evidence ID | Linked source + exact revision | UI question / covered O-ID(s) | Screens / states / viewports actually included | Render/inspection standing and method | What this does NOT prove |
| --- | --- | --- | --- | --- | --- |
| VIS-01 | `<HTML/image/etc path + revision>` | `<O1/O3/O4/O5/O7 + question>` | `<...>` | `NOT VISUALLY VERIFIED / CHECKED + actual observation ref` | `<user test, API, accessibility, etc.>` |

**Required visual review boundary:** Untuk new/material UI, prose atau tabel tanpa inspectable visual O1 tidak cukup untuk final visual decision. Renderer tidak tersedia = **NOT VISUALLY VERIFIED** dan affected visual acceptance gap; jangan menciptakan klaim rendering. Existing accepted visual proofs dapat direferensikan jika benar-benar mencakup affected scope.

## O1 — Hi-Fi Screen Designs (default required for new/material UI)

| Screen/surface ID | Actor goal and accepted UX anchor | Visual composition, main content/actions and hierarchy | Visual evidence ref | Scope / accepted/proposed standing |
| --- | --- | --- | --- | --- |
| UI-SCREEN-01 | `<UX flow/IA/state source>` | `<...>` | `<VIS-01 + exact revision>` | `<...>` |

**Sufficiency:** `<new inspectable proof / already accepted equivalent + exact revision / evidenced no-impact exception>`. Untuk meaningful new visual decision, **jangan hanya mendeskripsikan layout**.

## O2 — Interactive Prototype (conditional)

**Trigger:** `<interaction cannot be responsibly reviewed through static proof? YES / NO + concrete reasoning>`

| Prototype/ref | Actual simulated interactions and states | Source/evidence and inspection | Not proven / prohibited real effects |
| --- | --- | --- | --- |
| `<... / N/A>` | `<...>` | `<...>` | `<no real auth/API/data effects, etc.>` |

Simulasi clickable tidak membuktikan product behavior, acceptance, real users atau integration. JS minimal hanya jika dibutuhkan dan diizinkan.

## O3 — Responsive Designs (affected scope required)

| Screen / state | Representative viewport / device context | Information priority, layout/reading order and overflow behavior | Visual evidence + actual inspection | Open limitations |
| --- | --- | --- | --- | --- |
| `<...>` | `<e.g. narrow/wide actual reviewed contexts>` | `<...>` | `<VIS-ID or NOT CHECKED>` | `<...>` |

Bukan kewajiban universal untuk semua angka breakpoint; cakup affected behavior yang material dengan evidence.

## O4 — UI Interaction States (material states required)

| UI state / trigger | Accepted UX/Product meaning and source | Visible copy/affordance/feedback, focus/recovery | State visual evidence | Actual inspection / exception |
| --- | --- | --- | --- | --- |
| `<loading / validation / denied / unknown / recovery / success, as applicable>` | `<...>` | `<...>` | `<VIS-ID>` | `<...>` |

Jangan menyamakan pending, unknown, failed, success atau verified jika Product truth membedakannya. Jangan mengarang state transitions atau backend result.

## O5 — UI Components & Styles (affected scope required)

| UI component / element | Existing approved precedent or scoped new candidate | Variant, typography/color/spacing/interaction appearance | Visual evidence / implementation freedom | Reusable standard status |
| --- | --- | --- | --- | --- |
| `<...>` | `<effective source / PROPOSED>` | `<...>` | `<...>` | `<feature candidate / existing standard>` |

Frontend component API/CSS/framework belongs to Engineering. Local new variant **tidak otomatis** menjadi reusable project standard.

## O6 — Reusable UI Component Library (conditional)

**Reuse trigger:** `<repeated use evidenced across real project needs? YES / NO + concrete reason>`

| Candidate library/component | Actual repeated-use need | Owner/project-standard decision required | Scope, affected consumers & source standing |
| --- | --- | --- | --- |
| `<... / N/A>` | `<...>` | `<not automatically approved>` | `<...>` |

Jika belum dibutuhkan, jangan membangun library besar atau mempromosikan global tokens/style tanpa owner approval.

## O7 — Final UI Copywriting (affected scope required)

| Screen/state/element | Final candidate UI text, language and placement | Accepted Product/Legal terms, copy source and standing | Visual evidence / unresolved review |
| --- | --- | --- | --- |
| `<...>` | `<actual user-facing copy>` | `<...>` | `<...>` |

Consequential wording/legal disclosures tetap tunduk pada Product/Legal owner. Tidak semua perubahan copy memerlukan approval baru bila secara sah didelegasikan.

## O8 — Final Visual Assets (conditional)

| Asset/ref & intended purpose | Provenance/license/availability | Exact project source + standing | Actually inspected / fit & limitations | Required approval or remaining gap |
| --- | --- | --- | --- | --- |
| `<... / N/A>` | `<...>` | `<...>` | `<...>` | `<...>` |

Visual references, generated candidates, icons dan brand assets tidak otomatis production-ready atau approved. Jangan klaim telah melihat pixel hanya dari filename.

## O9 — Design Review & Acceptance References

| Decision ID / affected O-ID | Actual question, trade-off & review finding | Human decision/owner or OPEN | Exact reviewed UI artifact revision | Evidence gaps / exclusions |
| --- | --- | --- | --- | --- |
| UI-DEC-01 | `<...>` | `<PROPOSED / accepted with separate evidence>` | `<...>` | `<...>` |

**Approval record external to approved bytes.** Commit, filled template, rendered prototype atau reviewer suggestion bukan pengganti actual legitimate Human acceptance.

## Consumer Handoff & Decision-Specific Completion — required

| Consumer / intended decision | Exact accepted project-owned UI evidence + Product/UX/Standard origins | UI constraints and delegated implementation freedom | Compatibility/verification status | Material gap / owner |
| --- | --- | --- | --- | --- |
| `<e.g. Engineering implementation of this screen set>` | `<exact refs/revisions>` | `<...>` | `<SUFFICIENT / CONDITIONAL / BLOCKED / UNVERIFIED>` | `<...>` |

**Generic consumer Input Contract check:** `<actual applicable formed contract test, or NOT APPLICABLE>`

**Project-bound consumer check:** `<real project authority/security/accessibility/copy/asset/readiness and scoped acceptance, or NOT CHECKED>`

**Performed checks vs not performed:** `<actual inspected screens/viewports/states, source-only limitations, accessibility/user/API/runtime NOT CHECKED>`

**Next legitimate decision and owner:** `<...>`

**Nonclaims:** UI acceptance does **not** approve Product/UX changes, reusable project standards, API/security contracts, frontend implementation, deployment, runtime behavior, accessibility certification, asset licensing, or release. This template carries information, **not execution or write authorization**.
