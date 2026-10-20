# Authorization and Resource-Level Access (Go)

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** Go services with authenticated, privileged or tenant/resource-scoped actions.
> **Triggers:** authorization, IDOR, owner, role, resource ID, tenant, permission, delegated access.

## 01 — Applicability

Apply whenever a handler or service reads, changes, or grants access to a resource whose visibility or mutation is restricted. Authentication, public access and authorization are separate questions. For genuinely public resources, explicitly establish public policy instead of inventing a user-owned permission requirement.

## 02 — Principle / Rule

- Establish the authenticated principal from trusted server-verified identity, never from client-supplied user or role fields.
- Check **both** permitted action/capability and scope/relationship to the particular resource on each relevant request, including nested resources and indirect lookups. Knowing an identifier is not permission.
- Default deny if scope, role, resource ownership or privilege provenance cannot be established; enforce on the server, not only via hidden UI controls.
- An application-internal role must not be represented as independently verified external legal authority merely because it authorizes an internal action.
- Never infer that any two roles are mutually exclusive, transferable or delegable without owning product/project policy.

## 03 — Rationale & Risk

A valid session plus a broad role check can still permit horizontal privilege escalation when an attacker supplies another organization's resource ID. Inconsistent checks across read/write/endpoints create IDOR. Unexamined privilege grants can turn an internal role into an incorrect external trust claim.

## 04 — Application Guidance

1. Identify action, principal, target resource and explicit authorization relationship before the operation.
2. Query/filter within the allowed scope or check a resource relationship using trusted server-side data; do not use a client's `organization_id` as proof of membership.
3. Centralize a meaningful reusable policy check when needed; always call it at all relevant entry points. Cross-tenant queries, background jobs and administrative exceptions need explicit policy.
4. Prefer 404 where resource existence itself is confidential; otherwise 403 can be suitable. Choose consistently by the API's disclosure policy; do not reflexively return one code in every case.
5. For privilege creation/change, enforce project-defined eligibility and authorized actor/resource linkage; use durable attribution where the product requires it.

**Illustrative failure:** `GET /organizations/{org}/private-settings` verifies a session and a generic `owner` label but does not verify that this person holds the permitted relationship **to this organization**.

## 05 — Verification

Test unauthenticated, wrong-role, same-role/wrong-resource, cross-tenant, deleted/revoked-role, stale-session and properly authorized cases. Test any legitimate public/delegated exceptions. Verify checks on both handler and service/bypass paths as applicable; record actual executed tests rather than claims.

## 06 — Boundaries & Trade-offs

This guidance does not define an application's role taxonomy or legal-representation semantics. Policy ownership is project-specific. Scope decisions and grant/revocation concurrency may demand DB constraints/transactions; do not treat a successful guard function as proof of race safety. Independence/approvals follow owning project security gates.

## References

- https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
- https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html
