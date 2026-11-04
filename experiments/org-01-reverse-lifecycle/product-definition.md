# ORG-01 — Product / Product Definition

> **Status:** FINAL WORKING MODEL FOR THIS EXPERIMENT — approved by Anhar on 2026-11-03 for recording. **NOT canonical Harscode policy, NOT a new Kencleng Product Contract, NOT proof of validated user demand or actual ORG-01 delivery.**
> **Repository scope:** Harscode-Workspace `refactor/harscode-foundation` (research branch; `main` remains operational).
> **Method:** Reverse lifecycle, high-level illustrative ORG-01 case. No comparison, audit, or replacement of existing ORG-01 artifacts.
> **Experiment decision owner:** Anhar.

**Aktor:** Calon Pembentuk Organisasi.

**Tujuan:** Mendefinisikan masalah, kebutuhan aktor, nilai produk, meaningful journey, domain roles, dan aturan yang menentukan keberhasilan pembentukan organisasi.

## 1. INPUT

| No. | Input konkret | Kebutuhan |
| --- | --- | --- |
| 1 | **Product Direction & Initiative Context** — arah produk dan alasan kemampuan ini dibutuhkan | **Wajib** |
| 2 | **Problem Statements & Signals** — masalah pengguna, observasi, atau hipotesis awal | **Wajib** |
| 3 | **Candidate Actor & Context** — calon pengguna, kebutuhan, konteks, dan tujuan | **Wajib** |
| 4 | **Domain Context & Terminology** — organisasi, membership, `Owner`, dan konsep terkait | **Wajib** |
| 5 | **Existing Product Behavior & Boundaries** — capability dan batasan produk yang sudah berlaku | **Wajib jika existing product** |
| 6 | **Existing Business Rules & Policies** — aturan atau keputusan Product terdahulu | **Wajib jika relevan** |
| 7 | **Stakeholder Goals & Decision Authority** — tujuan stakeholders dan siapa yang berwenang memutuskan | **Wajib** |
| 8 | **Product Success Signals** — indikator awal keberhasilan | **Wajib, boleh provisional** |
| 9 | **User Research & Existing Feedback** — interview, observasi, usability findings, feedback nyata | **Wajib dipertimbangkan jika tersedia dan relevan** |
| 10 | **Legal, Privacy & Compliance Constraints** — ketentuan yang membatasi produk dan perlakuan data | **Wajib jika material** |
| 11 | **Known Business & Operational Constraints** — dependency, waktu, resource, dan batasan operasional | **Wajib jika material** |
| 12 | **Related Product Dependencies** — kemampuan terkait yang memengaruhi outcome | **Sesuai kebutuhan** |
| 13 | **Market & Competitor References** — referensi solusi dan pola produk sejenis | **Nice to have** |

Klasifikasi **Wajib** merujuk pada informasi yang harus cukup untuk keputusan terkait, **bukan** kewajiban 13 dokumen terpisah. Hipotesis boleh digunakan untuk eksplorasi jika dinyatakan eksplisit; hipotesis tidak boleh direpresentasikan sebagai validated evidence. Existing relevant research tidak boleh diabaikan.

**Product Contract bukan input wajib untuk memulai Product Definition:** kontrak tersebut justru output dari fase ini. Existing Product Contracts yang relevan, bila ada, dapat menjadi input sebagai current rules atau constraints. Product tidak harus menerima fully specified requirements dari awal.

## 2. PROCESS

| No. | Process | Aktivitas konkret |
| --- | --- | --- |
| 1 | **Product Intent & Problem Definition** | Memahami masalah, nilai yang ingin diberikan, dan alasan produk membutuhkan kemampuan ini |
| 2 | **Actor & Context Analysis** | Mengidentifikasi aktor, tujuan, kebutuhan, konteks, dan hambatannya |
| 3 | **Domain Role & Authority Definition** | Mendefinisikan makna `Owner`, cara memperoleh role, kewenangan, dan batasannya |
| 4 | **Product User Journey Definition** | Mendefinisikan meaningful progression aktor, termasuk success, failure, dan uncertain outcomes |
| 5 | **Product Outcome & Scope Definition** | Menentukan bounded outcome ORG-01 dan batas scope |
| 6 | **Product Requirements & Business Rules** | Menentukan requirements, domain invariants, dan consequential rules |
| 7 | **Success & Acceptance Definition** | Menentukan success criteria, acceptance criteria, dan observable outcomes |
| 8 | **Product Review & Refinement** | Mengevaluasi konsistensi intent, roles, journey, requirements, dan acceptance |
| 9 | **Human Product Review & Approval** | Meminta approval untuk consequential Product decisions yang akan menjadi authority |

