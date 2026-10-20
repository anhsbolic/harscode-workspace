# Go Secrets and Sensitive Data in Logs

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** Go application logging, errors, HTTP diagnostics, personal data and credential handling.
> **Triggers:** secret, PII, token, logging, log.Printf, slog, fmt, MarshalJSON, redaction, error chain.

## 01 — Applicability

Use whenever a service logs identities, requests, errors or object structs; treat authentication, identity and sensitive personal data as higher-risk. Apply the owning project's retention, privacy, incident and audit obligations.

## 02 — Principle / Rule

- Never log raw credentials, tokens, session IDs, signing keys, private payloads, unnecessary PII or full user-controlled bodies.
- Treat wrapped errors and formatted structs as **potentially sensitive**. Formatting with `%+v` or serializing entire structs can expose fields not obvious at the callsite.
- Prefer an explicit allowlist of safe structured fields (event name, bounded error category, trace/correlation ID, permitted pseudonymous reference) rather than a broad object dump.
- Do **not** change a model's `MarshalJSON` solely for log redaction when the same serialization may be used for API responses, persistence or signatures. Separate log projection or explicit logger attributes from canonical serialization.
- Prevent log injection by structuring user input or escaping control characters when unavoidable; logging an error is not proof it has been sanitized.

## 03 — Rationale & Risk

Error chains may include SQL strings, URLs with query credentials, connection strings and identifying fields. A serializer-based redaction patch can accidentally corrupt expected API or storage data while masking an observability issue.

## 04 — Application Guidance

1. Classify each logged field by purpose and exposure; keep identity/authorization decisions auditable without raw secrets.
2. Define a minimal safe event schema: action, result, non-sensitive reason category, permitted resource reference and correlation ID.
3. For error logging, report a stable error code/category and bounded operation name; inspect library error types before emitting their `Error()` text.
4. Ensure client-facing errors use safe public messages while internal trace details stay access-controlled.
5. Test logging through both success and failure paths; audit debug middleware, panic handling, HTTP clients and third-party libraries for payload logging.
6. When a project requires PII audit data, store in the appropriate controlled channel with explicit safeguards; do not quietly omit legally material evidence or expose it in ordinary application logs.

## 05 — Verification

Capture representative logs from successful requests, rejected authorization, malformed input, SQL errors and retries. Seed synthetic secret markers and assert they never appear in logs, traces, metrics or client responses. Verify API and persistence serialization remain unchanged by logging-only redaction.

## 06 — Boundaries & Trade-offs

Over-redaction can hinder diagnosis; use bounded, authorized correlation instead of raw payloads. Encryption at rest does not make logs safe. This document is not an organization's full privacy/audit retention policy.

## References

- https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html
- https://go.dev/doc/security/best-practices
