# session-boundaries.md (Codex)

## What this translates

`workflow/README.md` already defines the portable default session boundary for one feature:

```text
1. Exploration + Techplan
2. Build + Patch
3. Code Review
4. Testing
```

Pull-request generation consumes the approved/verified result afterward.

Codex does not change this lifecycle. The harness translation only explains how to preserve the same context/authority separation when using Codex sessions or optional native subagents.

## Portable baseline: fresh/re-grounded sessions

The correctness baseline is ordinary Codex session isolation.

### Session 1 — Exploration + Techplan

Purpose:

- understand the target repo and requirement;
- resolve material ambiguity;
- produce/review the execution contract.

Expected posture:

- read-heavy;
- full planning reasoning where Harscode requires it;
- write only the planning/task artifacts the active Harscode prompt permits;
- do not begin production implementation merely because the plan looks obvious.

Ground on the target repo's applicable `AGENTS.md`, relevant project/spec sources, and the current Harscode Exploration/Techplan guidance.

### Session 2 — Build + Patch

Purpose:

- execute the locked plan;
- run the tight edit → verify → fix loop;
- apply later patch plans produced by review/testing.

Expected posture:

- narrow production write scope;
- terse process narration;
- load only the planning output and project sources needed to implement the current work unit rather than carrying the full Exploration trail forward.

When Code Review or Testing later requests a patch, route implementation back to this authority. Do not quietly convert the review/testing context into a second build owner.

### Session 3 — Code Review

Purpose:

- independently inspect the implementation for safety, quality, and consistency issues.

Expected posture:

- read-only production scope where practical;
- do not fix findings inside the review session;
- produce findings/patch-plan input according to Harscode Code Review guidance.

A review session that edits its own findings away loses the separation Harscode created this boundary to preserve.

### Session 4 — Testing

Purpose:

- independently verify observable correctness with the appropriate objective/static/rendered/runtime evidence.

Expected posture:

- production code read-only where practical;
- test/evidence artifacts may be created only where the active Harscode/target-repo guidance permits;
- if a product-code fix is needed, route it back through Build/Patch and then re-run verification.

Testing is the final independent verifier when Harscode uses a separate Testing phase.

## Re-grounding a fresh Codex session

A new session does not need the entire previous chat transcript.

Re-ground on the smallest sufficient durable state:

```text
target repo AGENTS.md hierarchy
+ current task/feature artifact(s)
+ relevant canonical project/spec docs
+ current Harscode phase guidance
+ specific prior finding/patch plan when re-entering Build
```

Do not paste raw Exploration logs into Build unless the plan explicitly says a particular log contains unresolved evidence the implementation needs.

## Codex native subagents / multi-agent tools

Current Codex releases expose native multi-agent/subagent capability. Treat that as an optional optimization layer, not as Harscode policy.

A native subagent is useful when it creates a real isolation or parallelism benefit, for example:

- an independent review lane;
- independent targeted investigation of separate concerns;
- bounded verification work that can report evidence back to the main session.

Do not require subagents merely because the capability exists.

Do not use a subagent to bypass Harscode authority separation — e.g. spawning a write-capable reviewer that both identifies and silently fixes its own findings.

If native multi-agent mechanics change or are unavailable, fall back to the four durable session boundaries above. The workflow must remain valid without them.

## Parallelism boundary

Parallel Codex agents are safe only when the underlying Harscode/project work is safe to parallelize.

Harness concurrency never overrides:

- overlapping write-scope concerns;
- migration/order dependencies;
- shared contracts;
- project protected paths;
- human-review gates.

The harness can execute a parallel plan; it does not decide whether the plan is logically safe.

## Pull-request generation

PR generation should consume the final diff plus the durable Harscode artifacts/evidence required by `workflow/pull-request/`.

Do not reconstruct PR truth from the build session's memory when the final repository state or final Testing evidence says something else.
