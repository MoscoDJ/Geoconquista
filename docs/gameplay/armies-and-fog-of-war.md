# Ejércitos y niebla de guerra

| Campo | Valor |
|---|---|
| ID | FS-005 |
| Estado | `PROPUESTO` (reglas v0, E1) |
| Fecha | 2026-11-06 |
| Fuentes | Plan de arranque H-05, H-06 y §6.3; R-04 y R-05; observación 4 de la revisión del 2026-11-04 (movimiento) |
| Aprobación | Pendiente del creador, en G1 |

## 1. Tropas y milicia

- Una **tropa real** es una unidad militar secreta que pertenece a un jugador y está en uno de sus países.
- Todo país **sin tropas reales** tiene una **milicia** pública que defiende con D = 1. La milicia no es una tropa: no se mueve, no ataca, no paga mantenimiento y no se retira.
- No hay reservas fuera del mapa: toda tropa está siempre en un país.

## 2. Reclutar (acción estratégica)

- Solo puede reclutar quien posee los 3 países de un **bloque completo** (R-04).
- Por cada bloque completo, como máximo `reclutamiento_max_por_bloque` = 2 tropas nuevas por turno, pagando `coste_tropa` cada una.
- Las tropas nuevas se colocan **directamente** en países propios de ese bloque, repartidas como quiera el jugador.
- Si después se pierde un país del bloque, ya no se recluta con ese bloque. Las tropas ya desplegadas se quedan.

## 3. Mover (acción estratégica)

Esto resuelve la observación 4 de la revisión del 2026-11-04.

- El jugador traslada cualquier cantidad de tropas reales **de un país propio a un país propio vecino** (vecindades de `territories-and-blocks.md` §3).
- Es un solo traslado por turno: un origen y un destino.
- Si el origen se queda sin tropas, vuelve a defenderse con la milicia.

## 4. Niebla de guerra

- **Cifras exactas:** solo el dueño ve cuántas tropas tiene en cada país.
- **Lo que ven los demás y la consola:** la **banda de amenaza** de cada país:

  | Banda | Tropas reales |
  |---|---|
  | Milicia | 0 |
  | Baja | 1–2 |
  | Media | 3–4 |
  | Alta | 5 o más |

- **Espionaje:** la carta «Filtración» revela la cifra exacta de un país rival **solo al espía**, hasta el inicio de su siguiente turno. El público ve quién espió y qué país, pero no la cifra.

## 5. Revelaciones

| Evento | Qué ven el público y la consola | Qué ve el dueño |
|---|---|---|
| Reclutar, mover o desmovilizar | Solo el cambio de banda, si lo hay. Nunca la cifra ni el coste | Sus tropas exactas y su saldo |
| Espionaje | Quién espió y qué país | El espía: la cifra exacta de ese país, durante el tiempo indicado |

La inferencia que permite un cambio de banda es intencional: avisa a la mesa de que algo se mueve (pilar 2 de la visión).

## 6. Criterios de aceptación

- **AC-005.1:** un jugador sin ningún bloque completo no puede reclutar.
- **AC-005.2:** con 2 bloques completos, el máximo por turno es 4 tropas, y cada una va a un país del bloque que la generó.
- **AC-005.3:** mover tropas a un país que no es vecino, o que no es propio, se rechaza.
- **AC-005.4:** un país que pasa de 2 a 3 tropas cambia de banda «baja» a «media» en las vistas ajenas; uno que pasa de 3 a 4, no cambia nada en las vistas ajenas.
- **AC-005.5:** ninguna vista pública, de consola ni de otro jugador contiene la cifra exacta de tropas de un país, salvo la del espía durante el espionaje.
- **AC-005.6:** al terminar el espionaje, la vista del espía vuelve a mostrar solo la banda.

## 7. Preguntas para el creador

1. ¿Te parece bien que «mover» sea un solo traslado entre países vecinos por turno?
