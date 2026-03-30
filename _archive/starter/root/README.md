# AI starter governance

Este directorio (`ai/`) es el sistema de gobierno del starter.
Define como pensar, como decidir y como ejecutar cambios para que el producto escale con coherencia en `template-web`, `template-app` y `template-backend`.

## Para que sirve este starter

- Estandariza decisiones de producto, arquitectura y UX antes de escribir codigo.
- Reduce retrabajo al forzar descubrimiento de contexto y reglas reales.
- Evita drift entre backend, web y app con contratos y auditorias.
- Permite pasar de "idea" a "proyecto operativo" con artefactos concretos.

## Flujo recomendado (inicio rapido)

1. Leer `ai/starter.md`.
2. Ejecutar `ai/START_NEW_PROJECT.md`.
3. Seguir `ai/setup/start-new-project-flow.md` y su stack completo de `ai/setup/*.md`.
4. Generar artefactos minimos en `ai/instructions/`:
   - `project-context.md`
   - `domain-map.md`
   - `feature-map.md`
   - `glossary.md`
5. Entrar a ejecucion diaria con `ai/agent-workflow.md` + `ai/instructions/*.md`.

## Archivos raiz y su importancia

| Archivo | Rol | Importancia |
|---|---|---|
| `ai/starter.md` | Canon de arranque para proyecto nuevo. | Alinea que se hereda, que se revisa y que no se copia. |
| `ai/START_NEW_PROJECT.md` | Playbook operativo de inicializacion. | Evita empezar features sin contexto base. |
| `ai/agent-workflow.md` | Secuencia obligatoria de ejecucion. | Reduce cambios impulsivos y obliga validacion integral. |
| `ai/README.md` | Mapa de navegacion del sistema AI. | Acelera onboarding del equipo tecnico y de agentes. |

## instructions/: reglas del sistema

| Archivo | Para que se usa | Por que es clave |
|---|---|---|
| `ai/instructions/instructions.md` | Punto de entrada canonico. | Define orden de lectura y disciplina cross-layer. |
| `ai/instructions/product-rules.md` | Reglas de claridad de producto y decisiones funcionales. | Mantiene consistencia de negocio y lenguaje. |
| `ai/instructions/backend-rules.md` | Reglas de arquitectura, contratos y validacion backend. | Protege estabilidad y escalabilidad del backend. |
| `ai/instructions/app-rules.md` | Reglas de UX y sistema de interfaz mobile. | Evita deuda visual y flujos inconsistentes. |
| `ai/instructions/template-web-design-system.md` | Reglas de composicion y diseno web del starter. | Mantiene coherencia UI en web y reutilizacion real. |
| `ai/instructions/template-governance-rules.md` | Reglas para extraer/harden templates. | Separa reusable vs acoplado a dominio. |
| `ai/instructions/starter-semantics.md` | Semantica canonica del starter (workspace, account, etc). | Evita sinonimos ambiguos y errores de modelo mental. |
| `ai/instructions/project-context.template.md` | Plantilla para identidad y alcance del proyecto. | Base de decisiones de producto y arquitectura. |
| `ai/instructions/domain-map.template.md` | Plantilla de entidades, limites y vocabulario de dominio. | Reduce confusiones entre modulos y responsabilidades. |
| `ai/instructions/feature-map.template.md` | Plantilla de capacidades, superficies y prioridades. | Ordena roadmap y evita scope creep. |
| `ai/instructions/glossary.template.md` | Plantilla de glosario de terminos de producto. | Unifica lenguaje entre negocio, UX y codigo. |

## setup/: motor de descubrimiento y sintesis

| Archivo | Para que se usa | Por que es clave |
|---|---|---|
| `ai/setup/start-new-project-flow.md` | Flujo maestro de setup conversacional. | Coordina discovery -> sintesis -> generacion. |
| `ai/setup/project-discovery-interview.md` | Reglas para entrevistar al usuario/equipo. | Mejora calidad de requerimientos desde el inicio. |
| `ai/setup/project-discovery-question-bank.md` | Banco de preguntas para cubrir vacios de contexto. | Evita preguntas aleatorias y garantiza cobertura minima. |
| `ai/setup/project-synthesis-rules.md` | Reglas para transformar discovery en artefactos. | Convierte texto libre en decisiones accionables. |
| `ai/setup/project-generation-rules.md` | Politica para decidir que archivos generar. | Evita sobre-documentar o crear ruido innecesario. |
| `ai/setup/project-completion-gate.md` | Gate de readiness antes de construir features. | Previene arrancar sin base operativa suficiente. |

