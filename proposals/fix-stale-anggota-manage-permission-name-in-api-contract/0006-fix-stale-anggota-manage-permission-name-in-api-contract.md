# Proposal: Fix Stale `anggota.manage` Permission Name in `API-D01-akun.yaml`

**Status:** Proposed
**Date:** 2026-09-12
**Origin:** Domain `akun` closure audit (`.agents-local/backend/domain-reports/D01-domain-akun-closure-audit.md`, Finding 2) — surfaced while cross-checking the API contract against currently-shipped code before considering the domain done.
**Proposed scope:** docs-only change to `docs/api/API-D01-akun.yaml`. Three single-line text swaps, no structural change to the file.
**Target area:** `docs/api/API-D01-akun.yaml` lines 89, 555, 607 — the D01-01 (`/api/stokis/members`) and D01-06 (`/api/stokis/members/pool`, `/api/stokis/members/pool/{member}/pick`) endpoint sections, both marked in the file's own header as already rewritten to match shipped code (unlike D01-04/05/07/09, which still use the old convention).

## Context

`Database\Seeders\PermissionSeeder.php` was rewritten from scratch as Task 10a (D01-tasks.md), compiling the permission catalog from `Otorisasi-KoperasiQu.md` §4. That catalog defines `account.manage-member-profile` as the permission gating a Stokis's ability to manage its own Anggota — not `anggota.manage`, which was never a valid domain tag under `Otorisasi-KoperasiQu.md` §3's naming convention (`account`, `catalog`, `due-zis`, `purchasing`, `program`, `incentive`, `recap`, `notification` — `anggota` isn't one of them). This rename is documented in `.agents-local/backend/domain-reports/task-10a-permission-seeder-and-anggota-manage-rename.md`, and confirmed complete in code: `grep -rn "anggota\.manage"` across `app/`, `routes/`, `tests/`, `database/` returns zero hits; every reference — `MemberPolicy`, `PermissionSeeder`, and every test file — uses `account.manage-member-profile`.

## The Drift

`API-D01-akun.yaml`'s own header states that its D01-01, D01-02, D01-03, and D01-06 sections were rewritten to match shipped code (proposal 0001 in the `docs/` repo — `project/proposals/0001-api-convention-shipped-code-authoritative.md` — and this repo's own proposal 0005 for the D01-06 section specifically). Despite that, three error-response descriptions in those already-"shipped-code-authoritative" sections still name the retired permission:

| Line | Section | Current text | Should read |
|---|---|---|---|
| 89 | D01-01, `POST /api/stokis/members`, `403` | `Bukan Stokis, atau tidak punya permission \`anggota.manage\`.` | `Bukan Stokis, atau tidak punya permission \`account.manage-member-profile\`.` |
| 555 | D01-06, `GET /api/stokis/members/pool`, `403` | `Bukan role stokis, atau role stokis tanpa permission anggota.manage.` | `Bukan role stokis, atau role stokis tanpa permission \`account.manage-member-profile\`.` |
| 607 | D01-06, `POST /api/stokis/members/pool/{member}/pick`, `403` | `Bukan stokis / tanpa anggota.manage, atau self-pick (I6.2).` | `Bukan stokis / tanpa \`account.manage-member-profile\`, atau self-pick (I6.2).` |

This is an ordering artifact, not a second divergent decision: proposal 0005 (which rewrote the D01-06 section to match shipped code) landed *before* Task 10a's permission rename — D01-06's build predates D01-08's exploration, where Task 10a actually ran, in the commit history. Nobody had reason to revisit these three lines afterward, since the sections themselves were otherwise already correct.

## Why Revise the Doc Rather Than Match Code to It

Not applicable in the usual sense — there's no genuine alternative reading here. `account.manage-member-profile` is the only permission name the shipped code, the seeder, and the canonical permission catalog (`Otorisasi-KoperasiQu.md` §4.1) agree on; `anggota.manage` doesn't exist anywhere in the current codebase and was already established (via the Task 10a rename, itself already recorded as a deliberate correction of ad hoc pre-catalog naming) as the name to retire. This proposal doesn't reopen any decision — it just finishes propagating one that already happened.

## Recommendation

Apply the three replacements in the table above verbatim. No other text in these sections needs to change — the surrounding error-code, status, and schema references are otherwise already correct and consistent with the code.

## Impact / Scope of Applying This

Documentation-only. No code, test, or seeder change — `account.manage-member-profile` has been the only name in use anywhere in the running application since Task 10a. Applying this proposal brings the API contract's text in line with code that has already been correct for some time; it doesn't change any behavior.

## What This Proposal Does NOT Do

- Does not edit `docs/api/API-D01-akun.yaml` directly — per `AGENTS.md` §5 and this repo's established proposal process, that file lives in a separate, authoritative repo an agent should not write to, even for a change this mechanical.
- Does not touch any other still-stale section of the same file (D01-04, D01-05, D01-07, D01-09 remain on the old Indonesian-path/RFC 9457 convention) — those are pre-existing, already-tracked, separate follow-ups (see that file's own header note and D01-09's manifest cross-cutting item), not part of this proposal's scope.
- Does not revisit or reopen the Task 10a rename decision itself — that's settled; this is purely finishing its propagation into one lagging document.
