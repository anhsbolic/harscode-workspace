# Product Design Discussion Facilitation

Use this guidance when an AI agent is collaborating with a human on upstream product-design decisions.

This file defines **how to conduct the conversation**, not what the final design should be.

The goal is not to interview the human, collect preferences, or generate attractive options. The goal is to help the human progressively reduce ambiguity until durable product/design decisions are explicit enough to become authority.

## 1. Do not run product design as a questionnaire

Avoid long upfront surveys that ask the human to decide every design dimension before the conversation has established which dimensions actually matter.

Weak pattern:

```text
Choose:
- brand personality
- color
- typography
- card radius
- illustration style
- icon style
- motion style
- layout density
```

Stronger pattern:

```text
understand current truth
→ identify the highest-leverage unresolved question
→ ask a small number of questions
→ interpret the answer
→ challenge it where necessary
→ recommend a next direction
→ narrow the decision space
→ repeat
```

Questions should emerge from previous answers rather than from a static checklist.

## 2. Work one decision cluster at a time

Do not ask the human to resolve product posture, trust model, palette, typography, imagery, surfaces, motion, and implementation readiness in one pass.

A useful order often looks like:

```text
product truth / constraints
→ user hesitation / confidence gap
→ product posture
→ creative direction
→ representative proof
→ concrete visual system
→ authority / handoff
```

The exact sequence may vary, but later concrete decisions should not outrun unresolved upstream ones.

Rule of thumb:

> Ask only the next question whose answer materially changes the decision space.

## 3. Prefer questions with downstream consequences

Good questions constrain several later decisions at once.

Examples:

- What is the user most uncertain about before taking the core action?
- What must the product never imply unless it can prove it?
- Which part of the experience should carry optimism: imagery, copy, progress, motion, or something else?
- Which qualities must survive a future logo/name refresh?
- Where should public and authenticated surfaces intentionally differ in expressive intensity?

Lower-leverage questions such as exact radius preference or icon style usually belong later.

Before asking a question, test:

> If the human answers this, will it materially change what we recommend next?

If not, the question is probably premature or unnecessary.

## 4. Interpret the answer; do not merely record it

After the human answers, explain what that answer changes.

Weak:

> Got it. Noted.

Stronger:

> If distribution transparency is the main hesitation, then trust should be carried primarily by chronology, source attribution, and post-action evidence. A generic verification badge would not solve the actual confidence gap.

The agent should convert raw preference or product context into design implications.

Useful structure:

```text
What I heard
→ what it implies
→ what it rules out
→ what decision becomes possible next
```

## 5. Challenge assumptions proportionally

Do not default to agreement.

Test assumptions where the consequence matters, especially around:

- trust;
- persuasion;
- vulnerable users;
- money;
- safety;
- evidence/provenance;
- irreversible actions;
- durable brand identity;
- expensive-to-reverse implementation precedent.

But challenge should be proportional.

Do not invent objections merely to appear rigorous.

A useful pattern:

```text
Human proposes direction
→ identify strongest risk / contradiction
→ explain consequence
→ test whether the direction survives
→ carry it forward if it does
```

If an idea survives scrutiny, say so and move forward rather than reopening it repeatedly.

## 6. Recommend; do not only enumerate options

AI assistance is less useful when it dumps several plausible directions and refuses to synthesize.

When enough evidence exists:

1. present the meaningful alternatives;
2. explain the trade-offs;
3. state which direction you recommend carrying forward and why;
4. keep the human as final authority.

Example shape:

```text
A optimizes trust clarity but risks coldness.
B carries the desired optimism but risks overstating progress.
C is mature and restrained but risks feeling financial/institutional.

Given the current constraints, I recommend carrying B's emotional thesis forward with A's evidence discipline.
```

A recommendation is not a human override. It is a synthesis service.

## 7. Distinguish preference from constraint

Not every human statement has equal authority.

Try to distinguish:

```text
PRODUCT / DOMAIN CONSTRAINT
A fact the design must preserve.

DESIGN PRINCIPLE
A durable behavioral preference with downstream consequences.

WORKING PREFERENCE
A current direction worth testing.

TASTE REACTION
Useful feedback, but not yet a durable rule.
```

Do not promote an isolated taste reaction directly into a canonical design rule without checking whether it generalizes.

Conversely, do not treat a product/domain constraint as a visual preference that can be traded away.

## 8. Narrow the decision space progressively

A healthy discussion should reduce uncertainty over time.

Do not continually reopen earlier layers unless new evidence creates a material contradiction.

Example progression:

```text
OPEN: overall emotional posture
↓
LOCKED: calm optimism, no sadness-selling
OPEN: how optimism appears visually
↓
LOCKED: documentary imagery + evidence-led progress
OPEN: exact palette/type
↓
WORKING: candidate palette + font pairing
↓
PROVED: representative boards survive review
↓
LOCKED: concrete visual-system direction
```

This prevents endless circular exploration.

## 9. Maintain explicit decision state

Long design discussions accumulate context quickly.

Periodically summarize the state using categories such as:

