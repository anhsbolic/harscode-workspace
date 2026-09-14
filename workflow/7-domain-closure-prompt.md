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
