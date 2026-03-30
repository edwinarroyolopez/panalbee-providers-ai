# web-providers - design system and operational UI bar

## Master UX/UI rule (mandatory)

`web-providers` must feel like a premium operational curation console.

Not acceptable:

- generic admin look
- dense bureaucratic tables
- component collage without intention
- decorative noise competing with decisions

Required:

- sober and precise visual language
- reduction-first composition
- clear hierarchy and spacing
- fast scan and fast action
- consistent and calm interaction states

## Canonical location

- **Primitives:** `web-providers/src/components/ui/` (Button, Input, Card, Select, TextArea, FileInput, ...)
- **Composed reusables:** `web-providers/src/components/<Name>/` (Modal, SideNav, StatusPill, ImageUpload, ...)
- **Domain components:** `web-providers/src/modules/<module>/components` — only when the component **depends** on domain types, copy, hooks, or services specific to that module
- **Public showcase (optional):** `web-providers/src/app/system-design/` (no auth, mock/demo data, `noindex`)

### Mandatory reuse workflow

1. Implementing or changing UI → open `web-providers/src/components` and match existing primitives/compositions first.
2. If you need a variant → extend the shared primitive or add a thin wrapper in shared space; avoid parallel implementations under `modules/`.
3. If the new piece is reusable across modules and has no domain coupling → place it under `web-providers/src/components` (not under `modules/.../components`).

### Page acceptance (operational surfaces)

A page on an active operational route fails review if:

- it visually or verbally resembles the historical starter (template titles, placeholder English, generic “admin table” with no hierarchy),
- it introduces duplicate controls that already exist in shared components,
- or it violates the master UX/UI rule (generic, bureaucratic, or mediocre instead of sober, precise, premium operational craft).

## Route and module boundaries (mandatory)

- Route `page.tsx` files compose module pieces; they do not host full behavior.
- If a screen needs remote orchestration, create a module hook.
- If a block can be reused or separately reasoned about, extract a module component.
- Keep catalogs/options/status mappings in module constants.
- Keep parsing/formatting and pure transforms in module utils.

Practical thresholds to extract from a route file:

1. More than one async mutation/query flow
2. More than one modal with dedicated behavior
3. More than one status/decision catalog
4. Repeated inline handlers for state transitions
5. Large styled-component blocks mixed with orchestration

## UX criteria by surface

### Cards

- Prioritize rapid scan and immediate signal.
- Keep high-frequency actions close to the card context.
- Avoid decorative cards or card-as-form anti-patterns.

### Modals

- Increase decision depth without breaking operational rhythm.
- Show only what materially improves decisions.
- Avoid turning modals into overloaded pseudo-pages.

### Tables

- Keep only decision-relevant columns.
- Preserve whitespace and readability.
- Support sustained operation without visual fatigue.

### States and badges

- Status meaning must be immediate at a glance.
- Use consistent semantics and visual mapping across routes.
- Avoid ambiguous color/label combinations.

### Actions

- Primary actions must be visible and unambiguous.
- Important actions cannot be visually timid or hidden.
- Placement must follow operational frequency and context.

### Copy

- Short, clear, operational, human.
- No unnecessary technical wording.
- No inflated or empty corporate text.

## Unified modal policy

- Keep one canonical modal component in shared components.
- Module-level modals should converge to canonical modal unless a domain-specific behavior requires a controlled exception.

## Component policy

- Do not duplicate overlays or wrappers without behavior value.
- **Reuse is mandatory before creating new variants** of selects, text areas, file inputs, status chips, cards shells, or modal frames.
- Shared components stay behavior-light; domain logic stays in module features.
- Preserve naming aligned with `ai/instructions/glossary.md`.
- UX/UI agents and skills must treat `web-providers/src/components` as the first stop in every UI task.

## Reduction and acceptance gate

Before accepting UI work, ask:

1. Can we simplify further without losing operational power?
2. Is the primary action obvious instantly?
3. Does hierarchy guide the eye without effort?
4. Is there redundant visual/textual noise?
5. Does this improve decision speed and confidence?
6. Does this feel inevitable instead of merely correct?

If any answer is weak, iterate.

---

## Contextual help pattern (operational screens)

- Use the **shared** help trigger + modal (`web-providers/src/components/OperationalHelp` or successor) with the canonical `Modal` shell.
- One reusable pattern; screen-specific content via props or module-local constants (sections: purpose, decisions, how to operate, actions, expectations).
- Help must be **discoverable** (visible icon/control near the screen title or primary context), not buried.

## Bulk import pattern (mass intake)

- Compose `ui/FileInput` (or button + hidden input) inside the shared **bulk import panel**; do not leave a raw file input as the only affordance on operator routes.
- Always show: expected format, link/button to format help, validation error list from the server, phase/progress (read → validate → persist → reconcile), and result summary.
- When the contract supports **partial insert** (p. ej. proveedores), the panel debe ofrecer fase de **decisión** clara: totales insertables / no insertables, detalle por fila (código + mensaje), CTA primaria “insertar solo válidos” y salida “descartar archivo”; el archivo no se puede sustituir hasta cerrar esa decisión.
- After a successful write, run **bounded reconciliation** (refetch or poll list/lote endpoints) so the operator sees data catch up—especially when the API is synchronous today and may become async later.
- Surfaces con lotes reversibles (proveedores): historial de cargas y acción de reversión con confirmación explícita (p. ej. frase o equivalente), copy operacional en español.
- Domain-specific parse/validate/import calls stay in **module hooks**; the visual shell stays shared.

---

## Public / trust pages

Legal-adjacent public routes (`privacy`, `data-deletion`, etc.) must use **product-accurate** copy for Panalbee Providers Airlock (internal operational tool, single-tenant, no consumer storefront fiction). Starter placeholder lines (“plantilla genérica”, “texto placeholder”) are not acceptable on a live product surface.
