# Instructions - Panalbee Providers Airlock

## Purpose

This is the entry point for any human or coding agent working on the active product:

- `web-providers`
- `backend-providers`

The governance center is the active domain files, not the historical starter context.

## Mandatory reading order

Before implementing:

1. `ai/instructions/instructions.md` (this file)
2. `ai/instructions/project-context.md`
3. `ai/instructions/domain-map.md`
4. `ai/instructions/feature-map.md`
5. `ai/instructions/glossary.md`
6. `ai/instructions/product-rules.md`
7. `ai/instructions/backend-rules.md`
8. `ai/instructions/template-web-design-system.md` for web UI work in `web-providers`
9. `ai/agent-workflow.md`

---

## Active architecture and scope

- Surface: `web-providers`
- API/backend: `backend-providers`
- Tenancy: single-tenant internal (v1)
- Actor model (v1): `admin` only
- Auth (v1): `telefono + password`

Do not introduce multi-tenant, billing, or plan-tier complexity unless explicitly requested in a later phase.

---

## Domain-first rule

Treat the system as an operational airlock with this chain:

1. intake de proveedores
2. evaluacion y curaduria
3. intake de productos por proveedor
4. decisiones operativas trazables
5. salida controlada por exportacion

Do not reduce this product to generic CRUD behavior.

## Master UX/UI rule (non-negotiable)

In this product, UX is part of the domain.

Every UI decision in `web-providers` must support fast, confident operational decisions with minimum cognitive load. "Correct" but generic, noisy, or bureaucratic UI is not acceptable.

Required quality bar:

- sober, precise, premium operational look
- strong visual hierarchy and reduced friction
- obvious primary actions close to context
- concise, operational copy (no empty corporate language)
- coherent states (loading, empty, blocked, error, success)

Acceptance questions (mandatory):

1. Is the main action immediately clear?
2. Is there removable noise in layout, copy, or controls?
3. Does the screen help decide faster and better?
4. Do cards/modals/tables feel intentional and consistent?
5. Is beauty coming from order and proportion, not decoration?

If any answer is uncertain, iterate before shipping.

---

## Cross-layer implementation rule

Every meaningful change must answer:

1. Which domain step does this change improve?
2. Which entities are affected?
3. Is `estado`, `decision`, `motivo`, or traceability impacted?
4. What backend-client contracts change?
5. What must be enforced on backend (not UI-only)?
6. What user-facing state/feedback changes in `web-providers`?
7. How will it be validated?

If these answers are unclear, stop and clarify before coding.

## Shared components and reuse (web-providers, mandatory)

1. **Inventory first:** Before adding a component inside `web-providers/src/modules/<module>/components`, inspect `web-providers/src/components` (including `components/ui/`).
2. **Placement:** If the piece is domain-agnostic (could serve more than one surface without importing module services/hooks/types), it belongs in shared `components/`, not inside a module.
3. **No silent duplication:** Do not fork another select, modal shell, file input, textarea, or badge “because it is faster.” Extend shared primitives or compose them.
4. **Quality bar:** A screen is not “done” if it still feels like the historical starter: generic marketing, placeholder English, template metadata, or noisy layout on routes that operators use daily.
5. **Contextual help:** Primary operational screens must expose a consistent help entry point (shared modal pattern) with structured, operational copy—not improvised tooltips as the only documentation.
6. **Mass imports:** Bulk JSON/file intake must use the shared bulk-import operational pattern: format explanation, validation errors visible, phased feedback, post-persist reconciliation (refetch/poll as appropriate), and outcome summary. Thin file inputs alone are insufficient.

This rule applies to all UI tasks, including those driven by UX/UI agents and skills.

---

## Frontend architecture discipline (web-providers)

In `web-providers`, route files are orchestration entrypoints, not behavior containers.

Mandatory rule:

> A route is structurally invalid if `page.tsx` contains logic that should live in `hooks`, `components`, `services`, `types`, `utils`, or `constants`.

Minimum expected split for relevant surfaces:

- data orchestration and state transitions -> module hooks
- remote calls and payload contracts -> module services
- reusable visual sections -> module components
- pure transforms/parsers/formatters -> module utils
- static options/reason catalogs/status maps -> module constants

If a UI works but structure is disordered, it does not meet product quality.

---

## Airlock invariants (non-negotiable)

- Decision events are mandatory for governed transitions.
- No `descartado` without structured reason.
- No `priorizado` or `aprobado` without structured reason.
- `aprobado` does not imply `exportado`.
- Only `listo_para_exportar` can move to export via the export API; `exportado` is not a manual toggle.
- Decision traceability always captures `quien`, `cuando`, `que_decision`, `por_que`.

---

## Implementation quality rule

A change is not complete because it compiles.

It is complete when:

- domain intent is preserved
- backend rules enforce truth
- contracts are coherent in all consumers
- UI states are clear and operational
- traceability is complete where required

Use `ai/agent-workflow.md` audit gate for closure.

---

## Canonical governance locations

Source of truth in this repository:

- `ai/agent-workflow.md`
- `ai/instructions/*.md`
- `ai/agents/*.agent.md`
- `ai/skills/*.skill.md`

If a file conflicts with active domain files, active domain files win.
