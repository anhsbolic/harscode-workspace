# S1 Interaction Sequence — Human-Direct Coordinator and Specialist Flow (Proposed)

> **Status:** Logical **harness-neutral** first-use interaction, not a native CLI configuration, executable workflow engine, or evidence of real dispatch.
> **External boundary:** **Human ↔ Space Coordinator Agent**. Balad may give the Human independent advice or review already-produced evidence on request, but has **no operational messages to the Coordinator**. Compare [input–output chain](input-output-chain.md) for static dependencies and [Human Approval Gates](human-approval-gates.md) for binding stop conditions.

## Execution and approval boundaries

```mermaid
sequenceDiagram
    autonumber
    actor H as Human
    participant C as S1 Coordinator Agent
    participant S as Project Sources
    participant RA as Requirements Analyst
    participant SA as Solution Architect
    participant ES as Experience Specialist
    participant RV as Solution Reviewer
    participant A as Project Artifacts

    H->>C: Ask for S1 preflight directly and choose mode if not supervised
    C->>S: Check formed definition, I1-I4 sources and runtime requirements
    C-->>H: Report readiness, proposed scope and Human gates

    alt Formation or required preflight conditions not ready
        C-->>H: BLOCKED or NOT READY, no internal execution
    else Prerequisites checked
        H->>C: Authorize exact I4 invocation and write scope
        C->>A: Record Human approval, pinned inputs and execution mode

        C->>RA: Assign approved I1-I4 to produce X1
        RA->>S: Read original source authority directly
        RA->>A: Persist X1 revision and findings
        RA-->>C: Return X1 ref and unresolved authority issues

        opt Supervised mode, X1 observation milestone
            C-->>H: Show X1 ref, findings and next assignment
            H->>C: Continue, revise or stop within authorized scope
        end

        C->>SA: Assign X1 plus I2/I3 to produce O1 and O2
        SA->>A: Persist O1 and O2 revisions
        SA-->>C: Return architecture contracts and unknowns
        C->>ES: Assign X1, O1/O2 and original design authority
        ES->>S: Read relevant original design source
        ES->>A: Persist O3 experience/state revision
        ES-->>C: Return O3 and any interface mismatch

        opt Material Product Authority or protected action gate
            C-->>H: Hold affected downstream action, present gate evidence and revision
            alt Exact Human authorization is valid
                H->>C: Approve scoped decision or protected action
                C->>A: Record gate ID, approved revision and permitted resume
            else Denied, missing or stale decision
                C-->>H: BLOCKED for affected action, preserve available evidence
                Note over C,RV: Do not execute work depending on unresolved gate
            end
        end

        opt Supervised mode, solution-contract observation milestone
            C-->>H: Show O1/O2/O3 refs, deltas and proposed independent review
            H->>C: Continue, revise or stop within authorized scope
        end

        C->>RV: Assign current X1/O1/O2/O3 plus ORIGINAL I1/I2/I4
        RV->>S: Independently inspect original approved authority
        RV->>A: Check current versioned producer outputs
        RV->>A: Persist O4 obligations and O5 review findings
        RV-->>C: Return review evidence and limitations

        opt Review findings require authorized corrections
            C->>SA: Route affected O1/O2 issue to owning producer if relevant
            C->>ES: Route affected O3 issue to owning producer if relevant
            C->>RA: Route affected X1 issue to owning producer if relevant
            Note over C,RA: Revisions only where affected and authorized
            C->>RV: Request re-review of actually changed artifact edges
            RV-->>C: Return updated O4/O5 refs or unresolved blocker
        end

        C->>A: Assemble actual revision-pinned output and gate evidence
        C-->>H: Deliver result, O1-O5 refs, blockers and verification limits

        alt Human accepts concrete revision for downstream
            H->>C: Record final acceptance for exact output revision
        else Human defers or requests changes
            H->>C: Record nonacceptance and authorized next action if any
        end
    end
```

## Interpretation

- **Formed Space + direct invocation first.** A file/profile does not instantiate an Agent. The Human initiates the Coordinator only after separate formation, actual runtime readiness and concrete scope authorization. Default mode is `supervised`. `autonomous` is valid only when explicitly selected by Human; the Coordinator cannot promote itself.
- **Supervision is not authorization.** In supervised mode, milestone `continue` steers ordinary work but **does not approve Product Authority, protected changes or final downstream acceptance**. The optional supervision pauses may be configured proportionately for the actual pilot.
- **Approval gates always apply.** In either mode, G1/G2 material decisions or protected actions pause the **affected dependent work** until exact Human authorization; other independent authorized work may continue. The diagram's following lines never override a BLOCKED gate.
- **No fixed Agent topology.** Runtime may use isolated subagents or explicit sessions after verification. These depicted messages express responsibility, not proof of native orchestration or automatic secure pause/resume. Reviewer must receive original authority independently and cannot revise producer output.
- **Real outputs and Human acceptance:** retain actual producer revisions, review findings, gate decisions and limitations. The final acceptance applies to an exact bundle revision; the Coordinator cannot self-approve. No Balad-to-Coordinator operational channel exists.
