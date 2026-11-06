# Hitos y puertas

| Campo | Valor |
|---|---|
| Estado | `APROBADO` por el creador, 2026-11-05 (G0). El mapa de países se añadió después, con D-06 y D-12 |
| Fecha | 2026-11-05 |
| Fuente | Plan de arranque §6.1 y §7, con D-01 a D-10 |

No hay fechas, porque no existen estimaciones justificadas. Cada etapa termina en una **puerta** con criterios de salida. El detalle completo (entregables, dependencias y recursos) está en el [plan de arranque](plan-de-arranque.md) §7.

## Línea principal

```text
E0 ──┬─► E1: reglas v0 / G1 ─────────────────┐
     ├─► E2: S1, S3, S4 / G2a (laptop) ─────┴─► E3 / G3 ─► E4 ─► E5 (desarrollo + sesiones) ──┐
     └─► E2: S2, S4 en Pi / G2b ───────────────────────────────────────────────────────────┴─► Cierre E5 ─► E6 ─► E7
```

| Etapa | Qué produce | Puerta de salida | Estado |
|---|---|---|---|
| **E0. Gobernanza y visión** | ADR-000, `AGENTS.md`, skill, `docs/README.md`, `vision.md` y este documento | **G0:** el creador aprueba ADR-000 y la visión; quedan autorizados los spikes y la exploración de arte y audio | **Completada:** G0 aprobada el 2026-11-05 |
| **E1. Reglas v0** | Documentos de gameplay del slice, `parameters.md`, el mapa de países (D-06) como datos, el asilo político (D-09) y los escenarios límite como casos ejecutables | **G1:** el creador aprueba las reglas v0 como provisionales para el slice | **Completada:** G1 aprobada el 2026-11-06 (FS-001 a FS-008) |
| **E2. Spikes** | S1 (móviles y app Android de tablet en la red local), S2 (Pi 5 y kiosko), S3 (router sin WAN), S4 (SQLite durable) | **G2a:** ADR-001 con evidencia en laptop. **G2b:** ADR-002 con evidencia en la Pi | Autorizada |
| **E3. Documentación del slice** | Arquitectura, protocolo, UX de las tres superficies, contenido mínimo, estrategia de pruebas y matriz de aceptación | **G3:** autorización de código | Pendiente de G2a |
| **E4. Motor, simulador y visor** | `engine`, `protocol` y `content` con pruebas; simulador con bots; visor de desarrollo | AC del motor en verde e informe del simulador que fija la variante y los parámetros | — |
| **E5. Vertical slice** | Servidor, cliente con 3 rutas y app Android de consola; sesiones con personas | Sesión de aceptación con 4 personas en la Pi 5, sin WAN | — |
| **E6. MVP** | Cinco modos, tratados, las 5 casillas, victorias y exilio | Partidas completas con 3 a 6 jugadores | — |
| **E7. Publicación** | Licencias, guía de instalación, CI y paquetes +18 separados | Instalación limpia en la Pi siguiendo solo la guía | — |

## Línea de arte y audio (D-04)

Avanza en paralelo y se engancha a la línea principal por los documentos de UX: **ningún activo definitivo se produce sin que un documento de UX lo pida.**

| Etapa | Qué produce | Depende de | Criterio de salida |
|---|---|---|---|
| **A0. Dirección** | Exploración de tres direcciones visuales y dos sonoras en `exploracion/`; marcos de estilo del tablero, una carta y un emblema; paleta, tipografías y paleta sonora | G0 y los accesos a las herramientas | `art-direction.md` y `audio-direction.md` en `APROBADO`. **En curso** |
| **A1. Kit del slice** | Mapa vectorial de países (D-06), dados virtuales y su animación, emblemas y colores de jugador, iconos de casilla, la carta de espionaje, efectos básicos y música del lobby y de la partida | A0 y los documentos de UX de E3 | Activos en `assets/` con manifiesto; legibilidad a 2 m (AC-UX-02) comprobada en la pantalla real |
| **A2. Kit del MVP** | Ilustraciones de los cinco mazos por modo, música por fase narrativa, voces del narrador en español (D-30) y animaciones de eventos | A1 y las specs de E6 | Catálogo completo con estado editorial `aprobado` |
| **A3. Publicación** | Icono y recursos de la app Android, licencias de activos y paquetes +18 separados | A2 y E7 | Manifiesto completo y licencias verificadas |

## Siguiente paso

1. E2: spikes S1 (móviles y app Android en la red local), S3 (router sin WAN) y S4 (SQLite durable) en ramas `spike/*`, para cerrar G2a.
2. A0 y A1: mapa estilizado retocado a mano en vectorial y recorrido de casillas alrededor del mapa.
3. E3, tras G2a: arquitectura, protocolo, UX de las tres superficies y matriz de aceptación, para cerrar G3.
