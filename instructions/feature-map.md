# Feature Map - Panalbee Providers Airlock

## Scope and alignment

This map defines v1 feature surfaces and flow boundaries for this product.
Implementation behavior remains governed by inherited rule files.
Architecture names in this project are `web-providers` (web surface) and `backend-providers` (API surface).

## Primary v1 flow chain (explicit)

1. Provider discovery happens outside the platform.
2. Provider intake enters the airlock through JSON validation + import.
3. Provider evaluation decides discard vs continue.
4. Product scraping happens outside the platform for accepted providers.
5. Product intake is loaded per provider via product JSON.
6. Product review happens inside the airlock (cards + detail modal).
7. Product decisions (`priorizar`, `descartar`, `aprobar`) are captured with reasons.
8. Approved products move to `listo_para_exportar`.
9. Controlled output (JSON/CSV) runs only from `listo_para_exportar`.

## Feature matrix

| Feature / flow | Surface | Backend area | Gate | Notes |
|----------------|---------|--------------|------|-------|
| Admin authentication | Web | Auth | `admin` login | `telefono + password` |
| Provider JSON validation/import | Web | Intake (providers) | Authenticated `admin` | Validación enriquecida (totales, insertables, códigos por fila); import `all_or_nothing` (histórico) o `insert_valid_only`; lote `proveedores` + listado/reversión segura |
| Provider listing/filter/pagination | Web | Providers query | Authenticated `admin` | Operational filtering, growth-ready; contextual help + bulk JSON import shell (phased UX, reconcile refetch) |
| Provider evaluation decision | Web | Curation (providers) | Decision invariants | Discard requires structured reason |
| Provider detail view | Web | Providers + curation read | Authenticated `admin` | Includes product intake entrypoint; contextual help; product bulk import shell |
| Product JSON validation/import per provider | Web | Intake (products) | Provider context + auth | Products enter as `cargado` (non-approved); `intake_lote` persisted |
| Product cards review | Web | Products query | Authenticated `admin` | Fast scan + inline decision actions |
| Product detail modal review | Web | Products + decisions | Authenticated `admin` | Context-rich decision path |
| Product decision capture | Web | Curation (products) | Decision invariants | Prioritize/approve/discard require reason rules |
| Export JSON/CSV | Web | Output/export | State gate + trazabilidad | Solo `listo_para_exportar`; descarga real; registro `ProductExport`; transición a `exportado` con decisión `exportar` |

## Navigation map (web v1)

- Authenticated root: operational dashboard/list view.
- Providers list route: filtering + pagination + intake actions.
- Provider detail route: provider profile + product intake + product review surface.
- Export route/panel: export operations over eligible products.

## API map (contract level)

Base path: `/api`

| Area | Responsibilities | Auth | Notes |
|------|------------------|------|-------|
| Auth | Login, JWT, `GET /auth/me` | Public login, protected rest | JWT: `sub`, `phone`, `role`, `accountId` (scope interno). `me`: `user` + `organization` + `stats.activeMembers` — sin tier, billing, workspaces ni capabilities comerciales |
| Intake providers | Validate/import provider JSON; listar/revertir lotes de proveedores | Protected | Lote `kind: proveedores`; trazabilidad y reversión condicionada |
| Providers | List/filter/detail/state snapshot | Protected | Snapshot data with linked decisions |
| Intake products | Validate/import product JSON by provider; optional intake lot listing | Protected | Rejects auto-approval assumptions; batch trace |
| Products | List/filter/card payload/detail payload; per-product state with decisions | Protected | Optimized for fast operational review |
| Decisions | Create/read decision events + reasons | Protected | Traceability mandatory fields |
| Exports | Generate JSON/CSV from eligible set | Protected | Solo `listo_para_exportar`; transacción + decisión `exportar`; JSON incluye `meta.exportRecordId`, motivos y `actorUserId`; cabeceras `X-Export-Id`, `X-Exported-Count` |

## Gate model (v1)

- Role matrix: single `admin` operational actor.
- Operational gates: state + decision invariant enforcement.
- Export gate: only products currently in `listo_para_exportar` are exportable.

## Explicit out of scope (v1)

- Direct Panalbee injection.
- Multi-user internal assignment workflows.
- Advanced reviewer metrics dashboards.
- Commercial plan/tier feature gating.
