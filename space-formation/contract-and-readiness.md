# Space Contract, Compatibility and Readiness

> This is a **semantic contract floor** for reusable Spaces, not a universal YAML schema, mandatory file template, Space catalog, workflow engine or claim of tested runtime mechanics.

## Two independently inspectable layers

| Layer | Source/owner | Contract question |
| --- | --- | --- |
| **Reusable Space capability** | Human-approved Harscode experimental Space definition | Which classes of input are accepted, what bounded production is permitted, and which exact output types, quality and evidence are guaranteed or honestly refused? |
| **Concrete invocation binding** | Current owning project sources + **Human-direct** authorization to the Space Coordinator (Balad advisory only) | Which project-specific values, desired behavior, repo revision, permissions and acceptance evidence instantiate that contract **without changing its generic meaning**? |

Project-agnostic does **not** mean unconstrained. Define strict generic quality/format/conformance obligations. Do not store feature-specific endpoint lists, Kencleng semantics or historical solution decisions in a reusable definition.

### Required content of a reusable definition

For the **one coherent external responsibility** of the Space, make these independently checkable (one compact Markdown document can suffice):

1. **Identity/scope/version:** what the capability is for; explicitly excluded work; owning definition, status and intended reuse context.
2. **Generic input contract:** required/optional inputs, form/type, provenance/approval/version constraints, cross-input consistency requirements, scoped authorization and refusal for nonconforming input.
3. **Generic output contract:** required/conditional output **artifact kinds** and their own conformance/producer/consumer ownership, form/format, invariants, evidence obligations and versioned external handoff. A Space may produce multiple typed artifacts for different consumers; do not require one physical output file or one artifact per Agent.
4. **Result semantics:** what complete, partial, failed, unknown or blocked means; what must *not* be claimed as successful; where stop/escalation occurs.
5. **Internal composition:** the **Space Coordinator Agent** role as the Human-invoked internal work coordinator (not automatically a separate native process), why one/more Specialists are needed, bounded assignments, source access, independent review and capability/knowledge requirements.
6. **Execution boundary and modes:** `supervised` is the **default**. `autonomous` requires explicit Human choice for the **concrete invocation**. Define Human visibility/continuation milestones separately from non-waivable consequence-based approval gates; specify permitted paths/actions, tool and isolation requirements, and what enforcement has been verified.
7. **Durable output and evolution:** return artifacts/evidence consumers can inspect without old chat; approved definition versus invocation state; version/change impact and improvement-request path.
8. **Readiness/assurance and Human Approval Gates:** determine during formation which consequential transitions require Human authority, what exact artifact/decision revision and evidence are presented, what action is blocked, and when approval becomes valid/invalid; include output acceptance as separate from execution authorization.

The list defines *content*, not eight files or eight mandatory process stages. Use proportionate precision; don't require a full threat model for a low-risk file-format conversion, and don't hand-wave security when a Space can grant privileged access.

### Minimum cross-Space handoff semantics

A producing Space returns an **inspectable delivery package**: one logical handoff with zero or more individually addressable payload artifacts, as required by its output contract and concrete assignment. The package can be a document section/index plus linked files; **no mandatory JSON/YAML schema, file count, directory, artifact registry or global validator** is implied. An empty payload is valid only for a truthful blocked/failed report, never for a falsely complete required output.

Every handed-off package must make these **minimum facts discoverable** (explicitly `unknown`, `not performed` or `not applicable` where true, never an invented value):

| Required handoff fact | Meaning |
| --- | --- |
| **Producer and contract identity** | Space capability/definition revision, concrete invocation/binding ref, declared output contract/type and version or immutable owning ref |
| **Payload artifact index** | Each artifact's logical type/purpose, real location + immutable/reconstructable revision, accountable producer/owning authority, intended consumer(s) and linked output-contract obligation; distinguish **required**, conditional, supporting or not produced |
| **Input provenance** | Pinned owning original sources and material upstream artifact revisions supporting the payload; no replacement of project authority with a summary |
| **Delivery and evidence** | Result/completeness with required-artifact coverage, actual validation/review evidence refs and limits; distinguish performed checks from proposed tests |
| **Decision and acceptance standing** | Delegated/proposed/unresolved decisions, applicable Human gate decisions tied to revision/scope, **whether downstream use is authorized** separately from production COMPLETE |
| **Consumption constraints** | Exact blockers, missing content/format, allowed scope, relevant compatibility dependencies and revalidation conditions if artifacts change |

