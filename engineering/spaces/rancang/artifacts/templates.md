# Rancang — Optional Eight-Output Content Prompts

> **Standing:** Short, non-binding **content sufficiency prompts**, not the detailed output template. For comprehensive authoring use [Bahasa Indonesia](../templates/rancang-output.id.md) or [English](../templates/rancang-output.en.md). The [Rancang contract](../contracts.md) governs semantics and effective target-project standards take precedence. Neither the prompts nor the comprehensive templates require eight files.

| Output | Questions the intended implementer should be able to answer |
| --- | --- |
| **O01 Blueprint** | Which components, data flows, integration boundaries and technical constraints? Why feasible and proportionate? |
| **O02 AuthN/AuthZ** | Who is principal/actor, who grants or revokes rights, which trusted layer enforces resource permission, and what happens on denied/expired/replayed requests? |
| **O03 API Contract** | What operation/event, input/output requiredness, versions, success/error/unknown semantics and authorization apply? Does a real consumer require a complete typed project-format proposal? |
| **O04 Data/DB** | Which entities/relationships, constraints, ownership, atomicity, persistence and migration/compatibility consequences are material? What is genuinely N/A? |
| **O05 State/Error** | Who owns each authoritative state, how do retries/concurrency/unknown outcomes behave and how do consumers recover truthfully? |
| **O06 Security Design** | Which binding threat/trust/data controls are **authored by Architect**, at which enforcement point, and what independent Security findings remain open? |
| **O07 Verification Specification** | What observable positive/negative/security/recovery falsifies the design guarantee, who will verify and what has actually been run? |
| **O08 Handoff** | Which exact sources and revisions, accepted/proposed standings, owning UX/Security/Solution reviews, consumer compatibility, Human decisions and next authorized action? |

Optional source-to-obligation trace and diagrams are *supporting working evidence* when useful; they are not a ninth required output. Auth/financial/security/runtime details must be grounded in actual accepted project originals rather than examples.
