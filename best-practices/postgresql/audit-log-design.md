# audit-log-design.md

**Location:** `postgresql/audit-log-design.md`

**Principle**
For a table that serves as an audit trail, the ban on `UPDATE`/`DELETE` should ideally be enforced at the database level (`REVOKE`, a trigger that rejects modification) — not just an application-layer rule, since the application layer can be bypassed by direct DB access. Equally important: the audit log itself must be designed with a deliberate view of what may be logged vs. what must be redacted — an audit log that records raw payloads without filtering easily becomes a quiet PII leak.

**Bad**
```sql
-- no DB-level protection, the application "promises" not to UPDATE/DELETE
CREATE TABLE audit_log (id UUID, actor_id UUID, action TEXT, payload JSONB);
```
```go
auditLog.Payload = fmt.Sprintf("%+v", request) // the entire request goes into the log, including PII
```

**Good**
```sql
CREATE TABLE audit_log (id UUID, actor_id UUID, action TEXT, payload JSONB);
REVOKE UPDATE, DELETE ON audit_log FROM app_user; -- enforced at the DB level
```
```go
auditLog.Payload = redactSensitiveFields(request, []string{"password", "national_id", "card_number"})
```

**Checklist**
- [ ] `UPDATE`/`DELETE` on the audit table is `REVOKE`d at the DB level for the application role
- [ ] There is an explicit list of fields that must be redacted before entering the audit log
- [ ] The audit log does not record raw, unfiltered payloads by default
- [ ] There is a periodic review of what is actually being captured in production audit logs