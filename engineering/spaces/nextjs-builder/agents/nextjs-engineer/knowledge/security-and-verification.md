# Frontend Security, Testing SOP, and Evidence Limits

> **Applicable when:** source changes affect frontend trust boundaries, private data, scripts/HTML, auth flows, risky mutations, testing selection or completion claims. Follow effective project security and verification policy. This knowledge is not a global security audit or universal test mandate.

## Frontend security is bounded but real

Protect Server/Client separation: server-only secrets and privileged dependencies must not be imported into client-reachable code. Keep private data from unnecessary HTML/props/hydration, URLs, browser storage, analytics, error displays and logs; CSS masking does not prevent exposure if the original value was already sent to the browser. For user-provided rich text, select project-approved safe rendering/sanitization; ordinary React escaping must not be bypassed casually.

Follow actual project session transport. Do **not** assume browser-readable bearer JWT, refresh-on-401, CSRF token header or cookie settings unless effective authority says so. State-changing requests and cookies need project-approved CSRF/Origin and session behavior; neither CORS nor a hidden button proves authorization. For sensitive operations, service/backend must enforce actor/resource/action grants—frontend gate is UX only. Account change invalidates relevant private data and late responses.

Review dependencies and exposure only where affected risk warrants it. Security-critical unknowns beyond Engineer/Reviewer competence should be escalated with concrete consequences and proposed specialist review, not blanket “secure” claims.

## SOP first, risk-aware methods second

First identify whether project testing is manual-only, automated, mixed or unspecified; who owns QA; what is forbidden; what tools and environments are authorized. If automation is explicitly prohibited, don't write or run it. If the project leaves methods unspecified, choose the smallest permitted evidence suitable for changed outcomes: source/static check, behavior assertion, browser rendering/keyboard observation, integration exercise or downstream manual QA.

A material high-risk case poorly covered by allowed methods warrants a **scoped Human exception request**: failure mode, proposed smallest added test, data/tools/side effects, benefit, fallback and residual risk. Never run a forbidden check before approval or treat rejection as successful verification. Legal/security protections remain subject to appropriate higher-priority authority.

Test at the boundary that could actually fail. Static checks find syntax/type issues; focused component tests can prove selected interactions; network-boundary mocks can exercise frontend HTTP consumption, whereas mocking the whole hook often hides request/cache bugs; real integration needs a real provider. Assertions should target observable actions, errors and forbidden effects rather than incidental classes or call counts. Testing utilities may be unavailable and no test script is mandatory merely because it exists.

## Reliable evidence, not rituals

Record the exact code/contract revision, method, executed command or manual observation, provider identity (mock/real), relevant conditions, result and known limits. An executable returning zero tests is not evidence of behavior; a build pass is not visual confirmation. Material UI may require rendered observation, subject to actual SOP and assigned Human QA owner. An independent review must use real separate context and access where required.

Do not invent universal coverage floors, mandatory Playwright, complete screenshot suites, automatic infrastructure install or new CI. Distinguish `IMPLEMENTED`, `TESTED`, `RENDER-VERIFIED`, `REAL-API-INTEGRATED`, `SECURITY-ASSESSED`, `HUMAN-ACCEPTED` and `DELIVERED`. Leave external/manual-owned acceptance pending when it has not happened.
