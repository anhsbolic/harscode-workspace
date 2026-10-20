# openapi-spec-first-drift.md

**Location:** `restapi/openapi-spec-first-drift.md`

**Principle**
If a spec (OpenAPI/Swagger) is treated as the source of truth for the API contract, sync discipline has to be actively maintained — a stale spec is more dangerous than no spec at all, because API consumers trust it. Before committing a change to a handler/schema, make sure generated code (client/server stubs) has been regenerated from the latest spec, and that the error-response shape matches exactly too, not just the happy-path schema.

**Bad**
```yaml
# openapi.yaml says the error response is: { "error": "string" }
```
```go
// the actual handler sends a different shape, never synced back to the spec
json.NewEncoder(w).Encode(map[string]string{"message": "not found", "code": "404"})
```

**Good**
Checklist before committing a change to an endpoint:
1. `openapi.yaml` is updated first, reflecting the intended change (request/response shape, including the error shape)
2. The generator (`oapi-codegen`/`openapi-typescript`/equivalent) is rerun
3. The handler is verified to match the generated types exactly, including the error-response shape
4. The generated-code diff is reviewed — unexpected changes in generated files are a signal the spec and implementation had already drifted

**Checklist**
- [ ] `openapi.yaml` is updated before or alongside a handler change, not afterward
- [ ] Generated code is rerun on every spec change and the result is committed
- [ ] The error-response shape, not just the happy path, is defined in the spec and validated to match
- [ ] There is a periodic (even manual) check comparing the actual handler against the spec for endpoints that change infrequently