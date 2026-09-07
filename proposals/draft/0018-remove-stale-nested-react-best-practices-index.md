# 0018 — Remove stale nested React best-practices index

Status: Accepted  
Date: 2026-09-07  
Protection Tier: general  
Triggered by: React best-practices routing audit performed while preparing proposals 0016–0017. `best-practices/react/index.md` was found to be a stale duplicate of the canonical workspace-wide `best-practices/index.md`, while `best-practices/AGENTS.md` explicitly instructs agents to start from the canonical `index.md`.

Target area: best-practices

Target file(s):

- Delete: `best-practices/react/index.md`

## Gap found

The workspace's routing model is intentionally centralized:

1. agents enter `best-practices/`;
2. `best-practices/AGENTS.md` instructs them to read `index.md` first;
3. the canonical `best-practices/index.md` contains the trigger-keyword table and Security Concern Map;
4. category guidance is opened only after a routing match.

`best-practices/react/index.md` breaks that model.

The nested file:

- declares its own location as `best-practices/index.md`, indicating it originated as a copied root index rather than a deliberately scoped React index;
- duplicates the global routing table instead of containing React-only routing;
- has drifted behind the canonical index as new guidance has been added;
- creates a second source that future agents or maintainers could accidentally update independently.

Keeping both files means every best-practice addition potentially has two indexes to synchronize, even though workspace governance names only one canonical entry point.

A category-local index would only be justified if the workspace explicitly adopted hierarchical routing and defined how the global index delegates to it. No such model currently exists.

## Proposed change

Delete:

```text
best-practices/react/index.md
```

Do not replace it with another React-local routing document.

`best-practices/index.md` remains the sole routing source for:

- trigger keywords;
- security-critical markers;
- summaries;
- Security Concern Map entries.

`best-practices/AGENTS.md` already points agents to that canonical entry point, so no governance change is required.

Before deletion, perform a repository-wide reference check for explicit links to `best-practices/react/index.md` or `react/index.md`.

If any functional reference exists, update it to:

```text
best-practices/index.md
```

as part of this proposal rather than retaining the duplicate file.

## Rationale

One routing source is easier for both humans and agents to keep correct.

The change does not alter any React engineering principle. It only removes an accidental parallel source of truth that conflicts with the workspace's existing progressive-disclosure architecture.

Deleting the duplicate is preferable to "bringing it up to date":

- synchronizing two copies solves the current drift but preserves the mechanism that caused it;
- a React-only sub-index would introduce a new hierarchical-routing architecture without a demonstrated need;
- the global index is still small enough to perform its intended trigger scan and already contains React rows alongside every other category.

This proposal is intentionally independent of proposals 0016 and 0017. It can be accepted and implemented regardless of whether either frontend-guidance proposal changes later.

---

After human review: update the Status above. If Accepted, delete the nested index and leave this proposal in place — it serves as the proposal log/changelog.