This is an **external handoff contract**, not a prescribed internal Specialist artifact format. The producing Space's reusable output contract defines the semantic guarantees and which payload artifacts are required or conditional. The **owning project** resolves actual artifact locations, canonical authority, approval and protected-write policy. A package index does **not** create authority over an underlying project artifact.

**Multiple consumers / shared interface example:** A solution-design Space may expose a versioned **API interface contract** for a Frontend Space and Backend Space as a linked payload alongside its solution decision bundle. The output must name the interface contract's owning authority, current decision/approval standing, exact revision, coverage and both consumers. FE and BE must check the **same compatible authoritative interface baseline**, not independently infer endpoints, errors or schemas. A narrative O2 design contract does **not** automatically become an approved machine-readable OpenAPI file; creating/updating a protected formal spec needs project authorization. API artifacts are conditional on actual consumers and constraints, **not universal mandatory files**. A downstream implementation may produce code, migrations or tests instead, each indexed with its own conformance and evidence.

A consumer checks both the generic **output artifact type/guarantee → input requirement** and the concrete **artifact revision/authority/content → assignment binding**. A well-formed envelope never implies an artifact is approved, complete or safe to consume. If a required shared artifact is missing, contradicted, unapproved or version-incompatible, hold only the dependent consumption and record the exact gap.

### Human Approval Gate Contract (formation-time semantic requirement)

For each materially consequential transition, specify **(a) trigger** (decision or output), **(b) required evidence** and immutable/reconstructable artifact revision, **(c) authorized Human/owning authority**, **(d) blocked downstream action**, **(e) exact resume scope and condition** including material-change invalidation. A valid decision must be recorded at an approved durable location and checked against the affected output revision before proceeding. Missing, stale, denied or scope-mismatched approval → affected work **BLOCKED** in both modes; never infer consent from silence, `autonomous` mode, an earlier formation decision or an unrelated approval.

**Supervised continuation checkpoint** is distinct: the Human can inspect intermediate assignments/results and say `continue` at meaningful milestones selected for the actual invocation. This is operational steering, **not** automatic acceptance of a Specialist's output as a binding project decision. Do not demand Human approval after every Agent handoff. In autonomous mode, Coordinator advances ordinary authorized work but still halts at all mandatory Human gates. Require concrete sandbox/tool enforcement proportionate to risk; a prompt-based pause alone does not guarantee secure prevention.

**Illustrative Builder, not a formed capability:** after a Planning Specialist produces a reviewed Techplan, **Human approval of that Techplan's exact revision** is required **before Build work using it**. The Coordinator may autonomously plan/review, but cannot dispatch the gated Build action until approval and associated write scope are valid. A material Techplan revision invalidates the affected approval. Security/protected changes may impose additional conditional gates; final delivery acceptance is separate. An S1 solution-design-only Space does **not** inherit this Builder gate automatically.

**Coordinator / authority:** Human invokes the Space Coordinator directly. Balad may advise on choices and inspect provided results but cannot dispatch, request action from, resume, or communicate directly with Coordinator. Coordinator cannot self-approve gates or change the mode or approval rules unilaterally. Mode, pinned sources, gate decisions and continuation permissions belong to the concrete invocation's durable state, not to ChatGPT memory.

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

If compatibility fails, identify the first broken producer/consumer edge, affected outcome, and whether the remedy belongs to project binding, contract adaptation/versioning, Human product decision, or a genuinely new capability. Balad may **advise the Human** about cross-Space compatibility, but does not coordinate execution or handoffs with Space Coordinators. Each Human-invoked Space validates its own received input conformance.

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

An internal Specialist or Space may suggest a change to generic I/O, quality checks, model binding, knowledge or composition based on actual work. Return **evidence + proposed delta + affected upstream/downstream contracts + migration/version impact** to the Human. The Human may consult Balad for advisory review and independently bring the proposal to Human-led formation review; Balad does not contact the Coordinator. Protected project meaning and active invocation scope cannot change just because an internal Agent recommended improvement.
