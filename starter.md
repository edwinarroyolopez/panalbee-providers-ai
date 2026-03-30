# Starter Canon (new-project entry)

## Purpose

This starter is a reusable base to launch a new product with a shared AI governance system.

It includes:

- canonical implementation rules (`ai/instructions/*.md`)
- execution workflow (`ai/agent-workflow.md`)
- reusable specialized guidance (`ai/agents/*.agent.md`, `ai/skills/*.skill.md`)
- setup engine for new projects (`ai/setup/*.md`)

Use this file as the first context when the user says: "vamos a empezar un proyecto nuevo".

## Canonical vs review-required inheritance

Inherit by default:

- `ai/instructions/instructions.md`
- `ai/instructions/product-rules.md`
- `ai/instructions/backend-rules.md`
- `ai/instructions/app-rules.md`
- `ai/agent-workflow.md`
- `ai/START_NEW_PROJECT.md`
- `ai/setup/*.md` (this setup engine)

Inherit with product review (adapt, do not copy blindly):

- `ai/instructions/project-context.template.md`
- `ai/instructions/domain-map.template.md`
- `ai/instructions/feature-map.template.md`
- `ai/instructions/glossary.template.md`
- `ai/agents/*.agent.md`
- `ai/skills/*.skill.md`

Do not inherit without explicit decision:

- legacy/example domain copy
- routes/modules not used by the product
- context-specific workflows created for a previous product

## What "start a new project" means

Starting a new project is not just cloning and wiring envs. It is a guided discovery + synthesis + generation process:

1. collect free-form business/product prose
2. extract what is already clear
3. ask only minimal missing questions
4. synthesize canonical project context artifacts
5. generate only the necessary AI governance files

## Required outputs for a new project

Minimum outputs expected before feature work:

- `ai/instructions/project-context.md`
- `ai/instructions/domain-map.md`
- `ai/instructions/feature-map.md`
- `ai/instructions/glossary.md`

Optional outputs (only when justified):

- additional `ai/instructions/*.md`
- specialized `ai/agents/*.md`
- reusable `ai/skills/*.md`
- execution `ai/workflows/*.md`

## Setup engine

Detailed operational behavior lives in:

- `ai/setup/start-new-project-flow.md`
- `ai/setup/project-discovery-interview.md`
- `ai/setup/project-discovery-question-bank.md`
- `ai/setup/project-synthesis-rules.md`
- `ai/setup/project-generation-rules.md`
- `ai/setup/project-completion-gate.md`

Use them as a coordinated system, not as isolated checklists.
