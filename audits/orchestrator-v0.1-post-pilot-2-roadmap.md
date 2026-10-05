# Orchestrator v0.1 — Post-Pilot #2 Roadmap

> Status: Stage 0 COMPLETE — baseline dibekukan; Stage 1 berikutnya, stages 2–7 belum dimulai.
> Scope: progress dan keputusan episode Post-Pilot #2 pada branch `pilot/orchestrator-v0.1`; bukan runtime guidance atau canonical Harscode policy.
> Next action: klasifikasikan sample critical path menjadi necessary assurance cost versus avoidable workflow cost, lalu uji 3–5 root causes pada Stage 1.

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

### 1. Separate necessary assurance cost from avoidable workflow cost — PENDING

- **Objective:** identifikasi 3–5 root causes utama, dampak, dan confidence.
- **Inputs/evidence:** baseline Stage 0; contoh review yang menemukan defect material, late contract changes, status-only work, premature dispatch, repeated state/projection updates, fidelity repairs.
- **Decisions:** biaya yang menjaga correctness/authority/safety versus biaya yang dapat dihindari; hubungan sebab-akibat yang supported versus dugaan.
- **Exit criteria:** tiap root cause punya concrete episode anchors, counterexample/batas, serta mekanisme perbaikan yang bisa diuji; tidak mengklaim time/cost savings yang belum diukur.
- **Output:** ranked cause map dan assurance floor.
- [ ] Klasifikasikan sample critical path, bukan seluruh file berdasarkan jumlahnya saja.
- [ ] Settle 3–5 root causes dan assurance floor berbasis evidence.

### 2. Settle Harscode identity dan positioning — PENDING

- **Objective:** jelaskan problem utama, Human versus orchestration-agent posture, dan modular applicability dari backend-only sampai end-to-end product development.
- **Inputs/evidence:** cause map; `README.md`/current operational authority; Pilot #2 operator/Participant evidence dan target-project boundary.
- **Decisions:** identity yang cukup presisi untuk memandu vNext; bagian yang invariant versus optional/conditional.
- **Exit criteria:** statement yang bisa diuji terhadap kasus backend-only dan end-to-end; Human authority, product truth, dan agent coordination boundary tidak ambigu.
- **Output:** explicit identity/positioning decision record di sini, bukan perubahan runtime policy otomatis.
- [ ] Uji framing terhadap dua bentuk project dan counterexample Pilot #2.
- [ ] Catat decision, owner, rationale, dan unresolved questions.

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
