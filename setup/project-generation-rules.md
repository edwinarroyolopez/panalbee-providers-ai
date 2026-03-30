# Project Generation Rules

## Objective

Generate only necessary AI governance artifacts after synthesis, avoiding redundant or cosmetic files.

## Baseline generation (always)

Create/update the four canonical context files:

- `ai/instructions/project-context.md`
- `ai/instructions/domain-map.md`
- `ai/instructions/feature-map.md`
- `ai/instructions/glossary.md`

## Decision rules by artifact type

### Additional `ai/instructions/*.md`

Create when:

- a durable product rule is not covered by existing canonical instructions
- the rule affects repeated implementation decisions
- the rule is cross-layer and should be centralized

Do not create when:

- the rule is one-off
- it duplicates `instructions.md`, `product-rules.md`, `backend-rules.md`, or `app-rules.md`

### `ai/agents/*.md`

Create when all are true:

- there is a specialized decision pattern
- it recurs across multiple tasks
- it requires a stable review or design lens

Do not create when:

- behavior can be handled by existing workflow + instructions
- specialization is temporary or narrow to one ticket

### `ai/skills/*.md`

Create when all are true:

- there is a repeatable step-by-step recipe
- success criteria are clear and reusable
- multiple future tasks benefit from the same playbook

Do not create when:

- guidance is generic
- there is no reusable sequence

### `ai/workflows/*.md`

Create when:

- there is a multi-phase process requiring ordering/gates
- process touches multiple roles or layers
- completion conditions are explicit

Do not create when:

- workflow is just cosmetic reformatting of existing flow
- one instruction file can capture it adequately

## Anti-inflation checks (mandatory)

Before creating any non-baseline file, answer:

1. Which repeated decision does this file prevent from being improvised?
2. What existing canonical file is insufficient, specifically?
3. What is the smallest artifact that solves the gap?

If answers are weak, do not create the file.

## Naming and scope rules

- file names should reflect stable capability, not temporary projects
- each new file must declare purpose, triggers, and non-goals
- avoid overlap between agents, skills, and workflows
