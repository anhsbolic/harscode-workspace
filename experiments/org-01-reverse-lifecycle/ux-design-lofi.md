# ORG-01 — UX Design / Lo-Fi

> **Status:** FINAL WORKING MODEL FOR THIS EXPERIMENT — approved by Anhar on 2026-11-03 for recording. **NOT canonical Harscode policy, NOT a Kencleng Design approval, NOT tested usability evidence.**
> **Repository scope:** Harscode-Workspace `refactor/harscode-foundation` (research branch; `main` remains operational).
> **Method:** Reverse lifecycle, high-level illustrative ORG-01 case. No comparison/audit of existing ORG-01 artifacts.
> **Experiment decision owner:** Anhar.

**Aktor:** Calon Pembentuk Organisasi.

**Tujuan:** Merancang pengalaman pembentukan organisasi yang jelas, efisien, mudah digunakan, dan sesuai kebutuhan aktor sebelum desain visual final.

## 1. INPUT

| No. | Input konkret | Kebutuhan |
| --- | --- | --- |
| 1 | **Product Intent & Selected Outcome** — tujuan produk dan outcome pembentukan organisasi | **Wajib** |
| 2 | **Actor Definition & Goals** — aktor, tujuan, kebutuhan, dan konteksnya | **Wajib** |
| 3 | **Product User Journey** — meaningful progression, success, failure, unknown states | **Wajib** |
| 4 | **Product Requirements & Business Rules** — pembentukan organisasi, makna `Owner`, konsekuensi | **Wajib*** |
| 5 | **Product Acceptance Criteria** — kondisi keberhasilan yang harus dipenuhi | **Wajib untuk keputusan relevan** |
| 6 | **Content & Information Requirements** — informasi yang diisi, dipahami, dan dilihat aktor | **Wajib** |
| 7 | **Accessibility & Device Requirements** — desktop/mobile, keyboard, accessibility | **Wajib** |
| 8 | **Existing IA & Navigation Patterns** | **Wajib jika tersedia dan relevan** |
| 9 | **Known Technical Constraints** | **Wajib jika relevan** |
| 10 | **User Research & Usability Findings** | **Nice to have** |
| 11 | **UX Patterns & Design References** | **Nice to have** |

*Bounded UX exploration boleh menggunakan Product hypotheses dengan status dan uncertainty eksplisit. Consequential decisions yang akan dikunci memerlukan relevant Product authority dan approval, proportional to consequence. Evidence pengguna yang tersedia dan relevan tetap perlu dipertimbangkan; status “Nice to have” bukan izin untuk mengabaikannya. Klasifikasi input menunjuk informasi/material yang diperlukan, bukan sebelas file wajib.*

**Bukan input yang diperlukan secara default:** Hi-Fi UI Design, final visual Design System, final web assets, API Contract, Database Schema, atau final Engineering Solution. Known technical constraints yang benar-benar relevan tetap harus diperhitungkan.

## 2. PROCESS

| No. | Process | Aktivitas |
| --- | --- | --- |
| 1 | **Actor Scenario Analysis** | Memahami tujuan, konteks, hambatan, dan kebutuhan aktor |
| 2 | **UX Flow Design** | Merancang urutan interaksi pembentukan organisasi |
| 3 | **Information Architecture (IA)** | Menyusun information hierarchy, grouping, dan form contents |
| 4 | **Webpage Map & Route Design** | Menentukan halaman, webpage paths, hubungan, dan navigasi |
| 5 | **Lo-Fi Wireframing** | Membuat sketsa struktur halaman, forms, buttons, dan navigation |
| 6 | **Interaction & State Design** | Menentukan form behavior, validation, loading, success, failure, dan unknown states |
| 7 | **Lo-Fi Prototyping** | Membuat clickable prototype sederhana |
| 8 | **UX Evaluation & Refinement** | Walkthrough, evaluasi clarity, efficiency, accessibility, dan revisi |
| 9 | **Human UX Review & Acceptance** | Review flow, wireframes, webpage map, dan interaction decisions |

Proses bersifat iteratif, bukan kewajiban sembilan langkah linear.

## 3. OUTPUT

| No. | Output konkret |
| --- | --- |
| 1 | **Actor Scenario & UX Journey** — skenario konkret pengalaman aktor |
| 2 | **UX Flow Diagram** — alur interaksi utama dan alternatif |
| 3 | **Information Architecture** — struktur informasi dan content hierarchy |
| 4 | **Navigation Structure** — hubungan antarhalaman dan navigasi |
| 5 | **Webpage Map & Route Specification** — webpage paths, page purpose, entry/exit points, dan page vs UI state |
| 6 | **Lo-Fi Wireframes** — struktur setiap layar |
| 7 | **Interaction & UI State Requirements** — form behavior, validation, loading, success, failure, dan uncertainty |
| 8 | **Lo-Fi Interactive Prototype** — simulasi alur dan navigasi |
| 9 | **UX Review & Decision Record** — feedback, revisi, accepted UX decisions, dan unresolved questions |

**Webpage Map & Route Specification** adalah output eksplisit Lo-Fi dan bagian dari **kontrak Design untuk Hi-Fi**. Exact paths adalah proposed/accepted Design choices sesuai standing review; bisa direkonsiliasi bila ada material technical constraints. Bukan kewajiban sembilan dokumen terpisah.

## 4. OUTCOME — UX DESIGN TARGET

1. **Goal-Oriented** — pengalaman fokus pada tujuan membentuk organisasi.
2. **Intuitive** — urutan tindakan dan navigasi mudah dipahami.
3. **Clear IA** — informasi tersedia dalam konteks dan momen yang tepat.
4. **Efficient** — tidak ada langkah atau interaksi yang membebani tanpa manfaat.
5. **Trustworthy** — konsekuensi `Owner`, keberhasilan, kegagalan, dan uncertainty dipahami dengan benar.
6. **Accessible** — struktur interaksi mempertimbangkan kebutuhan aksesibilitas.

**Target akhir:** UX Flow, IA, Webpage Map, Lo-Fi Wireframes, dan Interaction Requirements yang koheren, dapat dievaluasi lewat prototype, serta melalui Human UX Review. Ini adalah target kualitas desain, **bukan bukti usability pengguna nyata**.

## Agreed boundaries (working experiment decisions)

- **Product owns** meaningful actor progression dan consequential requirements.
- **UX Design — Lo-Fi owns** interaction flow, IA, webpage structure, navigation, dan proposed webpage paths. Product User Journey adalah **input**; UX Flow dan Webpage Map adalah **output**.
- Lo-Fi **tidak menentukan** final visual styling, API endpoints, database schema, atau authentication mechanism.
- Product-consequential changes dikembalikan kepada Product owner; UX Design tidak boleh membuat Product policy baru secara sepihak.
- Technical constraints yang material dapat memicu reconciliation terhadap navigasi atau webpage paths; Rancang tidak sepihak mengambil alih Design ownership.

## Decision and evidence standing

- Anhar menyepakati Webpage Map & Route Specification sebagai output Lo-Fi dan input/kontrak Design bagi Hi-Fi dalam eksperimen ini.
- Anhar meng-approve daftar Input dan kemudian **meng-approve keseluruhan Input → Process → Output → Outcome Lo-Fi** untuk eksperimen, serta secara eksplisit mengotorisasi persist ke direktori eksperimen.
- Belum ada perbandingan dengan existing ORG-01 docs, independent usability evaluation, real execution, Design authority project approval, atau promosi ke Harscode `main`.
- **Repository discipline:** Persist hanya setelah satu fase selesai dan izin eksplisit Anhar.
