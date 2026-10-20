# 0029 — Domain-grouped projects: optional domain closure review, and domain sequencing made conditional

**Status:** Accepted - Anhar
**Date:** 2026-09-14
**Protection Tier:** general
**Triggered by:** A manual whole-domain audit on koperasiqu-web-app's backend track (domain `akun`, features `D01-01` through `D01-09`), run before declaring the domain done. Every feature had individually reached a testing commit, yet the domain was not actually finished: one feature (`D01-09`) had been decomposed into 5 tasks and only the first had ever been built. The same audit found five more issues no per-feature phase was positioned to catch — a stale permission name in "already revised" API contract prose, a hardcoded value where sibling implementations were config-driven, a live rule violation from pre-domain boilerplate, a domain-wide task (a global rate limiter) that belonged to no feature's task list and so was never built, and a manual-testing collection that had fallen behind later features. While reviewing the resulting proposal, the workspace owner set a firm constraint: domain-level phases must only apply to projects that actually divide their work by domain — they are not a required part of this workflow. That constraint exposed that proposal 0026 had already made domain sequencing an unconditional hard rule.
**Supersedes:** the staged draft that originated in koperasiqu-web-app (`.agents-local/backend/proposals/0007-domain-closure-review-checklist.md` plus `domain-closure-review-checklist-draft.md`), which was copied here unnumbered. Its checklist content is carried forward below, generalized and restructured to this workspace's conventions.
**Target area:** workflow (lightweight phases + one new root prompt)
**Target file(s):**
- `workflow/README.md` — new section `## Domain-Grouped Projects (Optional)`, the single place the condition is defined
- New: `workflow/7-domain-closure-prompt.md`
- `workflow/0-domain-sequencing-prompt.md` — intro and "When To Use This" state the condition
- `workflow/AGENTS.md` — the 0026 hard-rule bullet rewritten as conditional, covering both domain prompts
- `README.md` (root) — § Usage step 3 marked optional, new optional step 12; § Task Working Directory Structure's `{DOMAIN_PATH}` note marked domain-grouped-only
- `workflow/5-testing/guidelines.md` — § Final Verification Before Considering Done gets a full-suite check for cross-cutting changes
- `workflow/3-build/guidelines.md` — § What this phase is not gets the self-contradicting-task-file rule

## Gap found

### 1. No domain-level check exists

The per-feature pipeline (exploration → techplan → build → code-review
→ testing) verifies each feature against its own techplan. Nothing
verifies a domain as a whole once all its features are through that
pipeline: whether every decomposed task actually landed, whether
features agree with each other (shared catalogs, config conventions),
whether the domain's published API contract still matches what
shipped, and whether a cross-cutting concern that no single feature
owns got built at all. The koperasiqu `akun` audit above is a concrete
instance, not a hypothetical — every per-feature signal looked green,
and every feature's own reports were honest about their gaps, but
nothing forced a domain-level rollup that would read them together.

### 2. Domain-level guidance is currently unconditional

