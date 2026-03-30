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

- **Primitives:** `web-providers/src/components/ui/` (Button, Input, Card, ...)
- **Composed reusables:** `web-providers/src/components/<Name>/` (Modal, SideNav, ImageUpload, ...)
- **Domain components:** `web-providers/src/modules/<module>/components`
- **Public showcase (optional):** `web-providers/src/app/system-design/` (no auth, mock/demo data, `noindex`)

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
- Shared components stay behavior-light; domain logic stays in module features.
- Preserve naming aligned with `ai/instructions/glossary.md`.

## Reduction and acceptance gate

Before accepting UI work, ask:

1. Can we simplify further without losing operational power?
2. Is the primary action obvious instantly?
3. Does hierarchy guide the eye without effort?
4. Is there redundant visual/textual noise?
5. Does this improve decision speed and confidence?
6. Does this feel inevitable instead of merely correct?

If any answer is weak, iterate.
