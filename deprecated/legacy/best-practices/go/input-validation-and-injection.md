> **Location:** `best-practices/go/input-validation-and-injection.md`

# Input Validation & Injection Surface

## 1. Log injection: unsanitized user input in log lines enables log forging

**Principle:** Writing user-controlled input directly into log lines lets an attacker inject characters (newlines, terminal escape sequences, log-format delimiters) that forge fake log entries, corrupt log parsing, or in the worst case exploit a downstream log viewer that interprets escape sequences.

### Bad
```go
logger.Info(ctx, fmt.Sprintf("login attempt for user: %s", username))
```
If `username` is attacker-controlled and contains `"\nERROR: system compromised, admin override granted"`, naive log viewers or line-based log parsers can be tricked into treating the injected text as a separate, legitimate-looking log entry.

### Good
```go
logger.Info(ctx, "login attempt", zap.String("username", username))
```
Structured logging (fields passed separately from the message, not interpolated into a free-text string) means the logging library controls escaping/encoding of field values — a newline in `username` is encoded as part of the field's value, not able to inject a fake line into the log stream.

**Checklist:**
- Prefer structured logging (fields as separate parameters, not string-interpolated into the message) for any log line that includes user-controlled input.
- If free-text interpolation is unavoidable, strip/escape control characters (newlines, carriage returns) from user input before it reaches a log line.

---

## 2. Shelling out with user input risks command injection

**Principle:** Passing user-controlled data into a command executed via a shell (`sh -c "..."` with interpolated input, or any exec path that goes through shell interpretation) lets an attacker break out of the intended argument and inject additional commands.

### Bad
```go
cmd := exec.Command("sh", "-c", fmt.Sprintf("convert %s output.png", userProvidedFilename))
```
A filename like `"; rm -rf / #"` gets interpreted by the shell as a separate command, not as a literal filename.

### Good
```go
cmd := exec.Command("convert", userProvidedFilename, "output.png")
```
`exec.Command` without going through `sh -c` passes arguments directly to the program's argv — no shell interpretation, so there's no injection surface via shell metacharacters. Additionally, validate `userProvidedFilename` against an allowlist pattern (expected filename format) before use, regardless.

**Checklist:**
- Avoid `sh -c` (or any shell-interpreting exec path) with user-controlled input entirely — use `exec.Command(program, arg1, arg2, ...)` directly, which doesn't invoke a shell.
- Even without shell interpretation, validate user input against an expected format (allowlist) before passing it to any external process — don't rely solely on avoiding the shell as the only safeguard.

---

## 3. Validate at the boundary, not scattered through business logic

**Principle:** Input validation belongs at the entry point (HTTP handler, GraphQL resolver, message consumer) where untrusted data first enters the system — not re-checked ad-hoc at various points deeper in the call stack. Scattering validation makes it easy to miss a path, and makes it unclear which layer is actually responsible for guaranteeing data is well-formed.

**Checklist:**
- Once data has passed boundary validation and is represented by a typed struct (not a raw string/map), downstream code should be able to trust its shape — if downstream code still needs defensive checks, that's a signal boundary validation is incomplete, not a reason to add more scattered checks deeper in.
- For each new entry point (new endpoint, new resolver, new consumer), explicitly confirm what validation runs before the payload reaches business logic — don't assume "some layer probably checks this."