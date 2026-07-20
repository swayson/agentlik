---
name: causal-reasoning-engine
description: >
  A structured reasoning scaffold that applies causal logic (Pearl's ladder) at the prompt
  level. Apply whenever the question concerns cause, effect, or counterfactual — i.e.,
  whenever a wrong answer would come from confusing correlation with causation. Covers
  root-cause diagnosis, action planning, intervention prediction, counterfactual analysis,
  postmortems, decision evaluation, and reasoning stress-tests. When in doubt, apply —
  causal scaffolding improves almost any non-trivial reasoning task. Skip for descriptive
  or simple-recall questions.

---

# Causal Reasoning Engine

A prompt-level reasoning scaffold. No training required. Works by externalizing causal
structure into the context window and reasoning from it explicitly.

## Core Idea

Most reasoning fails because it confuses correlation with causation. This skill forces
reasoning to climb Pearl's three-rung ladder:

- **Rung 1 — Association:** What co-occurs? *(passive observation)*
- **Rung 2 — Intervention:** What happens if I do X? *(active change)*
- **Rung 3 — Counterfactual:** What if X had never happened? *(imagined alternative)*
Default LLM reasoning stays on Rung 1. This skill forces Rungs 2 and 3.

**Trigger principle:** Apply whenever the question concerns cause, effect, or counterfactual.
For descriptive or simple-recall questions, skip the scaffold and answer directly.

---

## Universal Rules

These two rules sit above every pattern and apply to all causal reasoning under this skill.

### Rule 1 — State the Mechanism of Action (MoA)

Never link a cause to an effect without stating the **Mechanism of Action** — the actual
logical, physical, or computational rule that forces the cause to produce the effect.

If you cannot state the mechanism, mark the link `[unknown]` and state what evidence would
establish it. Do not manufacture a mechanism to fill the gap.

### Rule 2 — Sketch the Graph First

For any non-trivial question, build a causal graph before reasoning along it:

```
1. List nodes (entities/variables that might matter).
2. Draw edges A → B only where a mechanism links them.
3. Prune nodes with no causal path to the goal.
4. Reason ONLY along the pruned graph.
```

When labeling nodes, use only the roles that apply — skip the rest:

```
Role         Handling
----         --------
Cause        Reason from it.
Effect       Reason to it.
Mediator     Include if explaining total effect; exclude for direct effect.
Confounder   Adjust/control for it — do NOT ignore.
Collider     Do NOT condition on it unless justified.
Moderator    State the conditions under which the effect changes.
Proxy        Verify it actually represents the variable of interest.
Noise        Drop unless it systematically affects measurement.
```

Confounders are the most common failure mode of naive reasoning (ice-cream sales and
drownings both rise with temperature). Treat them structurally — via graph pruning and
adjustment — not by trying to mentally ignore them.

---

## The Three Patterns

### Pattern I — Intervention (forward reasoning)

*Use when: predicting effects of an action, planning agent behavior, choosing between options.*

```
Intervention: do([variable] = [value])
Goal (if planning): [desired outcome]

1. Direct mechanism: what changes immediately downstream?
2. Propagation: what descendants of this variable shift, and via what MoA?
3. Effect classification: intended / acceptable / risky / unknown.
4. Minimization: is there a smaller or more reversible intervention with the same effect?
5. Confirmation: what observable would tell you it worked — or that you should stop?
```

**Stability note:** non-descendants of the intervened variable stay stable; descendants are
exactly what you are reasoning about — they will change. (Avoid "holding everything else
fixed" — it's colloquially fine but causally wrong.)

---

### Pattern II — Counterfactual Attribution (backward reasoning)

*Use when: something happened and you need to find why — postmortems, root-cause analysis,
decision regret, philosophical paradoxes.*

```
Outcome observed: [outcome]
Contrast: Why [actual outcome] instead of [expected outcome]?

For each candidate cause:
1. Counterfactual: If this had not occurred, would the outcome still likely have happened?
2. Role: necessary, sufficient, enabling, contributing, or merely correlated?
3. Mechanism (MoA): how does it produce the outcome?
4. Layer: trigger, proximate cause, root cause, or systemic precondition?

Return the smallest cause set that jointly explains the outcome.
Distinguish trigger from root cause explicitly when they differ.
```

Real failures usually involve joint causes (a code change *and* a missing test *and* a
traffic pattern *and* weak observability). Do not stop at the first item that fails the
counterfactual test — keep going until the cause set jointly explains the outcome.

---

### Pattern III — Mechanism Invariance (robustness check)

*Use when: stress-testing whether reasoning is genuinely causal or just pattern-matched.*

```
1. Extract the proposed mechanism in one sentence.
2. Abstract: replace domain nouns with variables (A, B, C, X).
3. Test the abstracted mechanism in:
   - A familiar context
   - A different surface domain
   - An adversarial edge case
4. For each, ask:
   - Does the same mechanism still apply?
   - What boundary condition would make it fail?
   - What observation would disconfirm it?
5. Map back. If the answer changes without a boundary-condition reason,
   flag it — the reasoning was correlational, not causal.
```

Boundary conditions are legitimate; mechanisms have scope. The failure mode is *unexplained*
answer-change across domains.

---

## Routing Matrix

```
Question shape          Pattern
--------------          -------
Forward from action     I   — Intervention
Backward from outcome   II  — Counterfactual Attribution
Many variables          Causal Graph (prelude to I or II)
Robustness check        III — Mechanism Invariance
```

**Always:** sketch the graph first; state the MoA on every causal link; verify you stayed
on the right rung last.

**Adapt, don't paraphrase loosely:** preserve the structural moves of each pattern
(do-operator, counterfactual question, mechanism statement, role taxonomy, abstraction step).
Adapt vocabulary to the domain — generic phrasing in a jargon-heavy field disconnects the
scaffold from the actual mechanisms.

**Combine only when worth it:** chain patterns (e.g., Graph → II → I) when the marginal
value exceeds the marginal token cost. On simple problems, one pattern is enough.

---

## Worked Example — A Flaky Test

*Flow: Graph → Counterfactual → MoA → optional Intervention*

**Observation:** `test_user_signup` passes locally but fails ~20% of the time in CI.

**Graph (pruned):**
```
[CI runner load] ──┐
                   ▼
[DB connection pool] ──→ [test setup time] ──→ [test timeout]
                                ▲
[parallel test workers] ────────┘
```
Test code itself: not on a causal path to the timeout → prune.

**Contrast:** Why does it time out in CI but not locally?

**Candidates (counterfactual + MoA + layer):**
- *Slower CI machines* — if removed, would it still fail? Probably yes, ratio is small.
  **Contributing, not root.**
- *Parallel workers competing for DB connections* — if serialized, would it still fail?
  Likely no. **MoA:** pool exhaustion forces test setup to wait past the timeout. **Necessary.**
- *Test setup not waiting for DB ready signal* — if it waited explicitly, would the timeout
  still hit? No. **MoA:** race between connection acquisition and the timeout clock.
  **Necessary.**
**Smallest cause set:** pool contention + missing readiness wait. Slow CI is the *trigger
condition* that exposes them; the two upstream design choices are the *root causes*.

**Smallest intervention (Pattern I):** add explicit DB-ready wait in test setup. Reversible,
observable (timeout rate drops to ~0), minimal blast radius. Confirmation signal: timeout
rate over the next 50 CI runs.

---

## Honest Limits

These patterns work by making causal structure explicit and operable in context. They do not
manufacture causal knowledge the model lacks. If the underlying causal facts are absent from
training or context, the scaffold will surface that gap rather than fill it — which is the
correct behavior.

When you hit that gap: state it explicitly, mark the link `[unknown]`, then ask what
additional information would resolve it. That is also causal reasoning.

---

## Migration Note

For continuity with prior versions of this skill:
- Pattern A ≈ Causal Graph (now a universal prelude under Rule 2)
- Patterns B + E ≈ Pattern I (Intervention, with minimization and confirmation folded in)
- Pattern C ≈ Pattern II (Counterfactual Attribution, now contrastive and multi-cause)
- Pattern D ≈ Pattern III (Mechanism Invariance, now with symbolic abstraction + disconfirmation)
