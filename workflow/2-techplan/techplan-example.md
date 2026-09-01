# Tech Plan: Daily NIE Expiration Check (Cron + Reminder + Freeze)

> Ticket    : GMRT-51524
> Author    : Anhar Solehudin (@anhsbolic)
> Date      : 2026-08-10
> Updated   : 2026-08-13 
> Status    : Draft

---

## 1. Background

The catalog must check each Alat Kesehatan (ALKES) and Obat product's NIE expiration date daily and act on it: remind the seller at H-45/30/14, and freeze (take down) when the NIE has expired.

The data reality differs between the two categories. For ALKES, the KFA Kemenkes API returns `identifier_ids[].end_date` and the service already extracts it into a custom-form field (`ConstructCustomFormKFAAlkes`, `service.go:11707`), but never persists it to a dedicated column. For Obat, KFA does not reliably supply the NIE end date, so the seller must enter it manually via a "Masa Berlaku NIE" datepicker (`FormType = DATE`, added in migration `000122`); that value currently sits only in `product_custom_form_value`.

The cron therefore needs (a) a new `product_kfa.nie_expired_date` column + a `nie_expired_date_source` discriminator (`MEDICAL_DEVICES` for ALKES, `FARMASI` for Obat), (b) a backfill of existing ALKES rows from `identifier_ids`, (c) an upsert-side wiring so new/edited Obat rows populate the same column, and (d) a daily `/cron/nie-expiration` endpoint that reads the column and runs three branches. The schedule itself (00:01 WIB) is configured on an external scheduler — the service only exposes the endpoint.

## 2. Scope

**In scope:**
- New `product_kfa` columns `nie_expired_date DATE` + `nie_expired_date_source TEXT` (migration `000123`), with a check constraint. **No backfill in the migration** — the backfill is a separate batched local script (outside the codebase), run manually after `000123` deploys.
- Separate batched local script (outside the codebase) to backfill existing ALKES rows from `identifier_ids` into `nie_expired_date` with `source = MEDICAL_DEVICES`. Idempotent (`WHERE nie_expired_date IS NULL`), non-blocking on invalid dates (regex guard), batched by keyset pagination on `product_id` with per-batch commit. Run manually after `000123` deploys, before enabling the cron schedule.
- Separate Go script (outside the codebase) to backfill existing FARMASI rows from a stakeholder-provided spreadsheet into `nie_expired_date` with `source = FARMASI`. Skip rows that already have a `nie_expired_date` (log/report skipped count). Run manually when the spreadsheet is ready. **Spreadsheet not yet received** — see Active Open Item.
- New `PRODUCT_ACTION_REASON = NIE_EXPIRED` + map/label entries.
- New `NIE_EXPIRED_DATE_SOURCE_MEDICAL_DEVICES` / `_FARMASI` constants and `NIE_EXPIRED_REASON_TEXT`.
- Two new `/cron/nie-expiration/{alkes,farmasi}` POST endpoints sharing one parameterized service method with three branches (take-down, reminder, aman).
- Obat upsert wiring: extract seller "Masa Berlaku NIE" → `product_kfa.nie_expired_date` (source `FARMASI`).
- ALKES upsert wiring: extract from `identifier_ids` → `product_kfa.nie_expired_date` (source `KFA`).
- Reminder notification helper (direct `TriggerNotification`, deterministic `TransactionID`) using the existing generic in-app workflow `pnd-general-inapp` (constant `GENERAL_IN_APP_NOTIFICATION`, `constant.go:210`) — NOT a dedicated NIE workflow. Payload is two keys: `generalInAppContent` + `targetUrl`. Precedent: `buildKFADataChangedNotification` (`service.go:10138-10148`, GMRT-52308).
- `upsertProductKFA` OnConflict + `getProductKFAByProductIDs` SELECT updated for both new columns.

**Out of scope (explicit):**
- Novu workflow registration — **RESOLVED, not needed.** The reminder reuses the existing `pnd-general-inapp` workflow (already registered and in prod via GMRT-52308, `constant.go:210` `GENERAL_IN_APP_NOTIFICATION`). No new workflow registration required.
- External scheduler config for 00:01 WIB — infra, out of repo.
- Unfreeze after NIE renewal (PRD is freeze + reminder only).
- "Nomor Izin Edar Tidak Berlaku" (revoked) case — needs a Kemenkes revocation signal not in scope; only the date-based "Kadaluwarsa" case is handled.
- Backfill of existing Obat rows from `identifier_ids` (no KFA-derived NIE end date for FARMASI — backfill is via stakeholder spreadsheet, not extraction).
- Channel mix for the reminder (in-app / email / WhatsApp) — reminder is **in-app / on-site only** per PM clarification. `pnd-general-inapp` is a generic in-app workflow (in-app/feed channel step only, per GMRT-52308 techplan:838). Code does not enforce channels — that's a Novu template concern — but the shared workflow's in-app-only nature already matches the PM requirement.
- GraphQL schema change to `UpsertProductKFAInput` — not needed; seller value arrives via custom form.

## 3. Requirements

| Condition | Requirement | Source/Note |
|---|---|---|
| Daily cadence | Cron runs once at 00:01 WIB, externally triggered | PRD; clarification #2 (REST-only) |
| Pre-condition | Only products with non-NULL `nie_expired_date` are evaluated | PRD pre-condition; NULL = skip |
| Reminder | At H-45, H-30, H-14 (exact day), send reminder to seller's admin-company persona; status stays "Tayang" | PRD; Tech Lead 3.2 "Exact" |
| Take-down | When `nie_expired_date <= today` AND `status <> FREEZE`, freeze with reason `NIE_EXPIRED`; take-down notification fires for `ACTIVE_TO_FREEZE` | PRD re-read: `expiry == today` also takes down (R18 revised); Tech Lead direction (past = expired) kept, boundary aligned to PRD |
| Aman | Neither branch matches → no-op | PRD |
| Obat input | Seller "Masa Berlaku NIE" datepicker writes to `nie_expired_date` with `source = FARMASI`, format `YYYY-MM-DD` | Tech Lead 2.3.3; clarification #1, #5 |
| ALKES input | `identifier_ids` NIE end date (latest) writes to `nie_expired_date` with `source = MEDICAL_DEVICES` at upsert and via backfill | Tech Lead 2.2.1 |
| Idempotency | Same-day double-fire of cron must not double-send reminder | Tech Lead 3.2.1 "stateless" + deterministic `TransactionID` |
| Non-blocking | Invalid/missing date strings are skipped, not errored | Clarification #4 |

