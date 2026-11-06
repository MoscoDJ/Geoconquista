# Victoria, fin de partida y asilo político

| Campo | Valor |
|---|---|
| ID | FS-007 |
| Estado | `PROPUESTO` (reglas v0, E1) |
| Fecha | 2026-11-06 |
| Fuentes | Plan de arranque H-09 y H-10 (sustituido); D-09 y D-14 (asilo político); observación 2 del consolidador |
| Aprobación | Pendiente del creador, en G1 |

## 1. Victoria por dominio

- Gana quien, al cierre de una ronda, posee **K = 3 bloques completos** (`parameters.md` §1) y los sigue poseyendo al cierre de la ronda siguiente.
- La ronda de espera da a los demás una última oportunidad de reaccionar.
- Si dos jugadores cumplen la condición a la vez, la victoria es compartida.

## 2. Fin por límite de rondas

- La partida termina al cerrar la ronda `rondas_limite`: 12 con 3–4 jugadores y 10 con 5–6.
- Gana quien posea **más países**. Empate: más bloques completos. Si persiste, victoria compartida.

La victoria por **sumisión** (vasallaje sobre todos los demás) depende de los tratados y se especifica en E6 (`diplomacy.md`).

## 3. Asilo político (D-09, D-14)

Sustituye al «gobierno en el exilio» del plan (H-10A y H-10B).

### 3.1 Cuándo se pide

Un jugador que **pierde su último país** (por combate o por cualquier efecto) pierde su gobierno y debe pedir asilo inmediatamente. La partida se pausa hasta resolverlo.

Empezar la partida sin países no cuenta: solo se activa al perder el último país después de haber tenido alguno.

### 3.2 Requisito: tener poder que ofrecer

- Para pedir asilo hay que tener al menos `cartas_minimas_para_asilo` = 1 carta en la mano (`core-loop.md` §4). **Solo cuentan las cartas guardadas**; el efectivo no (D-22).
- Quien no tiene ninguna carta **queda eliminado** directamente.

### 3.3 Cómo se pide

1. El jugador elige a otro jugador y le ofrece una o más de sus cartas. La oferta solo la ven los dos (`partes_tratado`).
2. Ese jugador acepta o rechaza en su móvil.
3. Si rechaza, el solicitante puede pedírselo a otro jugador. Cada jugador puede recibir como máximo una solicitud.
4. **Si nadie acepta, el solicitante queda eliminado** (D-14).

### 3.4 Al aceptar

- Las cartas ofrecidas pasan a la mano del anfitrión.
- El anfitrión elige en cuál de sus países vive el asilado. El tablero muestra el icono del asilado sobre ese país.
- Se publica que hubo asilo y quién acoge a quién; las cartas entregadas, no.
- **El anfitrión no puede expulsar al asilado** (D-22). El asilo solo termina cuando el asilado recupera un país o cuando el refugio cae (§3.6).

### 3.5 La vida del asilado

- **Conserva su turno.** Cobra el `ingreso_base` (sin ingreso por países, porque no tiene) y no paga mantenimiento, porque no tiene tropas.
- Lanza dados, avanza, resuelve casillas (compra, arancel, cartas) y puede comerciar.
- **No tiene acción estratégica**, porque no tiene países ni tropas.
- **Vuelve al mapa** en cuanto consigue un país: comprándolo al caer en uno libre o por comercio (`economy.md` §5). En ese momento el asilo termina.

### 3.6 Si el refugio cae

- Si el anfitrión pierde el país donde vive el asilado, el asilado se traslada a otro país del anfitrión.
- Si el anfitrión se queda sin países, él mismo debe pedir asilo, y su asilado también debe buscar un nuevo anfitrión con las reglas de §3.3, o queda eliminado.

### 3.7 Eliminación

- El jugador eliminado deja de tener turno. Su efectivo vuelve al banco y sus cartas van al descarte.
- Puede quedarse como espectador.
- Una eliminación temprana deja a una persona sin jugar el resto de la partida. Se mide en las sesiones de E5 y E6 (CE-08).

## 4. Criterios de aceptación

- **AC-007.1:** un jugador con 3 bloques completos al cierre de la ronda 6 que los conserva al cierre de la ronda 7 gana al cerrar la ronda 7. Si pierde uno durante la ronda 7, la partida sigue.
- **AC-007.2:** con 4 jugadores, la partida termina al cerrar la ronda 12, y gana quien tiene más países.
- **AC-007.3:** un jugador que pierde su último país sin cartas queda eliminado sin solicitud de asilo.
- **AC-007.4:** un jugador con 1 carta que pierde su último país, y al que rechazan todos los demás jugadores, queda eliminado.
- **AC-007.5:** si el anfitrión acepta, la carta ofrecida pasa a su mano, y el asilado conserva su turno sin acción estratégica.
- **AC-007.6:** un asilado que compra un país libre deja de estar asilado y recupera la acción estratégica desde su siguiente turno.
- **AC-007.7:** un jugador que empieza con 0 países y todavía no ha comprado ninguno no está asilado ni puede ser eliminado.
- **AC-007.8:** la vista pública muestra quién acoge a quién, nunca qué cartas se entregaron.
- **AC-007.9:** ningún comando permite al anfitrión terminar un asilo.

## 5. Preguntas para el creador

1. ~~¿Qué cuenta como «poder»?~~ Solo las cartas guardadas (D-22).
2. ~~¿El anfitrión puede expulsar al asilado?~~ No (D-22).
3. ¿El asilado puede ganar la partida? Con estas reglas, solo si vuelve al mapa.
