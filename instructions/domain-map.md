# Domain Map - Panalbee Providers Airlock

## Scope and alignment

This map defines active domain structure and vocabulary boundaries for this product.
It complements, and does not duplicate, inherited implementation rules.

## Core entities

| Entity | Description | Owner scope |
|--------|-------------|-------------|
| `usuario` | Internal actor that authenticates and executes operational decisions. v1 starts with `admin`. | organization |
| `proveedor` | External supplier candidate entering the airlock for evaluation. | organization |
| `producto` | Candidate product associated to one provider, reviewed inside the airlock. | organization |
| `intake_lote` | Import batch metadata (kind `productos` \| `proveedores`, validation summary, errores detallados cuando aplica, actor, timestamps, revocación). | organization |
| `decision` | Auditable operational event taken over provider or product. | organization |
| `motivo` | Structured reason code used to justify a decision. | catalog (organization) |
| `exportacion` | Controlled output record for approved products (JSON/CSV in v1). | organization |

## Relationship model (high level)

- A `proveedor` can have many `producto` records.
- A `proveedor` and a `producto` can each receive many `decision` events.
- A `decision` references one or more `motivo` codes and optional comment.
- `intake_lote` groups import operations for providers/products and stores validation outcomes.
- Cargas de **proveedores** (`kind: proveedores`): sin `providerId` en el lote; cada proveedor insertado referencia el lote (`intakeLoteId`). Inserción puede ser total (`all_or_nothing`) o parcial (`insert_valid_only`) con resumen explícito.
- Reversión de lote de proveedores: elimina solo proveedores de esa carga, solo si siguen `ingresado` y sin productos; el documento de lote conserva `revokedAt` / `revokedByUserId`.
- `exportacion` groups products exported from `listo_para_exportar`.

## State model (snapshot layer)

### Provider states

- `ingresado`
- `en_evaluacion`
- `descartado`
- `apto_para_scraping`
- `con_productos_cargados`

### Product states

- `cargado`
- `priorizado`
- `descartado`
- `aprobado`
- `listo_para_exportar`
- `exportado`

## Operational event model (decision layer)

Decision types (applies to provider/product depending on context):

- `aprobar`
- `descartar`
- `priorizar`
- `marcar_listo_siguiente_paso`

Mandatory traceability payload per decision:

- `quien` (user id)
- `cuando` (timestamp)
- `que_decision` (typed action)
- `por_que` (one or more structured reasons + optional free comment)

## Core boundary: estado vs decision vs motivo

- `estado`: current snapshot of the entity lifecycle.
- `decision`: immutable operational event that explains why state changed (or why it was confirmed).
- `motivo`: structured reason code that semantically justifies a decision.

A state change without a supporting decision is invalid for governed transitions.

## Invariants and transition constraints

- `descartado` requires at least one `motivo`.
- `priorizado` requires at least one `motivo`.
- `aprobado` requires at least one `motivo`.
- `aprobado` does not imply `exportado`.
- `listo_para_exportar` is explicit intermediate state before export.
- Export operations can only consume products in `listo_para_exportar`.

## Bounded contexts

| Context | Owns |
|--------|------|
| Identity | Internal users and authentication (`telefono + password`); scope interno expuesto como `organization` en `GET /auth/me` (sin modelo comercial tier/billing en v1) |
| Intake | Provider/product JSON ingestion, validation, lot trace |
| Curation | Evaluation, decisions, reasons, state transitions |
| Output | JSON/CSV export orchestration and export traceability |

## Integrations

- External data sources (web research and scraping outputs) as upstream inputs.
- Panalbee direct injection is deferred (not v1 integration).

## Assumptions and pending decisions

- Final dedupe keys for provider/product imports remain implementation-level pending.
- Reason catalog governance process (who can edit reason sets) is deferred from v1.
