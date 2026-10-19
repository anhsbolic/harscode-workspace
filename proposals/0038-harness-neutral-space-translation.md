# Make harness translations consume approved Space execution requirements

**Status:** Proposed
**Date:** 2026-10-19
**Protection Tier:** general
**Triggered by:** The first Feature Solution Design Space candidate embedded `spaces/feature-solution-design/harness/codex.md`, conflating reusable capability requirements with one pilot harness's mechanics. Human directed correction: Spaces must be harness-agnostic, with harness optimization owned by Harscode workspace.
**Target area:** harness-optimization
**Target file(s):**
- `harness-optimization/AGENTS.md` — add approved Space definitions as valid translation sources and update scoped routing.
- `harness-optimization/README.md` — extend the translation-only source boundary to formed/approved Space execution requirements and Specialist packages.
- `harness-optimization/codex/README.md` — permit on-demand translation of harness-neutral Space/Agent requirements to supported Codex mechanisms without prescribing an S1-specific launcher.

## Gap found

The existing translation-only guidance says it translates only `workflow/` or `best-practices/`. That wording predates formed Space/Agent capability contracts. S1 now owns only harness-neutral [execution requirements](../spaces/feature-solution-design/composition/execution-requirements.md) such as original-source access, bounded writes, scoped Agent knowledge, independent reviewer context and versioned handoff; the earlier Codex-specific file is being removed from S1.

Without an explicit approved Harscode-level source route, a future operator may either put Codex mechanics back inside Space definitions or attempt to use an unreviewed harness adapter as independent policy. Neither is appropriate. This proposal is **not** approval to form/invoke S1 or confirmation that a Codex runtime supports the stated requirements.

## Proposed change (exact intended text)

### `harness-optimization/AGENTS.md`

Replace:

```text
- **Translation only. Never policy.** The underlying rule must already exist in `workflow/` or `best-practices/`.
```

with:

```text
- **Translation only. Never policy.** The underlying requirement must already exist in the applicable authoritative Harscode source: `workflow/`, `best-practices/`, or an explicitly approved reusable Space definition under `spaces/`. Research candidates may be assessed experimentally within a separately authorized pilot; their unapproved content is not operational Harscode policy.
```

Add under Routing:

```text
- Reusable Space / Specialist execution requirements → inspect the selected, pinned and approved `spaces/<space>/` definition and its harness-neutral execution requirements; then route to the selected harness's relevant mechanism docs. Do not make a harness adapter the Space policy owner.
```

### `harness-optimization/README.md`

Replace the introductory summary:

```text
- `harness-optimization/` — **how** a specific agent harness (Claude Code,
  Codex, OpenCode CLI, or others added later) executes and enforces the two above
```

with:

```text
- `spaces/` — approved reusable capability contracts, internal Specialist responsibilities, Agent-owned knowledge, and harness-neutral execution requirements (currently experimental when not formed).
- `harness-optimization/` — **how** a particular harness expresses and enforces applicable requirements from their owning sources without changing them.
```

Replace:

```text
If writing a file here requires inventing a new rule, a new threshold, or a
new exception that doesn't already exist in `workflow/` or
`best-practices/`, that's a signal the content belongs in one of those two
pillars first, as its own proposal.
```

with:

```text
If writing a file here requires inventing a new rule, threshold or exception that does not exist in the relevant owning Harscode source (such as `workflow/`, `best-practices/` or an approved `spaces/` definition), return the question to that owner first rather than creating a second policy through a harness adapter.
```

Add after the first translation-only explanation:

```text
## Reusable Space boundary

A reusable Space owns WHAT it must produce, WHAT capabilities and isolation/permissions its Specialists require, and HOW it reports evidence truthfully. This area owns harness-specific translation only after checking actual supported mechanisms; invocation-owned model/effort, permissions, target paths and tested runtime observations stay in user/project binding. An unformed research candidate can guide a scoped experiment, but cannot silently become operational policy or a guaranteed launcher.
```

### `harness-optimization/codex/README.md`

Replace:

```text
Portable rules live in `workflow/` and `best-practices/`. This directory maps them onto Codex-native instruction/session/skill/sandbox behavior.
```

with:

```text
Portable rules and capability requirements live in their owning Harscode authority (e.g. `workflow/`, `best-practices/`, and approved reusable `spaces/`). This directory translates only the applicable ones into Codex-native instruction/session/skill/sandbox behavior; a proposed Space definition is not a runtime-ready Agent config.
```

Add after `## Canonical phase prompts` (without changing phase prompts):

```text
## Space and Specialist usage (when triggered)

For an approved/research-authorized Space, read its pinned generic I/O and harness-neutral execution requirements first. Map the actual requirements to the verified, currently available Codex instruction-loading, context/session isolation, permission/sandbox and observability mechanisms documented here. Keep role-specific knowledge with the Space's Specialist package; do not copy it into this harness directory. Bind actual project/model/effort settings in local authorized runtime configuration, not the Space contract or reusable Codex guidance.

A declared Agent profile does not configure or launch a native Codex subagent. If any material Space execution requirement cannot be verified in this Codex version or permission scope, report NOT READY; do not weaken the Space contract or claim independence from a role label. No default backend/frontend/S1 adapter or dispatcher is imposed.
```

## Rationale and tradeoffs

The concrete failure is in reusable S1: `harness/codex.md` duplicated both generic execution requirements and pilot-specific Codex steps inside the Space. Correcting S1 now is allowed as experimental formation work. Correcting **protected shared harness guidance** is a separate general-tier proposal, not an ordinary direct edit. A minimal routing extension suffices; no global schema, adapter registry or immediate new per-harness file is justified until real use demonstrates a need.

Space-specific capability requirements remain generic enough to be translated to another eligible harness. Codex is **only the chosen prospective first C1 test harness**, not part of S1 identity. Runtime feature support, independent Agent context and security permissions must be verified at first-use preflight.

## Acceptance / rollout boundary

- Human reviews this exact proposal and records **Accepted** or requested revision before editing `harness-optimization/`.
- After acceptance, apply only the three scoped protected-file changes above; preserve existing workflow and best-practices routing, then inspect links and effective text.
- No change to `main`, Kencleng code, actual model inventory, invocation permissions, or formation approval is implied.
