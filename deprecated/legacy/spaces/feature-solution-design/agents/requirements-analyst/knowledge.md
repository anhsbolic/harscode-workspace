# Requirements Analyst — Agent-Owned Knowledge

**Scope:** Only knowledge needed to convert authoritative requirements into a faithful production map. This is working technique, not a second product/spec authority.

## Traceability and source classification

- Prefer source → requirement/invariant → responsible outcome → verification obligation. An approved behavior may map to multiple experience/engineering outcomes; never assume one-to-one files/phases.
- Separate (a) authoritative meaning, (b) directly derived obligation, (c) delegated implementation choice, (d) open Human-owned decision, and (e) supporting evidence/history.
- A user-facing trust or provenance claim needs both positive and negative requirements (e.g. "what it guarantees" and "what it does not guarantee").
- Preserve failure/conflict/incomplete pathways; a map of happy paths is structurally incomplete for consequential actions.

## Information-quality checks

- Cite the exact section/requirement ID and revision, not only filename/title.
- Compare requirements with scope exclusions; do not reintroduce intentionally excluded work as a prerequisite.
- When two apparent requirements conflict, locate actual authority and version before proposing reconciliation.
- Distinguish "unknown mechanism" (normal design freedom) from "unknown product semantics" (potential blocker).

## Local trigger discipline

Read when extracting approved behavior/acceptance. Do not load the global `best-practices/index.md` by default. Project's root/scoped instructions and explicit security permission boundaries remain directly binding; this file cannot override them.
