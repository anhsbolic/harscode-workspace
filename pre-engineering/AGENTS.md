# AGENTS.md — pre-engineering/

Use this area when project-owned Product Truth exists but product behavior is not yet concrete enough for engineering to proceed without inventing meaning.

## Hard rules

- Project product/domain truth remains owned by the target project.
- A target project may explicitly make Human-approved commitment-specific product behavior / requirements binding for downstream work within that bounded commitment without promoting those details into whole-product canonical Product Authority; scope and precedence must be explicit.
- Read current product authority before historical specs, implementation, or code.
- Existing implementation, prototypes, schemas, and historical artifacts are evidence, not automatic Product Authority.
- Work scenario/workflow-first; do not default to persona × feature matrices.
- Distinguish capability / product behavior from feature / surface / implementation.
- Do not solve technical architecture, API, database, component, or implementation design here.
- A ready commitment may progress without resolving unrelated blocked future commitments.
- Default to one active commitment route at a time.
- A minimum prerequisite behavior may travel inside the active commitment only when it is materially required for dependency closure and the combined scope remains meaningful, semantically ready enough, truthful, and bounded.
- Reaching durable pre-engineering handoff does **not** prove that a prerequisite's real product behavior has been implemented / delivered.
- Pre-engineering route completion means the durable handoff is prepared and Human-approved; independent cold-start consumption by a fresh engineering reader is later validation evidence, not another pre-engineering stage.
- Interaction exploration precedes confirmed behavior; confirmed behavior precedes requirements.
- Derive Experience Requirements and Engineering Requirements from the same confirmed behavior.
- Durable correctness must not depend on remembered chat context.
- Human approval is required for substantive product decisions before promoting them to durable state.
- A progress dashboard may visualize state but must not become Product Authority.
- Dashboard readiness / dependency signals must reflect an owning artifact or evidence source; when no owner has established BLOCKED / WAITING / ELIGIBLE / dependency state, use PARKED / UNRESOLVED or omit the stronger claim.

## Routing

- Overall scope / authority / model → `README.md`
- Run one commitment depth-first → `commitment-route.md`
- Start a fresh commitment session → `kickoff-prompt.md`
- Maintain an optional visual progress dashboard → `control-tower.md`
