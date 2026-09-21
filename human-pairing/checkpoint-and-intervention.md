# Checkpoints and Human Intervention

This document explains how a Human should respond to workflow checkpoints without becoming the prompt engineer for the active Run.

Canonical checkpoint behavior remains owned by the active workflow phase.

## Default posture

At a normal checkpoint, prefer the smallest Human response that communicates the decision.

Example:

```text
Stage 1 Approved, lanjut ke Stage 2.
```

Do not restate durable workflow rules, scope boundaries, authority hierarchy, model choice, or solution constraints merely to make the agent remember them.

Those belong in the Run artifacts and canonical Harscode guidance.

## Approve when

Approve and continue when:

- the agent understands the task and authority correctly;
- the proposed routing/stage output is materially sound;
- no Human-owned decision is missing;
- no unsafe or out-of-scope behavior must be corrected before proceeding.

Keep the approval concise.

## Correct when

Intervene with a correction when the agent:

- materially misreads the requirement;
- uses the wrong authority precedence;
- treats a hypothesis as settled scope;
- invents product/design/security semantics;
- crosses a protected boundary;
- misstates current durable state in a way that would affect the next step.

Correct the smallest material issue. Avoid rewriting the whole prompt.

If the issue came from bad durable guidance rather than local execution, record it as system/pilot evidence.

## Escalate to an Authority Decision when

Do not solve the issue through ad-hoc checkpoint wording when the unresolved question would establish or materially change:

- Product meaning;
- Design authority;
- Security/privacy policy;
- scope ownership;
- public contract semantics;
- another concern owned by a Human Authority.

Route the question as an `Authority Decision` and keep execution blocked only where that decision is actually required.

## Do not hide system weakness with prompt engineering

If the agent needs repeated reminders of rules that are already durable, resist adding increasingly detailed checkpoint prompts.

Prefer:

```text
observe failure
→ classify cause
→ record pilot/system evidence
→ fix the owning durable guidance when justified
```

over:

```text
observe failure
→ write a larger Human prompt every time
```

## Human approval is not orchestration ownership

A Human checkpoint decision does not mean the Human must:

- create downstream Work Units manually;
- choose the next workflow phase from memory;
- restate Run context;
- select files to inspect;
- author the agent's solution.

After the checkpoint, the Orchestrator should resume routing from durable state.

## Session transition at checkpoints

A checkpoint may also be a good place to move to a fresh Session.

When doing so, keep the decision simple:

```text
Stage 2 Approved. Stop di sini; Stage 3 dilanjutkan di fresh Session.
```

A fresh Session does not automatically create a new Run. See `session-continuity.md` for continuation-fitness rules.

## Pilot interpretation

During CRTV, a checkpoint is also an observation point.

Useful evidence includes:

- whether the Human could approve with a short response;
- whether the agent honored the stop;
- whether durable artifacts were sufficient;
- whether the Human had to add solution-steering instructions;
- whether a correction belonged to execution, orchestration, workflow guidance, or project authority.

The target is not zero Human involvement.

The target is Human involvement focused on decisions and corrections that genuinely belong to the Human.
