# Workflow-v2 Validation #1 Retrospective

> Validation run: Kencleng Frontend Experience Foundation
> Date: 2026-09-15
> Harscode execution baseline: `workflow-v2@fce5721d996b013c7c9357745978cd9511592a78`
> Harscode evidence head before this retrospective: `07a51a93100afeb4e78b5124d64decae62679f6f`
> Kencleng baseline: `4ef5a50caa89e58e2cc2a5feea3e693a17bf8c3f`
> Kencleng validation result: `validation-01-frontend-experience-foundation@341767481d3f49b4822ca9be7c5d5c176f7d1d58`
> Human owner: Anhar
> Purpose: preserve validation evidence before changing workflow-v2 guidance

## Outcome

Validation #1 preserved correctness well enough to justify continuing the workflow-v2 experiment. Exploration, Techplan, Build, independent Code Review, patch re-entry, and independent Testing all completed through durable artifacts without requiring hidden chat state to reconstruct the work.

The run also exposed operator friction and verification repetition that should be refined before the next validation checkpoint. The evidence supports targeted changes; it does not support redesigning the lifecycle.

## What worked

### Progressive context and durable handoff

The workflow successfully transferred durable decisions rather than raw chat history. Fresh Code Review and Testing sessions were able to operate from the Techplan, current diff/build evidence, and exact pointers.

The `## Phase handoff` pattern was especially useful. It made phase completion visible and supplied artifact/context pointers for the next actor.

### Optional Techplan mechanisms stayed optional

The task did not justify independent Techplan review under the current Complex gate, and decomposition did not create a useful execution boundary. This supports keeping both mechanisms conditional rather than ritualizing them.

### Independent verification found real defects

Code Review found a required browser regression that was not reliably executable at the representative viewport scope. Build/Patch traced the failure to browser-context/service-worker behavior and stabilized the test harness without broadening production scope.

Testing then found a separate missing observable branch: the Techplan-required background-revalidation/stale notice had implementation behavior but no test coverage. Testing returned a narrow patch plan to Build; Build added the missing coverage; Testing independently verified the patch and passed with flagged external follow-ups.

These findings show that independent Review and Testing still buy correctness signal even when Build already runs focused verification.

## Benchmark evidence

The Kencleng run recorded the following non-cached token totals by Codex session grouping:

| Session grouping | Total | Input | Output | Cached input |
|---|---:|---:|---:|---:|
| Exploration + Techplan + decomposition gate | 77,114 | 64,205 | 12,909 | 1,767,424 |
| Build + patches | 96,416 | 82,665 | 13,751 | 1,821,952 |
| Code Review rounds | 195,992 | 175,470 | 20,522 | 4,372,864 |
| Testing rounds | 221,317 | 195,071 | 26,246 | 6,071,552 |

Review + Testing therefore consumed most of the recorded non-cached usage. That is not automatically waste: both phases found defects the previous phase had not closed. However, the run also repeatedly executed overlapping Vitest/Playwright/full verification, including after narrow patches whose affected scope did not justify replaying every broad check.

Benchmark limitations:

- there is no clean pre-Exploration usage snapshot;
- the first Codex session combines Exploration, Techplan synthesis, and the decomposition gate, so those phases cannot be separated precisely;
- cached input is recorded separately and must not be treated as economically identical to uncached input;
- allowance deltas are only clean when no other Codex work consumes the same pool.

The run is therefore useful for directional phase-cost evidence, not a rigorous token-for-token comparison against workflow-v1/main.

## Friction and lessons

### 1. Workflow artifact provenance is under-specified

Durable artifacts did not consistently record who/what authored them, when, model/reasoning/session identity when agent-authored, or the target/workflow revision against which they were produced. Git history helps but does not fully reconstruct harness execution provenance.

Lesson: workflow-generated artifacts need a compact provenance header. Git remains the primary version history; do not invent manual semantic versions unless an artifact contract already needs one.

### 2. Phase handoff semantics are good but operator-facing wording is too mechanical

`Session recommendation: CONTINUE | FRESH` works as a routing enum but leaves the human to translate it into an actual action. Review-to-Patch also left uncertainty about whether to return to an existing Build session or create a fresh one.

Lesson: preserve the semantics but render them as a human-readable session transition with a reason, for example `Continue Techplan synthesis in this session because ...`, `Start a fresh Code Review session because independence matters`, or `Return to the existing Build session because the patch is narrow and context remains focused`.

The handoff should also distinguish `Human decision` from `Open / deferred`; a material decision can survive in durable artifacts without being surfaced strongly enough to the operator at the moment it matters.

### 3. Plan enough to make Build safe; do not optimize for exhaustive pre-execution certainty

The human owner explicitly prefers fail-fast execution over long plan/review iteration. The run supports that preference: many implementation/testing mechanics were cheaper to learn from live execution than to over-speculate during planning.

