# Template — Product Definition (Bahasa Indonesia)

> **Standing:** DRAFT FOR HUMAN REVIEW. Optional research authoring aid; not approved project Product authority.
> **Reference:** [Product Definition](../product-definition.md) and [Authority & Approval](../authority-and-approval.md).

Dokumen ini menangkap **intent, actor, meaningful Product journey dan selected bounded outcome**. Jangan menciptakan sumber binding Product requirements kedua; consequential SC/REQ/AC yang diterima harus tersedia di Product Contract.

## Identitas dan standing

| Item | Isian |
| --- | --- |
| Project / bounded concern | `<...>` |
| Legitimate Product decision owner | `<...>` |
| Current effective source and revision | `<...>` |
| Working status / evidence | `EXPLORATORY / PROPOSED / APPROVED only with exact approval reference` |
| Intended decision / receiving responsibility | `<what information is needed for what decision>` |
| Material assumptions and unknowns | `<...>` |

## O1 — Product Intent & Value Definition

- Masalah dan observed signals: `<...>`
- Arah produk, alasan initiative, intended value: `<...>`
- Pihak yang memperoleh/terdampak oleh value: `<...>`
- Promise, batas klaim, dan yang tidak dijanjikan: `<...>`
- Evidence, hipotesis, dan tingkat keyakinan: `<...>`

## O2 — Actor Definition & Goals

| Actor perspective | Context, needs, goal | Material responsibilities/affected actors | Evidence standing |
| --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<observed / hypothesized / accepted>` |

**Actor ≠ Domain Role.** Domain Role berhubungan dengan kedudukan/kewenangan dalam domain dan aturan peroleh/ubah/hilangnya ketika material; catat binding meaning dalam Product Contract. Jangan asumsikan RBAC.

## O3 — Product User Journey

| Meaningful point | Actor intention / understanding | Legitimate domain consequence | Failure / partial / unknown meaning |
| --- | --- | --- | --- |
| Initial situation | `<...>` | `<...>` | `<...>` |
| Before consequential action | `<...>` | `<...>` | `<...>` |
| Action / transition | `<...>` | `<...>` | `<...>` |
| Result / later inspection | `<...>` | `<...>` | `<...>` |

Catat relevant dependencies dan affected actors. Ini bukan UX Flow, webpage map, route plan, screen design atau API sequence.

## O4 — Selected Product Outcome

- Bounded outcome and actor value: `<...>`
- Scope included/excluded: `<...>`
- Real prerequisites, availability and unknowns: `<...>`
- Related outcomes without assumed execution order: `<...>`
- Legitimate selection owner, source/revision, decision standing: `<...>`

Selection tidak otomatis menyetujui Product Contract atau memberi implementation permission.

## Decision-specific sufficiency and unresolved questions

| Issue | Affected claim / decision | Owner | Evidence, risk, blocking scope |
| --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` |

Nyatakan apakah intended decision sudah **SUFFICIENT**, hanya **EXPLORATORY**, atau **BLOCKED** beserta alasan. Label ini bukan workflow state.

Product Contract efektif, jika ada: `<path + immutable revision>`

Approval Record, jika ada: `<actual decision + exact approved artifact>`

Jangan menyembunyikan binding Product rules di dokumen eksploratif atau menyatakan validated user demand tanpa empirical evidence.
