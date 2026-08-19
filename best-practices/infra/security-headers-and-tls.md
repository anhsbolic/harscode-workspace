# security-headers-and-tls.md

**Location:** `infra/security-headers-and-tls.md`

**Principle**
Security headers at the reverse-proxy level (Caddy, Nginx, or equivalent) are an easy layer to skip because they aren't "application code" — yet the reverse proxy is the most natural place to enforce them consistently across every endpoint without repeating logic in each handler. Minimum set: a Content-Security-Policy (CSP) restricting script/style sources, `X-Content-Type-Options: nosniff` (prevent MIME-sniffing), a `Referrer-Policy` that doesn't leak sensitive URLs to third parties, and HSTS to force HTTPS on subsequent requests.

**Bad**
```
# Caddyfile with no security headers at all
app.example.com {
    reverse_proxy localhost:8080
}
```

**Good**
```
app.example.com {
    reverse_proxy localhost:8080
    header {
        Content-Security-Policy "default-src 'self'"
        X-Content-Type-Options "nosniff"
        Referrer-Policy "strict-origin-when-cross-origin"
        Strict-Transport-Security "max-age=31536000; includeSubDomains"
    }
}
```

**Checklist**
- [ ] CSP is in place and scoped to actual need (no `unsafe-inline`/`unsafe-eval` unless genuinely required and its risk is understood)
- [ ] `X-Content-Type-Options: nosniff` is in place
- [ ] `Referrer-Policy` doesn't leak full URLs (including sensitive query strings) to other origins
- [ ] HSTS is active with a reasonable `max-age`, and `includeSubDomains` if all subdomains are indeed HTTPS