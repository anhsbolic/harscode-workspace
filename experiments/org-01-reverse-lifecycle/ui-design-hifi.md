# ORG-01 — UI Design / Hi-Fi

> **Status:** FINAL WORKING MODEL FOR THIS EXPERIMENT — approved by Anhar for recording on 2026-11-03; **NOT canonical Harscode policy, NOT project Design approval, NOT user-tested**.
> **Scope:** Illustrative ORG-01 design for a single actor, without auditing or comparing existing ORG-01 documents or implementation.
> **Owner of experiment decisions:** Anhar. **Branch:** `refactor/harscode-foundation` (research only).

**Aktor:** Calon Pembentuk Organisasi.

**Tujuan:** Menghasilkan desain antarmuka pembentukan organisasi yang jelas, intuitif, accessible, responsive, konsisten secara visual, dan berkualitas.

## 1. INPUT

| Input konkret | Kebutuhan |
| --- | --- |
| **UX Flow Diagram** — alur pembentukan organisasi, navigation, review, submit, dan hasil | **Wajib** |
| **Lo-Fi Wireframes** — struktur layar, penempatan informasi, dan navigasi | **Wajib** |
| **Webpage Map & Route Specification** — accepted webpage paths, page purpose, entry/exit points, serta page vs UI state | **Wajib** |
| **Product Requirements & Business Rules** — aturan pembentukan, kewenangan `Owner`, keberhasilan dan kegagalan | **Wajib** |
| **Screen Content & Information** — informasi organisasi, form fields, penjelasan kewenangan dan pesan penting | **Wajib** |
| **UI States & Interaction Requirements** — default, loading, validation, success, error dan uncertain result | **Wajib** |
| **Brand & Visual Guidelines** — typography, colors, visual identity dan design principles | **Wajib*** |
| **Responsive & Accessibility Requirements** — desktop, mobile, contrast, keyboard, focus dan readability | **Wajib** |
| **Design Quality Criteria / Anti-AI Slop Guidelines** — visual quality, information density, purposeful visuals dan natural copy | **Wajib** |
| **Existing Design System & UI Component Library** — components, variants, styles dan tokens yang sudah ada | **Wajib jika tersedia** |
| **Web Assets** — logo, icons, illustrations, images, fonts | **Sesuai kebutuhan desain** |
| **Visual References / Moodboard** — referensi gaya visual dan composition | **Nice to have** |
| **Usability Research / User Feedback** — evidence kebutuhan atau kesulitan pengguna | **Nice to have** |

*Jika Brand Guidelines belum ada, diperlukan arahan atau kebebasan eksplisit untuk menentukan visual direction. `Wajib` berarti informasi/materialnya harus cukup, tidak harus satu dokumen terpisah. Research yang tersedia tetap dipertimbangkan secara proporsional; status *nice to have* bukan izin mengabaikan evidence yang relevan.*

**Cross-stage clarification (2026-11-04, approved by Anhar):** Webpage Map & Route Specification dari UX Lo-Fi adalah explicit Design contract untuk Hi-Fi, bukan hal yang boleh diam-diam diubah saat visual design. Technical constraints yang material perlu direkonsiliasi dengan Design owner; ini tidak memerlukan dokumen baru.

## 2. PROCESS

1. **Screen & Content Planning** — menentukan screens, content hierarchy, dan informasi yang ditampilkan.
2. **Visual Direction** — menentukan typography, colors, visual style, composition, dan brand expression.
3. **Reusable UI Component Design & Management** — reuse existing components; create/extend jika justified; define variants, states, responsive behavior; maintain component library.
4. **Hi-Fi Screen Design** — mendesain form, review, navigation, authentication continuation, dan result screens.
5. **Responsive Design** — mendesain desktop/mobile layouts dan adaptasi komponen.
6. **Interaction & UI States Design** — mendesain default, loading, validation, success, failure, dan unknown states.
7. **UI Copywriting & Visual Assets** — menyiapkan Bahasa Indonesia yang natural dan visual assets yang diperlukan.
8. **Interactive Prototyping** — membuat clickable prototype main flow dan relevant alternative states.
9. **Design Review & Refinement** — visual dan interaction review, accessibility, usability walkthrough, **Anti-AI Slop review**, Human feedback, dan refinement.

**Anti-AI Slop** dipertimbangkan sepanjang Visual Direction, Hi-Fi Screen Design, Copywriting, dan Design Review. Contoh review: visual tidak sekadar dekoratif, information hierarchy jelas, copy tidak robotic, UI containers tidak berlebihan, dan setiap kompleksitas punya nilai bagi aktor. Cards, gradients, atau ilustrasi tidak otomatis salah; evaluasi berdasarkan kegunaannya.

Proses boleh iteratif; prototype review dapat memicu revisi screen, component atau copy.

## 3. OUTPUT

1. **Hi-Fi Screen Designs** — desain visual final untuk screens yang relevan.
2. **Interactive Prototype** — clickable prototype dengan alur dan interaksi.
3. **Responsive Designs** — desktop dan mobile layouts.
4. **UI Interaction States** — loading, validation, success, failure, empty jika relevan, dan uncertain state.
5. **UI Components & Styles** — components, typography, colors, spacing dan visual specifications.
6. **Reusable UI Component Library** — reusable components, variants, states dan interaction specifications yang dibuat atau diperbarui seperlunya.
7. **Final UI Copywriting** — Bahasa Indonesia natural, jelas, kontekstual.
8. **Final Visual Assets** — logo, icons, illustrations, images, fonts yang diperlukan.
9. **Design Review & Acceptance Record** — feedback, revisi, penilaian quality criteria termasuk Anti-AI Slop, dan keputusan Human terhadap desain.

Yang sudah tersedia dan unchanged tidak perlu dibuat ulang. Library komponen adalah *Design-level contract*, bukan implementasi code. Jangan membangun library besar demi satu flow sederhana.

## 4. OUTCOME — DESIGN-LEVEL TARGET

Aktor calon pembentuk organisasi mendapat rancangan pengalaman yang:

1. **Clear** — memahami tindakan dan informasi yang diperlukan.
2. **Intuitive** — alur mudah diikuti tanpa kebingungan yang tidak perlu.
3. **Informative** — memahami konsekuensi membentuk organisasi dan menjadi `Owner` internal.
4. **Transparent** — keberhasilan, kegagalan dan ketidakpastian dikomunikasikan jujur.
5. **Accessible** — mempertimbangkan accessibility dan berbagai ukuran layar.
6. **Visually Coherent** — konsisten dengan brand, mudah dibaca, tidak generik atau berlebihan.

**Target akhir:** Hi-Fi design matang secara visual, interaction, content dan component consistency; dapat dievaluasi lewat prototype dan telah melalui Human Design Review. Ini adalah *desired design outcome*, **bukan bukti usability nyata, kelulusan implementasi, ataupun approval desain Kencleng**.

## Decision and evidence standing

- Anhar menerima reusable UI component management sebagai bagian Process & Output Hi-Fi (working experiment decision).
- Anhar menerima Anti-AI Slop sebagai quality criteria Input dan sebagai bagian dari review (working experiment decision).
- Anhar meng-approve susunan Input → Process → Output → Outcome ini **sebagai working experiment model** dan secara eksplisit mengotorisasi update direktori eksperimen.
- Model ini belum dibandingkan dengan existing ORG-01 docs, belum menjalani independent review/user test, dan belum dipromosikan menjadi Harscode policy.
- **Repository update discipline:** Persist eksperimen hanya setelah satu fase selesai dan atas izin eksplisit Anhar. Fase sebelumnya/lainnya tidak otomatis berubah standing.
