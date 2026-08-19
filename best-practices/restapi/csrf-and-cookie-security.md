# csrf-and-cookie-security.md

**Location:** `restapi/csrf-and-cookie-security.md`

**Principle**
If any authentication token (especially a refresh token) is stored in a cookie, every endpoint relying on that cookie — including the refresh endpoint itself — is potentially CSRF-vulnerable unless explicit mitigation is applied. Minimum mitigation: a `SameSite=Strict` or `Lax` cookie attribute, combined with a custom header check (browsers don't send custom headers cross-origin without a preflight that CORS can block) or a double-submit token pattern.

**Bad**
```go
http.SetCookie(w, &http.Cookie{
    Name:     "refresh_token",
    Value:    token,
    HttpOnly: true,
    // no SameSite, no other CSRF mitigation
})
```

**Good**
```go
http.SetCookie(w, &http.Cookie{
    Name:     "refresh_token",
    Value:    token,
    HttpOnly: true,
    Secure:   true,
    SameSite: http.SameSiteStrictMode, // first layer of CSRF mitigation
})
// the refresh endpoint also checks a custom header that can only be sent same-origin
if r.Header.Get("X-Requested-With") != "expected-client-marker" {
    http.Error(w, "forbidden", 403)
    return
}
```

**Checklist**
- [ ] Cookies storing authentication tokens have an explicit `SameSite` attribute (`Strict` or `Lax` as the flow requires)
- [ ] There is a second CSRF mitigation (custom header check or double-submit token) on top of `SameSite`, not relying on one layer alone
- [ ] The refresh endpoint is treated as CSRF-sensitive, not exempted
- [ ] Cookies have `Secure` (HTTPS only) and `HttpOnly` (not accessible to JS) attributes