## 4. Rules & Validation

- **R1 (Take-down fires)** given a product with `nie_expired_date <= today` and `status <> FREEZE`, when the cron runs, then `FreezeUnfreezeProducts` is called with `ReasonEnum = NIE_EXPIRED`, `UserID = SYSTEM`, `PersonaID = SYSTEM`, and the product transitions to `FREEZE`. The boundary `expiry == today` is included (R18 revised).
- **R2 (Take-down notification, ACTIVE only)** given R1 with `status = ACTIVE` before the freeze, then the `ACTIVE_TO_FREEZE` notification (`pnd-product-status-changed`) fires via the Pub/Sub subscriber. Given `status` is non-ACTIVE, non-FREEZE (e.g., `BLOCKED`, `IN_REVIEW`), then the freeze still happens but NO notification fires (transition not in `PRODUCT_STATUS_CHANGED_FROM_TO`).
- **R3 (Take-down idempotent on re-fire)** given a product already `FREEZE`, when the cron runs, then `UpdateProductStatusWithReturning` returns no updated IDs; no duplicate action log, no duplicate notification.
- **R4 (Reminder H-45)** given `nie_expired_date == today + 45` and `status <> FREEZE`, when the cron runs, then a reminder notification is sent with `daysRemaining = 45`, `TransactionID = nie-reminder-<productID>-45-<expirationDate>`, and the product status is unchanged.
- **R5 (Reminder H-30 / H-14)** same as R4 with `+30` and `+14` respectively.
- **R6 (Aman)** given `nie_expired_date > today` and not in `{today+45, today+30, today+14}`, when the cron runs, then no action is taken.
- **R7 (NULL expiry skipped)** given `nie_expired_date IS NULL`, when the cron runs, then the product is excluded from both branches (SQL NULL semantics; defensive `IS NOT NULL` filter added).
- **R8 (Obat upsert, valid date)** given an Obat upsert with custom-form "Masa Berlaku NIE" value matching `YYYY-MM-DD`, when the upsert is processed, then `product_kfa.nie_expired_date` is set and `nie_expired_date_source = 'FARMASI'`.
- **R9 (Obat upsert, invalid date — preserve)** given an Obat upsert with an unparseable date string, then the error is logged (`logger.Error`) and the existing `nie_expired_date` is preserved (not overwritten with NULL). The product save succeeds — non-blocking. The seller is not forced to re-fill the field.
- **R10 (Obat upsert, empty date — preserve)** given an Obat update where "Masa Berlaku NIE" is empty/absent, then the existing `nie_expired_date` is preserved (not overwritten with NULL) via pre-fetching the existing `product_kfa` row before the OnConflict write. On a brand-new Obat insert with no date, `nie_expired_date` is NULL (correct — seller hasn't filled it yet). **Obat-only** — ALKES does not preserve (let it go to NULL if KFA stops supplying the date).
- **R11 (ALKES upsert)** given an ALKES upsert, then `nie_expired_date` is set from the latest matching `identifier_ids[].end_date` (where `code == nie`, `end_date != NULL`) with `source = MEDICAL_DEVICES`.
- **R12 (Backfill, ALKES valid)** given an existing ALKES row (`kfa_source = 'KFA_ALKES'`) with a matching `identifier_ids` entry whose `end_date` matches `^\d{4}-\d{2}-\d{2}$`, when the backfill script runs, then `nie_expired_date` is set and `nie_expired_date_source = 'MEDICAL_DEVICES'`.
- **R13 (Backfill, invalid date skipped)** given an ALKES row whose `end_date` does not match the regex, then the row is skipped (non-blocking); `nie_expired_date` stays NULL.
- **R14 (Backfill, FARMASI rows skipped)** given a row with `kfa_source = 'KFA_FARMASI'`, then the ALKES backfill does not touch it (Obat existing data left NULL).
- **R15 (Backfill idempotent)** given a row where `nie_expired_date IS NOT NULL` (e.g., set by Obat upsert), when the backfill SQL re-runs, then the row is not overwritten.
- **R16 (Reminder same-day dedup)** given the cron double-fires on the same day, then Novu dedups by `TransactionID`; one reminder per (product, milestone, expirationDate).
- **R17 (Reminder missed day not retried)** given the scheduler misses H-45 for a product, then on H-44 the filter does not match; the H-45 reminder is not retried (stateless + exact-day trade-off).
- **R18 (Take-down boundary — `expiry == today` IS take-down)** given `nie_expired_date == today`, when the cron runs, then take-down fires (same as R1). The product is frozen on its expiry day, not the day after. **Revised** after re-reading PRD: the PRD's "Expiration Date lebih dari atau sama dengan Today Date" was initially read as inverted Indonesian, but on re-read the boundary `== today` is intended to take down. The Tech Lead's strict `<` is overridden on this boundary only; the direction (past = expired) is kept. Previous version of this rule had a one-day grace — that is removed.

### Timeline reference (per product per expiry cycle)

The exact-day filters make the cron stateless — only three days produce reminders, and only the expiry day itself (and every day after) produces take-down. Every other day is a no-op.

| Timeline (relative to today) | Condition (filter) | Action | Notification | Status |
|---|---|---|---|---|
| `expiry > today+45` (far future) | no match | none (aman) | none | unchanged |
| `expiry == today+45` | reminder, milestone 45 | send reminder "akan habis dalam 45 hari" | reminder (Novu) | unchanged (Tayang) |
| `today+30 < expiry < today+45` | no match | none (aman) | none — H-45 already fired; H-30 not yet | unchanged |
| `expiry == today+30` | reminder, milestone 30 | send reminder "akan habis dalam 30 hari" | reminder (Novu) | unchanged |
| `today+14 < expiry < today+30` | no match | none (aman) | none — H-30 already fired; H-14 not yet | unchanged |
| `expiry == today+14` | reminder, milestone 14 | send reminder "akan habis dalam 14 hari" | reminder (Novu) | unchanged |
| `today < expiry < today+14` | no match | none (aman) | none — H-14 already fired; not yet expired | unchanged |
| `expiry == today` (R18 boundary — take-down fires) | take-down (branch 1) | freeze with `NIE_EXPIRED` | take-down notification **only if `ACTIVE_TO_FREEZE`** (R2) | `→ FREEZE` |
| `expiry < today` AND `status <> FREEZE` | take-down (branch 1) | freeze with `NIE_EXPIRED` | take-down notification **only if `ACTIVE_TO_FREEZE`** (R2) | `→ FREEZE` |
| `expiry <= today` AND `status = FREEZE` | excluded by `status <> FREEZE` | none (idempotent, R3) | none | `FREEZE` (unchanged) |

Total reminders per product per expiry cycle: **exactly 3** (H-45, H-30, H-14). Never more (exact-day filter, no window). Never fewer unless the scheduler misses a day (R17 — no retry).

## 5. Decision Log

| Option considered | Why rejected/accepted |
|---|---|
| **A. Take-down direction `expiry <= today`** (PRD boundary + Tech Lead direction) | **Chosen.** Direction (past = expired) per Tech Lead; boundary `== today` included per PRD re-read. Initial synthesis chose strict `<` (Tech Lead); revised after PM re-read PRD and confirmed `expiry == today` should also take down. The PRD's "lebih dari atau sama dengan" was inverted Indonesian for the direction, but the boundary `== today` is genuine. |
| B. Take-down direction `expiry < today` (Tech Lead strict) | Rejected on the boundary — one-day grace removed; `expiry == today` now takes down. Direction still matches Tech Lead (past = expired). |
| C. Take-down direction `expiry >= today` (PRD literal, inverted) | Rejected — would take down a product expiring *tomorrow* today; the PRD's "lebih dari" wording is inverted for the direction, only the "sama dengan" (== today) boundary is kept. |
| **A. Filter scope `status <> FREEZE`** (Tech Lead) | **Chosen.** Tech Lead governs. Accepted consequence: non-ACTIVE products frozen by the cron get NO take-down notification (R2). |
| B. Filter scope `status = ACTIVE` (PRD "Tayang") | Rejected by Tech Lead; kept as a one-line fallback if PM later wants narrower scope. |
| **A. Single column `nie_expired_date` + `nie_expired_date_source`** | **Chosen** (clarification #1). Obat and ALKES write to the same column, distinguished by source. |
| B. Two columns (`nie_expired_date` + `nie_input_expired_date`) | Rejected — redundant; source discriminator is sufficient. |
| **A. One freeze reason `NIE_EXPIRED`** | **Chosen.** Tech Lead's logic only produces the date-based "Kadaluwarsa" case. "Tidak Berlaku" (revoked) needs a separate Kemenkes signal, out of scope. |
| B. Two reasons (`NIE_EXPIRED` + `NIE_REVOKED`) | Rejected for this story/task; can be added later with the same pattern. |
| **A. Reason wording "Nomor Izin Edar Kadaluwarsa"** (PRD) | **Chosen.** PRD is authoritative for this story/task; "Kadaluwarsa" is more direct than migration 000032's "Masa Berlaku Nomor Izin Edar Habis" (different table, different flow). |
| B. Reuse migration 000032 wording | Rejected — conflates curation reject reason with freeze reason. |
| **A. `nie_expired_date` type `DATE`** | **Chosen.** PRD uses date-only language; cron comparison is exact-day. Avoids the 00:00:00 vs current-time ambiguity of `TIMESTAMPTZ`. |
| B. Type `TIMESTAMPTZ` | Rejected — forces a time-component decision every comparison. |
| **A. `nie_expired_date_source` type `TEXT` + CHECK** | **Chosen.** Two values; cheaper to evolve than a PG enum; matches `kfa_source` precedent (000091). |
| B. PG enum `CREATE TYPE` | Rejected — `ALTER TYPE` cost for a two-value set is not justified. |
| **A. Reminder idempotency: stateless + exact-day filter + deterministic `TransactionID`** | **Chosen** (Tech Lead 3.2.1 + 3.2). Filter is primary dedup; Novu `TransactionID` is same-day safety net. |
| B. Marker table for "already reminded" | Rejected — contradicts "stateless"; overkill given exact-day filter. |
| **A. Backfill via separate local script, batched, outside the codebase** | **Chosen.** Avoids holding a long lock during migration; batches keep each transaction short (keyset pagination on `product_id`, commit per batch); the script is run manually after `000123` deploys, so the operator controls timing. Idempotent by `WHERE nie_expired_date IS NULL` — safe to re-run. |
| B. Backfill via SQL `UPDATE` in migration `000123` | Rejected — the `jsonb_array_elements` UPDATE holds a lock proportional to row count; on a large table this blocks deploys. Moving the backfill out of the migration eliminates the lock risk entirely. |
| C. Go cron endpoint (`/cron/nie-backfill`) | Rejected — lingering endpoint + service-account config; one-shot operation doesn't justify it. |
| **A. Obat backfill via stakeholder-provided spreadsheet (Go script, outside codebase)** | **Chosen** (Tech Lead update). Stakeholder provides a spreadsheet with NIE expiry dates for existing Obat products. A Go script reads the spreadsheet and updates `product_kfa.nie_expired_date` with `source = FARMASI`. Skip rows that already have a `nie_expired_date` (log/report skipped count). Run manually when the spreadsheet is ready. **Spreadsheet not yet received** — see Active Open Item. |
| B. No backfill for Obat existing rows | Rejected (decision reversed) — original plan was "no Obat backfill; existing rows out of cron scope until seller edits". Tech Lead confirmed a stakeholder spreadsheet will be provided; existing Obat rows should be backfilled. |
| C. Set `source = 'FARMASI'` + NULL date for Obat | Rejected — makes "NULL means out of scope" ambiguous. |
| **A. One cron endpoint, three sequential branches** | **Chosen.** Branch 1 (take-down) error aborts branch 2 (reminder); reminder runs next day. Take-down is safety-critical. |
| B. Three endpoints | Rejected — three schedule entries, overkill for a daily job. |
| C. One endpoint with error isolation | Rejected — silent take-down failure worse than a visible abort. |
| **A. Two routes, one parameterized function (`/cron/nie-expiration/alkes` + `/cron/nie-expiration/farmasi`)** | **Chosen.** Operational isolation (disable/schedule/monitor per category) without code duplication. The cron's logic is identical across categories — only the filter on `nie_expired_date_source` differs. The two-route boundary lives at the handler/router layer; the service takes a `source` param. If the two ever genuinely diverge, split the function then (premature split now would duplicate ~150 lines of batch/reminder logic). |
| B. Two fully-separate cron endpoints + two service methods | Rejected — duplicates the batch/reminder/`getPersona`/`TriggerNotification` logic for no current divergence. |
| C. One endpoint, no category parameter (processes both) | Rejected — no operational isolation; a bad ALKES backfill can't be disabled without killing Obat coverage. |
| **A. Reminder via direct `TriggerNotification`** (Path A) | **Chosen.** Reminder is not a status change; Path B (Pub/Sub event) is built for status transitions. |
| B. Reminder via `EventProduct.NotificationSpec` (Path B) | Rejected — would force a status-change shape the reminder doesn't have. |
| **A. Reminder workflow = existing `pnd-general-inapp`** (constant `GENERAL_IN_APP_NOTIFICATION`, `constant.go:210`) | **Chosen** (PM update). The Novu workflow `pnd-general-inapp` is already registered and in prod (used by GMRT-52308's `buildKFADataChangedNotification`, `service.go:10138-10148`). Reusing it avoids Novu-config proliferation for a one-line in-app message + CTA. Payload contract is two keys: `generalInAppContent` (message body, interpolated Go-side) + `targetUrl` (CTA link). Precedent's payload (`service.go:10141-10144`) sends ONLY these two keys — no `subject`, `sellerCompanyName`, `productName`, `daysRemaining`, `expirationDate`, `role`, `personaId`, `institutionId`. The reminder follows the same minimal shape. |
| B. Reminder workflow = dedicated `pnd-seller-product-nie-expiry-reminder` (original techplan) | Rejected — PM confirmed `pnd-general-inapp` is the workflow to use. No new Novu workflow will be registered. The original Open Item #1 ("workflow not yet registered") is obsolete. |
| C. Reminder workflow = `pnd-product-status-changed` (the take-down workflow) | Rejected — that workflow is built for status transitions with `ACTIVE_TO_FREEZE`-shaped content (email + WhatsApp + in-app); the reminder has no status change and is in-app only. |
| **A. Reminder content interpolated Go-side** (`fmt.Sprintf` into `generalInAppContent`) | **Chosen** (matches GMRT-52308 precedent — `KFA_DATA_CHANGED_CURATION_NOTIFICATION_CONTENT` is a Go constant, not a Novu template variable). Simpler Novu template; the message string is the payload. |
| B. Reminder content interpolated Novu-side (send raw `productName` + `daysRemaining` as payload keys, let Novu build the string) | Rejected — diverges from the `pnd-general-inapp` contract (which reads only `generalInAppContent` + `targetUrl`); would require a different workflow or a custom Novu template function. |
| **A. Reuse existing `ACTIVE_TO_FREEZE` transition** | **Chosen.** PRD says "As it is"; take-down wording stays generic. Reason text goes to action log only. |
| B. New `NIE_EXPIRED_FREEZE` transition with custom wording | Rejected — contradicts PRD "As it is". |
| **A. Obat upsert wiring as separate step after `ConstructCustomFormKFAPharmacy`** | **Chosen.** The pharmacy construct is an overwrite function; Obat source is `FARMASI` (don't overwrite). |
| B. Add `Masa Berlaku NIE` to pharmacy `checkerMap` | Rejected — would overwrite the seller's value with KFA (wrong source). |
| **A. `getPersona` returns one persona per institution** | **Chosen** (verified `service.go:13112`, deduped). One reminder recipient per seller. |
| B. Send to all admin personas | Rejected — would require changing `getPersona`'s filter; out of scope. |

## 6. Backward Compatibility

- **Database**: migration `000123` is additive (`ADD COLUMN IF NOT EXISTS`) + a check constraint. **No backfill in the migration** — backfills are separate scripts run manually after the migration deploys. Existing rows stay NULL until the scripts run. Down migration drops the constraint and columns. No existing column is altered.
- **API**: the new `/cron/nie-expiration` endpoint is purely additive. No existing endpoint changes. No GraphQL schema change (`UpsertProductKFAInput` unchanged; seller NIE date arrives via custom form).
- **Existing clients/data**: products without `nie_expired_date` are untouched by the cron (filtered out by `IS NOT NULL`). Existing ALKES rows get a populated `nie_expired_date` after the ALKES backfill script runs; nothing about their status changes until the cron first runs. Existing Obat rows stay NULL until the stakeholder spreadsheet backfill is run (spreadsheet not yet received — see Active Open Item).
- **Deprecation path**: none. The custom-form "Masa Berlaku NIE" field for ALKES continues to be filled by `ConstructCustomFormKFAAlkes` (display copy); the new `product_kfa.nie_expired_date` is the cron's source of truth, the custom-form value is a display artifact.

## 7. Edge Cases & Risks

| Risk | Likelihood | Severity | Mitigation |
|---|---|---|---|
| Reminder re-fires every day if filter were a window (not exact) | Avoided by design | High (seller spam) | Exact-day equality filter (R4–R5); deterministic `TransactionID` for same-day double-fire (R16). |
| Take-down fires for non-ACTIVE product → no notification | By design (Tech Lead `<> FREEZE`) | Medium (seller not informed for non-Tayang freeze) | Accepted; flip filter to `status = ACTIVE` if PM objects (one-line change). |
| `time.Now().UTC().Date()` gives wrong WIB day | High if naive | High (reminder off-by-one) | Compute `today` via `now.In(jakartaLocation).Date()` (precedent `service_report.go:1158`). |
| `upsertProductKFA` OnConflict misses new columns → stale values | High if missed | High (silent data drop) | Add both columns to the OnConflict record in the same change. |
| `getProductKFAByProductIDs` SELECT misses new columns → Go zero-values | High if missed | Medium (cron reads NULL) | Add both columns to the SELECT list. |
| Obat partial update wipes `nie_expired_date` (seller leaves field empty) | Avoided by design (R10 preserve) | Medium (seller loses NIE date) | R10 — pre-fetch existing `product_kfa` row before OnConflict; if no new date supplied, inherit existing `NieExpiredDate`/`NieExpiredDateSource`. Obat-only. |
| Backfill scripts run outside the codebase — window between `000123` deploy and backfill execution | Low | Low (cron sees all NULLs in that window; no take-down/reminder fires; non-blocking) | Run the ALKES backfill script immediately after deploying `000123`, before enabling the cron schedule (infra side). |
| First-run after backfill arms thousands of rows for freeze/reminder at once | Medium | High (mass freeze/notify spike) | Accepted — the cron is silent (no pre-flight log per Tech Lead). Operator monitors via Cloud Logging error logs if the cron fails. |
| No index on `product_kfa.nie_expired_date` → cron does seq scan | High (new column, no index shipped) | Medium (slow cron) | Ship `000123` without an index; measure `EXPLAIN ANALYZE` on prod data after first run; add follow-up migration if needed. |
| Novu workflow name typo fails at runtime, not compile time | Low (reusing `GENERAL_IN_APP_NOTIFICATION` constant, already in prod) | Medium (silent notification failure) | Constant in code; `pnd-general-inapp` already verified in prod via GMRT-52308. |
| Scheduler misfires/misses H-45 → reminder lost (no retry) | Low | Medium (missed milestone) | Accepted per Tech Lead "stateless + exact" (R17). |
| Seller with no verified admin-company persona | Low | Low (one product skipped) | Log + continue (mirror `service_report.go:317`). |
| `NieExpiredDate *time.Time` nil deref in reminder formatting | Low (filter excludes NULL) | Medium (panic) | Defensive nil-check in `sendNIEReminderNotification` before `.In(jakartaLocation).Format`. |
| `TransactionID` for renewal: same product, new expiry | Low | Low (would dedup wrongly if ID didn't include expiry) | ID format includes `expirationDate` so renewal fires a new reminder. |

---

## 8. Interface Contract

Per `product/AGENTS.md`: validation in service layer via `go-playground/validator`; `context.Context` as first param; error messages as `ErrMsg`-prefixed constants (no inline literals in `apierror.WithDesc`); migration version globally unique per service (use `create-migration` skill; next is `000123`).

**DB Schema changes** (migration `000123_add_nie_expired_date_to_product_kfa`):
```sql
BEGIN;
ALTER TABLE product_kfa
    ADD COLUMN IF NOT EXISTS nie_expired_date DATE,
    ADD COLUMN IF NOT EXISTS nie_expired_date_source TEXT;
ALTER TABLE product_kfa
    ADD CONSTRAINT nie_expired_date_source_valid
    CHECK (nie_expired_date_source IS NULL OR nie_expired_date_source IN ('MEDICAL_DEVICES', 'FARMASI'));
COMMIT;
```
**No backfill in the migration.** The ALKES backfill is a separate batched local script, run manually after `000123` deploys (see §9 step 1b and §10). Down: drop constraint `nie_expired_date_source_valid`, drop columns `nie_expired_date`, `nie_expired_date_source`.

**API changes:**
```
POST /cron/nie-expiration/alkes     (new, externally triggered at 00:01 WIB, MEDICAL_DEVICES rows)
POST /cron/nie-expiration/farmasi   (new, externally triggered at 00:01 WIB, FARMASI rows)
  -> 200 {"status": true} on success
  -> error on failure (mirrors /cron/product-report/expired-by-system)
Both routes call the same handler, which passes the source to the service. No GraphQL schema change.
```

**Business logic flow (concise):**
```
NIEExpirationCheck(ctx, source):
  today = now.In(jakartaLocation).Date() at midnight WIB

  nieExpirationTakeDown(ctx, today, source):
    loop batchSize=500, Page=1:
      ListProductsForNIEWithFilter(goqu.And(
        nie_expired_date <= today, status <> FREEZE,
        nie_expired_date IS NOT NULL, nie_expired_date_source = source))
      if empty: break
      FreezeUnfreezeProducts(ProductStatus: FREEZE, UserID: SYSTEM, PersonaID: SYSTEM, Items)
      (notification fires automatically for ACTIVE_TO_FREEZE via Pub/Sub subscriber)

  nieExpirationReminder(ctx, today, source):
    for days in [45, 30, 14]:
      target = today.AddDate(0,0,days)
      ListProductsForNIEWithFilter(goqu.And(
        nie_expired_date == target, status <> FREEZE,
        nie_expired_date IS NOT NULL, nie_expired_date_source = source), PerPage: 1000)
      getPersona(RoleNames: [PERSONA_ADMIN_COMPANY_ROLE], InstitusiIDs: unique sellerIDs, Statuses: [PERSONA_VERIFIED])
      for each product: sendNIEReminderNotification(TransactionID: "nie-reminder-<id>-<days>-<expiry>",
        NotificationName: GENERAL_IN_APP_NOTIFICATION, Payload: {generalInAppContent, targetUrl}, To: [{UserID: persona.UserID}])

  aman: no-op
```

## 9. Architecture / Plan

1. Migration `000123` (use `create-migration` skill): add columns + check constraint **only**. **No backfill in the migration.**
1b. Backfill script — ALKES (separate, outside the codebase, run manually after `000123` deploys, before enabling the cron schedule): batched SQL `UPDATE` with `jsonb_array_elements` extraction. Idempotent (`WHERE nie_expired_date IS NULL`), non-blocking on invalid dates (regex `^\d{4}-\d{2}-\d{2}$` guard), restricted to ALKES rows (`kfa_source = 'KFA_ALKES'`). Batched by keyset pagination on `product_id`, commit each batch.
1c. Backfill script — FARMASI (separate Go script, outside the codebase, run manually when the stakeholder spreadsheet is received): reads the spreadsheet, updates `product_kfa.nie_expired_date` with `source = FARMASI`. Skip rows that already have a `nie_expired_date`. **Spreadsheet not yet received** — see Active Open Item.
2. Constants (`constant.go`): `NIE_EXPIRED` enum + `PRODUCT_ACTION_REASON_MAP` + `PRODUCT_ACTION_REASON_TO_LABEL` entries; `NIE_EXPIRED_DATE_SOURCE_MEDICAL_DEVICES`/`_FARMASI`; `NIE_EXPIRED_REASON_TEXT`; `NIE_EXPIRY_REMINDER_NOTIFICATION` (semantic alias to `GENERAL_IN_APP_NOTIFICATION`); `NIE_EXPIRY_REMINDER_NOTIFICATION_CONTENT_FMT` (Go-side `fmt.Sprintf` template for `generalInAppContent`).
3. Model (`model.go`): `KFA.NieExpiredDate *time.Time`, `KFA.NieExpiredDateSource string`, new `ProductForNIE` read model.
4. Repository (`repository.go`): extend `upsertProductKFA` OnConflict + `getProductKFAByProductIDs` SELECT; add `ListProductsForNIEWithFilter` shared method following `ListProductReportWithFilter` convention.
5. Service — upsert wiring (`service.go`): after `ConstructCustomFormKFAPharmacy` call `extractObatNIEExpiryToKFA`; after `ConstructCustomFormKFAAlkes` call `extractAlkesNIEExpiryToKFA`. Handle R10 (preserve existing on empty Obat input).
6. Service — cron (`service_nie.go`): `NIEExpirationCheck`, `nieExpirationTakeDown`, `nieExpirationReminder`, `processNIETakeDownBatch`, `sendNIEReminderNotification`. Uses `GENERAL_IN_APP_NOTIFICATION` (`"pnd-general-inapp"`); payload is `{generalInAppContent, targetUrl}` only.
7. Handler (`handler.go`): `NIEExpirationCheckAlkes` and `NIEExpirationCheckFarmasi` thin wrappers.
8. Routes (`routes.go`): `POST /cron/nie-expiration/alkes` and `POST /cron/nie-expiration/farmasi`.
9. Index: **ship `000123` without an index**, measure `EXPLAIN ANALYZE` on production data after first run, add follow-up migration only if needed.

## 10. Implementation Details

Reference file:function + signature. Full snippet only for the genuinely novel extraction helpers.

**File**: `product/migrations/000123_add_nie_expired_date_to_product_kfa.up.sql`
- Change: new migration (see §8). Use `create-migration` skill. Column-add + check constraint only — no backfill.

**File**: `product/domains/product/constant.go`
- Change: add `NIE_EXPIRED PRODUCT_ACTION_REASON = "NIE_EXPIRED"` to the const block (`:458-482`); add `PRODUCT_ACTION_REASON_MAP` entry; add `PRODUCT_ACTION_REASON_TO_LABEL[NIE_EXPIRED]`; add source constants `NIE_EXPIRED_DATE_SOURCE_MEDICAL_DEVICES` / `NIE_EXPIRED_DATE_SOURCE_FARMASI`; add `NIE_EXPIRED_REASON_TEXT`; add `NIE_EXPIRY_REMINDER_NOTIFICATION = GENERAL_IN_APP_NOTIFICATION` (semantic alias); add `NIE_EXPIRY_REMINDER_NOTIFICATION_CONTENT_FMT`.

**File**: `product/domains/product/model.go` (`:1802-1861`)
- Change: add `NieExpiredDate *time.Time` and `NieExpiredDateSource string` to `KFA` struct. Add new `ProductForNIE` read model (ID, Name, SellerID, SellerName, NieExpiredDate).

**File**: `product/domains/product/repository.go`
- `upsertProductKFA` (`:5807-5856`): add both new columns to OnConflict record.
- `getProductKFAByProductIDs` (`:5867+`): add both new columns to SELECT.
- New: `ListProductsForNIEWithFilter(ctx, expression, order, pagination) ([]ProductForNIE, error)` — follows `ListProductReportWithFilter` convention (`:7058-7107`). `product` INNER JOIN `product_kfa`, 5-column SELECT, soft-delete filters, `Where(expression)`, pagination via `page.GetOffset`. Add to `Repository` interface near `:123`.

**File**: `product/domains/product/service.go` (`:5035-5051`)
- Change: after `ConstructCustomFormKFAPharmacy` add `extractObatNIEExpiryToKFA` + R10 preserve block; after `ConstructCustomFormKFAAlkes` add `extractAlkesNIEExpiryToKFA`.
- New helpers (novel):
```go
func extractObatNIEExpiryToKFA(customFormValues []ProductCustomFormValueDB, kfaDB *KFA) {
    for _, cfv := range customFormValues {
        if cfv.Name != string(PRODUCT_HEALTH_MAPPING_MASA_BERLAKU) { continue }
        if cfv.Value == "" { continue }
        parsed, err := time.Parse(time.DateOnly, cfv.Value)
        if err != nil {
            logger.Error(ctx, "invalid Masa Berlaku NIE date %q for product %s: %v", cfv.Value, kfaDB.ProductID, err)
            continue
        }
        kfaDB.NieExpiredDate = &parsed
        kfaDB.NieExpiredDateSource = NIE_EXPIRED_DATE_SOURCE_FARMASI
        return
    }
}

func extractAlkesNIEExpiryToKFA(kfaDB *KFA) {
    if kfaDB.NIE == nil { return }
    var latest *time.Time
    for _, id := range kfaDB.IdentifierIDs.Data {
        if id.Code == nil || *id.Code != *kfaDB.NIE { continue }
        if id.EndDate == nil { continue }
        end := (*time.Time)(id.EndDate)
        if latest == nil || end.After(*latest) { latest = end }
    }
    if latest != nil {
        kfaDB.NieExpiredDate = latest
        kfaDB.NieExpiredDateSource = NIE_EXPIRED_DATE_SOURCE_MEDICAL_DEVICES
    }
}
```

- R10 preserve wiring (Obat update path only, before `upsertProductKFA`):
```go
if kfaDB.NieExpiredDate == nil {
    existingKFA, err := ths.repo.GetProductKFAByProductIDs(ctx, []string{productID})
    if err != nil { /* log, continue with nil */ }
    if len(existingKFA) > 0 && existingKFA[0].NieExpiredDate != nil {
        kfaDB.NieExpiredDate = existingKFA[0].NieExpiredDate
        kfaDB.NieExpiredDateSource = existingKFA[0].NieExpiredDateSource
        logger.Warn(ctx, "preserving existing nie_expired_date for product %s — no new date supplied", productID)
    }
}
```
On insert path (new product), no pre-fetch — NULL until first fill. ALKES path skips this block entirely.

**File**: `product/domains/product/service_nie.go` (new) or `service_report.go`
- `NIEExpirationCheck(ctx context.Context, source string) error` — entry point. Silent cron — error logs only.
- `nieExpirationTakeDown(ctx, today, source)` — `batchSize=500`, `Page=1` loop; calls `FreezeUnfreezeProducts` with `SYSTEM` actor.
- `nieExpirationReminder(ctx, today, source)` — three single-pass queries (no loop); per-product `sendNIEReminderNotification` with `logger.Error` + continue on failure.
- `processNIETakeDownBatch(ctx, products)` — builds `FreezeUnfreezeProductItem` slice, calls `FreezeUnfreezeProducts`.
- `sendNIEReminderNotification(ctx, product, daysRemaining, recipientUserID)` — direct `TriggerNotification` using `GENERAL_IN_APP_NOTIFICATION`; payload: `{generalInAppContent, targetUrl}` only. `TransactionID = "nie-reminder-<id>-<days>-<expiry>"`. Defensive nil-check on `NieExpiredDate`.

**Logging**: use `product/shared-libs/logger`. Silent cron — error logs only (`logger.Error`). No pre-flight/post-run Info logs.

**File**: `product/domains/product/handler.go`
- `NIEExpirationCheckAlkes(w, req)` — calls `svc.NIEExpirationCheck(ctx, string(NIE_EXPIRED_DATE_SOURCE_MEDICAL_DEVICES))`.
- `NIEExpirationCheckFarmasi(w, req)` — calls `svc.NIEExpirationCheck(ctx, string(NIE_EXPIRED_DATE_SOURCE_FARMASI))`.
- Both mirror `ProductReportExpiredBySystem` (`:1344`).

**File**: `product/server/routes.go`
- Add `POST /cron/nie-expiration/alkes` and `POST /cron/nie-expiration/farmasi` routes alongside existing cron routes (`:139`, `:141`).

## 11. Files Changed / Files NOT Changed

| File | Change Type | Description |
|---|---|---|
| `migrations/000123_add_nie_expired_date_to_product_kfa.{up,down}.sql` | New | Columns + constraint only (no backfill). |
| `domains/product/constant.go` | Edit | New reason enum, map entries, source constants, reminder notification name (alias to `GENERAL_IN_APP_NOTIFICATION`), reminder content format string, reason text. |
| `domains/product/model.go` | Edit | Two new `KFA` fields; new `ProductForNIE` read model (5 fields). |
| `domains/product/repository.go` | Edit | OnConflict + SELECT extensions; new `ListProductsForNIEWithFilter` method + interface entry. |
| `domains/product/service.go` | Edit | Wire two extract helpers at `:5035-5051`; R10 preserve block. |
| `domains/product/service_nie.go` | New (or `service_report.go`) | Cron service methods + reminder helper. |
| `domains/product/handler.go` | Edit | `NIEExpirationCheckAlkes` + `NIEExpirationCheckFarmasi` handlers. |
| `server/routes.go` | Edit | New `/cron/nie-expiration/alkes` + `/cron/nie-expiration/farmasi` routes. |

| File | Reason untouched |
|---|---|
| `graph/product.graphqls`, `graph/model/models_gen.go` | No GraphQL schema change. |
| `graph/mapper.go` | `UpsertProductKFAInputToSpec` unchanged. |
| `client/kfa/` | `kfa.IdentifierID.EndDate` already exists; no client change. |
| `events/subscription/service.go` | Take-down notification already wired by `FreezeUnfreezeProducts` core. |
| `shared-libs/notification/` | `TriggerNotificationRequest` shape unchanged. |

## 12. Testing Checklist

Derived 1:1 from §4.

- [ ] R1: take-down freezes an eligible product with `NIE_EXPIRED` reason.
- [ ] R2 (ACTIVE): take-down notification fires for `ACTIVE_TO_FREEZE`.
- [ ] R2 (non-ACTIVE): take-down freezes but no notification for `BLOCKED_TO_FREEZE` etc. ⚠️ Filtering take-down by `status = ACTIVE` only is wrong — Tech Lead's rule is `status <> FREEZE`.
- [ ] R3: re-running take-down on already-FREEZE product is a no-op.
- [ ] R4: H-45 reminder fires with `daysRemaining=45` and correct `TransactionID`; status unchanged.
- [ ] R5: H-30 and H-14 reminders fire independently with their own `TransactionID`. ⚠️ The reminder query must stay single-pass per milestone — looping it like the take-down query causes an infinite loop, since reminders don't mutate state.
- [ ] R6: products outside the three reminder days and not past expiry → no action.
- [ ] R7: NULL `nie_expired_date` excluded from both branches.
- [ ] R8: Obat upsert with `YYYY-MM-DD` sets `nie_expired_date` + `source=FARMASI`. ⚠️ Adding both new columns to the table but forgetting `upsertProductKFA`'s OnConflict clause silently retains the stale value; forgetting them in `getProductKFAByProductIDs`'s SELECT makes the cron read a Go zero-value instead of NULL. Both places need both columns.
- [ ] R9: Obat upsert with invalid date logs and leaves `nie_expired_date` untouched. ⚠️ Putting the Obat extraction inside `ConstructCustomFormKFAPharmacy`'s `checkerMap` overwrites the seller's value with KFA's (wrong source) — use the separate `extractObatNIEExpiryToKFA` step instead.
- [ ] R10: Obat update with empty date preserves existing `nie_expired_date`.
- [ ] R11: ALKES upsert sets `nie_expired_date` from latest matching `identifier_ids[].end_date`, `source=MEDICAL_DEVICES`. ⚠️ Reusing `kfa_source` as the discriminator conflates endpoint source with value source — use the dedicated `nie_expired_date_source` column.
- [ ] R12: backfill script populates eligible ALKES rows with `source=MEDICAL_DEVICES`.
- [ ] R13: backfill script skips rows with non-`YYYY-MM-DD` `end_date`.
- [ ] R14: backfill script does not touch `kfa_source = 'KFA_FARMASI'` rows.
- [ ] R15: backfill script re-run does not overwrite rows where `nie_expired_date IS NOT NULL`.
- [ ] R16: same-day cron double-fire produces one reminder per (product, milestone) via Novu `TransactionID` dedup. ⚠️ `TransactionID = uuid.New()` defeats this — it must be deterministic (`nie-reminder-<id>-<days>-<expiry>`), or a same-day double-fire sends two reminders.
- [ ] R17: scheduler missing H-45 → no reminder on H-44.
- [ ] WIB date: `today` computed in WIB, not UTC (mock clock test). ⚠️ `time.Now().UTC().Date()` shifts the reminder a calendar day early/late around 00:01 WIB — use `now.In(jakartaLocation).Date()`.
- [ ] Cron is silent — no pre-flight or post-run Info logs on success.
- [ ] Error logs emitted on batch failure, per-product reminder failure, or Novu dispatch failure.
- [ ] Reminder `NotificationName` equals `GENERAL_IN_APP_NOTIFICATION` (`"pnd-general-inapp"`). ⚠️ Using `pnd-seller-product-nie-expiry-reminder` (the originally-proposed dedicated workflow) fails at runtime, not compile time — it was never registered.
- [ ] Reminder `Payload` has exactly two keys: `generalInAppContent` + `targetUrl`. ⚠️ `pnd-general-inapp` ignores extra keys (`subject`, `productName`, `daysRemaining`, etc.) — sending them just clutters the payload with no effect.

### Test Focus Pointer (carry-over from exploration Risk lens)

Areas flagged as concurrency/perf/security-sensitive during exploration Stage 2, still relevant after synthesis:

| Area | Why sensitive | Still relevant post-synthesis? |
|---|---|---|
| Same-day cron double-fire → reminder dedup (R16) | Concurrency — Novu `TransactionID` dedup is the only safety net if the exact-day filter and a re-run overlap in the same window | Yes — needs a concurrent/double-run test, not just a single-call unit test |
| Backfill script batch commits on `product_kfa` at scale | Performance — keyset-paginated `UPDATE` against a large table; no index ships with `000123` (§7) | Yes — measure `EXPLAIN ANALYZE` after first prod run per §9 step 9; flag if the follow-up index migration becomes urgent |
| `today` boundary computed in WIB vs UTC | Correctness-critical time boundary — a naive UTC read shifts every milestone by a day (§7) | Yes — covered by the WIB mock-clock checklist line above, listed here since it was also flagged during exploration as a risk area, not just a rule |

## 13. Open Items

Lifecycle rules in `rules.md` § 8. An item lives in exactly one of the two lists below at any time — never both, never neither once raised.

### Active — need external input or verification

1. **FARMASI backfill spreadsheet — not yet received.** Script can't be finalized until it arrives. **Owner: Tech Lead / stakeholder.**

### Resolved (kept for reference)

1. ~~**Dedicated Novu workflow (`pnd-seller-product-nie-expiry-reminder`) needs to be registered before launch**~~ **RESOLVED — not needed.** PM confirmed the reminder reuses the existing, already-registered `pnd-general-inapp` workflow instead (see §5 Decision Log, §2 Scope). No new Novu workflow registration required.