# encryption-at-rest.md

**Location:** `postgresql/encryption-at-rest.md`

**Principle**
A column holding sensitive (PII) data encrypted with nondeterministic encryption cannot be queried directly with `WHERE column = $1` against the ciphertext, because ciphertext from the same plaintext will differ on every encryption. For lookup needs (e.g. finding a user by encrypted email), store a separate HMAC column apart from the ciphertext column — HMAC is deterministic for lookups, ciphertext is for secure storage. The HMAC key MUST differ from the encryption key (see `go/secrets-and-key-management.md`) — if they're the same, knowing one exposes the other.

**Bad**
```sql
-- attempting to query nondeterministic ciphertext directly
SELECT * FROM users WHERE email_encrypted = $1; -- will never match
```

**Good**
```sql
CREATE TABLE users (
    id UUID PRIMARY KEY,
    email_ciphertext BYTEA NOT NULL,   -- nondeterministic encryption, for storage
    email_hmac TEXT NOT NULL UNIQUE    -- deterministic HMAC, for lookup only
);
```
```go
lookupHMAC := computeHMAC(email, hmacLookupKey) // DIFFERENT key from the encryption key
row := db.QueryRow("SELECT * FROM users WHERE email_hmac = $1", lookupHMAC)
```

**Checklist**
- [ ] Nondeterministic ciphertext columns are never used directly in a `WHERE` condition
- [ ] A separate HMAC column exists for any lookup/uniqueness need on encrypted data
- [ ] The HMAC key and encryption key are different keys
- [ ] Which columns need HMAC lookup (searched/unique) vs. ciphertext only (write-only/read-by-ID) has been deliberately decided