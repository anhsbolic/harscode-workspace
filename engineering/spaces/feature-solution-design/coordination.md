# Rancang — Coordination and Durable Continuity

> **Standing:** Rancang vNext material amendment candidate / NOT YET FORMATION APPROVED. [External contract](contracts.md) governs input/output semantics. This file does not install or invoke Agents.
> **Owner:** Rancang internal accountability. Human directly addresses [Space Coordinator](agents/space-coordinator/agent.md); no external agent, including Balad, has a dispatch channel.

## 1. Human-direct start and resume

A Human can say "mulai ORG-01" or "lanjutin STORY-12" without supplying full internal fields. Coordinator interprets **start** or **resume** intent, resolves the actual project, work identifier, its standing/revision, and durable Rancang assignment record(s) through permitted discovery. It must not guess across branches, projects, duplicate identifiers or similarly named work.

- **Start:** Locate effective accepted bounded objective and project standards; see whether related Rancang assignment already exists. Define a bounded objective/consumer/output contract rather than assuming one upstream outcome equals one Space invocation.
- **Resume:** Locate the matching **specific Rancang assignment**, not just the Product/Story identifier. Open its durable state and exact original source/output/approval revisions. If multiple assignments match, ask Human only for the necessary distinction. If no state exists, say so; do not invent former progress or approval.
- **Discovery versus production:** Permitted read-only discovery is not production, arbitrary external access, autonomous operation or write authority. After discovery, obtain exact Human authorization for material production scope, tools/actions, writing, destinations and consequential gates.

The Coordinator may discuss material decisions with Human **in the same session**. A Human statement changing owning Product, Design or Engineering authority must still be durably approved/persisted by its appropriate owner before that change is consumed as effective authority.

## 2. Coordinator's contract accountability

Coordinator owns assignment resolution, logical input acceptance, applicability/readiness triage, scoped Specialist delegation, Agent returns and revision joins, protected Human decisions, exact-output handoff and minimum durable state. It **does not** own Product/Design policy, substantive X1/O1–O4 edits, Security Findings, independent Solution Review or Human acceptance.

Before consequential production: confirm formed exact definition revision, bounded input standing, required constraints and project refs, intended consumers, actual permitted tools/write surfaces, Human approval, and usable externally provided Harness/runtime evidence. **Rancang does not certify the Harness.** No incomplete initial Human utterance is a reason to refuse permitted discovery.

Each assigned internal responsibility receives only relevant original refs, revisioned input, expected output and owner/destination, permitted actions, evidence requirements and stop criteria. For relevant user-facing work, the Coordinator enables experience inputs to reach material technical selection in time; this is not a required sequential phase or separate handoff. Coordinator reconciles changed dependencies, does not rewrite findings, and may protect unaffected work from local blockers. One concrete accountable producer owns each verification obligation.

### Bounded Engineering–Experience challenge and unresolved decisions

- Architect owns O1/O2 mechanisms; Experience owns O3 and surfaces relevant actor/consumer needs early enough to influence material technical choices. They challenge each other against accepted meaning, effective Design/Engineering standards, technical feasibility, security and total Engineering cost. No mandatory debate, fixed iteration count, consensus vote or UX artifact is required when the solution is straightforward.
- For a consequential disagreement, accountable producers explain the competing approaches, what binding requirements each satisfies, evidence, downside and reversible options. The independent Solution Reviewer evaluates material experience benefit against implementation/operational burden and risks, checks Security Findings, and returns a reasoned recommendation or an evidence/authority gap. The Reviewer does not take ownership of O1/O2/O3 or decide Product/Design policy.
- Within delegated Engineering discretion, the owning producer records a defensible choice and rationale, including material dissent if relevant; Reviewer assesses it. A mere preference disagreement is not an automatic Human gate. If a material decision cannot be justified or exceeds delegated authority, the Coordinator holds only the dependent edge and presents exact alternatives, rationale, reviewer recommendation, remaining dissent, impact and requested Human decision. Persist any authority-changing decision in its owning project artifact before relying on it.

## 3. Six defined roles

These are six **semantic actors**, not a requirement for six native sessions. Actual tools, context separation and identity require Harness evidence.

