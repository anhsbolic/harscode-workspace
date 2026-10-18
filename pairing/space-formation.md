# Space Formation and Readiness — Balad Research Guidance v0

> **Status:** Experimental, for Station 5 on `research/harscode-purpose-llm-fit`; not `main` policy, a validated schema, a Space instance or authorization to execute.
> **Owner:** Human + Balad for formation reasoning and approval routing. Actual production belongs to an authorized Space.
> **Foundational authority:** [Station 4 closeout](../research/checkpoints/station4-closeout-space-only-2026-10-18.md); start with [Balad entrypoint](AGENTS.md).
> **Intent:** A fresh Balad session should be able to propose a reusable bounded Space from varied task/project sources without a long Human prompt or hidden conversational history.

## 1. Determine the needed capability, not a phase label

Input can be an approved product commitment, PRD, TRD, task/issue, research question, incident or partial brief. Recover the **actual Human goal**, owning source/version, acceptance obligations, material constraints and permission boundaries. Multiple documents may describe one obligation; choose the current owning truth and avoid assembling a new parallel product spec.

Assess:
- Is substantive **product meaning** missing, contradicted or genuinely unaccepted? If yes, identify exact evidence and owner; the route may be Human decision or a proposed bounded product-oriented Space for analysis, without granting it product approval authority.
- Are architecture, API, database, identity-provider, user-flow or implementation details merely **engineering/design freedom intentionally left open**? If so, do not claim product immaturity. A solution-forming responsibility may be justified if Builder cannot safely take the available inputs without material engineering decisions.
- Does an existing Space match the desired production outcome and contract? Prefer **reuse**, then **adapt**, then **form** a new Space only when the necessary capability is actually missing.

One Space has one **coherent bounded production responsibility**, not necessarily one task, old workflow stage, Agent or phase. It may contain internal work stages and several agents if outcomes, contracts, context and assurance are genuinely cohesive. A dedicated Space must pay for extra formation/coordination cost through capability fit, trustworthy separation or reuse value.

## 2. Compose a justifiable input → output chain

For the current commitment, describe the **first decision/action-ready production outcome** and what must exist before it. Where warranted, map the next plausible outcome(s) as dependencies. Do not hardcode a global Product → Solution → Build → Review → Test pipeline.

At every proposed Space boundary, identify:
- **Input**: named/artifact reference(s), owning source/version or acceptance provenance, necessary content/state, authorization, schema/semantic conditions and a **checkable conformance rule**. Conformant does not mean semantically correct upstream; Balad owns that judgment.
- **Responsibility**: what this Space produces, what decisions are delegated internally, and what cannot be decided.
- **Output**: concrete deliverables, invariants/acceptance evidence, tested/untested claims, limitations and next-space-compatible handoff.
- **Handoff**: who assesses acceptance, what requires Human judgment, and whether a downstream Space can consume the result without inventing material decisions.

A missing input/uncertain downstream branch should be recorded as **conditional**, not padded with speculative Spaces. For C1, approved Stage 5/6 product meaning must be respected; cold-start sufficiency should be inspected, not assumed perfect or automatically reopened.

## 3. Required logical content of a formed Space

Before any claim of **formation complete**, a reusable Space definition must make the following independently inspectable (Markdown with addressable headings is enough for the pilot; exact file layout/schema is not yet approved):

1. **Identity and status:** distinct name, purpose, owning definition/version, research/candidate/ready state, and scope of reuse vs target-project binding. No unvalidated claim of operational maturity.
2. **Production contract:** single coherent outcome, inclusion/exclusion boundaries, acceptable input conditions (including provenance), output artifacts, evidence threshold, failure/partial/unknown result semantics, and explicit stop/escalation cases.
3. **Composition:** justified Specialist Agent capabilities/roles and interaction/transfer of work **inside** the Space. Include true independence for claims requiring it; don't use role labels as evidence.
4. **Agent formation binding:** for each Agent, defined specialization, internal assignment/output, capability limits, appropriate model/tool requirements, applicable targeted knowledge and actual permission/guardrail boundaries. An Agent Profile is declarative; it is not a tested executable Agent.
5. **Harness and knowledge:** resolvable paths and versions for stable/research guidance, references, project constraints, Codex/other harness instructions or Skills/MCP tools where actually available. Bind minimal triggered knowledge; avoid copying a whole Library into each Agent. Do not claim experimental drafts are canonical.
6. **Execution and authority:** project binding mechanism, authorized worktrees/paths/actions, sandbox/network credentials/approvals, how scoped invocation receives its assignment, and how the Space prevents crossing its authority. A mere instruction to obey permissions is not proof of enforced access control.
7. **State and handoff:** distinguish immutable/reusable definition from concrete invocation/active working state and from project-owned durable artifacts. Specify how to recover latest **valid** working state and return output/evidence without relying on old chat. This is a logical ownership requirement; `harscode-state` remains a candidate physical home, not a proven implementation.
8. **Assurance and readiness:** required test/review independence, tools/evidence, conformance checks, known gaps and who can authorize first invocation. Security-sensitive verification and project gates are never self-waived.

