# Combate

| Campo | Valor |
|---|---|
| ID | FS-006 |
| Estado | **`APROBADO`** por el creador, 2026-11-06 (G1). Provisional para el slice: las cifras se ajustan con el simulador sin nueva aprobación; cambiar una regla exige actualizar este documento y aprobarlo otra vez |
| Fecha | 2026-11-06 |
| Fuentes | Plan de arranque H-07 y sus comprobaciones (§6.2); D-08 y D-13 (dados virtuales) |
| Aprobación | Creador, 2026-11-06 (G1, D-25) |

## 1. Declarar un ataque (acción estratégica)

- Se ataca **desde un país propio con al menos una tropa real** hacia un **país de otro jugador** que sea vecino (`territories-and-blocks.md` §3).
- Los **países libres no se atacan**: solo se compran (D-22). Así la economía sigue importando.
- Máximo un ataque por turno, porque es la acción estratégica.
- El atacante compromete en secreto N tropas, entre 1 y las que tenga en el país de origen.
- Antes de lanzar los dados, el atacante puede desistir. Pierde la acción estratégica del turno, pero no tropas.

## 2. Defensa

- El defensor usa su guarnición D: las tropas reales del país atacado o, si no tiene, la milicia (D = 1).
- El defensor no elige nada en v0. La retirada, si la hay, es automática (§4).

## 3. Tirada

- El atacante y el defensor lanzan **un dado cada uno**, deslizando el dedo en su móvil (D-13). Si el defensor tiene milicia, también lanza él. El host genera los valores (`core-loop.md` §3).
- **Ataque** = N + dado del atacante.
- **Defensa** = D + dado del defensor + 1.
- El empate lo gana el defensor.

| Diferencia N − D | Probabilidad de que gane el atacante |
|---|---|
| 0 | 10/36 (27,8 %) |
| +1 | 15/36 (41,7 %) |
| +2 | 21/36 (58,3 %) |
| +3 | 26/36 (72,2 %) |
| +4 | 30/36 (83,3 %) |

## 4. Resultado

**Si gana el atacante:**
- El atacante pierde 1 tropa solo si D ≥ N y N ≥ 2. En otro caso, ninguna.
- El defensor pierde hasta 2 tropas reales.
- Si al defensor le quedan tropas, **se retiran** al país propio vecino con menor código de país en orden alfabético. Si no tiene ningún país propio vecino (está **cercado**), las pierde todas.
- El atacante **ocupa** el país con sus supervivientes. El país cambia de dueño. El origen se queda con las tropas que no se comprometieron, o con la milicia.
- Si era el último país del defensor, este pierde su gobierno y puede pedir asilo (`victory-and-endgame.md` §3).

**Si gana el defensor:**
- El atacante pierde 1 tropa, o hasta 2 si Defensa − Ataque ≥ 3. Nunca más de N. Los supervivientes vuelven al origen.
- El defensor pierde 1 tropa solo si N ≥ D y D ≥ 2.

## 5. Revelaciones

- **Público y consola:** países de origen y destino, los dos dados, quién ganó, el país de retirada (si la hubo) y las nuevas bandas de amenaza. **Nunca** N, D ni las bajas exactas.
- **Cada bando:** sus propias bajas y sus tropas restantes.
- **Inferencias aceptadas:** con los dados públicos, saber quién ganó acota la diferencia N − D. Una retirada revela que D ≥ 3; su ausencia tras perder sin estar cercado revela que D ≤ 2. Son parte del diseño (plan §6.3).

## 6. Criterios de aceptación

Cada caso fija estado inicial, dados y resultado esperado. El simulador y las pruebas del motor (E4) los ejecutan tal cual.

- **AC-006.1 (milicia):** N = 1 contra milicia. Dados 6 y 1: Ataque 7 > Defensa 3. Gana el atacante, sin bajas, y ocupa con 1 tropa.
- **AC-006.2 (fortaleza):** N = 1 contra D = 5. Para las 36 combinaciones de dados gana el defensor; el atacante pierde su tropa y el defensor ninguna.
- **AC-006.3 (retirada):** N = 4 contra D = 3, con el defensor dueño de un país vecino. Dados 5 y 2: Ataque 9 > Defensa 6. El atacante no pierde nada; el defensor pierde 2 y su tropa superviviente se retira; el atacante ocupa con 4.
- **AC-006.4 (cerco):** el mismo caso, sin países propios vecinos del defensor. El defensor pierde las 3 tropas.
- **AC-006.5 (varias salidas):** el defensor tiene dos países vecinos propios, `DEU` y `FRA`. La retirada va a `DEU`.
- **AC-006.6 (derrota amplia):** N = 2 contra D = 4. Dados 1 y 6: Ataque 3, Defensa 11, diferencia 8. El atacante pierde 2 (todas las comprometidas). El defensor no pierde ninguna, porque N < D.
- **AC-006.7 (conservación):** en cualquier combate, tropas finales = tropas iniciales − bajas. Ninguna tropa se duplica al ocupar o al retirarse.
- **AC-006.8 (país libre):** declarar un ataque contra un país sin dueño se rechaza.
- **AC-006.9 (privacidad):** tras cualquier combate, ninguna vista ajena contiene N, D ni las bajas exactas.

## 7. Preguntas para el creador

1. ~~¿Los países libres se pueden atacar?~~ No, solo se compran (D-22).
2. ~~¿Retirada automática?~~ Sí en v0 (D-24). Si en las sesiones resulta artificial, se cambia por que el defensor elija el destino.
