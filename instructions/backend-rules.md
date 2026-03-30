# Backend Engineering Rules - backend-providers

## 1. Backend role

`backend-providers` is the source of truth for:

- domain invariants
- traceability
- access control
- API contracts consumed by `web-providers`

No critical rule may depend only on frontend behavior.

---

## 2. Active domain model priority

Backend design must prioritize:

- `estado` as current snapshot
- `decision` as immutable operational event
- `motivo` as structured reason data
- `trazabilidad` as mandatory audit trail

Do not collapse these concepts into a single generic status update.

---

## 3. Active architecture and scope

- v1 scope is single-tenant internal (one organization).
- v1 actor model starts with `admin`.
- Auth identity is `telefono + password`.

Do not model `account/workspace/tier/billing` as backend defaults in v1.

---

## 4. Module boundaries

Organize by bounded contexts aligned with the active domain:

- `auth`
- `users`
- `providers`
- `products`
- `intake`
- `decisions`
- `exports`

Recommended structure per module:

```txt
src/
  <module>/
    <module>.module.ts
    <module>.controller.ts
    <module>.service.ts
    dto/
    schemas/
    guards/
    constants/
    utils/
```

Keep controllers thin; keep business rules in services.

Controller smell triggers immediate refactor:

1. transition or validation logic duplicated in controllers
2. payload transformation beyond basic request mapping
3. orchestration of multiple domain actions inside controller methods

---

## 5. Validation and intake integrity

- Validate every JSON intake payload before persistence.
- Persist validation outcomes with batch (`intake_lote`) trace.
- Reject silent partial inserts without explicit outcome reporting: la inserción parcial de proveedores debe usar `importMode: insert_valid_only`, devolver `insertedCount` / `skippedCount` y persistir el lote con resumen coherente.
- Errores de validación de importación proveedores: clasificar con `code`, `blocksRecord` y agregar por fila; el cliente debe poder calcular insertables vs no insertables.
- Reversión de lote de proveedores: transacción o reglas equivalentes; no eliminar proveedores de otras cargas; bloquear si hay estado distinto de `ingresado` o productos vinculados.
- Keep DTO/schema constraints aligned with domain invariants, not temporary UI convenience.

---

## 6. Decision and state invariants

Backend must enforce at least:

- `descartado` requires structured reason(s)
- `priorizado` requires at least one structured reason
- `aprobado` requires at least one structured reason
- `aprobado` does not imply `exportado`
- export eligibility requires `listo_para_exportar`

Any transition violating these rules must fail with structured errors.

---

## 7. Traceability contract

Every governed decision must persist:

- `quien`
- `cuando`
- `que_decision`
- `por_que` (reason codes + optional comment)

No destructive or high-impact state transition should be accepted without traceability.

---

## 8. API contracts

Contracts must be explicit, stable, and classifiable:

- predictable response shapes
- stable naming
- typed decision and state enums
- reason codes as structured values
- errors mapped by class (`validation`, `forbidden`, `conflict`, `not_found`, `internal`)

Clients must not infer business meaning from ambiguous payloads.

---

## 9. Persistence discipline

- stable field names
- timestamps for audit-sensitive records
- indexes based on real query patterns
- keep event-like decision history append-safe
- do not model persistence around one screen only

---

## 10. Access control

v1 has a simple actor model, but backend enforcement is still mandatory:

- authenticated `admin` is required for protected operations
- state-sensitive operations must be backend-gated
- export endpoints must enforce eligibility states

Do not rely on hidden buttons as access control.

---

## 11. Error handling

Differentiate at minimum:

- validation errors
- unauthorized/forbidden
- not found
- conflict/invalid transition
- export eligibility block
- internal failure

Error payloads must support operational UI messaging.

---

## 12. Testing priorities

Prioritize:

1. service-level invariants for state/decision/motivo
2. intake validation and dedupe behavior
3. guarded transitions and forbidden transitions
4. export eligibility checks from `listo_para_exportar`
5. cross-layer contract compatibility with `web-providers`

---

## 13. Cross-layer release gate

Backend work that changes behavior is complete only if:

1. DTO validation matches real domain rules
2. routes and parameters are explicit
3. services enforce invariants
4. persistence captures state and decision trace correctly
5. client compatibility is confirmed
6. blocked responses are structured for clear UX

No backend feature is complete if `web-providers` cannot interpret it safely.
