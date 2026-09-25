# Harscode Orchestrator Protocol v0.1

> Status: Pilot Candidate
> Scope: coordination semantics; tooling/storage/harness implementation remains project-defined.

## Purpose

Transform approved product intent into coordinated, verifiable delivery while preserving authority boundaries and making current state reconstructable.

## Core objects

- **Parent Outcome** — approved larger result.
- **Work Unit** — bounded outcome that must become true.
- **Work Graph** — current cross-Work-Unit coordination topology: known Work Units, canonical HARD/SOFT dependency edges, and produced milestone/rendezvous conditions. It coordinates outcomes; it does not own implementation detail.
- **Run** — one execution occurrence of a workflow activity.
- **Role** — semantic responsibility.
- **Specialization** — project-specific refinement of a Role.
- **Participant** — human or non-human executor identity.
- **Session** — bounded execution context used by a Participant.
- **Decision** — governance question/result; not itself work.
- **Finding** — observed evidence/problem; may affect multiple Work Units.
- **Blocker** — active inability to progress; always has next-action ownership.
- **Dependency** — causal prerequisite, HARD or SOFT.
- **Artifact** — durable output of a Run or Decision.
- **Event** — material chronological fact.
- **Project Learning** — promoted reusable evidence-backed knowledge; not authority.
- **Harscode Space** — optional durable execution/evidence container.
- **Control Surface** — current-state projection; never an independent source of truth.

## Work Unit contract

Every Work Unit has exactly one primary type:

- `DELIVERY`
- `ENABLER`
- `RECONCILIATION`
- `VERIFICATION`

A Work Unit has a stable definition and one current-state projection of what is true now.

Conceptually:

```text
Work Unit
├── Definition
│   ├── ID / title / type / parent
│   ├── outcome / scope
│   ├── completion condition
│   └── coordination ownership
└── Current State
    ├── execution status
    ├── scheduling state when active/applicable
    ├── horizon / readiness
    ├── current Run / milestone
    ├── Human gate / authority sync
    └── active blocker
```

For every current-state field there is exactly one current value. Updating current state replaces that field's prior current value; historical values must not remain as competing current-state sections in the same record.

Work Unit identity is not a repo/path/issue/PR/session/run. Structural evolution is traceable through `split_from`, `merged_from`, `derived_from`, `supersedes`, and `superseded_by`.

Cross-Work-Unit dependency topology has one canonical owner: the Work Graph. A Work Unit record may display a derived dependency summary for readability, but it must not become an independently maintained second dependency truth.

## Roles and assignment

Canonical roles:

- Human Authority
- Orchestration Operator
- Explorer
- Planner
- Implementer
- Reviewer
- Verifier

Execution assignment lives primarily on a Run:

```text
Run
→ Role
→ Specialization
→ Participant
→ Session
```

Assignee means Participant, never Session. A Work Unit may additionally name a Coordination Owner.

Every non-human execution path must have a discoverable human escalation route. A one-to-one human pair is optional.

## Decision classes

- Routine Execution
- Delivery Decision
- Authority Decision
- Protected Authorization

Delivery Decision chooses how to execute settled authority. Authority Decision establishes, changes, or resolves material authority. When uncertain, treat the question as Authority Decision until ownership is identified.

## State

Execution status:

```text
NOT_STARTED | ACTIVE | WAITING | BLOCKED | WAITING_HUMAN | STALLED | VERIFYING | DONE | CANCELLED
```

Scheduling state:

```text
PARKED | QUEUED | DISPATCHED | RUNNING
```

Human horizon:

```text
NOW | NEXT | LATER
```

Severity:

```text
INFO | ATTENTION | HIGH | CRITICAL
```

These are independent dimensions.

Scheduling describes active scheduling posture only. When a Work Unit is terminal (`DONE` or `CANCELLED`), it has no active scheduling posture in the semantic model. A concrete representation may omit, null, or mark scheduling non-applicable; it must not invent a terminal scheduling value such as `DONE` unless the protocol explicitly adds one later.

## Dependencies and blockers

Dependency types may include AUTHORITY, CONTRACT, DELIVERY, DATA, ENVIRONMENT, VERIFICATION, HUMAN_DECISION, and EXTERNAL. Scope dependencies to the affected Work Unit/batch rather than blocking unrelated work.

Every active Blocker records classification, affected work, severity, next-action owner, required action, evidence/source, and safe unaffected work.

## Runs, history, and loops

Filesystem names do not encode workflow chronology. Runs and Events do.

Events are append-only material coordination history. Record facts such as Run dispatch/completion/failure, Work Unit state transitions, Human Decisions, Blocker open/close, milestone promotion, and Work Graph structural amendments. Events explain how current state was reached; they are not current state themselves. Detailed command/read telemetry remains Run-local rather than being promoted into global Event history.

Re-entering a phase creates a new Run. A repeated Run requires meaningful delta: new evidence, authority decision, material plan amendment, different implementation approach, resolved dependency, or specific defect correction.

Repeated unresolved causes become `STALLED`; stop mechanical workflow repetition, diagnose, and reroute.

## Authority and learning

Canonical project authority defines what should currently be true in its owned concern. Code/runtime is evidence of what is implemented.

Approved authority-affecting change:
```text
Finding → Decision → canonical authority update → downstream reconciliation
```

Mandatory authority synchronization gates Work Unit completion.

Project Learning follows:
```text
Observation → Learning Log → Learning Proposal → human review → promoted Project Learning
```

Learning does not become authority.

## Scoped retrieval

Knowledge is pull-based and progressively disclosed:

```text
task scope + role + specialization + workflow phase
→ routing index
→ applicable subindex
→ minimum relevant documents
```

Reading an index does not imply reading its descendants. Reuse valid Project Learning before scheduling redundant Exploration.

## Harscode Space

A dedicated Space is optional. Create one when durable execution history provides meaningful coordination/reuse/audit value: multiple Runs/Sessions, cross-role coordination, review/rework, Decisions, Blockers, handoffs, learning logs, or reconciliation.

Storage is project-defined. Logical durability is required; physical co-location with code is not.

## Control Surface

Project the current state: current outcome, NOW/NEXT/LATER, active/blocked/stalled work, human attention, ready work, sessions, and next actions.

The Control Surface is derived from the Work Graph, Work Unit Current State, and open Decisions/Blockers. It must be regenerable from those underlying orchestration records. If it conflicts with underlying current state, the Control Surface is stale and must be regenerated; it does not become authority by recency or wording.

## Runtime resolution

Machine-local runtime bindings are not project authority. A target project may provide local runtime configuration for paths and Human-declared available models.

Model selection is fit-for-purpose, not strongest-by-default. The Orchestrator reads the Human-owned registry, chooses the least costly sufficiently capable model, and MUST obtain explicit Human approval before using any model marked as approval-required. The Orchestrator must not mutate the model registry.

The Human ↔ Orchestrator pairing model is configured separately from per-Run execution model selection. Pairing escalation does not imply stronger execution models, and a stronger execution model does not imply pairing escalation.

## Workflow evolution

The Orchestrator may identify a workflow gap, use temporary routing, and propose reusable guidance. It must not silently promote a new canonical Harscode workflow.

## Pilot freeze rule

Do not expand this protocol merely because another abstraction seems elegant. Change it only when real execution exposes a contradiction, missing representational capability, repeated operational friction, unsafe ambiguity, or material unnecessary complexity.
