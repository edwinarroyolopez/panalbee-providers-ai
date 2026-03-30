# Start New Project Flow (master workflow)

## Intent

Turn new-project setup into a conversational system with five mandatory phases:

1. intake libre
2. analysis
3. minimal missing questions
4. synthesis
5. generation

The agent must avoid blind questionnaires and avoid document inflation.

## Entry conditions

Trigger this flow when the user says they want to start a new project (or equivalent) and references this starter.

Before asking discovery questions, read:

1. `ai/starter.md`
2. `ai/START_NEW_PROJECT.md`
3. this file + the other `ai/setup/*.md` files

## Phase 1 - Intake libre (mandatory first step)

Ask for free-form context first.

Expected prompt style:

- ask the user to paste all available prose, notes, constraints, goals, and business flows
- do not present a full form
- do not ask category-by-category questions yet

Output of phase 1:

- raw discovery input captured as source material

## Phase 2 - Analysis

Analyze the prose and return a structured readout:

- what is clear
- detected entities
- detected surfaces/channels
- inferred auth/tenancy/capability model
- detected primary flows
- ambiguities and risks

Output contract for this phase:

1. "Understood"
2. "Detected model"
3. "Unknowns"

## Phase 3 - Minimal missing questions

Only ask what blocks synthesis and generation.

Rules:

- ask the minimum set needed to close real gaps
- batch concise questions by priority
- each question must state why it is needed
- mark assumptions explicitly if the user prefers to defer

Use `ai/setup/project-discovery-question-bank.md` as a source, not as a checklist.

## Phase 4 - Synthesis

Transform discovery into canonical context artifacts using `ai/setup/project-synthesis-rules.md`:

- `ai/instructions/project-context.md`
- `ai/instructions/domain-map.md`
- `ai/instructions/feature-map.md`
- `ai/instructions/glossary.md`

These are mandatory setup outputs.

## Phase 5 - Generation

Decide additional files with `ai/setup/project-generation-rules.md`:

- create only what is justified
- avoid duplication with existing canon
- do not create decorative workflows/agents/skills

Possible outputs:

- `ai/instructions/*.md`
- `ai/agents/*.md`
- `ai/skills/*.md`
- `ai/workflows/*.md`

## Completion gate

Before declaring setup ready, validate `ai/setup/project-completion-gate.md`.

If the gate fails, report exactly what is missing and continue discovery.
