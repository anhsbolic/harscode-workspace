# Product Contract — Template Reusable I1 v0.1 (Draf Bahasa Indonesia)

> **Status:** USULAN RISET / BELUM DISETUJUI SEBAGAI KEBIJAKAN OPERASIONAL HARSCODE. Ini adalah template penyusunan **output Product**, bukan kontrak wajib baru untuk Rancang, Product Space, atau tahap runtime.
> **Pemilik concern:** Product Harscode. **Makna Product, revisi yang disetujui, serta konvensi dokumen spesifik tetap dimiliki proyek tujuan dan Human yang berwenang.**
> **Acuan consumer:** Input `I1` Rancang pada [definisi v3 yang memperoleh formation approval, commit `4b49d0dd0db74cf34a927cadc938ae724676a75a`](https://github.com/anhsbolic/harscode-workspace/blob/4b49d0dd0db74cf34a927cadc938ae724676a75a/engineering/spaces/feature-solution-design/contracts.md) — **research-only, runtime belum terverifikasi**. `I2` (constraint Design/arsitektur/keamanan), `I3` (repository/kode/lingkungan), dan `I4` (penugasan dan izin langsung dari Human) tetap terpisah.
> **Padanan bahasa:** [Template English v0.1](product-contract-template-draft.md) memiliki struktur dan tujuan yang sama. Gunakan **satu bahasa** untuk satu artefak, bukan dua salinan Product Contract yang sama-sama authoritative.
> **Konteks evaluasi:** Template reusable ini akan diuji pada satu outcome Product Kencleng. Aturan peran, entitas, dan acceptance spesifik Kencleng tetap milik Kencleng, **bukan aturan generik Harscode**.
> **Pilihan desain:** Menstandarkan **struktur makna**, bukan jumlah file, perluasan PRD wajib, mekanisme workflow, ataupun hubungan satu outcome = satu Space. Jika proyek sudah memiliki template authoritative yang memenuhi kebutuhan consumer, gunakan template proyek itu.

## Identitas artefak dan authority

| Informasi | Makna yang perlu tersedia |
| --- | --- |
| Proyek dan outcome terbatas | `<proyek, kode, hasil Product yang ingin dicapai>` |
| Product owner | `<Human/pemilik kewenangan Product>` |
| Status dokumen | `DRAFT / PROPOSED / APPROVED` berdasarkan evidence nyata |
| Revisi artefak | `<path + commit/blob SHA>` setelah artefak tersebut benar-benar ada |
| Persetujuan dan lingkup | `<keputusan, pemberi approval, outcome, revisi tepat, waktu/rujukan>`; `BELUM DISETUJUI` jika belum ada |
| Sumber Product dan urutan authority | `<dokumen sumber dan revisi; pisahkan binding, proposal, riset, dan evidence>` |
| Lingkup keberlakuan | `<proyek, ruang lingkup, kondisi berlaku, pengecualian>` |
| Consumer | `<contoh: Rancang I1 atau pemilik Design; klaim kecocokan dan batasannya>` |

Menggunakan template ini **tidak otomatis** menghasilkan Product Contract yang mengikat. Input `I1` yang sah memerlukan outcome, perilaku, acceptance, dan rujukan sumber **yang benar-benar disetujui pada revisi spesifik**, serta pemeriksaan kecocokan consumer ketika akan digunakan.

## 1. Outcome Product dan Success Criteria

Jelaskan secara ringkas **siapa**, **dalam situasi apa**, **dapat melakukan tindakan bermakna apa**, **kebenaran/keadaan Product apa yang berubah**, dan **mengapa perubahan itu penting**. Nyatakan juga hal yang **tidak otomatis** dijanjikan oleh outcome ini.

**Pernyataan outcome:** `<Dalam situasi ..., aktor ... dapat ..., sehingga ... benar-benar terjadi dan hasilnya dapat dipahami atau diperiksa kembali ...>`

**Success Criteria (SC):** Kondisi pada **level outcome** yang harus dapat diperiksa untuk menyatakan keberhasilan secara sah. Gunakan jumlah minimum yang cukup, bukan resep teknis atau target pertumbuhan pengguna.

| ID | Kondisi outcome yang harus benar | Batas makna / hal yang tidak dijamin | Sumber dan keputusan pendukung |
| --- | --- | --- | --- |
| `SC-01` | `<kondisi hasil yang benar-benar harus terwujud>` | `<apa yang tidak dibuktikan oleh kondisi ini>` | `<sumber/revisi tepat, APPROVED atau PROPOSED>` |

Jika beberapa kondisi **harus terpenuhi bersama**, sebutkan secara eksplisit. Success Criteria yang material tetapi masih `PROPOSED` **belum boleh diperlakukan sebagai kondisi keberhasilan yang disetujui**. KPI/metrik bisnis berbeda dari kriteria keberhasilan outcome, kecuali relevansinya memang diputuskan Product owner.

## 2. Pengalaman Aktor dan Makna Konsekuensinya

Catat momen yang bermakna bagi aktor. **Jangan otomatis menetapkan layar, waktu login, urutan API, atau teknologi interaksi.**

| Momen | Apa yang perlu dapat dilakukan, dipahami, atau disimpulkan aktor secara sah | Akibat Product dan batas klaimnya |
| --- | --- | --- |
| Kondisi awal | `<situasi, klaim, hal belum pasti>` | `<keadaan awal yang sebenarnya>` |
| Sebelum akibat penting berlaku | `<konsekuensi, kewenangan, batas yang perlu dipahami>` | `<apa yang belum dan akan berlaku>` |
| Tindakan | `<tindakan bermakna yang boleh dilakukan aktor>` | `<hasil bila syarat terpenuhi>` |
| Berhasil dan diperiksa kembali | `<hasil yang dapat dipahami atau diperiksa kemudian>` | `<keadaan sebenarnya dan makna yang bertahan>` |
| Ditolak, gagal, sebagian, atau belum pasti (jika material) | `<apa yang berbeda dari keberhasilan>` | `<apa yang tidak boleh diklaim>` |

Jelaskan alasan jika momen tertentu tidak berlaku. Ilustrasi pengalaman **tidak** otomatis menjadi aturan Product yang disetujui.

## 3. Perilaku Product, Kewenangan, dan Invariants

| ID | Perilaku / kewajiban semantik Product | Kewenangan aktor dan syarat | Invariant / kesimpulan terlarang | Sumber dan status |
| --- | --- | --- | --- | --- |
| `REQ-01` | `<apa yang wajib benar, bukan mekanisme>` | `<aktor, kewenangan, keadaan>` | `<apa yang tidak boleh dianggap benar>` | `<sumber/revisi tepat; APPROVED atau PROPOSED>` |

Kontrak yang **mengikat** tidak boleh diam-diam memuat aturan material `PROPOSED`. Minta keputusan pemilik authority atau persempit scope beserta konsekuensi pada Success Criteria dan Acceptance Criteria. Pilihan implementasi yang didelegasikan tetap milik Design/Engineering.

## 4. Acceptance Criteria dan Pemeriksaan Batas Makna

**Acceptance Criteria (AC)** memeriksa apakah perilaku Product memenuhi aturan dan **Success Criteria**. Success Criteria menyatakan *kapan outcome berhasil*; AC menyatakan *pengamatan apa yang membuktikan atau membantah klaim tersebut*.

| ID | Requirement dan Success Criteria terkait | Skenario (positif, ditolak, gagal, sebagian, belum pasti) | Hasil yang dapat diperiksa | Klaim salah yang harus dicegah |
| --- | --- | --- | --- | --- |
| `AC-01` | `REQ-01 / SC-01` | `<kasus relevan>` | `<hasil yang dapat diamati dan sesuai makna Product>` | `<sukses palsu, kewenangan atau verifikasi yang tidak sah>` |

Cakup hanya kasus material. Acceptance yang dirumuskan **bukan bukti** bahwa tes software sudah dieksekusi atau kemampuan sudah delivered.

## 5. Dependencies, Cakupan, dan Kebebasan Solusi

| Hal | Penjelasan yang dibutuhkan |
| --- | --- |
| Prasyarat Product yang nyata | `<perilaku yang diperlukan; tersedia / tidak tersedia / belum diverifikasi>` |
| Bukti atau sinyal lintas concern | `<bukti atau pemilik lain yang material; status observasi>` |
| Hasil dalam cakupan | `<outcome/perilaku yang dijanjikan>` |
| Pengecualian eksplisit | `<hal yang tidak dijanjikan atau tidak otomatis benar>` |
| Kebebasan Design | `<interaksi, penyampaian informasi, keputusan visual dalam batas Product>` |
| Kebebasan Engineering | `<arsitektur, state, interface, penyimpanan, transaksi, mekanisme pengujian>` |
| Rujukan constraint lain yang diketahui | `<pemilik/sumber I2/I3 yang relevan, tanpa menganggap I1 menyetujui atau memenuhi I2/I3>` |

Dokumen spesifikasi, mock, diagram, implementasi historis, atau seeded data **bukan bukti** prasyarat Product sudah tersedia di runtime.

## 6. Open Decisions & Blockers

| Pertanyaan dan klaim yang terpengaruh | Pemilik keputusan | Status | Konsekuensi blocker / keputusan yang dibutuhkan |
| --- | --- | --- | --- |
| `<pertanyaan Product spesifik>` | `<Human yang berwenang>` | `OPEN / PROPOSED / PARKED` | `<SC/REQ/AC terdampak atau alasan tidak blocking>` |

`OPEN` **tidak otomatis mendesak**. Hanya pertanyaan yang material untuk outcome yang sedang dikontrakkan yang harus diselesaikan sebelum revisi `I1` tersebut menjadi binding. Jangan otomatis menyalin keputusan dari paket historis. **Potential Conflicts**, jika relevan, adalah kategori keadaan yang perlu dijelaskan secara spesifik di kontrak hasil, bukan kewajiban mendeteksi semua konflik secara universal.

## 7. Kesiapan Konsumsi dan Batas Handoff

| Hal yang diperiksa | Evidence atau status nyata |
| --- | --- |
| Makna Product disetujui pada revisi sumber tepat? | `<APPROVED / PROPOSED / BLOCKED dan bukti>` |
| Outcome, SC, pengalaman, aturan, invariant, dan AC konsisten? | `<rekonsiliasi yang dilakukan dan keterbatasannya>` |
| Tidak ada keputusan Product material tersembunyi? | `<temuan atau blocker dengan pemiliknya>` |
| Ketersediaan prasyarat dan sinyal eksternal dijelaskan dengan jujur? | `<diamati / hilang / belum diverifikasi>` |
| Cocok dengan kontrak generik Rancang `I1`? | `<diperiksa / kondisional / belum diverifikasi; acuannya>` |
| Cocok untuk consumer pada penugasan proyek tertentu? | `<diperiksa / kondisional / terblokir / belum diverifikasi; buktinya>` |

**Kesimpulan handoff:** `<DRAFT — BELUM SIAP / PRODUCT DISETUJUI TAPI KECOCOKAN CONSUMER BELUM DIBUKTIKAN / I1 DISETUJUI UNTUK SCOPE SPESIFIK / BLOCKED>` sesuai evidence, bukan sekadar struktur template lengkap.

Artefak ini hanya menyediakan makna Product milik `I1`. **Tidak** menyediakan `I2`, `I3`, atau `I4`; tidak membentuk atau menjalankan Space, dan tidak memberi izin Engineering. Bila proyek tujuan mempunyai format efektif yang berbeda, selaraskan dengan pemilik dan kontrak consumer, bukan membuat sumber utama kedua.

## 8. Informasi Material Tambahan (Kondisional)

Isi **hanya jika ada informasi penting** untuk memahami Product atau dikonsumsi oleh consumer yang benar-benar tidak cocok di bagian 1–7.

Setiap butir perlu menyebut **apa yang penting**, **mengapa tidak cocok di bagian standar**, **sumber dan statusnya**, **risiko bila disalahartikan**, serta **pemilik/langkah lanjut** bila relevan.

Jika tidak ada, tulis `Tidak ada informasi material tambahan.`

**Bukan tempat menyembunyikan aturan:** Requirement mengikat, invariant kritis, Success Criteria, acceptance, batas keamanan, blocker material, dan keputusan Product OPEN tetap berada pada bagian pemiliknya. Catatan tambahan tidak menciptakan authority baru.

---

## Catatan untuk consumer: referensi upstream

**Tuliskan catatan berikut (atau padanan yang setara) pada akhir setiap Product Contract yang memakai template ini:**

> **Catatan referensi upstream:** Kode dan tautan sumber di dokumen ini digunakan oleh Product untuk provenance, pencatatan keputusan, dan audit upstream. Consumer downstream, termasuk Rancang, **tidak perlu menelusuri atau memvalidasi ulang sumber riset Product maupun mengartikan kode referensi upstream untuk mendapatkan aturan tambahan**. Seluruh makna Product yang mengikat untuk outcome ini harus tertulis langsung dalam Product Contract pada revisi yang disetujui. ID `SC`/`REQ`/`AC` boleh digunakan untuk keterlacakan **di dalam kontrak ini**. Pemeriksaan keaslian approval, revisi `I1`, konsistensi isi kontrak, `I2/I3`, serta constraint keamanan tetap merupakan tanggung jawab consumer sesuai kontrak yang berlaku. Temuan kontradiksi material dikembalikan kepada pemiliknya, bukan diselesaikan dengan menyusun ulang Product requirements dari referensi upstream.

**Batas adopsi:** Definisi Rancang v3 yang sudah mendapat formation approval **masih** mewajibkan pemeriksaan sumber aslinya. Catatan ini menyatakan **target model handoff**; pengecualian upstream Product source re-check untuk Rancang memerlukan amendment dan formation approval baru pada revisi tepat, bukan berlaku otomatis karena template ini.

## Penerapan dan evaluasi

Draf ini adalah **usulan format reusable**, bukan gate penyelesaian universal. Uji pada Product Contract dari proyek nyata (pilot pertama: Kencleng O1), kemudian lakukan **uji pembaca baru / kecocokan consumer I1 yang benar-benar terpisah** sebelum mengusulkan adopsi operasional. Jika tidak memberi manfaat dibanding standar proyek yang ada, cukup jadikan panduan opsional. Approval template, jika diberikan, **berbeda** dari approval Product Contract yang memakainya dan berbeda dari formation/invocation Rancang.
