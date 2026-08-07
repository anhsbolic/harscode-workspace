# Sniffing Checklist

Run these five lenses on every area explored in Stage 2 — not as a
separate pass at the end, but while exploring that area. The goal is to
surface things that would otherwise only be discovered during
implementation or, worse, in production.

## 1. Risk

What could break, and how far does it reach? Not just "this function
could fail" but who/what depends on it — other services, other product
types, existing data, existing clients.

## 2. Edge Cases

Null, empty, boundary values, concurrent access, partial state — for
*this specific area*, not a generic checklist. What's the actual
plausible edge case here, given what this code does?

## 3. Miscontext

Does the PRD/ticket assume this area behaves a certain way, when the
actual code does something different? This is the gap between "what the
requirement author believes exists" and "what actually exists" — often
invisible until someone reads the code directly.

## 4. Misleading Signals

Something that *looks* like it supports the requirement but doesn't
actually function yet. Example (real, from GMRT-50941): a `Registrar`
field existed in the API client model and looked "already there" — but
it was never mapped through to the domain model, so nothing downstream
actually used it. Surface-level presence isn't the same as working
end-to-end.

## 5. Inconsistency

Contradictions between two parts of the codebase, or between
documentation/ticket and what the code actually does. Note these
explicitly rather than silently picking whichever one seems more
authoritative — that judgment call belongs to Stage 3 or to a human, not
buried in Stage 2 output.

## How to Report Findings

Keep findings attached to the area they came from, not collected into a
separate "risks" document — the context of *where* something was found
matters for whoever reads it next. A one-line flag is enough at this
stage; developing it into a full risk analysis with mitigation options
is Stage 3 work.