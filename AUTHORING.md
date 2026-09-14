# Harscode Guidance Authoring Standard

Use this file when creating or editing Harscode guidance itself. It is an authoring standard, **not** a runtime document every project agent must read.

## Goal

Optimize for **correctness density**: the smallest amount of guidance that preserves the decisions, boundaries, and evidence an agent needs to act correctly.

Shorter is not automatically better. A cohesive 300-line contract can be safer than five fragments that require the reader to reconstruct hidden dependencies. Conversely, a long file that mixes unrelated concerns forces every reader to pay for content they do not need.

## Writing rules

1. **Be direct.** State the rule, decision, or routing instruction first. Remove greetings, filler, repeated conclusions, generic motivation, and prose that does not change behavior.
2. **One semantic source of truth.** Link to an existing authority instead of restating it. A short routing sentence is fine; a second hand-maintained copy is not.
3. **Rationale earns its space.** Keep rationale when it prevents a likely misinterpretation, records a non-obvious trade-off, or explains a proven failure mode. Historical narrative that no longer changes execution belongs in history/retro/proposals.
4. **Separate runtime rules from examples/history.** Examples calibrate; retros explain how a rule was learned. Neither should become mandatory runtime context when the stable rule already captures the lesson.
5. **Use addressable headings.** A reader should be able to locate the relevant concern by heading or targeted search without absorbing the entire file.
6. **Prefer explicit triggers.** Conditional guidance should say when to open/use it. Avoid instructions such as “read everything in this folder.”
7. **Preserve executability.** Do not remove behavior, ownership, interface, security/authority, risk, or verification detail merely to make a document shorter.
8. **Avoid narration inside artifacts.** Artifacts record decisions/evidence, not the model's conversational journey to reach them.

## Context temperature

Classify guidance by how often it belongs in an active execution context:

- **HOT** — small routing/hard-rule surfaces or phase authority needed on most runs. Keep concise and stable.
- **WARM** — substantive guidance opened when a known trigger applies. It may be detailed, but should be independently addressable.
- **COLD** — examples, retrospectives, proposal history, old designs, and deep rationale. It may be long; do not make it a default runtime read.

Temperature describes loading behavior, not importance. A COLD historical record can be important without belonging in every agent context.

## When to split a document

Do **not** split solely because a file is long. Split when distinct topics have distinct triggers/readers and can be consumed independently without forcing readers to reconstruct a hidden contract.

For HOT/WARM runtime guidance, roughly **250–300 lines or 16–20 KB** is a soft review signal: ask whether the file still represents one cohesive concern. It is not a hard limit and must never justify removing required detail.

Useful split signals:

- readers repeatedly need only one subsection;
- unrelated concerns have independent change cadence;
- the file mixes rules with long examples/history;
- a routing/index layer can reliably direct readers to separate authorities.

Bad split signal:

- “this file crossed N lines” while every section is required together to understand one contract.

## Clue maps and indexes

A clue map routes; it does not summarize authority into a second copy.

Good:

```text
file upload → best-practices/go/file-upload-handling.md
trigger: multipart/file-upload boundary
```

Bad:

```text
file upload → a paragraph re-explaining every rule from the target file
```

If the clue map becomes large, improve its searchability or split routing by independently useful concern. Do not require agents to read the whole map as prose before they know what they need.

## Review check for guidance edits

Before finalizing a Harscode guidance change, ask:

- Does this introduce a second source of truth?
- Is every mandatory read necessary for the active decision?
- Could examples/history become conditional instead?
- Did brevity remove an execution-critical detail?
- Can the intended reader find the relevant section without scanning unrelated material?
- Does the change preserve current correctness while reducing ambiguity or repeated context?
