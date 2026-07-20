---
name: foresight-error-correction
description: "Build and run the feedback loop that futures work does not get for free — writing tripwires that can fire before an outcome resolves, keeping a timestamped surprise ledger, scoring past predictions honestly, and diagnosing whether a miss was about direction, timing, or mechanism (which have completely different repairs). Use whenever someone is reviewing a forecast, scenario, plan, or strategy against what actually happened — postmortems, retrospectives, 'we didn't see this coming', 'why did we get this wrong', 'was that a good call', quarterly strategy reviews, updating a roadmap after a surprise, or setting up any system meant to catch a wrong assumption early. Also use proactively right after producing forecasts or scenarios, to attach tripwires before the reasoning is lost. Trigger even when the user frames it as blame, luck, or hindsight rather than as error correction."
---

# Foresight Error Correction

## Why this exists

Futures work has no natural grader. Memory silently revises predictions into having been right, and the same wrong model survives decade after decade because nobody ever wrote down what it committed to.

Everything here is machinery for manufacturing the correction the world will not supply on its own. Three components: **tripwires** (fire before resolution), **the surprise ledger** (captures the highest-information events), and **failure-type diagnosis** (turns a miss into a specific repair).

## Component 1: Tripwires

A tripwire is a near-term, checkable observable that a longer-range claim entails. It converts an unfalsifiable outlook into something that can be wrong on a schedule.

**Write them at the moment of the forecast**, not later. The reasoning that generates a good tripwire evaporates within days.

A usable tripwire has all four of:
- A **date**, sooner than the thing being forecast
- An **observable** that someone could check without argument
- A **direction**: which way it cuts
- A **prior commitment**: what you will do if it fires
```
TRIPWIRE
Claim it tests: [the forecast or scenario]
By: [date]
Observable: [specific, checkable, no interpretation needed]
If observed: [claim is on track / needs revision]
If NOT observed: [what specifically changes]
Pre-committed response: [what you will actually do]
```

Bad tripwire: "watch for increased adoption." Good tripwire: "by 30 Sept, at least two of the top five vendors have shipped this in a generally available product."

**The pre-committed response is the part that does the work.** Without it, a fired tripwire gets absorbed as "interesting" and changes nothing.

## Component 2: The surprise ledger

A surprise is the highest-yield object in the entire practice. It is the only free evidence you get that your model has a hole. Most of it is wasted because nobody writes it down while it still stings.

Log every surprise, immediately, with a timestamp:

```
SURPRISE
Date:
What happened:
What I expected instead:
Why my model said the other thing: [the actual belief, not a tidy reconstruction]
What in the model has to change:
Does this contradict any recorded forecast? [which one]
```

The third field is where the value is and where people cheat. Write the belief you actually held, including the embarrassing version. A reconstructed reason is worse than nothing because it teaches you a lesson you did not need.

**Review the ledger periodically** — monthly is a workable cadence, and reviewing your biggest misses on a schedule is a habit of people who measurably improve. Look for repeats. The same surprise twice is a structural blind spot, not bad luck.

## Component 3: Diagnose which kind of wrong

This is the step that determines whether anything improves. Conflating the three is the main reason people forecast for years without getting better.

| Failure type | Signature | Usual cause | Repair |
|---|---|---|---|
| **Direction** | Predicted up, it went down | The model is wrong, not miscalibrated | Rebuild the causal story; this is the serious one |
| **Timing** | Right thing, wrong when | An underweighted constraint or a slower actor | Find the rate-limiting step you ignored; widen future intervals on this class |
| **Mechanism** | Right outcome, wrong path | Lucky, not right | Fix the model even though the score looks fine — this failure hides |
| **Resolution** | Question meant something else | Sloppy criteria | Fix the process upstream, not the belief |

**Mechanism failures are the dangerous ones**, because the outcome vindicates you and the error survives untouched. Explicitly ask, on every hit: *did it happen for the reason I said?* A right answer for the wrong reason is a miss dressed as a win.

**Timing errors are not near-misses.** "Right but early" is the most-abused phrase in this field. Treat a timing error as a real error with a specific cause: something moved slower than you modelled, and you can usually name it.

## Component 4: Scoring, honestly

When reviewing past predictions:

1. **Use the written record only.** If it was not written down with a date, it does not count. Do not let anyone, including yourself, reconstruct what they "basically thought". This rule feels harsh and is the whole point.
2. **Score the set, not the anecdote.** One vindicated call proves nothing. Look at all recorded predictions, including the boring ones, especially the boring ones.
3. **Check calibration separately from accuracy.** Of the things called ~70% likely, did roughly 70% happen? A forecaster can be well-calibrated and useless (no discrimination), or sharp and overconfident. These need different fixes.
4. **Count the omissions.** What happened that was never on any list? A record of only the things you thought about flatters you enormously.
## Composing with a fresh claim

When someone brings a new forecast or scenario, run this attachment sequence:

1. Extract every claim that could be wrong
2. Write a tripwire for each one that matters
3. Note which past surprises this claim would have failed to anticipate
4. Ask what the claim forbids — if it forbids nothing, it is not yet a claim
**The hard-to-vary test.** A good explanation has details that cannot be swapped out without wrecking it. If the specifics of a scenario could be freely substituted and the story would work just as well, it is explaining nothing, and no tripwire will save it. Send it back before spending effort on measurement.

## Retrodiction, with a warning

Testing a model against history is useful and is easy to fake.

- Run the model forward from a past date and check what it actually says — do not check whether it is *compatible* with what happened. Nearly everything is compatible with everything.
- **You cannot un-know an outcome.** Asking yourself or a model to reason "as if" ignorant of a known result does not produce genuine ignorance; measured accuracy under simulated ignorance is dramatically worse than real ignorance. Retrodiction is therefore evidence of a weak kind. Trust it far less than a tripwire that fired in real time.
- Prefer short-fuse forward tests: questions resolving in days or weeks give real feedback fast and cannot leak.
## Output contract for a review

```
## What was claimed
[verbatim from the record, with dates]

## What happened

## Verdict per claim
| Claim | Outcome | Failure type | Repair |

## Mechanism check
[for each apparent hit: right for the stated reason?]

## Omissions
[what happened that was on nobody's list]

## Model changes
[specific — "widen timelines on regulatory steps", not "be humbler"]

## New tripwires
```

Keep "model changes" concrete. "Be more careful" is not a repair; it is a feeling.

## Related skills

- `forecast-discipline` — for generating the forecasts this scores
- `futures-metacognition` — for scenario work and mode routing
- `causal-reasoning-engine` — for direction and mechanism failures, where the causal story needs rebuilding
