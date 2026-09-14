# harness-optimization/

## What this is

A third pillar, sibling to `workflow/` and `best-practices/`:

- `workflow/` — **what** to do, by phase (process knowledge)
- `best-practices/` — **what** is correct, by technology (domain knowledge)
- `harness-optimization/` — **how** a specific agent harness (Claude Code,
  Codex, or others added later) executes and enforces the two above

## The one rule that keeps this pillar honest

**Translation only. Never policy.**

Every file in this tree answers "how do I express an already-decided rule in
this harness's native mechanism?" — never "what should the rule be?"

If a harness translation needs a new lifecycle rule, threshold, exception, or
correctness rule that does not already exist in `workflow/` or
`best-practices/`, change the owning pillar first through its normal governance.
The harness translation follows afterward.

Context/session policy is owned by `workflow/context-management.md`; harness
session, subagent, skill, or command mechanics translate that policy rather than
creating a second lifecycle.

## Structure

```text
harness-optimization/
├── README.md
├── AGENTS.md
├── token-optimization.md
├── <harness-name>/
│   ├── README.md
│   ├── token-optimization.md   # when applicable
│   └── <track>/                # only when translation genuinely differs
```

A `<harness-name>/<track>/` split is used only when the harness translation
differs meaningfully by track. Track-specific application/domain knowledge is
not enough reason to duplicate translation files.

## Governance level

Same protection posture as `best-practices/`: **agent-protected,
proposal-gated** on ordinary work. See `AGENTS.md` and root
`proposals/README.md`.

This stricter bar is deliberate because content here can directly change tool,
write, network, session, or instruction behavior. A wrong translation can
silently under-fence or over-fence an agent.

## Harness freshness disclaimer

Harness mechanics change quickly. Every `<harness-name>/README.md` must state:

```text
Effective as of: <harness name + version/date>
Last verified: <date>
Re-verify: recommended every ~2-3 months, or after a material harness change
```

Past-due capability/mechanic claims are hypotheses until re-verified. Stable
Harscode policy does not become stale merely because one harness translation
does.

## Project-agnostic by construction

Nothing here should hardcode a target project's feature, domain, path list, or
business rule. Actual project harness instances/configuration live in the
target repo or user configuration; this tree documents reusable translation
patterns.