`workflow/` is meant to be generic and portable across projects
(`workflow/README.md` § What's Explicitly Out of Scope Here). Not every
project divides its work by domain — many are planned and built
feature by feature with no grouping above `{TASK_PATH}`. Proposal 0026
nonetheless landed domain sequencing as:

- a hard rule in `workflow/AGENTS.md` ("Before the first feature session
  in a new domain, run `0-domain-sequencing-prompt.md`…"),
- a numbered step (3) in root `README.md` § Usage with no qualifier,
- a `{DOMAIN_PATH}` description in § Task Working Directory Structure
  written as if every project has one.

Adding a closure review on the same footing would compound that. Adding
it as optional while leaving sequencing mandatory would make the two
ends of the same domain bracket inconsistent.

### 3. Two items in the staged draft aren't domain-specific

The staged draft's checklist included a full-test-suite rule for
cross-cutting changes (its item 7) and a tie-breaker for a task file
that contradicts itself (its item 8). Both apply to any project,
domain-grouped or not. Placed only inside an optional domain phase,
projects that skip the phase would never see them.

## Proposed change

### A. `workflow/README.md` — new section

Insert immediately before `## Governance`:

~~~markdown
## Domain-Grouped Projects (Optional)

Some projects divide their roadmap/spec by domain — e.g. a domain whose
planned features are `D01-01` through `D01-09` — and group those
features' `{TASK_PATH}` folders under a shared `{DOMAIN_PATH}`. **For
those projects only**, two domain-level prompts bracket the per-feature
cycle:

- `0-domain-sequencing-prompt.md` — before the first feature in a
  domain: which planned features can run in parallel sessions and which
  must wait on another.
- `7-domain-closure-prompt.md` — after every feature in the domain has
  finished testing: a whole-domain check before the domain is declared
  done.

Neither is part of the default lifecycle. A project that plans and
builds feature by feature, without grouping features by domain, skips
both entirely — nothing to record, no placeholder file, no note that
they were skipped.

"Domain" here means how the *work* is divided and planned, not
Domain-Driven Design. A DDD codebase planned feature by feature doesn't
need these prompts; a non-DDD codebase whose roadmap is split by domain
can use them.

The two prompts are independent of each other. Closure can run for a
domain that never had a `_domain-manifest.md` (it falls back to the
domain spec for the feature list), and producing a manifest doesn't
oblige a closure review — though a domain large enough to need
sequencing is usually large enough to benefit from closure.

The numbers mark lifecycle *position* (before exploration / after
testing), not obligation.

Origin: proposal 0029, which also retrofitted this condition onto
0026's sequencing prompt after it had landed as an unconditional rule.
~~~

### B. New file: `workflow/7-domain-closure-prompt.md`

Follows § Prompt File Shape. `When To Use This` / `What This Is Not`
sit before `Inputs` for the same reason they do in
`0-domain-sequencing-prompt.md`: whether the prompt applies at all is
the first thing a reader needs. The checklist sits after `## Prompt`
as a phase-specific section (shape item 4), like
`4-code-review-prompt.md`'s breakdown.

~~~~markdown
# Domain Closure Review Prompt

Runs once per domain, after every feature in that domain has finished
its own per-feature cycle, and before the domain is declared done.
Checks the domain as a whole — the things no single feature's testing
phase is positioned to see. **Optional:** applies only to projects that
group their work by domain (`workflow/README.md` § Domain-Grouped
Projects).

## When To Use This

- Only if the project groups its features by domain. If it doesn't,
  this prompt doesn't apply — skip it entirely.
- The trigger: someone is about to declare a domain finished, start
  building another domain against this one's API, or archive the
  domain's folder — and every planned feature in the domain (per
  `_domain-manifest.md` if one exists, otherwise `{DOMAIN_SPEC}`) has
  completed its testing phase.
- Once per domain. Re-run only if the domain reopens — a feature added
  or substantially reworked after the review.
- Running `0-domain-sequencing-prompt.md` earlier is not a
  prerequisite.

## What This Is Not

- **Not a fix session.** This is verification only. Every finding goes
  back through the normal cycle — a patch plan executed in a build
  session, then code-review/testing as usual (`workflow/README.md` §
  Session Boundaries). A closure review that finds and fixes things in
  the same breath, without that surrounding rigor, stops being an
  independent check.
- **Not a re-run of per-feature testing.** It doesn't re-verify each
  feature against its own techplan. It reads the features' existing
  reports — their actual text, not just their pass/fail — and checks
  what only becomes visible across features.
- **Not a decision point.** If a finding needs a product, contract, or
  authority decision, record it as open and report it — don't resolve
  it here (`workflow/README.md` § Phase Convergence).

## Inputs required before running

- `{DOMAIN_PATH}` — the domain's parent directory; the review is
  written here.
- `{DOMAIN_SPEC}` — whatever enumerates the domain's planned features.
- `{DOMAIN_PATH}/_domain-manifest.md`, if it exists — preferred as the
  feature list baseline.
- `{HARSCODE_WORKSPACE_ROOT}` — see `workflow/README.md` § Path
  Variables Convention.
- `[TARGET REPO CONVENTION FILE PATH]` — the target repo's `AGENTS.md`
  (or equivalent), specifically its non-negotiable rules.
- The domain's published API contract(s) and any manual-testing
  collection or guide the project maintains, if they exist.
- Precondition: every feature in the domain has finished its testing
  phase.

## Response Style

Full reasoning, no compression — this is a verification pass whose
output decides whether a domain counts as done (`workflow/README.md` §
Response Style By Phase). Deliverable completeness is high: every
finding carries concrete file/line evidence, not an impression.

## Prompt

```
Read {HARSCODE_WORKSPACE_ROOT}/workflow/7-domain-closure-prompt.md in
full first — "When To Use This" and "What This Is Not" define what this
session may and may not do. In particular: do not fix anything you
find, and do not resolve open decisions.

Response style: full reasoning, complete deliverable — every finding
needs file/line evidence.

Feature list baseline: {DOMAIN_PATH}/_domain-manifest.md if it exists,
otherwise {DOMAIN_SPEC}. Read the target repo's convention file
([TARGET REPO CONVENTION FILE PATH]) for its non-negotiable rules.
For every feature under {DOMAIN_PATH}, read its build, patch, and
testing reports in full.

Run every section of this file's Checklist against the domain as a
whole, in order. Don't skip a section because an earlier one came back
clean.

Write {DOMAIN_PATH}/_domain-closure-review.md in the shape described
under Output. End by telling me the verdict, the blockers (if any), and
which findings need a decision from me.
```

## Checklist

### 1. Spec delivery completeness

- Every planned feature's **entire** scope landed — not just that a
  build/testing report exists. A feature whose techplan was decomposed
  into multiple tasks needs every task accounted for, not only the
  first.
- Read the reports' own text for phrases like "not yet built",
  "deferred", or "pass with follow-ups". Those are the authors' honest
  signals; a green result doesn't override them.
- Cross-check the domain's task list against what's live in code
  (routes, migrations, seeders, jobs). A task silently absorbed into
  another feature's build is fine — note where it actually landed.
- Look specifically for cross-cutting work no single feature owns (a
  global rate limiter, a shared error convention, shared middleware).
  A purely per-feature decomposition is exactly where these fall
  through.

### 2. API contract cross-check

- Diff the published contract against what shipped: paths, methods,
  request/response fields, status codes.
- Include enum-like string values the contract names in prose —
  permission names, status values, error reason codes. A rename fully
  propagated through code and tests can still survive in contract
  prose.
- Prioritize sections the contract itself claims are current. A
  section honestly marked as not yet revised is lower risk than one
  that claims to match shipped code and doesn't.

### 3. Cross-artifact consistency

- Where the domain defines a shared catalog (a permission matrix, a
  status enum, a config-value table), verify every derived artifact
  (seeder, policy, contract prose, frontend constants) matches it
  exactly — each can drift independently while looking internally
  consistent.
- For every value the spec marks "configurable", confirm it's actually
  read from configuration and not a literal. Watch siblings implemented
  at different times: one can be hardcoded while the others next to it
  are config-driven.

### 4. Decision-record status

- Walk every proposal or decision record this domain's work produced,
  in any repo. Confirm each status reflects reality — a "Proposed"
  record that was actually applied should say so.
- List what is still genuinely open, so it doesn't disappear once the
  domain reads as closed.

### 5. Testing-docs completeness

- Enumerate the live routes/endpoints from the application itself (its
  router's own listing), not from a hand-written document, and diff
  against the project's manual-testing collection or guide. Endpoints
  added later, especially under a different namespace (admin/internal),
  are the usual gap.
- Any "not testable yet / in progress" note for a surface that has
  since shipped is now misleading, not just outdated — flag it.

### 6. General sweep

- Check the target repo's non-negotiable rules against the domain's
  *current* code, not against what techplans planned. Code that
  predates the domain (leftover boilerplate) counts as much as code the
  domain introduced.
- Where a removal or contract change happened on one side of a
  cross-track boundary (e.g. a backend endpoint deleted), check whether
  the other side still depends on it (a frontend page still calling
  it). The review doesn't fix the other track — it records the
  dependency as an explicit follow-up.

Fixes that come out of this review and are cross-cutting are subject to
`workflow/5-testing/guidelines.md` § Final Verification's full-suite
check, same as any other cross-cutting change.

## Output

Write `{DOMAIN_PATH}/_domain-closure-review.md`:

- **Verdict** — `Closed` or `Not closed`, with the blocking findings
  listed if not closed.
- **Findings** — one entry per finding: checklist section, what was
  found, file/line evidence, status (`resolved` / `patch planned` /
  `proposed` / `open — needs decision`), and where the follow-up lives.
- **Open items carried forward** — anything not blocking closure but
  not done either, so it survives the domain being marked closed.
- **Progress Log** — timestamped entries appended as findings are
  resolved in later sessions: what was fixed, what surprised you, what
  took more than one attempt. The verdict is updated when the last
  blocker clears.

## Notes

- Next step after the review: turn each unresolved finding into work
  through the normal cycle. A finding owned by a specific feature gets a
  patch plan in that feature's `{TASK_PATH}`. A finding no feature owns
  (e.g. an unbuilt cross-cutting task) becomes its own task folder under
  `{DOMAIN_PATH}` and runs the per-feature cycle like any other task.
- Append to the Progress Log as findings close; don't rewrite the
  original findings. Change the verdict to `Closed` only when no
  blocker remains.
- If the Progress Log shows this checklist missed something that will
  recur on other domains, correct this prompt — in the moment for a
  small addition, via a `general`-tier proposal if the change is
  structural.
- Automation (e.g. a script diffing the route list against a testing
  collection, or grepping for configurable-but-hardcoded values) is not
  covered here; this prompt defines what to check, not how to automate
  it.
- Cross-reference: `0-domain-sequencing-prompt.md` is the optional
  opening bracket of the same domain.
~~~~

### C. `workflow/0-domain-sequencing-prompt.md`

Intro paragraph — append one sentence:

Before:
```markdown
Runs once per domain, before the first feature in that domain gets its
first exploration session — not once per feature. Produces a coarse,
domain-wide dependency/parallel-safety graph across all of a domain's
*planned* features, so you know which ones can run in parallel sessions
and which must wait on another, before picking which one to start next.
```

After:
```markdown
Runs once per domain, before the first feature in that domain gets its
first exploration session — not once per feature. Produces a coarse,
domain-wide dependency/parallel-safety graph across all of a domain's
*planned* features, so you know which ones can run in parallel sessions
and which must wait on another, before picking which one to start next.
**Optional:** applies only to projects that group their work by domain
(`workflow/README.md` § Domain-Grouped Projects).
```

`## When To Use This` — insert a new first paragraph:

```markdown
Only if the project groups its features by domain. If it doesn't, this
prompt doesn't apply — skip it entirely and start at exploration.
```

### D. `workflow/AGENTS.md`

Before:
```markdown
- Before the first feature session in a new domain, run
  `0-domain-sequencing-prompt.md` and produce `{DOMAIN_PATH}/
  _domain-manifest.md` before picking which feature to start. Don't
  default to strict serial order across a domain's features without
  having checked this.
```

After:
```markdown
- Domain-level prompts apply only if the project groups its work by
  domain (`README.md` § Domain-Grouped Projects) — otherwise skip them
  and don't mention them. When it does: run
  `0-domain-sequencing-prompt.md` before the first feature in a new
  domain (don't default to strict serial order without it), and run
  `7-domain-closure-prompt.md` after the domain's last feature finishes
  testing, before declaring the domain done.
```

### E. Root `README.md`

§ Usage, step 3 — Before:
```markdown
3. Before the first feature in a new domain, run
   `workflow/0-domain-sequencing-prompt.md` once to produce that
   domain's `_domain-manifest.md` — it tells you which of the domain's
   planned features can run in parallel sessions and which must wait on
   another. Skip this for a domain's 2nd+ feature once the manifest
   already exists and nothing new has been added to scope.
```

After:
```markdown
3. *(Optional — only if the project groups its work by domain; see
   `workflow/README.md` § Domain-Grouped Projects.)* Before the first
   feature in a new domain, run `workflow/0-domain-sequencing-prompt.md`
   once to produce that domain's `_domain-manifest.md` — it tells you
   which of the domain's planned features can run in parallel sessions
   and which must wait on another. Skip this for a domain's 2nd+ feature
   once the manifest already exists and nothing new has been added to
   scope.
```

§ Usage, new step after step 11 ("Create the pull request."):
```markdown
12. *(Optional — domain-grouped projects only.)* Once every feature in
    a domain has finished testing, run
    `workflow/7-domain-closure-prompt.md` before declaring the domain
    done. Its findings go back through the normal cycle (patch plans,
    or new tasks for unowned cross-cutting work) — they're not fixed
    inside the review.
```

§ Task Working Directory Structure, first paragraph — Before:
```markdown
`{DOMAIN_PATH}` is the parent directory holding every feature's
`{TASK_PATH}` within one domain (e.g. all of a domain's `D0X-NN-*`
feature folders live directly under it). `_domain-manifest.md` (leading
underscore, sorts before every feature folder) is the only file that
lives directly under `{DOMAIN_PATH}` rather than inside a specific
feature's `{TASK_PATH}` — it's the output of
`workflow/0-domain-sequencing-prompt.md`, see step 3 of § Usage above.
```

After:
```markdown
*(Domain-grouped projects only — a project that doesn't group work by
domain has no `{DOMAIN_PATH}`; each `{TASK_PATH}` stands on its own.)*
`{DOMAIN_PATH}` is the parent directory holding every feature's
`{TASK_PATH}` within one domain (e.g. all of a domain's `D0X-NN-*`
feature folders live directly under it). `_domain-manifest.md` (output
of `workflow/0-domain-sequencing-prompt.md`, step 3 of § Usage) and
`_domain-closure-review.md` (output of
`workflow/7-domain-closure-prompt.md`, step 12) are the only files that
live directly under `{DOMAIN_PATH}` rather than inside a specific
feature's `{TASK_PATH}` — the leading underscore sorts them before
every feature folder.
```

### F. `workflow/5-testing/guidelines.md` — § Final Verification Before Considering Done

Add a checklist item after "Backward compatibility explicitly verified,
not just assumed":

```markdown
- [ ] If the change is cross-cutting (a shared middleware, trait, base
      class, or anything else applied across every route/module), the
      target repo's **entire** test suite has run clean — not only the
      tests for the feature that motivated it. A cross-cutting change
      can expose a latent bug in code this task never touched (origin:
      a rate-limiting middleware's post-response bookkeeping surfaced
      an unrelated service's missing transaction wrapper).
```

### G. `workflow/3-build/guidelines.md` — § What this phase is not

Append a paragraph:

```markdown
The same applies when a techplan or task file contradicts itself — most
often an abbreviated interface-contract snippet disagreeing with an
explicit "mirrors X" / "implement exactly like Y" instruction in the
same file or its parent techplan. If the difference is material
(behavior, the contract a caller sees, an authority/security boundary,
data shape), stop and ask — don't pick one. If it's mechanical only
(local naming, internal shape the contract doesn't expose), follow the
mirroring instruction and record the discrepancy in the build report.
Either way it's written down, never resolved silently. See
`workflow/README.md` § Phase Convergence.
```

## Rationale

**Why generic.** "Is the domain actually done, as a whole?" is a
question any project that plans by domain eventually faces, and the
failure shapes found in the koperasiqu audit — partially built
decomposed features, contract prose drift after a rename, unowned
cross-cutting tasks, testing docs lagging later endpoints — aren't tied
to that project's stack or naming. The checklist is written against
generic artifacts (a domain spec, a contract, a convention file, a
router listing), not koperasiqu files.

**Why conditional, and defined in one place.** This workspace is meant
to fit projects with different planning shapes. Domain grouping is one
of them, not a default. Defining the condition once in
`workflow/README.md` and pointing to it from the prompts, `AGENTS.md`,
and root `README.md` avoids restating it with drifting wording in four
places — the same single-source-of-truth discipline the workspace
applies elsewhere. Retrofitting 0026 in the same proposal keeps the
opening and closing brackets of a domain on the same footing.

**Why closure is a prompt, not a guidelines folder.** § Canonical Phase
Prompts makes a root `*-prompt.md` the invocation surface for a phase,
and 0026 already established that shape for the domain grain. A
separate `domain-closure/` folder would be structure without a second
file to justify it yet; one can be added if examples accumulate.

**Why items moved out of the staged draft.**
- *Full suite for cross-cutting changes* (draft item 7) → `5-testing/`,
  because it holds for any project.
- *Self-contradicting task file* (draft item 8) → `3-build/`, because
  it's a build-time situation in any project. The draft's rule ("the
  mirroring instruction always wins") was narrowed: material conflicts
  stop and ask, consistent with § Phase Convergence and the existing
  "What this phase is not" section — the techplan contract is what a
  lead approved, so build shouldn't silently override it.
- *Confirm before touching a fenced-adjacent path* (draft item 6) →
  dropped. What counts as fenced is owned by the target repo's own
  convention file, and `0-domain-sequencing-prompt.md` already defers
  to that declaration rather than defining it.
- The draft's koperasiqu-specific references (named individuals,
  "Golden Rules", `D0X-tasks.md`, the project's own report locations)
  were generalized.

**Not addressed.**
- Automating any checklist item.
- An `examples.md` for closure. The one real worked example (the
  koperasiqu `akun` audit) is project-specific and stays in that repo;
  a generic example can be added once a second domain has run this.

---

*After human review: update the Status above. If Accepted, merge into
the target documents and leave this proposal in place (don't delete
it) — it serves as this folder's changelog. See `proposals/README.md`
for the Protection Tier distinction and numbering convention.*
