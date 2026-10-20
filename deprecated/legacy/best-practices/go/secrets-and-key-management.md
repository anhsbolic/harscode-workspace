# secrets-and-key-management.md

**Location:** `go/secrets-and-key-management.md`

**Principle**
Every key serves one purpose — never reuse one key across multiple purposes (e.g. the same key used for encryption-at-rest and also for HMAC lookups, or for signing JWTs). Reusing a key across purposes means compromising one use case opens up an unrelated use case. Have a clear key-rotation strategy (documented as a plan even if not yet needed), and enforce strict discipline so development/sandbox keys never end up in a commit — use `.env`/a secret manager, and exclude them explicitly via `.gitignore`.

**Bad**
```go
// one env var used for multiple purposes
key := os.Getenv("APP_SECRET")
encryptedData := encrypt(data, key)
hmacLookup := hmac.New(sha256.New, []byte(key)) // same key!
jwtToken := signJWT(claims, key)                // same key again!
```

**Good**
```go
encryptionKey := os.Getenv("PII_ENCRYPTION_KEY")
hmacLookupKey := os.Getenv("PII_HMAC_LOOKUP_KEY")   // separate from the encryption key
jwtSigningKey := os.Getenv("JWT_SIGNING_KEY")        // separate again

encryptedData := encrypt(data, encryptionKey)
hmacLookup := hmac.New(sha256.New, []byte(hmacLookupKey))
jwtToken := signJWT(claims, jwtSigningKey)
```

**Checklist**
- [ ] No single key is used for more than one purpose (encryption, HMAC, signing each have separate keys)
- [ ] A key-rotation plan is documented, even if not yet implemented
- [ ] `.env`/secret files are in `.gitignore`, and no `.env.example` contains a default value resembling a real secret
- [ ] Production and development/sandbox secrets are never swapped or shared