# testing-automation-boundary.md

**Location:** `react/testing-automation-boundary.md`

**Principle**
The same lesson this workspace already learned the hard way for techplan review (`workflow/2-techplan/retro.md` — a rule restated in prose gets skipped, twice, regardless of model or person; converting it into an explicit mechanical check is what actually held) applies to frontend correctness/security checklist items too. If a checklist item's violation can be pattern-matched from the AST (a banned function call, a banned prop usage, a banned identifier appearing in JSX) it belongs in a lint rule, not in a human reviewer's memory. The boundary: **grep/AST-pattern-matchable → automate. Requires understanding intent (does this test actually prove anything, does this UX decision feel right) → stays manual**, and specifically stays at the human checkpoint / Finalize smoke-test stage this workspace's workflow already defines — this file doesn't add a new manual stage, it narrows what the existing one needs to spend attention on.

**Bad**
```md
<!-- checklist item, sits in a review guideline as prose, relies on the -->
<!-- reviewer remembering to check it on every PR -->
- [ ] No component calls `fetch` directly outside `lib/api/`
```
Same failure shape as R18 / severity-leak in the techplan driving story: correct advice, restated instead of enforced, and it recurs.

**Good**
```js
// eslint.config.mjs
export default [
  {
    // default: raw fetch is banned everywhere
    rules: {
      'no-restricted-globals': ['error', {
        name: 'fetch',
        message: 'Use the centralized apiFetch client from lib/api/, not raw fetch(). See react/api-client-centralization.md.',
      }],
    },
  },
  {
    // the one place raw fetch is allowed: the client itself
    files: ['lib/api/client.ts'],
    rules: { 'no-restricted-globals': 'off' },
  },
];
```
```js
// dangerouslySetInnerHTML: banned by default (react/no-danger), only escapable
// with an explicit disable comment — forces the exception to be visible and
// reviewable, rather than silently allowed everywhere
{
  rules: {
    'react/no-danger': 'error',
  },
}
// usage now requires an explicit, reviewable justification at the call site:
// eslint-disable-next-line react/no-danger -- sanitized via DOMPurify.sanitize, see xss-and-content-sanitization.md
<div dangerouslySetInnerHTML={{ __html: DOMPurify.sanitize(narrative) }} />
```
```js
// custom rule sketch: flag `error.message`/`err.toString()` used directly
// inside JSX — the exact shape that leaks raw backend error text to the user
{
  rules: {
    'no-restricted-syntax': ['error', {
      selector: 'JSXExpressionContainer > MemberExpression[property.name="message"]',
      message: 'Do not render error.message directly — use a generic, user-facing message. See react/loading-empty-error-state-conventions.md.',
    }],
  },
}
```

**Checklist — decision table for any new checklist item found in this workspace's other `react/` files**

| Question | If yes | If no |
|---|---|---|
| Can the violation be described as an AST/text pattern (banned call, banned prop, banned identifier)? | Automate — lint rule or `tsc` | Stays manual |
| Does checking it require reading what the code is trying to prove (test intent, UX judgment, visual match to a reference)? | Stays manual | — |
| Is it a runtime/rendered-DOM property (contrast, focus order, ARIA tree)? | Automate the mechanical subset (`jest-axe`/`@axe-core/react`) — but keep a manual pass too, automated a11y tooling catches roughly a third to half of real issues, not all | — |

- [ ] Every "no raw X" / "always do Y" item added to any `react/` best-practice file in this workspace is checked against the table above before being left as prose-only
- [ ] Lint rules that ban a pattern by default include an explicit, reviewable escape hatch (a disable comment with justification), not a silent allowlist buried in config — makes exceptions visible at review time instead of invisible
- [ ] Automated a11y checks (`jest-axe`) are treated as a floor, not a substitute for a manual keyboard/screen-reader pass — this workspace's Finalize/smoke-test stage remains where that manual pass happens, not a new stage
- [ ] "Gates aren't gamed" (assertions actually test something, thresholds not quietly lowered) stays a human-checkpoint item regardless of how much lint/type coverage exists — no lint rule substitutes for reading whether a test's mock is at the right layer (see `component-test-mocking-discipline.md`)