# Local Environment Preparation — Working Guidance

> **Standing:** WORKING / RESEARCH-ONLY; Agent-owned guidance, not general project architecture or a setup-script catalog.
> **Entry:** [Standalone Agent contract](agent.md). Current project authority overrides generic preferences within applicable safety/Human gates.

## Practical reasoning loop

Use **discover → diagnose → recommend → ask → prepare (only if approved) → validate → report**, skipping stages that do not apply. This is a mental model, not a mandatory pipeline or state machine.

1. **Ground in current project authority.** Read root/scoped Agent instructions, owning stack/setup docs and executable files (e.g. manifests/lockfiles, Makefile, Compose, env examples, version files). Pin source revisions where possible. Distinguish accepted conventions, executable facts, optional capabilities, historical scaffolding and unresolved decisions.
2. **Identify the narrow readiness goal.** A frontend UI task, a backend DB integration test and an object-upload task need different prerequisites. Prefer what the intended consumer actually needs, not "run everything".
3. **Observe safely before proposing changes.** Check OS/runtime/tool availability and versions only through available **permitted non-mutating** inspection. Read command definitions before execution: package scripts, tests, generators and health checks can install, create caches, modify files, contact services or run arbitrary code. Do not access secret values just to establish presence.
4. **Diagnose with evidence tiers.** Separate repository-supported setup, actual machine observation, untested assumptions and failures. If no machine access exists, say so. Prefer a project-supported mechanism over inventing another.
5. **Recommend minimally and ask once per meaningful action scope.** Explain the observed gap, why it matters now, intended command/change and material side effects; ask for clear Human authorization. If the tool/runtime can affect more than approved, do not quietly take the larger action.
6. **Execute only approved scope; verify actual behavior.** Validate required service/process reachability, relevant dependency/tool compatibility and the intended workflow. Record failures and actual modifications; an install finishing is not integrated readiness. Report partial evidence rather than trying unrelated repairs.
7. **Handoff compactly.** State READY/PARTIAL/BLOCKED/UNVERIFIED for the precise activity and machine, supporting checks, residual issues and consumer recheck triggers. Persist if necessary only to an explicitly authorized, project-owned destination.

## Natural Human interactions

**Missing optional service:** "Untuk pekerjaan saat ini, MinIO [diperlukan/tidak diperlukan] berdasarkan [project source]. Saat ini [observasi]. Aku merekomendasikan [aksi]. Aksi ini akan [dampak]. Boleh aku lakukan?" Do not prepare MinIO just because a Compose service exists.

**Container runtime:** First inspect available permitted evidence or ask: "Project menyediakan Compose. Kamu memakai Docker atau Podman di mesin ini?" Adapt commands to the answer and current project config; do not rewrite scripts without need. Knowing the tool choice is not permission to start services.

**Permission refusal or change:** Human may decline, narrow scope or choose another project-compatible tool. Respect the decision and return useful diagnosis; do not try alternative execution paths to bypass it.

## Proportionate risk checks

- **Credentials:** verify required configuration presence without printing secret contents; never copy secrets into handoffs or commit them. Request authorization for creation, replacement or rotation.
- **Ports/exposure:** distinguish loopback-only assumptions from demonstrated binding. When local services use sample credentials, warn about possible network reachability before starting them if material.
- **Dependencies:** honor project lockfiles and package sources; flag materially floating versions, untrusted install hooks or version incompatibilities when they matter. No speculative full-stack upgrades.
- **Data and state:** treat migrations, resets, volume deletion, cleanup and service shutdown as potentially consequential; secure explicit scope and consider recovery before executing.
- **Portability:** prefer the existing OS/package manager/container runtime when compatible. Avoid devcontainers, Nix or additional layers unless they solve an observed requirement.
- **Verification:** source documentation is not a successful run; command success is not necessarily end-to-end readiness. Identify each unperformed check.

## Evidence quality examples

- "Compose defines PostgreSQL port 5435" = **repository configuration evidence**, not proof PostgreSQL is reachable on this machine.
- "Human reports using Podman" = **Human-provided environment fact** until verified where needed, not grounds for assuming Docker.
- "The relevant command completed and database connectivity passed on this machine" = **performed runtime evidence** for that bounded check, not universal project readiness.

A diagnosis can end without mutations and without READY. Do not introduce a multi-Agent review process, cross-project status store or ceremony without an observed failure that needs it.
