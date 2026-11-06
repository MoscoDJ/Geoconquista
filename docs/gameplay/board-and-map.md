# Tablero y recorrido

| Campo | Valor |
|---|---|
| ID | FS-002 |
| Estado | `PROPUESTO` (reglas v0, E1) |
| Fecha | 2026-11-06 |
| Fuentes | Plan de arranque DEC-02 y H-01; D-12, D-15, D-16, D-19; `territories-and-blocks.md` (FS-003) |
| Aprobación | Pendiente del creador, en G1 |

El tablero público tiene dos partes: el **mapa** (países, bloques, propietarios y amenaza; ver FS-003) y el **recorrido**, un anillo de casillas por el que avanzan las fichas de los jugadores. Caer en un país del recorrido permite comprarlo; caer en una casilla especial roba de su mazo. Una sola ficha por jugador, en el recorrido; en el mapa no hay fichas, solo colores y símbolos.

## 1. Variante A: una casilla por país (base)

32 casillas: la Salida, los 24 países y 7 casillas especiales. Cada bloque ocupa tres casillas seguidas y va seguido de una casilla especial, de modo que completar un bloque comprando es posible pero exige suerte o comercio.

| Casillas | Contenido |
|---|---|
| 0 | Salida |
| 1–3 | Latinoamérica: México, Brasil, Argentina |
| 4 | Correo |
| 5–7 | África: Nigeria, Sudáfrica, Egipto |
| 8 | Verdad o Reto |
| 9–11 | Asia del Sur: Indonesia, India, Irán |
| 12 | Hacienda |
| 13–15 | Medio Oriente: Arabia Saudita, Israel, Turquía |
| 16 | Migración |
| 17–19 | Europa occidental: España, Francia, Reino Unido |
| 20 | Correo |
| 21–23 | Europa oriental: Polonia, Alemania, Rusia |
| 24 | Mensajería |
| 25–27 | Asia oriental: Corea del Sur, Corea del Norte, China |
| 28 | Verdad o Reto |
| 29–31 | Pacífico Norte: Taiwán, Japón, Estados Unidos |

- Los precios suben a lo largo del recorrido, de 20 a 40 (`parameters.md` §2).
- Con dos dados la media es 7 casillas, así que una vuelta lleva unos 4–5 turnos.
- Pasar por la Salida **no** da dinero: el ingreso se cobra al inicio de cada turno (`economy.md` §2).

## 2. Variante B: una casilla por bloque (a comparar en el simulador)

16 casillas: la Salida, 8 casillas de bloque y 7 especiales, alternadas en el mismo orden que la variante A.

- Al caer en una casilla de bloque, el jugador **elige** un país libre de ese bloque y puede comprarlo.
- Si el bloque no tiene países libres, paga el arancel de un país de ese bloque al jugador que más países tenga en él; en empate, al primero en el orden de asiento a partir del jugador que cayó.
- Da más control al jugador y menos azar. El simulador compara A y B con el parámetro `variante_recorrido`.

## 3. Casillas especiales

| Casilla | Qué hace en las reglas v0 | Estado |
|---|---|---|
| Salida | Nada. Es el punto de partida | Definida |
| Correo | Roba una carta del mazo de Correo y la guarda en la mano (`core-loop.md` §4). En el slice el mazo tiene una sola carta: «Filtración» (espionaje) | Definida para el slice |
| Hacienda, Migración, Mensajería, Verdad o Reto | **Sin efecto en el slice.** Sus mazos y efectos se especifican en E6 (`content/card-catalog-and-governance.md`, `truth-or-dare.md`) | Pendiente de E6 |

## 4. Movimiento en el recorrido

- El jugador en turno lanza **dos dados** deslizando el dedo en su móvil (D-13). El host genera el resultado (`core-loop.md` §3) y la ficha avanza la suma en el sentido de las casillas.
- Los dobles no tienen efecto especial en v0.
- Varias fichas pueden ocupar la misma casilla.

## 5. Presentación en el tablero público

- El recorrido rodea el mapa por el borde del marco de latón (D-19). Cada casilla de país muestra el color del dueño o el tono neutro si está libre; las especiales, su icono de mazo.
- El diseño exacto (tamaños, iconos y animaciones) se fija en `ux/public-display.md` (E3).

## 6. Criterios de aceptación

- **AC-002.1:** con la variante A, el recorrido tiene 32 casillas y cada uno de los 24 países aparece exactamente una vez.
- **AC-002.2:** una ficha en la casilla 30 que avanza 5 termina en la casilla 3.
- **AC-002.3:** pasar por la Salida no modifica la tesorería.
- **AC-002.4:** con la variante B, caer en un bloque sin países libres cobra el arancel al jugador con más países del bloque; con empate entre dos, cobra el primero en el orden de asiento a partir del jugador que cayó.
- **AC-002.5:** caer en Hacienda, Migración, Mensajería o Verdad o Reto en el slice no cambia el estado de la partida, salvo la posición de la ficha.

## 7. Preguntas para el creador

1. ¿Te parece bien el orden del recorrido, con los precios subiendo de Latinoamérica (20) a Pacífico Norte (40)?
2. ¿Los dobles deberían hacer algo (repetir turno, por ejemplo)? Recomendación: nada en v0, para no alargar los turnos.
