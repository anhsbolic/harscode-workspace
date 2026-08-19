# migrations-safety.md

**Location:** `postgresql/migrations-safety.md`

**Principle**
For migrations run manually (not automated via CI/CD), additive-first discipline matters: new columns are added nullable first, backfilled, then changed to `NOT NULL` in a separate migration — not made `NOT NULL` directly in one migration that can fail midway if existing data doesn't yet satisfy the constraint. Avoid migrations that lock large tables for extended periods (e.g. `ALTER TABLE ... ADD COLUMN ... DEFAULT` on a large table without considering the lock behavior of the Postgres version in use). Ensure `up`/`down` are genuinely reversible and tested in both directions, not just written symmetrically on paper.

**Bad**
```sql
-- one migration, straight to NOT NULL — fails if any existing row has NULL
ALTER TABLE users ADD COLUMN phone_verified BOOLEAN NOT NULL DEFAULT false;
```

**Good**
```sql
-- migration 1: add nullable column
ALTER TABLE users ADD COLUMN phone_verified BOOLEAN;

-- (backfill run separately, outside the migration or in the next one)
UPDATE users SET phone_verified = false WHERE phone_verified IS NULL;

-- migration 2: only made NOT NULL after backfill is complete
ALTER TABLE users ALTER COLUMN phone_verified SET NOT NULL;
ALTER TABLE users ALTER COLUMN phone_verified SET DEFAULT false;
```

**Checklist**
- [ ] New columns are added nullable first, with `NOT NULL` in a separate migration after backfill
- [ ] Migrations on large tables have their locking impact checked before running in production
- [ ] The `down` migration is genuinely reversible and has been tested, not just written symmetrically
- [ ] Migrations already applied in any environment are never edited afterward — corrections go into a new migration