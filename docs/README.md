# Documentación de Geoconquista

La documentación aprobada es el contrato entre diseño, implementación y pruebas. **Si no está documentado y aprobado, no se implementa.** Las reglas para agentes están en [`AGENTS.md`](../AGENTS.md) y su justificación en [ADR-000](decisions/ADR-000-gobernanza.md).

## Estado de las puertas

| Puerta | Qué autoriza | Estado |
|---|---|---|
| G0 | Arranque: gobernanza, visión, spikes y exploración de arte y audio | **`APROBADO`** por el creador, 2026-11-05 |
| G1 | Reglas v0 aprobadas (E1) | **`APROBADO`** por el creador, 2026-11-06 |
| G2a | Stack, red local y persistencia validados en laptop (ADR-001) | No iniciada |
| G2b | Hardware Raspberry Pi 5 validado (ADR-002) | No iniciada |
| G3 | **Código de producto** (`apps/`, `packages/`, `tools/`) | No iniciada |

Etapas y criterios de salida: [roadmap/milestones.md](roadmap/milestones.md).

## Registro de decisiones del creador

| ID | Fecha | Decisión |
|---|---|---|
| D-01 | 2026-11-04 | No hay prototipo en papel. Las reglas v0 se escriben y se aprueban; el ritmo y el balance se miden con el simulador; la diversión, en sesiones con personas sobre el slice digital. |
| D-02 | 2026-11-04 | Los jugadores entran por QR desde el navegador, sin instalar nada. La tablet usa una app nativa. |
| D-03 | 2026-11-05 | La tablet de consola es **Android** como plataforma principal. El creador también tiene iPad y cuentas de desarrollador de Google y Apple; el iPad queda como plataforma secundaria. |
| D-04 | 2026-11-05 | El kit gráfico y sonoro (ilustraciones, iconos, mapa, música, efectos y voces) lo genera y lo edita el agente con herramientas generativas (OpenAI, Google AI Studio, Replicate, Magnific, ElevenLabs) y locales. El creador proporciona accesos y aprueba los resultados. La meta es calidad de producción. |
| D-05 | 2026-11-05 | El creador trabaja en **Visual Studio Code**, no en Cursor. Las reglas para agentes son `AGENTS.md`, `CLAUDE.md` y la skill de `.claude/`; no se mantiene configuración de Cursor. |
| D-06 | 2026-11-05 | **P-02:** el mapa usa **países reales y actuales**, en bloques de 3 (R-04). Cuántos son jugables y cómo se tratan el resto del mundo y los territorios disputados queda en P-15. |
| D-07 | 2026-11-05 | **P-08:** la tesorería de cada jugador es **privada**. Los países, los bloques y el ingreso territorial base son públicos (plan §4.3). |
| D-08 | 2026-11-05 | **P-11:** los dados no son físicos. El jugador lanza dados virtuales que caen en la tablet. Sustituye a R-03 y deja obsoleta DEC-11. **Precisado por D-13.** |
| D-09 | 2026-11-05 | **P-13:** quien pierde su último país puede **pedir asilo político** en un país ocupado por otro jugador, siempre que conserve algún poder (comodines o *counters*) que le sirva a quien lo acoge. Sustituye a H-10A y H-10B como base. **Precisado por D-14.** |
| D-10 | 2026-11-05 | `Contexto/` queda **solo en local**: no se publica en el repositorio. |
| D-11 | 2026-11-06 | **Dirección de arte A, sala de guerra cinematográfica, para todo el juego.** Se descartan B y C, también para los mazos party. |
| D-12 | 2026-11-06 | **P-15:** **24 países jugables en 8 bloques de 3.** Se aceptan las demás recomendaciones de P-15: el resto del mundo en gris y no jugable, ningún territorio disputado jugable, fronteras de Natural Earth y sin banderas reales. La lista concreta es una propuesta en `gameplay/territories-and-blocks.md`. **Modificado por D-15.** |
| D-13 | 2026-11-06 | **P-16:** los dados se lanzan **solo deslizando el dedo** en el móvil; no se agita. Motivo: el juego es open source y no debe exigir a nadie un dominio ni certificados. Todo sigue siendo HTTP en la red local y desaparece el spike S5. |
| D-14 | 2026-11-06 | **P-17:** si **nadie acoge** al jugador que pide asilo, **queda eliminado** de la partida. |
| D-15 | 2026-11-06 | **Cambio en la lista de países:** salen Canadá, Colombia y Australia; entran **Corea del Norte, Taiwán e Israel**. Sustituye, para estos tres, la regla de D-12 de que ningún territorio disputado es jugable. Cisjordania y Gaza siguen en gris, como no jugables. Los bloques se rehacen en `gameplay/territories-and-blocks.md`. |
| D-16 | 2026-11-06 | **Mapa estilizado:** los países jugables pequeños se agrandan para que no se pierdan a 2 m (opción b de la pregunta de escala). |
| D-17 | 2026-11-06 | **Narrador:** la voz «El Faraón – Powerful and Mysterious» de la biblioteca de ElevenLabs, para todas las frases del narrador. |
| D-18 | 2026-11-06 | **Música:** dirección **híbrida** electrónica-orquestal. |
| D-19 | 2026-11-06 | **Tablero y cartas:** se aprueba la composición del tablero (fondo de mesa de guerra generado + mapa vectorial con colores de jugador planos) y el formato de carta de «Filtración» (ilustración a página completa con marco, insignia de mazo y texto encima). Ambos son la referencia de estilo. |
| D-20 | 2026-11-06 | Se aprueban la **lista de 24 países y su reparto en 8 bloques** de `gameplay/territories-and-blocks.md`. |
| D-21 | 2026-11-06 | **Efectos de sonido (exploración A0):** valen los de dados, compra, bloque completo y carta de Correo. Hay que rehacer los de declaración de ataque y conquista. |
| D-22 | 2026-11-06 | **Reglas v0:** para pedir asilo solo cuentan las **cartas guardadas**, no el efectivo; el anfitrión **no puede expulsar** al asilado; los países libres **solo se compran**, no se atacan; la **consola puede lanzar los dados** por un jugador que no lo hace, con registro público. |
| D-23 | 2026-11-06 | **Efectos rehechos:** se elige la **variante 3** de declaración de ataque (ping de radar, pulso y golpe de taiko) y la **variante 3** de conquista («braam» con golpe final de sello). |
| D-24 | 2026-11-06 | **Cierre de preguntas de las reglas v0:** «mover» es un traslado por turno entre vecinos; el recorrido y sus precios se quedan como están; los dobles no hacen nada; la retirada es automática en v0; máximo 3 cartas en la mano y 1 por turno; perdonar un arancel es gratis; los tipos de vecindad solo cambian el dibujo; el asilado solo gana si vuelve al mapa; los **objetivos secretos salen del MVP** por ahora. **El banco nunca pone el dinero de un jugador:** quien no puede pagar debe hipotecar o vender, y si aun así no alcanza, quiebra (`gameplay/economy.md` §5 y §6). |
| D-25 | 2026-11-06 | **G1 aprobada:** las reglas v0 (FS-001 a FS-008), incluido el diseño de hipoteca, venta de emergencia y quiebra, quedan aprobadas como provisionales para el slice. |
| D-26 | 2026-11-06 | **Licencias (P-10):** código AGPL-3.0-or-later; contenido CC BY-SA 4.0; nombre y logotipo reservados; aportaciones con DCO, sin CLA; código de conducta Contributor Covenant. Las voces pueden tener una licencia más cerrada. Ver ADR-003. |
| D-27 | 2026-11-06 | **Audio con licencia cerrada:** voces, efectos y música generados con ElevenLabs llevan la licencia de audio de Geoconquista (`LICENSES/LicenseRef-Geoconquista-Audio.md`): solo se redistribuyen como parte del juego o de un derivado. |

