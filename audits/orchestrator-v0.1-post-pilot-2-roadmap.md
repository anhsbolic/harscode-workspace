# Orchestrator v0.1 — Post-Pilot #2 Roadmap

> Status: Stages 0–1 COMPLETE; Stage 2 DECISION-READY — positioning candidate menunggu keputusan Anhar; stages 3–7 belum dimulai.
> Scope: progress dan keputusan episode Post-Pilot #2 pada branch `pilot/orchestrator-v0.1`; bukan runtime guidance atau canonical Harscode policy.
> Next action: Anhar menerima atau mengoreksi satu positioning candidate Stage 2 di bawah; setelah itu catat exact decision sebelum Stage 3.

## Objective dan batas

Tingkatkan **correct product capability per unit coordination effort** tanpa melemahkan authority, safety, reconstructability, dan necessary independent evidence. Ukur hasil produk dan biaya koordinasi bersama; jumlah artefak atau Run saja bukan ukuran keberhasilan.

Kencleng Slice 2 Pilot #2 sedang **Human HOLD**. Evaluation/reporting boleh berjalan; development Pilot #2, termasuk prepared `EXP-S2-008-001`, tidak boleh di-dispatch. Resume memerlukan instruksi Human eksplisit dan rekonstruksi durable state. Branch ini tetap Pilot Candidate; jangan promote ke `main` selama episode ini belum menghasilkan promotion decision.

## Source dan status klaim awal

| Kelas | Pernyataan dan anchor | Implikasi |
|---|---|---|
| Observation / evidence | Kencleng `validation-04-orchestrator-slice-2@8b9a0503d0c92f60434d704a3796b7329b0adebe`: `docs/project/kencleng-development-tracker.md` (Current WU-S2-003 update), `docs/project/slice-2-progress-workflow-evaluation-2026-10-05.md`, dan `docs/project/slice-2-harscode-evaluation-evidence-2026-10-05.md`. Tracker mencatat HOLD; evaluasi mencatat hasil produk, assurance, friction, serta batas pengukuran. | Ini snapshot evidence; baca current project state lagi sebelum setiap resume/CRTV. Angka 126 Run directories/401 files/507,312 whitespace words dan minimum 44 Human hours punya batas metode dalam lampiran; bukan estimasi biaya total atau Run yang completed. |
| Observation / authority | Harscode `pilot/orchestrator-v0.1@63ec4e0fd4f45a9820939ff8e568031236ce98f4`: `README.md` Status, `orchestration/AGENTS.md`, `orchestration/protocol-v0.1.md`, `orchestration/pilot-2-candidate/README.md`. `main@b64fa11082a094d0e1b6e9488c20eac1c7f9777b` adalah operational baseline. | Candidate guidance tidak otomatis menjadi policy operational. Target-project truth tetap milik Kencleng. |
| Hypothesis | Assurance dan authority cukup kuat, tetapi product/contract readiness yang belum converged, ditambah execution dan orchestration misses, memperbesar avoidable workflow cost. | Diagnosis ini perlu diuji dengan evidence per penyebab; jangan menyimpulkan semua Review, artefak, atau gates berlebih. |
| Working decision | Anhar meminta HOLD, episode evaluasi ini, roadmap 0–7, dan penundaan promotion. | Berlaku sebagai arah kerja episode; tidak menetapkan Harscode policy baru atau acceptance Kencleng. |
| Settled decision | Belum ada keputusan settled Post-Pilot #2 tentang identity, vNext semantics, atau promotion. | Catat decision, owner, evidence, dan exact revision di sini ketika benar-benar settled. |

Dokumen ini adalah **satu progress ledger** episode: perbarui status, checklist, next action, evidence links/revisions, dan decision record di sini. Jangan menduplikasi current Kencleng state atau memindahkan project truth ke Harscode. Git history menyimpan perubahan; jangan menimpa evidence historis tanpa jejak.

## Frozen Stage 0 baseline

