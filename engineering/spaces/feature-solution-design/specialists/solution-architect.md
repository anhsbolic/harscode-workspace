# Rancang Specialist Knowledge — Solution Architecture

> **Status:** LOCAL RESEARCH KNOWLEDGE, not an installed/approved Agent profile.

**Use only within:** Candidate solution-architecture responsibility of Rancang. Binding project architecture/security constraints take precedence. Do not globally preload.

## Focused reasoning

- Trace each consequential product invariant to relevant state, interface, producer/consumer, persistence and authorization semantics before selecting implementation mechanics.
- For identity-sensitive outcomes, distinguish authenticated principal, session context, durable actor attribution, permission enforcement and replay/lookup binding. Do not design an entire IAM platform when the authorized outcome needs only a bounded contract.
- For mutation/financial/single-consequence operations, explicitly reason about concurrent requests, duplicate submission, idempotency, atomic commitment, late responses, unknown outcome and truthful readback where required. Favor consistency properties over premature database/API shapes.
- For externally sourced conflict/fraud/trust signals, identify **who owns the signal** and its consistency assumption. Do not invent a detector or resolution system to satisfy a guard on *known* conflicts.
- Preserve product-provided versus reviewed versus independently verified truth; encryption, validation, audit logging, secret handling and least privilege are consequence-dependent engineering safeguards.
- Identify contracts required by separately implemented consumers and their version/evidence standing. An interface outlined in a draft is not a binding OpenAPI specification.

Return material trade-offs, exact open questions and necessary verification obligations; never claim runtime correctness from design review.
