# Armies and fog of war

> This is the English translation of [armies-and-fog-of-war.md](armies-and-fog-of-war.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| ID | FS-005 |
| Status | **`APROBADO`** (approved) by the creator, 2026-11-06 (G1). Provisional for the slice: the figures are tuned with the simulator without new approval; changing a rule requires updating this document and approving it again |
| Date | 2026-11-06 |
| Sources | Startup plan H-05, H-06 and §6.3; R-04 and R-05; observation 4 of the 2026-11-04 review (movement) |
| Approval | Creator, 2026-11-06 (G1, D-25) |

## 1. Troops and militia

- A **real troop** is a secret military unit that belongs to a player and is in one of their countries.
- Every country **without real troops** has a public **militia** that defends with D = 1. The militia is not a troop: it does not move, does not attack, does not pay upkeep and does not retreat.
- There are no reserves off the map: every troop is always in a country.

## 2. Recruit (strategic action)

- Only a player who owns the 3 countries of a **complete bloc** (R-04), **none of which is mortgaged** (`economy.md` §5.1), can recruit.
- For each complete bloc, at most `reclutamiento_max_por_bloque` = 2 new troops per turn, paying `coste_tropa` for each one.
- The new troops are placed **directly** in own countries of that bloc, distributed however the player wants.
- If a country of the bloc is later lost, the player can no longer recruit with that bloc. Troops already deployed stay.

## 3. Move (strategic action)

This resolves observation 4 of the 2026-11-04 review.

- The player transfers any number of real troops **from an own country to a neighboring own country** (adjacencies in `territories-and-blocks.md` §3).
- It is a single transfer per turn: one origin and one destination.
- If the origin is left without troops, it goes back to being defended by the militia.

## 4. Fog of war

- **Exact figures:** only the owner sees how many troops they have in each country.
- **What the others and the console see:** the **threat band** of each country:

  | Band | Real troops |
  |---|---|
  | Militia | 0 |
  | Low | 1–2 |
  | Medium | 3–4 |
  | High | 5 or more |

- **Espionage:** the “The Leak” card reveals the exact figure of a rival country **only to the spy**, until the start of their next turn. The public sees who spied and which country, but not the figure.

## 5. Disclosures

| Event | What the public and the console see | What the owner sees |
|---|---|---|
| Recruit, move or demobilize | Only the band change, if there is one. Never the figure or the cost | Their exact troops and their balance |
| Espionage | Who spied and which country | The spy: the exact figure of that country, for the stated time |

The inference that a band change allows is intentional: it warns the table that something is moving (pillar 2 of the vision).

## 6. Acceptance criteria

- **AC-005.1:** a player without any complete bloc cannot recruit.
- **AC-005.2:** with 2 complete blocs, the maximum per turn is 4 troops, and each one goes to a country of the bloc that generated it.
- **AC-005.3:** moving troops to a country that is not a neighbor, or that is not one's own, is rejected.
- **AC-005.4:** a country that goes from 2 to 3 troops changes from the “low” to the “medium” band in other players' views; one that goes from 3 to 4 changes nothing in other players' views.
- **AC-005.5:** no public view, console view or other player's view contains the exact troop figure of a country, except the spy's during espionage.
- **AC-005.6:** when espionage ends, the spy's view goes back to showing only the band.

## 7. Questions for the creator

1. ~~Is “Move” a single transfer between neighbors per turn?~~ Yes (D-24).
