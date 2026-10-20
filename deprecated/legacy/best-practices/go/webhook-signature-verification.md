# webhook-signature-verification.md

**Location:** `go/webhook-signature-verification.md`

**Principle**
Every endpoint that receives a callback/webhook from an external party must verify a signature (HMAC or equivalent) before processing the payload, and must apply replay protection (a timestamp/nonce window) so a valid payload can't be replayed repeatedly. Without this, the callback endpoint becomes a way to forge status/events from outside the system.

**Bad**
```go
func HandleWebhook(w http.ResponseWriter, r *http.Request) {
    var payload WebhookPayload
    json.NewDecoder(r.Body).Decode(&payload)
    processEvent(payload) // no signature verification at all
}
```

**Good**
```go
func HandleWebhook(w http.ResponseWriter, r *http.Request) {
    body, _ := io.ReadAll(r.Body)
    signature := r.Header.Get("X-Signature")
    if !verifyHMAC(body, signature, webhookSecret) {
        http.Error(w, "invalid signature", 401)
        return
    }
    timestamp := r.Header.Get("X-Timestamp")
    if isOutsideReplayWindow(timestamp, 5*time.Minute) {
        http.Error(w, "stale request", 401)
        return
    }
    if seenNonce(r.Header.Get("X-Nonce")) { // replay protection
        http.Error(w, "duplicate request", 401)
        return
    }
    var payload WebhookPayload
    json.Unmarshal(body, &payload)
    processEvent(payload)
}
```

**Checklist**
- [ ] Signature verification uses constant-time comparison, not a direct `==`/`bytes.Equal` that's timing-sensitive
- [ ] There is replay protection via a timestamp window and/or nonce tracking
- [ ] The signing secret is separate from other secrets (see `secrets-and-key-management.md`)
- [ ] The raw request body used for verification is the actual bytes received, not a re-serialized version after decoding