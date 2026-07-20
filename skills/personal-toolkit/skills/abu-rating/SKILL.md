---
name: abu-rating
description: "Apply the A/B/U (New/Known/Unclear) epistemic rating framework to communication, teaching, learning, and knowledge calibration tasks. Use this skill whenever the user wants to teach or explain something to a specific audience, calibrate shared knowledge with a collaborator, assess what someone already knows, structure a curriculum or explanation sequence, rate information for its novelty or relevance, or diagnose why communication is failing. Trigger on phrases like 'explain this to', 'calibrate with', 'what do they already know', 'how do I teach', 'find common ground', 'am I pitching this right', or any situation involving knowledge transfer between two parties."
---

# ABU Rating Skill

## Core Model

Rate any piece of information `I` relative to a **specific person P at a specific time t**:

| Rating | Condition |
|--------|-----------|
| **A** | True, relevant, AND not yet known to P — updates their model |
| **B** | True, relevant, AND already known to P — confirms their model |
| **U** | False, OR irrelevant, OR too many missing B's to integrate |

**Critical constraint:** A/B/U is never a property of information alone. It is always a relation: `f(information, person, time)`. The same item can be A for one person and B for another.

---

## The U Problem (most important insight)

U has three distinct causes that look identical from the outside:

1. **Falsity** — the information is wrong
2. **Irrelevance** — true, but doesn't connect to P's goals or model
3. **Missing B floor** — true and relevant, but P lacks the prerequisite B's to integrate it
When you observe a U, always diagnose which cause fired before responding. Default assumption: missing B floor, until disproven.

**Disambiguation moves:**
- Check falsity: Can you verify the claim independently?
- Check relevance: Ask P what they're trying to accomplish
- Check B floor: Back up one inferential step and probe there
---

## Key Structural Concepts

**B floor** — the intersection of what both parties already know. Communication requires this. Find it before transmitting A's.

**A ceiling** — the frontier of what's new to P. Good teaching lives just above this line.

**Inferential distance D(I,P)** — the number of B's missing between P's current knowledge and the target A. You cannot skip these. Each B reduces D by 1.

---

## The Eight Sequences

Apply the right sequence to the right goal:

### 1. Bisection Calibration — find B floor fast
Present information at the midpoint of estimated knowledge. A → go lower. B → step higher. U → run disambiguation, then go lower. Converges in O(log n) exchanges.

### 2. Teaching Ladder — deliver a specific A
Structure: `B × D(I,P) → A → [U]*`
Count the required B's first. Lead with them in order. Deliver A only after the scaffold is in place. Continue past A until first consistent U to find the true frontier.

### 3. Coherence Test — verify the A actually landed
After delivering A, present a necessary logical consequence C. If A was integrated, C should now be rated B by P. If C is still A or U, the A was acknowledged but not understood. Re-scaffold.

### 4. Socratic Elicitation — build B floor more durably
Instead of stating B's, ask P to retrieve and state them. Retrieval practice during B establishment produces stronger A integration. Slower, but retention is strictly better.

### 5. Frontier Probe — find A ceiling quickly
Escalate A's until first consistent U that survives disambiguation. Binary variant: start extreme, bisect down. Use for onboarding, curriculum design, or assessing collaboration overhead.

### 6. Compression Stream — maximum density between calibrated peers
Precondition: B floor perfectly shared. Strip all B's — they carry zero information. Transmit only A's. Fragile: any B floor miscalibration immediately produces U with no scaffold to recover from.

### 7. Decay Refresh — maintain knowledge against forgetting
B's at time t₀ can decay to effective-U by t₀+Δ. Probe before predicted decay point. Re-present as A if decayed. Schedule with spaced repetition logic.

### 8. Perspective Triangulation — validate A from a different path
Two people with different B floors who reach the same A provide stronger evidence for that A's truth. Seek this when stakes are high and you want to verify a conclusion isn't an artifact of your particular inferential chain.

---

## Decision Guide

| Situation | Use sequence |
|-----------|-------------|
| Don't know what P knows | 1 — Bisection Calibration |
| Teaching a specific concept | 2 — Teaching Ladder |
| Checking if understanding is real | 3 — Coherence Test |
| Teaching for retention | 4 — Socratic Elicitation |
| Assessing someone's level | 5 — Frontier Probe |
| Collaborating with a peer | 6 — Compression Stream |
| Reviewing previously taught material | 7 — Decay Refresh |
| High-stakes claim validation | 8 — Perspective Triangulation |

---

## Applying the Model in Practice

**Step 1:** Identify the two parties (or self + material).

**Step 2:** Estimate the B floor. What do you know they know? What's uncertain?

**Step 3:** Calculate inferential distance. How many steps between their frontier and the target A?

**Step 4:** Select a sequence from the table above.

**Step 5:** Execute. Rate each exchange A/B/U as you go. Adjust sequence if U appears unexpectedly.

**Step 6:** On unexpected U — stop, disambiguate the cause, adjust scaffold before continuing.