### Dados virtuales: nota técnica (D-08 y D-13, `PROPUESTO` hasta G1)

- **El resultado lo genera el host,** con un generador aleatorio con semilla que queda registrado. El gesto de deslizar solo **dispara** la tirada: su fuerza no cambia el resultado, y la animación de la tablet termina en el valor ya decidido. Así se cumple el invariante «el host es la única autoridad» (`AGENTS.md` §6) y una partida se puede reproducir.
- **Quién lanza:** en combate, atacante y defensor desde su propio móvil; en movimiento, el jugador en turno.
- **Dónde se ve:** los dados caen en la tablet y el tablero repite el resultado con una animación breve. Esto último sigue siendo una propuesta; el creador no lo ha confirmado.

### Asilo político: propuesta (D-09 y D-14, `PROPUESTO` hasta G1)

Las «cartas que se guardan» no existen todavía: hoy cada carta se aplica al robarla (H-08). El asilo necesita que haya cartas que se guardan en la mano.

- El asilo se pide a un jugador concreto y es un **tratado** que el motor hace cumplir (H-11). El anfitrión puede **aceptarlo o rechazarlo**.
- **El asilado** conserva su turno y el subsidio de exilio, y vive en un país del anfitrión. Desde ahí puede reentrar comprando un país libre o con la reentrada civil de H-10B.
- **El anfitrión** recibe al aceptar las cartas guardadas que se pactaron. Romper el asilo cuenta como romper un tratado.
- **Si nadie lo acoge, queda eliminado** (D-14). Propuesta: quien no tiene ningún poder que ofrecer no puede pedir asilo, así que también queda eliminado. Una eliminación temprana deja a una persona mirando el resto de la partida. Se mide en las sesiones de E5 y E6 (CE-08).

