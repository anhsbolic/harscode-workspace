# deletion-vs-anonymization.md

**Location:** `data-modeling/deletion-vs-anonymization.md`

**Principle**
Soft delete (a `deleted_at` timestamp, row stays) and hard delete (row actually removed) get chosen by habit more often than by weighing what they're each for. Soft delete protects referential integrity — other rows that reference this one don't break, and audit/report history stays intact — but it's a poor fit for personal data that a privacy regulation or a user's own erasure request says must actually stop existing. Hard delete satisfies erasure but breaks referential integrity and audit history the moment anything else points at that row. Anonymization is the actual middle ground for most "user asked to be forgotten" cases: null or hash the personal fields, keep the row (and its relationships, its place in aggregate reports) intact. A separate, append-only deletion-request table (who asked, when, what was anonymized) gives the erasure action itself an audit trail, which a raw hard delete or an in-place soft-delete flag can't provide.

**Bad**
```sql
-- Treating "user requested deletion" as a single global switch, with no
-- distinction between "remove personal data" and "remove the row",
-- and no record that a deletion request ever happened.

-- Option A: hard delete — breaks every order that references this user,
-- and destroys the audit trail of what this user did.
DELETE FROM users WHERE id = :user_id;

-- Option B: soft delete only — row and every PII field are still sitting
-- there in full, unencrypted-at-rest reads, doing nothing to satisfy an
-- actual erasure request; deleted_at just hides it from default queries.
UPDATE users SET deleted_at = now() WHERE id = :user_id;
```

**Good**
```sql
-- Anonymize personal fields, keep the row for referential/audit integrity
UPDATE users
SET
    email = 'deleted-' || id || '@anonymized.invalid',
    full_name = NULL,
    phone_number = NULL,
    deleted_at = now()
WHERE id = :user_id;

-- Separate, append-only audit trail for the erasure action itself —
-- not deleted alongside the anonymization, this IS the compliance record
CREATE TABLE deletion_requests (
    id UUID PRIMARY KEY,
    subject_user_id UUID NOT NULL,
    requested_at TIMESTAMPTZ NOT NULL,
    requested_via TEXT NOT NULL,      -- 'self_service', 'support_ticket', etc.
    fields_anonymized TEXT[] NOT NULL,
    processed_at TIMESTAMPTZ
);

-- Orders/audit logs referencing this user still resolve correctly —
-- they just show anonymized identity data, not a broken foreign key
-- or a row that silently vanished.
```

**Checklist**
- [ ] "Soft delete" and "erasure/anonymization" are treated as two distinct mechanisms, not the same `deleted_at` flag doing both jobs
- [ ] Personal data fields are explicitly nulled or hashed on an erasure request — a `deleted_at` flag alone is not treated as satisfying erasure
- [ ] The row itself is kept (not hard-deleted) when other rows reference it, so referential integrity and historical reports survive an erasure request
- [ ] A separate, append-only table records that a deletion/erasure request happened (who, when, via what channel, which fields were affected) — this record is not itself subject to the same anonymization
- [ ] Hard delete is reserved for data with no referential integrity concerns and no regulatory/audit reason to retain a trace — not used as the default erasure mechanism
