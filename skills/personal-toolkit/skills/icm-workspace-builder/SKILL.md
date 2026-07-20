---
name: icm-workspace-builder
description: Design and scaffold an Interpretable Context Methodology (ICM) workspace for a sequential, repeatable, human-reviewable workflow. Use when the user asks to build an ICM workspace, create a multi-stage workflow folder, scaffold a file-based pipeline, or set up an ICM for a topic. Interviews the user only for missing decisions, then creates `CLAUDE.md`, workspace routing, shared references, numbered stage contracts, and output folders. Not for one-off tasks, tightly coupled agent collaboration, high concurrency, or complex automated branching.
disable-model-invocation: true
---

# ICM Workspace Builder

Build an inspectable, file-based workflow in which one agent executes numbered stages. Each stage reads explicitly named inputs, performs one job, and writes human-editable artifacts for later stages.

Use plain language. Assume the user may not be technical.

## Core model

An ICM workspace separates five context layers:

1. `CLAUDE.md` — workspace identity and global operating rules
2. `CONTEXT.md` — workspace routing and stage map
3. `stages/NN-slug/CONTEXT.md` — one stage's contract
4. `shared/` or stage `references/` — stable rules reused across runs
5. Stage `output/` folders — working artifacts that change each run

Keep stable rules separate from working artifacts:

- **Reference material:** voice guides, rubrics, templates, policies, schemas
- **Working artifacts:** intake briefs, research, drafts, reports, delivery records

The filesystem is the orchestration layer. Do not invent framework code unless mechanical or external-system work requires a script.

## First: determine whether ICM fits

ICM is a good fit when the workflow is:

- sequential;
- repeatable with different inputs;
- naturally decomposable into at least three meaningful transformations;
- improved by inspecting or editing intermediate artifacts; and
- manageable through file-based handoffs.

ICM is usually not the right fit for:

- one-off or one-to-two-step tasks;
- real-time collaboration among agents;
- high-concurrency services;
- complex automated branching;
- workflows whose important state cannot be represented as inspectable files.

If fit is uncertain, ask:

> Quick fit check: ICM works best for a repeatable sequence of at least three stages where each stage creates an artifact the next stage can read. Does that describe this workflow?

If not, briefly recommend a simpler skill, script, or orchestration framework and stop unless the user explicitly wants to continue.

## Interview policy

Gather only information that is still missing.

- Ask one focused question at a time.
- Skip questions already answered.
- Reflect answers only when doing so confirms an interpretation.
- Ask follow-ups only when an ambiguity would change the architecture.
- Use the user's terminology in generated files.
- Offer a concrete proposed answer when the user is unsure.
- Do not make the user reason about context layers, determinism, replay, or idempotency.
- Do not generate files until the stage map and target folder are confirmed.

Capture these decisions:

1. workflow purpose;
2. operator and cadence;
3. final deliverable;
4. starting inputs;
5. ordered stages;
6. human review gates;
7. branching or optional stages;
8. external effects;
9. stable references and rules;
10. target workspace name and location.

## Discovery questions

Ask only the unanswered questions below.

### Purpose

> In one sentence, what should this workflow accomplish? What will exist at the end that does not exist at the start?

Capture an action, object, and intended audience.

### Operator and cadence

> Who runs it, and when—for each client, weekly, on demand, or on another schedule?

### Final deliverable

> What is the final deliverable? Include its audience, contents, format, and any important length or quality requirements.

### Starting inputs

> What does each run start with, and where does that material come from?

Distinguish:

- values the user types;
- files the user provides;
- folders the workflow reads;
- external systems a stage must query.

### Stage discovery

> Walk me through what happens from start to finish in plain English. Do not worry about naming or numbering the steps.

Convert the answer into stages. Each stage should:

- have one primary job;
- produce a concrete, inspectable artifact;
- avoid combining unrelated judgment or transformations;
- provide what a later stage actually needs.

Then propose:

> I see these stages:
>
> 1. **[Name]** — reads [input] and produces [artifact]
> 2. **[Name]** — reads [artifact] and produces [artifact]
> 3. **[Name]** — reads [artifact] and produces [deliverable]
>
> Is this the right sequence? Should anything be split, combined, optional, or reordered?

Revise until confirmed.

If fewer than three meaningful stages remain, recommend a simpler skill instead.

### Review gates

> Which outputs should a person approve or edit before the workflow continues?

Recommend gates at high-leverage decisions such as:

- scope or direction;
- source selection;
- scoring or diagnosis;
- structure or outline;
- final approval before publication or delivery.

Do not add a gate after every stage by default.

### Branches

> Are any stages optional, or does the next stage depend on a condition?

Prefer simple human-selected routes. If branching is complex or automated, explain that ICM may need a script or a workflow framework.

### External effects

> Does any stage send, publish, upload, update, delete, purchase, or otherwise change an outside system?

Mark such stages as side-effecting. They must require explicit approval unless the user clearly requests automation.

### Stable references

> What rules should stay the same across runs—for example a rubric, voice guide, template, policy, schema, or brand guide?

Place cross-stage references in `shared/`. Place references used by only one stage in that stage's `references/` folder.

