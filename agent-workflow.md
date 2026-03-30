# Agent Workflow - Active Product

## Purpose

This file defines how coding agents execute work in the active product architecture:

- `web-providers`
- `backend-providers`

Rule files define what must be respected. This file defines how to execute safely.

## Mandatory companions

Read before meaningful implementation:

1. `ai/instructions/instructions.md`
2. `ai/instructions/project-context.md`
3. `ai/instructions/domain-map.md`
4. `ai/instructions/feature-map.md`
5. `ai/instructions/glossary.md`
6. `ai/instructions/product-rules.md`
7. `ai/instructions/backend-rules.md`
8. `ai/instructions/template-web-design-system.md` when changing `web-providers`

---

## Core principle

Do not jump into code because a request sounds obvious.

A good change preserves:

- domain clarity
- clean architecture
- backend-client contract integrity
- decision traceability
- operational UX clarity
- maintainability

## Master UX/UI rule (mandatory)

For any UI work in `web-providers` (components, pages, layouts, tables, cards, modals, forms, review flows, interaction states, copy), apply a reduction-first operational quality bar equivalent to top-tier product craft.

Non-negotiable expectations:

- clarity over ornament
- hierarchy over noise
- direct action over bureaucracy
- speed of comprehension and operation
- consistency across the full surface

UI must feel like a premium operational control surface, not a generic admin dashboard.

Before accepting a UI change, verify:

1. Can this be simplified without losing operational power?
2. Is the primary action obvious at first glance?
3. Does visual hierarchy guide the eye with minimal effort?
4. Is there any avoidable visual/textual noise?
5. Does the interaction improve decision speed and confidence?
6. Does this look and behave as one coherent system?

If any answer is weak, the UI is not ready.

---

## Active-domain principle

The source of truth is the active product domain, not the historical starter.

Before implementing, confirm:

- which entity and workflow step is affected (`proveedor`, `producto`, `intake`, `decision`, `exportacion`)
- whether the change touches `estado`, `decision`, `motivo`, or traceability
- whether the change belongs to `backend-providers`, `web-providers`, or both

---

## Standard execution sequence

1. Understand the request in domain language.
2. Identify affected workflow stage.
3. Identify affected layers (`backend-providers`, `web-providers`, cross-layer).
4. Read relevant files and existing patterns.
5. State the business rule in plain language.
6. Define contract impact (if any).
7. Implement safely.
8. Validate consistency and invariants.
9. Test/validate expected behaviors.
10. Run implementation audit when needed.
11. Update documentation when durable rules changed.
12. Report outcome and residual risks.

Do not skip steps.

## web-providers shared components gate (mandatory)

Before creating any **new** component under `web-providers/src/modules/**/components`:

1. Search `web-providers/src/components` (primitives under `ui/`, composed pieces at top level) for an existing reusable match.
2. If the UI is **not** domain-specific (no provider/product/decision vocabulary, no module-only hooks or services), it must **not** live under `modules/.../components`. Either reuse shared or extract to `web-providers/src/components` (or `components/ui/` for primitives).
3. Do not add silent duplicates (“almost the same” selects, text areas, file inputs, status pills, modals) in module folders.

A page or flow is **not** acceptable if it still reads like a generic starter, placeholder copy, or bureaucratic admin chrome on **active** operational surfaces.

Operational UX agents and skills must enforce this gate together with the master UX/UI rule.

---

## Rule — Contextual help per operational screen (mandatory)

Every **relevant operational screen** in `web-providers` must be evaluated for contextual help.

For primary airlock surfaces (at minimum: provider list, provider detail / curation desk, export surfaces, major intake flows):

- Expose a **visible help control** (icon or equivalent) that opens a **single reusable help pattern** (shared modal shell + structured sections), not ad-hoc paragraphs scattered in the layout.
- Help content must answer, in clear operational language: what the screen is for, which decisions happen there, how to run the flow correctly, what important actions mean, and what the operator should expect from the system.
- Do not ship one-off help modals per screen when the same shared pattern can carry screen-specific copy via props or module constants.

---

## Rule — Bulk / mass import flows (mandatory)

Any **mass import** (JSON batches, files, or equivalent) must be implemented as a **reusable operational flow**, not an isolated `input type="file"` with only a toast on failure.

The UX must include, as applicable:

