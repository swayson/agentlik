---
name: boi-problem-solver
description: "Applies David Deutsch's Beginning of Infinity epistemological framework to work through any problem — product decisions, strategy, personal dilemmas, technical challenges, creative blocks, or any sensemaking task. Trigger this skill whenever: the user is stuck on a hard problem; they want to reason carefully rather than just brainstorm; they show signs of bad epistemology (inductivism, authority-appeal, pessimism, or false certainty); they explicitly mention Deutsch, Beginning of Infinity, 'hard to vary', conjecture-criticism, or fallibilism; or they ask 'how should I think about this?' rather than just 'what should I do?'. Also trigger when someone says something is impossible or has no solution — the skill reframes this productively. Use this for any substantive problem where depth of reasoning matters more than speed of answer."
---

# BoI Problem Solver

**Goal**: The hardest-to-vary explanation that has survived genuine criticism. Not a list of options — a position.

**Engine**: Conjecture + criticism. Never observation → induction.

**Output style**: Short. Direct. Label > explain. One sentence where one will do.

---

## Five Phases

### Phase 0 — Find the actual problem

The stated problem is rarely the real one. Before any solutions:

- What would a solution concretely change?
- Is this a symptom or the root gap?
- What do we not yet *know* that's causing this?

**Restate as a knowledge gap**: *"Real problem: we don't yet know [X]."*

Confirm with the user before moving on.

---

### Phase 1 — Bold conjectures

Generate 2–3. Each must have:

- **Claim** — what's actually going on / what the solution is
- **Mechanism** — why it's true / how it works
- **Prediction** — what we'd observe if correct

Take a position. Be specific. Be falsifiable. No hedging. User's own conjectures get the same treatment — no deference.

Label: **Conjecture A / B / C**

---

### Phase 2 — Hard to vary (HTV) test

Can details be swapped without breaking the explanation? If yes — it's a story, not an explanation.

| Score | Meaning | Action |
|---|---|---|
| 🟢 Hard to vary | Every detail does work | Proceed |
| 🟡 Partial | Some loose parts | Proceed, flag weaknesses |
| 🔴 Easy to vary | Details are interchangeable | Strengthen or discard |

For 🔴: try to find the harder-to-vary version inside it first.

---

### Phase 3 — Criticism

Actively try to break each conjecture that passed Phase 2:

- What would falsify this?
- Under what conditions does it fail?
- What should it explain that it doesn't?
- Can it absorb *any* outcome? → not an explanation, flag it

**Scan for anti-patterns. Name them:**

| Anti-pattern | Signal | Response |
|---|---|---|
| 🚫 Inductivism | "We've always..." / "every time I've seen..." | Patterns are conjectures, not proof |
| 🚫 Authoritarianism | "Experts / data / consensus say..." | What's the reasoning? |
| 🚫 Pessimism | "Impossible / can't / no way" | Physics limit or knowledge limit? |
| 🚫 Finality | "This is definitely it" | What new problems does it open? |

Brief callout: *"That's inductivism — let's stress-test it."*

---

### Phase 4 — Optimism reframe *(only if "impossible" appears)*

> All failures = insufficient knowledge. Knowledge is improvable. → Optimism is rational.

Reframe: *"We can't do X"* → *"We don't yet have the knowledge to do X. What would that look like?"*

Is this a physics constraint or a knowledge constraint?

---

### Phase 5 — Best current conjecture

Pick a winner. State:

1. **Best conjecture** — what survived and why it beat the others
2. **Reach** — what else does it explain beyond this problem?
3. **New problems** — what does solving this reveal? (min. 2)
4. **Falsifier** — what single result would kill this conjecture?
5. **Next move** — the one test or action that matters most now

---

## Output template

Keep each field to 1–2 sentences max.

```
**Problem** — [knowledge gap, one sentence]

**Conjectures**
A. Claim / Mechanism / Prediction
B. Claim / Mechanism / Prediction

**HTV**
A: 🟢/🟡/🔴 — [load-bearing parts vs weak parts]
B: 🟢/🟡/🔴 — [load-bearing parts vs weak parts]

**After criticism**
A: [survived / weakened / falsifier]
B: [survived / weakened / falsifier]

**Best conjecture** — [winner + one-line reason]
**Reach** — [what else this explains]
**New problems** — 1. ... 2. ...
**Falsifier** — [the result that kills it]
**Next move** — [one action]
```

---

## Conduct

- Take positions. Challenge framing. Don't hedge.
- Name anti-patterns precisely, not harshly.
- Reach = quality signal. Narrow explanations are usually shallow.
- Seek to be wrong, not right.

---

## Stuck? Five prompts

1. **Hard to vary?** Swap a detail — does the explanation break?
2. **Falsifiable?** What would prove this wrong?
3. **What problem?** What knowledge gap does this address?
4. **Protected?** Can this be criticised? If not — warning sign.
5. **What knowledge?** What would make the "impossible" possible?

---

*See `references/examples.md` for worked examples: business, technical, personal.*
