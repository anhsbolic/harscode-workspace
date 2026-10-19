# AGENTS.md — space-formation/ (Experimental)

Read [README.md](README.md) to establish scope and ownership. Use this area when **Anhar and ChatGPT are developing/revising a reusable Space capability**, not for an ordinary Balad project intake.

## Route by concern

- Analyze Balad's Formation Request; challenge capability fit and generalization → [formation-guidance.md](formation-guidance.md).
- Design strict generic I/O, invocation binding, handoff conformance and readiness/assurance → [contract-and-readiness.md](contract-and-readiness.md).
- For shared Harscode guidance edits, follow root [AUTHORING.md](../AUTHORING.md) and the current branch's applicable governance. The target project's own instructions/authority remain binding.

## Hard rules

- **Human + ChatGPT owns formation design for the current research pilot. Balad stops at a Formation Request.** Only Anhar approves formation and material reusable-contract decisions.
- Start from a **real project capability gap**, not an attractive role label or a predesigned workflow. Check existing, actually formed definitions before deciding reuse/adapt/new formation.
- Keep **reusable Space contracts** independent of project-specific **invocation bindings**. Both generic and bound inter-Space handoffs must be compatible; unknown is not PASS.
- One Space has a coherent external production responsibility. Define a **Human-invoked Space Coordinator Agent role**, bounded internal Specialist responsibilities and evidence ownership without presuming a separate native process for every role. Execution mode is **supervised by default**; autonomous must be explicitly chosen by the Human for a specific authorized invocation.
- Explicitly define the received-input preconditions, produced-output contract, truthful failure/partial/unknown states, evidence expectations and authority boundary. Never invent tool access or independence evidence.
- During formation, identify **consequence-based Human Approval Gates**: triggering decision/artifact, evidence and pinned revision, Human authority, blocked downstream action, valid resume condition and material-change invalidation. Gates apply in **both supervised and autonomous modes**; do not require Human approval at every Specialist handoff by default.
- Balad is advisory-only. It must **not invoke, request dispatch from, coordinate with or resume a Space Coordinator Agent**. Human directly invokes the Coordinator; formation, invocation, protected-write approval and final acceptance remain separate.
- Material security/privileged-write safeguards, Human approval and the first invocation stay separate from declarative formation; do not silently perform project engineering or build a runtime engine as "formation".
- Real execution may propose contract/Agent/knowledge improvements. **Do not silently mutate a reusable definition or invalidate active bindings**; assess impacted consumers and obtain Human approval.
- Remain EXPERIMENTAL on this research branch. Do not treat a created definition as proven or promote it to operational `main` without separate authority.
