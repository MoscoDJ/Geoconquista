# Combat

> This is the English translation of [combat.md](combat.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| ID | FS-006 |
| Status | **`APROBADO`** (approved) by the creator, 2026-11-06 (G1). Provisional for the slice: the figures are tuned with the simulator without new approval; changing a rule requires updating this document and approving it again |
| Date | 2026-11-06 |
| Sources | Startup plan H-07 and its checks (§6.2); D-08 and D-13 (virtual dice) |
| Approval | Creator, 2026-11-06 (G1, D-25) |

## 1. Declaring an attack (strategic action)

- An attack is made **from an own country with at least one real troop** against **another player's country** that is a neighbor (`territories-and-blocks.md` §3).
- **Free countries cannot be attacked**: they can only be bought (D-22). That way the economy still matters.
- At most one attack per turn, because it is the strategic action.
- The attacker secretly commits N troops, between 1 and the number they have in the origin country.
- Before rolling the dice, the attacker can back out. They lose the turn's strategic action, but no troops.

## 2. Defense

- The defender uses their garrison D: the real troops in the attacked country or, if there are none, the militia (D = 1).
- The defender chooses nothing in v0. The retreat, if there is one, is automatic (§4).

## 3. Roll

- The attacker and the defender roll **one die each**, with a swipe on their phone (D-13). If the defender has the militia, they still roll. The host generates the values (`core-loop.md` §3).
- **Attack** = N + attacker's die.
- **Defense** = D + defender's die + 1.
- The defender wins ties.

| Difference N − D | Probability that the attacker wins |
|---|---|
| 0 | 10/36 (27.8%) |
| +1 | 15/36 (41.7%) |
| +2 | 21/36 (58.3%) |
| +3 | 26/36 (72.2%) |
| +4 | 30/36 (83.3%) |

## 4. Outcome

**If the attacker wins:**
- The attacker loses 1 troop only if D ≥ N and N ≥ 2. Otherwise, none.
- The defender loses up to 2 real troops.
- If the defender has troops left, they **retreat** to the neighboring own country with the lowest country code in alphabetical order. If the defender has no neighboring own country (they are **encircled**), they lose them all.
- The attacker **occupies** the country with their survivors. The country changes owner. The origin keeps the troops that were not committed, or the militia.
- If it was the defender's last country, the defender loses their government and can ask for asylum (`victory-and-endgame.md` §3).

**If the defender wins:**
- The attacker loses 1 troop, or up to 2 if Defense − Attack ≥ 3. Never more than N. The survivors return to the origin.
- The defender loses 1 troop only if N ≥ D and D ≥ 2.

## 5. Disclosures

- **Public and console:** origin and destination countries, both dice, who won, the retreat country (if there was a retreat) and the new threat bands. **Never** N, D or the exact losses.
- **Each side:** their own losses and their remaining troops.
- **Accepted inferences:** with the dice public, knowing who won narrows down the difference N − D. A retreat reveals that D ≥ 3; its absence after losing without being encircled reveals that D ≤ 2. These are part of the design (plan §6.3).

## 6. Acceptance criteria

Each case sets the initial state, the dice and the expected outcome. The simulator and the engine tests (E4) run them exactly as written.

- **AC-006.1 (militia):** N = 1 against the militia. Dice 6 and 1: Attack 7 > Defense 3. The attacker wins, with no losses, and occupies with 1 troop.
- **AC-006.2 (fortress):** N = 1 against D = 5. For all 36 dice combinations the defender wins; the attacker loses their troop and the defender none.
- **AC-006.3 (retreat):** N = 4 against D = 3, with the defender owning a neighboring country. Dice 5 and 2: Attack 9 > Defense 6. The attacker loses nothing; the defender loses 2 and their surviving troop retreats; the attacker occupies with 4.
- **AC-006.4 (encirclement):** the same case, with no neighboring own countries for the defender. The defender loses all 3 troops.
- **AC-006.5 (several exits):** the defender has two neighboring own countries, `DEU` and `FRA`. The retreat goes to `DEU`.
- **AC-006.6 (heavy defeat):** N = 2 against D = 4. Dice 1 and 6: Attack 3, Defense 11, difference 8. The attacker loses 2 (all those committed). The defender loses none, because N < D.
- **AC-006.7 (conservation):** in any combat, final troops = initial troops − losses. No troop is duplicated when occupying or retreating.
- **AC-006.8 (free country):** declaring an attack against a country with no owner is rejected.
- **AC-006.9 (privacy):** after any combat, no other player's view contains N, D or the exact losses.

## 7. Questions for the creator

1. ~~Can free countries be attacked?~~ No, they can only be bought (D-22).
2. ~~Automatic retreat?~~ Yes in v0 (D-24). If it feels artificial in the sessions, it will be changed so that the defender chooses the destination.