Baseline ini adalah **historical evaluation snapshot**, bukan current authorization untuk melanjutkan Kencleng. Exact Harscode candidate-guidance revision sebelum roadmap ialah [`63ec4e0`](https://github.com/anhsbolic/harscode-workspace/tree/63ec4e0fd4f45a9820939ff8e568031236ce98f4); operational `main` ialah [`b64fa11`](https://github.com/anhsbolic/harscode-workspace/tree/b64fa11082a094d0e1b6e9488c20eac1c7f9777b). Kencleng HOLD/evaluation commit ialah [`8b9a050`](https://github.com/anhsbolic/kencleng/tree/8b9a0503d0c92f60434d704a3796b7329b0adebe) pada `validation-04-orchestrator-slice-2`. Harscode refs diverifikasi terhadap remote sebelum roadmap dibuat; Kencleng `8b9a050` diverifikasi terhadap remote saat freeze. Checkout pembacaan bersih.

**Evidence index pada Kencleng `8b9a050`:** [tracker](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/docs/project/kencleng-development-tracker.md), [evaluation report](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/docs/project/slice-2-progress-workflow-evaluation-2026-10-05.md), [evidence inventory and methods](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/docs/project/slice-2-harscode-evaluation-evidence-2026-10-05.md), [Work Graph](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/work-graph.md), [Events](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/events.md), [WU003 manifest](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/manifest.md), [WU008 manifest](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-008/manifest.md), dan [prepared Invocation](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-008/runs/EXP-S2-008-001/invocation.md). Untuk Stage 1, mulai dari report dan lampiran; ikuti links ke exact Run evidence, bukan menyimpulkan dari nama direktori.

- **Observed state:** tracker, Work Graph, Events, dan manifests selaras: WU003/WU008 `ACTIVE / PARKED`, `EXP-S2-008-001` prepared/undispatched. `CONTRACT_READY` dan `FRONTEND_MOCK_VERIFIED` earned dalam scope masing-masing; `BACKEND_VERIFIED`, `INTEGRATED_VERIFIED`, dan Slice completion belum earned. Exact WU003 [candidate](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/techplan.candidate.md) tetap Draft / In Review; SHA-256 `e895a1da8b90e7f88c449651a9a46add59e1a1d610cce3cc7b739d0c12c30315` cocok dengan bytes pada commit. [RV10 findings](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/RV-S2-003-010/review-findings-1.md) dan launch record juga cocok dengan hash di Events. OI9 acceptance, exact candidate approval, dan positive migration-design Review tetap open.
- **Measurement boundary:** appendix menghitung 126 Run directories, 401 Space files, dan 507,312 whitespace words dari snapshot **`7e731f9` plus working tree setelah HOLD, sebelum event/report evaluasi ditambahkan**. Commit `8b9a050` memuat final report dan state HOLD; jangan klaim jumlah kata appendix direproduksi persis dari commit final, atau direktori Run = completed/dispatched Run. Minimum 44 Human hours adalah self-report untuk 11 tanggal kalender 2026-09-25–2026-10-05, bukan timesheet.
- **Evidence gaps:** tidak ada pemisahan actual Human time per phase versus Kencleng/Harscode, total AI cost/tokens, comparable before/after task, causal savings, atau full technical/security re-review. Evaluasi tidak menjalankan tests/runtime baru. Ini membatasi confidence dan desain ukuran Stage 5; bukan alasan menghapus gate assurance.

## Stage 1 diagnosis — evidence-backed, episode-scoped

Sample dipilih dari critical path dan positive outcome, bukan dari jumlah file. Pada Kencleng `8b9a050`, independent [RV-S2-003-005](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/RV-S2-003-005/review-findings-1.md) menemukan enam blocking schema/design gaps; [RV-S2-003-008](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/RV-S2-003-008/review-findings-1.md) menemukan replay `status_token` yang tidak dapat dipenuhi oleh one-way verifier. Itu **necessary assurance**: defect material ditemukan sebelum schema write. [TST-S2-004-001](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-004/runs/TST-S2-004-001/testing-report-001.md) memberi independent frontend mock evidence dan menyatakan batas backend/integration/security secara eksplisit. Exact Human/source acceptance, protected Tier-0 authorization, dan durable decision provenance juga menjaga authority; jangan dihitung otomatis sebagai waste.

Avoidable cost tampak pada [BLD-S2-003-002](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/BLD-S2-003-002/report.md), yang di-dispatch sebelum prerequisite migration-design Review yang sudah tertulis terpenuhi; Participant berhenti aman tanpa production write. [TP-S2-006-005](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-006/runs/TP-S2-006-005/report-techplan.md) memperbaiki Human report yang sebelumnya kehilangan applicable Interface Contract; Human digest-nya perlu, repair Run-nya dapat dicegah dengan first-pass completeness. [TP-S2-002-005](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-002/runs/TP-S2-002-005/launch-record.md) hanya menyelaraskan status ke approval yang sudah durable; ini mengikuti posture saat itu, sedangkan current `orchestration/run-contract.md` sudah mengizinkan bounded deterministic reconciliation bila semua pre/postconditions terpenuhi. Pengulangan frontier pada beberapa surface tercatat di [Stage A baseline](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/experiments/current-state-simplification/stage-a-baseline.md); saat itu surface masih setuju, jadi tidak boleh mengklaim sudah terjadi routing failure.

**Empat root causes prioritas untuk episode ini** (urut menurut critical-path impact dan bukti mekanisme, bukan jam/cost terukur):

1. **Cross-surface contract readiness terlambat.** WU002 `CONTRACT_READY` cukup untuk baseline contract, tetapi combined recovery/admission/storage scenarios baru membuka gap melalui RV005 dan RV008; WU005–008 dibentuk untuk concern yang berbeda, dengan WU008 masih parked/unaccepted. **Confidence:** tinggi untuk rework path, rendah untuk besaran biaya. **Batas:** sebagian owner decisions dan replay semantics memang baru muncul; tidak semua harus settled sejak Exploration. **Uji vNext:** sebelum dependent Build, jalankan beberapa scenario lintas source/API/persistence yang relevan; ukur open owner decisions dan material re-entry sesudah approval tanpa menunda scope independen yang sudah ready.
2. **Batch dispatch tidak selalu memeriksa prerequisite yang sudah diketahui.** BLD003002 memakai approval model/pairing tetapi tidak membawa positive migration-design Review yang disyaratkan plan; fail-closed Participant mencegah write. **Confidence:** tinggi untuk satu miss ini, belum cukup untuk klaim frekuensi sistemik. **Batas:** protected pairing dan migration Review tetap perlu; BLD003001 menghasilkan bounded cap projection meski whole spine belum selesai. **Uji vNext:** cek exact prerequisites untuk batch yang akan dijalankan dari existing plan/state sebelum dispatch; hitung Build yang STALLED karena gate tertulis terlewat dan capability/evidence yang dihasilkan per batch.
3. **First-pass artifact fidelity/completeness lemah pada beberapa handoff.** Missing Interface Contract memicu TP006005; [RV-S2-003-009](https://github.com/anhsbolic/kencleng/blob/8b9a0503d0c92f60434d704a3796b7329b0adebe/.harscode-spaces/s2-guest-donation-truthful-state/WU-S2-003/runs/RV-S2-003-009/review-findings-1.md) menemukan predecessor approval ditulis seolah berlaku pada successor. **Confidence:** tinggi untuk repeat repair, tidak ada model/time comparison. **Batas:** independent Review tetap bernilai karena menangkap salah reliance boundary; RV10 atas correction diminta Human, bukan universal required loop. **Uji vNext:** periksa applicable sections, authority/status provenance, exact approval target, dan file anchors sebelum handoff; catat repair Run yang hanya mengisi omitted required output atau salah provenance.
4. **Current-state projection dan mechanical lifecycle work terlalu sering ditulis ulang.** Stage A melihat frontier terulang pada manifest, Work Graph, Control Surface, Parent Outcome, tracker, dan Events; evaluasi menemukan prepared WU008 pointer HEAD/path stale. TP002005 menunjukkan status-only Participant path yang sekarang bisa dihindari secara kondisional. **Confidence:** tinggi untuk pengulangan dan contoh drift, rendah untuk effort savings. **Batas:** beberapa surface punya reader/function berbeda dan Stage A tidak menemukan contradiction; current deterministic path sudah ada, jadi belum perlu automation framework baru. **Uji vNext:** pakai owner per current fact dan pointer/projection yang cukup, lalu minta fresh session rekonstruksi frontier; ukur contradiction/stale pointer dan status-only Run yang lolos kriteria deterministic, tanpa menghapus event/provenance material.

**Assurance floor untuk Stage 2–5:** Human/project authority dan exact acceptance tetap mengendalikan product/security/source truth; protected writes memerlukan izin yang berlaku; material plan/schema/code changes mendapat independent Review dan applicable Testing; unfulfilled prerequisite harus fail closed; current state dan material history harus dapat direkonstruksi dari durable sources. Tidak ada bukti yang mendukung penghapusan gate hanya untuk menurunkan hitungan Run. Magnitude/ROI empat penyebab di atas belum terukur; Stage 5 harus menguji efeknya terhadap capability **dan** safety.

## Stage 2 positioning candidate — awaiting Anhar

**Source status:** rekomendasi hasil pembacaan [`README.md`](../README.md), [`orchestration/protocol-v0.1.md`](../orchestration/protocol-v0.1.md), [`orchestrator-operating-model.md`](../orchestration/pilot-2-candidate/orchestrator-operating-model.md), [`workflow/AGENTS.md`](../workflow/AGENTS.md), [`product-design/README.md`](../product-design/README.md), dan diagnosis Stage 1. Ini belum settled decision atau perubahan canonical guidance. `main` tetap operational baseline; Human-Assisted dedicated Orchestrator adalah posture Pilot #2, bukan syarat universal untuk menggunakan Harscode.

**Rekomendasi identity:** Harscode adalah **panduan kerja modular untuk pengembangan software berbantuan AI, dari intent/authority proyek yang cukup jelas sampai capability yang diverifikasi**. Ia membantu Human dan agents menjaga keputusan dan sumber otoritatif, membatasi pekerjaan, menyimpan state yang dapat direkonstruksi, serta menghasilkan evidence yang proporsional dengan risiko. Kriteria evaluasi vNext adalah correct capability per coordination effort dengan assurance floor Stage 1.

**Authority dan koordinasi:** product/domain truth serta keputusan material Design, API, Security/Privacy, dan risk dimiliki owner yang dinamai proyek; Harscode menyediakan cara merutekan dan mengeksekusi keputusan itu. Human dapat menjadi Participant. Orchestrator agent, bila dipakai, mengoordinasikan Work Units/Runs, memfasilitasi pertanyaan decision-ready, dan merekonsiliasi durable state; ia tidak mendapat authority material atau menggantikan Explorer/Planner/Implementer/Reviewer/Verifier. Engineering workflow tetap dapat dipakai langsung tanpa Orchestrator. Physical Space, UI, model, dan dispatch mechanism adalah pilihan implementasi sesuai kebutuhan.

| Uji applicability | Jalur minimum yang cukup | Boundary yang diuji |
|---|---|---|
| Backend-only dengan product/API contract sudah accepted | Project truth → engineering Exploration → Techplan → Build → Review/Testing sesuai canonical applicability → exact delivery evidence; load best-practices terkait. | Tidak memerlukan product-brand/UI cycle atau Orchestrator/Space hanya karena Harscode dipakai. Security/financial gates tetap mengikuti risiko nyata. |
| End-to-end delivery dengan UI direction masih open dan dependensi lintas stack | Project owner menetapkan product truth → conditional product-design authority → engineering per bounded outcome; Orchestrator bila coordination topology memang perlu → integration dan independent evidence. | “End-to-end” mencakup design-to-engineering delivery untuk intent proyek, bukan mengambil alih strategi produk, market validation, atau project-specific truth. Frontend mock proof tidak menjadi real integration proof. |
| Bounded maintenance/bug fix | Project authority/current code → applicable engineering route dan bukti perubahan yang cukup. | Tidak otomatis membuat Work Graph, dedicated Space, Participant Profile, atau seluruh phase sebagai ceremony; phase applicability tetap mengikuti canonical workflow. |

**Challenge yang perlu disadari:** frasa “end-to-end product development” terlalu luas bila dibaca sebagai Harscode pemilik product discovery sampai business outcome. Current authority hanya mendukung reusable guidance dari project-owned intent ke verified software delivery, dengan product-design support saat diperlukan. Positioning yang lebih luas memerlukan authority dan real evidence baru; jangan dipromosikan dari wording roadmap ini.

**Decision request untuk Anhar:** terima atau koreksi rekomendasi identity, Human/Orchestrator posture, dan batas “end-to-end” sebagai **satu positioning decision**. Jika diterima, catat exact wording sebagai settled *episode decision* di dokumen ini. Itu tetap belum mengubah operational `main` atau candidate runtime policy; Stage 3 memakai keputusan tersebut sebagai lensa audit.

## Roadmap

### 0. Freeze Pilot #2 evidence baseline — COMPLETE

- **Objective:** tetapkan snapshot yang dapat direkonstruksi dan batas klaimnya.
- **Inputs/evidence:** exact Harscode dan Kencleng revisions di atas; tracker HOLD, evaluation report, inventory, Work Graph/Events/Run anchors yang dirujuk report.
- **Decisions:** apa yang masuk baseline, mana self-report/inventory versus runtime verdict, dan apa yang belum terukur.
- **Exit criteria:** exact refs dan evidence anchors diverifikasi; status HOLD/milestone/gates tercatat tanpa mengubah Kencleng state; gaps serta measurement limits eksplisit.
- **Output:** baseline evidence index dan open evidence gaps di dokumen ini.
- [x] Temukan source HOLD, evaluasi, inventory, dan dua repository revisions awal.
- [x] Verifikasi exact refs/anchors serta catat final baseline dan evidence gaps.
- [x] Baseline dapat dibaca fresh session dari immutable refs dan evidence index di atas.

### 1. Separate necessary assurance cost from avoidable workflow cost — COMPLETE

- **Objective:** identifikasi 3–5 root causes utama, dampak, dan confidence.
- **Inputs/evidence:** baseline Stage 0; contoh review yang menemukan defect material, late contract changes, status-only work, premature dispatch, repeated state/projection updates, fidelity repairs.
- **Decisions:** biaya yang menjaga correctness/authority/safety versus biaya yang dapat dihindari; hubungan sebab-akibat yang supported versus dugaan.
- **Exit criteria:** tiap root cause punya concrete episode anchors, counterexample/batas, serta mekanisme perbaikan yang bisa diuji; tidak mengklaim time/cost savings yang belum diukur.
- **Output:** ranked cause map dan assurance floor.
- [x] Klasifikasikan sample critical path, bukan seluruh file berdasarkan jumlahnya saja.
- [x] Catat empat root causes prioritas, confidence/batas, uji vNext, dan assurance floor di atas sebagai working diagnosis episode.

### 2. Settle Harscode identity dan positioning — AWAITING ANHAR

- **Objective:** jelaskan problem utama, Human versus orchestration-agent posture, dan modular applicability dari backend-only sampai end-to-end product development.
- **Inputs/evidence:** cause map; `README.md`/current operational authority; Pilot #2 operator/Participant evidence dan target-project boundary.
- **Decisions:** identity yang cukup presisi untuk memandu vNext; bagian yang invariant versus optional/conditional.
- **Exit criteria:** statement yang bisa diuji terhadap kasus backend-only dan end-to-end; Human authority, product truth, dan agent coordination boundary tidak ambigu.
- **Output:** explicit identity/positioning decision record di sini, bukan perubahan runtime policy otomatis.
- [x] Uji framing terhadap backend-only, end-to-end, dan bounded maintenance; check terhadap authority serta counterexample Pilot #2.
- [ ] Anhar menerima/mengoreksi wording dan boundary; catat settled episode decision, owner, dan rationale.

### 3. Audit lifecycle dan artifact dari outcome — PENDING

- **Objective:** nilai setiap handoff/artefak terhadap capability, assurance, dan reconstructability yang diberikannya.
- **Inputs/evidence:** Stage 0–2; actual Pilot #2 artifacts dan current owners untuk Exploration, Techplan, Review, Build, Testing, Work Unit, Run, Participant Profile, Invocation, dan Orchestration.
- **Decisions:** keep/refine/remove/conditional per concern, berdasarkan function dan failure mode; pisahkan semantic/authority requirement dari file layout atau tooling mechanism.
- **Exit criteria:** tiap concern punya tujuan, cost, observed failure, necessary evidence/gate, dan kandidat penyederhanaan dengan containment.
- **Output:** outcome-oriented audit matrix, dengan references ke owning guidance; belum mengedit protected/canonical guidance.
- [ ] Audit Exploration, Techplan, Review, Build, dan Testing.
- [ ] Audit Work Unit, Run, Participant Profile, Invocation, dan Orchestration.

### 4. Design minimal Harscode vNext candidate — PENDING

- **Objective:** buat perubahan sekecil mungkin yang mengatasi root causes tanpa kehilangan assurance floor.
- **Inputs/evidence:** identity decision dan audit matrix.
- **Decisions:** candidate semantics, explicit non-goals, authority owner, migration/reversibility, dan perubahan mana yang perlu proposal/protected approval.
- **Exit criteria:** tiap perubahan punya causal rationale, expected effect, safeguard, observable test, serta fallback; tidak ada framework baru tanpa problem nyata.
- **Output:** bounded candidate spec/proposals pada owning repo area; tautkan exact revisions di sini.
- [ ] Pilih perubahan minimal dan petakan owner/gate.
- [ ] Review consistency terhadap operational `main` dan target-project authority.

### 5. Bounded CRTV with explicit measures — PENDING

- **Objective:** uji candidate dalam real task yang disetujui Human dan comparable sebisanya.
- **Inputs/evidence:** frozen candidate revision, baseline Stage 0, authorized target scope, current project state, required independent verification.
- **Decisions:** scope dan stop conditions sebelum run; data apa yang feasible dicatat tanpa telemetry framework.
- **Exit criteria:** ada observed capability outcome dan safety/authority evidence; catat coordination effort (Human time bila tersedia, Run/re-entry beserta sebab, prerequisite misses, duplicated work, first-pass completeness), serta perbedaan scope dan missing data.
- **Output:** CRTV report dengan exact refs dan outcome versus cost; bukan pass/fail dari jumlah dokumen atau target savings arbitrer.
- [ ] Predeclare scope, measures, assurance floor, dan stop conditions.
- [ ] Jalankan hanya setelah authorization/resume yang berlaku; kumpulkan evidence.

### 6. Keep / Refine / Reject — PENDING

- **Objective:** evaluasi tiap candidate change dari hasil CRTV, bukan preferensi desain.
- **Inputs/evidence:** Stage 5 report, deviations, regressions, dan independent findings.
- **Decisions:** keep/refine/reject per change, confidence, unresolved risk, dan perlu/tidaknya eksperimen tambahan.
- **Exit criteria:** keputusan menyebut observed effect, downside, dan evidence limit; refinement yang material kembali ke bounded CRTV.
- **Output:** decision record serta exact candidate revision yang diterima atau ditolak.
- [ ] Putuskan tiap change; jangan mempromosikan hypothesis sebagai proven.

### 7. Promotion decision — PENDING

- **Objective:** putuskan apakah dan apa yang layak dipromosikan ke `main`.
- **Inputs/evidence:** Stage 6 decisions; compatibility/authority review; current `main` dan branch revisions; outstanding risks.
- **Decisions:** promote, partial promote, atau defer/reject oleh Anhar; scope dan urutan proposal/merge jika berlaku.
- **Exit criteria:** keputusan eksplisit dengan exact changes, assurance evidence, containment/fallback, dan unresolved items; tidak ada silent promotion.
- **Output:** promotion decision record di sini; merge/operational status berubah hanya lewat action terpisah yang authorized.
- [ ] Presentasikan promotion case dan residual risks untuk Human decision.
- [ ] Catat keputusan dan exact revisions; eksekusi promotion hanya bila diotorisasi.

## Parked sampai semantics settled

- `workspace.harscode.dev` dan public documentation/productization.
- Graph/memory management.
- Big tooling/automation framework.

Reopen item hanya jika evidence baru menunjukkan ia perlu untuk correctness/operability episode ini atau setelah Stage 2–4 settle relevant semantics. Catat alasan di decision record sebelum mengubah scope.

## Decision record

| Date | Class | Decision / status | Evidence and owner |
|---|---|---|---|
| 2026-10-05 | Working decision | HOLD Kencleng Slice 2 development; Post-Pilot #2 evaluation proceeds; no promotion now. | Anhar instruction; Kencleng tracker at `8b9a050`. |
| 2026-10-05 | Evaluation baseline | Freeze Stage 0 pada Harscode `63ec4e0`/`main@b64fa11` dan Kencleng `8b9a050`; appendix tetap dibaca sebagai pre-report snapshot `7e731f9` plus working tree. | Exact refs/anchors dan selected hashes diverifikasi; evidence index dan limits di atas. Ini bukan policy atau resume decision. |
| 2026-10-05 | Working diagnosis | Stage 1 memprioritaskan empat root causes di atas; assurance floor dipertahankan untuk audit dan CRTV. | Kencleng `8b9a050` report plus sampled Run artifacts; Harscode `orchestration/run-contract.md` current candidate semantics. Bukan settled Harscode policy atau measured causal savings. |
| 2026-10-05 | Recommendation pending | Stage 2 positioning candidate di atas menunggu keputusan Anhar. | Current Harscode `main`/pilot guidance dan Stage 1 diagnosis; belum mengubah operational/canonical policy. |