```text
LOCKED
Human-approved or otherwise durable enough to treat as current authority.

WORKING
Strong candidate being tested; not yet authority.

OPEN
Material decision intentionally unresolved.

REJECTED / SUPERSEDED
Explored but no longer active.
```

Do this especially:

- after a major synthesis;
- before starting visual proofs;
- before concrete token decisions;
- before canonicalization;
- before engineering handoff.

Decision-state summaries are more useful than repeating the whole conversation.

## 10. Separate exploration language from authority language

Use language that reflects certainty.

During exploration:

- candidate;
- working direction;
- hypothesis;
- proof target;
- carry forward;
- still open.

After approval:

- approved;
- canonical;
- invariant;
- current authority.

Do not say a candidate is canonical simply because it is detailed.

## 11. Use examples and contrasts to clarify abstract choices

Humans often respond better to concrete contrasts than abstract scales.

Instead of:

> Should the brand be 7/10 expressive?

Prefer:

> Should public surfaces feel like a calm editorial publication while product surfaces become more operational, or should the same expressive treatment remain strong throughout?

When useful, explain why the distinction matters downstream.

## 12. Use visual generation as a test, not as premature solutioning

Do not generate moodboards, screens, or image studies simply because visual tools are available.

Generate visuals when there is a specific unresolved question that a visual proof can answer.

Examples:

- Does the palette remain mature when applied to dense product UI?
- Does the selected typography pairing retain readability in operational surfaces?
- Can provenance classes remain distinguishable without badge/color theatre?
- Does the public/product expressive split still feel like one brand?

Before generating a proof, state what would count as failure.

If no failure criterion exists, the proof is likely decorative.

## 13. Protect product truth during creative exploration

Creative exploration can move quickly. Product truth should not.

Whenever a promising direction implies a claim, ask:

```text
Who knows this?
Who reports it?
Is it verified?
Is it pending?
Can the product actually say this?
```

Do not let a compelling visual treatment normalize unsupported semantics.

## 14. Do not optimize prematurely for the current codebase

Upstream product design should not inherit stale implementation merely because rebuilding is inconvenient.

During design exploration, current implementation is context—not authority.

Questions such as component migration, token representation, library choices, and reset strategy belong at the design-to-engineering handoff unless implementation constraints materially change product behavior.

## 15. Know when to stop asking and start proving

Conversation alone eventually has diminishing returns.

Move from discussion to a proof when:

- the conceptual direction is coherent;
- remaining uncertainty is genuinely visual/spatial;
- alternatives can be evaluated by seeing them;
- further verbal questioning would repeat the same trade-off.

Move from proof back to discussion if the visual reveals a conceptual contradiction.

## 16. Human approval is a gate, not ceremony

When a decision creates durable product or brand precedent, explicitly ask for approval before promoting it to authority.

Typical gates include:

- product/design thesis;
- selected creative direction or synthesis;
- representative visual proof;
- concrete visual-system decisions;
- replacement of existing design authority;
- engineering-readiness declaration.

Do not bury approval inside a long response.

Make the decision being approved clear.

## 17. Do not force closure where ambiguity is healthy

Some decisions can remain OPEN without blocking implementation.

Examples may include:

- exact motion easing;
- final illustration production spec;
- optional secondary accent;
- future logo refinement.

If an unresolved decision does not affect the current implementation boundary, record it rather than inventing false precision.

## 18. Conversation anti-patterns

Avoid:

- giant questionnaires;
- asking preference questions before product questions;
- acknowledging without interpreting;
- listing options without recommendation;
- agreeing with every idea;
- adversarial contrarianism;
- silently turning taste into principle;
- reopening approved decisions without new evidence;
- generating visuals before knowing what they need to prove;
- treating generated copy/data as canonical product semantics;
- letting implementation convenience decide upstream direction;
- accumulating context without periodic decision-state summaries.

## Facilitation loop

A compact reusable loop:

```text
1. ORIENT
   What is already true / decided?

2. FIND THE LEVER
   What unresolved question has the largest downstream effect?

3. ASK
   Ask a small number of concrete questions.

4. INTERPRET
   Explain what the answer implies and what it rules out.

5. CHALLENGE
   Test the strongest assumption or risk where meaningful.

6. RECOMMEND
   When evidence is sufficient, propose a direction.

7. CONFIRM
   Let the human accept, reject, or refine it.

8. UPDATE STATE
   Mark LOCKED / WORKING / OPEN / REJECTED.

9. PROVE
   Use visual or structural proof when conversation alone is no longer enough.

10. PROMOTE
    Canonicalize only after the appropriate human gate.
```

The loop is adaptive, not a mandatory ten-step ceremony on every turn.

## Rule of thumbs

- Ask fewer, higher-leverage questions.
- Each question should change what happens next.
- Interpret answers instead of merely recording them.
- Challenge the premise before optimizing the solution when stakes justify it.
- Give a recommendation once the evidence supports one.
- Human authority does not require AI passivity.
- Earlier approved decisions should narrow later exploration.
- Keep explicit decision state in long discussions.
- Generate visuals to test hypotheses, not to create momentum.
- A useful design conversation should reduce ambiguity over time.