- Clear description of the **expected file shape** (root array vs wrapper object, required fields, dedupe hints).
- Visible access to help (format + operational context).
- **Pre-submit validation** feedback (server validation errors listed, not only a count).
- Feedback that processing **started** (phase / progress, not silent spinners).
- **Reconciliation feedback** after persistence: if the API is synchronous, use explicit phases plus **post-write polling or refetch** of authoritative lists until the UI reflects the new batch (or a bounded timeout), so operators see “processing → synced.” If the API later becomes async, the same shell should accept a job-status poll without rewriting screens.
- **Outcome summary**: inserted counts, validation summary, conflict/dedupe messaging from the contract.
- **Provider mass import** must use the operational contract: summary insertable vs not insertable, errores con `code` y fila, inserción parcial explícita (`insert_valid_only`), lote `proveedores` persistido, listado y reversión segura en UI — no volver a un único “válido/inválido” opaco.
- Operational copy (Spanish product language per glossary); no starter placeholder text on active routes.

Orchestration belongs in **module hooks**; shared **presentation** belongs under `web-providers/src/components`. Route `page.tsx` files must not absorb bulk-import state machines.

---

## web-providers structural rule (mandatory)

A route is not accepted if `page.tsx` absorbs logic that belongs to module layers.

Required module-first split:

- `components/` for visual blocks
- `hooks/` for orchestration and stateful behavior
- `services/` for remote calls/contracts
- `types/` for shared module types
- `utils/` for pure transforms/parsers/formatters
- `constants/` for catalogs/config options

`page.tsx` must stay a thin route entrypoint that composes module pieces.

Immediate refactor triggers:

1. route file mixes remote orchestration, parsing, and full UI blocks
2. repeated inline handlers with business transitions
3. status/decision catalogs declared inside route files
4. helper functions inside render-heavy route files
5. route file becomes the only place where behavior can be understood

---

## Business rule check (mandatory)

Before coding, write the rule as:

- current behavior
- desired behavior
- blocking conditions
- traceability impact

If this cannot be stated clearly, implementation is premature.

---

## Cross-layer contract discipline

For backend-client work:

- backend defines contract truth
- all consumers must be updated
- errors must be classifiable and operationally meaningful
- avoid transitional ambiguity

Use `ai/skills/backend-app-contract-sync.skill.md` as needed.

---

## Airlock domain invariants (must hold)

- `estado` is snapshot, not explanation.
- `decision` is the operational event explaining state transitions.
- `motivo` is structured reason data, not optional decoration.
- `descartado` requires reason.
- `priorizado` and `aprobado` require at least one structured reason.
- `aprobado` is not `exportado`.
- export is allowed only from `listo_para_exportar`.
- `exportado` is reached only through the controlled export path (decision `exportar`), not via generic state PATCH.

---

## Implementation audit gate

Run an explicit audit for cross-layer, gating-sensitive, or state-machine changes:

1. real entrypoint and navigation continuity
2. contract alignment across all consumers
3. DTO/schema/persistence coherence
4. backend enforcement of critical rules
5. loading/blocked/error/success states in UI
6. traceability completeness (`quien`, `cuando`, `que_decision`, `por_que`)
7. validation commands executed and reported

Use:

- `ai/skills/implementation-release-audit.skill.md`
- `ai/agents/implementation-auditor.agent.md` when a formal verdict is needed

---

## Documentation update rule

When a durable domain rule changes, update:

- `ai/instructions/domain-map.md`
- `ai/instructions/feature-map.md`
- `ai/instructions/glossary.md`

Do not leave durable behavior documented only in code.

---

## Agent and skill map (active)

| Concern | Use |
|--------|-----|
| Domain workflow design | `ai/agents/domain-workflow-architect.agent.md`, `ai/skills/business-workflow-design.skill.md` |
| Contract sync | `ai/agents/contract-integrator.agent.md`, `ai/skills/backend-app-contract-sync.skill.md` |
| Operational UX | `ai/agents/operational-ux-guardian.agent.md`, `ai/skills/operational-ui-flow-builder.skill.md` |
| State traceability | `ai/skills/operational-state-traceability.skill.md` |
| Release audit | `ai/agents/implementation-auditor.agent.md`, `ai/skills/implementation-release-audit.skill.md` |

Template-hardening agents/skills are not active for this product phase.
