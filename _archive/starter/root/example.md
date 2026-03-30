Vamos a empezar un proyecto nuevo.

Usa primero:
- `ai/starter.md`
- `ai/START_NEW_PROJECT.md`
- `ai/setup/start-new-project-flow.md`
- `ai/setup/project-discovery-interview.md`
- `ai/setup/project-synthesis-rules.md`
- `ai/setup/project-generation-rules.md`
- `ai/setup/project-completion-gate.md`

Quiero que sigas el flujo de setup conversacional del starter:
1. primero analiza mi prosa libre del negocio
2. luego resume lo que entiendes
3. luego hazme solo las preguntas faltantes
4. después sintetiza los archivos base del proyecto
5. y solo si aplica, genera `ai/instructions/*.md`, `ai/agents/*.md`, `ai/skills/*.md` y `ai/workflows/*.md`

Aquí va la descripción del proyecto:

Estamos creando una plataforma SaaS para talleres de reparación de celulares.
El objetivo es que un taller pueda registrar equipos recibidos, estados de reparación, repuestos usados, pagos parciales y entregas finales.
Habrá una app para recepción rápida en mostrador y una web para administración.
Cada negocio tendrá su propia cuenta y dentro de ella podrá manejar varias sucursales o estaciones de trabajo.
Necesitamos autenticación con roles.
Probablemente existirán capabilities para funciones premium como reportes avanzados, historial fotográfico por equipo y exportaciones.
Los usuarios principales serán dueño, administrador, técnico y recepcionista.
El flujo principal comienza cuando entra un celular al taller: se registra, se diagnostica, se aprueba el costo, se repara, se cobra y se entrega.
Quiero que el sistema sea claro, operativo y muy fácil de usar.

Empieza por decirme:
- qué ya entendiste
- qué entidades detectas
- qué superficies detectas
- qué decisiones parecen claras
- qué vacíos faltan por resolver

Después hazme solo las preguntas mínimas necesarias para completar el setup.
