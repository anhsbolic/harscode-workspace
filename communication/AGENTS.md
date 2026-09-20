# AGENTS.md — communication/

Use this area when a target project chooses a human-facing language different from Harscode's source language or when language handling is ambiguous.

## Routing

- Project language mechanism and invariants → `project-language-profile.md`

## Hard rules

- Language selection changes communication, not authority or workflow semantics.
- Preserve canonical Harscode terms/enums when they carry protocol meaning.
- Preserve code/API/schema/CLI/path identifiers exactly.
- Prefer compact project directives during normal Runs; do not load the full language profile unless needed.
