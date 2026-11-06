# Board and track

> This is the English translation of [board-and-map.md](board-and-map.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| ID | FS-002 |
| Status | **`APROBADO`** (approved) by the creator, 2026-11-06 (G1). Provisional for the slice: the figures are tuned with the simulator without a new approval; changing a rule requires updating this document and approving it again |
| Date | 2026-11-06 |
| Sources | Startup plan DEC-02 and H-01; D-12, D-15, D-16, D-19; `territories-and-blocks.md` (FS-003) |
| Approval | Creator, 2026-11-06 (G1, D-25) |

The public board has two parts: the **map** (countries, blocs, owners and threat; see FS-003) and the **track**, a ring of spaces along which the players' tokens move. Landing on a country on the track lets you buy it; landing on a special space draws from its deck. One token per player, on the track; there are no tokens on the map, only colors and symbols.

## 1. Variant A: one space per country (base)

32 spaces: Start, the 24 countries and 7 special spaces. Each bloc takes up three consecutive spaces and is followed by a special space, so completing a bloc by buying is possible but takes luck or trade.

| Spaces | Content |
|---|---|
| 0 | Start |
| 1–3 | Latin America: Mexico, Brazil, Argentina |
| 4 | Mail |
| 5–7 | Africa: Nigeria, South Africa, Egypt |
| 8 | Truth or Dare |
| 9–11 | South Asia: Indonesia, India, Iran |
| 12 | Tax Office |
| 13–15 | Middle East: Saudi Arabia, Israel, Turkey |
| 16 | Immigration |
| 17–19 | Western Europe: Spain, France, United Kingdom |
| 20 | Mail |
| 21–23 | Eastern Europe: Poland, Germany, Russia |
| 24 | Messaging |
| 25–27 | East Asia: South Korea, North Korea, China |
| 28 | Truth or Dare |
| 29–31 | North Pacific: Taiwan, Japan, United States |

- Prices rise along the track, from 20 to 40 (`parameters.md` §2).
- With two dice the average is 7 spaces, so one lap takes about 4–5 turns.
- Passing Start does **not** give money: income is collected at the start of each turn (`economy.md` §2).

## 2. Variant B: one space per bloc (to be compared in the simulator)

16 spaces: Start, 8 bloc spaces and 7 special spaces, alternating in the same order as variant A.

- When landing on a bloc space, the player **chooses** a free country in that bloc and may buy it.
- If the bloc has no free countries, they pay the tariff of one country in that bloc to the player who has the most countries in it; in a tie, to the first in seating order starting from the player who landed.
- It gives the player more control and less chance. The simulator compares A and B with the `variante_recorrido` parameter.

## 3. Special spaces

| Space | What it does in the v0 rules | Status |
|---|---|---|
| Start | Nothing. It is the starting point | Defined |
| Mail | Draws a card from the Mail deck and keeps it in the hand (`core-loop.md` §4). In the slice the deck has a single card: “The Leak” (espionage) | Defined for the slice |
| Tax Office, Immigration, Messaging, Truth or Dare | **No effect in the slice.** Their decks and effects are specified in E6 (`content/card-catalog-and-governance.md`, `truth-or-dare.md`) | Pending E6 |

## 4. Movement on the track

- The player whose turn it is rolls **two dice** by swiping on their phone (D-13). The host generates the result (`core-loop.md` §3) and the token moves forward by the sum in the direction of the spaces.
- Doubles have no effect (D-24).
- Several tokens can occupy the same space.

## 5. Presentation on the public board

- The track runs around the map along the edge of the brass frame (D-19). Each country space shows the owner's color, or the neutral tone if it is free; special spaces show their deck icon.
- The exact design (sizes, icons and animations) is set in `ux/public-display.md` (E3).

## 6. Acceptance criteria

- **AC-002.1:** with variant A, the track has 32 spaces and each of the 24 countries appears exactly once.
- **AC-002.2:** a token on space 30 that moves forward 5 ends on space 3.
- **AC-002.3:** passing Start does not change the treasury.
- **AC-002.4:** with variant B, landing on a bloc with no free countries pays the tariff to the player with the most countries in the bloc; with a tie between two, the first in seating order starting from the player who landed collects.
- **AC-002.5:** landing on Tax Office, Immigration, Messaging or Truth or Dare in the slice does not change the game state, except for the token's position.

## 7. Questions for the creator

1. ~~Track order and prices from 20 to 40?~~ Yes (D-24).
2. ~~Do doubles do anything?~~ No (D-24).
