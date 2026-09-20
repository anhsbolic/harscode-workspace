# Project Communication Language

Harscode supports target projects that use a human-facing communication language different from Harscode's source language.

The project communication setting is intentionally small.

## Project setting

A target project MAY provide only these two values:

1. `COMMUNICATION_LANGUAGE` — the human-facing language to use.
2. `COMMUNICATION_PROFILE_PATH` — optional path to additional project-specific communication guidance.

Example with an additional profile:

```text
COMMUNICATION_LANGUAGE = Bahasa Indonesia
COMMUNICATION_PROFILE_PATH = docs/project/communication-profile.md
```

Example without an additional profile:

```text
COMMUNICATION_LANGUAGE = English
COMMUNICATION_PROFILE_PATH = none
```

The profile path is optional. A project MUST NOT be required to create a dedicated communication-profile document merely to use Harscode.

## Semantics

`COMMUNICATION_LANGUAGE` affects human-facing prose.

It MUST NOT change:

- Harscode protocol semantics;
- canonical protocol enum/status/type values;
- Work Unit / Run identifiers;
- code symbols;
- API fields;
- schema names;
- CLI commands;
- file paths;
- branch names;
- commit SHAs;
- externally defined identifiers or contract terms.

When translation would reduce precision, canonical Harscode and technical terms MAY remain in English.

## Optional profile

If `COMMUNICATION_PROFILE_PATH` is present, load it only when the Run needs the additional communication rules it contains.

If it is absent or `none`, do not synthesize a profile and do not treat the absence as a missing dependency.

## Orchestrated Runs

The Orchestrator MAY carry these values into a Run invocation:

```text
COMMUNICATION_LANGUAGE = <project-selected language>
COMMUNICATION_PROFILE_PATH = <path or none>
```

Normal Runs should receive only the communication context needed for execution.