Material product/domain semantics, authority/security, architecture/ownership, interface/data contracts, irreversible operations, and verification strategy must still be resolved before Build. Local implementation shape, test mechanics, naming, and cheap-to-discover details need not be pre-solved when Build can derive them safely from current code.

### 4. Techplan synthesis should make early routing recommendations

Independent Techplan review and decomposition are optional, but today the human may need to invoke their prompts merely to learn that they should be skipped.

Lesson: synthesis should recommend whether independent review is worth considering and whether decomposition is likely to create a real execution/context benefit. The dedicated review/decomposition prompts remain the authority if invoked; synthesis only performs early routing.

Human approval remains the gate. A capable human may approve a comprehensible non-Complex plan without independent review.

### 5. Verification needs economics and ownership, not merely a list of commands

The run showed repeated Playwright/Vitest execution across Build, Review, Patch, and Testing. Some repetitions were justified: a newly authored browser test must be exercised; Review used targeted Playwright to prove a suspected flaky regression; Testing appropriately reran independent browser verification. Other repetitions were excessive, especially broad browser replay after a narrow test-only patch.

Lesson: the Techplan should state for non-trivial verification:

- what evidence is required;
- why that evidence/tool is worth running;
- the risk if it is skipped;
- the primary phase/human owner.

Build owns focused edit-loop confidence. Code Review is primarily independent diff reasoning and may run a targeted repro when needed to substantiate a finding. Testing owns independent final/broad verification. A narrow patch reruns affected verification unless the patch materially broadens risk/scope.

### 6. Browser automation should be justified by behavior/risk, not ceremony

In this task, Playwright was defensible because responsive route behavior, CTA navigation, mobile drawer behavior, and focus return are browser-level concerns and the task explicitly requested repeatable browser evidence.

That does not generalize into `material UI = always add/run Playwright everywhere`. A visual-only spacing/typography adjustment may be better served by focused component checks plus rendered human/agent inspection. The planning contract should explain why browser automation is warranted and what risk remains if omitted.

### 7. Creative product/brand exploration belongs upstream when the engineering spec needs a stronger design direction

The run intentionally chose a conservative, truth-preserving calibration of the existing `/` surface and explicitly rejected new brand-defining assets. Build correctly followed that locked contract. The human owner nevertheless expected more creative brand exploration.

Lesson: do not add a new Harscode creative lifecycle. When brand/UI direction is materially open, perform product/design exploration upstream (for example in a dedicated ChatGPT/design session), obtain a human-selected direction, then feed a clear durable design brief/spec into Harscode. Harscode Exploration remains responsible for engineering understanding, ambiguity/conflict discovery, and solutioning within that prepared product/design direction.

### 8. Benchmarking is harness observability and should start before the first phase

The first run began telemetry too late for a clean Exploration baseline. Benchmark guidance should be harness-specific and capture before/after session state, session/model/reasoning identity, fresh-vs-continued state, token/allowance data exposed by the client, human prompts, rescue prompts, clarifications, and outcome quality.

Telemetry must remain outside phase correctness artifacts unless a task explicitly needs it.

## Accepted refinement scope after Validation #1

The human owner accepted the following refinement directions for workflow-v2:

1. compact workflow-artifact provenance;
2. clearer Phase Handoff with explicit Human decision and human-readable session transition;
3. Techplan early routing recommendations for independent review and decomposition plus proportional/fail-fast planning language;
4. verification rationale/risk/primary-owner guidance and sharper Build/Review/Testing verification boundaries;
5. Codex harness operator/benchmark guidance, including proportional approval around destructive filesystem/Git actions.

## Explicit non-goals

Validation #1 does **not** justify:

- making independent Techplan review mandatory;
- making decomposition mandatory;
- creating a new Patch lifecycle phase;
- creating a durable Stage-1 Exploration artifact merely for ceremony;
- creating a Harscode creative-design lifecycle;
- removing independent Code Review or Testing;
- banning Playwright or broad final verification;
- optimizing solely for token reduction at the expense of correctness.

## Next validation shape

Do not replay the same implementation merely to obtain a prettier metric. That task is contaminated by learned solutions and known defects.

After the accepted refinements are applied, freeze a new workflow-v2 candidate checkpoint and run it on a different real task. For Kencleng, the human owner intends the next frontend iteration to restart from a deliberately clean frontend implementation foundation after a stronger upstream brand/design direction is prepared. Existing Validation #1 code remains evidence/history until that reset is intentionally prepared; it should not be silently deleted as part of this Harscode refinement.

Evaluate the next run directionally on:

- same-or-better correctness;
- rescue/clarification prompts;
- human uncertainty about next actions;
- handoff quality;
- repeated verification;
- context/usage proportionality;
- final outcome quality.
