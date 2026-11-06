# Geopolitica

**Proyecto:** Geoconquista, un juego híbrido de mesa y digital sobre geopolítica, economía, guerra y eventos sociales.
**Documento:** plan de arranque del desarrollo. Es el borrador consolidado del debate (9 turnos de la fase inicial entre los participantes A, B y C) y **no aprueba reglas ni tecnología**. **Revisión del 2026-11-04 y 2026-11-05:** incorpora las decisiones del creador D-01 a D-10 (registradas en `docs/README.md`). Donde este plan contradiga una decisión D-##, prevalece la decisión. Esta copia en `docs/roadmap/` es la vigente; el original del debate queda archivado en `Contexto/plan.md`.
**Fuentes analizadas:** `GEOCONQUISTA_BRIEF_DEBATE.md`, `README.md`, `gobernanza/extras.md`, `gobernanza/cursor-doc-first-skill-pack-original.zip` (24 archivos) y las tres capturas de `referencias-visuales/`.

**Etiquetas usadas en este plan:**

| Etiqueta | Significado |
|---|---|
| `[REQ]` | Requisito expreso del creador (brief §3.1). Este plan no lo modifica. |
| `[REC]` | Recomendación del plan. Necesita la aprobación del creador. |
| `[HIP]` | Hipótesis de diseño que se debe validar con el simulador, una prueba automática, una sesión con personas o un spike. |
| `[PEND]` | Decisión abierta que pertenece al creador. |
| `[HECHO]` | Dato comprobado en una fuente, que se cita en el lugar donde aparece. |

---

## 1. Objetivo y resultado esperado

**Objetivo.** Pasar de un brief con muchas preguntas abiertas a un desarrollo autorizado y trazable. Ese desarrollo debe producir primero un juego **divertido en una mesa real** y después una aplicación sólida. El plan respeta *Documentation First* `[REQ]`: no se escribe código de producto antes de aprobar su documentación.

**Resultado esperado, por hitos verificables:**

1. **Gobernanza unificada.** Un solo juego de convenciones documentales. Hoy hay tres que se contradicen (ver §4.4).
2. **Reglas v0 del núcleo documentadas y aprobadas** (D-01: sin prototipo en papel). El bucle de turno, la relación entre el recorrido y el mapa, la compra e intercambio de países, los bloques, los ejércitos ocultos, un ataque y una vía de victoria se fijan por escrito, con sus parámetros, antes de programarlos. El ritmo y el balance se miden después con el simulador; la diversión, con personas sobre el slice digital.
3. **Riesgos técnicos descartados con spikes desechables:** clientes móviles sin instalación, pantalla en Raspberry Pi, red local sin Internet y persistencia durable.
4. **Documentación crítica aprobada.** Con ella se autoriza el código (puerta G3).
5. **Vertical slice digital** que demuestra tres cosas: sincronización, secreto militar y diversión.
6. **MVP** con las cinco modalidades `[REQ]`, guardado y recuperación, y pruebas en hardware real.

**Qué no es este plan:** no es el GDD ni una spec aprobada. Las cifras y reglas de §6.2 son hipótesis de partida para las reglas v0 (E1). Las decisiones de §5 están en estado `RECOMENDADO` o `PENDIENTE`; solo D-01 y D-02 (§5) vienen del creador.

---

## 2. Necesidades del usuario y criterios de éxito

### 2.1 Actores

| Actor | Necesidad principal |
|---|---|
| **Creador** (supuesto: desarrolla solo y con agentes como Cursor) | Un camino ordenado en el que el agente no invente reglas, la documentación sea el contrato y el riesgo se reduzca pronto. |
| **Jugadores** (3–6 `[HIP]`) | Jugar cara a cara con dados reales, negociar y mirar el móvil solo lo necesario. Unirse sin complicaciones. |
| **Operador de la consola** (tablet) | Capturar dados y resolver casillas con rapidez y sin poder hacer trampa (ver DEC-06). |
| **Público de la mesa** | Entender el estado de la partida desde la pantalla grande sin ver secretos. |
| **Contribuidores open source** (más adelante) | Specs claras, pruebas y un proceso de cambios explícito. |

### 2.2 Criterios de éxito del producto

Las metas numéricas son `[HIP]` y se calibran tras las primeras sesiones con personas (E5).

| ID | Criterio | Meta inicial | Cómo se mide |
|---|---|---|---|
| CE-01 | Duración de la partida | 90–120 min con 3–4 jugadores; menos de 150 min con 5–6 | Cronometraje en las sesiones con personas (E5/E6) |
| CE-02 | Tiempo de turno sin negociación | Media de 60–90 s o menos (ver cálculo en §4.3) | Registro del motor en las sesiones E5/E6 |
| CE-03 | La mesa manda sobre la pantalla | Encuesta posterior a la partida: «miré el móvil más de lo que quería» en menos del 30 % de los jugadores | Encuesta corta |
| CE-04 | Privacidad militar | **Cero** exposiciones no autorizadas de tropas rivales en interfaces, mensajes o registros accesibles a jugadores; revisar también deducciones exactas por costes y resultados | Pruebas de proyección y de secuencias observables (§8.2); revelaciones deliberadas definidas en la spec |
| CE-05 | Offline real | Una partida completa con el router **sin salida a Internet** | Prueba de aceptación en hardware |
| CE-06 | Unirse sin instalar | Desde el escaneo del QR hasta estar en el lobby: menos de 60 s en Android e iOS | Spike S1 y sesiones E5 |
| CE-07 | Recuperación | Se conserva todo comando confirmado. Cada solicitud sin respuesta se consulta o reintenta con el mismo ID y se aplica como máximo una vez; no se garantiza conservar solicitudes que aún no llegaron a persistirse | Prueba de corte de energía (AC-PERS-01) |
| CE-08 | Agencia | Ningún jugador queda más de 2 rondas sin decisiones significativas | Observación en las sesiones E5/E6 |
| CE-09 | Trazabilidad | Cada regla implementada tiene un ID de spec, un AC y una prueba | Revisión de la matriz de aceptación |

---

## 3. Alcance incluido y excluido

### 3.1 Incluido en este plan

- Etapas E0–E7 (§7): desde la gobernanza hasta la publicación open source del MVP.
- El diseño del núcleo jugable como reglas v0 que se validan con pruebas automáticas, el simulador y sesiones digitales con personas, con una traza de referencia de fin a fin (§6.2.1).
- Las decisiones de arquitectura, red, persistencia, privacidad y contenido necesarias para el MVP.
- Las cinco modalidades `[REQ]`, cada una con un catálogo **pequeño** de contenido validado.
- Las pruebas en Raspberry Pi real y en red local sin Internet `[REQ]`.

### 3.2 Excluido del MVP (puede volver más adelante si se aprueba)

| Excluido | Motivo |
|---|---|
| Juego en línea, cuentas o nube | Contradice el modo offline `[REQ]` y añade complejidad sin beneficio para la mesa. |
| Integración con WhatsApp real o mensajes a contactos reales | El brief lo trata solo como nombre temático (§6.4). Además hay riesgos de privacidad y de marca. |
| Dados virtuales como mecánica principal | Contradice `[REQ]`. El botón «TIRAR DADOS» de la captura móvil **no se implementa**. |
| Apps nativas en tiendas (App Store y Play Store) | Ver DEC-03. El MVP usa clientes web servidos por el host. |
| Varios mapas, clases de unidades, fortificaciones, reservas fuera del mapa o logística avanzada | Se usa una unidad genérica desplegada directamente en territorios en el MVP (brief §5.2). |
| Tiempo real tipo RTS | El juego es por turnos. Age of Empires inspira la preparación estratégica, no la mecánica en tiempo real. |
| Bots o IA rivales jugables | Solo existen bots **de simulación** para medir el balance (E4). |
| Kit físico extenso (sellos, sirena, pasaportes, etc.) | El MVP se juega con dados y fichas comunes (brief §8). Los accesorios son opcionales y quedan para una fase posterior. |
| Idiomas distintos del español | Se dejan preparados (textos en contenido externo), pero no se traducen. |

---

## 4. Requisitos y restricciones

### 4.1 Requisitos del creador `[REQ]` (brief §3.1)

| ID | Requisito | Implicación para el plan |
|---|---|---|
| R-01 | El nombre es **Geoconquista** | Las capturas dicen «Dominio Global» y no deben copiarse (§4.4). |
| R-02 | Juego híbrido con tablero grande en una pantalla conectada al host (inicialmente una Raspberry Pi) | Spike S2 en una Pi real. |
| R-03 | ~~Dados reales, capturados con el teclado numérico de la tablet~~ **Modificado por D-08 y D-13:** dados virtuales que el jugador lanza deslizando el dedo en el móvil y que caen en la tablet | DEC-11 queda obsoleta. El resultado lo genera el host. |
| R-04 | Países comprables agrupados en **bloques de 3**. Completar un bloque permite formar ejércitos | Núcleo de §6.2. |
| R-05 | Ejércitos **ocultos** para los rivales, y el dueño puede consultarlos | Las vistas se filtran en el servidor (§6.3). |
| R-06 | Invasiones con victoria, derrota, defensa y acuerdos | Hipótesis H-07. |
| R-07 | Varias vías de victoria, entre ellas conquista y sumisión | Hipótesis H-09. |
| R-08 | Casillas de Hacienda, Migración, Correo Electrónico, WhatsApp y Verdad o Reto | Hipótesis H-08 y P-05 (nombre WhatsApp). |
| R-09 | Tablet con pestañas: banco, ejércitos, cartas, verdad o reto, rankings, dashboard, administración y teclado | DEC-06: la pestaña «Ejércitos» **no** muestra tropas ajenas. |
| R-10 | Móvil privado por jugador: dinero, países, ejércitos, ranking y gráficos | Los gráficos usan solo datos públicos (territorios, bloques e ingresos territoriales base). |
| R-11 | Lobby local con unión de la tablet y los móviles | QR, código de sala e IP manual (DEC-08). |
| R-12 | **Sin Internet obligatorio** | Hay que eliminar dependencias ocultas de CDN (§4.3). |
| R-13 | Open source y *Documentation First* | E0 y §6.5. |
| R-14 | **Cinco modos:** `familiar_u18`, `familiar_18`, `party_18`, `party_extreme_18`, `parejas_18` | Comparten el núcleo y cambian los mazos (§6.4). |

### 4.2 Restricciones y supuestos de contexto

| ID | Restricción o supuesto | Tipo |
|---|---|---|
| C-01 | Desarrollo en Linux/Kubuntu | Hecho (brief §10.2) |
| C-02 | No hay una Mac disponible | **Supuesto.** Sin Mac no se pueden compilar apps iOS nativas (brief §10.2). Por eso los clientes web resultan más atractivos. |
| C-03 | Un solo desarrollador con agentes de IA | **Supuesto.** Pesa a favor de una base de código y un lenguaje. |
| C-04 | Presupuesto bajo, sin fecha comprometida | **Supuesto.** El plan no promete fechas (brief §12.2). |
| C-05 | Hay una Raspberry Pi 5 disponible para las pruebas | **Supuesto.** Si se retrasa, se bloquean S2 y el cierre en hardware de E5 (`G2b`), pero el motor y la validación en laptop Linux (`G2a`) avanzan sin bloqueo (§7). |
| C-06 | Los móviles de los jugadores son heterogéneos, de Android e iOS, algunos antiguos | Hecho (brief §15.8) |
| C-07 | Contenido +18 en un proyecto open source | Requiere separar los paquetes de contenido y hacer revisión editorial (§6.4). |

### 4.3 Requisitos derivados (inferencias de este plan)

- **Presupuesto de tiempo por turno** (inferencia aritmética). Las capturas muestran «Ronda 8 / 30»: con 30 rondas y 6 jugadores saldrían 180 turnos, que en 120 min dejan **40 s por turno**, algo irreal si hay compra, carta y ataque. Con los límites candidatos de H-09, la cuenta cambia: 12 rondas con 4 jugadores son 48 turnos en 120 min, y 10 rondas con 6 jugadores son 60 turnos en 150 min. En ambos casos quedan unos **150 s por turno con todo incluido**: los 60–90 s de mecánica de CE-02 más la negociación, los retos y las transiciones. **Conclusiones:**
  - El número de rondas debe depender del número de jugadores, o la partida debe terminar por condiciones y no por rondas fijas.
  - Cada turno necesita un máximo de acciones (H-02).
  - El simulador (E4) debe comprobar si 10–12 rondas (unas 2–3 vueltas al recorrido A con 2d6) bastan para completar bloques y llegar a la fase militar. Si en la simulación la variante A no forma ningún bloque hacia la ronda 5 (RK-02), se activan antes de alargar la partida tres palancas previstas en el diseño (brief §5.1): (1) adjudicar **2 países iniciales por jugador** (de bloques distintos) al arrancar la partida, (2) ajustar precios/ingresos o (3) elegir la variante B de recorrido por bloques.
