# Guardrails

Hard stops and no-assumption boundaries for Techplan synthesis/revision.

## 1. Protected Guidance Requires a Proposal

Do not change protected files in this folder during ordinary task work. Use the root proposal mechanism and the applicable human gate.

## 2. Exploration Evidence Is Read-Only History

Do not rewrite/delete `{TASK_PATH}/1-exploration/logs/` to make synthesis easier. Reconcile duplication/conflict in the Techplan and preserve source anchors.

## 3. Do Not Silently Change a Locked Material Contract

If an Approved/Implemented Techplan would change a material product/domain rule, scope, authority/security boundary, architecture/ownership decision, interface/data contract, risk acceptance, or verification strategy, do not overwrite the current-effective plan.

Keep the existing `{TASK_PATH}/2-techplan/techplan.md` as the current-effective predecessor and prepare or continue a single `{TASK_PATH}/2-techplan/techplan.candidate.md` as the Draft/In Review successor. The candidate may cross the applicable planning Review/resolution/Human gate, but it does not become current-effective until the exact successor is approved and promoted through bounded lifecycle reconciliation.

Do not create versioned Techplan copies merely to preserve history. Git plus reconstructable revision/provenance pointers are the default content history.

Do not classify change safety by section number alone. §8 Interface Contract, §12 verification obligations, and §13 Open Items can be material even though older guidance once called later sections “derived.”

Mechanical corrections that do not change executable meaning may be updated normally and recorded where the workflow/report expects them. When an already-Approved artifact crosses a reliance boundary, preserve enough before/after provenance to show that the allowed correction was mechanical rather than a hidden contract revision.

## 4. Read Target-Repo Authority Before Declaring Its Contract

Before finalizing interface/implementation conventions, read the applicable target-repo `AGENTS.md`/README/convention/spec source. Harscode is portable; it does not invent project-specific naming, error, API, state, design, or build conventions.

## 5. Do Not Invent Technical Facts

Paths, symbols, signatures, schema/API details, existing behavior, and line/section anchors must come from durable source material or a direct live-code/spec check. If uncertain, write `TBD — verify` / Open Item rather than presenting a guess as fact.

## 6. Stop on Newly Discovered Breaking/Data/Authority Risk

If synthesis reveals a potential breaking change, risky data operation, security/authority boundary change, or existing-client impact that the Exploration evidence did not make explicit, surface it for resolution. Do not quietly downgrade it into a routine Edge Case.

## 7. Full Code Snippets Only When They Add Contract Value

Prefer `path + symbol + intended change + precedent`. Include a full body/snippet only when the logic is genuinely novel/non-obvious and the snippet materially reduces implementation ambiguity. Code remains source of truth for exact implementation.

## 8. Human Report Cannot Introduce Decisions

Generate `report-techplan.md` from `report-template.md` only when the exact Techplan artifact/revision being presented has converged enough to enter the Human approval gate, after applicable planning review/resolution has converged. The report is derived Human-review evidence; it is not a separate authority object and is not generated as a post-approval artifact.

The planning workflow participant that owns the current Techplan semantics generates or regenerates the report. The Orchestrator may dispatch that work but must not silently author the report as a substitute for the planning participant.

If the report needs a fact/decision/risk that is absent or ambiguous in the Techplan, fix/reopen the Techplan instead of inventing the answer in the report.

## 9. Diagram Must Be Syntax- and Semantics-Valid

When a diagram is warranted, validate both rendering syntax and branch/state/control-flow meaning against the Techplan rules/contracts. If either cannot be confirmed, fix or simplify the diagram rather than shipping an attractive contradiction.

## 10. Resolved Open Items Stay Recorded

Move resolved items to §13 Resolved with the actual resolution; never silently delete them. If the resolution materially changes the contract, apply §3 as well.

## 11. Approved Human Report Must Stay Derived

When the current-effective Approved Techplan is replaced by an approved successor, regenerate `report-techplan.md` from the successor before treating the report as current. During candidate review, the report must identify the exact candidate revision it represents. The Techplan artifact under review remains authoritative if the two disagree.

## 12. Flagged Sensitive Risk Needs a Traceable Pointer

A surviving concurrency/perf/security-sensitive Exploration finding must appear in §12 Test Focus Pointer with its evidence anchor. If no longer relevant, retain an explicit N/A/reason or Decision Log pointer.

If uncertain whether a finding requires specialized Testing coverage, surface the uncertainty instead of silently omitting the risk or running a heavyweight test inside Build.
