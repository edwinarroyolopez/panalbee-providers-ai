# Glossary - Panalbee Providers Airlock

## Scope and alignment

This glossary defines canonical product language for UI, API, docs, and persistence naming.
It prevents domain drift and avoids importing misleading semantics from other systems.

## Canonical terms

| Term | Definition | Avoid confused with |
|------|------------|---------------------|
| `airlock` | Operational layer before Panalbee where data is filtered and curated. | Final catalog or storefront |
| `intake` | Controlled data entry into the airlock (with validation). | Direct insert without checks |
| `proveedor` | External supplier candidate under evaluation. | Approved final partner by default |
| `producto` | Candidate item associated to a provider and reviewed in airlock. | Already published catalog item |
| `estado` | Current lifecycle snapshot of an entity. | Decision history |
| `decision` | Traceable operational event taken by a user over an entity. | Mere status toggle |
| `motivo` | Structured reason code linked to a decision. | Unstructured notes only |
| `priorizado` | Marked as high-interest for follow-up, not yet final output. | Approved or exported |
| `aprobado` | Accepted in curation step, eligible to progress. | Exported |
| `listo_para_exportar` | Explicit pre-output state after approval. | Export completed |
| `exportado` | Successfully output through supported channel. | Approved without output |
| `curaduria` | Human-in-the-loop review and filtering process. | Raw ingestion |
| `descarte` | Decision to reject an entity with required reason(s). | Silent deletion |
| `trazabilidad` | Auditable record of who/when/what/why for decisions. | Generic logs without business meaning |
| `organization` | Internal scope record in API (`GET /auth/me`) for the single-tenant airlock; persisted historically as `Account` in Mongo. | Commercial customer account, billing profile, or multi-workspace tenant |
| `carga` / `lote` (intake) | Unidad de importación masiva con metadatos, resumen de validación e inserción; puede referirse a productos de un proveedor o a proveedores globales. | “Batch” opaco sin id ni historia |
| `inserción parcial` | Persistir solo filas válidas cuando el archivo mezcla errores, con `importMode: insert_valid_only` y conteos explícitos de omitidos. | Import silencioso a medias |
| `reversión de lote` | Eliminación explícita de los registros creados por una carga (proveedores), con comprobaciones de seguridad y marca de revocación en el lote. | Borrado genérico sin vínculo al intake |

## Decision types (producto)

Además de `aprobar`, `descartar`, `priorizar` y `marcar_listo_siguiente_paso`, el tipo **`exportar`** registra la transición **`listo_para_exportar` → `exportado`** solo mediante el endpoint de exportación controlada (no como toggle manual).

## Decision reason vocabulary

Decision reasons are structured codes plus optional free comment.

Example export batch reason codes:

- `salida_controlada_airlock`
- `lote_validado_para_panalbee`
- `revision_completa_y_coherente`
- `alineado_con_objetivo_comercial`

Example approval reason codes:

- `precio_muy_bajo`
- `alta_rentabilidad`
- `buena_presentacion_visual`
- `alineado_con_la_categoria`
- `alto_potencial_comercial`
- `diferenciacion_frente_a_otros`

Example operational reason codes (proveedor / intake):

- `carga_de_productos_registrada` — transición trazable del proveedor a `con_productos_cargados` tras un intake de productos válido (no aprueba productos).

Example discard reason codes:

- `precio_poco_competitivo`
- `baja_calidad_visual`
- `producto_poco_atractivo`
- `baja_confianza_en_el_proveedor`
- `informacion_incompleta`
- `no_alineado_con_el_catalogo_objetivo`

## Ambiguous/problematic terms (do not use as domain anchors)

- `CRUD de proveedores` as product definition.
- `catalogo final` for non-curated data.
- `publicado` when the intended meaning is `exportado`.
- `priorizado` as synonym of `aprobado`.
- `aprobado` as synonym of `exportado`.
- `importado` as synonym of `validado`.
- `descartar` implemented as silent delete.

## Naming discipline

- Keep domain terms stable across UI labels, API resources, and persistence fields.
- Prefer explicit state and decision names over generic `status`/`action` labels.
- If a new term is introduced, define it here before broad usage.