Las recomendaciones que todavía no son decisiones (DEC-01 a DEC-12) están en el [plan de arranque](roadmap/plan-de-arranque.md) §5.

## Estados de documento

`PROPUESTO` → `APROBADO` (con aprobador y fecha) → `OBSOLETO`. `PENDIENTE` marca algo que espera una respuesta del creador. Solo el creador aprueba.

## Índice

Leyenda: ✅ existe · ⏳ previsto en la etapa indicada.

### Gobernanza y producto
- ✅ [decisions/ADR-000-gobernanza.md](decisions/ADR-000-gobernanza.md): reglas documentales y para agentes. `APROBADO`
- ✅ [decisions/ADR-003-licencias.md](decisions/ADR-003-licencias.md): licencias y aportaciones. `APROBADO` (D-26, D-27)
- ✅ [product/vision.md](product/vision.md): visión, pilares, requisitos y límites. `APROBADO`
- ✅ [roadmap/milestones.md](roadmap/milestones.md): etapas, puertas y estado. `APROBADO`
- ✅ [roadmap/plan-de-arranque.md](roadmap/plan-de-arranque.md): plan consolidado del debate, con las revisiones del 2026-11-04 y 2026-11-05. Referencia, no spec; las decisiones D-## prevalecen sobre él.

### Gameplay (E1, reglas v0)
- ✅ [gameplay/core-loop.md](gameplay/core-loop.md) (FS-001): preparación, turno, dados virtuales y cartas. `APROBADO` (G1)
- ✅ [gameplay/board-and-map.md](gameplay/board-and-map.md) (FS-002): recorrido, variantes A y B, casillas. `APROBADO` (G1)
- ✅ [gameplay/territories-and-blocks.md](gameplay/territories-and-blocks.md) (FS-003): 24 países, 8 bloques y vecindades. `APROBADO` (D-20, G1)
- ✅ [gameplay/economy.md](gameplay/economy.md) (FS-004): tesorería, ingreso, compra, arancel y comercio. `APROBADO` (G1)
- ✅ [gameplay/armies-and-fog-of-war.md](gameplay/armies-and-fog-of-war.md) (FS-005): tropas, reclutar, mover, bandas y espionaje. `APROBADO` (G1)
- ✅ [gameplay/combat.md](gameplay/combat.md) (FS-006): ataque, tirada, bajas y retirada. `APROBADO` (G1)
- ✅ [gameplay/victory-and-endgame.md](gameplay/victory-and-endgame.md) (FS-007): dominio, límite de rondas y asilo político. `APROBADO` (G1)
- ✅ [gameplay/parameters.md](gameplay/parameters.md) (FS-008): todas las cifras. `APROBADO` (G1)
- ⏳ `gameplay/diplomacy.md`, `game-modes.md` y `truth-or-dare.md` (E3/E6)

### Arquitectura (E2/E3)
- ⏳ `decisions/ADR-001-stack-y-clientes.md` y `ADR-002-pantalla-publica.md` (con evidencias de los spikes)
- ⏳ `architecture/system-context.md`, `authority-and-privacy.md`, `protocol.md`, `persistence.md`, `offline-lan.md` y `deployment.md`

### UX (E3)
- ⏳ `ux/public-display.md`, `admin-tablet.md`, `player-mobile.md` y `lobby.md`

### Contenido (E3/E6)
- ⏳ `content/card-catalog-and-governance.md`

### Arte y audio (línea A, en paralelo)
- ✅ [assets/art-direction.md](assets/art-direction.md): dirección de arte. `PROPUESTO`
- ✅ [assets/audio-direction.md](assets/audio-direction.md): dirección de audio. `PROPUESTO`
- ✅ [assets/pipeline.md](assets/pipeline.md): herramientas, flujo, manifiesto y licencias. `PROPUESTO`

### Pruebas (E3)
- ⏳ `testing/test-strategy.md`, `acceptance-matrix.md` y `playtest-plan.md`

### Plantillas
- ✅ [templates/feature-spec.md](templates/feature-spec.md), [templates/adr.md](templates/adr.md), [templates/card.md](templates/card.md), [templates/asset-brief.md](templates/asset-brief.md) y [templates/session-report.md](templates/session-report.md)

## Material de origen

`Contexto/` contiene el brief del creador, la transcripción del debate, la gobernanza heredada y las capturas conceptuales. Es material de consulta: **nada de ahí se implementa sin pasar a un documento de `docs/` aprobado.** `Contexto/` queda solo en local y está ignorado por git (D-10).
