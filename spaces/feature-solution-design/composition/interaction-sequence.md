# S1 Interaction Sequence — Logical Invocation, Handoffs and Review (Proposed)

> **Purpose:** Show **who acts when**, what each actor consumes/produces, material branches, review feedback and external Human decisions during a bounded invocation. This is an **illustrative logical sequence**, not a universal workflow engine, fixed session count, automatic authorization or proof that a particular runtime can dispatch these roles.
> **Companion:** [Input–output chain](input-output-chain.md) is the static producer–consumer and artifact map. [Space](../SPACE.md), [input](../contracts/input.md), and [output](../contracts/output.md) contracts own the normative semantics.

## Actors, messages and artifact checkpoints

```mermaid
sequenceDiagram
    autonumber
    actor H as Human
    participant P as Pairing
    participant C as Space Coordinator
    participant S as Project Sources
    participant RA as Requirements Analyst
    participant SA as Solution Architect
    participant ES as Experience Specialist
    participant RV as Solution Reviewer
    participant A as Project Artifacts

    H->>P: Request preparation for an approved project commitment
    P->>S: Locate current I1/I2/I3 and consumer expectations
    P-->>H: Present proposed I4 scope, readiness and approval gates

    alt Missing inputs, runtime capability or necessary authority
        P-->>H: BLOCKED / NOT READY; no invocation
    else Preflight sufficient for an explicit decision
        H->>P: Authorize concrete I4 invocation and write scope
        P->>C: Bind pinned I1-I4 and approved output destinations
        C->>S: Verify input revisions, access and conformance

        alt Material input or authorization mismatch
            C-->>P: BLOCKED with source and owner of gap
            P-->>H: Request resolution; do not produce solution
        else Inputs conform and work is authorized
            C->>RA: Assign I1-I4 and X1 destination
            RA->>S: Read original approved behavior and constraints
            RA->>A: Persist X1 source and obligation map
            RA-->>C: Return X1 revision and any open authority gaps

            C->>SA: Assign X1 and applicable I2/I3
            SA->>S: Inspect current architecture and source anchors
            SA->>A: Persist O1 shared decisions and O2 interface contracts
            SA-->>C: Return O1/O2 revisions and unresolved decisions

            C->>ES: Assign X1, O1/O2 and applicable design sources
            ES->>S: Read original behavior and UI/UX authority
            ES->>A: Persist O3 experience and state contracts
            ES-->>C: Return O3 revision and contract mismatches

            opt Material experience/interface mismatch
                C->>SA: Route exact O1/O2 issue to its owning producer
                SA->>A: Update affected O1/O2 within approved scope
                C->>ES: Reconcile O3 against current O1/O2
                ES->>A: Update affected O3 revision
            end

            C->>RV: Assign current X1/O1/O2/O3 and original I1/I2/I4
            RV->>S: Read original approved authority DIRECTLY
            RV->>A: Inspect versioned producer outputs
            RV->>A: Persist O4 obligations and O5 review findings
            RV-->>C: Return revision-scoped conformance result

            opt Reviewer finds material defects
                alt Human-owned decision or permission required
                    C-->>P: BLOCKED or PARTIAL; exact unresolved decision
                    P-->>H: Request decision before affected production
                else Scoped producer correction is allowed
                    opt X1 source map is affected
                        C->>RA: Return source/trace finding
                        RA->>A: Persist corrected X1 revision
                    end
                    opt O1 or O2 contract is affected
                        C->>SA: Return exact solution finding
                        SA->>A: Persist corrected O1/O2 revision
                    end
                    opt O3 experience contract is affected
                        C->>ES: Return exact experience finding
                        ES->>A: Persist corrected O3 revision
                    end
                    C->>RV: Re-review affected edges and current versions
                    RV->>S: Recheck affected original source anchors
                    RV->>A: Persist updated O4/O5 review evidence
                    RV-->>C: Return revised verdict or remaining blockers
                end
            end

            C->>A: Assemble actual revision-pinned O1-O5 bundle
            C-->>P: Handoff result, artifact refs and limits
            P-->>H: Present bundle; request separate output acceptance

            alt Human accepts concrete output for downstream
                H->>P: Record acceptance of exact output revision
                P-->>H: Coordinate future consumer compatibility
            else Human requests changes or has not decided
                H-->>P: Keep delivery unaccepted; route next action
            end
        end
    end
```

## How to read this sequence

1. **Human gates are separate.** An approved Space **formation** is a prerequisite outside the diagram. The initial invocation approval shown above is separate from the later Human decision to accept a concrete produced solution for downstream use.
2. **Pairing versus Space.** Pairing coordinates upstream authority and external compatibility. The authorized Space checks received input conformance, performs bounded work and returns truthful output. Neither role can create product authority from a summary.
3. **Urutan logis, bukan scheduling kaku.** The depicted producer checkpoints expose key dependencies; Architect and Experience Specialist may collaborate or overlap when a concrete assignment allows it. No mandated native Agent count, fixed session transitions, or runtime dispatcher is defined.
4. **Independent review.** Reviewer must independently read I1/I2 originals and the current X1/O1/O2/O3 revisions. Reviewer owns O4/O5, not producer output corrections. Independence requires runtime/context evidence, not different role labels alone.
5. **Bounded feedback.** Each finding returns only to its owning producer and triggers review of affected revisions. Human-owned decisions and material security approvals cannot be replaced with automatic retry or indefinite correction loops. A remaining gap yields PARTIAL/BLOCKED rather than fictitious COMPLETE.
6. **Real artifact ownership.** `Project Sources` and `Project Artifacts` are logical representations of target-project authoritative sources and approved artifact locations; the diagram does not allocate a new storage engine or directory. Persist actual refs/versions according to [state](../invocation/state-and-handoff.md).
7. **Outcome honesty.** `COMPLETE` describes S1 design-delivery conformance, not feature implementation, runtime integration, Human acceptance, or downstream compatibility proof. Other truthful states and evidence limits remain valid.

Use [execution requirements](execution-requirements.md), [responsibilities](responsibilities.md) and [kickoff](../invocation/kickoff-prompt.md) when moving from the diagram to an actually authorized assignment.
