# v0 rules parameters

> This is the English translation of [parameters.md](parameters.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| ID | FS-008 |
| Status | **`APROBADO`** (approved) by the creator, 2026-11-06 (G1). Provisional for the slice: the figures are tuned with the simulator without a new approval; changing a rule requires updating this document and approving it again |
| Sheet version | `v0.1` (2026-11-06) |
| Sources | Startup plan §6.2 (initial parameter sheet) and H-01 to H-12; D-07, D-09, D-12 to D-15 |
| Approval | Creator, 2026-11-06 (G1, D-25) |

All the game's figures live here and in the content data, **never in the code** (`AGENTS.md` §6). None of them is validated: they are the starting point for the simulator (E4) and for the sessions with people (E5). Changing a figure does not change a rule, so it does not require going back to G1; it does require bumping the version of this sheet and recording it in the session report.

## 1. Game

| Parameter | Value | Where it is used |
|---|---|---|
| `jugadores_min` / `jugadores_max` | 3 / 6 | `core-loop.md` §1 |
| `variante_recorrido` | `A` (one space per country); alternative `B` (one space per bloc) | `board-and-map.md` |
| `paises_iniciales_por_jugador` | 0 (alternative to measure: 2 from different blocs) | `core-loop.md` §1 |
| `tesoreria_inicial` | 100 | `economy.md` §1 |
| `rondas_limite` | 12 with 3–4 players; 10 with 5–6 | `victory-and-endgame.md` §2 |
| `bloques_para_dominio` (K) | 3 | `victory-and-endgame.md` §1 |

## 2. Economy

| Parameter | Value | Where it is used |
|---|---|---|
| `ingreso_base` | 10 per turn | `economy.md` §2 |
| `ingreso_por_pais` | 5 per owned country per turn | `economy.md` §2 |
| Price per bloc | Latin America 20 · Africa 20 · South Asia 25 · Middle East 25 · Western Europe 30 · Eastern Europe 30 · East Asia 35 · North Pacific 40 | `economy.md` §3 |
| Tariff by price | 20 → 5 · 25 → 6 · 30 → 8 · 35 → 9 · 40 → 10 | `economy.md` §4 |
| `enfriamiento_comercial` | One full cycle of turns ($t+P$) | `economy.md` §7 |
| `acuerdos_por_turno` | 1 (emergency sales do not count) | `economy.md` §7 and §5.2 |
| Mortgage value by price | 20 → 10 · 25 → 13 · 30 → 15 · 35 → 18 · 40 → 20 (half, rounded up) | `economy.md` §5.1 |
| Cost to pay off the mortgage | 20 → 11 · 25 → 15 · 30 → 17 · 35 → 20 · 40 → 22 (mortgage + 10%, rounded up) | `economy.md` §5.1 |

## 3. Armies and combat

| Parameter | Value | Where it is used |
|---|---|---|
| `coste_tropa` | 10 | `armies-and-fog-of-war.md` §2 |
| `reclutamiento_max_por_bloque` | 2 troops per complete bloc per turn | `armies-and-fog-of-war.md` §2 |
| `tropas_sin_mantenimiento` | 2 (each player's first 2 troops do not pay) | `economy.md` §2 |
| `mantenimiento_por_tropa` | 2 per troop from the 3rd onward, per turn | `economy.md` §2 |
| `milicia` | D = 1, public, does not move or pay | `armies-and-fog-of-war.md` §1 |
| Threat bands | militia (0) · low (1–2) · medium (3–4) · high (5+) | `armies-and-fog-of-war.md` §3 |
| `bonus_defensa` | +1 | `combat.md` §3 |
| `bajas_max` | 2 per side per combat | `combat.md` §4 |
| `margen_bajas_extra_atacante` | 3 (if Defense − Attack ≥ 3, the attacker loses up to 2) | `combat.md` §4 |

## 4. Cards and spaces

| Parameter | Value | Where it is used |
|---|---|---|
| `max_cartas_en_mano` | 3 | `core-loop.md` §4 |
| `cartas_jugadas_por_turno` | 1 | `core-loop.md` §4 |
| `duracion_espionaje` | Until the start of the spy's next turn | `armies-and-fog-of-war.md` §4 |
| `penalizacion_pasar_verdad_reto` | 10 (no debt: it is charged until the balance reaches 0) | E6, `truth-or-dare.md` |

## 5. Asylum

| Parameter | Value | Where it is used |
|---|---|---|
| `cartas_minimas_para_asilo` | 1 | `victory-and-endgame.md` §3 |

## 6. How they are used in the simulator

- The simulator changes **one parameter at a time** and leaves the rest the same (plan §6.2).
- First planned batch: `variante_recorrido` A versus B; `paises_iniciales_por_jugador` 0 versus 2; `tesoreria_inicial` 80, 100 and 120.
- Signals that require reviewing figures: no complete bloc before round 5 (RK-02); a victory path above 60%; a first-seat advantage; games that do not reach the military phase.
