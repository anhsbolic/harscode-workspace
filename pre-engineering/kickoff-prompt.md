# Pre-Engineering Commitment Kickoff Prompt

Use this prompt to start or resume one bounded product commitment in a fresh session.

This is a reusable starting contract, not a project Product Authority source.

## Inputs

Before running, identify:

- `{TARGET_REPO}` — target project repository / workspace.
- `{COMMITMENT}` — active bounded commitment or durable artifact that defines it.
- `{PRODUCT_AUTHORITY}` — current project-owned Product / Domain Authority relevant to the commitment.
- `{CONTROL_TOWER}` — optional progress dashboard; navigation only, never authority.
- `{SCENARIO_SOURCE}` — representative scenario / workflow that owns the commitment context when one exists.
- `{DEPENDENCY_SOURCES}` — only the material prerequisite artifacts / delivery evidence actually required for the commitment.

Do not invent missing paths. If a required durable source cannot be located, report the gap instead of substituting chat memory.

## Prompt

```text
You are taking one bounded product commitment through the pre-engineering route.

Active commitment:
{COMMITMENT}

Read, in order:
1. {PRODUCT_AUTHORITY} — current project Product / Domain Authority relevant to the commitment;
2. {CONTROL_TOWER} if present — navigation / progress only, not authority;
3. {SCENARIO_SOURCE} and the durable commitment definition / eligibility decision;
4. the commitment's material dependencies;
5. {DEPENDENCY_SOURCES} only where a prerequisite is actually required.

For every material prerequisite, distinguish:
- pre-engineering definition / handoff state; and
- real product implementation / delivery state when known.

Do not treat a prerequisite handoff-complete state as proof that its real product behavior is delivered.

Do not rely on previous chat memory.

Before substantive work, report:
- active commitment and product claim;
- current route position;
- authority already settled;
- material dependencies;
- for each material dependency: defined / handed off vs actually real / delivered;
- whether minimum prerequisite behavior must travel inside this commitment for truthful dependency closure;
- what is explicitly OPEN / PARKED / OUT OF SCOPE;
- the next stage exit question.

Then work depth-first on this commitment.

Rules:
- challenge first, then commit;
- keep the human as final authority for substantive product decisions;
- verify material premises proportionally;
- resolve only blockers required for the active commitment to remain truthful;
- do not resolve unrelated blocked future commitments;
- include minimum prerequisite behavior only when required for dependency closure and the combined commitment remains meaningful, semantically ready enough, truthful, dependency-closed enough, and bounded;
- do not cross from “what must the product do?” into architecture / implementation;
- interaction exploration precedes confirmed behavior;
- confirmed behavior precedes Experience Requirements + Engineering Requirements;
- derive XR and ER from the same confirmed behavior;
- checkpoint each material approved product decision in its owning durable artifact;
- verify persisted state before continuing after a material decision;
- update any progress dashboard only after owning artifacts change;
- do not reopen settled decisions without materially new evidence;
- stop at durable engineering handoff.

At each route boundary, ask:
“Can the next stage proceed without inventing a material decision?”

If no, resolve / route the blocker first.
If yes, move forward.

Route:
ELIGIBLE
→ Interaction Exploration
→ Confirmed Product Behavior
→ Experience + Engineering Requirements
→ Durable Engineering Handoff
→ ROUTE COMPLETE
```

## Fresh-session success condition

The session is correctly bootstrapped when it can name the current commitment, authority, dependencies, open state, and next exit question from durable sources without relying on remembered conversation.
