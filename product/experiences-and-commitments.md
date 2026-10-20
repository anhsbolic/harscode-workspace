# Product Experiences and Commitments

> **Status:** WORKING / RESEARCH-ONLY. Product-semantic guidance; not a fixed stage model.
> **Sources of authority:** Approved target-project artifacts, not this file.

## Core principle

Start with **the actor's meaningful experience**, not a screen, technical capability, agent assignment or requirements spreadsheet. A coherent product outcome should be explainable in plain language:

> In this situation, a person wants to accomplish something. They can take these consequential actions with enough understanding. If it works, this real product state or capability becomes true and inspectable. If it does not, the product does not imply a false success.

A good narrative must remain traceable to evidence or approved product decisions. Do not turn a plausible story into unearned project truth.

## 1. Discover representative experiences (before commitment selection)

Understand the product **whole enough** to identify important actor situations and relationships. For each representative scenario, ask:

- Who acts and why? Who is affected, relies on the result, or must independently decide?
- What is the starting situation, including assumptions, constraints and relevant current state?
- What can the actor know, see, do and validly conclude?
- What real consequence changes the product state? What makes the result useful?
- Which other actors, real capabilities, provenance or eligibility conditions must exist?
- What does interruption, failure, conflict, uncertainty or non-participation mean?
- Which findings are observed, hypothesized, approved, or still unknown?

Use representative scenarios to discover outcome candidates, missing authority and dependencies. Do not require one scenario per persona, a persona-by-feature matrix, a complete journey map or every exception flow for the whole product.

## 2. Select meaningful product commitments

A **product commitment** is a Human-selected bounded claim about a meaningful actor/product outcome. It is not inherently an Epic, Story, UI screen, Engineering Space, implementation assignment or release.

Challenge each candidate on five qualities:

| Quality | Test |
| --- | --- |
| **Meaningful** | Does a real actor gain a worthwhile outcome, rather than only an internal prerequisite or administrative deliverable? |
| **Semantically sufficient** | Are consequential actors, authority, success, failure and truth meaning understood enough to explore the experience without downstream guesswork? |
| **Dependency-closed enough** | Are the real prerequisite behaviors already available, included within a still-bounded outcome, or explicitly shown not required? |
| **Truthful** | Could its claimed result be demonstrated without mistaking mock/seeded state, handoff completion, review, or unrelated status for real product delivery? |
| **Bounded** | Can the product outcome be explored and specified coherently without absorbing unrelated product domains? State uncertainty instead of asserting size from intuition. |

A candidate may be **eligible for product clarification** without being implementation-ready. Selecting it does not mean one downstream Space can or should own all associated solution decisions.

When a prerequisite is absent, **wait** for real behavior, or **include** only the minimum prerequisite that supports the same meaningful outcome and remains bounded. If neither works, record the dependency blocker. A prepared specification, approved handoff or fixture does not make an absent product capability real. Product dependencies form a **partial order**, not an automatic total roadmap.

If the actor outcome cannot be split without creating misleading intermediate success, **keep it coherent**. Complex technical dependencies are a reason to examine downstream assignment boundaries, not to manufacture new independently delivered products.

## 3. Clarify the selected commitment's experience

Follow the actor's experience from trigger to consequence and durable result. Capture only material scenes:

| Question | Required reasoning |
| --- | --- |
| **Entry** | What can the person start with or without? What is known, assumed or claimed? |
| **Before consequence** | What must they understand before an authority-bearing, irreversible or material effect? |
| **Action and responsibility** | What can the person do? What must the product attribute or authorize? |
| **Successful outcome** | Which product facts become true together, and what can the actor inspect later? |
| **Negative paths** | How does incomplete, failure, conflict, uncertainty or lost response differ from success? |
| **Truth and provenance** | Which actor-provided assertions, reviews or independent facts must stay distinct? |
| **Out of scope** | Which tempting adjacent outcomes, account/permission details, recovery mechanisms, reviews or downstream capabilities are not promised? |

Do not assume a linear UI flow. The sequence above represents **semantic dependencies**; authentication timing, exact screens, API shape and persistence mechanism are not specified by the narrative.

A product may leave recovery optional but still require truthful handling of an incomplete result. A known conflicting signal may require a safeguard without creating a new conflict detection or adjudication system. Where the source of a required external signal is unknown, preserve the guard's binding meaning and expose the source/readiness gap rather than fabricating a provider.

## 4. Confirm behavior and acceptance

Test narrative scenes for contradictions, accidental new product commitments, and mechanisms masquerading as business rules.

- **Confirmed behavior:** What must actually happen at the product-semantic level?
- **Invariants:** What cannot become false across successful, failed or partial outcomes?
- **Experience obligations:** What must be possible, understandable, visible, distinguishable or inspectable?
- **System obligations:** What must the delivered product preserve for those experience claims to remain true?
- **Acceptance evidence:** What observable results or negative-path checks would demonstrate truthful behavior?
- **Freedom and gaps:** What remains a Design or Engineering choice, and which Human-owned product decisions are genuinely unresolved?

Express these obligations in whatever project-owned artifacts suit the real complexity. Experience Requirements and Engineering Requirements may be useful separate views **derived from the same confirmed behavior**; do not make exact labels, a mandatory stage count, or a separate file per view universal policy. Preserve source anchors, approvals and invariants whenever the views are separated.

Requirement completeness by count is not proof of product coherence or implementation correctness.

## 5. Cross-boundary discipline

- **Product commitment boundary** is defined by meaningful, truthful actor outcome.
- **Design boundary** concerns interaction and expression while honoring product semantics.
- **Engineering assignment boundary** concerns coupled solution decisions, runnable work, contracts and verification responsibility.
- **Delivered reality** requires actual product behavior and evidence, not only a spec, prototype, accepted solution design or completed engineering task.

No one-to-one mapping between commitments, design assignments, Specialist Agents or Spaces is presumed. Keep an integration/consumer path for every material constraint, but do not introduce a Delivery Units taxonomy before it is justified.

## Progress and reopening

Use the owning project's decision vocabulary and existing governance. Distinguish **observed**, **hypothesized**, **working**, **Human-approved scoped**, **blocked**, **parked** and **delivered** when consequential. Do not add a status registry merely to encode these distinctions.

At each material handoff ask: **Can the next owner proceed without inventing product truth?** If not, return the specific question to its owner. Reopen an approved meaning only on materially new evidence; approval of upstream behavior does not imply downstream environment readiness.
