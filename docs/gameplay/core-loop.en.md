# Game loop

> This is the English translation of [core-loop.md](core-loop.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| ID | FS-001 |
| Status | **`APROBADO`** (approved) by the creator, 2026-11-06 (G1). Provisional for the slice: the figures are tuned with the simulator without a new approval; changing a rule requires updating this document and approving it again |
| Date | 2026-11-06 |
| Sources | Startup plan H-02, DEC-06 and §6.2.1; D-08, D-13; notes from the 2026-11-04 review (4 and 5) |
| Approval | Creator, 2026-11-06 (G1, D-25) |

## 1. Setup

1. Between 3 and 6 players join (`parameters.md` §1). Each one picks a name and a color.
2. The host draws the **seating order** with its seeded random generator. The order is made public.
3. Each player receives the `tesoreria_inicial` (private) and starts with 0 countries and 0 troops (`paises_iniciales_por_jugador` = 0).
4. All tokens start on Start.

## 2. Round and turn

A **round** is one turn for each player, in seating order. Each turn has six phases, always in this order:

| Phase | What happens | Detail |
|---|---|---|
| 1. Income | The player collects their income and pays upkeep | `economy.md` §2 |
| 2. Dice | They roll two dice by swiping on their phone | §3 |
| 3. Movement | Their token moves forward on the track | `board-and-map.md` §4 |
| 4. Space | The space is resolved: buy, pay the tariff or draw a card | `economy.md` §3–§4, `board-and-map.md` §3 |
| 5. Actions | Optional: **one** trade agreement, **one** card, mortgage or pay off mortgages, and **one** strategic action (recruit, move or attack) | `economy.md` §5 and §7, §4, `armies-and-fog-of-war.md` §2, `combat.md` |
| 6. End | The player ends their turn | — |

- Verbal negotiation is free at any time, but it only takes effect when it is formalized in phase 5 of the player whose turn it is.
- There is no timer by default.
- Since there is only one strategic action per turn, no one ever recruits and attacks in the same turn. This gives neighbors at least one turn of warning when a threat band goes up.

## 3. Virtual dice

- **Who rolls:** in movement, the player whose turn it is; in combat, the attacker and the defender, each from their own phone (`combat.md` §3).
- **How:** by swiping up on the phone (D-13). The motion sensor is not used.
- **Who decides the result:** the host, with its seeded random generator. The gesture only triggers the roll; its strength does not change the result. The dice animation on the tablet ends on the value already decided, and the board repeats it.
- **Public result:** dice values are public and are kept in the game log.
- **If someone does not roll:** the console can roll on their behalf (D-22). It is recorded in the public log as “rolled from the console”. This way a distracted person, or one whose battery has died, does not hold up the table.

## 4. Cards

- Cards drawn on a special space are **kept in the hand**, which is private (`propietario`). The board shows how many cards each player has, not which ones.
- Maximum `max_cartas_en_mano` = 3. If a player draws a fourth, they choose one to discard.
- At most **one card per turn** is played, in phase 5 of the player's own turn. Playing it does **not** use up the strategic action.
- Kept cards are the “leverage” that lets a player request asylum (`victory-and-endgame.md` §3).

## 5. The console

The console (tablet) shows the game and the dice falling, resolves spaces according to these rules and allows pausing. It does not see anyone's troops, balances or cards, and it has no arbitrary commands of the “give money” kind (DEC-06).

## 6. Acceptance criteria

- **AC-001.1:** with the same seed and the same sequence of commands, the game produces exactly the same result, dice included.
- **AC-001.2:** a player who tries to recruit and attack in the same turn gets a rejection on the second action.
- **AC-001.3:** a roll-dice command out of turn, or from a player who is not taking part in the combat, is rejected on the server.
- **AC-001.4:** a player with 3 cards who draws a fourth ends up with 3 cards, after choosing which one to discard.
- **AC-001.5:** playing a card in phase 5 does not prevent taking the strategic action of the same turn afterwards.
- **AC-001.6:** the public view and the console view show the number of cards each player has and never their content.

## 7. Questions for the creator

1. ~~Can the console roll for a player who does not?~~ Yes (D-22).
2. ~~Three cards in hand and one per turn?~~ Yes (D-24).
