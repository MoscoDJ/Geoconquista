# Victory, end of the game and political asylum

> This is the English translation of [victory-and-endgame.md](victory-and-endgame.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| ID | FS-007 |
| Status | **`APROBADO`** (approved) by the creator, 2026-11-06 (G1). Provisional for the slice: the figures are tuned with the simulator without new approval; changing a rule requires updating this document and approving it again |
| Date | 2026-11-06 |
| Sources | Startup plan H-09 and H-10 (replaced); D-09 and D-14 (political asylum); observation 2 of the consolidator |
| Approval | Creator, 2026-11-06 (G1, D-25) |

## 1. Victory by domination

- The winner is whoever, at the close of a round, owns **K = 3 complete blocs** (`parameters.md` §1) and still owns them at the close of the following round.
- The waiting round gives the others one last chance to react.
- If two players meet the condition at the same time, the victory is shared.

## 2. End by round limit

- The game ends at the close of round `rondas_limite`: 12 with 3–4 players and 10 with 5–6.
- The winner is whoever owns **the most countries**; mortgaged ones count. Tie: most complete blocs. If the tie persists, shared victory.

Victory by **submission** (vassalage over all the others) depends on treaties and is specified in E6 (`diplomacy.md`).

## 3. Political asylum (D-09, D-14)

It replaces the plan's “government in exile” (H-10A and H-10B).

### 3.1 When it is requested

A player who **loses their last country** (through combat, bankruptcy or any effect) loses their government and must ask for asylum immediately. The game pauses until it is resolved.

Starting the game without countries does not count: it only triggers when the last country is lost after having had at least one.

### 3.2 Requirement: having leverage to offer

- To ask for asylum, a player must have at least `cartas_minimas_para_asilo` = 1 card in their hand (`core-loop.md` §4). **Only kept cards count**; cash does not (D-22).
- A player who has no cards **is eliminated** directly.

### 3.3 How it is requested

1. The player chooses another player and offers them one or more of their cards. Only the two of them see the offer (`partes_tratado`).
2. That player accepts or rejects on their phone.
3. If they reject, the requester can ask another player. Each player can receive at most one request.
4. **If nobody accepts, the requester is eliminated** (D-14).

### 3.4 On acceptance

- The offered cards pass to the protector's hand.
- The protector chooses in which of their countries the refugee lives. The board shows the refugee's icon on that country.
- The fact that there was asylum, and who is sheltering whom, is published; the cards handed over are not.
- **The protector cannot expel the refugee** (D-22). The asylum only ends when the refugee regains a country or when the refuge falls (§3.6).

### 3.5 The refugee's life

- **They keep their turn.** They collect the `ingreso_base` (with no per-country income, because they have none) and pay no upkeep, because they have no troops.
- They roll dice, move forward, resolve spaces (purchase, tariff, cards) and can trade.
- **They have no strategic action**, because they have neither countries nor troops.
- **They return to the map** as soon as they get a country: by buying it when they land on a free one, or through trade (`economy.md` §7). At that moment the asylum ends.

### 3.6 If the refuge falls

- If the protector loses the country where the refugee lives, the refugee moves to another of the protector's countries.
- If the protector is left without countries, they must ask for asylum themselves, and their refugee must also look for a new protector under the rules of §3.3, or is eliminated.

### 3.7 Elimination

- The eliminated player no longer has a turn. Their cash returns to the bank and their cards go to the discard pile.
- They can stay on as a spectator.
- An early elimination leaves a person without playing for the rest of the game. This is measured in the E5 and E6 sessions (CE-08).

## 4. Acceptance criteria

- **AC-007.1:** a player with 3 complete blocs at the close of round 6 who keeps them at the close of round 7 wins at the close of round 7. If they lose one during round 7, the game continues.
- **AC-007.2:** with 4 players, the game ends at the close of round 12, and whoever has the most countries wins.
- **AC-007.3:** a player who loses their last country with no cards is eliminated without an asylum request.
- **AC-007.4:** a player with 1 card who loses their last country, and who is rejected by all the other players, is eliminated.
- **AC-007.5:** if the protector accepts, the offered card passes to their hand, and the refugee keeps their turn without a strategic action.
- **AC-007.6:** a refugee who buys a free country stops being a refugee and regains the strategic action from their next turn.
- **AC-007.7:** a player who starts with 0 countries and has not yet bought any is not a refugee and cannot be eliminated.
- **AC-007.8:** the public view shows who is sheltering whom, never which cards were handed over.
- **AC-007.9:** no command allows the protector to end an asylum.

## 5. Questions for the creator

1. ~~What counts as “leverage”?~~ Only kept cards (D-22).
2. ~~Can the protector expel the refugee?~~ No (D-22).
3. ~~Can the refugee win?~~ Only if they return to the map (D-24).
