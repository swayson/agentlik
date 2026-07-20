---
name: empirical-schematization
description: >
  Constructs provisional objects and executable temporal rules from
  observations. Use when interacting with an unfamiliar system, debugging
  unknown behavior, reverse-engineering an environment, or deciding among
  competing causal explanations.
---

# Empirical Schematization

## Purpose

Do not begin by asking, "What should I do?"

First ask:

1. What is actually given?
2. How has it been synthesized into objects and events?
3. What temporal rule makes the proposed concept applicable?
4. What appearance should result from the proposed action?
5. What result would require reconstructing the representation?

The goal is not to produce a plausible explanation. The goal is to construct
and test an operational schema.

## Epistemic separation

Keep the following distinct:

- GIVEN: Directly observed or returned by a tool.
- SYNTHESIZED: An entity, property, event, or identity constructed by
  combining observations.
- SCHEMA: A procedural rule describing how a concept applies over time.
- JUDGMENT: A claim that a schema applies in the present case.
- ANTICIPATION: The observation expected if the judgment is correct.
- ACTION: A controlled intervention.
- RESULT: The observation obtained after the action.
- REVISION: A change to the schema or the representation.

Never report a synthesized entity as though it were simply given.

## Procedure

### 1. Apprehend the given

Record only what is directly available.

Do not initially use unexplained causal or functional terms such as:

- controls
- causes
- blocks
- enables
- wants
- means
- is for

Example:

Bad:
"The button controls the door."

Good:
"A red region appeared at coordinates x and y.
A rectangular boundary was visible elsewhere.
Their functional relation is unknown."

### 2. Synthesize a provisional state

Propose what must be tracked across observations:

- Candidate objects
- Candidate boundaries
- Properties
- Quantities
- Locations
- Event order
- Identity across time
- Relevant background conditions

Mark every element as provisional.

Ask whether an apparent object should instead be:

- Divided into multiple objects
- Combined with another object
- Treated as a process
- Treated as a relation
- Treated as an observation artifact

### 3. Generate schemata

For each important concept, specify an operational temporal procedure.

A schema must contain:

- Preconditions
- Operation or action
- Expected transition
- Observable result
- Timescale
- Scope
- Possible falsifier

Use this form:

SCHEMA:
Given conditions C,
if operation A occurs,
then appearance O should occur within interval T,
unless boundary condition B applies.

Do not accept abstract labels without an operational schema.

For example, do not merely claim that X "causes" Y.
Specify what intervention on X should alter Y, under which conditions,
and what observation would oppose that claim.

### 4. Examine categories

Use these as questions, not as assumptions.

#### Quantity

- What is being counted as one?
- Is this one object, many objects, or a total system?
- Can the state be divided into components?
- At what scale does the proposed rule hold?

#### Quality

- What property is present?
- What would count as its absence?
- Does it vary by degree?
- What would count as zero or a limiting case?

#### Relation

- What persists while states change?
- What regular temporal dependence is proposed?
- What intervention could distinguish causation from coincidence?
- Are two components mutually constraining each other?

#### Modality

- What is merely possible under the current representation?
- What is presently actual?
- What is necessary only if the proposed model is accepted?
- Which outcomes remain underdetermined?

### 5. Produce competing schemata

When evidence permits multiple explanations, preserve them.

For each candidate, state:

- What it explains
- What it predicts
- What it does not explain
- What observation would distinguish it from alternatives

Do not collapse alternatives merely to simplify planning.

### 6. Select an action

Prefer an action that:

- Is reversible
- Changes one relevant condition
- Minimizes cost and irreversible consequences
- Produces different predictions under competing schemata
- Has an observable outcome
- Can be stopped after one transition

Classify the action as one of:

- MEASUREMENT: Improves observation without intentionally changing the system
- INTERVENTION: Changes a candidate variable
- DISCRIMINATION: Separates competing schemata
- REPLICATION: Repeats a prior intervention
- BOUNDARY TEST: Tests where a schema ceases to apply
- GOAL ACTION: Pursues the objective using an already tested schema

Do not use a goal action as though it were automatically a valid experiment.

### 7. Register anticipation before acting

Before invoking an external action, record:

- Chosen action
- Active schema
- Predicted observation
- Alternative predictions
- Relevant background conditions
- Confidence
- Falsification condition
- What will be revised if the prediction fails

Do not act if no observable consequence has been specified.

### 8. Execute one controlled action

Perform only the registered action.

Do not silently add actions because the first result was inconvenient.

### 9. Judge the result

Compare the result with the registered anticipation.

Classify it as:

- CONFORMS
- PARTIALLY CONFORMS
- CONTRADICTS
- INCONCLUSIVE
- UNOBSERVABLE

Distinguish:

- Prediction failure
- Measurement failure
- Action execution failure
- Incorrect object identity
- Missing state variable
- Incorrect temporal scale
- Incorrect transition rule
- Incorrect boundary condition

### 10. Revise

A contradiction does not merely require lowering confidence.

Consider revising:

1. The property values
2. The transition rule
3. The relevant variables
4. The identity of objects
5. The object boundaries
6. The timescale
7. The causal direction
8. The observation model
9. The category used to organize the phenomenon

After revision, replay the new schema against all previous observations.

## Required output

Before an action, output:

### Given
Direct observations only.

### Synthesis
Provisional objects, events, and quantities.

### Candidate schemata
Executable temporal rules.

### Present judgment
Which schema may apply now and why.

### Anticipations
Predictions from each viable schema.

### Selected action
One controlled intervention and its purpose.

### Revision commitments
What will change under each possible outcome.

After an action, output:

### Result
The new direct observation.

### Comparison
How it differs from each registered anticipation.

### Judgment
Conforms, contradicts, or remains inconclusive.

### Revision
Changes to the representation or schema.

### Next question
The most important remaining uncertainty.
