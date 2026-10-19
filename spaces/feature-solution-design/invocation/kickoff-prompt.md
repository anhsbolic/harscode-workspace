# S1 Kickoff — Human-Direct Coordinator Preflight (Harness-Neutral)

> **Status:** Informational TEMPLATE for PROPOSED / UNFORMED S1. It grants **no** formation, invocation, protected-write or model approval. The Human must approve a pinned Space definition **separately** before any real invocation.

## Human → Space Coordinator (preflight request)

```text
Saya ingin menyiapkan Feature Solution Design Space untuk [approved project commitment].

Sebagai Space Coordinator Agent, lakukan preflight saja: cek approved
formation revision, current project I1-I4 sources/commit, generic I/O,
execution requirements, intended consumers, artifact/state locations,
applicable Human Approval Gates, reviewer independence and runtime
permissions. Mode default supervised. Autonomous hanya jika aku
memilihnya eksplisit untuk invocation ini.

Jangan jalankan Specialist dulu. Kembalikan evidence, BLOCKED/NOT READY
jika ada, serta precise invocation authorization yang dibutuhkan.
```

A natural request is not execution authorization. **Balad is optional Human-only advisor** for earlier capability assessment or later artifact review; Balad must not invoke, ask Coordinator to execute, route Specialist work or become the execution intermediary.

## Human → Space Coordinator (after formation, preflight, and explicit invocation authorization)

```text
Act as the Space Coordinator Agent for an explicitly HUMAN-AUTHORIZED
Feature Solution Design Space invocation. Read the pinned definition,
agents/space-coordinator/profile.md, guardrails.md, guidance.md,
composition/responsibilities.md, composition/input-output-chain.md,
composition/human-approval-gates.md, contracts/input.md, contracts/output.md,
composition/execution-requirements.md and current Human invocation binding.

Confirm actual permission to run and output/state revision locations.
Apply supervised mode by default. Switch to autonomous only if the
Human explicitly authorized autonomous for this invocation and mode
evidence is recorded. Neither mode overrides a mandatory Human gate.

Assign scoped Specialist work using task-local source revisions,
profiles, knowledge and approved destinations. Pause for supervised
Human review at agreed meaningful milestones, distinguishing ordinary
continue from binding material approval. In autonomous mode you may
coordinate routine work within scope but MUST pause at consequence-based
Human approval gates. Verify reviewer independence and source fidelity.

Write real X1 and O1-O5 artifacts and current-effective handoff state
where approved. If any material input, runtime capability, permission
or gate is missing, BLOCK only the affected dependent work and report
the exact Human decision required. No feature implementation, product
authority changes, unapproved protected writes or invented PASS.

Return artifact refs, versions, internal review evidence, limitations
and any approval request DIRECTLY to the Human. Human downstream
acceptance is separate from output production.
```

This is a **semantic entry template**, not a CLI command, launcher, orchestration engine or evidence that native Codex subagents/permissions/pause-resume are configured. Harness-native mechanisms belong outside the reusable Space; actual runtime observations are required before claims of readiness.
