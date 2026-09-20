# Project Language Profile

Harscode source guidance is written in English, but target projects may choose a different human-facing communication language.

The selected project language changes communication only. It MUST NOT change authority, workflow semantics, protocol vocabulary, identifiers, code symbols, API/schema fields, or externally defined contract terms.

## Project profile

A target project MAY define:

- default human-facing language;
- handling of technical English terminology;
- canonical Harscode terms that remain untranslated;
- protocol enum/value handling;
- handling of exact authority quotations;
- handling of code/API/schema/CLI/path identifiers.

## Required invariants

Project language selection MUST preserve:

- canonical Harscode object names when they carry protocol meaning;
- exact protocol enum/status/type values;
- Work Unit / Run identifiers;
- file paths, branch names, commit SHAs, CLI commands;
- code symbols, API fields, schema names, and externally defined identifiers;
- exact source wording when wording itself is authoritative or materially relevant.

## Human-facing prose

Human-facing explanation, rationale, handoff prose, report narrative, Finding/Decision descriptions, and Control Surface prose MAY follow the selected project language.

A project using a non-English language SHOULD prefer natural prose in that language while preserving canonical English technical terms when translation would reduce precision or create terminology drift.

Example:

```text
Status: ACTIVE
Scheduling: RUNNING
Role: Explorer

Tujuan Run:
Menghasilkan evidence yang cukup untuk memahami...
```

Do not translate canonical enum values into localized synonyms such as `AKTIF`, `TERBLOKIR`, or `BERJALAN`.

## Routing and context economy

The full profile is WARM guidance. Normal Runs should receive only the compact project directive needed for execution.

Preferred flow:

```text
target-project router/instructions
→ compact language directive
→ full language profile only when language handling is ambiguous
```

Do not require every agent to reread this file in full merely because the project uses a non-English language.

## Orchestrated Runs

When Orchestrator Protocol v0.1 prepares a Run invocation, the project language profile is an optional routing input.

The invocation SHOULD carry a compact directive such as:

```text
Human-facing prose: Bahasa Indonesia.
Preserve canonical Harscode terms/enums and code/API/schema identifiers in English.
```

The Orchestrator must not translate canonical protocol semantics while generating the invocation.

## Project ownership

Harscode defines this mechanism only.

The target project owns the actual language choice and any project-specific terminology preference.
