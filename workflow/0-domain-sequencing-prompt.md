# Domain Sequencing Prompt

Runs once per domain, before the first feature in that domain gets its
first exploration session — not once per feature. Produces a coarse,
domain-wide dependency/parallel-safety graph across all of a domain's
*planned* features, so you know which ones can run in parallel sessions
and which must wait on another, before picking which one to start next.

## When To Use This

Run this the first time you're about to start exploration on any
feature in a domain that doesn't have a `_domain-manifest.md` yet. Skip
it for that domain's 2nd, 3rd, etc. feature once the manifest already
exists — unless the domain's planned feature list has changed since
(a feature added, removed, or re-scoped), in which case regenerate it.

Do not run this per-feature — that's what
`2-3-techplan-decomposition-prompt.md` is for, at a finer grain, after a
specific feature's techplan is locked. This prompt runs earlier and
coarser: before any feature in the domain has an exploration or techplan
yet.

## What This Is Not

- **Not a replacement for per-feature decomposition.** This pass reasons
  at the shared-resource/fencing grain — does feature A and feature B
  touch the same table, the same service, the same file-path-fencing-
  tier path — not at rule-level implementation detail. Most features in
  scope won't have an exploration or techplan yet at this point, so
  detail below that grain isn't available to reason about honestly.
- **Not equally confident as the post-techplan decomposition graph.**
  State this explicitly in the output: this manifest is necessarily
  coarser and more provisional than `2-3-techplan-decomposition-
  prompt.md`'s manifest, precisely because it runs before any of the
  domain's features have been explored. If a feature's own exploration
  later surfaces a cross-feature dependency this pass missed, that's an
  expected outcome, not a failure of this pass — revisit/regenerate the
  domain manifest when it happens, don't treat the original as settled.
- **Not reinterpretation of anything already decided.** If the domain's
  feature list, scope, or an invariant it depends on is ambiguous or
  looks wrong, stop and report it — don't resolve it here.

## Inputs required before running

- `{DOMAIN_SPEC}` — whatever enumerates this domain's planned features
  (a roadmap/spec document, or an existing set of placeholder feature
  folders under `{DOMAIN_PATH}`). Read it in full before doing anything
  else.
- `{DOMAIN_PATH}` — the parent directory that will hold every feature's
  `{TASK_PATH}` within this domain, and where `_domain-manifest.md` gets
  written (see root `README.md` § Task Working Directory Structure).
- `{HARSCODE_WORKSPACE_ROOT}` — see `workflow/README.md` § Path
  Variables Convention.
- The target repo's own `AGENTS.md` (or equivalent) — specifically
  whatever File-Path-Fencing-Tier-0-class section it declares. This
  prompt does not define what counts as fenced; it reads the existing
  declaration and checks it against the domain's planned features.

## Response Style

Full detail, no compression, same as the per-feature decomposition
prompt (`workflow/README.md` § Response Style By Phase) — this is a
planning-type pass whose output other sessions will rely on to decide
execution order. State the splitting axis chosen and why, explicitly.

## Prompt

```
Read {HARSCODE_WORKSPACE_ROOT}/workflow/0-domain-sequencing-prompt.md in
full first — "When To Use This" and "What This Is Not" define what
you're allowed to do here and what you must not do (no per-feature
implementation detail, no resolving ambiguity on your own, explicit
lower-confidence caveat in the output).

Response style: full detail, no compression — this output is what
later sessions use to decide execution order.

Read {DOMAIN_SPEC} in full — this domain's planned feature list. Read
the target repo's own AGENTS.md (or equivalent) for its File-Path-
Fencing-Tier-0-class declaration, if any.

For each pair of planned features in this domain, reason about whether
they share a hard dependency (one's data model, service, or contract is
a prerequisite for the other), a soft/fencing overlap (both would touch
the same Tier-0-class fenced path, or the same shared table/service,
without one strictly requiring the other to exist first), or no
relationship at all. Use the same "hard dependency" / "no hard
dependency" vocabulary as
{HARSCODE_WORKSPACE_ROOT}/workflow/2-3-techplan-decomposition-prompt.md
§ 2, at the domain grain instead of the per-task grain.

State explicitly that this graph is coarser and more provisional than a
post-techplan decomposition manifest, since it's produced before any
of these features have been explored — this must appear in the output,
not just be true implicitly.

Write {DOMAIN_PATH}/_domain-manifest.md: the feature list, the
dependency/parallel-safety graph, explicit fencing-overlap call-outs,
and a one-line recommended starting order. Report which pairs (if any)
you flagged as fencing overlaps, so I can confirm before anyone starts
on them.
```

## Output

Write to `{DOMAIN_PATH}/_domain-manifest.md`:

- The domain's planned feature list.
- A dependency/parallel-safety graph between features (hard dependency /
  fencing overlap / no relationship), same vocabulary as the per-task
  decomposition manifest.
- Explicit call-outs of any File-Path-Fencing-Tier-0-class overlap
  between features — these are exactly the pairs that should stay
  serial, or route through a single explicitly-asked-for session, per
  the target repo's own fencing rule.
- A recommended starting order (which feature(s) can begin exploration
  in parallel sessions right away, which should wait).
- The lower-confidence caveat, stated directly (see "What This Is Not").

## Notes

- This is a snapshot at generation time, same as the per-task
  decomposition manifest — don't hand-edit it to track progress.
- If a later feature's exploration or techplan surfaces a cross-feature
  dependency this pass didn't catch, that's expected, not a defect —
  regenerate `_domain-manifest.md` rather than patching around the
  surprise ad hoc.
- This prompt intentionally does not define or invent what counts as a
  fenced path — it reads whatever the target repo's own `AGENTS.md` (or
  equivalent) already declares. If that repo has no such declaration,
  the fencing-overlap check has nothing to check against; say so rather
  than silently skipping it.
- Cross-reference: `2-3-techplan-decomposition-prompt.md` for the
  finer-grained, higher-confidence version of this same kind of graph,
  run per-feature after that feature's techplan locks.
