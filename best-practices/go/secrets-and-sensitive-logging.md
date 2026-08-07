> **Location:** `best-practices/go/secrets-and-sensitive-logging.md`

# Secrets & Sensitive Data in Logs and Errors

## 1. Logging an error value can leak whatever sensitive data it wraps

**Principle:** An error returned from an upstream call (HTTP client, DB driver, third-party SDK) can embed response bodies, headers, or query parameters — which may contain tokens, API keys, or PII. Logging `err` directly assumes the error's string representation is safe, which is often not verified.

### Bad
```go
resp, err := paymentClient.Charge(ctx, req)
if err != nil {
    logger.Error(ctx, "payment failed", err) // err might embed the full request/response, including card data or tokens
    return err
}
```

### Good
```go
resp, err := paymentClient.Charge(ctx, req)
if err != nil {
    logger.Error(ctx, "payment failed",
        zap.String("order_id", req.OrderID),
        zap.String("error_code", classifyError(err)), // a sanitized, known-safe classification
    )
    return fmt.Errorf("payment charge failed for order %s: %w", req.OrderID, err) // %w still fine for errors.Is/As internally, just don't print the full chain to an untrusted sink
}
```

**Checklist:**
- Before logging an error from a third-party client/SDK verbatim, check whether that client's error type can embed request/response payloads — if so, log a sanitized summary (error code, category) instead of the raw error string.
- This applies especially to payment gateways, auth providers, and any client interacting with systems that handle credentials or PII — assume the error *can* contain sensitive data unless the client's documentation says otherwise.

---

## 2. Logging a struct wholesale (`%+v`, full JSON marshal) leaks any sensitive field it contains

**Principle:** `fmt.Sprintf("%+v", user)` or `json.Marshal(user)` dumps every field, including ones that shouldn't appear in logs (password hashes, tokens, national ID numbers, full card numbers). This is easy to introduce during debugging and easy to forget to remove.

### Bad
```go
logger.Info(ctx, fmt.Sprintf("processing user: %+v", user)) // dumps every field, including user.PasswordHash, user.NationalID
```

### Good
```go
logger.Info(ctx, "processing user", zap.String("user_id", user.ID)) // only the fields actually needed for debugging context
```
For types that are frequently at risk of being logged wholesale (auth-related structs especially), implement a custom `String()`/`MarshalJSON()` method that redacts sensitive fields by default, so even an accidental `%v`/`%+v` doesn't leak them:
```go
func (u User) String() string {
    return fmt.Sprintf("User{ID: %s, Email: %s}", u.ID, maskEmail(u.Email)) // no PasswordHash, no NationalID
}
```

**Checklist:**
- Never log a struct via `%+v`/`%v`/wholesale JSON marshal if it contains credentials, tokens, or PII — log specific, deliberately chosen fields instead.
- For structs that hold sensitive fields by design (user credentials, payment info, auth tokens), consider a custom `String()`/`MarshalJSON()` that redacts by default, as a defense against accidental wholesale logging elsewhere in the codebase.
- Treat this as part of code review for any new struct with fields like password, token, secret, national ID, card number — check every place that struct gets logged.