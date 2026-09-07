# New category: data-modeling/

**Status:** Proposed
**Date:** 2026-09-07
**Protection Tier:** general
**Triggered by:** locking the ERD/schema-design approach for a new project, surfacing three cross-database schema patterns with concrete rationale that don't fit any existing category
**Target area:** best-practices
**Target file(s):**
- `best-practices/data-modeling/multi-persona-account.md` — new file
- `best-practices/data-modeling/historical-snapshot-fk.md` — new file
- `best-practices/data-modeling/deletion-vs-anonymization.md` — new file
- `best-practices/index.md` — new `data-modeling` category rows + Security Concern Map entries

## Gap found

`postgresql/` exists but is scoped to Postgres-specific mechanics (indexing, locking, encryption-at-rest, migrations) — it isn't the place for cross-database *schema design* decisions that apply just as well on MySQL or any other RDBMS. Three such decisions came up while designing a schema with multiple account personas, transaction history, and PII deletion requirements:

1. Multi-role accounts (one login, several "hats") are commonly modeled as one fat table with nullable per-role columns — this degrades badly as roles grow and makes it unclear which columns are even valid together.
2. Transaction/history records that reference a mutable entity (e.g. an assignment, a price, a status) need the value *at the time*, not the current value — a plain foreign key silently rewrites history when the referenced row changes.
3. Soft delete and "right to erasure" pull in opposite directions (keep the row for referential/audit integrity vs actually remove personal data) — teams default to whichever one they know without weighing the trade-off against the other.

None of these are Postgres-specific or tied to one project's domain — they're schema-design decisions that recur across any relational schema with role complexity, historical records, or PII.

## Proposed change

Add a new `best-practices/data-modeling/` folder with three files (full content below), plus new rows in `best-practices/index.md`.

### `index.md` additions

New rows in the main trigger-keyword table:

| Category | File | Trigger keywords | Security-critical | Summary |
|---|---|---|---|---|
| data-modeling | [data-modeling/multi-persona-account.md](data-modeling/multi-persona-account.md) | multi-role account, persona, nullable columns, credential table, profile table | no | Split credential / generic-profile / per-role-attribute into separate tables instead of one table with nullable per-role columns; supports an account holding multiple roles at once |
| data-modeling | [data-modeling/historical-snapshot-fk.md](data-modeling/historical-snapshot-fk.md) | snapshot column, historical foreign key, mutable reference, point-in-time | no | Snapshot a referenced value at transaction time alongside the live foreign key when the referenced entity can change after the fact, so history doesn't silently rewrite itself |
| data-modeling | [data-modeling/deletion-vs-anonymization.md](data-modeling/deletion-vs-anonymization.md) | soft delete, hard delete, anonymization, right to erasure, deletion request | yes | Soft delete preserves referential/audit integrity but can conflict with privacy-erasure requirements; anonymization (null/hash PII, keep the row) is often the actual middle ground needed |

Security Concern Map additions:

| Concern | Files (add to) |
|---|---|
| pii-and-encryption | + `data-modeling/deletion-vs-anonymization.md` |

### New files

See attached file contents (`multi-persona-account.md`, `historical-snapshot-fk.md`, `deletion-vs-anonymization.md`) — full text ready to paste into `best-practices/data-modeling/`.

## Rationale

All three principles are database-engine-agnostic schema design decisions, not Postgres-specific mechanics (which is what `postgresql/` is scoped to) and not tied to any one project's table/domain names — the examples below use generic entity names (`accounts`, `assignments`, `orders`), not any specific project's vocabulary.
- `multi-persona-account.md` is the schema-design counterpart to `go/interface-and-slice-semantics.md`'s general concern about over-generalized shared structures hiding which fields are actually valid together — applied to table design instead of Go types.
- `historical-snapshot-fk.md` complements `postgresql/audit-log-design.md` (which covers audit-log immutability) with a distinct, more common failure mode: a *live* foreign key on an ordinary transactional table quietly changing the meaning of old records, not just audit-log tampering.
- `deletion-vs-anonymization.md` complements `postgresql/encryption-at-rest.md` (protecting PII at rest) by addressing what happens when PII needs to stop existing at all — a decision every schema with personal data eventually has to make, regardless of database engine.

This belongs in shared guidance rather than a project's own `AGENTS.md` because none of the three principles depend on any specific project's regulatory scope, domain vocabulary, or database engine — they're the kind of decision that recurs on essentially any schema with role complexity, history, or personal data.

---

*After human review: update the Status above. If Accepted, merge into
the target document and leave this proposal in place (don't delete
it) — it serves as this folder's changelog. See `proposals/README.md`
for the Protection Tier distinction and numbering convention.*
