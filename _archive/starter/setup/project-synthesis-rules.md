# Project Synthesis Rules

## Objective

Convert discovery input into four canonical context files with clear ownership and minimal ambiguity.

Mandatory outputs:

- `ai/instructions/project-context.md`
- `ai/instructions/domain-map.md`
- `ai/instructions/feature-map.md`
- `ai/instructions/glossary.md`

## Synthesis principles

1. Prefer explicit decisions over vague prose.
2. Mark assumptions when evidence is incomplete.
3. Keep language consistent with chosen canonical vocabulary.
4. Separate facts, decisions, and open questions.
5. Do not duplicate the same rule in multiple files without reason.

## File contracts

### `project-context.md`

Must include:

- product identity and mission
- target users/actors
- shipped surfaces (v1)
- auth model summary
- tenancy/scope model
- capability and plan model (if any)
- non-goals and constraints

### `domain-map.md`

Must include:

- core entities and relationships
- bounded contexts and ownership boundaries
- domain events/state transitions (high level)
- canonical terminology for domain concepts

### `feature-map.md`

Must include:

- v1 feature list by surface
- primary flows and entry points
- API/contract touchpoints (at map level)
- gating matrix (role/capability/plan)
- deferred features/backlog boundaries

### `glossary.md`

Must include:

- canonical allowed terms
- forbidden terms/legacy synonyms
- term mapping notes when migration is needed

## Handling unknowns

If information is missing:

- include an "Assumptions" section
- include a "Pending decisions" section
- ensure missing items do not violate completion gate

## Quality bar before generation

Do not proceed to specialized generation until:

- the four files are coherent with each other
- auth/tenancy/surface decisions are explicit
- top workflows are represented
- glossary resolves naming conflicts
