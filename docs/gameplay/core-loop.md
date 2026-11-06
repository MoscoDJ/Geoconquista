# Bucle de juego

| Campo | Valor |
|---|---|
| ID | FS-001 |
| Estado | **`APROBADO`** por el creador, 2026-11-06 (G1). Provisional para el slice: las cifras se ajustan con el simulador sin nueva aprobación; cambiar una regla exige actualizar este documento y aprobarlo otra vez |
| Fecha | 2026-11-06 |
| Fuentes | Plan de arranque H-02, DEC-06 y §6.2.1; D-08, D-13; observaciones de la revisión del 2026-11-04 (4 y 5) |
| Aprobación | Creador, 2026-11-06 (G1, D-25) |

## 1. Preparación

1. Se unen entre 3 y 6 jugadores (`parameters.md` §1). Cada uno elige nombre y color.
2. El host sortea el **orden de asiento** con su generador aleatorio con semilla. El orden se publica.
3. Cada jugador recibe la `tesoreria_inicial` (privada) y empieza con 0 países y 0 tropas (`paises_iniciales_por_jugador` = 0).
4. Todas las fichas empiezan en la Salida.

## 2. Ronda y turno

Una **ronda** es un turno de cada jugador, en el orden de asiento. Cada turno tiene seis fases, siempre en este orden:

| Fase | Qué pasa | Detalle |
|---|---|---|
| 1. Ingreso | El jugador cobra su ingreso y paga el mantenimiento | `economy.md` §2 |
| 2. Dados | Lanza dos dados deslizando el dedo en su móvil | §3 |
| 3. Movimiento | Su ficha avanza en el recorrido | `board-and-map.md` §4 |
| 4. Casilla | Se resuelve la casilla: comprar, pagar arancel o robar carta | `economy.md` §3–§4, `board-and-map.md` §3 |
| 5. Acciones | Opcionales: **un** acuerdo comercial, **una** carta, hipotecar o levantar hipotecas, y **una** acción estratégica (reclutar, mover o atacar) | `economy.md` §5 y §7, §4, `armies-and-fog-of-war.md` §2, `combat.md` |
| 6. Cierre | El jugador termina su turno | — |

- La negociación verbal es libre en cualquier momento, pero solo tiene efecto cuando se formaliza en la fase 5 de quien está en turno.
- No hay temporizador por defecto.
- Al ser una sola acción estratégica por turno, nunca se recluta y ataca en el mismo turno. Eso da a los vecinos al menos un turno de aviso cuando sube una banda de amenaza.

## 3. Dados virtuales

- **Quién lanza:** en el movimiento, el jugador en turno; en un combate, el atacante y el defensor, cada uno desde su móvil (`combat.md` §3).
- **Cómo:** deslizando el dedo hacia arriba en el móvil (D-13). No se usa el sensor de movimiento.
- **Quién decide el resultado:** el host, con su generador aleatorio con semilla. El gesto solo dispara la tirada; su fuerza no cambia el resultado. La animación de los dados en la tablet termina en el valor ya decidido, y el tablero lo repite.
- **Resultado público:** los valores de los dados son públicos y quedan en el registro de la partida.
- **Si alguien no lanza:** la consola puede lanzar en su nombre (D-22). Queda en el registro público como «lanzado desde la consola». Así una persona distraída o sin batería no bloquea la mesa.

## 4. Cartas

- Las cartas robadas en una casilla especial se **guardan en la mano**, que es privada (`propietario`). El tablero muestra cuántas cartas tiene cada jugador, no cuáles.
- Máximo `max_cartas_en_mano` = 3. Si roba una cuarta, elige una para descartar.
- Se juega como máximo **una carta por turno**, en la fase 5 del propio turno. Jugarla **no** consume la acción estratégica.
- Las cartas guardadas son el «poder» que permite pedir asilo (`victory-and-endgame.md` §3).

## 5. La consola

La consola (tablet) muestra la partida y la caída de los dados, resuelve las casillas según estas reglas y permite pausar. No ve tropas, saldos ni cartas de nadie, y no tiene comandos arbitrarios del tipo «dar dinero» (DEC-06).

## 6. Criterios de aceptación

- **AC-001.1:** con la misma semilla y la misma secuencia de comandos, la partida da exactamente el mismo resultado, dados incluidos.
- **AC-001.2:** un jugador que intenta reclutar y atacar en el mismo turno recibe un rechazo en la segunda acción.
- **AC-001.3:** un comando de lanzar dados fuera de turno, o de un jugador que no participa en el combate, se rechaza en el servidor.
- **AC-001.4:** un jugador con 3 cartas que roba una cuarta termina con 3 cartas, después de elegir cuál descarta.
- **AC-001.5:** jugar una carta en la fase 5 no impide hacer después la acción estratégica del mismo turno.
- **AC-001.6:** la vista pública y la de la consola muestran el número de cartas de cada jugador y nunca su contenido.

## 7. Preguntas para el creador

1. ~~¿La consola puede lanzar por un jugador que no lo hace?~~ Sí (D-22).
2. ~~¿Tres cartas en la mano y una por turno?~~ Sí (D-24).
