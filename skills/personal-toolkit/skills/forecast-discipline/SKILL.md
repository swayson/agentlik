---
name: forecast-discipline
description: "Produce calibrated probabilistic forecasts on resolvable questions using the practices that measurably win forecasting tournaments — base rates first, agentic multi-source research, ensembling across independent framings, extremity capping, and explicit resolution criteria. Use whenever a question has or could have a date and an outcome that will be checkable — 'will X happen by Y', 'how likely is', 'what are the odds', 'when will', 'should I bet on', estimating timelines, sizing risks, evaluating a claim someone else has forecast, or judging whether a prediction was any good. Also use when a user states a confident claim about a future event and would benefit from it being turned into a scored, falsifiable forecast. Trigger even when the user asks casually and does not use the word 'forecast' or 'probability'."
---

# Forecast Discipline

## Scope

This skill handles **resolvable** questions: there is an outcome, and someone could later check it. If the question is not resolvable, use `futures-metacognition` instead — do not produce false precision on an unscoreable question.

The practices below are drawn from what actually correlates with accuracy in live forecasting tournaments rather than from what sounds rigorous. Several things that sound rigorous do not work, and they are listed in the anti-patterns section. Take that section seriously; it is the part most likely to contradict your instincts.

## Step 0: Nail the resolution criteria first

Before any research, write down exactly what would count as a Yes. Most forecasting errors are not probability errors — they are the forecaster answering a slightly different question than the one asked.

State explicitly:
- The precise event
- The deadline, with a timezone if it is tight
- The resolution source
- At least one edge case and how it resolves
If the question is genuinely ambiguous, say so and forecast the most natural reading, naming it.

**Guard against the resolved-question trap.** Before forecasting, check whether the question has already resolved. Bots and humans both lose badly by giving near-certain forecasts on questions they have misread as already settled, or by treating stale news as current. Verify the current state before assigning any probability above 0.9 or below 0.1.

## Step 1: Base rate before news

Compute an explicit base rate before reading any current information. This correlates strongly with accuracy and almost nobody does it — among tournament winners it separates the top of the field from the rest.

- What is the reference class?
- How often has this class of event happened in comparable windows?
- What is the naive rate implied by the time remaining?
Write the number down. It is your anchor. Everything after this is an update on it, and you should be able to say how far you moved and why.

Also look for **similar previously resolved questions**. This is a distinguishing habit of strong forecasters and a cheap one.

## Step 2: Research iteratively, from more than one source

Two findings matter here:

- **Iterative/agentic search beats one-shot retrieval**, substantially. Search, read, notice what you still do not know, search again. Removing search entirely degrades accuracy several-fold.
- **Breadth of sources beats brand of source.** No single search provider reliably wins. Use two or three distinct kinds of source — news, primary documents, market or platform prices where they exist — rather than trying to find the one best one.
Look specifically for: the most recent status change, the mechanism that would have to fire for Yes, who has the power to make it happen, and whether anything has already been scheduled.

## Step 3: Forecast from independent framings, then aggregate

Do not produce one number. Produce several from genuinely different angles, then combine. Ensembling is near-universal among winners.

Use three to five framings, chosen to be as decorrelated as you can make them, for example:

- The base rate, updated minimally
- The inside view: the specific mechanism and its known blockers
- The outside view on the actors: what do these people usually do
- The market or crowd view, if one exists
- The steel-manned opposite: argue the other side properly, then read off what probability that argument implies
Aggregate by median rather than mean — the median is robust to a single framing going badly wrong, and that is the actual failure mode.

**Do not use multiple personas.** Assigning fictional expert characters to the framings does not improve accuracy and reportedly hurts; the final aggregating step becomes bad at genuine criticism when the disagreement is theatrical rather than structural. Vary the *reasoning approach*, not the costume.

## Step 4: Cap the extremes

Before finalising, pull any probability outside roughly 3%–97% back toward that band unless you have a specific, verified reason for extremity — a completed event, a legal certainty, a physical impossibility.

The reasoning is asymmetric: one misread, hallucinated, or stale-news error at 99% can erase an enormous amount of accumulated accuracy, while the upside of being extremely confident and right is bounded. Capping is the single strongest differentiator among strong forecasters.

## Step 5: Check your own calibration drift

Ask: across the forecasts I have made in this conversation or this project, am I systematically too confident? Forecasters, human and machine, tend toward overconfidence, and a blanket shrink toward 50% often improves scores. If you have made several forecasts, look at them as a set, not one at a time.

## Output contract

```
**Question**: [restated precisely, with resolution criteria and deadline]

**Base rate**: [number] — [reference class and how derived]

**Key updates**:
- [factor] → moves toward [Yes/No] because [mechanism]
- [factor] → ...

**Framings**:
| Framing | Probability |
|---|---|
| Base rate, minimally updated | X% |
| Inside view / mechanism | X% |
| Actor behaviour | X% |
| Steel-manned opposite | X% |

**Forecast: X%** [median of framings, after capping]

**What would change this most**: [the one piece of information with the highest value]

**Tripwire**: by [date], if this is on track, expect to observe [specific, checkable]
```

The tripwire is not optional. It is what converts a forecast into something that can correct you before resolution. Hand it to `foresight-error-correction` if the user is tracking a set of these.

## Anti-patterns

These are things that sound like good practice and are not:

- **"Let me reason as a Bayesian."** Prompts and framings built around explicit Bayesian ceremony consistently underperform. Do the actual updating — anchor, then move for stated reasons — without the vocabulary. The ritual language substitutes for the practice.
- **Anchoring on the crowd.** Optimising to match a community prediction or market consensus degrades performance once you are near that level, and it caps you at it. Use the crowd as one framing among several, not as the target.
- **Retrodicting with a model that already knows the answer.** Asking a model to "pretend it doesn't know" what happened does not work — measured accuracy degrades by roughly half compared to genuine ignorance. Any backtest needs a strict information cutoff enforced from outside, not a request for amnesia. This applies to you: if you are testing a method against past events you know the outcome of, your result is close to worthless.
- **Single-source confidence.** One well-written article is one source.
- **Precision as a substitute for accuracy.** 63.7% is not a better answer than 65%; it is the same answer with a false signal of resolution. Round to something your evidence can actually support.
## Calibration note on your own limits

On resolvable questions, current AI forecasting sits meaningfully above the general public and below the strongest human forecasters, with the gap narrowing but not closed as of mid-2026. Claims that AI has reached superforecaster parity rest mostly on backtests with information-leakage problems and have not reproduced under live forward-looking evaluation.

Be useful and be calibrated about being useful: a well-structured forecast from this process is a real contribution to a decision, and it is not an oracle. Say so when the stakes warrant it.

## Related skills

- `futures-metacognition` — for unresolvable, long-horizon, or normative questions
- `foresight-error-correction` — for scoring, tracking, and learning from resolved forecasts