Do **not** turn these content obligations into eight mandatory files, a universal registry, a state machine, runtime engine, or a fixed number of Agents. A small one-Agent Space can document them proportionally, including explicit non-applicability.

## 4. Formation versus execution authority

**Assessment:** Balad may inspect trusted sources and propose formation **read-only**. This is the default for short Human requests to "check readiness".

**Formation:** only after scoped Human permission, Balad may author declarative Space/Agent definitions and configuration proposals, bind reusable knowledge and perform non-production checks of references/structure/capabilities. Confirm target **research** branch, writable paths and protected rules. Persist approved formation outcomes in Harscode's research-owned reusable definition area; do not choose a permanent directory layout or create an operational state store merely because a future design might need one.

**Invocation:** actual work requires a selected formed Space with accepted input contract, actual tools/capabilities, correct project branch/state and valid permission. The first C1 invocation is **separately authorized**. Balad never dispatches a Specific Agent directly for task-related engineering production and never represents a readiness inspection as real production evidence.

**Bootstrap containment:** no first-space paradox: Balad may configure *declarative capability definitions* by explicitly authorized formation work, but code changes to Kencleng or substantive Space tooling implementation are not hidden inside that permission. If genuine implementation is needed to make the first Space operable, surface the exact gap and obtain a separate approved execution route; don't silently broaden Balad into a Builder.

**Product extension:** product-oriented Spaces may be proposed for real product bottlenecks; doing product work within such a Space is still a Station 5 experimental extension requiring Human approval of scope/authority. Product Space output is candidate evidence/decisions, not a canonical project approval.

## 5. Knowledge gaps and harness readiness

Classify missing knowledge into: **(a) adequate existing guidance**, **(b) source-supported scoped reference sufficient for limited work**, **(c) draft/new guidance proposed**, and **(d) critical unresolved safeguard/capability blocking affected execution**. Only (d) must block affected readiness. Balad may request a new Best Practice or related guideline with trigger, owner, sources and verification criteria; scoped approved research use does not promote it to operational `main`.

Verify **actual** harness mechanics at formation: whether the relevant repository instructions load; reference paths exist; Skills/MCP/CLI/browser tools are accessible; sandbox privileges are appropriate; independent Agent execution and review can really be separated; and constraints are not just decorative prose. If untested, say *configured but unverified*. If missing, escalate or reduce scope honestly.

## 6. Report format and completion claims

Report only the granularity needed for Human judgment:
- **Verified input/readiness** — accepted authority, material gaps versus open engineering choices.
- **Composition reasoning** — minimum justified Space responsibilities and immediate/conditional I/O dependencies; consider reuse/adaptation before creating.
- **First formation candidate** — rationale, Agent capabilities, knowledge/tool needs, independent assurance and contract outline.
- **Blockers / permission request** — exact gap and what Human decision/write scope is needed.

Use precise states: **PROPOSED** (analysis only), **FORMED / UNVERIFIED** (definition exists, capability unproven), **READINESS-CHECKED** (state exactly which checks passed), **INVOCATION-AUTHORIZED** (only after valid approval), **OUTPUT VERIFIED** (only from actual execution evidence). These are **communication labels**, not a mandatory workflow engine or file-state schema.

Never claim formation, tool access, permission, independent verification or C1 delivery based only on a plausible design. Stop when the next consequential action requires Human authorization.
