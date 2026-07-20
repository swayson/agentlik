# BoI Framework — Worked Examples

Use these to calibrate depth and tone. Each example is abbreviated — real sessions go deeper.

---

## Example 1 — Business (retention drop)

**Stated**: "Our user retention is dropping and we don't know how to fix it."

**Phase 0** — Probe: where does drop-off happen? Is the mechanism known?
**Restated**: *"We don't know which experience causes users to decide the product isn't worth continuing with."*

**Conjectures**
- **A. Activation gap** — Users churn before reaching core value. Onboarding friction stops them hitting the "aha" moment. → Retention correlates with completing one specific first-session action.
- **B. Promise-reality gap** — Marketing acquires a persona the product doesn't serve. → Churned users describe jobs-to-be-done that differ from retained users.
- **C. Habit gap** — Product is useful but lacks a recurring trigger to bring users back. → Retained users have an identifiable external trigger; churned users don't.

**HTV**
- A: 🟢 — "activation event" is load-bearing; swap it for "general engagement" and the prediction changes entirely
- B: 🟡 — "different persona" is loose; needs specifying
- C: 🟡 — "no trigger" is clear; "habit loop" needs tightening

**After criticism**
- A: Falsified if users who completed the activation event still churn at high rates
- B: Falsified if churned users want exactly what retained users use
- C: Falsified if churned users show consistent return behaviour before dropping off

**Best conjecture** — A. Hardest to vary, sharpest prediction, cheapest to test.
**Reach** — Explains why "adding features" rarely fixes retention. Applies to free-trial conversion, B2B onboarding.
**New problems** — 1. What is the activation event? 2. What specifically causes onboarding friction?
**Falsifier** — Cohort data showing high churn among activation-event completers.
**Next move** — Pull retention cohorts segmented by activation event completion.

---

## Example 2 — Technical (system slowness)

**Stated**: "Our system is getting slow and we need to scale."

**Phase 0** — "Slow" and "scale" are symptom + assumed solution. What specifically is slow?
**Restated**: *"We don't know the binding constraint, so we risk solving the wrong thing."*

**Conjectures**
- **A. DB bottleneck** — A single query (N+1 or missing index) runs on every request. Adding servers doesn't help. → Profiling shows DB time at 70%+ of request duration.
- **B. External latency** — Requests block on synchronous third-party calls. → Tracing shows spans stuck on I/O.

**HTV** — Both 🟢. Each mechanism is specific; swapping it changes the solution entirely.

**Anti-pattern** — "We should add Redis / go microservices" — authoritarianism. What does the profiler say first?

**Best conjecture** — Test A first (more common, cheaper to fix).
**Reach** — Identifies the binding constraint before optimising. Applies to any performance problem (cf. Theory of Constraints).
**Falsifier** — Profiling shows DB time under 30%.
**Next move** — Run profiler on representative production traffic.

---

## Example 3 — Personal (job offer)

**Stated**: "I don't know whether to take this job offer."

**Phase 0** — What creates the uncertainty specifically?
**Restated**: *"I don't know which of my concerns are real constraints versus imagined ones."*

**Conjectures**
- **A. Risk-calibration problem** — Hesitation is fear, not substance. Discomfort is being misread as evidence. → With a guaranteed return option, the decision would be immediate.
- **B. Values-conflict problem** — The new role genuinely trades off things that make work satisfying. → The person can name specific daily-work aspects that would get worse, not just different.

**HTV** — Both 🟢 if values (B) can be named concretely.

**Anti-pattern** — "Everyone I've asked thinks I should take it" — authoritarianism. What's their reasoning, and does it apply here?

**Falsifiers**
- A: Person says no even with a guaranteed return option → A wrong, B likely right
- B: Person can't name specific daily-work downsides → B wrong, A likely right

**Next move** — Ask: "If you could try for 3 months with a guaranteed return — immediate yes?" Answer in 30 seconds. Start there.
