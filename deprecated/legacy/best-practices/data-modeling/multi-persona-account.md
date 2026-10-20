# multi-persona-account.md

**Location:** `data-modeling/multi-persona-account.md`

**Principle**
When one account can hold multiple roles at once (not a strict hierarchy — e.g. an account can be both a "seller" and a "buyer" simultaneously), the tempting shortcut is one wide `accounts` table with a nullable column set per role. It degrades fast: every new role adds more nullable columns to every row regardless of relevance, "which columns are valid together" becomes tribal knowledge instead of a constraint the schema enforces, and a query has no clean way to express "accounts that are sellers" without a pile of `IS NOT NULL` checks standing in for a real relationship. Splitting into a credentials/identity table (what makes the account unique — login, auth status), a generic profile table (one-to-one, personal data shared across all roles), and one attribute table per role (one-to-one or one-to-many, only rows that hold that role have one) makes "does this account currently hold role X" a join's existence, not a column's nullness, and lets an account hold several role-attribute rows simultaneously without schema changes.

**Bad**
```sql
-- One fat table, nullable columns per role, growing without bound
CREATE TABLE accounts (
    id UUID PRIMARY KEY,
    email TEXT NOT NULL,
    password_hash TEXT NOT NULL,
    full_name TEXT,
    -- seller-only columns, NULL for every non-seller account
    seller_store_name TEXT,
    seller_payout_method TEXT,
    seller_verified_at TIMESTAMPTZ,
    -- buyer-only columns, NULL for every non-buyer account
    buyer_shipping_address TEXT,
    buyer_loyalty_tier TEXT,
    -- "is this a seller?" is now an implicit convention, not a real check
    -- e.g. WHERE seller_store_name IS NOT NULL
    created_at TIMESTAMPTZ NOT NULL
);
```

**Good**
```sql
-- Identity/credentials: what makes the account unique
CREATE TABLE accounts (
    id UUID PRIMARY KEY,
    email TEXT NOT NULL UNIQUE,
    password_hash TEXT NOT NULL,
    created_at TIMESTAMPTZ NOT NULL
);

-- Generic profile: one-to-one, shared across every role
CREATE TABLE account_profiles (
    account_id UUID PRIMARY KEY REFERENCES accounts(id),
    full_name TEXT NOT NULL,
    phone_number TEXT
);

-- Per-role attribute tables: only accounts holding that role have a row
CREATE TABLE seller_attributes (
    account_id UUID PRIMARY KEY REFERENCES accounts(id),
    store_name TEXT NOT NULL,
    payout_method TEXT NOT NULL,
    verified_at TIMESTAMPTZ
);

CREATE TABLE buyer_attributes (
    account_id UUID PRIMARY KEY REFERENCES accounts(id),
    shipping_address TEXT,
    loyalty_tier TEXT NOT NULL DEFAULT 'standard'
);

-- "Is this account a seller?" is now a real, indexable relationship
SELECT a.* FROM accounts a
JOIN seller_attributes s ON s.account_id = a.id
WHERE a.id = :account_id;

-- An account can hold both roles at once with no schema change:
-- just insert into both seller_attributes and buyer_attributes for the same account_id.
```

**Checklist**
- [ ] Credentials/identity, generic profile, and per-role attributes live in separate tables — not one table with nullable columns per role
- [ ] "Does this account hold role X" is expressed as a join/existence check against a role attribute table, not a nullness check on a shared column
- [ ] An account holding two roles simultaneously requires no schema change — just a row in each relevant attribute table
- [ ] Adding a new role means adding a new attribute table, not adding more nullable columns to an existing shared table
- [ ] A wide table with per-role nullable columns is treated as a design smell to flag in review, not accepted as "how it's always been done here"
