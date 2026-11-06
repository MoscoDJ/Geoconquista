# ADR-000 — Gobernanza documental y reglas para agentes

| Campo | Valor |
|---|---|
| Estado | `APROBADO` |
| Fecha | 2026-11-05 |
| Aprobador | Creador, 2026-11-05 (G0) |
| Origen | Plan de arranque, DEC-09 y §4.4 (G-1 a G-9) |

## Contexto

El proyecto heredó tres juegos de convenciones que se contradicen: el brief (`Contexto/GEOCONQUISTA_BRIEF_DEBATE.md` §11), el suplemento `Contexto/gobernanza/extras.md` y el paquete de Cursor (`Contexto/gobernanza/cursor-doc-first-skill-pack-original/`). El plan de arranque (`docs/roadmap/plan-de-arranque.md` §4.4) registró nueve conflictos, G-1 a G-9, y recomendó adoptar el paquete de Cursor corregido (DEC-09).

Hay tres hechos más que este ADR también debe cubrir:

- El desarrollo se hace con agentes de programación desde Visual Studio Code: Claude Code y cualquier otro que lea `AGENTS.md` (D-05). Unas reglas repetidas en varios archivos acabarían divergiendo.
- El creador decidió no hacer prototipo en papel (D-01). Eso adelanta el código del motor y hace todavía más importante que no se programen reglas sin aprobar.
- El creador pidió que el agente genere y edite el kit gráfico y sonoro (D-04). Eso introduce activos generados con IA, que necesitan trazabilidad y licencia.

## Decisión

### 1. Una sola fuente de reglas para agentes
`AGENTS.md`, en la raíz, contiene todas las reglas. `CLAUDE.md` lo importa. El procedimiento vive en una sola skill, `.claude/skills/documentation-first/SKILL.md`. No hay configuración de Cursor: el creador trabaja en Visual Studio Code (D-05), y la del paquete heredado no se instala. Los archivos `AGENTS.md` y `CLAUDE.md` de la app de debate se movieron a `Contexto/debate-app/`, porque son instrucciones para los participantes del debate y no para trabajar en este repositorio.

### 2. Precedencia por estado (resuelve G-1)
Se descartan los dos órdenes fijos por carpeta: el de `extras.md` (gameplay primero) y el del paquete (specs primero). Rige el criterio de `AGENTS.md` §3: `APROBADO` prevalece sobre `PROPUESTO`, y entre dos documentos aprobados prevalece el más reciente solo si cita al anterior. Cualquier otro conflicto bloquea la implementación.

### 3. IDs (resuelve G-2)
`FS-###`, `AC-###.#`, `ADR-###`, `D-###`, `CARD-<tipo>-###` y `EVT-###`.

**Ajuste sobre DEC-09:** las cartas usan el **tipo** (`hacienda`, `migracion`, `correo`, `mensajeria`, `verdad`, `reto`) y no el modo. Una carta puede pertenecer a varios modos (campo `modos[]`), y un ID por modo la duplicaría. Los AC provisionales del plan (`AC-CORE-01`, `AC-PRIV-01`, etc.) se renumeran como `AC-###.#` en E3, cuando cada uno quede asignado a su spec.

### 4. Árbol documental (resuelve G-3)
El árbol del brief §11.2, más los siguientes documentos:

- `docs/decisions/ADR-000-gobernanza.md` (este documento).
- `docs/gameplay/parameters.md`: todas las cifras de las reglas v0 (D-01).
- `docs/testing/acceptance-matrix.md`.
- `docs/assets/art-direction.md`, `audio-direction.md` y `pipeline.md` (D-04).
- `docs/roadmap/plan-de-arranque.md`: copia vigente del plan. El original del debate queda archivado en `Contexto/plan.md` y no se vuelve a editar.

No se copian los archivos stub del paquete de Cursor (`game-loop.md`, `modes.md`, `host-screen.md`, `system-overview.md`, etc.).

### 5. Modo de parejas (resuelve G-4)
`parejas_18`.

### 6. Visibilidad (resuelve G-5)
Cuatro niveles: `público`, `propietario`, `partes_tratado` y `sistema`. Se descartan `public/private/admin` de `extras.md` y el nivel `moderador` del brief §9.4, porque moderar no da acceso a secretos (DEC-06).

