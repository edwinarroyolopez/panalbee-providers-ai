# Project Context - Panalbee Providers Airlock

## Identity

- **Product name**: Panalbee Providers Airlock
- **One-line value proposition**: Operational intake and curation layer that filters external supplier/product data before controlled output to Panalbee.
- **Primary users (v1)**: `admin` (single internal operational actor).
- **Product mission**: Reduce operational and data-quality risk by ensuring only reviewed, reasoned, traceable decisions move forward.

## Governance alignment

This file defines product-specific context only and must be applied together with:

- `ai/instructions/instructions.md`
- `ai/instructions/product-rules.md`
- `ai/instructions/backend-rules.md`
- `ai/instructions/template-web-design-system.md`

No base implementation rules are redefined here.

## Surfaces (v1)

- **Web (`web-providers`)**: Yes. Primary operational control surface.
- **Mobile app**: No (out of scope for v1).
- **Backend (`backend-providers`)**: Yes. Intake, validation, decision traceability, listing, and export support APIs.

## Auth model (v1)

- **Identity mechanism**: Internal auth.
- **Identity fields**: `telefono` + `password`.
- **Initial actor model**: Single `admin` user.
- **Forward compatibility**: Model must allow future internal users (operators/reviewers) without domain redesign.

## Tenancy and scope (v1)

- **Multitenancy**: Single-tenant internal.
- **Default scope**: One organization operating one airlock domain.
- **Future evolution**: Architecture should remain extensible for future multi-organizacion needs.

## Capability and plan model

- **v1 expectation**: No complex capability/plan matrix.
- **Current gate model**: State- and rule-driven operational gates (not tier-driven).
- **Explicit note**: Commercial plans/capabilities are not part of v1 product scope.

## Product intent and operating chain

The core product is a decision chain, not a generic CRUD admin:

1. Discover providers from external sources.
2. Intake providers via JSON.
3. Evaluate provider presence and potential.
4. Discard with required reason, or mark as fit for product scraping.
5. Intake products per provider via JSON.
6. Review products visually (cards + detail modal) for fast operational decisions.
7. Decide per product: prioritize, discard, approve.
8. Move approved products to `listo_para_exportar` and export in controlled modes.

## Non-goals and constraints (v1)

- Not an ecommerce storefront.
- Not the final Panalbee catalog.
- No direct Panalbee injection in v1.
- No provider external portal.
- No auto-approval assumptions for imported providers/products.
- Every operational decision must be traceable.

## Quality and UX direction

- Interface should be sober, premium, clear, and operational.
- Decision-taking must be fast and low-friction.
- Cards and modal-based workflows are first-class, not secondary.
- Avoid bureaucratic or noisy admin patterns.

## Assumptions (provisional)

- Session/token technical mechanism will follow implementation constraints, while preserving `telefono + password` identity model.
- Dedupe rules will be defined in implementation detail with conservative defaults and explicit collision reporting.

## Pending decisions (non-blocking)

- Final dedupe key composition for provider and product imports.
- Concrete API-level export contract details (shape/versioning).

## Links

- `ai/instructions/domain-map.md`
- `ai/instructions/feature-map.md`
- `ai/instructions/glossary.md`
