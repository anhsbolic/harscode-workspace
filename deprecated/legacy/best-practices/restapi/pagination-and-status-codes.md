> **Location:** `best-practices/restapi/pagination-and-status-codes.md`

# Pagination & Status Code Discipline

## 1. Offset pagination degrades and drifts under concurrent writes

**Principle:** `LIMIT/OFFSET` pagination re-scans and discards `OFFSET` rows on every page (expensive at high offsets), and its results shift if rows are inserted/deleted between page requests — a client paging through results can see duplicate or skipped items.

### Bad
```sql
SELECT * FROM orders ORDER BY created_at DESC LIMIT 20 OFFSET 10000;
```
At high offsets this scans and discards 10,000 rows before returning the next 20. If a new order is inserted while the client is paging, every subsequent offset shifts by one, causing a duplicate or skipped row.

### Good
```sql
-- cursor is the created_at (and id, for tiebreak) of the last row seen
SELECT * FROM orders
WHERE (created_at, id) < ($1, $2)
ORDER BY created_at DESC, id DESC
LIMIT 20;
```
Cursor (keyset) pagination doesn't rescan skipped rows and stays stable under concurrent inserts, because it filters relative to a known position rather than counting from the start.

**Checklist:**
- For any list endpoint expected to have deep pagination or high write concurrency, default to cursor-based pagination, not offset.
- If offset pagination is kept for simplicity on a low-traffic/low-write endpoint, document that "stable pagination under concurrent writes" is explicitly not guaranteed.

---

## 2. Status codes should reflect the actual failure category, not always 200 or always 500

**Principle:** HTTP status codes are how infra (retry logic, monitoring, caching layers) and clients distinguish "retry this" from "don't retry, fix the request" from "server's fault." Returning `200` with an error payload, or `500` for a client validation error, breaks that signal for every layer that relies on it.

### Bad
```go
func (h *Handler) GetOrder(w http.ResponseWriter, r *http.Request) {
    order, err := h.repo.FindByID(ctx, id)
    if err != nil {
        w.WriteHeader(http.StatusOK) // always 200, error is in the body
        json.NewEncoder(w).Encode(map[string]string{"error": "not found"})
        return
    }
}
```
A caching proxy or CDN in front of this endpoint may cache the "not found" response as if it were a valid 200. A client's automatic retry logic (which typically retries 5xx, not 4xx or 2xx) won't retry a real transient failure disguised as 200 either.

### Good
```go
if err != nil {
    if errors.Is(err, ErrNotFound) {
        w.WriteHeader(http.StatusNotFound) // 404 — client error, don't retry as-is
    } else {
        w.WriteHeader(http.StatusInternalServerError) // 500 — server fault, safe to retry
    }
    json.NewEncoder(w).Encode(errorBody(err))
    return
}
```

**Checklist:**
- `4xx` = the client sent something that will fail again on identical retry (bad input, not found, unauthorized) — don't return `5xx` or `200` for these.
- `5xx` = the server failed in a way that might succeed on retry (DB timeout, downstream unavailable) — reserve this for genuine server-side failure, not validation errors.
- Never encode a real failure as `200` with an error field in the body "to keep the client code simple" — it breaks every piece of infrastructure that inspects status codes instead of parsing bodies.