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

Each assigned internal responsibility receives only relevant original refs, revisioned input, expected output and owner/destination, permitted actions, evidence requirements and stop criteria. Coordinator reconciles changed dependencies, does not rewrite findings, and may protect unaffected work from local blockers. One concrete accountable producer owns each verification obligation.

## 3. Six defined roles

These are six **semantic actors**, not a requirement for six native sessions. Actual tools, context separation and identity require Harness evidence.

| Agent | Consumes | Accountable return | Forbidden responsibility |
| --- | --- | --- | --- |
| [Space Coordinator](agents/space-coordinator/agent.md) | Human intent, work/source state, all producer/reviewer returns | Scoped assignments, Human gates, revisioned bundle and acceptance standing | Producer content or independent findings |
| [Requirements Analyst](agents/requirements-analyst/agent.md) | Accepted bounded work input and materially applicable standards | X1 Engineering Obligation Map | Product/Design reconstruction or solution selection |
| [Solution Architect](agents/solution-architect/agent.md) | X1, effective technical baseline, applicable Design/security constraints | O1/O2, designated O4, bounded Engineering Standards proposal/update where authorized | Product/Design policy, feature implementation, independent review |
| [Experience Specialist](agents/experience-specialist/agent.md) | X1, effective Product/Design constraints, current O1/O2 | O3 and designated O4 | Design Standards or UI implementation |
| [Security Specialist](agents/security-specialist/agent.md) | Effective security obligations, exact proposals/standards change | Independent Security Findings and affected re-assessment | Owning/writing the proposals assessed |
| [Solution Reviewer](agents/solution-reviewer/agent.md) | Effective originals, X1/O1–O4, Security Findings and consumers | Independent overall O5 review findings | Producer edits, overriding Security Findings |

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
- Human decisions, proposed/approved Engineering Standards changes and exact effective revisions; performed versus NOT RUN evidence; actual review independence/limitations; affected blockers and next safe action.

On resume, re-open state **and real current authority**, compare each material dependency and approval scope; reuse only still-valid outputs/reviews and permitted actions. A change invalidates only affected joins. Chat memory, an earlier assistant answer, or a guessed default branch is not durable project state. If state is missing or unreadable, report the gap and offer a new bounded assignment.

No global scheduler, registry, status engine or cross-Space orchestration is implied. Report production COMPLETE/PARTIAL/BLOCKED/FAILED according to [external contract](contracts.md), distinct from Human acceptance and runtime verification.
