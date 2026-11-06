# Reglas para agentes de programación — Geoconquista

Este archivo es la **única fuente** de reglas para cualquier agente que trabaje en el repositorio (Claude Code en Visual Studio Code u otros). `CLAUDE.md` solo remite aquí. La justificación de cada regla está en [ADR-000](docs/decisions/ADR-000-gobernanza.md).

## 1. Documentation First

**Si no está documentado y aprobado, no se implementa.**

- No se inventan reglas, cifras, efectos, pantallas, botones, textos de error, estados ni contratos. Lo que falte se registra como pregunta o propuesta en `docs/`, no se resuelve por intuición en el código.
- Cambiar una regla, un flujo o la arquitectura exige actualizar y aprobar primero el documento, y después el código.
- Un conflicto entre documentos **bloquea** la implementación hasta resolverlo (ver §3).

## 2. Qué se puede crear y cuándo

| Qué | Cuándo | Dónde |
|---|---|---|
| Documentación | Siempre, en estado `PROPUESTO` | `docs/` |
| Spikes técnicos (código desechable de E2) | Tras aprobar G0 | Rama `spike/<id>`; nunca se fusiona. Solo sus conclusiones pasan a un ADR |
| Exploración de arte y audio | Tras aprobar G0 | `exploracion/` (ignorado por git). Solo lo aprobado pasa a `assets/` con su entrada en el manifiesto |
| `apps/`, `packages/`, `tools/` (código de producto) | **Solo tras la puerta G3** | Estructura de `docs/roadmap/plan-de-arranque.md` §6.3 |
| `assets/` (activos definitivos) | Cuando la dirección de arte o audio esté `APROBADO` y un documento de UX pida el activo | `assets/` + `assets/manifest.json` |

Estado actual de las puertas: ver `docs/README.md`.

## 3. Estados y precedencia

- Estados de documento: `PROPUESTO`, `PENDIENTE`, `APROBADO` (con aprobador y fecha) y `OBSOLETO`.
- Solo el creador aprueba. Un agente nunca marca nada como `APROBADO` por su cuenta.
- Ante un conflicto: `APROBADO` prevalece sobre `PROPUESTO`. Entre dos documentos aprobados prevalece el más reciente **solo si cita explícitamente** al anterior. En cualquier otro caso se declara `HAY_CONFLICTO_DOCUMENTAL` y no se implementa.

## 4. Convenciones

- **IDs:** `FS-###` (spec de funcionalidad), `AC-###.#` (criterio de aceptación de la spec `###`), `ADR-###`, `D-###` (decisión del creador), `CARD-<tipo>-###` (carta), `EVT-###` (evento).
- **Modos:** `familiar_u18`, `familiar_18`, `party_18`, `party_extreme_18`, `parejas_18`. Nunca `couples_18`.
- **Visibilidad:** `público`, `propietario`, `partes_tratado` y `sistema`. La consola (tablet) **no** tiene un nivel propio de secretos.
- **Idiomas (D-29):** la documentación se escribe y se aprueba en español, que es la versión canónica. Cada documento tiene su traducción al inglés en `<nombre>.en.md`, que se actualiza **en el mismo commit** que el original. Si difieren, manda el español. No se traducen los estados, los IDs ni los identificadores de datos. Excepción: el plan de arranque solo está en español.
- **Rutas documentales:** el árbol de `docs/README.md`. No crear documentos con nombres alternativos (`game-loop.md`, `modes.md`, `host-screen.md`, etc.).
- **Stack y hardware:** no se asume ninguna tecnología. Se remite a ADR-001 (stack y clientes) y ADR-002 (pantalla pública).

## 5. Contrato de salida

Cualquier tarea que cree o modifique código, specs, contenido o activos empieza con estos cinco puntos. Las preguntas y explicaciones no lo necesitan.

1. **Documentos fuente:** archivos y secciones que gobiernan la tarea.
2. **Estado documental:** `LISTO_PARA_IMPLEMENTAR`, `FALTA_DOCUMENTACION` o `HAY_CONFLICTO_DOCUMENTAL`.
3. **Acción inmediata:** `VOY_A_DOCUMENTAR`, `VOY_A_IMPLEMENTAR` o `VOY_A_ACTUALIZAR_DOCS_Y_LUEGO_IMPLEMENTAR`.
4. **Trazabilidad:** IDs de spec, AC y ADR, y módulos o activos afectados.
5. **Resultado:** al cerrar, qué cambió y por qué, qué pruebas lo cubren y qué quedó pendiente.

El procedimiento completo está en la skill `documentation-first` (`.claude/skills/documentation-first/SKILL.md`).

## 6. Invariantes técnicos (válidos con cualquier stack)

- El host es la única autoridad: los clientes envían comandos y nunca deciden el estado.
- El servidor filtra cada vista. Ningún cliente recibe el estado completo ni datos privados ajenos.
- Ninguna función esencial depende de Internet: nada de CDN, fuentes remotas, analítica ni IA en tiempo de partida.
- Las reglas viven en el motor y las cifras en datos de contenido, nunca en la interfaz ni como constantes sueltas.
- Cartas, retos y textos viven en contenido estructurado con ID, modos y estado editorial.

## 7. Secretos y activos generados

- Las claves de API van **solo** en `.env` (ignorado por git; plantilla en `.env.example`). Nunca en código, documentos, prompts guardados ni mensajes de commit.
- Todo activo generado con IA registra en `assets/manifest.json` la herramienta, el modelo, la fecha, el prompt, las ediciones y los términos de licencia aplicables. Sin esa entrada no entra en `assets/`.

## 8. Git

- Los commits y las descripciones de PR **no llevan atribución** de ningún asistente: ni `Co-Authored-By`, ni «Generated with», ni ninguna variante. El mensaje termina en su última línea de contenido.
- Solo se hace commit o push cuando el creador lo pide.
- Los commits del creador, incluidos los que hace un agente por encargo suyo, **no** llevan `Signed-off-by`: el creador es el titular y no firma DCO. El DCO (`git commit -s`) es para las aportaciones externas (ADR-003, `CONTRIBUTING.md`).
