# S1 Human Approval Gates — Proposed

> **Status:** Formation-time declarative S1 gate contract, not proven runtime enforcement. Applies to both `supervised` (default) and explicit Human-selected `autonomous`. See general [formation gate semantics](../../../space-formation/contract-and-readiness.md).

## Gate and transition map

| Boundary | Trigger / revision-bound evidence | Human decision and blocked action | Resume / invalidation |
| --- | --- | --- | --- |
| **F — Formation (external prerequisite)** | Exact S1 reusable definition Git revision | Human authorizes formation before S1 can claim FORMED; **no Space invocation** solely from file presence | Changed material definition needs separate owning review; not an invocation grant |
| **I — Invocation (external prerequisite)** | Exact I1–I4 assignment sources, project ref/SHA, scope, output/state locations, chosen mode and actual runtime readiness | Human directly authorizes S1 execution; **Coordinator cannot start** from a Balad advisory message or generic approved definition | Valid only for authorized project/revision/tools/writes and `supervised` unless Human explicitly chooses `autonomous` |
| **G1 — Material owner decision (conditional)** | X1/O1/O2/O3 or review uncovers a materially unresolved Product Authority, cross-consumer commitment or risk choice not delegated to S1; cite exact source, proposed choice, affected artifact revision | Owning Human decides before any downstream production **depending on that unsettled choice** | Record exact decision and affected revision/scope; material revision or changed premise requires reconsideration |
| **G2 — Protected/security permission (conditional)** | Proposed work would require otherwise protected project/spec/auth/security change or materially expands granted tool/path/decision scope | Authorized Human approves specific action/revision/path before **that action**; otherwise leave it blocked | Permission bound to exact scoped action and project rules; unrelated or stale approval does not carry over |
| **A — Final downstream acceptance (external)** | Actual versioned O1–O5 bundle, internal review status, source trace, unresolved findings and evidence limits | Human decides accept / request changes / defer before downstream use as **binding accepted solution** | Accept exact bundle revision and scope, not future unreviewed revisions; S1 output production alone grants no implementation permission |

**Not mandatory approval gates:** X1 completion, ordinary O1/O2/O3 handoffs, internal Reviewer completion, routine delegated corrections. In default **supervised** mode, the Coordinator offers Human *progress review + continue/revise/stop* at meaningful milestones (initial S1 suggestion: after X1, after O1/O2/O3, plus final output). These are **supervision checkpoints**, not automatic promotion to approved Product Authority. In autonomous mode these review pauses may be omitted, but F/I/G1/G2/A obligations are unchanged.

## Evidence and stop rule

A gate needing Human approval must expose the **trigger**, **owning source and relevant artifact/ref/version**, **observed review/evidence**, **specific Human authority**, **exact action held**, and **scope/revision that could be resumed**. A Coordinator may continue unaffected authorized work where safe, but may not proceed along the blocked dependency or self-approve. Denied, absent, ambiguous, scope-mismatched or materially stale approval remains **BLOCKED**; revisions to approved consequential content invalidate the affected authorization until revalidated.

Keep a minimal durable approval/continuation record in the concrete authorized invocation state; do not create a new workflow engine or assume ChatGPT memory is the approval ledger. For protected actions, real harness/tool permissions must respect the stop boundary; a prompt saying "pause" alone is not verified enforcement.

**No automatic Techplan gate in S1:** S1 produces solution design, not Builder/implementation. A future Builder Space should declare a reviewed **Techplan-revision Human approval** as a mandatory gate **before Build execution**, in both modes, without importing that requirement into every Space.