- **Offline sin dependencias ocultas.** `[HECHO]` Flutter Web descarga CanvasKit desde un CDN por defecto, salvo que se compile con `--no-web-resources-cdn`. También descarga las fuentes de respaldo desde `fonts.gstatic.com` cuando las fuentes incluidas no tienen un glifo (parámetro `fontFallbackBaseUrl`). Fuentes: [docs.flutter.dev, inicialización web](https://docs.flutter.dev/platform-integration/web/bootstrapping) y el [cambio en flutter.js sobre el CanvasKit local](https://chromium.googlesource.com/external/github.com/flutter/flutter/+/74688cea3d14954277dd9342d4f9db838eee3050%5E%21). Cualquier stack web debe pasar una **prueba con DNS externo bloqueado** (AC-NET-01).
- **Contexto seguro en el host frente a contexto no seguro en la LAN.** `[HECHO]` `http://127.0.0.1` y `http://localhost` son orígenes potencialmente confiables; la IP privada remota por HTTP no lo es. Esto permite solicitar `Screen Wake Lock` en un navegador compatible del host, pero **no garantiza su concesión ni permanencia**: puede rechazarse o liberarse. S2 verifica el navegador y la configuración de reposo del sistema reales. Fuentes: [W3C Secure Contexts](https://w3c.github.io/webappsec-secure-contexts/) y [MDN Screen Wake Lock API](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Wake_Lock_API). Servir recursos desde el host permite jugar sin Internet sin depender de service workers. S1 comprueba la conexión LAN con datos móviles activos y, si falla, el procedimiento de mantener Wi-Fi o desactivar temporalmente datos. Apple documenta [Connectivity Assist](https://support.apple.com/en-us/127686), que sustituye Wi-Fi Assist en versiones recientes; no se presupone que cambie el enrutamiento de una IP local. En Android se registra el comportamiento del dispositivo concreto, sin atribuirlo a una función no verificada.
- **Secreto militar y economía.** `[HECHO: deducción aritmética]` Si el saldo público baja 30 y cada tropa cuesta 10, se deducen 3 tropas aunque se elimine el campo del mensaje. Lo mismo ocurre con mantenimiento proporcional, bajas exactas o fuerza total de combate. `[REC consolidada de A, B y C]` **Tesorería (efectivo exacto) y gastos militares privados** durante la partida; en cambio, **los países, bloques y el ingreso territorial base por ronda son públicos**, lo que sostiene los rankings, los gráficos comparativos (R-10) y la negociación diplomática sin revelar cuánto efectivo se transformó en ejército. Se define una matriz de revelaciones explícitas para combate, espionaje e impagos (§6.3, P-08). *Alternativa documentada si el creador prefiere efectivo público en P-08:* separar la tesorería pública de un «Presupuesto de Defensa» opaco (el jugador transfiere una partida cerrada al ministerio militar o recluta por cupo gratuito de bloque completo), de modo que el gasto público no guarde relación 1:1 con las tropas reclutadas.
- **Visibilidad con al menos 4 niveles:** `público`, `propietario`, `partes_tratado` y `sistema`. El modelo `public/private/admin` de `extras.md` no basta y contradice el principio de que moderar no da acceso a secretos. Por el mismo motivo no se adopta el nivel `moderador` de los cinco del brief §9.4 (G-5): la consola no tiene secretos propios (DEC-06, §6.3).

### 4.4 Hallazgos del análisis de la documentación y las capturas

**Contradicciones en las capturas.** Todas son ilustrativas (brief §14) y **nada de ellas se implementa sin una spec**.

| # | Hallazgo | Riesgo si se copia | Tratamiento |
|---|---|---|---|
| V-1 | Las tres capturas dicen **«Dominio Global»**, no Geoconquista | Identidad incorrecta y posible conflicto de nombre | Usar solo Geoconquista (R-01) |
| V-2 | El tablero agrupa el mapa en **7 bloques continentales grandes**. El móvil dice «Bloques completos 1/8» y muestra **4** países europeos con estrella dorada (Francia, España, Italia y Alemania) junto a «Europa Occidental 3/3» | Contradice los bloques de 3 (R-04) y es incoherente consigo misma | El mapa sale de la spec `board-and-map` |
| V-3 | El borde muestra números hasta 95, con tramos desordenados (20, 30, 25, 35), sin correspondencia visible con países o eventos; podría ser una pista de puntuación, pero esa función es una **interpretación**, no un hecho documentado | Copiarlo no define dónde caer para comprar o activar eventos | DEC-02: especificar el recorrido y su correspondencia con el mapa |
| V-4 | La tabla de la tablet muestra los **ejércitos exactos de todos los jugadores** | Fuga directa de secretos (R-05) | DEC-06: la consola no ve tropas ajenas |
| V-5 | Acciones rápidas de la tablet: «Dar dinero», «Aplicar multa», «Condonar deuda» y «Subsidio global» | Dan poder arbitrario al operador y abren la puerta a trampas | DEC-06: solo comandos definidos por las reglas, más corrección auditada |
| V-6 | Botón «TIRAR DADOS» en el móvil | Contradice R-03 | Excluido (§3.2) |
| V-7 | El móvil muestra «Bonificación activa: +15 % ingresos» por un bloque completo | Añade una bonificación no aprobada; R-04 exige desbloquear ejércitos, pero no prohíbe otros efectos | La spec de bloques decide si existe algún bono extra |
| V-8 | Temporizador «Próximo turno en 02:15» y «Puntaje 1,250» | Temporizador y puntuación sin definir | H-02 y H-09 |
| V-9 | La tablet une «Correo / WhatsApp», incluye botones «VER MAZO» y el tablero añade «Evento Global» | La agrupación no define cómo se resuelven las casillas separadas de R-08; el botón no aclara si abre un catálogo público o el orden secreto | La spec distingue catálogo y descartes públicos del orden de robo, siempre de nivel `sistema`; no asumir la función por su etiqueta |
| V-10 | Logo de WhatsApp en las cartas del tablero y la tablet | Uso de una marca de terceros en un proyecto público | No usar el logo; P-05 |
| V-11 | Las cifras de dinero (millones), los impuestos (10 %) y los eventos («Guerra Fría +10 %») | Las cifras son decorativas (brief §5.5) | No se usan como balance |
| V-12 | El teclado numérico de la tablet (`02-tablet-admin-conceptual.png`) muestra teclas **`1`–`9` y `0`** junto a dos dados de 6 caras (`d6`) | Si se captura cada dado `1d6` por separado (DEC-11), las teclas `7`, `8`, `9` y `0` provocan errores de captura constantes | DEC-11 y AC-CMD-02: el teclado de dados solo habilita botones `1`–`6` por cada dado requerido |
| V-13 | El móvil (`03-movil-jugador-conceptual.png`) muestra «Ejércitos: 22 \| En reservas: 7», pero la suma de tropas en sus 5 países (5+4+6+5+2) ya da 22 | Ambigüedad entre tropas desplegadas y reservas en el limbo | H-05: en el MVP no hay reservas fuera del mapa; toda tropa reclutada se asigna a un país del bloque |

**Contradicciones en la gobernanza.** Se resuelven en ADR-000 (E0).

| # | Tema | `extras.md` | Paquete de Cursor | Brief |
|---|---|---|---|---|
| G-1 | Precedencia ante conflictos | gameplay > arquitectura > UX > implementación | **specs > ADR > arquitectura > UX > gameplay** (orden inverso) | La gobernanza debe resolverlo |
| G-2 | IDs | `FS-###`, `AC-###.#` | `SPEC-###`, `GDD-###`, `UX-###`, `ARCH-###`, `AC-XXX-001` | `FS-001`, `AC-001.1`, `CARD-…` |
| G-3 | Rutas y nombres de documentos | `docs/specs/feature-<slug>.md`, `docs/adr/`, `turn-structure.md`, `invasion-system.md` | `docs/specs/features/`, `docs/adr/`, `game-loop.md`, `modes.md`, `host-screen.md` (con stubs ya creados) | `docs/decisions/ADR-###`, `core-loop.md`, `game-modes.md`, `public-display.md` (§11.2) |
| G-4 | ID del modo de parejas | `parejas_18` | **`couples_18`** | `parejas_18` |
| G-5 | Visibilidad | `public/private/admin` | público, privado y solo administrativo | 5 niveles (§9.4) |
| G-6 | Estructura de apps | No aplica | `host_raspberry`, `tablet_admin`, `mobile_client`, `game_core` | `host_display`, `admin_tablet`, `player_mobile`, `local_server`, `game_domain` |
| G-7 | Autoridad para crear la estructura | No aplica | «Si aún no existen, **propón y crea** esta estructura base» | «**No crear** esta estructura sin un ADR aprobado» |
| G-8 | Premisas técnicas | No aplica | Da por hechos «Flutter como stack principal» y «Raspberry Pi como host» | Ambos son propuestas **no aprobadas** (§3.2) y se pide soportar también una laptop (§10.5) |
| G-9 | Contrato de salida del agente | No aplica | `.mdc` exige 4 bloques (`DOCUMENTAR \| IMPLEMENTAR…`) y `SKILL.md` exige 5 bloques distintos (`LISTO_PARA_IMPLEMENTAR…`) | Debe existir un único flujo sin ambigüedad (§11.5) |

`[REC]` para G-1: la precedencia correcta es por **nivel de abstracción y estado**. Un documento `APROBADO` prevalece sobre uno `PROPUESTO`. Entre documentos aprobados prevalece el más reciente que cite explícitamente al anterior. Cualquier contradicción detectada **bloquea** la implementación hasta que se resuelva (brief §11.1.6). Un orden fijo por carpeta, como proponen los dos borradores, induce errores en ambos sentidos.

---

## 5. Alternativas evaluadas y decisiones justificadas

Todas las decisiones están en estado **RECOMENDADO** o **PENDIENTE**, salvo las del creador registradas a continuación. Junto a cada una se indica el impacto y el documento donde debe registrarse.

### Decisiones del creador registradas

| ID | Fecha | Decisión | Efecto en el plan |
|---|---|---|---|
| D-01 | 2026-11-04 | No se hace prototipo en papel antes del código | DEC-01: E1 pasa a ser la redacción de las reglas v0; el simulador y el visor de E4 miden ritmo y balance; las sesiones con personas de E5 miden la diversión (RK-14) |
| D-02 | 2026-11-04 | Preferencia: los jugadores entran por QR desde el navegador, sin instalar nada; la tablet usa una app nativa | DEC-03 y DEC-04: TypeScript en todo y la consola empaquetada con Capacitor para Android (recomendación pendiente de ADR-001) |
| D-03 | 2026-11-05 | La tablet de consola es Android como plataforma principal; el iPad, secundaria (el creador tiene ambas y cuentas de desarrollador de Google y Apple) | P-14 respondida; la app de consola se hace primero para Android |
| D-04 | 2026-11-05 | El agente genera y edita el kit gráfico y sonoro con herramientas generativas (OpenAI, Google AI Studio, Replicate, Magnific, ElevenLabs) y locales; el creador da los accesos y aprueba | Línea de arte y audio A0–A3 en paralelo (`docs/roadmap/milestones.md`); procedimiento en `docs/assets/pipeline.md` |

D-02 es una preferencia expresada, no la aprobación de un stack: la elección concreta se aprueba en ADR-001 (G2a).

### DEC-01: Orden de trabajo. Reglas v0 por escrito, después motor y simulador
- **Alternativas:** (a) motor digital primero; (b) prueba de mesa en papel primero y spikes técnicos en paralelo; (c) todo a la vez.
- **Decisión del creador (D-01):** no hay prototipo en papel. El debate recomendaba (b); el creador lo descartó. Se adopta (a) con *Documentation First* intacto: ninguna regla se programa sin estar escrita y aprobada.
- **Cómo se sustituye lo que aportaba el papel `[REC]`:**
  - **Reglas v0 (E1):** H-01 a H-12 se convierten en reglas escritas, con todas sus cifras en `docs/gameplay/parameters.md`. El creador las aprueba como provisionales para el slice (G1).
  - **Casos límite como pruebas:** los escenarios de §8.3 (exilio, cerco, comercio A→B→C, impagos, inferencias encadenadas) se escriben en E1 como casos ejecutables y pasan a ser AC del motor.
  - **Simulador temprano (E4):** mide lo que depende del azar y la economía: ronda del primer bloque, rondas necesarias según el número de jugadores, variante A frente a B, ventaja por asiento y ciclos de rescate.
  - **Visor de desarrollo (E4):** una página interna en la que una sola persona juega todos los asientos contra el motor, para sentir el ritmo del turno sin reunir a nadie.
  - **Sesiones con personas (E5):** diversión, negociación, duración y agencia (CE-01/02/03/08) se miden sobre el slice digital. Esto no tiene sustituto.
- **Coste:** un cambio de regla descubierto con personas obliga a cambiar spec, código y pruebas (RK-14). **Mitigación:** cifras en datos y no en el código, reglas en módulos pequeños con sus AC y reglas v0 marcadas como provisionales.
- **Impacto:** E1 deja de ser una prueba de mesa y pasa a ser la redacción de las reglas v0; G3 depende de G1 (reglas v0 aprobadas) y de G2a.
- **Destino:** `docs/roadmap/milestones.md`.

### DEC-02: Cómo se conectan el recorrido y el mapa (prioridad de diseño, brief §5.1)
- **Alternativas:**
  - (A) **Una casilla por país.** El recorrido es un anillo con una casilla por cada país del mapa, más las casillas especiales. Caer en un país permite comprarlo. El mapa solo sirve para las adyacencias militares.
  - (B) **Una casilla por bloque o región.** Al caer en la casilla de un bloque se elige un país libre de ese bloque. Da más agencia y menos azar.
  - (C) **Sin recorrido.** Los dados mueven ejércitos por el mapa al estilo de Risk. Se descarta porque elimina las casillas especiales `[REQ]` y la sensación de recorrido.
  - (D) **Dos fichas por jugador**, una en el recorrido y otra en el mapa. Se descarta por la carga cognitiva y la poca legibilidad.
- **Recomendación:** especificar **A y B** en `board-and-map.md` como dos valores del parámetro `variante_recorrido` y compararlas en el simulador (E4); el slice usa la que mejor resulte. Se parte de A porque es más reconocible, al estilo Turista, y más fácil de leer en pantalla. Los bloques deben ser **geográficamente contiguos** en el mapa, de modo que completar un bloque tenga sentido tanto económico como militar. En ambas variantes se habilita la compraventa/intercambio bilateral de países entre jugadores (H-03) para evitar que los bloques queden bloqueados por el azar de los dados.
- **Consecuencia:** con 24 países y 8–12 casillas especiales, A tendría **32–36 casillas**; B, con 8 casillas de bloque, tendría **16–20** `[HIP]`. El simulador registra la frecuencia de eventos y vueltas de cada variante: no son equivalentes con los mismos dados.
- **Impacto:** define el diseño del tablero público (`/tablero`), el ritmo de compra y la velocidad a la que aparecen los ejércitos.
- **Destino:** `docs/gameplay/board-and-map.md`.

### DEC-03: Clientes de la tablet y los móviles. Web servida por el host o apps nativas
- **Alternativas:** (a) apps nativas Flutter en Android e iOS; (b) **clientes web servidos por el host en la LAN**, que se abren desde el QR; (c) un híbrido con web para invitados y app nativa opcional.
- **Preferencia del creador (D-02):** móviles por navegador desde el QR, sin instalar nada; tablet con app nativa.
- **Recomendación ajustada:** **(c) desde el slice.** Los móviles y la pantalla pública usan el cliente web servido por el host. La tablet usa una app Android que empaqueta **el mismo cliente** (`/consola`) con Capacitor (DEC-04). La consola sigue funcionando en un navegador como respaldo.
- **Razones:**
  - No exige instalar nada (brief §15.8).
  - Evita la App Store, la cuenta de desarrollador de Apple y la Mac (C-02).
  - Hay una sola versión de cliente, la del host, así que no hay desajustes de versión entre el servidor y los móviles.
  - La tablet puede ser **cualquier dispositivo autorizado**, lo que responde a la pregunta del brief §3.3.
  - **Por qué la tablet sí gana con app nativa:** `[HECHO]` la API Screen Wake Lock solo está disponible en contextos seguros ([MDN](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Wake_Lock_API)), y la consola abre `http://<IP_LAN>`, que no lo es (§4.3). En el navegador, la tablet puede apagar la pantalla a mitad de partida. La app lo evita con un complemento nativo y además da pantalla completa, sin barra del navegador ni recargas accidentales. Los móviles se consultan de vez en cuando, así que el apagado les afecta poco.
- **Costes:** depende del navegador, sobre todo de Safari en iOS. Además está la limitación del contexto no seguro (§4.3) y la suspensión del móvil. La app de tablet empaqueta el cliente y puede quedar desfasada respecto al servidor: al conectar se compara la versión del protocolo y, si no coincide, la app pide actualizarse o usar el navegador. Una app nativa para iPad exige Xcode en macOS (C-02); sin Mac, un iPad usa la consola en el navegador (P-14).
- **Impacto:** unifica el despliegue en un solo servidor local HTTP/WS y simplifica la entrada por QR.
- **Destino:** `docs/decisions/ADR-001-stack-y-clientes.md`.

### DEC-04: Stack tecnológico
Matriz ponderada preliminar. Las puntuaciones (1–5) son **juicio preliminar de los participantes** y se recalibran con las mediciones de S1 y S2.

| Criterio (peso) | A. Flutter nativo en todo | B. Servidor y motor en Dart + clientes Flutter Web | C. Servidor y motor en TypeScript (Node) + clientes web ligeros |
|---|---|---|---|
| Unirse sin instalar, móviles heterogéneos (20) | 1 | 5 | 5 |
| Offline real (15) | 5 | 4 (hay que configurar el CDN y las fuentes) | 5 |
| Motor puro, determinista y testable (15) | 5 | 5 | 4 |
| Rendimiento en la Pi y en móviles modestos (15) | 4 | 3 (paquete de CanvasKit pesado en móviles antiguos) | 5 |
| Desarrollo en Kubuntu sin Mac (10) | 2 | 5 | 5 |
| Mantenibilidad y una sola base de código (15) | 4 | 5 | 4 |
| Comunidad open source y soporte de agentes (10) | 4 | 4 | 5 |
| **Total ponderado (sobre 5)** | **3,50** | **4,45** | **4,70** |

- **Alternativas no priorizadas** (juicio de coste para este proyecto, no incompatibilidades comprobadas):
  - Godot, por ser poco natural para paneles administrativos y formularios densos.
  - Electron, por su consumo de memoria en la Pi frente a un servidor ligero con navegador en kiosko.
  - Tauri o arquitecturas mixtas (p. ej. Dart/Rust en servidor + TS en cliente), porque mantener dos lenguajes penaliza a un desarrollador individual (C-03) sin ventaja demostrada para este MVP.
  - Qt/QML, por el coste de los clientes móviles sin instalación.
- `[HECHO]` Flutter declara compatibilidad oficial con Linux **Arm64** en Debian 10–13 y Ubuntu 20.04–24.04, y en la web con Safari 15.6 o superior. Según esa misma tabla, la salida WebAssembly solo aplica a Chrome y Edge: **Safari y Firefox reciben solo JavaScript**. Por eso la medición de la opción B en un iPhone (S1) debe hacerse con la compilación JS. Fuente: [Flutter supported platforms](https://docs.flutter.dev/reference/supported-platforms). Raspberry Pi OS se basa en Debian, pero el **dispositivo concreto** se valida en S2.
- **Recomendación:**
  - **Se recomienda la arquitectura:** host autoritativo, motor puro sin interfaz y clientes web servidos por el host; ADR-001 se aprueba con G2a. S2 y la validación en Pi pertenecen a ADR-002/G2b, obligatorio para cerrar E5, sin bloquear G3/E4.
  - **Lenguaje recomendado: TypeScript (opción C)**, ya sin empate con B tras D-02. B solo ganaba si la tablet nativa se hacía en Flutter, pero entonces los móviles cargarían Flutter Web (su criterio más débil) y la consola tendría una segunda interfaz. Con C, la tablet nativa reutiliza el cliente web mediante Capacitor. **Metas candidatas `[HIP]` en S1:** transferencia inicial por LAN ≤5 MB y mediana de arranque interactivo ≤4 s en el móvil más modesto. Usar build de producción, caché vacía y la misma pantalla de prueba; registrar dispositivo, navegador, bytes transferidos y mediana/máximo de 5 arranques. **Cero peticiones externas** es condición del requisito offline. Los límites de peso/tiempo son preferencias iniciales por aprobar en ADR-001, no hechos que demuestren superioridad de un stack. S1 mide C; B solo se mide si C no pasa las metas. Si C falla, se reduce la interfaz antes de cambiar de stack o de revisar explícitamente las metas.
  - La opción A queda descartada para el MVP.
  - **Stack concreto recomendado `[REC]`** (las bibliotecas son candidatas; ADR-001 fija versiones y S1 las verifica):
    - **Monorepo** con pnpm workspaces, TypeScript estricto en todos los paquetes y Node.js LTS en el host.
    - **`engine`:** TypeScript puro sin E/S; Vitest para las pruebas y fast-check para las pruebas por propiedades de AC-PRIV-01.
    - **`protocol`:** esquemas Zod con los que el servidor valida cada comando entrante y de los que salen los tipos del cliente.
    - **`server`:** Fastify para HTTP y archivos estáticos, `ws` para WebSocket y better-sqlite3 para SQLite. Es síncrono, lo que encaja con la cola serializada por partida (§6.3), y admite los pragmas de S4.
    - **`client`:** Vite + React, un solo bundle con `/tablero`, `/consola` y `/jugador`; mapa de 24 regiones en SVG con animaciones CSS; fuentes e iconos dentro del bundle, sin peticiones externas (AC-NET-01). React porque es lo que mejor conocen los agentes de programación (C-03), y su peso cabe en la meta de 5 MB.
    - **`console-android`:** Capacitor empaqueta el mismo cliente, con un complemento para mantener la pantalla encendida, pantalla completa y orientación fija. `[PEND: verificar en S1]` que el WebView acepte HTTP/WS sin cifrar hacia la IP del host (configuración de tráfico en claro y de contenido mixto).
    - **Pantalla pública:** Chromium en modo kiosko (DEC-05), sin cambios.
- **Impacto:** define el lenguaje del monorepo, las herramientas de prueba y el empaquetado para la Pi y laptop.
- **Destino:** `docs/decisions/ADR-001-stack-y-clientes.md` y `docs/decisions/ADR-002-pantalla-publica.md`.

### DEC-05: Cómo se muestra la pantalla pública en el host
- **Alternativas:** (a) app nativa (Flutter Linux, si se elige B); (b) **navegador en modo kiosko** (Chromium) que abre la ruta `http://127.0.0.1:<puerto>/tablero` del mismo servidor.
- **Recomendación:** **(b)** por defecto. Usa el mismo cliente web que el resto, sirve igual en la Pi que en una laptop (brief §10.5), se ejecuta en contexto seguro local (`127.0.0.1`) permitiendo `Screen Wake Lock` y no necesita empaquetar dos binarios de interfaz distintos. Se pasa a (a) solo si S2 muestra problemas de rendimiento o de pantalla completa.
- **Impacto:** elimina una aplicación específica de plataforma y unifica el renderizado del tablero.
- **Destino:** `docs/decisions/ADR-002-pantalla-publica.md`.

### DEC-06: El papel de la tablet y del moderador (tema central, brief §9.2)
- **Alternativas:** (a) un moderador neutral que no juega y ve todo; (b) un jugador que opera la tablet; (c) la tablet rota entre jugadores.
- **Recomendación:** que la tablet sea una **«consola de mesa» sin privilegios secretos**, sea quien sea quien la opere (b o c).
  - La consola captura los dados, resuelve las casillas según las reglas, muestra cartas públicas y pausa o reanuda la partida.
  - **No ve** tropas, saldo privado, cartas privadas ni objetivos de nadie, ni el orden de los mazos.
  - **No dispone** de comandos arbitrarios como «dar dinero» o «aplicar multa» (V-5).
  - Las correcciones quedan en un **registro público** sin datos secretos y, si afectan a un rival, necesitan su confirmación. Solo se edita una captura antes de confirmar su resolución (DEC-11); tras revelar una carta o resolver un combate, un «deshacer» no restaura el secreto. El MVP no ofrece rollback general: se pausa y se registra la incidencia.
  - La pestaña «Ejércitos» de la consola muestra solo información pública: presencia o banda de amenaza aproximada.
- **Por qué:** mezclar moderación con acceso a secretos rompe el juego si el operador también juega. Además, un moderador que no juega es raro en una reunión social.
- **Coste:** pierde la figura de «árbitro omnisciente» para resolver disputas. La mitigación es que el motor resuelva todo y que haya un registro auditable.
- **Impacto:** modela los permisos del protocolo, el filtrado de `vista_consola` y la interfaz de administración.
- **Destino:** `docs/architecture/authority-and-privacy.md` y `docs/ux/admin-tablet.md`.

### DEC-07: Persistencia
- **Alternativas:** (a) guardar una instantánea JSON por turno; (b) un **registro de eventos** de solo inserción **más instantáneas periódicas** en SQLite; (c) una base relacional que refleje el estado completo.
- **Recomendación:** **(b)**.
  - Permite *replay*, depuración, auditoría (DEC-06) y recuperación tras un reinicio (CE-07).
  - El motor es determinista: el barajado se hace con una semilla guardada, de modo que se puede reconstruir el estado.
  - Cada partida guarda la versión de las reglas y la del contenido.
  - **Confirmación durable:** cada comando aceptado persiste sus eventos, nueva versión y resultado de idempotencia en una sola transacción **antes** de confirmar o publicar vistas. Al reiniciar se conserva todo comando confirmado; un comando persistido cuya respuesta se perdió devuelve el mismo resultado al reintentarlo.
  - `[HECHO]` SQLite en WAL con `synchronous=NORMAL` puede perder transacciones ante un corte de energía. `[REC]` S4 compara una configuración durable, inicialmente WAL + `synchronous=FULL`, y verifica almacenamiento real; matar el proceso no equivale a cortar la energía. Fuente: [SQLite, synchronous](https://www.sqlite.org/pragma.html#pragma_synchronous).
  - La semilla, el mazo ordenado y el registro íntegro son datos de nivel `sistema`; no se incluyen en exportaciones públicas ni en recursos descargables por los clientes.
- **Impacto:** asegura integridad ante cortes eléctricos en la mesa y habilita auditoría de fin de partida.
- **Destino:** `docs/architecture/persistence.md`.

### DEC-08: Red y descubrimiento
- **Recomendación:**
  - El **QR con la URL `http://<IP_LAN>:<puerto>/jugador?sala=<codigo>`** es el mecanismo principal (usa IP numérica directa, sin depender de resolución DNS ni mDNS).
  - La introducción de IP manual + código de sala queda como respaldo inmediato.
  - mDNS (`.local`) es opcional y nunca imprescindible, porque no se resuelve de forma fiable en todos los Android ni configuraciones LAN.
  - La **configuración recomendada** es un router Wi-Fi de viaje dedicado sin conexión WAN y sin portal cautivo ni redirección DNS.
  - El lobby y la guía describen el procedimiento verificado en S1 para mantener la Wi-Fi sin Internet; desactivar datos móviles queda como diagnóstico si falla la conexión LAN, no como requisito universal ni como consecuencia atribuida a un ajuste específico (§4.3).
  - El punto de acceso Wi-Fi interno de la propia Pi se ofrece solo como alternativa si S3 demuestra estabilidad con 8 clientes simultáneos (6 móviles, la tablet y margen) `[PEND: verificar en S3]`.
- **Impacto:** reduce la fricción de entrada (CE-06) y evita caídas silenciosas por portales cautivos o cambio automático a 4G/5G.
- **Destino:** `docs/architecture/offline-lan.md`.

### DEC-09: Gobernanza unificada (ADR-000)
- **Recomendación:** adoptar como **base el paquete de Cursor** (la regla `.mdc`, la skill y las plantillas), aplicando antes de E1/E3 estas correcciones obligatorias:
  - La precedencia por estado (`APROBADO` > `PROPUESTO`) y fecha con cita explícita (G-1).
  - Una sola serie de IDs: `FS-###`, `AC-###.#`, `ADR-###`, `CARD-<modo>-###`, `EVT-###` (G-2).
  - Un único árbol de rutas documentales: el de brief §11.2 (`docs/decisions/ADR-###-*.md`, `docs/gameplay/core-loop.md`, `docs/gameplay/game-modes.md`, `docs/ux/public-display.md`, etc.), actualizando `SKILL.md` y `.mdc` y eliminando los archivos stub duplicados del paquete original (G-3).
  - El ID `parejas_18` en lugar de `couples_18` (G-4).
  - Los 4 niveles de visibilidad: `público`, `propietario`, `partes_tratado`, `sistema` (G-5).
  - **Eliminar** de `SKILL.md` la instrucción «Si aún no existen, propón y crea esta estructura base» (G-7).
  - Convertir las premisas «Flutter» y «Raspberry» en referencias a ADR-001 y ADR-002 (G-8).
  - Unificar en `.mdc` y `SKILL.md` un **único contrato de salida** de 5 puntos con los estados `LISTO_PARA_IMPLEMENTAR`, `FALTA_DOCUMENTACION` y `HAY_CONFLICTO_DOCUMENTAL` (G-9).
- **Por qué:** el paquete de Cursor aporta el flujo operativo para el agente, pero sin corregir sus rutas, contratos y premisas induciría al agente a violar el propio brief desde el primer prompt.
- **Impacto:** gobierna todo el trabajo con IA y bloquea código prematuro.
- **Destino:** `docs/decisions/ADR-000-gobernanza.md`, `AGENTS.md` y `.claude/skills/documentation-first/SKILL.md` (sin configuración de Cursor, D-05).

### DEC-10: Mapa real o mundo ficticio — **resuelta por D-06: países reales y actuales**
- **Alternativas:** (a) países reales actuales; (b) **regiones reales con nombres geográficos** (por ejemplo «Cono Sur» o «Península Ibérica») en lugar de Estados; (c) un mundo ficticio.
- **Recomendación por defecto:** **(b)**. Conserva el atractivo de la geografía real, reduce la sensibilidad de «invadir países reales», sobre todo en el modo `familiar_u18`, y evita los territorios disputados.
- El mapa es **contenido intercambiable**, de modo que la decisión no bloquea el motor.
- `[HECHO]` Natural Earth declara sus datos vectoriales y raster de dominio público. Fuente primaria: [Natural Earth, condiciones de uso](https://www.naturalearthdata.com/about/terms-of-use/). Registrar capa y versión utilizadas; esto no determina por sí solo la selección de territorios del juego.
- **Impacto:** afecta al catálogo geográfico y al arte del tablero, sin acoplar el motor.
- **Destino:** `docs/gameplay/board-and-map.md`.

### DEC-11: Captura de los dados físicos — **`OBSOLETA` por D-08 (dados virtuales)**
- **Recomendación:**
  - Capturar **cada dado `1d6` por separado**, no la suma: dos valores de 1–6 para movimiento `[HIP]`, y un valor de 1–6 por bando en combate (H-07). La fase activa del motor determina cuántos dados se esperan y de quién.
  - En la interfaz de `/consola`, mostrar **únicamente los botones `1` a `6`** (más `Borrar` y `Confirmar`) para cada dado pendiente, eliminando las teclas `7`, `8`, `9` y `0` del mockup (V-12) para impedir errores de digitación en origen.
  - Mostrar los valores ingresados en la pantalla pública con una **confirmación explícita de 1 toque** y dejar una **ventana de corrección antes de confirmar**. La confirmación cierra la captura y ejecuta sus efectos; después no se vuelve a tirar ni se deshace para cambiar una carta revelada o un combate resuelto.
  - El servidor rechaza capturas fuera de turno, fuera de rango (1–6) y duplicadas mediante `id` idempotente y `versión_esperada`.
- **Impacto:** preserva el ritual de dados reales en mesa con captura rápida y a prueba de errores.
- **Destino:** `docs/gameplay/core-loop.md` y `docs/ux/admin-tablet.md`.

### DEC-12: Licencias
- **Recomendación:**
  - Separar la licencia del **código** (por ejemplo MIT, Apache-2.0 o GPL-3.0) de la del **contenido** (por ejemplo CC BY-SA 4.0).
  - Publicar los paquetes +18 como contenido separado y claramente etiquetado.
  - Que la elección la haga el creador (P-10). No bloquea hasta E7.
- **Impacto:** protege la distribución open source y separa el código de los activos editoriales.
- **Destino:** `docs/decisions/ADR-003-licencias.md`.

### 5.13 Matriz resumen de decisiones (control de aprobación)

| ID | Tema | Recomendación | Evidencia o razón | Impacto (Juego / UX / Arq) | Riesgo principal | Confianza | Estado / ¿Requiere aprobación? | Documento destino |
|---|---|---|---|---|---|---|---|---|
| DEC-01 | Orden de trabajo | Sin papel (D-01): reglas v0 escritas (E1) + spikes (E2); después motor, simulador y visor (E4) | Decisión del creador; Docs-First se mantiene | Hoja de ruta y puerta G3 | Retrabajo si las personas cambian reglas (RK-14) | Media | `DECIDIDO POR EL CREADOR` (sustitutos `RECOMENDADO`) | `docs/roadmap/milestones.md` |
| DEC-02 | Recorrido vs mapa | Especificar A (casilla/país) y B (casilla/bloque) con comercio; compararlas en el simulador | Resuelve el choque lineal vs adyacencia (brief §5.1) | Tablero, ritmo de bloques y guerra | Que en A tarden los bloques sin reparto inicial | Media-Alta | `RECOMENDADO` / Sí (G1) | `docs/gameplay/board-and-map.md` |
| DEC-03 | Clientes móviles y tablet | Móviles: web local vía QR. Tablet: app Android (Capacitor) con el mismo cliente y navegador como respaldo (D-02) | Cero instalación para jugadores; la tablet no apaga la pantalla ni muestra la barra del navegador | UX de entrada y topología LAN | Desfase de versión de la app; iPad sin Mac | Alta | `RECOMENDADO` / Sí (G0) | `docs/decisions/ADR-001-stack-y-clientes.md` |
| DEC-04 | Stack tecnológico | Host autoritativo + motor puro en TypeScript (opción C) + Capacitor para la tablet | Un solo lenguaje y un solo cliente para 1 dev; umbrales medibles en S1/S2 | Todo el código y build | Que el WebView de la tablet bloquee HTTP/WS sin cifrar (verificar en S1) | Media-Alta | `RECOMENDADO` (P-07 respondida en parte) / Sí (G2a) | `docs/decisions/ADR-001-stack-y-clientes.md` |
| DEC-05 | Pantalla pública | Navegador en modo kiosko (`127.0.0.1/tablero`) | Misma UI web en Pi y laptop; `localhost` es contexto seguro | Host y despliegue en Pi/laptop | Configuración de reposo en Wayland/`labwc` | Alta | `RECOMENDADO` / Sí (G2b) | `docs/decisions/ADR-002-pantalla-publica.md` |
| DEC-06 | Rol de la tablet | Consola de mesa sin secretos ni comandos arbitrarios | Permite que cualquier jugador opere la tablet sin hacer trampa | Privacidad, protocolo y UX tablet | Sin árbitro omnisciente ante disputas | Alta | `RECOMENDADO` / Sí (G0) | `docs/architecture/authority-and-privacy.md` |
| DEC-07 | Persistencia | Eventos + snapshots en SQLite (`WAL` + `synchronous=FULL`) | Recuperación ante corte eléctrico, auditoría y replay | Servidor y base de datos | Latencia de fsync en microSD lenta (medir en S4) | Alta | `RECOMENDADO` / Sí (G2a/G2b) | `docs/architecture/persistence.md` |
| DEC-08 | Red y unión LAN | Router dedicado sin WAN + QR a IP numérica + fallback manual | Evita fallos de mDNS y portales cautivos | UX de lobby y operación offline | Cambio automático del móvil a datos 4G/5G | Alta | `RECOMENDADO` / Sí (G2a) | `docs/architecture/offline-lan.md` |
| DEC-09 | Gobernanza (ADR-000) | Paquete Cursor corregido con rutas §11.2 y contrato único | Elimina 9 contradicciones entre borradores (G-1 a G-9) | Flujo de trabajo con Cursor | Que el agente ignore reglas si no se instala en E0 | Alta | `RECOMENDADO` / Sí (G0) | `docs/decisions/ADR-000-gobernanza.md` |
| DEC-10 | Geografía del mapa | Regiones geográficas reales (24 en 8 bloques de 3) | Atractivo real sin conflictos diplomáticos sensibles | Contenido y arte del mapa | Preferencia del creador por países actuales | Media | `PENDIENTE` (P-02) / Sí (antes de E1) | `docs/gameplay/board-and-map.md` |
| DEC-11 | Captura de dados | Dados reales `1d6` individuales, teclado `1`–`6` y confirmación | Cumple R-03 y elimina errores del teclado `0`–`9` (V-12) | UX de consola y máquina de estados | Fricción si no se corrige antes de confirmar | Alta | `RECOMENDADO` / Sí (G1) | `docs/ux/admin-tablet.md` |
| DEC-12 | Licencias | Separar licencia de código y de contenido; aislar packs +18 | Claridad legal y control de contenido sensible | Repositorio y distribución | Indecisión sobre copyleft vs permisiva | Alta | `PENDIENTE` (P-10) / Sí (antes de E7) | `docs/decisions/ADR-003-licencias.md` |

---

## 6. Arquitectura o estrategia de ejecución

### 6.1 Estrategia general

Las reglas v0 escritas y la validación técnica en laptop convergen en G3. No hay prototipo en papel (D-01): el balance se mide en el simulador de E4 y la diversión, con personas en E5. La validación de la Pi avanza por separado y condiciona el **cierre** de E5:

```text
E0 ──┬─► E1: reglas v0 / G1 ─────────────────┐
     ├─► E2: S1, S3, S4 / G2a (laptop) ─────┴─► E3 / G3 ─► E4 (motor, simulador, visor) ─► E5 (desarrollo + sesiones) ──┐
     └─► E2: S2, S4 en Pi / G2b (Pi real) ─────────────────────────────────────────────────────────────────────────────┴─► Cierre E5 ─► E6 ─► E7
```

Si el simulador (E4) o una sesión (E5) obliga a cambiar una **regla**, y no solo un parámetro, el cambio vuelve a G1: se actualiza y se aprueba la spec antes de tocar el código.

Los spikes de E2 **no son código de producto**: se hacen en una carpeta temporal o rama desechable y solo dejan conclusiones y mediciones en los ADR. Así se cumple *Documentation First* sin bloquear el aprendizaje técnico. `[REC]`: E0 debe autorizar explícitamente los spikes como excepción documentada.

### 6.2 Núcleo jugable: base de las reglas v0 `[HIP]`

Ninguna cifra está aprobada. E1 convierte cada hipótesis en una regla v0 escrita; el simulador, las pruebas automáticas y las sesiones con personas la **confirman, ajustan o descartan**.

| ID | Hipótesis | Qué se mide (simulador o sesiones) |
|---|---|---|
| H-01 | **Mapa:** 24 países o regiones en 8 bloques de 3, geográficamente contiguos. Cada país tiene precio, arancel e ingreso territorial base (públicos), y una lista de adyacencias terrestres o marítimas | Si hay países aislados o bloques demasiado fuertes |
| H-02 | **Turno:** (1) ingreso, (2) dados físicos, (3) movimiento, (4) resolver la casilla, (5) **comercio bilateral opcional** (máximo 1 acuerdo ejecutado) y **una** acción estratégica opcional (**reclutar**, **mover** o **atacar**: nunca reclutar y atacar en el mismo turno), (6) cierre. La negociación verbal es libre en cualquier momento, pero solo surte efecto cuando se formaliza en el turno. Sin temporizador por defecto | Duración del turno (CE-02), tiempos muertos y margen de reacción ante amenazas |
| H-03 | **Compra, arancel e intercambio:** compra al caer en país libre, sin subasta; arancel al caer en país ajeno, perdonable por su dueño. En fase 5 se ejecuta como máximo un acuerdo bilateral. Solo se entregan países sin tropas reales, sin combate pendiente y de propiedad directa de los firmantes. El dueño puede confirmar desmovilizarlas sin reembolso **dentro del mismo intercambio atómico**. El resultado del acuerdo no puede dejar a un firmante sin ningún país. Todo país transferido queda bloqueado para nuevo comercio durante una vuelta completa de turnos ($t+P$, definición debajo). Ambos aceptan los mismos términos; el dinero intercambiado solo lo ven los firmantes y el sistema | Desbloqueo de bloques, coste de desmovilización y cesiones repetidas. No se transfieren tropas ni se activa un rescate vendiendo el último país |
| H-04 | **Ingresos por ronda y solvencia:** al inicio del propio turno se cobra ingreso base + suma de ingresos de países propios menos mantenimiento militar, sin depender de pasar por la salida. La tesorería exacta y el mantenimiento pagado son privados (`propietario`); el ingreso territorial base (suma de los países propios) es público. Si el saldo privado no alcanza para el mantenimiento, se cobra hasta dejar el efectivo en `0` (sin deuda negativa) y se desmovilizan automáticamente las tropas no cubiertas (empezando por el país propio con mayor guarnición y, en empate, menor ID estable). En un arancel obligatorio superior al efectivo disponible, se paga todo el saldo restante hasta `0` | Inflación, ventaja del líder, resolución sin deuda de impagos y protección del secreto militar |
| H-05 | **Bloque completo y reclutamiento sin reservas abstractas:** poseer los 3 países de un bloque permite, como acción estratégica del turno, reclutar tropas pagando su coste y desplegarlas **directamente en países propios de ese bloque** (máximo 2 tropas nuevas por bloque completo y turno `[HIP]`, sin «reservas fuera del mapa»). Todo país sin tropas reales tiene una **milicia base pública de D=1** que no se mueve ni cuesta mantenimiento. Si se pierde un país del bloque, ya no se recluta en él, pero las tropas ya desplegadas permanecen | Si los bloques se completan a tiempo y si el tope de reclutamiento por turno evita ejércitos instantáneos |
| H-06 | **Niebla de guerra:** la pantalla pública y la consola muestran solo presencia y **banda de amenaza** por país (0/milicia, baja: 1–2, media: 3–4, alta: 5+ `[HIP]`). Las cantidades exactas solo las ve el dueño en su móvil. Como H-02 separa en turnos distintos «reclutar» y «atacar», subir de banda al reclutar da al vecino al menos un turno de alerta. Una carta de espionaje revela la cifra exacta de un país solo al espía durante 1 ronda | Si la mesa entiende el peligro en el mapa sin conocer el número exacto de tropas |
| H-07 | **Combate con bajas acotadas y retirada:** desde país propio adyacente, máximo 1 ataque por turno. Atacante compromete $N$ tropas reales en secreto (1 a las disponibles); defensor usa su guarnición $D$, o $D=1$ de milicia si está vacío. Antes de tirar se pacta o se bloquea el compromiso. Con `1d6` físico por bando: $\text{Ataque}=N+d_A$, $\text{Defensa}=D+d_D+1$; el empate defiende. **Si gana el atacante:** pierde 1 solo si $D\ge N$ y $N\ge 2$; defensor pierde hasta 2 tropas reales y retira supervivientes ($D-2\ge 1$) al país propio adyacente con menor ID estable (o elección previa si se ajusta tras E5), o pierde todos si está cercado sin salida propia; atacante ocupa con sus supervivientes. **Si gana el defensor:** atacante pierde 1, o hasta 2 si el margen $\text{Defensa}-\text{Ataque}\ge 3$, sin superar $N$; sus supervivientes permanecen en origen. Defensor pierde 1 solo si $N\ge D$ y $D\ge 2$. La milicia no es tropa real ni se retira | Evita desgaste garantizado con $N=1$; medir bajas, coste de retirada y aniquilación por cerco (que sigue siendo posible si se rodea al defensor) |
| H-08 | **Casillas especiales:** cada una roba de su mazo (Hacienda, Migración, Correo, WhatsApp/mensajería y Verdad o Reto). En el MVP hay **pocas cartas de efecto acotado**, cada una con duración explícita en rondas y sin efectos acumulables del mismo tipo. **Con la tesorería privada (P-08):** un efecto proporcional al efectivo, como la «Auditoría sorpresa: paga el 20 % de tu dinero» de la captura de la tablet, revelaría el saldo si se publicara el importe. Esos efectos se resuelven en `propietario`: el público ve que se aplicó, pero no la cantidad. Los efectos públicos usan importes fijos | Si las cartas producen giros sin arbitrariedad; que ningún efecto publique saldos |
| H-09 | **Victoria candidata:** (a) **Dominio:** controlar $K=3$ bloques completos al cierre de una ronda y mantenerlos hasta el cierre de la ronda siguiente; (b) **Sumisión:** tener vigentes al cierre de ronda tratados de vasallaje sobre **todos los demás jugadores** (sin cadenas ni ciclos; una firma aislada no termina la partida); (c) **Fin por límite de rondas:** 12 rondas con 3–4 jugadores y 10 con 5–6; gana quien controle más países (propios más vasallos, contando cada país una vez), desempatando por bloques completos y, si persiste, victoria compartida. La victoria económica independiente queda diferida fuera del MVP | Duración, cesiones que regalan la victoria y agencia del vasallo. $K$ y rondas se ajustan con el simulador (E4) y las sesiones (E5) |
| H-10 | **Gobierno en el exilio:** comienza al perder el último país que se poseía; empezar una partida con 0 países no activa rescate. Se conserva turno y subsidio. **H-10B, base recomendada (respeta R-04 sin excepción):** reentrada civil compensada, sin tropas nuevas. Mediante un vale protegido de rescate y usando la acción estratégica, el exiliado adquiere al banco un país libre (si existe, sin exigir caer en él) o, si los 24 países están ocupados, toma un país elegible según los dos niveles públicos y condiciones detalladas debajo, indemnizando el banco a su dueño por el precio base. El antiguo dueño conserva todas sus tropas (que se repliegan sin bajas); el exiliado recibe solo milicia ($D=1$). **H-10A, candidata condicionada a P-13:** insurgencia con $1+d_I$ contra $D+d_D+1$ para obtener país y 1 tropa, pagando su precio al banco. H-10A no demuestra por sí sola CE-08; cualquier elección de esa variante debe conservar una salida viable en los casos sin posibilidad de victoria | Validar acceso al rescate, conservación de tropas, privacidad de elegibilidad y posibles ciclos de pérdida/reentrada. La compensación no demuestra que el efecto se perciba justo |
| H-11 | **Tratados formalizados en el MVP:** compraventa/intercambio de países, no agresión, tregua, préstamo y vasallaje. Cada tratado temporal tiene duración en rondas; romperlo aplica una penalización sistémica pública. Las promesas verbales fuera de esos tipos no obligan al motor | Si se usan y si la traición resulta divertida y no frustrante |
| H-12 | **Verdad o Reto:** siempre se puede **pasar sin justificarlo**, con penalización moderada, fija y visible antes de aceptar. Si el jugador no tiene efectivo suficiente, se cobra hasta donde alcance su saldo (mínimo 0), sin generar deuda ni bloquear el turno. Cero retos con alcohol obligatorio, daño o contacto físico no consentido (brief §7.1) | Comodidad del grupo, posibilidad efectiva de pasar sin dinero y ritmo |

**Comprobaciones matemáticas y preparación de las reglas v0 (E1):**
- **Probabilidades de victoria en H-07:** Con dados `1d6` justos e independientes, el atacante vence si $N + d_A > D + d_D + 1$. Contando sobre las 36 parejas posibles $(d_A, d_D)$:
  - Con $N = D$: el atacante gana en **10/36 (27,8 %)** de las tiradas.
  - Con $N = D + 1$: gana en **15/36 (41,7 %)**.
  - Con $N = D + 2$: gana en **21/36 (58,3 %)**.
  - Con $N = D + 3$: gana en **26/36 (72,2 %)**.
  - Con $N = D + 4$: gana en **30/36 (83,3 %)**.
- **Ejemplos auditables de H-07 (casos límite verificados):**
  1. *Ataque mínimo contra milicia ($N=1$ vs $D=1$ virtual):* Si $d_A=6, d_D=1$ ($7 > 3$), gana el atacante; como $N=1$, sufre 0 bajas y ocupa el país con su 1 tropa.
  2. *Ataque mínimo contra fortaleza ($N=1$ vs $D=5$ reales):* El defensor gana **36/36**: el máximo ataque es 7 y la mínima defensa es 7, y el empate defiende. El atacante pierde su única tropa y el defensor sufre 0 bajas. Con $D=4$, en cambio, el atacante gana 1/36 (solo dados 6 y 1). Esta regla elimina el desgaste garantizado con ataques de $N=1$, pero no convierte todos los ataques en posibilidades reales de conquista.
  3. *Batalla grande con retirada ($N=4$ vs $D=3$ reales):* Si $d_A=5, d_D=2$ ($\text{Ataque}=9 > \text{Defensa}=6$), gana el atacante sin bajas ($D < N$), el defensor pierde 2 tropas y su **1 tropa superviviente se retira** al país propio adyacente con menor ID estable (o se elimina si está cercado sin salida propia), y el atacante ocupa el país con sus 4 tropas.
- **Ficha de parámetros inicial (`docs/gameplay/parameters.md`, E1):** Tabla versionada con precios `20–40`, ingreso base `10` + `5` por país, arancel `5–10`, tropa `10`, mantenimiento `2` por tropa a partir de la 3.ª y subsidio de exilio `15`. El vale civil de rescate cubre el precio base máximo del catálogo (`40` en esta ficha), no es efectivo libre. Deben fijarse también antes de jugar: tesorería inicial, orden/asiento inicial, movimiento militar, redondeos y vencimiento de efectos. **`países_iniciales_por_jugador`: `0` (base) frente a `2` de bloques distintos** si A no forma bloques hacia ronda 5; el simulador compara un cambio cada vez, manteniendo el resto de parámetros. El motor lee estas cifras de los datos de contenido, nunca de constantes en el código.

**Precisiones operativas consolidadas para las reglas v0 (E1/G1):**
- **H-10B, elegibilidad pública y conservación:** (1) países fuera de bloque completo cuyo dueño conserve al menos otro país tras la cesión; (2) si ese conjunto está vacío, países de los colíderes en **propiedad directa**, con al menos 2 países. En nivel 2 se ofrecen los de menor **banda pública** de amenaza, no menor cantidad secreta; el exiliado elige entre los empatados. Con 24 países y 3–6 jugadores, un colíder siempre tiene más de un país cuando otro está exiliado. Así existe destino para replegar todas las tropas: país propio adyacente de menor ID o, si no existe, cualquier otro propio de menor ID. No hay bajas, transferencia de tropas ni reducción a cero países del antiguo dueño. La lista de objetivos se obtiene solo de información pública; elegir el mínimo exacto habría revelado comparaciones entre guarniciones ocultas.
- **H-10B, financiación y activación:** al perder el último país por conquista rival o efecto obligatorio se habilita un vale de rescate, protegido frente a impuestos/aranceles y limitado al mayor precio base del catálogo. No puede venderse ni financiar tropas o H-10A. Con mapa lleno cubre la indemnización íntegra al dueño; si hay países libres, permite elegir y adquirir uno al banco mediante la acción estratégica, sin exigir caer en él. Se consume al recuperar un país; el sobrante caduca y también caduca si se recupera por otra vía. Vale, indemnización, propiedad y repliegue se resuelven juntos; el país adquirido recibe el enfriamiento comercial H-03 ($t+P$). Las cesiones voluntarias del MVP no pueden dejar al cedente sin países; por tanto no generan un vale. El vale se liga al precio máximo del catálogo porque una reserva fija (p. ej. `20`) sería insuficiente frente a precios de `40`. El simulador (E4) debe medir reconquistas sucesivas que vuelvan a activar el rescate; no se declara resuelto ese riesgo de balance, y si aparece un ciclo de «cosecha de indemnizaciones», se probará como palanca que el antiguo dueño recién indemnizado no pueda atacar el país cedido durante una vuelta ($t+P$) o que la indemnización al dueño se pague como máximo una vez por partida y par de jugadores.
- **H-10A, límite persistente:** cambiar la elegibilidad no cambia sus probabilidades: contra D≥5 es imposible ganar; contra milicia, dos intentos fallan ambos aproximadamente el 52,2 %. Aprobar la excepción a R-04 no basta para afirmar que esta variante cumple CE-08. G1 debe documentar su salida civil u otra solución comprobable.
- **Comercio H-03 y anti-abuso:** una propuesta no reserva recursos y caduca al cerrar el turno o al cambiar el estado confirmado. Primero se valida **sin modificar el estado** el resultado conjunto de desmovilización autorizada, pagos y cesiones: firmas, saldo, propiedad, tropas, enfriamiento y que cada firmante conserve al menos un país. Si algo falla, no cambia nada, incluidas las tropas que se pretendía desmovilizar. Si pasa, todo se persiste y publica como una única operación. Enfriamiento: si la transferencia ocurre en el turno global $t$ con $P$ participantes, no se puede volver a comerciar ese país antes del inicio del turno $t+P$. Terminar turno incrementa $t$ una vez; reconectar o reiniciar no lo altera. No vence simplemente al llegar el turno inmediato del comprador. Una oferta inválida usa error genérico sin revelar saldo.
- **Retirada H-07:** Para evitar una decisión adicional tras los dados, la hipótesis inicial usa el país propio adyacente con menor ID estable como destino automático; suma allí los supervivientes. Sin destino legal se aplica el cerco ya previsto. Se publica el destino y su nueva banda, nunca el número trasladado. Si esta prioridad resulta artificial en las sesiones de E5, se sustituye por elección previa del defensor al declarar la defensa. Las bajas directas están acotadas a 1–2, pero **el cerco sí puede eliminar una guarnición grande completa**.

### 6.2.1 Traza de referencia de fin a fin (guion del MVP y subconjunto para E5)

Esta secuencia ilustra el MVP (`[HIP]` sujeta a validación en E4/E5). **E5 cubre pasos 1–6 y 8**, usando espionaje como su única casilla especial y cierre por límite de rondas; **el pacto del paso 7 pertenece a E6**. En E5, una salida negociada del combate consiste solo en desistir antes de los dados, consumiendo la acción estratégica; pagos, cesiones por combate y pactos persistentes requieren sus specs de E6. La traza contiene saltos entre turnos: el guion reproducible de E3 debe especificar estado inicial, turnos omitidos, dados, semilla, precios y resultados esperados. No es todavía una partida simulada ni una prueba ejecutada.

| Paso | Acción en la mesa y dispositivos | Validación y efecto en el motor (`engine`) | Qué muestran `/tablero` y `/consola` (`vista_pública` / `vista_consola`) | Qué ve cada móvil en `/jugador` (`vista_jugador(i)`) |
|---|---|---|---|---|
| **1. Lobby y unión** | El host abre la sala `GC-42` y proyecta el QR en `/tablero`. La tablet se empareja como consola; Ana, Beto, Carla y Diego escanean el QR, eligen nombre, color y PIN de 4 dígitos, y aceptan el modo `familiar_u18`. | Crea sesiones autenticadas, asigna orden de turno, guarda semilla RNG y baraja mazos en nivel `sistema`. | Sala `GC-42`, 4 jugadores conectados, mapa inicial con 24 regiones libres y modo activo. | Su propio perfil, saldo inicial privado y estado «Sincronizado». |
| **2. Dados y compra** | Turno de Ana: cobra ingreso inicial, lanza dos dados físicos (`4` y `3`). El operador pulsa `4` y `3` en el teclado `1`–`6` de `/consola` y confirma. Ana cae en «Península Ibérica» (libre) y confirma comprarlo desde su móvil (o consola). | Verifica turno y rango `1`–`6`, avanza la ficha 7 casillas, descuenta el precio del saldo privado de Ana y le asigna el territorio. | Movimiento de la ficha de Ana, «Península Ibérica» cambia al color de Ana; el ingreso territorial base de Ana sube. | Ana ve su nuevo saldo exacto y su territorio; los demás no ven el saldo exacto de Ana. |
| **3. Intercambio y bloque** | Tras varias rondas, Ana tiene 2 regiones de «Europa Sur» y Beto tiene la 3.ª («Italia/Grecia»). En fase 5, Ana propone cambiar «Andes Centrales» por «Italia/Grecia», ambas sin tropas reales. Beto confirma los mismos términos. | Revalida la propuesta según H-03, ejecuta todo el intercambio o nada, aplica enfriamiento comercial de 1 vuelta completa ($t+P$) a ambos países y marca «Europa Sur» completo (3/3) para Ana. | Anuncio del intercambio y emblema de bloque completo. | Ana ve habilitado reclutar; ningún móvil ajeno recibe saldos. |
| **4. Reclutamiento oculto** | En el turno siguiente, como acción estratégica (fase 5), Ana recluta en secreto 2 tropas en «Península Ibérica» desde su móvil. | Descuenta el coste del saldo privado de Ana, suma +2 tropas reales a «Península Ibérica» y recalcula la banda de amenaza. | En «Península Ibérica» el icono pasa de milicia a **Amenaza Baja**, sin mostrar el número `2` ni el gasto de Ana. | Solo Ana ve `Tropas: 2` y su nuevo saldo; Beto, Carla, Diego y la consola ven solo «Amenaza Baja». |
| **5. Casilla especial y espionaje** | Carla cae en «Correo Electrónico». La consola resuelve la casilla; Carla recibe en su móvil una carta privada de **Filtración / Espionaje** y la usa sobre «Península Ibérica». | Verifica validez del objetivo y añade un permiso temporal de visibilidad para Carla sobre ese país durante 1 ronda. | Registro público: «Carla jugó una carta de inteligencia sobre Península Ibérica». | Carla ve en su móvil `Península Ibérica: 2 tropas (Ana)` durante 1 ronda; el resto sigue viendo solo la banda. |
| **6. Invasión y combate** | En un turno posterior, Ana (que ya acumuló $N=3$ tropas en «Península Ibérica») declara ataque contra «Magreb» de Diego (quien tiene $D=1$ tropa real oculta). No hay acuerdo previo. Ana tira `1d6` físico (`5`) y Diego tira `1d6` físico (`2`); la consola captura `5` y `2` y confirma. | Calcula $\text{Ataque} = 3 + 5 = 8$ vs $\text{Defensa} = 1 + 2 + 1 = 4$. Gana Ana: sufre 0 bajas ($D < N$). Diego pierde hasta 2 tropas reales y, como solo tenía $D=1$, no le quedan supervivientes que retirar (la retirada de H-07 exige $D - 2 \ge 1$). Ana ocupa «Magreb» con 3 tropas y «Península Ibérica» vuelve a la milicia. | Anuncia: «Ana conquista Magreb». Actualiza colores y bandas de amenaza. **No** publica los números `3` y `1`, aunque los dados físicos `5` y `2` son públicos. Si hubiera retirada, el cambio de banda en el país de destino sería una revelación prevista en la matriz de revelaciones. | Ana ve sus 3 tropas ahora en «Magreb»; Diego ve que perdió «Magreb» y su tropa. |
| **7. Tratado formalizado** | Diego propone desde su móvil un **Pacto de No Agresión (2 rondas)** con Ana. Ana acepta en su móvil. | Registra el tratado activo por 2 rondas; el motor bloqueará ataques directos entre ambos salvo ruptura con penalización pública. | El panel de acuerdos muestra «Pacto de No Agresión: Ana ↔ Diego (2 rondas)». | Ambos ven el tratado activo y el coste de penalización si decidieran romperlo. |
| **8. Cierre y victoria** | Al cerrarse la ronda 12 (límite para 4 jugadores en H-09), el motor evalúa las condiciones de fin de partida. | Cuenta territorios bajo control directo o vasallaje; Ana lidera con 9 regiones y 2 bloques completos. | Pantalla de fin de partida con el ganador, estadísticas y resumen histórico de la sesión. | Resumen personal de cada jugador. |

### 6.3 Arquitectura lógica `[REC]`

```text
                 Router Wi-Fi dedicado (sin WAN)
 ┌───────────────────────────────────────────────────────────────┐
 │ HOST (Raspberry Pi 5 o laptop)                                │
 │  servidor: HTTP (sirve los clientes) + WebSocket              │
 │   ├─ motor puro: comando → validación → eventos → estado      │
 │   ├─ proyecciones: estado → vista_pública / vista_jugador(i)  │
 │   │                / vista_consola   (filtrado en servidor)   │
 │   ├─ contenido: mapa y mazos por modo, validados al cargar    │
 │   └─ persistencia: SQLite (eventos + instantáneas)            │
 │  navegador en kiosko → http://127.0.0.1:<puerto>/tablero      │
 └───────────────┬───────────────────────┬───────────────────────┘
          /consola (tablet)       /jugador (móviles, vía QR)
```

- **Autoridad.** Solo el motor del servidor cambia el estado. Los clientes envían comandos con `id`, `versión_esperada` y parámetros. **El servidor obtiene rol y jugador de la sesión autenticada**, nunca de campos elegidos por el cliente. Una cola por partida serializa comandos y valida permisos, fase, turno, recursos y objetivo antes de persistirlos.
- **Privacidad por construcción.** Las proyecciones son funciones puras del motor y se prueban en aislamiento (`AC-PRIV-*`). El servidor **nunca envía el estado completo** a ningún cliente. Los logs públicos y los privados se generan por separado. Los rankings y gráficos solo usan campos públicos (territorios, bloques e ingresos territoriales base).
- **Alcance de la protección.** `[REC]` El MVP protege contra otras vistas y clientes manipulados, suponiendo un host y una LAN de confianza. HTTP/WS no ofrece confidencialidad de transporte; el dueño del host puede leer la base de datos. No se promete secreto frente a ese dueño ni a interceptación de red. Si ese alcance no basta, ADR-001 debe resolver HTTPS/WSS y su instalación offline antes de aprobar el despliegue. El registro público sirve para revisar acciones; no prueba por sí solo la honestidad del host.
- **Niveles de visibilidad:**
  - `público`: pantalla, consola y todos los jugadores.
  - `propietario`: solo el jugador dueño del dato (tesorería exacta, tropas exactas por país, cartas en mano).
  - `partes_tratado`: los firmantes de una propuesta o cláusula bilateral mientras no sea pública.
  - `sistema`: semilla RNG, orden de los mazos y estado interno completo; no se envía a ningún cliente.

  La consola **no** tiene un nivel propio de secretos (DEC-06).
- **Matriz de revelaciones autorizadas e inferencias acotadas (contrato para `authority-and-privacy.md` y `AC-PRIV-04`):**

| Evento o acción | Qué ve `público` / `consola` | Qué ven `propietario` / `partes_tratado` | Inferencia acotada aceptada |
|---|---|---|---|
| **Reclutamiento, movimiento o desmovilización** | Solo si cambia la **banda de amenaza** (`0/milicia`, `1–2`, `3–4`, `5+`) en los países afectados; nunca el coste ni la cifra | El dueño ve sus tropas exactas por país y su nuevo saldo | Subir o bajar de banda acota el rango de tropas del país, lo cual es intencional (H-06) |
| **Cobro de ingresos y mantenimiento (H-04)** | Ingreso territorial base por ronda (según países públicos). Si hay desmovilización forzosa por saldo 0, solo se ve el cambio de banda si ocurre | El dueño ve el desglose exacto (ingreso base + territorial − mantenimiento) y su efectivo | Ninguna sobre tropas mientras no cambie una banda |
| **Combate y retirada (H-07)** | País atacante y objetivo, dados físicos `d_A` y `d_D`, vencedor, país destino de retirada (si hubo) y nuevas bandas de amenaza | Cada bando ve sus propias bajas y tropas restantes exactas en origen/destino | Saber quién ganó con dados públicos acota la diferencia $N - D$, sin revelar las cifras exactas salvo caso extremo (p. ej. milicia conocida). Que haya retirada revela que $D \ge 3$, y su ausencia tras una victoria atacante revela que $D \le 2$ si el defensor no estaba cercado (el cerco se puede deducir del mapa público); ambas inferencias se aceptan como parte del diseño |
| **Carta de Espionaje (H-06)** | Qué jugador usó espionaje y sobre qué país | Solo el jugador espía ve la cifra exacta de tropas de ese país durante 1 ronda | El dueño sabe que ese país fue espiado |
| **Carta proporcional al efectivo (H-08, p. ej. Auditoría 20 %)** | Que la carta se aplicó al jugador objetivo, **sin publicar el importe descontado** | Solo el afectado ve el importe descontado y su nuevo saldo | Ninguna sobre el saldo |
| **Comercio bilateral (H-03)** | Países intercambiados y que hubo acuerdo | Solo los dos firmantes (`partes_tratado`) ven el monto de dinero incluido | Si una oferta falla, el error es genérico y no revela si faltó saldo |
| **Reentrada civil H-10B** | Exilio, vale disponible, objetivos elegibles calculados con países/bloques/bandas públicos; país cedido, precio base compensado y destino del repliegue | El antiguo dueño ve sus tropas exactas reubicadas y la indemnización; el exiliado recibe país con milicia, sin consultar tropas ajenas | La elegibilidad no compara cantidades secretas. Las nuevas bandas tras el repliegue dan rangos; su combinación con observaciones anteriores se prueba como en combate |
| **Impago parcial de arancel o penalización fija (H-04, H-12)** | Evento de «pago parcial por insolvencia» | El afectado ve su saldo en `0`; el acreedor del arancel ve cuánto cobró realmente | Revela que el jugador quedó con efectivo `0` en ese instante (fuga parcial aceptada y documentada) |

- **Límite de la matriz:** describe las revelaciones permitidas, no demuestra por sí sola ausencia de inferencias nuevas. AC-PRIV-04 debe combinar historial público con datos legítimos de cada observador (p. ej. cobros recibidos, bajas propias o espionaje previo). Una secuencia que reconstruya tropas mediante pagos no previstos exige revisar la regla o su revelación **antes** de G1/G3; no basta declarar cada mensaje inocuo por separado.

- **Identidad local.**
  - Al unirse, cada jugador elige su nombre, su color y un **PIN de 4 dígitos**.
  - El servidor emite un token de sesión que se guarda en el almacenamiento local del navegador.
  - Reconectarse desde el mismo dispositivo es automático. Hacerlo desde otro dispositivo requiere el PIN y la confirmación en la consola.
  - El QR/código de sala permite solicitar ingreso, no otorga identidad de otro jugador ni rol de consola. La consola se empareja mediante un código de autorización mostrado una sola vez en el host al crear la sala. El PIN tiene intentos limitados; el reemplazo de dispositivo revoca su sesión anterior.
  - Es una protección contra suplantaciones triviales entre amigos, no contra ataques criptográficos.
- **Reconexión.** Al reconectarse, el cliente pide la vista actual completa, no un diff, para que sea simple y robusto. Una tablet desconectada no bloquea la partida: la consola puede reabrirse en otro dispositivo autorizado.
- **Estados de UX del slice.** Cada superficie distingue `conectando`, `sincronizada`, `comando_pendiente` y `desconectada`. Una compra, intercambio, ataque o tratado muestra resumen antes de confirmar y no aparece aplicado hasta la respuesta del host; al perder conexión se bloquean nuevas acciones y se conserva el ID del comando pendiente para consultar o reintentar sin duplicarlo. Al terminar la sesión se borra la vista privada. Sin móvil compatible, se usa un dispositivo prestado con sesión privada; el modo de pasar un mismo teléfono entre varios jugadores queda fuera del MVP salvo spec propia.
- **Estructura del repositorio** (se crea **solo** tras aprobar ADR-001). Es más reducida que la del brief para que la mantenga una sola persona:

```text
geoconquista/
  docs/                 # fuente de verdad (§6.5)
  packages/
    engine/             # dominio + reglas + RNG con semilla + proyecciones (sin E/S)
    protocol/           # comandos, eventos, vistas y versión del protocolo
    content/            # esquemas, mapa y mazos por modo, validador
  apps/
    server/             # HTTP/WS, SQLite, sirve el cliente
    client/             # un cliente con 3 rutas: /tablero, /consola, /jugador
    console-android/    # app de tablet: Capacitor que empaqueta /consola (D-02)
  tools/
    simulator/          # simulación de balance con el engine
    viewer/             # visor de desarrollo: una persona juega todos los asientos (D-01)
```

  **Justificación:** el brief propone 6 paquetes y 4 apps. `domain` y `rules` se fusionan porque separarlos no aporta pruebas adicionales. La persistencia vive en el servidor hasta que haya otra consumidora. Un solo cliente con roles evita triplicar el código común. La app de tablet no es un segundo cliente: solo empaqueta el mismo código. El visor es una herramienta interna, no una superficie del producto. La separación motor/protocolo/contenido/apps, que es la que importa para las pruebas y la trazabilidad, se mantiene.

### 6.4 Contenido y las cinco modalidades `[REQ]` + `[REC]`

- **Mismo núcleo para todos los modos.** Cambian los mazos, las verdades y los retos, y quizá la intensidad de algunos eventos.
- **Esquema mínimo de carta:**
  - `id`, `tipo` y `modos[]`.
  - `intensidad` (1–3).
  - `visibilidad` y `objetivo_válido`.
  - `efecto`: una referencia tipada a un efecto **definido en la spec**, nunca código libre ni `eval`.
  - `duración`, `permite_pasar` (siempre verdadero en Verdad o Reto), `penalización_al_pasar`.
  - `estado_editorial`: `borrador`, `revisado` o `aprobado`.
  - `revisado_por`.
- **Regla de clasificación.** Una carta compartida entre modos debe aprobar la revisión del modo **más estricto** que incluya. Lo que pertenezca a `familiar_u18` se revisa de forma independiente.
- **Cambio de modo.** En el MVP el modo **se fija al iniciar la partida**. Cambiarlo durante la partida queda `[PEND]` (P-04b).
- **Catálogo del MVP.** E3 fija el mínimo del slice y E6 el de cada modo según frecuencia de robo observada y capacidad de revisión. Cuando un mazo se agota, se rebarajan sus descartes usando el RNG determinista del motor; no se promete ausencia de repeticiones durante 120 min sin medir antes la tasa de robo en E1/E5.

### 6.5 Documentation First operativo

**Estados de documento:** `PROPUESTO`, `PENDIENTE`, `APROBADO` (con aprobador y fecha) y `OBSOLETO`.

**Árbol mínimo canónico:** el del brief §11.2, más `docs/decisions/ADR-000-gobernanza.md` y `docs/testing/acceptance-matrix.md` (eliminando los nombres divergentes del paquete de Cursor según G-3).

**Orden de redacción en E3:**
1. `docs/product/vision.md`
2. `docs/gameplay/core-loop.md`
3. `docs/gameplay/board-and-map.md`
4. `docs/gameplay/territories-and-blocks.md`
5. `docs/gameplay/economy.md`
6. `docs/gameplay/armies-and-fog-of-war.md`
7. `docs/gameplay/combat.md`
8. `docs/architecture/authority-and-privacy.md`
9. `docs/architecture/protocol.md`
10. `docs/ux/public-display.md`, `admin-tablet.md`, `player-mobile.md`, `lobby.md`
11. `docs/architecture/persistence.md` y `offline-lan.md`
12. `docs/gameplay/game-modes.md`, `truth-or-dare.md` y `docs/content/card-catalog-and-governance.md`
13. `docs/gameplay/diplomacy.md` y `victory-and-endgame.md`
14. `docs/testing/test-strategy.md`, `acceptance-matrix.md` y `playtest-plan.md`

Con D-01, los documentos 2–7, `docs/gameplay/parameters.md` y la parte de `victory-and-endgame.md` sobre el fin por límite de rondas se redactan antes, en E1, como reglas v0. E3 solo los reabre si otro documento los contradice. `playtest-plan.md` describe las sesiones digitales de E5/E6, no pruebas en papel.

**Alcance documental de G3.** Todos estos temas deben estar cubiertos y aprobados para el alcance del vertical slice, incluidas sus exclusiones e interfaces con el MVP. El catálogo completo de los cinco modos, los tratados adicionales y sus specs detalladas pueden permanecer `PENDIENTES` fuera del slice hasta E6; no autorizan código por adelantado. Así se conserva *Documentation First* sin redactar cada carta antes de probar el núcleo digital. El creador aprueba; el autor o agente propone y mantiene la trazabilidad.

**Definition of Ready:** la de `extras.md` §1, más dos condiciones: que la spec cite la regla v0, o el resultado del simulador o de una sesión, que la respalda y que tenga el estado `APROBADO`.

**Definition of Done:** la de la regla `.mdc`, más la fila actualizada en `docs/testing/acceptance-matrix.md`.

**Guía para los agentes:** las reglas están en `AGENTS.md` y la skill en `.claude/skills/documentation-first/SKILL.md` (DEC-09, D-05). Cada tarea empieza con el contrato de salida unificado de 5 puntos, que exige declarar `LISTO_PARA_IMPLEMENTAR`, `FALTA_DOCUMENTACION` o `HAY_CONFLICTO_DOCUMENTAL` antes de tocar cualquier archivo.

---

## 7. Etapas, entregables y dependencias

No hay fechas: no se dispone de estimaciones justificadas (brief §12.2). Cada etapa termina en una **puerta** con criterios de salida.

| Etapa | Entregables | Depende de | Criterio de salida (puerta) |
|---|---|---|---|
| **E0. Gobernanza y visión** | ADR-000 (DEC-09), `AGENTS.md` y la skill; `docs/README.md` con registro de decisiones; `vision.md`; resolver P-01/P-03 y registrar cuándo se atenderán las demás preguntas según §10; autorización formal de los spikes desechables | Aprobación de este plan | **G0:** el creador aprueba ADR-000 y las decisiones de arranque que adopte |
| **E1. Reglas v0** (sin prototipo en papel, D-01) | Documentos de gameplay del slice (§6.5, pasos 2–7) con las reglas de H-01 a H-12; `docs/gameplay/parameters.md` con todas las cifras; las dos variantes de recorrido especificadas; los escenarios límite de §8.3 escritos como casos ejecutables (estado inicial, comandos, dados y resultado esperado) | G0 | **G1:** el creador aprueba las reglas v0 como provisionales para el slice; sin huecos en los escenarios límite; mecanismo de exilio elegido (H-10B o H-10A, P-13) y comportamiento del slice ante la pérdida del último país definido. No demuestra balance ni diversión: eso queda para E4 y E5 |
| **E2. Spikes técnicos** (en paralelo con E1, código desechable) | **S1:** Android antiguo e iPhone reales por QR, HTTP/WS y recursos locales; en la tablet, una app Capacitor de prueba que conecta por HTTP/WS sin cifrar a la IP del host y mantiene la pantalla encendida; probar Wi-Fi sin Internet, suspensión, reconexión y carga según protocolo DEC-04. **S2:** Pi 5, HDMI y kiosko local; verificar configuración de reposo y concesión/liberación de Wake Lock; mapa de 24 regiones durante 2 h. **S3:** router sin WAN y aislamiento; AP interno de Pi solo si se ofrecerá. **S4:** SQLite WAL + FULL, fallos antes/después de commit/respuesta y corte eléctrico en almacenamiento de prueba | G0 | **G2a (stack, LAN y persistencia en laptop Linux):** ADR-001 con evidencias de S1, S3 y S4 en host de desarrollo; la opción elegida pasa las metas de carga de DEC-04 aprobadas y reconexión sin dominios externos; la app de tablet (si es Android) conecta y mantiene la pantalla encendida. **G2b (hardware Pi 5):** ADR-002 con S2 pasando AC-HW-01 y S4 verificado en el almacenamiento real de la Pi (microSD/SSD) |
| **E3. Documentación crítica** | Los documentos de §6.5 aprobados **en el alcance del slice**; specs `FS-001` en adelante con AC; matriz de aceptación; esquema de contenido y política común de los cinco modos (los borradores pueden iniciarse en paralelo conforme cierren G0 y S1) | G1 y G2a. G3 **no espera a G2b**: `public-display.md` se aprueba con la evidencia de la laptop, y sus metas específicas de la Pi (reposo, FPS, temperatura) quedan delegadas a ADR-002, que debe estar aprobado antes de cerrar E5 | **G3: autorización de código.** Ningún conflicto documental en el alcance del slice y sus dependencias; DoR cumplido para todas las specs del slice |
| **E4. Motor, simulador y visor** | `engine`, `protocol` y `content` con pruebas deterministas y de privacidad, incluidos los escenarios límite de E1; simulador con bots simples que sustituye la parte medible del papel (D-01): ronda del primer bloque, rondas según el número de jugadores, variante A frente a B, `países_iniciales_por_jugador`, bajas de H-07, ciclos de rescate H-10B y sesgo por asiento; visor de desarrollo para jugar todos los asientos en una pantalla | G3 | AC del motor del slice en verde; partidas reproducibles por semilla, invariantes y fin de partida comprobados; informe del simulador que fija la variante y los parámetros del slice en `parameters.md`. Los bots no certifican diversión, negociación ni duración humana |
| **E5. Vertical slice digital** | Servidor, cliente con 3 rutas y app Android de consola (D-02): lobby; dados; movimiento; compra e intercambio H-03; bloques; reclutamiento oculto; ataque/retirada H-07; Correo con una carta de espionaje como única casilla especial; cierre por límite de rondas; guardado y recuperación; contenido mínimo de `familiar_u18`; **sesiones con personas** en laptop antes de la de aceptación, con actas de CE-01/02/03/08 (son las primeras pruebas humanas del proyecto) | E4 para desarrollar e integrar en laptop; **G2b obligatorio para cerrar E5** | Sesión de aceptación con 4 personas en Pi 5 real y router sin WAN; pasos 1–6 y 8 de §6.2.1, con preparación reproducible de E3; CE-04/05/06/07 superados. El pacto del paso 7 no es requisito de E5 |
| **E6. MVP** | Economía completa, tratados H-11, las 5 casillas, cinco modos con catálogos revisados, vías de victoria H-09 y mecanismo de exilio **elegido y aprobado en G1**, accesibilidad, host alternativo Linux y rejoin desde otro dispositivo. Windows/macOS sin promesa hasta validarlos | E5 y specs ampliadas y aprobadas antes de cada implementación | Partida completa con 3, 4, 5 y 6 jugadores; solo reutilizar actas de las mismas reglas y versión digital. CE-01 y AC del MVP superados; traza completa incluido el paso 7 |
| **E7. Publicación open source** | Licencias (ADR-003), guía de instalación para la Pi y la laptop, `CONTRIBUTING.md` con el proceso docs-first, CI con las pruebas, paquetes de contenido +18 separados y etiquetados | E6 | Repositorio público; una instalación limpia en la Pi siguiendo solo la guía tiene éxito |

**Dependencias críticas:**
- DEC-02 condiciona `board-and-map`, el motor y la pantalla.
- DEC-06 condiciona la privacidad, la UX de la consola y el protocolo.
- El resultado de S1 y P-07 condicionan ADR-001 (`G2a`).
- Separar `G2a` (laptop Linux) de `G2b` (Pi 5 real) garantiza que una demora en la Pi 5 o su almacenamiento no bloquee E3 ni el desarrollo del motor puro en E4 (cumpliendo C-05), sin rebajar la exigencia de probar en la Pi real antes de cerrar E5.
- P-02 condiciona el arte del mapa, pero no el motor.
- D-02 y P-14 condicionan la app de consola: sin tablet Android, la consola del slice usa el navegador.
- P-08 (tesorería), P-11 (dados de combate) y P-13 (H-10B civil sin tropas vs H-10A con excepción a R-04) condicionan la ficha de parámetros de E1. Si no hay respuesta previa, E1 usa las opciones por defecto de §10.1 y lo registra en el acta.

**Recursos materiales para E2 y E5.** Son un supuesto; no se dan precios porque no se han verificado. Si un recurso falta, solo se bloquea el spike que lo usa.

| Recurso | Lo usa | Nota |
|---|---|---|
| Raspberry Pi 5 con fuente oficial, refrigeración y la pantalla o TV de mesa | S2, S4 (`G2b`), E5 | C-05; su ausencia temporal no bloquea `G2a` ni E4 |
| Almacenamiento del host: la microSD prevista y, como alternativa, un SSD | S4 (`G2b`) | `[HIP]` La latencia de `synchronous=FULL` depende del medio. S4 mide en el almacenamiento real; si la microSD no cumple, se recomienda un SSD en ADR-002 |
| Router de viaje sin WAN | S1, S3 (`G2a`), E5 | DEC-08 |
| El Android más antiguo y un iPhone del grupo de juego, más la tablet de consola (Android para la app de D-02) | S1 (`G2a`) | Definen los umbrales reales de CE-06 y AC-NET-02 |
| 2–4 dados d6 | E5 | Sin compras especiales (brief §8). Con D-01 ya no hacen falta mapa impreso, fichas ni sobres |

### 7.1 Arranque inmediato: primeras acciones ejecutables

Este orden sirve para empezar sin escribir código de producto:

1. El creador responde P-01 y P-03 (antes de G0) y, si puede, también P-02, P-08, P-13 y P-14. P-07 ya tiene recomendación (DEC-04). Las demás preguntas se responden con su opción por defecto hasta su fecha límite.
2. Se crea el repositorio **solo con `docs/`, `AGENTS.md` y la skill**: ADR-000 con la corrección de G-1 a G-9, `docs/README.md` con el registro de decisiones y `vision.md`. Ningún directorio `apps/` ni `packages/` hasta G3.
3. Se aprueba G0 y se registra por escrito la autorización de los spikes desechables, fuera de la rama principal.
4. En paralelo:
   - **E1:** se redactan las reglas v0, `parameters.md`, el mapa de 24 regiones con sus adyacencias como datos y los escenarios límite como casos ejecutables.
   - **E2:** S1, S3 y la prueba inicial de S4 pueden empezar ya con la laptop Linux como host (`G2a`), y S2/S4 en la Pi 5 (`G2b`) en cuanto esté conectada.
5. Con las reglas v0 aprobadas (`G1`) y `G2a` (ADR-001) se cierran E3 y la puerta G3 para iniciar E4. El informe del simulador fija la variante y los parámetros del slice; las primeras sesiones con personas llegan en E5. Con `G2b` (ADR-002) se habilita el cierre en hardware de E5.

---

## 8. Validación y criterios de aceptación

### 8.1 Aceptación del plan (antes de E3)
- El creador responde las preguntas marcadas como «antes de G0» en §10.
- ADR-000 resuelve G-1 a G-9.

### 8.2 Criterios de aceptación técnicos del MVP (borrador; los IDs definitivos se fijan en E3)

La matriz de E3 asignará cada AC a su spec, hito, responsable y evidencia. E4/E5 cubren el núcleo del slice; exilio y tratados completos se verifican en E6. Un escenario calculado en este plan es una expectativa de prueba, **no evidencia de que la implementación pasó**.

| ID | Criterio |
|---|---|
| AC-CORE-01 | Cada país pertenece como máximo a un jugador; tropas y efectivo nunca son negativos. Turno, fase y recursos habilitan las acciones. Reclutar exige bloque completo, salvo una excepción de H-10A expresamente aprobada. Repetir una secuencia documentada de comandos/dados con el mismo estado y semilla da el mismo resultado. |
| AC-COMBAT-01 | Ejemplos de §6.2 y las 36 parejas de dados por configuración límite dan los resultados esperados; cubrir milicia, N=1/D=5, retirada con varias salidas y cerco. Las tropas finales equivalen a las iniciales menos las bajas previstas; ninguna se duplica al ocupar o retirar. |
| AC-END-01 | El slice termina al límite de rondas con su desempate documentado. Antes de implementar el MVP, la spec de H-09 debe fijar prioridad entre condiciones simultáneas y probar pérdida/recuperación de un bloque durante la ronda de dominio, expiración de vasallaje y empate. Cada país se cuenta una sola vez y se rechazan ciclos de vasallaje. |
| AC-PRIV-01 | Para cualquier estado generado (incluidos estados aleatorios de prueba por propiedades), `vista_jugador(i)` no contiene la cantidad exacta de tropas, el efectivo exacto, las cartas privadas ni los objetivos de ningún $j \neq i$, salvo lo revelado temporalmente por un efecto vigente dirigido a $i$. |
| AC-PRIV-02 | `vista_consola` y `vista_pública` no contienen ninguna cantidad exacta de tropas, efectivo privado ni el orden de los mazos. |
| AC-PRIV-03 | Los rankings, gráficos, notificaciones y logs públicos se calculan únicamente con campos públicos (territorios, bloques e ingresos territoriales base). Hay una prueba automática que lo verifica. |
| AC-PRIV-04 | Para cada observador (público, consola y cada jugador), estados/historias con iguales datos autorizados producen iguales vistas antes de una revelación prevista. Probar secuencias, no solo campos aislados: insolvencia→ingreso→mantenimiento→arancel, bajas propias, espionaje vencido y lista de objetivos de H-10B. No se acepta reconstrucción de tropas por pagos o elegibilidad no prevista en §6.3; las excepciones de combate/espionaje deben constar en la spec aprobada. |
| AC-AUTH-01 | Un cliente que manipula jugador/rol en el payload, solicita otra vista privada o abre `/consola` sin código de emparejamiento no obtiene permisos ni secretos. Un ingreso por QR no puede reclamar un asiento ocupado; se limita el intento de PIN y el dispositivo sustituido pierde acceso de inmediato. |
| AC-CMD-01 | Un duplicado autorizado con el mismo ID y parámetros devuelve el resultado persistido sin aplicarse otra vez, aunque su versión ya sea antigua. Un comando nuevo con `versión_esperada` obsoleta se rechaza con error visible. |
| AC-CMD-02 | Una captura de dados fuera de turno, con una cantidad de dados distinta de la requerida por la fase actual, o con un valor fuera de `1`–`6`, se rechaza en el servidor; además, la interfaz de `/consola` solo renderiza botones `1`–`6` por cada dado pendiente. |
| AC-CMD-03 | Dos comandos concurrentes incompatibles no consumen dos veces el mismo saldo, tropa o país. Un reintento tras reiniciar conserva la deduplicación. Reutilizar un ID con parámetros diferentes se rechaza; el resultado anterior solo se devuelve a su sesión autorizada. |
| AC-TRADE-01 | Validar el resultado hipotético de desmovilización, pagos y cesiones antes de mutar. Una oferta rechazada deja intactas **también las tropas**. La ejecución válida es indivisible y no deja a ningún firmante sin países. Una entrega A→B en turno $t$ impide B→C antes de $t+P$ aunque B juegue inmediatamente después. Caducidad, reintento y reinicio respetan ese vencimiento; un corte nunca deja una mitad aplicada. |
| AC-EXILE-01 | H-10B funciona con efectivo 0 y país de precio 40 usando el vale; empezar con 0 países no lo concede. La cesión nunca quita el último país a su dueño ni elimina/transfiere sus tropas. Cubrir todos los bloques completos, ausencia de vecinos propios, varias bandas empatadas y vuelta al exilio. Cambiar tropas secretas dentro de la misma banda no cambia objetivos elegibles. Pago, consumo del vale, enfriamiento y propiedad se aplican una sola vez. |
| AC-UX-01 | Antes de confirmar dados se pueden corregir; después de confirmar y resolver no se puede deshacer para cambiar una carta revelada o un combate resuelto. La pérdida de conexión muestra el estado pendiente y bloquea nuevas acciones; recuperar conexión no duplica el comando. |
| AC-UX-02 | En la pantalla y distancia reales de mesa, cuatro jugadores identifican turno, propietario, bloques y bandas de amenaza sin acercarse; objetivo inicial: 5 s a 2 m. Todo color de jugador se acompaña de símbolo/etiqueta accesible. Se prueba en S2/E5, antes del arte definitivo. |
| AC-NET-01 | Con el DNS y la WAN bloqueados, la partida se crea, se juega, se guarda y se restaura sin peticiones fallidas a dominios externos. Se verifica con la captura de red del navegador. |
| AC-NET-02 | Un móvil que se suspende 5 min y se reactiva recupera su vista sincronizada en menos de 5 s, sin perder sesión ni requerir recarga manual. |
| AC-PERS-01 | Tras un corte de energía se conserva **todo comando confirmado, incluido el último**. Un comando en vuelo cuya respuesta no llegó puede estar guardado o ausente; al reintentarlo con su mismo ID se aplica como máximo una vez. Se prueban fallos inyectados antes del commit, después del commit/antes de responder y después de responder. |
| AC-PERS-02 | Una partida guardada con una versión de reglas o contenido distinta se rechaza con un mensaje claro, o se migra de forma determinista si existe migración documentada. |
| AC-HW-01 | En la Pi 5, `/tablero` se muestra a pantalla completa por HDMI durante 2 h sin bloqueos, sin apagado de pantalla por inactividad (Wake Lock / desactivación de reposo en Wayland/`labwc`) y con animaciones fluidas. La meta numérica de FPS y temperatura se fija en ADR-002 a partir de S2. |
| AC-CONT-01 | El validador de contenido rechaza en CI y al arrancar el servidor cualquier carta sin modo, sin estado editorial `aprobado`, con efectos no registrados en la spec, o de `familiar_u18` con intensidad o etiquetas no permitidas. |
| AC-MODE-01 | En cada uno de los 5 modos, la partida solo carga y roba cartas clasificadas para ese modo. |
| AC-TOD-01 | Toda verdad o reto ofrece «Pasar» sin explicación y con penalización visible antes de aceptar, incluso con saldo cero (cobrando hasta el disponible sin deuda ni bloqueo). Cada participante acepta el modo en el lobby antes de iniciar; ningún modo eleva la intensidad durante la partida. |

### 8.3 Validación de la jugabilidad

Se usan las actas de las sesiones con personas (E5/E6) con las métricas CE-01, CE-02, CE-03 y CE-08, más:
- **Ventaja del primer jugador:** tasa de victoria según el orden de asiento, en el simulador y en las mesas.
- **Estrategia dominante:** una vía que supera el 60 % en el simulador es una señal exploratoria para revisar parámetros, no un fallo automático. Se registran número de partidas, semillas, políticas de los bots y distribución por asiento, repitiendo con perfiles distintos antes de atribuir el resultado a las reglas. Las mesas humanas deciden sobre negociación, faroleo y diversión.
- **Comprensión:** un jugador nuevo explica su situación, sus bloques y las bandas de amenaza vecinas tras 3 rondas.
- **Cobertura obligatoria (escenarios escritos en E1; pruebas automáticas y simulador en E4):** exilio con 8 bloques completos, efectivo 0, precios de 40 y ningún comerciante voluntario; dueño potencial con un solo país; inicio con 0 países frente a pérdida posterior del último; repetidas reconquistas del país rescatado. Retirada con varias salidas y cerco; venta fallida tras autorizar desmovilización; A→B→C en turnos consecutivos; inferencias encadenadas de §6.3. Registrar decisiones disponibles y efectos sobre terceros, no solo que exista una acción legal.
- **Orden de prioridad:** primero cerrar reglas ejecutables y privacidad del núcleo; después comparar el ritmo de los recorridos en el simulador con una sola modificación por ensayo; luego evaluar diversión y balance en las sesiones con personas. No ampliar mapas, contenido ni variantes mientras fallen esos criterios. G1 registra qué hipótesis se descartaron; G3 solo autoriza las que llegaron a specs aprobadas.

### 8.4 Lista de control contra el brief §19.4

El plan se considera insuficiente si incumple alguno de estos puntos:
- Incluye las cinco modalidades (R-14, E6).
- Mantiene los dados físicos (DEC-11).
- No depende de Internet (AC-NET-01).
- No filtra ejércitos ni por interfaz ni por costes públicos (AC-PRIV-* y matriz de §6.3).
- No toma nada de las capturas como aprobado (§4.4, V-1 a V-13).
- No programa código de producto antes de G3 (§7).
- Trata la relación entre el recorrido y el mapa y el desbloqueo de bloques (DEC-02, H-03).
- Trata a los eliminados incluso con mapa lleno y 8 bloques completos, los turnos largos y la ventaja acumulativa (H-02, H-04, H-05 y H-10).
- Incluye una traza de referencia de fin a fin (§6.2.1) y matriz de decisiones (§5.13).
- Incluye pruebas en la Pi y de recuperación ante corte eléctrico (S2, S4, AC-PERS-01 y AC-HW-01).
- Separa el vertical slice (E5), el MVP (E6) y lo excluido (§3.2).

---

## 9. Riesgos, supuestos y medidas de respuesta

### 9.1 Riesgos priorizados

| # | Riesgo | Prob. | Impacto | Mitigación | Disparador o señal |
|---|---|---|---|---|---|
| RK-01 | **Turnos eternos.** Compra, comercio, carta, ataque y negociación en el mismo turno | Alta | Alto | H-02 (1 acción estratégica por turno: reclutar, mover o atacar), comercio limitado a 1 acuerdo ejecutado, negociación libre fuera de turno y mazos acotados | Media de turno superior a 90 s en el visor o en las sesiones E5 |
| RK-02 | **El recorrido aleatorio impide completar bloques** y los ejércitos llegan tarde o nunca | Alta | Alto | Comercio/intercambio bilateral con desmovilización atómica desde las reglas v0 (H-03), comparación con la variante B en el simulador (DEC-02) y parámetro `países_iniciales_por_jugador = 2` (de bloques distintos) si en A no hay bloques hacia la ronda 5 | Menos de 1 bloque completo en toda la mesa hacia la ronda 5 en el simulador |
| RK-03 | **Bola de nieve, cerco, cesiones rotatorias o ciclos de rescate** | Media | Alto | Retirada H-07; enfriamiento hasta $t+P$; H-10B compensada con vale no convertible, objetivos por bandas públicas y conservación de tropas. Probar reconquistas repetidas (y bloqueo de reataque $t+P$ del dueño indemnizado si hay abuso) y efecto sobre el ganador | Líder de ronda 5 gana más del 70 % de simulaciones; jugador sin agencia 2 rondas; rescates que generan compensaciones repetidas o deciden sistemáticamente al ganador |
| RK-04 | **Fuga de secretos** por consola, costes públicos, cartas proporcionales, ranking, botón «Ver mazo», logs o permisos falsificados | Media | Alto | DEC-06, tesorería privada (P-08), matriz de revelaciones de §6.3, mazos en nivel `sistema`, AC-PRIV-* y AC-AUTH-01; explicitar host y LAN de confianza | Cualquier fallo de privacidad o deducción exacta no prevista |
| RK-05 | **Scope creep o agente que inventa reglas** | Alta | Alto | ADR-000, DoR, corrección de rutas y contrato único en `.mdc` y `SKILL.md` (DEC-09) y revisión de cada PR contra las specs | Código sin ID de spec o conflicto documental |
| RK-06 | **Safari o móviles antiguos** no rinden o suspenden WebSocket | Media | Medio | S1 con el mismo protocolo de medición para B/C (compilación JS en Safari), metas candidatas de DEC-04 y reconexión AC-NET-02 | S1 falla en carga, CE-06 o AC-NET-02 |
| RK-07 | **Aislamiento o pérdida de acceso LAN** en Wi-Fi sin Internet | Media | Alto | Router sin WAN ni portal, QR numérico y guía basada en el comportamiento observado en S1; no asumir la causa por el nombre de un ajuste | Fallos en S1 o S3 |
| RK-08 | **Contenido +18 problemático o mal clasificado** | Media | Alto | Revisión editorial, el modo más estricto manda, opción de pasar siempre disponible incluso sin saldo (AC-TOD-01) y cero retos peligrosos (brief §7.1) | Una carta sin revisión en un paquete |
| RK-09 | **Marcas y sensibilidad geopolítica:** «WhatsApp», su logo y países reales en conflicto | Media | Medio | P-05, DEC-10 (regiones geográficas) y prohibición de usar logos de terceros o activos de Turista, Risk o Monopoly | Revisión antes de E7 |
| RK-10 | **Hardware de la Pi:** pantalla que entra en reposo (DPMS/`swayidle`), drivers o temperatura, o retraso en disponer de la Pi | Media | Medio | Desacoplar `G2a` (laptop Linux) de `G2b` (Pi 5) para no frenar E3/E4; S2 temprano con desactivación de salvapantallas en Wayland/`labwc` y `Screen Wake Lock` en `127.0.0.1` | S2 falla en AC-HW-01 |
| RK-11 | **Exceso de pantalla:** la mesa pierde el protagonismo | Media | Alto | Móvil solo para consultar secretos y confirmar acciones, dados siempre físicos (DEC-11) y encuesta CE-03 tras cada sesión | CE-03 por encima del 30 % |
| RK-12 | **Partidas guardadas incompatibles** entre versiones | Baja | Medio | La versión de reglas y contenido se guarda en cada partida (DEC-07, AC-PERS-02) | Cambio de reglas tras la publicación |
| RK-13 | **Agotamiento del desarrollador individual** por un alcance excesivo | Media | Alto | Sin prototipo en papel (D-01), puertas G0–G3, monorepo compacto de 3 paquetes y 2 apps (§6.3) y un slice E5 pequeño (sin el motor de tratados temporales de E6) | E5 se alarga sin acercarse a sus criterios |
| RK-14 | **Retrabajo por reglas no probadas con personas** (consecuencia de D-01) | Alta | Medio | Cifras en datos (`parameters.md`), reglas en módulos pequeños con sus AC, simulador y visor antes del slice, reglas v0 marcadas como provisionales y primeras sesiones de E5 en laptop, antes de pulir la interfaz | Una sesión de E5 obliga a cambiar una regla sustantiva, no solo un parámetro |
| RK-15 | **App de tablet desfasada o inviable** (iPad sin Mac, WebView que bloquea HTTP/WS sin cifrar) | Media | Medio | Comparación de versión del protocolo al conectar, consola siempre disponible en el navegador, verificación en S1 y P-14 | Error de versión en la consola, fallo de conexión en S1 o tablet iPad en el grupo |

### 9.2 Supuestos de este plan (a confirmar)

- Los de §4.2: C-02 (sin Mac), C-03 (un solo desarrollador), C-04 (presupuesto bajo) y C-05 (Pi 5 disponible).
- Sin prototipo en papel (D-01), el creador puede reunir al menos una mesa de 4 personas para las sesiones de E5; E6 cubre todo el rango admitido (3 a 6 jugadores).
- El español es el único idioma del MVP.
- `[REC consolidada de A, B y C]` La tesorería exacta y el gasto militar son privados durante la partida; los países, bloques y el ingreso territorial base son públicos y sostienen el ranking y los gráficos (R-10). La decisión final pertenece al creador (P-08).

---

## 10. Preguntas y desacuerdos pendientes

### 10.1 Preguntas al creador (agrupadas por hito de decisión)

Están agrupadas según el momento en que se necesitan para no abrumar el arranque. **Ninguna es bloqueante para aprobar este plan**: cada una tiene una opción por defecto recomendada que permite avanzar si el creador prefiere decidir más adelante.

**Grupo 1 — Arranque, gobernanza y stack técnico (antes de G0 / G2a):**

| ID | Pregunta | Opción por defecto recomendada | Cuándo se necesita |
|---|---|---|---|
| P-01 | ¿Quién opera la tablet? ¿Un jugador, un turno rotativo o un moderador que no juega? | Una consola sin secretos, operada por cualquiera (DEC-06) | Antes de G0 |
| P-03 | ¿Acepta clientes web servidos por el host en lugar de apps nativas para el MVP? | Sí (DEC-03) | Antes de G0 |
| P-07 | ¿Tiene experiencia o preferencia firme por Flutter/Dart, o por TypeScript/web? | **Respondida en parte (D-02):** web para los móviles y app nativa para la tablet. Recomendación: TypeScript en todo y la consola empaquetada con Capacitor para Android (DEC-04); falta aprobarla en ADR-001 | Antes de G2a |
| P-14 | ¿La tablet de consola es Android o iPad? | **Respondida (D-03):** Android como principal; iPad secundario. La app de iPad con Capacitor necesita compilarse en macOS (Mac propia o servicio de compilación en la nube) | Antes de S1 |

**Grupo 2 — Reglas y mapa para las reglas v0 (antes de E1 / G1):**

| ID | Pregunta | Opción por defecto recomendada | Cuándo se necesita |
|---|---|---|---|
| P-08 | ¿La tesorería exacta de cada jugador es privada o pública? Con costes por tropa, los cambios de saldo públicos revelan el ejército | **Respondida (D-07): privada.** Tesorería y gasto militar privados; ingresos territoriales, países y bloques públicos (§4.3). Si prefiere efectivo público, usar un presupuesto de defensa opaco o reclutamiento por cupo de bloque | Antes de E1 |
| P-02 | ¿Mapa de países reales, regiones reales o mundo ficticio? | **Respondida (D-06): países reales y actuales.** Queda abierta P-15 | Antes de E1 |
| P-09 | ¿Rango de jugadores 3–6 y duración objetivo de 90–120 min (3–4 jug.) y <150 min (5–6 jug.)? | Sí, como hipótesis que las sesiones de E5/E6 deben validar | Antes de E1 |
| P-11 | ¿Los combates también usan dados físicos? | **Respondida (D-08): no.** Los dados son virtuales y caen en la tablet. Ver P-16 | Antes de E1 |
| P-13 | ¿Para el jugador en exilio prefiere la reentrada civil compensada sin tropas (H-10B, que respeta R-04 al 100 %) o acepta la excepción a R-04 de crear 1 tropa mediante insurgencia con dado (H-10A)? | **Respondida (D-09): asilo político.** El creador propone un mecanismo nuevo en lugar de H-10A o H-10B; queda abierta P-17 | Antes de G1 |
| P-15 | Con países reales (D-06): ¿cuántos países son jugables? R-04 exige bloques de 3, así que son múltiplos de 3. ¿Qué pasa con el resto del mundo y con los territorios disputados? | **Respondida (D-12):** 24 países en 8 bloques, con las demás recomendaciones. **24 países jugables en 8 bloques contiguos de 3**, como en las cifras del plan. El resto del mundo se dibuja en gris, no jugable. Ningún territorio disputado es jugable; las fronteras siguen la capa *de facto* de Natural Earth. Sin banderas reales (`art-direction.md` §7) | Antes de E1 |
| P-16 | Con dados virtuales (D-08): ¿el movimiento también se lanza agitando el móvil? ¿La tirada se ve también en la pantalla grande? | **Respondida (D-13):** solo deslizar el dedo, para movimiento y combate. Sí a las dos: un único mecanismo para movimiento y combate; los dados caen en la tablet y el tablero repite el resultado con una animación breve | Antes de E1 |
| P-17 | Asilo político (D-09): qué gana el asilado, qué recibe quien lo acoge, si se puede rechazar, qué pasa sin «poder» que ofrecer y cómo se sale del asilo | **Respondida en parte (D-14):** si nadie lo acoge, queda eliminado. El resto se propone en `docs/README.md`. Ver la propuesta de `docs/README.md`, D-09 | Antes de G1 |

**Grupo 3 — Modos, marcas, curaduría editorial y publicación (antes de E3 / E6 / E7):**

| ID | Pregunta | Opción por defecto recomendada | Cuándo se necesita |
|---|---|---|---|
| P-04 | (a) Modo Parejas +18: ¿se juega en duplas o individualmente con eventos de pareja? (b) ¿Se permite cambiar de modo durante la partida? | Individual con cartas de pareja; modo fijo en el MVP | Antes de E3 (`game-modes.md`) |
| P-05 | ¿La casilla «WhatsApp» mantiene ese nombre público o se renombra, por ejemplo a «Mensajería» o «Chat privado»? | Nombre genérico en la interfaz pública, sin el logo; «WhatsApp» como referencia temática interna | Antes de E3 |
| P-12 | ¿Quién revisa editorialmente el contenido +18 y el de `familiar_u18`? | El creador, más al menos una persona externa por paquete | Antes de E6 |
| P-10 | ¿Licencia del código y del contenido? | La decide el creador. Separar código y contenido (DEC-12) | Antes de E7 |
| P-06 | *Cerrada por requisito expreso:* el nombre es **Geoconquista** | Mantener R-01; las capturas («Dominio Global») no reabren esta decisión | No requiere respuesta |

### 10.2 Puntos convergidos y asuntos pendientes de revisión

**Estado consolidado al cierre de la fase inicial (turno 9).** Todos los desacuerdos registrados entre los participantes A, B y C quedaron resueltos con argumentos técnicos y verificaciones aritméticas (**0 desacuerdos pendientes**). Sin embargo, la rotación de turnos dejó sin revisión cruzada completa las precisiones de B del turno 8 (no revisadas por A) y las de C del turno 9 (no revisadas por A ni B); se detallan en «Puntos sin consenso». Los acuerdos entre participantes **no sustituyen la aprobación del creador**.

| Tema | Estado entre A, B y C | Qué falta |
|---|---|---|
| Tesorería privada, con países, bloques e ingreso territorial públicos (P-08) | **Acordado por A, B y C** | Respuesta del creador (P-08) |
| E1 acotado: comparación A/B y dos partidas completas (4 y 6 jugadores) | **Acordado por A, B y C**; **sustituido por la decisión del creador D-01** (sin papel) | Reglas v0 (`G1`), simulador (E4) y sesiones (E5) |
| Arquitectura: host autoritativo, motor puro, clientes web locales, kiosko y monorepo reducido | **Acordado por A, B y C** | ADR-001 (`G2a`) y ADR-002 (`G2b`) con evidencias de S1–S4 |
| Lenguaje: TypeScript (C) o Dart/Flutter Web (B) | **Acordado por A, B y C** (recomendación condicionada, sin discrepancia). Revisión posterior: C + Capacitor para la tablet, tras D-02 | Aprobación del creador en ADR-001 y medición en S1 |
| Combate H-07 con bajas acotadas, retirada determinista y cerco | **Acordado por A, B y C** (incluidas las inferencias de retirada $D\ge 3$ / $D\le 2$ en §6.3) | Calibración en el simulador (E4) y las sesiones (E5) |
| Comercio H-03 de países sin tropas, desmovilización atómica, enfriamiento $t+P$ y prohibición de quedar con 0 países | **Acordado por B y C**; A aceptó la base (países sin tropas, desmovilización y enfriamiento) en el turno 7, pero no revisó las tres precisiones de B del turno 8 que C aceptó en el turno 9 | Prueba de ritmo y anti-abuso en el simulador (E4) y las sesiones (E5) |
| Exilio H-10: dos niveles, reentrada civil H-10B por defecto con vale protegido, conservación de $\ge 1$ país del dueño anterior y selección por bandas públicas | **Acordado por B y C**; A aceptó H-10B y los dos niveles en el turno 7, pero no revisó el vale, la exclusión del dueño con 1 país ni la selección por bandas públicas (B, turno 8), que C aceptó en el turno 9 | Respuesta a P-13 y validación en E4/E5 de equidad, ciclos de rescate y agencia |
| Desacoplamiento G2a/G2b: G3, E4 y el desarrollo de E5 no esperan a la Pi; el cierre de E5 sí | **Acordado por A, B y C** | Evidencia real en Pi 5 y aprobación de `G2b` antes de cerrar E5 |
| Alcance de E5: pasos 1–6 y 8 de la traza; el pacto del paso 7 queda para E6 | **Acordado por A, B y C** | Guion reproducible en E3 |

**Comprobaciones abiertas para el simulador (E4) y las sesiones (E5)** (son hipótesis a medir, no desacuerdos del debate):
- Si 10–12 rondas bastan para llegar a la fase militar con el recorrido A. Si no, se prueba `países_iniciales_por_jugador = 2` (de bloques distintos) o la variante B antes de alargar la partida.
- Si H-10B, al romper el bloque de un colíder, actúa como un freno a la bola de nieve aceptable o como una forma de hacer de árbitro del ganador.
- Si la regla de retirada automática por menor ID resulta artificial en la mesa.
- Si el vale no convertible y las reconquistas repetidas subsidian indirectamente al conquistador (probando la palanca de bloqueo de reataque $t+P$ del dueño indemnizado si ocurre); y si impedir ceder voluntariamente el último país limita demasiado la diplomacia.
- Si alguna secuencia de impagos, ingresos y cobros privados permite reconstruir tropas fuera de las revelaciones autorizadas.

**Historial de revisiones:** el detalle turno a turno (versiones 1 a 9, con lo que cada participante aceptó, rechazó o corrigió) está en `debate.md`. La tabla anterior recoge el estado vigente.

---

## Puntos sin consenso

Al cierre de la fase inicial (turno 9) ningún participante mantenía una objeción abierta. Los desacuerdos registrados durante el debate (tesorería pública o privada, dimensionamiento de E1, regla de bajas de H-07, suficiencia de la insurgencia para el exilio y criterio de selección de objetivos de H-10B) se cerraron con la aceptación expresa de quien discrepaba. Sin embargo, por el orden de rotación (A → B → C), tres bloques de cambios no fueron revisados por todos los participantes. Se registran aquí con la postura de cada uno; no se tratan como consenso.

**1. Criterio de selección de objetivos en el nivel 2 de H-10B (mapa lleno con todos los bloques completos).**
- **C (turno 6):** el exiliado toma el país **menos guarnecido** de los colíderes. Motivo: garantizar siempre un objetivo legal y cargar el coste de la reentrada en quien lidera.
- **A (turno 7):** aceptó la elegibilidad en dos niveles y **conservó ese criterio**; sus correcciones se limitaron a la condición verificable de mapa lleno y al repliegue no letal.
- **B (turno 8):** lo **rechazó**: calcular la lista con la guarnición exacta revelaría comparaciones entre fuerzas secretas no contempladas en la matriz de revelaciones. Propuso usar exclusivamente la **menor banda pública de amenaza** y la propiedad territorial, y marcó el punto como pendiente de revisión de C.
- **C (turno 9):** aceptó la versión de B. A no volvió a intervenir, de modo que su última postura registrada es la del criterio exacto. El texto de §6.2 y §6.3 recoge la versión de B y C.

**2. Precisiones de B (turno 8) aceptadas por C (turno 9) y no revisadas por A.** Afectan a H-03, H-10B, §6.3 y §8.2:
- Vale protegido de rescate ligado al precio máximo del catálogo, en lugar de la reserva fija de `20` que C propuso en el turno 6 y A conservó en el turno 7. Motivo de B: una reserva de `20` no indemniza un país de precio `40`; empezar sin países no debe activar rescate.
- Exclusión como objetivo de los países cuyo dueño solo tiene uno. Motivo de B: sin otro país no hay destino donde conservar sus tropas.
- Enfriamiento comercial hasta $t+P$ en lugar de «siguiente turno del comprador» (C, turno 6). Motivo de B: el comprador puede jugar inmediatamente después y volver a transferir el país.
- Validación conjunta sin mutar el estado antes de ejecutar desmovilización, pagos y cesiones. Motivo de B: desmovilizar antes de validar podía eliminar tropas en una oferta rechazada.
- Prohibición de que una cesión voluntaria deje a un firmante con 0 países; nuevos AC-CORE-01, AC-COMBAT-01, AC-END-01 y AC-EXILE-01; AC-PRIV-04 ampliado a historias por observador; orden de prioridad de §8.3.

C los aceptó íntegramente con comprobación lógica propia (turno 9). A no los vio.

**3. Añadidos de C (turno 9) sin revisión de A ni B.**
- La palanca condicional ante una «cosecha de indemnizaciones»: que el dueño recién indemnizado no pueda atacar el país cedido durante $t+P$, o que la indemnización se pague como máximo una vez por partida y par de jugadores (§6.2 H-10B, RK-03 y comprobaciones abiertas de §10.2). Motivo de C: dejar lista una mitigación determinista para el riesgo de reconquistas repetidas que B señaló en el turno 8. B solo había pedido que E1 lo midiera; no propuso ni evaluó esa palanca.
- La agrupación de §10.1 en tres bloques por hito y la declaración de acuerdo unánime en la tabla de §10.2. Esta consolidación ajustó dos filas de esa tabla para reflejar quién revisó cada precisión; el resto se mantiene.

---

## Observaciones del consolidador pendientes de revisión

1. **Momento de crear la estructura de código.** §6.3 dice que `packages/` y `apps/` «se crea solo tras aprobar ADR-001», que se aprueba en `G2a`. §7.1 (paso 2) dice «Ningún directorio `apps/` ni `packages/` hasta G3». Son compatibles si rige la condición más tardía (G3), pero el plan no lo dice y G-7 exige una regla única. Conviene fijarla en ADR-000.
2. **Pérdida del último país durante E5.** El slice incluye conquista (H-07) y una sesión de aceptación con 4 personas, pero el exilio (H-10) se verifica en E6 según §8.2. Si un jugador pierde su último país en la sesión de E5, el slice no define qué ocurre. Opciones a decidir: incluir un H-10B mínimo en E5, que el guion reproducible de E3 impida ese caso, o especificar un comportamiento provisional (por ejemplo, conservar turno y subsidio sin reentrada).
3. **Documentos del brief §11.2 ausentes del orden de redacción de E3.** §6.5 declara canónico el árbol del brief §11.2, pero su lista de 14 pasos omite `docs/architecture/system-context.md` y `docs/architecture/deployment.md`. Falta indicar si pertenecen al alcance del slice (G3) o a E6/E7; la guía de instalación de E7 depende de `deployment.md`.
4. **Numeración de §5.13.** La matriz resumen se titula «5.13» aunque las decisiones usan los encabezados DEC-01 a DEC-12 y no existen §5.1 a §5.12. Se conserva porque §8.4 y las actas la citan así; renombrarla exigiría actualizar esas referencias.

---

## Observaciones de la revisión del 2026-11-04 pendientes de revisión

**Estado al 2026-11-06:** las reglas v0 proponen solución para la 2 (`economy.md` §4: el banco completa el arancel), la 4 (`armies-and-fog-of-war.md` §3: mover), la 5 (`core-loop.md` §2) y la observación 2 del consolidador (`victory-and-endgame.md` §3: asilo). La 1 (objetivos secretos) sigue abierta.

1. **Objetivos secretos sin definir.** AC-PRIV-01 y DEC-06 protegen los «objetivos» de cada jugador, que el brief §3.2 lista como candidatos, pero ninguna hipótesis los define y las vías de victoria de H-09 son públicas. Hay que decidir si entran al MVP o se quitan de esos textos.
2. **Impago parcial revela el saldo exacto al acreedor.** En la matriz de §6.3, el acreedor ve cuánto cobró; como el deudor queda en `0`, conoce su efectivo exacto previo. La matriz solo admite que se revela el `0`. Hay que corregir la inferencia aceptada o cambiar la regla.
3. **El paso 6 de §6.2.1 puede caer en la observación 2 del consolidador.** Si «Magreb» era el último país de Diego, el slice entra en exilio sin regla. El guion de E3 debe fijar que Diego conserva otros países. Con D-01, el comportamiento ante la pérdida del último país queda como requisito de G1 (fila E1 de §7).
4. **Movimiento militar sin regla.** H-02 permite «mover» como acción estratégica, pero ninguna hipótesis define cómo, y el paso 6 lo necesita. Debe quedar en las reglas v0.
5. **Cláusula redundante en H-02.** «Nunca reclutar y atacar en el mismo turno» ya se deduce de permitir una sola acción estratégica por turno.
