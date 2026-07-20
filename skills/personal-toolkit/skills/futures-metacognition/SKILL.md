---
name: futures-metacognition
description: "Metacognitive discipline for reasoning about the future — routing between forecasting mode and visioning mode, matching specificity to time horizon, separating prediction from prophecy, and surfacing hidden worldview assumptions. Use this whenever the user asks what will happen, what could happen, or what should happen over any horizon beyond the immediate — trend analysis, scenario work, strategy under uncertainty, technology roadmaps, 'where is X heading', 'what's the future of Y', 'will Z still matter in N years', horizon scanning, futures workshops, or any request to imagine, project, or plan for a future state. Also use when a user presents a single confident future and would be better served by alternatives, or when their question silently mixes 'what is likely' with 'what is desirable'. Trigger even if the user never says 'futurism' or 'foresight' by name."
---

# Futures Metacognition

## The problem this solves

A futurist reasons about an object that produces no observations. Every other discipline is corrected by its subject matter; this one's subject matter arrives too late to correct anything.

So the failure mode is almost never a wrong step. It is operating in the **wrong register** — delivering a vision with the confidence markers of a forecast, or applying forecast-grade caution to a question that was asking what is worth wanting.

This skill is a router and a set of checks, not a procedure. Run the checks; pick the mode; produce the mode's output contract.

## Step 1: Route before you answer

Read the request and classify it. Say which mode you are in, in one line, before producing anything.

| Signal in the request | Mode | Go to |
|---|---|---|
| Resolvable question, a date, a probability, "will X happen by" | **Forecast** | Use the `forecast-discipline` skill; stop here |
| "What could happen", "what are the scenarios", planning under uncertainty | **Scenario** | Section 3 |
| "What should we build", "what's the world we want", mission or narrative work | **Vision** | Section 4 |
| "Why is this happening", "what's really driving this" | **Diagnosis** | Section 5, then usually Scenario |
| Mixed or unclear | **Split it** | Section 2 |

If the request contains a resolvable question with a deadline, it is a forecasting task and belongs in `forecast-discipline`. Do not hand-wave it into a scenario exercise; that is how questions escape being scored.

## Step 2: Split mixed requests explicitly

Most real questions blend "what is likely" with "what is worth wanting". These demand opposed virtues and must not share a sentence.

|  | Forecast register | Vision register |
|---|---|---|
| Virtue | calibration, granularity, willingness to be boring | coherence, boldness, moral imagination |
| Asks | what is likely | what is worth wanting |
| Fails as | timid mush | confident fantasy |

When a request blends them, name the split out loud and answer both parts separately with a visible boundary between them. A blended product — a vision carrying forecast-grade confidence markers — is the single most common pathology in this field, and the one users are least able to detect.

## Step 3: Scenario mode

**Match specificity to horizon.** The characteristic sin is long-horizon confidence delivered with short-horizon detail. Enforce:

- **0–2 years**: base rates, installed base, things already in the pipeline. Specifics are legitimate.
- **2–7 years**: system dynamics, feedback loops, path dependency. Name mechanisms, not events.
- **7+ years**: only invariants and constraints survive — physics, demographics, energy, materials, latency, attention, trust, regulatory throughput, human time. Anything more specific is decoration; label it as such if you include it.
**Prediction vs. prophecy.** You cannot predict the content of future knowledge, because predicting it would be having it. Everything downstream of ideas-not-yet-had is unforecastable in principle, not merely in practice. Police this boundary explicitly — say which parts of your answer sit on the forecastable side and which are prophecy.

**Constraints predict better than trends.** Before extrapolating any curve, ask what the slow variable is. Slow variables win. A trend that must cross a hard constraint will bend at the constraint, not at the trend's own logic.

**Never produce a single-track future.** If you find yourself writing one, you have made a mistake. Minimum viable output is one central line plus two structurally different alternatives — not optimistic/pessimistic variants of the same story, which is the same story three times.

**Scenario output contract:**

```
## What is (nearly) invariant
[constraints and slow variables that hold across all branches]

## What is genuinely uncertain
[the 2-3 variables that actually drive divergence]

## Branches
### [Name] — driven by [which uncertainty resolving which way]
[3-5 sentences. Mechanism, not narrative flourish.]
[repeat for each branch]

## Tripwires
[for each branch: a near-term observable, with a date, that would tell you this branch is arriving]

## What this changes about what you do now
```

The tripwires section is mandatory. A scenario with no tripwire is decoration — it can never be wrong, and so it can never teach anything. Hand the tripwires to `foresight-error-correction` if the user wants them tracked.

## Step 4: Vision mode

Here boldness is the virtue and hedging is the failure. But three constraints still bind:

- **Label it.** State plainly that this is a claim about what is worth wanting, not a forecast. Do not smuggle in probabilities.
- **Answer "whose future is this, and who is absent from it?"** Futures are contested political goods. A great deal of futurism is present-day preference wearing a lab coat. Name whose interests the vision serves and who bears its costs.
- **Stay reflexive.** Images of the future are causally active — a shared image of the future shapes the behaviour that produces the future. You are never purely describing. Flag this when the vision is intended to be circulated, because then its effect is part of its content.
## Step 5: Diagnosis mode — find the layer

When someone is stuck, they are usually stuck at a layer. Work down:

1. **Litany** — the headline, the reported numbers, the thing everyone repeats
2. **Systems** — the causes: economic, technological, institutional
3. **Worldview** — the assumptions that make the systems seem natural
4. **Myth** — the deep story or metaphor underneath
Name which layer the user's framing sits at, then go at least one layer deeper. Most disagreements that look like disputes about facts are disputes at the worldview layer wearing litany-layer clothes.

For hard causal questions inside this step, `causal-reasoning-engine` composes well here.

## Always-running checks

Run these against your own draft before delivering. If any fails, revise rather than caveat.

- Am I predicting, or prophesying?
- Does my specificity match my horizon?
- What would make me wrong, and by when would I know?
- Am I extrapolating a variable, or modelling a system? What did I hold constant that will not stay constant?
- What is invariant here versus what is merely fashionable?
- Which layer am I stuck at?
- Which mode am I in, and have I mixed the products?
- Whose future is this, and who is missing?
- Is this description, or is it intervention?
## Failure patterns to avoid

**Amara's law, applied to yourself.** People overestimate the short run and underestimate the long run. When you catch yourself producing a dramatic two-year forecast and a modest twenty-year one, you have it backwards.

**Trend-extrapolation as analysis.** Drawing the line forward is not a model. State the mechanism that makes the line continue, then state what would break it.

**Signal laundering.** A signal is one observation. A trend is a signal with a time series. A driver is a trend with a mechanism. Do not promote one to the next without saying you did.

**Novelty bias.** The interesting thing is rarely the important thing. Ask what persists, not what is new — durability comes from how cheaply a thing can be re-made from what is already lying around, not from how novel or elegant it is.

**Hindsight-cheating models.** If your framework explains the last thirty years effortlessly, test it: run it forward from a date thirty years ago and see whether it actually says what happened, or whether you are reading the answer off the back of the book.

## Related skills

- `forecast-discipline` — for any resolvable, dated, probability-bearing question
- `foresight-error-correction` — for tripwire tracking, surprise ledgers, and diagnosing which kind of wrong you were
- `causal-reasoning-engine` — for the systems layer in diagnosis mode
