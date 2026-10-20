# cors-configuration.md

**Location:** `restapi/cors-configuration.md`

**Principle**
Combining `Access-Control-Allow-Credentials: true` with `Access-Control-Allow-Origin: *` (wildcard) is a classic and dangerous misconfiguration — modern browsers actually reject this literal combination, but implementations that try to "work around" it by reflecting whatever origin sent the request as the allowed origin (not a literal wildcard, but effectively the same) still open the same hole. The allowed-origin list must be explicit and specific, especially when the API and frontend sit on separate origins (e.g. behind a reverse proxy).

**Bad**
```go
w.Header().Set("Access-Control-Allow-Origin", r.Header.Get("Origin")) // reflects any origin
w.Header().Set("Access-Control-Allow-Credentials", "true") // + credentials = a hole
```

**Good**
```go
var allowedOrigins = map[string]bool{
    "https://app.example.com": true,
    "https://staging.example.com": true,
}

origin := r.Header.Get("Origin")
if allowedOrigins[origin] {
    w.Header().Set("Access-Control-Allow-Origin", origin) // only an explicitly whitelisted origin
    w.Header().Set("Access-Control-Allow-Credentials", "true")
}
```

**Checklist**
- [ ] There is no combination of a wildcard origin with `Allow-Credentials: true`
- [ ] Allowed origins are an explicit whitelist, not a reflection of whatever origin the request carries
- [ ] The origin whitelist is configured per environment (dev/staging/prod differ), not one hardcoded list for all
- [ ] Preflight (`OPTIONS`) requests are handled consistently with the same origin policy