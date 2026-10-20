# S1 Generic Output Contract — Proposed

The deliverable is an inspectable **implementation-consumable Solution Delivery Bundle**, not a label saying “design done.”

## Required output interfaces

| ID | Logical output | Required coverage and conformance |
| --- | --- | --- |
| O1 | Shared solution decisions | Traceable material decisions, rationale, alternatives only when consequential, delegated authority vs approval pending; architecture/ownership and cross-boundary dependency decisions |
| O2 | Interfaces and state/invariant contracts | Consumer/producer responsibilities, data/API interactions and error/result semantics, state ownership, persistence/consistency requirements, authorization/trust boundaries and version expectations to the extent required for safe implementation |
| O3 | Experience/interaction contracts | Pre-effect consequence disclosure, action availability, success/incomplete/conflict/unauthorized states, durable user-visible meaning and relevant applicable UI/UX authority without inventing product commitments |
| O4 | Verification obligations | Each acceptance/invariant mapped to expected validation observable(s), responsible future verification boundary, risk/negative-path coverage, required independent evidence and known unavailable test mechanisms |
| O5 | Review, trace and handoff evidence | Original source refs+revisions → all O1–O4 decisions/output sections; internal review findings, relevant Human gate IDs/decisions with exact artifact revisions, unresolved blockers, checker provenance, output revision and consumer-specific readiness limits |

Logical O1–O5 can be sections of one deliverable or linked files: semantic coverage is mandatory, file count is not. Each component must be addressable by stable heading/ID.

The **external Solution Delivery Bundle** must also satisfy the [minimum cross-Space handoff semantics](../../../space-formation/contract-and-readiness.md): identify its actual versioned payload artifacts (O1–O5 sections/files and any separately consumable supporting contracts), their type, ownership, authoritative standing, source refs, intended consumers, evidence and consumption limits. A required interface artifact can serve multiple consumer Spaces while keeping a **single pinned authoritative revision**. Do not confuse an artifact listed in the bundle with a new authority or a completed downstream compatibility check.

A **consumer-required API Contract** may be represented in O2 or as an additional linked, explicitly typed interface artifact when the concrete assignment requires independently addressable FE/BE consumption. Describe operations, input/output/error/result semantics, security/identity and version expectations to the required level, without inventing project-approved endpoints. Real machine-readable OpenAPI or other project-owned formal specifications may be produced **only when authorized and required**; otherwise report the intended interface and its **proposed/not-yet-binding** status, formalization owner and gap. Do not make a separate API document mandatory for every S1 invocation.

## Compatibility and completeness

Before reporting **COMPLETE / candidate for Human acceptance**:

1. Original authority and accepted behavioral constraints are reflected without unsupported reinterpretation, with explicit scoped omissions.
2. Shared API/data/experience/error/identity obligations are coherent together, including failure paths, not merely happy-path narrative.
3. Each material interface says who produces and consumes it; any consumer-critical linked artifact has a real ref/revision and one authority owner, and its conformance/approval standing is explicit. Stack-specific binding honors actual project architecture without hardcoding a stack into S1's reusable contract.
4. O4 directly traces to original acceptance, including abuse/security risks where in scope. Review is not a proof of running software.
5. O5 makes missing/conditional decisions visible and identifies if they block a consumer. An unresolved decision that a consumer must not invent → **BLOCKED/PARTIAL**, not implementation-ready.

## Output state vs decision state

- **Production result:** `COMPLETE`, `PARTIAL`, `BLOCKED`, `FAILED`; verification can additionally be `UNVERIFIED` with scope.
- **Decision standing per material item:** `APPROVED SOURCE` (existing authority), `DELEGATED DECISION` (within assignment scope), `PROPOSED / HUMAN REVIEW REQUIRED`, `UNRESOLVED`, or `REJECTED / SUPERSEDED`. These are annotations, not a new operational workflow engine.
- **Human acceptance:** independently records `ACCEPTED FOR DOWNSTREAM`, `CHANGES REQUESTED`, or `NOT YET DECIDED`. Human acceptance binds an exact output revision; a complete deliverable, supervised continuation, or autonomous execution is **not** automatically accepted project specification.
- **Evidence level:** `DESIGN REVIEWED` / `NOT REVIEWED`; never call design-only evidence `RUNTIME VERIFIED`.

The output path/revision, approved downstream bindings and any mutable state belong to the concrete invocation, not this generic file.
