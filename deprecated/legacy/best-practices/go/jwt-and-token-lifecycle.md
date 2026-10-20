# jwt-and-token-lifecycle.md

**Location:** `go/jwt-and-token-lifecycle.md`

**Principle**
Tokens with different purposes (access token vs. step-up/pending-verification token vs. refresh token) must use different algorithms and/or keys — never reuse one signing key across all token types. Reason: if one token type's issuance path is ever compromised (e.g. a "pending MFA" token gets generated too permissively), the same key must not be usable to forge a token with higher scope. Refresh tokens require rotation (each refresh invalidates the old token and issues a new one) plus reuse detection — if an already-rotated refresh token is presented again, that's a signal it was stolen, and the entire token family must be revoked.

**Bad**
```go
// all token types share the same secret
accessToken := jwt.NewWithClaims(jwt.SigningMethodHS256, claims)
mfaPendingToken := jwt.NewWithClaims(jwt.SigningMethodHS256, claims) // same key as access token
// refresh token reused repeatedly, no rotation
```

**Good**
```go
// access token: asymmetric algorithm, key separate from other token purposes
accessToken := jwt.NewWithClaims(jwt.SigningMethodES256, accessClaims)
// narrow-purpose token (e.g. pending step-up verification): different key & algorithm,
// explicit scope claim, short expiry
mfaPendingToken := jwt.NewWithClaims(jwt.SigningMethodHS256, mfaPendingClaims)

// refresh: rotate on use, detect reuse
newRefresh, err := refreshStore.RotateAndDetectReuse(ctx, oldRefreshTokenID)
if errors.Is(err, ErrReuseDetected) {
    refreshStore.RevokeFamily(ctx, tokenFamilyID) // reuse = stolen, revoke the whole family
}
```

**Checklist**
- [ ] Each token type (access, step-up/pending, refresh) uses a different key and/or algorithm
- [ ] Refresh tokens are rotated on every use, not reusable until expiry
- [ ] There is a reuse-detection mechanism that triggers revocation of the entire token family
- [ ] Token storage location (in-memory vs. cookie) reflects a deliberate XSS-vs-CSRF trade-off, not a framework default
- [ ] Each token type's expiry is proportional to its risk (narrower-scope tokens get shorter expiry)