## agents/: especialistas para casos complejos

| Archivo | Especialidad | Valor principal |
|---|---|---|
| `ai/agents/contract-integrator.agent.md` | Integracion backend-cliente y contratos. | Reduce rupturas entre APIs y consumidores. |
| `ai/agents/domain-workflow-architect.agent.md` | Diseno de flujos de dominio. | Asegura flujos con sentido de negocio real. |
| `ai/agents/operational-ux-guardian.agent.md` | Coherencia UX operacional. | Mejora continuidad entre estados y acciones. |
| `ai/agents/specialization-context-architect.agent.md` | Modelado de perfiles/capabilities/contextos. | Escala personalizacion sin duplicar apps. |
| `ai/agents/implementation-auditor.agent.md` | Auditoria final de implementaciones. | Detecta huecos antes de release. |
| `ai/agents/template-system-architect.agent.md` | Arquitectura general de templates. | Define estructura reusable y limites claros. |
| `ai/agents/template-web-component-governor.agent.md` | Gobierno de componentes web template. | Sostiene consistencia y composicion del UI kit. |
| `ai/agents/template-contract-boundary-guardian.agent.md` | Fronteras de contrato y ownership de modulos. | Reduce acoplamiento accidental. |
| `ai/agents/template-release-auditor.agent.md` | Cierre de calidad para liberar template. | Disminuye riesgos al publicar starters. |

## skills/: procedimientos reutilizables de ejecucion

| Archivo | Uso | Beneficio directo |
|---|---|---|
| `ai/skills/backend-app-contract-sync.skill.md` | Sincronizar cambios de contrato backend/app/web. | Menos bugs por desalineacion de payloads. |
| `ai/skills/business-workflow-design.skill.md` | Diseñar y validar flujos de negocio. | Flujos mas claros y auditables. |
| `ai/skills/capability-profile-feature-gating.skill.md` | Definir gating por capability/perfil. | Control fino de acceso y monetizacion. |
| `ai/skills/dashboard-composition-by-profile.skill.md` | Componer dashboards por perfil. | UX contextual sin romper base comun. |
| `ai/skills/domain-vertical-modeling.template.skill.md` | Template para modelar verticales de dominio. | Reutilizacion guiada para nuevos sectores. |
| `ai/skills/finance-traceability-link.skill.md` | Trazabilidad entre eventos y finanzas. | Mejora auditoria y confianza operativa. |
| `ai/skills/implementation-release-audit.skill.md` | Checklist de release de implementacion. | Reduce issues post-release. |
| `ai/skills/operational-state-traceability.skill.md` | Trazar estados operativos end-to-end. | Facilita soporte e investigacion de incidentes. |
| `ai/skills/operational-ui-flow-builder.skill.md` | Construir flujos UI operacionales robustos. | Menos friccion en tareas criticas de usuario. |
| `ai/skills/domain-decoupling-pass.skill.md` | Desacoplar codigo especifico de dominio. | Hace el template mas reutilizable. |
| `ai/skills/public-component-showcase-design.skill.md` | Diseñar showcase de componentes publicos. | Acelera adopcion de componentes compartidos. |
| `ai/skills/reusable-component-extraction.skill.md` | Extraer componentes verdaderamente reutilizables. | Reduce duplicacion y deuda tecnica. |
| `ai/skills/template-folder-boundary-design.skill.md` | Definir fronteras de carpetas y ownership. | Mejora mantenibilidad y escalabilidad. |
| `ai/skills/template-optimization-pass.skill.md` | Optimizar template para performance y limpieza. | Baja costo de mantenimiento. |
| `ai/skills/template-readiness-audit.skill.md` | Auditar readiness general del template. | Permite liberar con criterio objetivo. |

## Ventajas de tener este sistema

- Alineacion total entre negocio, producto, backend y UX desde el dia 1.
- Menos errores por contratos rotos y por decisiones locales sin contexto.
- Onboarding mas rapido para devs y agentes AI por reglas y rutas claras.
- Capacidad de escalar a multiples perfiles o dominios sin rehacer arquitectura.
- Mejor calidad de release por gates, auditorias y checklists reutilizables.
- Reutilizacion real del starter, evitando copiar basura de proyectos anteriores.

## Nota de uso

`template-app/ai/README.md` esta marcado como deprecated.
La fuente canonica de gobierno AI es siempre `ai/` en la raiz del repo.