| Agent | Consumes | Accountable return | Forbidden responsibility |
| --- | --- | --- | --- |
| [Space Coordinator](agents/space-coordinator/agent.md) | Human intent, work/source state, all producer/reviewer returns | Scoped assignments, Human gates, revisioned bundle and acceptance standing | Producer content or independent findings |
| [Requirements Analyst](agents/requirements-analyst/agent.md) | Accepted bounded work input and materially applicable standards | X1 Engineering Obligation Map | Product/Design reconstruction or solution selection |
| [Solution Architect](agents/solution-architect/agent.md) | X1, effective technical baseline, applicable Design/security constraints | O1/O2, designated O4, bounded Engineering Standards proposal/update where authorized | Product/Design policy, feature implementation, independent review |
| [Experience Specialist](agents/experience-specialist/agent.md) | X1, effective Product/Design constraints, current O1/O2 | O3 and designated O4 | Design Standards or UI implementation |
| [Security Analyst](agents/security-analyst/agent.md) | Effective security obligations, exact proposals/standards change | Independent Security Findings and affected re-assessment | Owning/writing the proposals assessed |
| [Solution Reviewer](agents/solution-reviewer/agent.md) | Effective originals, X1/O1–O4, Security Findings, material trade-offs and consumers | Independent overall O5 findings and reasoned trade-off recommendation | Producer edits, overriding Security Findings or Human-owned decisions |

Required independent Security/Solution assessments may be proportional to actual risk, but findings and limits must be truthfully represented. A role name alone does not prove independent execution. Unselected role obligations must either be fulfilled under a justified permitted combination or marked inapplicable/blocked with rationale; never silently vanish.

## 4. Consequential gates, without mandatory approval at every handoff

| Gate | Held work | Human evidence to continue |
| --- | --- | --- |
| **Formation** | No production using materially amended, unapproved Space definition | Explicit Human approval of **exact revised formation** |
| **Invocation** | Consequential production/writes without scoped authorization | Resolved assignment, work/definition refs, scope, tool/actions, destinations and mode |
| **External Product/Design decision** | Any dependent solution that would invent/change external semantics | Relevant owning decision and effective approved source revision; discussion may occur in same session |
| **Engineering Standard evolution** | New or changed standard and dependent binding claims | Reviewed exact proposal, authorized Human decision, permitted write, verified effective project-owned revision |
| **Protected/scope expansion** | Newly privileged/security/protected actions or expanded work | Explicit Human action/path/revision approval and real tool containment |
| **Final bundle acceptance** | Treating Rancang's output as Human-accepted binding handoff | Human acceptance of exact bundle revision; separately authorize downstream implementation/spec adoption |

Default is supervised. Human may steer continue/revise/stop in current scope without converting an ordinary checkpoint into approval. Autonomous execution requires separate explicit Human authorization; no mandatory gate disappears. Standards proposals do not silently become project policy; feature API/spec adoption is separately downstream owned.

## 5. Durable assignment identity and resumption

After each authorized production invocation, preserve minimum reconstructable **target-project-owned** state (one existing document or referenced artifacts is enough):

- Project/repository/ref, distinct **Rancang assignment identity**, upstream work identifiers, exact formed Space definition revision, scoped objective, consumers, authorization and writable destinations.
- Accepted authoritative work input, effective standards and technical evidence refs/revisions; Agent ownership and actual artifact revisions (X1/O1–O5 plus separately owned Security Findings).
- Human decisions, proposed/approved Engineering Standards changes and exact effective revisions; material unresolved alternative/reviewer recommendation and affected edge if any; performed versus NOT RUN evidence; actual review independence/limitations; affected blockers and next safe action.

On resume, re-open state **and real current authority**, compare each material dependency and approval scope; reuse only still-valid outputs/reviews and permitted actions. A change invalidates only affected joins. Chat memory, an earlier assistant answer, or a guessed default branch is not durable project state. If state is missing or unreadable, report the gap and offer a new bounded assignment.

No global scheduler, registry, status engine or cross-Space orchestration is implied. Report production COMPLETE/PARTIAL/BLOCKED/FAILED according to [external contract](contracts.md), distinct from Human acceptance and runtime verification.
