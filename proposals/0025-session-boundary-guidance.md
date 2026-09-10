# 0025 — Session boundary guidance: which phases share a session, which don't

**Status:** Accepted
**Date:** 2026-09-10
**Protection Tier:** general
**Triggered by:** Real usage pattern on koperasiqu-web-app's backend track — every feature was run as exploration + techplan + build + all patches in one continuous session, then code-review in a second session, then testing in a third. `README.md` § Usage only ever blessed one specific merge ("running exploration and techplan synthesis in one session is fine," step 3) and said nothing about the other phase boundaries, leaving session-splitting entirely to individual judgment with no stated default
**Target area:** workflow (lightweight phases — no formal protection today, addressed here for traceability given the change touches the root `README.md`'s numbered Usage list, not just a single phase's own guideline file)
**Target file(s):**
- `workflow/README.md` — new `## Session Boundaries` section
- `workflow/AGENTS.md` — one new hard-rule bullet pointing at it
- `README.md` (root) — step 3 of `## Usage` gets a cross-reference instead of standing as the only stated session-merge rule

## Gap found

This workspace already has the underlying idea — the "amnesiac
contractor" framing (root `README.md` § Philosophy) and, more
concretely, `harness-optimization/claude-code/frontend/subagents.md`'s
explicit statement that a code-review subagent shouldn't have `Write`
access to what it's reviewing, i.e. each phase's authority should be
fenced from the others. But that idea was only ever expressed as a
Claude-Code-specific *mechanism* (subagents), never as a harness-
agnostic *default* for how many sessions a feature should span when an
agent isn't using subagents at all (e.g. working interactively, one
session at a time, pasting each phase's prompt by hand). Without a
stated default, "exploration+techplan+build+patches in one session" is
indistinguishable from a deliberate choice versus just how long the
session happened to keep going — exactly the kind of judgment call this
workspace's own philosophy says shouldn't be left implicit.

## Proposed change

Add to `workflow/README.md`, after "Why Each Stage Has a Different
Internal Structure" and before "Governance":

```markdown
## Session Boundaries

This section states the default number of sessions a single feature
(one `{TASK_PATH}`) should span, and where the boundaries fall — the
harness-agnostic counterpart to `harness-optimization/<harness>/
<track>/subagents.md`'s per-phase tool/context isolation, for whoever
isn't running phases as separate subagents.

**Default: four sessions per feature**, grouped by shared authority and
response-style tier (`README.md` § Response Style By Phase), not by raw
phase count:

1. **Exploration + Techplan** — both planning-type (full reasoning,
   read-mostly). Merging these two, specifically, is the one combination
   root `README.md` § Usage already blesses (step 3) — this section
   doesn't change that, it generalizes what comes after it.
2. **Build + Patch loop** — execution-loop, terse, and the tool scope
   genuinely differs from planning (write access, running the code).
   Every patch this feature ever needs — whether it came from this
   session's own iteration, or from a patch-plan written later by
   code-review or testing — executes here, per `README.md` § Task
   Working Directory Structure's existing rule that patches are always
   build activity.
3. **Code-review** — its own session. Different concern (investigating
   already-built code, not building it) and, per `subagents.md`'s
   existing principle, should not carry write access into that
   investigation.
4. **Testing** — its own session, same reasoning as code-review: a
   different concern from building, verified independently rather than
   from inside the build session's own accumulated context.

**Why not fold build into session 1:** a build session inheriting
exploration/techplan's full raw reasoning trail (which, on a non-trivial
feature, can be a dozen-plus log files) carries deadweight context into
a phase that's supposed to run terse and iterate fast — the same
context-isolation reasoning `subagents.md` already applies to Claude
Code's native subagent boundary applies just as well to a plain session
boundary when subagents aren't in use.

**Why not split further** (e.g. exploration and techplan as two
sessions): not disallowed, but not the default either — root `README.md`
step 3 already covers this case, and splitting a small/linear feature
further is the same "premature structure" the decomposition prompt
(`2-3-techplan-decomposition-prompt.md`) already warns against for a
different granularity.

**Re-entry after code-review or testing asks for a patch:** the patch
itself is drafted and executed back in the build session's context (a
continuation of session 2, or a fresh session re-grounded on
`techplan.md` plus the specific patch-plan — either is fine). What must
not happen is drafting the patch fix *inside* the code-review or testing
session — that session's tool scope shouldn't include `Write` in the
first place, per `subagents.md`'s existing separation-of-authority
principle.

This is guidance, not a hard rule — same tier as every other lightweight
`workflow/` phase (see Governance below): correct it in the moment if a
specific feature is small enough that a stricter split is pure overhead,
same posture the decomposition prompt already takes toward "premature
structure."
```

`workflow/AGENTS.md` gets one new bullet under Hard rules:

```markdown
- Default session split for one feature: (exploration+techplan),
  (build+patch loop), (code-review), (testing) — four sessions, not one
  per phase and not one for the whole feature. See `README.md` §
  Session Boundaries for the rationale and the one blessed exception
  (merging exploration+techplan).
```

Root `README.md` step 3 of `## Usage` gets a trailing cross-reference
added (`— see workflow/README.md § Session Boundaries for how the rest
of a feature's phases are meant to split across sessions`) instead of
being the only place this topic is addressed.

## Rationale

Genuinely generic — "how many sessions should one feature span, and
where do the boundaries fall" applies to any project using this
workflow under any harness, independent of Claude Code specifically
(which is why it belongs in `workflow/README.md`, not
`harness-optimization/`). It's also directly derivative of reasoning
this workspace already committed to once for the Claude-Code-subagent
case (0010) — this proposal generalizes that same reasoning to the
harness-agnostic default, rather than inventing a new principle.

Written as a proposal despite targeting a "lightweight, corrected in
the moment" phase area, because the change is structural (a new
top-level section plus an edit to the root `README.md`'s own numbered
Usage list) rather than a single guideline-file correction — consistent
with how 0007 (a genuinely structural addition) went through the
proposal process even though nothing forced it to.
