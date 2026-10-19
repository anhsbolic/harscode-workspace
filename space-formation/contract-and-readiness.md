# Space Contract, Compatibility and Readiness

> This is a **semantic contract floor** for reusable Spaces, not a universal YAML schema, mandatory file template, Space catalog, workflow engine or claim of tested runtime mechanics.

## Two independently inspectable layers

| Layer | Source/owner | Contract question |
| --- | --- | --- |
| **Reusable Space capability** | Human-approved Harscode experimental Space definition | Which classes of input are accepted, what bounded production is permitted, and which exact output types, quality and evidence are guaranteed or honestly refused? |
| **Concrete invocation binding** | Current owning project sources + scoped Human authorization, coordinated by Balad | Which project-specific values, desired behavior, repo revision, permissions and acceptance evidence instantiate that contract **without changing its generic meaning**? |

Project-agnostic does **not** mean unconstrained. Define strict generic quality/format/conformance obligations. Do not store feature-specific endpoint lists, Kencleng semantics or historical solution decisions in a reusable definition.

### Required content of a reusable definition

For the **one coherent external responsibility** of the Space, make these independently checkable (one compact Markdown document can suffice):

1. **Identity/scope/version:** what the capability is for; explicitly excluded work; owning definition, status and intended reuse context.
2. **Generic input contract:** required/optional inputs, form/type, provenance/approval/version constraints, cross-input consistency requirements, scoped authorization and refusal for nonconforming input.
3. **Generic output contract:** produced output type, form/format, invariants, quality, evidence/verification obligations, owner/consumer handoff and traceable source/revision.
4. **Result semantics:** what complete, partial, failed, unknown or blocked means; what must *not* be claimed as successful; where stop/escalation occurs.
5. **Internal composition:** why one/more Specialist Agents are needed, bounded assignments and shared/isolated context, independent checks where required, model/effort/tool/knowledge constraints.
6. **Execution boundary:** permissible paths/actions, project binding, sandbox/tool dependencies, sensitive-change Human approvals, and which enforcement is actually verified versus only described.
7. **Durable output and evolution:** return artifacts/evidence consumers can inspect without old chat; approved definition versus invocation state; version/change impact and improvement-request path.
8. **Readiness/assurance:** which conditions must be tested before invocation, including honest treatment of independence/security, and who can accept resulting outputs.

The list defines *content*, not eight files or eight mandatory process stages. Use proportionate precision; don't require a full threat model for a low-risk file-format conversion, and don't hand-wave security when a Space can grant privileged access.

### Example: REST API Production capability (illustrative, not a formed Space)

**Generic IN:** approved API contract defining required operations and error semantics; target repo/revision and stack constraints; authorized write scope and applicable security rules.

**Generic OUT:** implemented REST operations conforming to supplied API semantics and types, change references, applicable automated test/contract-conformance evidence, and explicit untested cases or limitations. Reject a missing or contradictory operation contract instead of inventing product requirements.

**C1 binding:** only operations and identity/Organization/Owner meanings **later approved by C1 solution work**. Login/logout are not guaranteed C1 scope simply because this capability can implement REST APIs.

Example failure: if the assigned security mechanism needs a Human protected-write approval not supplied, report **BLOCKED** for that work, not successful production. If backend code is produced but not verified, report delivered files with **UNVERIFIED** evidence rather than a fully conforming API.

### Two-level inter-Space compatibility

For each material **producer output → consumer input** edge, compare:

| Dimension | Generic capability fit | Concrete binding fit |
| --- | --- | --- |
| Type/format | Producer's declared output kind/format fulfills downstream required input, including usable evidence | Actual artifact/source/schema versions match consumer's expected project binding |
| Semantics | Producer guarantees relevant generic invariants and transparent failure state | Content satisfies current product/engineering decisions and consuming assignment obligations |
| Authority/scope | Output may legitimately be reused and input preconditions are satisfiable | Actual source approvals, target revisions, permissions and security boundaries are compatible |
| Acceptance/evidence | Consumer can independently check the conformance threshold | Required project-specific checks have observed evidence, or are marked unverified |

**Proposed** edges are hypotheses; **contract-checked** edges require inspecting real formed definitions; **consumed/validated** edges require the real output to be checked by the consumer. Do not collapse these into a single PASS.

At parallel joins, verify that **all required outputs and versioned interfaces** are jointly compatible. Independent assurance must also consume **original acceptance authority** directly; it may reject a solution that is internally consistent but violates that authority.

If compatibility fails, identify the first broken producer/consumer edge, affected outcome, and whether the remedy belongs to project binding, contract adaptation/versioning, Human product decision, or a genuinely new capability. Balad owns cross-Space coordination; an invoked Space validates its **own received input conformance**.

## Definition approval versus operational claims

| Claim | Minimum evidence |
| --- | --- |
| **PROPOSED** | Candidate contract and formation reasoning, no formation approval |
| **FORMED / DEFINITION APPROVED** | Explicit Human approval, persisted inspectable Space definition/version, declared bounds |
| **CONFIGURED / UNVERIFIED** | Relevant Agent/tool/harness wiring declared, but no demonstrated readiness |
| **READINESS-CHECKED** | Actual bounded input, references, tool access, permission/sandbox, Agent routing and applicable independence checks reported with results |
| **INVOCATION-AUTHORIZED** | Human/scope approval valid for the concrete invocation; not implied by formation |
| **OUTPUT VERIFIED** | Real production and conformance/assurance evidence, with consumer acceptance where required |

These are descriptive **claims**, not an imposed sequential state machine. A Space can be formation-approved and still not invocable.

## Improvement without silent contract drift

An internal Specialist or Space may suggest a change to generic I/O, quality checks, model binding, knowledge or composition based on actual work. Return **evidence + proposed delta + affected upstream/downstream contracts + migration/version impact**. Balad reports/routes it; Anhar + ChatGPT review the reusable change. Protected project meaning and active invocation scope cannot change just because an internal Agent recommended improvement.
