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
- What **end-to-end outcome and acceptance evidence** would make this commitment complete? Identify material missing product decisions without pretending open engineering design choices are blockers. Space reuse/adaptation/formation is assessed **after** the outcome/dependency chain is sketched, not used to dictate the chain.

One Space has one **coherent bounded production responsibility**, not necessarily one task, old workflow stage, Agent or phase. It may contain internal work stages and several agents if outcomes, contracts, context and assurance are genuinely cohesive. A dedicated Space must pay for extra formation/coordination cost through capability fit, trustworthy separation or reuse value.

## 2. Establish end-to-end I/O chain integrity before Space mapping

**Start from the accepted Human/project commitment and work toward the intended verified end condition**, not from a preselected first Space or familiar workflow phases. Build a **provisional outcome dependency graph** sufficient to explain how the commitment could become complete. A logical outcome is not automatically a Space, an Agent, a file, a phase or an invocation.

- **Entry:** name the current-effective source authority and accepted commitment/requirements, including its version or pinned baseline and material preconditions.
- **Outcomes and edges:** identify the necessary produced results and why the next consumer needs them. Model real independent/parallel production, branches and **join points** where several results must be compatible before a downstream outcome is valid.
- **End condition:** identify the actual delivered result, independent/appropriate assurance evidence and owning Human/project acceptance needed to justify completion. The final verified outcome is not automatically a Space.
- **Conditional territory:** mark uncertain downstream choices, dependencies or paths as **conditional/unresolved**, with the evidence or decision needed to firm them up. Make the overall logical path visible without pretending downstream contracts are fixed in advance.
- **No phase pipeline:** do not force Solution → Backend → Frontend → Review → Test or any other universal sequence. Some assignments need one coherent Space, others parallel capabilities, and some stop at a Human decision. Graph shape comes from required results, not tool convenience.

For each **material handoff / graph edge**, assess:

| Concern | Checkable question |
| --- | --- |
| Producer | Which accountable production responsibility can actually supply the needed output? |
| Output and provenance | What exact result/artifact/state/evidence is produced, by which source/version and under what authority? |
| Consumer | Which downstream responsibility consumes it and why? |
| Input conformance | What schema, semantics, invariants, acceptance status, version and permission must hold before the consumer can use it? |
| Failure/gap | If incomplete, stale, incompatible, missing or rejected, who resolves it and where does the chain stop/escalate? |

**Integrity checks:** no required output without an identified producer or justified external source; no consumer whose mandatory input is unexplained; no parallel branch merging without compatible contracts; no required end-condition/acceptance obligation without a path to credible verification evidence. Verification must test against **upstream owning acceptance/requirements directly**, not only against a possibly mistaken solution contract. Balad judges upstream semantic authority and cross-Space handoffs; each invoked Space validates **its own received input conformance**, not the whole upstream project.

Distinguish:
- **Structurally covered (provisional):** all *known necessary* outcomes have a plausible connected dependency/assurance path, and uncertainty is clearly bounded. This is **not** proof that future outputs exist or that every downstream detail is settled.
- **Execution-validated:** actual authorized producers supplied outputs, real consumers accepted compatible versions, and tests/reviews demonstrate the relevant end-condition claims. A diagram, proposal or declared PASS is insufficient.

Keep a compact graph (ASCII, Mermaid or simple dependency table) when it aids technical judgment; do **not** add a mandatory graph store, schema, Space catalog or workflow engine.

### Map graph responsibilities to existing Spaces, then formation candidates

**Only after the outcome graph is understood**, inspect actually accessible, current Space definitions and their authoritative scope, status, I/O contract, capability/knowledge/assurance bounds and runnable evidence. Check the real Harscode research/operational sources and any explicitly configured local Space definition location; a folder name, guide or historical experiment is **not** evidence that a reusable formed Space exists. If no usable existing Space is found, report that rather than inventing reuse.

For each material responsibility, classify **reuse / adapt / form / conditional / unresolved** and explain the fit:
- **Reuse:** actual existing definition with compatible purpose, input/output obligations, status and project-binding requirements; do not equate "exists" with "ready to invoke".
- **Adapt:** an existing capability can be changed within a coherent scope; material contract/authority changes still need approval.
- **Form:** no suitable capability exists; propose a distinct bounded responsibility that justifies formation cost, not a relabelled workflow phase.
- **Conditional/unresolved:** downstream design/authority/evidence is too uncertain to commit; show what determines its eventual mapping.

**Space boundaries need not match graph nodes.** A Space can own multiple tightly coupled results, while one logical outcome may require several Space outputs. Compare minimal compositions based on coherent contracts, safe execution, reuse and assurance independence. Avoid premature proliferation, but never merge responsibilities solely to reduce Space count at the expense of real authority/security/independence boundaries.

After mapping, choose the **nearest justified formation frontier** and detail only what its actual input contract and execution-readiness review require. Leave other mapped Spaces provisional until new evidence warrants formation. Human approves formation separately from invocation, and neither is granted by a clean dependency graph.

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

Report **conclusion and recommended next action first** in direct language. For substantive composition reviews, provide only the structure needed for Human judgment:
- **Authority and end-condition readiness:** source/baseline, accepted outcome, verified versus unknown.
- **Provisional end-to-end outcome graph:** producer-to-consumer edges, actual parallelism/joins, assurance/acceptance path and clearly conditional segments. Do not imply graph nodes are preapproved Spaces.
- **Material chain gaps and capability mapping:** missing/incompatible I/O, acceptance obligations without verification, and real existing-Space evidence versus adapt/form/conditional candidates.
- **First actionable frontier:** smallest justified formation candidate or other next decision, its input/output boundary and Specialist/knowledge/runtime needs; blockers and exact Human approval/write scope.

Use small tables/diagrams when they improve precision, with short reasoning for non-obvious choices. Do not demand a four-part dossier for a simple exchange or claim execution validation from a provisional chain.

Use precise states: **PROPOSED** (analysis only), **FORMED / UNVERIFIED** (definition exists, capability unproven), **READINESS-CHECKED** (state exactly which checks passed), **INVOCATION-AUTHORIZED** (only after valid approval), **OUTPUT VERIFIED** (only from actual execution evidence). These are **communication labels**, not a mandatory workflow engine or file-state schema.

Never claim formation, tool access, permission, independent verification or C1 delivery based only on a plausible design. Stop when the next consequential action requires Human authorization.