Process boleh iteratif dan proporsional terhadap keputusan yang sedang dibuat, bukan mandatory nine-step waterfall.

## 3. OUTPUT

| No. | Output konkret |
| --- | --- |
| 1 | **Product Intent & Value Definition** — problem, value proposition, dan tujuan kemampuan pembentukan organisasi |
| 2 | **Actor Definition & Goals** — aktor, kebutuhan, konteks, dan tujuan yang ingin dicapai |
| 3 | **Product User Journey** — meaningful progression dari kebutuhan awal hingga hasil; termasuk negative dan unknown states |
| 4 | **Selected Product Outcome** — bounded outcome ORG-01 dan scope boundaries |
| 5 | **Product Contract** — requirements, **Domain Roles & Authority Rules**, **Content & Information Requirements** yang consequential, business rules, invariants, success criteria, dan acceptance criteria |
| 6 | **Product Review & Approval Record** — Human decisions, approval scope, unresolved questions, dan revision standing |

**Domain Roles & Authority Rules** dan **Content & Information Requirements** yang consequential adalah bagian eksplisit Product Contract, **tidak otomatis dokumen terpisah**. Product menentukan informasi apa yang wajib dikumpulkan, ditampilkan/disampaikan, atau dipahami aktor karena alasan domain, aturan, atau konsekuensi Product. UX Design menentukan information grouping, presentation, hierarchy, dan interaction; Product tidak mengambil alih layout atau UI copy yang non-consequential. Keenam output merupakan logical artifacts yang dapat digabung bila cukup untuk actual decision.

## 4. OUTCOME — PRODUCT DEFINITION TARGET

1. **Clear Purpose** — jelas masalah apa yang diselesaikan dan mengapa kemampuan ini bernilai.
2. **Actor-Centered** — kebutuhan dan meaningful journey aktor dipahami.
3. **Defined Success** — jelas kapan organisasi dan initial `Owner` benar-benar dianggap berhasil.
4. **Truthful & Bounded** — aturan, scope, authority, failure, dan uncertainty terdefinisi dengan benar.
5. **Testable** — requirements memiliki acceptance criteria yang dapat diverifikasi.
6. **Authoritative** — consequential Product decisions memiliki scope approval dan authority yang jelas.

**Target akhir:** Product meaning, Actor Journey, Domain Roles, dan bounded Product Outcome cukup jelas dan durable untuk menjadi landasan UX Design dan keputusan downstream. **Bukan** klaim fitur berjalan atau value sudah tervalidasi pengguna.

## Agreed boundaries and working decisions

- **Actor ≠ Role.** Actor merepresentasikan perspektif dan tujuan; Domain Role merepresentasikan kedudukan dan kewenangan seseorang dalam konteks tertentu. Pada ORG-01, aktornya calon pembentuk organisasi, yang setelah sukses memiliki hubungan initial `Owner` pada organisasi baru.
- **Product owns Domain Roles & Authority Rules.** Product menentukan makna `Owner`, aturan memperoleh/kehilangan role, konsekuensi, kewenangan dan batasannya **sejauh material untuk ORG-01**. Tidak perlu mendefinisikan seluruh role Kencleng. Rancang owns mechanism dan technical enforcement (misalnya authorization checks), tanpa menyamakan Domain Role dengan implementasi RBAC tertentu.
- **Product User Journey ≠ UX Flow.** Product menentukan meaningful actor progression dan consequential sequence, bukan screens, URL paths, exact login timing, UI navigation, wireframes, API atau database. UX Design owns interaction sequence, navigation, dan webpage paths.
- **Decision-specific sufficiency.** Bounded exploratory UX boleh bertolak dari explicit Product hypotheses; consequential commitments yang dikunci memerlukan relevant Product authority dan approval proportional to consequence.
- **Approval ≠ empirical validation.** Human acceptance atas Product decisions tidak dengan sendirinya membuktikan product-market fit, actual user need, atau usable delivered software.
- **No documentation waterfall by default.** Kecukupan ditentukan oleh keputusan downstream, bukan kewajiban menyelesaikan setiap artifact secara maksimal.

## Decision and evidence standing

- Anhar menyepakati pemisahan Actor vs Role dan penempatan Domain Roles & Authority Rules di Product Contract.
- Anhar menyetujui daftar Input Product, lalu meng-approve keseluruhan Input → Process → Output → Outcome Product untuk **working experiment**, dan secara eksplisit mengotorisasi persist ke direktori eksperimen.
- Snapshot ini merekam diskusi dan keputusan eksperimen, bukan evidence hasil riset aktual, proof of real execution, approval existing Kencleng Product Contract, atau promosi lifecycle ke Harscode `main`.
- **Repository discipline:** persist hanya setelah satu fase selesai dan izin eksplisit Anhar.