### 7. Estructura de código (resuelve G-6, G-7 y la observación 1 del consolidador)
La estructura de `apps/`, `packages/` y `tools/` es la del plan §6.3. **Se crea solo tras la puerta G3.** Así se resuelve la diferencia entre «tras ADR-001» (§6.3) y «hasta G3» (§7.1): rige la condición más tardía. Se elimina la instrucción del paquete «Si aún no existen, propón y crea esta estructura base».

### 8. Sin premisas técnicas en las reglas (resuelve G-8)
Las reglas para agentes no dan por hechos ni Flutter ni la Raspberry Pi. El stack se decide en ADR-001 y la pantalla pública en ADR-002.

### 9. Contrato de salida único (resuelve G-9)
Se usan los cinco puntos de `AGENTS.md` §5, con los estados `LISTO_PARA_IMPLEMENTAR`, `FALTA_DOCUMENTACION` y `HAY_CONFLICTO_DOCUMENTAL`. Desaparece el formato de cuatro bloques de la regla `.mdc` original. El contrato aplica a las tareas que cambian código, specs, contenido o activos, no a preguntas ni explicaciones.

### 10. Excepciones autorizadas antes de G3
- **Spikes técnicos (E2):** código desechable en ramas `spike/<id>` que nunca se fusionan. Solo sus mediciones y conclusiones pasan a ADR-001 y ADR-002.
- **Exploración de arte y audio:** pruebas de estilo y variantes en `exploracion/`, carpeta ignorada por git. Nada de ahí se usa en el producto hasta que la dirección de arte o de audio esté aprobada y un documento de UX pida el activo.

### 11. Secretos y activos generados
Las claves de API van solo en `.env`, que está ignorado por git. Cada activo de `assets/` tiene una entrada en `assets/manifest.json` con su origen y los términos de licencia aplicables (`docs/assets/pipeline.md`).

### 12. Documentación bilingüe (D-29, añadido el 2026-11-06)

- El **español es la versión canónica**: los documentos se escriben, se revisan y se aprueban en español. Si la traducción dice algo distinto, manda el español.
- Cada documento tiene su traducción al inglés en un archivo hermano: `core-loop.md` → `core-loop.en.md`. La traducción empieza con una nota que enlaza el original y recuerda que manda el español.
- Todo cambio en un documento en español actualiza su `.en.md` **en el mismo commit**. Una traducción desactualizada se trata como un fallo de documentación.
- Los estados (`APROBADO`, `PROPUESTO`…), los IDs y los identificadores de datos no se traducen.
- Se traduce todo salvo `docs/roadmap/plan-de-arranque.md`, que queda como archivo histórico en español, y `Contexto/`.

### 13. Definition of Ready y Definition of Done
- **DoR:** la de `extras.md` §1, más dos condiciones: que la spec esté `APROBADO` y que cite la regla v0, o el resultado del simulador o de una sesión, que la respalda.
- **DoD:** el código implementa solo lo documentado, cada AC tiene una prueba que pasa, la fila de `acceptance-matrix.md` está actualizada y no queda ninguna decisión «solo en código».

## Alternativas consideradas

- **Adoptar `extras.md` como base.** Le falta el flujo operativo para el agente y su modelo de visibilidad es insuficiente.
- **Adoptar el paquete de Cursor sin corregir.** Llevaría al agente a crear la estructura antes de tiempo, a usar `couples_18` y a asumir Flutter, en contra del brief.
- **Mantener reglas separadas por herramienta (una copia por agente).** Duplicarlas garantiza que diverjan con el tiempo.

## Consecuencias

- **Positivas:** un solo lugar para cambiar las reglas; los agentes no pueden crear código de producto antes de G3; los activos generados quedan trazables para la publicación open source.
- **Negativas:** el contrato de cinco puntos añade fricción a cada tarea. Los activos requieren mantener el manifiesto.

## Aprobación

- El creador aprobó G0 el 2026-11-05: este ADR, `docs/product/vision.md` y `docs/roadmap/milestones.md`.
- `Contexto/` (brief, debate y capturas) queda **solo en local** y no se publica (D-10). Sigue ignorado por git.