### Target

> What should the workspace folder be called, and where should I create it?

Use lowercase kebab-case for the folder unless the user prefers another convention.

## Architecture rules

### Stage boundaries

A valid stage has:

- explicitly listed inputs;
- one primary responsibility;
- an observable process;
- concrete quality checks;
- explicitly named outputs;
- a continuation policy.

Split a stage when it contains separate decisions that may need independent review.

Do not split work merely to increase the stage count.

### Context scoping

Each stage should load only what it needs.

Never instruct an agent to read:

- the entire workspace;
- every prior output;
- all shared references;

unless that is genuinely necessary.

Name exact files or narrowly scoped folders in each Inputs table.

### Handoffs

Prefer named files over vague folder references.

Good:

- `../01-intake/output/brief.md`
- `../../shared/voice-guide.md`

Avoid:

- “Read everything from the previous stage.”
- “Use any relevant files in the workspace.”

If an upstream output does not contain everything the next stage requires, fix the contract rather than relying on conversation memory.

### Outputs

Create an `output/` directory for every stage.

Prefer markdown or JSON for intermediate representations. Use binary formats only for final deliverables or when required by an external tool.

Do not hardcode run-specific client names, topics, or dates into workspace instructions. Capture them in stage 01 output.

### Quality checks

Audit checks must be observable and specific.

Good:

- Every recommendation cites at least one source from `evidence.md`.
- All required report sections are present.
- The total score equals the sum of criterion scores.
- No claim is marked factual without a source URL.

Avoid:

- Make it high quality.
- Ensure it is compelling.
- Check that it looks good.

### Human review

Use one of these continuation policies:

- **Automatic:** continue after the output passes its checks.
- **Approval required:** show the output and wait for explicit approval.
- **Edit or approve:** invite the user to edit the artifact, then wait.
- **Final stage:** stop after presenting the deliverable.

For side effects, require approval immediately before execution.

### External effects

Separate content preparation from execution when practical.

Prefer:

1. prepare the email or update;
2. review it;
3. send or apply it in a distinct side-effecting stage.

A side-effect stage must:

- preview the exact action;
- require explicit confirmation;
- check whether the action already occurred;
- record the result in `output/execution-record.md`;
- avoid repeating a completed action on rerun.

Use a local script or MCP connection for mechanical system interaction. Keep judgment and approval in markdown contracts.

### Branching

Represent simple human-selected branches as clearly named optional stages, for example:

```text
03-standard-report/
03-priority-report/
```

Document the route condition in workspace `CONTEXT.md`.

Do not imply that folder numbering alone performs automated routing.

## Files to generate

Default structure:

```text
workspace-name/
├── CLAUDE.md
├── CONTEXT.md
├── shared/
│   ├── CONTEXT.md
│   └── reference-files.md
└── stages/
    ├── 01-stage-name/
    │   ├── CONTEXT.md
    │   ├── references/
    │   └── output/
    ├── 02-stage-name/
    │   ├── CONTEXT.md
    │   ├── references/
    │   └── output/
    └── 03-stage-name/
        ├── CONTEXT.md
        ├── references/
        └── output/
```

Omit empty `references/` folders if they add no value.

Create `shared/CONTEXT.md` when `shared/` contains multiple files or needs routing. For a single obvious shared file, it may be omitted.

Add scripts only when a stage needs deterministic processing or external-system interaction:

```text
scripts/
└── descriptive-name.py
```

Do not generate placeholder reference content as if it were authoritative. If a reference is needed but not supplied, create a clearly labeled template with `TODO` fields.

## `CLAUDE.md`

Keep this short. It identifies the workspace and establishes global behavior.

```markdown
# [Workspace Name]

## Purpose

[One-sentence purpose.]

## Operating rules

1. Read `CONTEXT.md` to locate the requested stage.
2. Before running a stage, read that stage's `CONTEXT.md`.
3. Load only the inputs named in the stage contract.
4. Write artifacts only to the locations named in the Outputs table.
5. Treat files in `shared/` and `references/` as stable constraints.
6. Treat files in `output/` as working artifacts that may have been edited by a human.
7. Stop at approval gates and before any external side effect.
8. Do not rely on prior chat when a required decision belongs in an artifact.

## Starting a run

If the user does not specify a stage, begin with stage 01. Ask only for required inputs that are not already available.
```

## Workspace `CONTEXT.md`

This is the routing layer.

```markdown
# Workflow Map

## Workflow

[Short description of the full workflow.]

**Operator:** [Who runs it]
**Cadence:** [When it runs]
**Final deliverable:** [Artifact and audience]

## Stage routing

| Stage | Use when | Reads | Produces | Continuation |
|---|---|---|---|---|
| `01-[slug]` | [routing condition] | [inputs] | [artifact] | [automatic / approval] |
| `02-[slug]` | [routing condition] | [artifact] | [artifact] | [automatic / approval] |
| `03-[slug]` | [routing condition] | [artifact] | [deliverable] | final |

## Routes and optional stages

[Conditions and human-selected routes, or "None — the workflow is linear."]

## Shared references

| File | Purpose | Used by |
|---|---|---|
| `shared/[file].md` | [stable rule] | [stages] |

## External effects

[List side-effecting stages and approval requirements, or "None."]
```

