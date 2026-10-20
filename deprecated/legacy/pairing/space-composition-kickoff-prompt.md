# End-to-End Space I/O Chain — Balad Kickoff Prompt

> **Status:** EXPERIMENTAL, Station 5 research. An optional **Human-facing starting prompt** for a **read-only Balad/Pairing assessment in Codex CLI**; not a mandatory phase, a Space definition or an authorization to form/invoke a Space.
> **Apply:** [Pairing](AGENTS.md) and [Space Composition / Formation Request](space-formation.md). Reusable Space design/formation belongs to [Anhar + ChatGPT](../space-formation/README.md).

## Reusable kickoff template

Replace the project/commitment pointer with what you know. A repository link, working directory, branch, approved artifact or simple commitment name is sufficient **if Balad can discover the rest**. Do not make the Human supply a long requirements package.

```text
Lur, kita evaluasi kebutuhan Harscode Spaces untuk menyelesaikan [PROJECT / COMMITMENT].

Periksa current authoritative inputs dan kondisi proyek yang relevan. Petakan end-to-end input/output chain dari titik awal sampai verified outcome, termasuk dependensi paralel bila memang diperlukan.

Cari reusable Space yang benar-benar tersedia dan nilai kecocokan kontraknya dengan kebutuhan proyek. Jika ada capability gap, siapkan Formation Request untuk direview bersama Anhar + ChatGPT.

Kita diskusi read-only dulu. Jangan mengubah file, membentuk Space, dispatch Agent, atau menjalankan engineering.
```

## Example — Kencleng C1 pilot

```text
Lur, kita lanjut pilot Station 5 Harscode menggunakan C1 Kencleng.

Evaluasi end-to-end Space I/O chain untuk menyelesaikan C1. Periksa authority proyek dan existing Spaces yang benar-benar tersedia; tunjukkan compatibility atau gap yang material. Bila perlu Space baru, berikan Formation Request untuk kita review.

Kita diskusi dulu, belum ada file writes, Space Formation, invocation, atau engineering execution.
```

## Expected Balad behavior (not a rigid output template)

From the short request, Balad should independently inspect effective authority and checked Space sources; give **one compact end-to-end outcome/capability map**, distinguish **generic reusable IN/OUT** from **project-specific binding**, identify decisive **producer OUT → consumer IN** compatibility/gaps, and name the nearest justified **reuse/adapt/form** opportunity. When a reusable capability is missing, provide a Formation Request with evidence and unresolved dependencies. Report any inaccessible source or unknown rather than declaring all Spaces absent.

**Do not:** require the Human to spell out every I/O contract in the prompt; force a fixed number of Spaces or an engineering-phase pipeline; turn an assessment into a design/implementation dossier; claim provisional mapping is execution evidence. Balad's output ends at **Formation Request**. Anhar + ChatGPT separately decide and author reusable definitions, and actual invocation requires its own authorization.

For a casual readiness question, a shorter prompt is valid. This example calibrates **who discovers and reports what**, not the amount of narration required.
