# Project Setup Completion Gate

## Purpose

Define when new-project setup is complete enough to begin real feature development safely.

Setup is complete only if all mandatory checks pass.

## Mandatory checks

### Identity and scope

- product identity and primary outcome are explicit
- v1 scope and explicit non-goals are documented
- target users/actors are identified

### Canonical synthesis artifacts

- `ai/instructions/project-context.md` exists and is coherent
- `ai/instructions/domain-map.md` exists and is coherent
- `ai/instructions/feature-map.md` exists and is coherent
- `ai/instructions/glossary.md` exists and is coherent

### Core architecture decisions

- auth model is explicit
- tenancy/scope model is explicit
- capability/plan gating expectations are explicit (or explicitly absent)
- shipped surfaces are explicit

### Workflow readiness

- top 3-5 core workflows are mapped
- at least one production-critical flow has clear entry point and boundaries
- key unknowns are either resolved or tracked as assumptions

### Generation discipline

- any additional `instructions/agents/skills/workflows` were created only with justification
- no duplicate/cosmetic governance files were added

## Failing conditions (cannot close setup)

- missing any of the four synthesis files
- contradictory terminology across files
- unresolved critical auth/tenancy/surface decisions
- inflation artifacts without clear reusable purpose

## Completion output format

When setup is complete, provide:

1. pass/fail result for each gate block
2. residual assumptions and risk notes
3. immediate next implementation lane (first feature slice)
