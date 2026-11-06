# Parámetros de las reglas v0

| Campo | Valor |
|---|---|
| ID | FS-008 |
| Estado | **`APROBADO`** por el creador, 2026-11-06 (G1). Provisional para el slice: las cifras se ajustan con el simulador sin nueva aprobación; cambiar una regla exige actualizar este documento y aprobarlo otra vez |
| Versión de la ficha | `v0.1` (2026-11-06) |
| Fuentes | Plan de arranque §6.2 (ficha de parámetros inicial) y H-01 a H-12; D-07, D-09, D-12 a D-15 |
| Aprobación | Creador, 2026-11-06 (G1, D-25) |

Todas las cifras del juego viven aquí y en los datos de contenido, **nunca en el código** (`AGENTS.md` §6). Ninguna está validada: son el punto de partida del simulador (E4) y de las sesiones con personas (E5). Cambiar una cifra no cambia una regla, así que no exige volver a G1; sí exige subir la versión de esta ficha y registrarlo en el acta de la sesión.

## 1. Partida

| Parámetro | Valor | Dónde se usa |
|---|---|---|
| `jugadores_min` / `jugadores_max` | 3 / 6 | `core-loop.md` §1 |
| `variante_recorrido` | `A` (una casilla por país); alternativa `B` (una casilla por bloque) | `board-and-map.md` |
| `paises_iniciales_por_jugador` | 0 (alternativa a medir: 2 de bloques distintos) | `core-loop.md` §1 |
| `tesoreria_inicial` | 100 | `economy.md` §1 |
| `rondas_limite` | 12 con 3–4 jugadores; 10 con 5–6 | `victory-and-endgame.md` §2 |
| `bloques_para_dominio` (K) | 3 | `victory-and-endgame.md` §1 |

## 2. Economía

| Parámetro | Valor | Dónde se usa |
|---|---|---|
| `ingreso_base` | 10 por turno | `economy.md` §2 |
| `ingreso_por_pais` | 5 por país propio y turno | `economy.md` §2 |
| Precio por bloque | Latinoamérica 20 · África 20 · Asia del Sur 25 · Medio Oriente 25 · Europa occidental 30 · Europa oriental 30 · Asia oriental 35 · Pacífico Norte 40 | `economy.md` §3 |
| Arancel según precio | 20 → 5 · 25 → 6 · 30 → 8 · 35 → 9 · 40 → 10 | `economy.md` §4 |
| `enfriamiento_comercial` | Una vuelta completa de turnos ($t+P$) | `economy.md` §7 |
| `acuerdos_por_turno` | 1 (las ventas de emergencia no cuentan) | `economy.md` §7 y §5.2 |
| Valor de hipoteca según precio | 20 → 10 · 25 → 13 · 30 → 15 · 35 → 18 · 40 → 20 (la mitad, redondeando hacia arriba) | `economy.md` §5.1 |
| Coste de levantar la hipoteca | 20 → 11 · 25 → 15 · 30 → 17 · 35 → 20 · 40 → 22 (hipoteca + 10 %, redondeando hacia arriba) | `economy.md` §5.1 |

## 3. Ejércitos y combate

| Parámetro | Valor | Dónde se usa |
|---|---|---|
| `coste_tropa` | 10 | `armies-and-fog-of-war.md` §2 |
| `reclutamiento_max_por_bloque` | 2 tropas por bloque completo y turno | `armies-and-fog-of-war.md` §2 |
| `tropas_sin_mantenimiento` | 2 (las 2 primeras tropas de cada jugador no pagan) | `economy.md` §2 |
| `mantenimiento_por_tropa` | 2 por tropa a partir de la 3.ª, por turno | `economy.md` §2 |
| `milicia` | D = 1, pública, no se mueve ni paga | `armies-and-fog-of-war.md` §1 |
| Bandas de amenaza | milicia (0) · baja (1–2) · media (3–4) · alta (5+) | `armies-and-fog-of-war.md` §3 |
| `bonus_defensa` | +1 | `combat.md` §3 |
| `bajas_max` | 2 por bando y combate | `combat.md` §4 |
| `margen_bajas_extra_atacante` | 3 (si Defensa − Ataque ≥ 3, el atacante pierde hasta 2) | `combat.md` §4 |

## 4. Cartas y casillas

| Parámetro | Valor | Dónde se usa |
|---|---|---|
| `max_cartas_en_mano` | 3 | `core-loop.md` §4 |
| `cartas_jugadas_por_turno` | 1 | `core-loop.md` §4 |
| `duracion_espionaje` | Hasta el inicio del siguiente turno del espía | `armies-and-fog-of-war.md` §4 |
| `penalizacion_pasar_verdad_reto` | 10 (sin deuda: se cobra hasta dejar el saldo en 0) | E6, `truth-or-dare.md` |

## 5. Asilo

| Parámetro | Valor | Dónde se usa |
|---|---|---|
| `cartas_minimas_para_asilo` | 1 | `victory-and-endgame.md` §3 |

## 6. Cómo se usan en el simulador

- El simulador cambia **un parámetro cada vez** y deja el resto igual (plan §6.2).
- Primera tanda prevista: `variante_recorrido` A frente a B; `paises_iniciales_por_jugador` 0 frente a 2; `tesoreria_inicial` 80, 100 y 120.
- Señales que obligan a revisar cifras: ningún bloque completo antes de la ronda 5 (RK-02); una vía de victoria por encima del 60 %; ventaja del primer asiento; partidas que no llegan a la fase militar.
