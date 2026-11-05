# Engineering Solution Architect — Technical Mechanism Knowledge

> **Type:** Architect-owned non-binding technical knowledge. This is **not** a cross-project technology policy, a substitute for Project Engineering Standards, UX expertise or independent Security assessment. [Agent](agent.md).

## Choose mechanism from constraints

Read actual code/ADRs/stack, accepted Product invariants, material UX needs, security controls and NFR. Compare local design vs modular boundaries vs distributed services only when actual scale, independent lifecycle, reliability or security needs justify complexity. For transactional invariants first identify what must be atomic; evaluate available project transaction, concurrency, idempotency/retry or compensation mechanisms without inventing distributed coordination.

## Consumer-critical technical completeness

Two independent implementers should not invent different operations, request/response requiredness, permissions, persistence constraints, error/unknown semantics or adoption boundaries from O01–O07. Use the effective project API/schema format; if shared typed consumers require it, deliver **complete proposed wire contract** plus normative guarantees and O07 cases. Mark adoption/owner and compatibility of existing canonical sources separately.

## Security and Experience challenge

Tech feasibility can identify risky UX assumptions but not authorize changing accepted webpage routes, interaction meaning or security floor. Independent UX Specialist grounds experience in Design originals; Security Analyst grounds threats and required safeguards in security originals. Architect authors concrete controls, chooses feasible safe approaches and precisely reports unresolved owners. Reviewer findings require correction or accountable nonblocking disposition, never a producer-written PASS.

## Quality floor

Address actual NFR and reliability under realistic constraints; trace key assertions to inspected source or explicitly provisional evidence. Prefer fit/sufficient and reversible experiments under uncertainty; preserve fallback and high-impact containment. Architecture diagrams are useful only when actual consumers benefit, not a fixed document requirement.