## Stage `CONTEXT.md`

Use this contract for every stage:

```markdown
# Stage NN: [Name]

## Objective

[One sentence describing this stage's single job.]

## Inputs

| Type | Source | Use |
|---|---|---|
| Working artifact | `[exact path]` | [what information to use] |
| Reference | `[exact path]` | [constraint or pattern to apply] |
| User input | [field or decision] | [why it is needed] |

If a required input is missing, stop and ask for it. Do not infer critical facts.

## Process

1. [Concrete transformation or decision.]
2. [Concrete transformation or decision.]
3. [Write the specified artifact.]

Stay within this stage's objective. Do not perform later stages early.

## Quality checks

Before completing the stage, verify:

| Check | Pass condition |
|---|---|
| [Name] | [Observable pass/fail condition] |
| [Name] | [Observable pass/fail condition] |

If a check fails, revise the artifact before presenting it.

## Outputs

| Artifact | Location | Format | Required contents |
|---|---|---|---|
| [Name] | `output/[file].md` | Markdown | [sections or schema] |

Do not write stage artifacts outside `output/`.

## Continuation

[One policy:]

- Continue automatically after all checks pass.
- Show the output and wait for explicit approval.
- Invite the user to edit the output, then wait for approval.
- Present the final deliverable and stop.
```

For a side-effecting stage, append:

```markdown
## External action

Before acting:

1. Show the exact action, destination, and payload.
2. Check `output/execution-record.md` for a prior successful execution.
3. Wait for explicit confirmation.
4. Execute once.
5. Record the timestamp, destination, action, result, and external identifier in `output/execution-record.md`.

If a successful matching record exists, do not repeat the action without new confirmation.
```

## Shared routing file

When needed, use:

```markdown
# Shared References

| File | Contains | Load when |
|---|---|---|
| `[file].md` | [description] | [stage or condition] |

Load only the files named by the current stage contract.
```

## Generation procedure

After the user confirms the design:

1. Normalize stage names and create stable numbered slugs.
2. Define each stage's exact input and output paths.
3. Check that every downstream input is produced upstream or supplied externally.
4. Identify stable references and place them at the narrowest useful scope.
5. Add measurable quality checks.
6. Mark approval gates, optional routes, and external effects.
7. Generate the complete folder tree.
8. Validate the workspace before reporting completion.

### Validation checklist

Confirm all of the following:

- Every stage has one primary job.
- Every stage has an `output/` directory.
- Every input path resolves to a generated or user-supplied artifact.
- Every downstream dependency has an upstream producer.
- Stable references are not mixed with per-run outputs.
- No stage is told to load irrelevant workspace content.
- Review gates match the user's decisions.
- Side effects require approval and produce an execution record.
- The final stage produces the requested deliverable.
- `CLAUDE.md`, workspace `CONTEXT.md`, and stage contracts agree.
- There are no unexplained placeholders except clearly marked reference templates.

Fix validation failures before presenting the workspace.

## Execution modes

### Filesystem access available

Create the files directly in the confirmed target directory.

Do not overwrite existing files without permission. If the directory exists:

1. inspect it;
2. summarize conflicts;
3. ask whether to merge, replace, or choose another location.

After writing, report:

- target path;
- files created;
- unresolved `TODO` items;
- first command or request to run.

### Chat-only mode

Provide:

1. the folder tree;
2. every non-empty file under a heading such as `## File: path/to/file.md`;
3. any empty directories that must be created;
4. unresolved `TODO` items.

Do not repeatedly explain the same architecture between files.

## Completion message

Keep the handoff concise:

> The workspace is ready at `[path]`.
>
> Start it by opening that folder in a compatible agent environment and saying:
>
> “Run the `[workspace-name]` workflow for [example input].”
>
> Begin with stage 01 unless you are resuming from an existing artifact. Review the first real run for missing inputs, weak checks, or unclear handoffs, then update the relevant `CONTEXT.md`. Assign one person to steward future changes.

## Common starting shapes

Offer these only when the user is stuck.

### Research to deliverable

1. Intake and scope
2. Evidence gathering
3. Synthesis or outline
4. Draft
5. Review and revision
6. Finalize or deliver

### Recurring client report

1. Capture run parameters
2. Collect client data
3. Analyze or score
4. Compose report
5. Approve
6. Deliver

### Source documents to structured output

1. Inventory and extract sources
2. Organize sections or themes
3. Validate structure
4. Transform each section
5. Assemble final artifact
6. Quality review

## Avoid

- Treating every multi-step request as an ICM candidate
- Requiring exactly eight questions
- Asking for information the user already supplied
- Combining intake with the first substantive transformation
- Vague inputs such as “previous work”
- Loading all references into every stage
- Treating conversation history as workflow state
- Hiding stable rules inside individual stage process steps
- Generating fake domain rules or rubrics
- Adding empty boilerplate files without a routing purpose
- Automating external effects without approval
- Claiming that folders provide complex automated branching
- Writing exact model prompts when a clear stage contract is sufficient
