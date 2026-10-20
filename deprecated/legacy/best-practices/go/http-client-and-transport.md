> **Location:** `best-practices/go/http-client-and-transport.md`

# HTTP Client & Transport Reuse

## 1. `http.DefaultClient` and freshly-constructed `&http.Client{}` have no timeout

**Principle:** `http.Client{}`'s zero value has no request timeout — a hung connection or a slow/unresponsive server can block a goroutine indefinitely. `http.DefaultClient` (used implicitly by `http.Get`, `http.Post`, etc.) has this same problem.

### Bad
```go
resp, err := http.Get(url) // uses http.DefaultClient, no timeout — can hang forever
```
```go
client := &http.Client{} // also no timeout
resp, err := client.Do(req)
```

### Good
```go
client := &http.Client{
    Timeout: 10 * time.Second, // covers the entire request lifecycle: connect, redirects, read body
}
```
For finer-grained control (connect timeout vs read timeout separately), configure the underlying `Transport` with `DialContext` timeouts, or prefer passing a `ctx` with a deadline into the request (`http.NewRequestWithContext`) alongside a client-level `Timeout` as a backstop.

**Checklist:**
- Never use `http.Get`/`http.Post`/`http.DefaultClient` directly in production code paths — always construct a client with an explicit `Timeout`.
- Prefer `http.NewRequestWithContext(ctx, ...)` so the request also respects the caller's context cancellation/deadline, not just a fixed client-level timeout.

---

## 2. Constructing a new `http.Client` (or `Transport`) per request exhausts connections instead of reusing them

**Principle:** `http.Client`'s underlying `Transport` maintains a connection pool (keep-alive connections) that's only effective if the same `Transport`/`Client` instance is reused across requests. Creating a new client per request means every request pays full TCP+TLS handshake cost, and under load can exhaust ephemeral ports.

### Bad
```go
func callDownstream(ctx context.Context, req Request) (*Response, error) {
    client := &http.Client{Timeout: 10 * time.Second} // new client, new connection pool, every call
    // ...
}
```

### Good
```go
type service struct {
    httpClient *http.Client // constructed once, reused across all calls
}

func NewService() *service {
    return &service{
        httpClient: &http.Client{
            Timeout: 10 * time.Second,
            Transport: &http.Transport{
                MaxIdleConnsPerHost: 20,
                IdleConnTimeout:     90 * time.Second,
            },
        },
    }
}
```

**Checklist:**
- Construct `http.Client` once (typically at service/dependency initialization) and reuse it across all outgoing requests to that dependency — never inside a per-request function body.
- Fully read and close the response body (`io.Copy(io.Discard, resp.Body)` if the body isn't needed, then `resp.Body.Close()`) on every code path, including error paths — an unclosed or partially-read body prevents the underlying connection from being returned to the pool for reuse.