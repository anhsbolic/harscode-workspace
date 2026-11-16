# Product Kickoff Prompt

> **Standing:** OPTIONAL RESEARCH CONVERSATION AID / NEW EXACT CONTENT HUMAN REVIEW PENDING. This prompt helps start bounded Product inquiry using the selected [Product Definition](product-definition.md), [Authority & Approval](authority-and-approval.md) and [Consumer Handoff](consumer-handoff.md). It is **not** a Product process requirement, binding source, approval gate, Agent instruction, Space invocation, or automatic repository-write authorization.

## Use

Supply the actual **target project repository/branch** and the **current effective Product foundation or other legitimate project-owned sources**. A Product Intent may be the foundation when the project has one; do not invent one when it does not. Replace the placeholders below and paste only the prompt into a new discussion. The assistant must inspect the current sources rather than assume a pinned checkpoint or conversation memory is authority.

## Copy-paste prompt

Kita akan mengerjakan Product untuk **<nama-project>** menggunakan **Harscode Product Definition** sebagai panduan.

Sumber awal:
- **Project:** <repository, branch, dan source Product yang berlaku, misalnya Product Intent jika ada>, beserta authority, evidence, dan standards yang relevan.
- **Harscode:** <repository dan branch/ref yang sengaja dipilih>, khususnya `product/` untuk Product responsibility, I/P/O/O, authority, dan consumer handoff.

Verifikasi dan pahami sumber-sumber tersebut terlebih dahulu. Source of truth Product tetap berada pada project; Harscode adalah reusable guidance, bukan pemilik keputusan Product project.

Berdasarkan sumber yang sah dan kebutuhan nyata project, bantu aku menentukan:

1. **Product outputs dan desired outcomes apa yang benar-benar diperlukan?**
2. **Mana yang sudah cukup tersedia, mana yang masih perlu dikerjakan, dan apa uncertainty/authority gap yang material?**
3. **Dari mana paling tepat kita mulai, apa dependensi materialnya, dan kapan pekerjaan Product cukup untuk consumer atau keputusan berikutnya?**

Jangan memaksakan tahapan, dokumen, mandatory output packet, atau urutan workflow. Nilai kebutuhan berdasarkan semantic responsibility, evidence, legitimate authority, dan actual consumer needs. Jangan menjadikan Product owner dari UX flow, UI design, atau Engineering mechanism.

Challenge asumsi yang material, berikan satu starting recommendation yang paling masuk akal, lalu ajak aku memulai pembahasan Product dari titik tersebut.

**Jangan mengubah repository atau menerima Product commitments baru tanpa persetujuan Human yang berwenang.** Jika sumber tidak dapat diakses, jelaskan gap verifikasinya secara eksplisit.

## Intended result (not a mandatory artifact packet)

The first response should identify the **minimum justified output/outcome needs**, what effective project information already satisfies them, what remains unresolved, and **one concrete starting decision or inquiry**. The Product work itself is sufficient only when an actual receiving responsibility can make its permitted decision from legitimate, reconstructable Product meaning without inventing consequential rules. Exploration may begin with labeled hypotheses; binding downstream commitments require appropriate project approval.

This prompt does not itself produce or approve four files, impose a staged Product process, or prove UX/Engineering readiness. Keep discoveries and approvals in their **owning project** when persistence is warranted.
