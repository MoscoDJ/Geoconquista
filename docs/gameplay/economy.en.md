# Economy

> This is the English translation of [economy.md](economy.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| ID | FS-004 |
| Status | **`APROBADO`** (approved) by the creator, 2026-11-06 (G1). Provisional for the slice: the figures are tuned with the simulator without new approval; changing a rule requires updating this document and approving it again |
| Date | 2026-11-06 |
| Sources | Startup plan H-03, H-04, §4.3 and §6.3 (disclosure matrix); D-07; D-24 (mortgage and sale instead of the bank completing payments) |
| Approval | Creator, 2026-11-06 (G1, D-25) |

## 1. Treasury

- Each player's treasury (their cash) is **private** (D-07): only its owner sees it.
- Each player's countries, their blocs and their base territorial income are **public**.
- The treasury is never negative. There is no debt.
- **The bank never puts in money to cover a player's payment** (D-24). A player who cannot pay mortgages or sells (§5); if that is still not enough, they go bankrupt (§6).

## 2. Income and upkeep (turn phase 1)

At the start of their turn, each player collects:

> `ingreso_base` + `ingreso_por_pais` × (own countries **without a mortgage**) − upkeep

- **Upkeep:** `mantenimiento_por_tropa` for each real troop from the third one on (`tropas_sin_mantenimiento` = 2).
- **If there is not enough for upkeep:** the player pays until their cash is at 0, and the troops not covered are disbanded, because there is nothing to pay them with. The bank does not step in. They are demobilized one at a time, always from the own country that has the most troops at that moment; on a tie, the one with the lowest country code in alphabetical order.
- **What is published:** the base territorial income (`ingreso_base` + `ingreso_por_pais` × countries without a mortgage). Upkeep and the breakdown are seen only by the owner. A forced demobilization is only noticeable if it changes a threat band.

## 3. Purchase (phase 4)

- On landing on a **free country**, the player can buy it by paying its price (`parameters.md` §2). There is no auction: if they do not buy it, it stays free.
- The purchased country takes on the player's color and has only the militia (`armies-and-fog-of-war.md` §1).

## 4. Tariff (phase 4)

- On landing on **another player's country without a mortgage**, the player pays that country's tariff to its owner. The owner can waive it from their phone, at no cost. The fact that they waived it is public.
- A **mortgaged** country does not collect a tariff.
- **If their cash is not enough:** before paying, the player must raise the money by mortgaging or selling (§5). If even that is not enough, they go bankrupt (§6).
- The creditor always receives exactly what the debtor pays. That way the creditor cannot deduce the debtor's balance, except in a bankruptcy.

## 5. Mortgaging and selling to pay

### 5.1 Mortgage

- The player can **mortgage** an own country to the bank and receives its mortgage value (`parameters.md` §2: half the price, rounded up).
- They can do it **whenever they want during their phase 5**, or **when they have to pay** something their cash does not cover. Because a player can also mortgage just because they want to, a mortgage does not prove that the player had no money.
- **A mortgaged country** still belongs to its owner: it counts for complete blocs, for victory and for the country count, and it keeps its troops. But:
  - it gives no per-country income (§2) and collects no tariff (§4);
  - while a bloc has any mortgaged country, that bloc **does not allow recruiting** (`armies-and-fog-of-war.md` §2).
- **Paying off the mortgage:** in their phase 5, the owner pays the bank the mortgage value plus 10% (`parameters.md` §2). Mortgaging and paying off mortgages do not use up the strategic action.
- If a mortgaged country changes owner (through trade or conquest), **the mortgage passes to the new owner**.
- The mortgage is public: the country is shown as mortgaged.

### 5.2 Emergency sale

- When they have to pay and do not have enough, the player can also **sell** a country to another player, at any moment during the payment and even if it is not their phase 5.
- It follows the trade rules (§7): both accept the same terms, the country is handed over without troops (the seller can demobilize them) and the last country cannot be sold.
- It does not count toward the limit of one deal per turn.

## 6. Bankruptcy

A player goes bankrupt when they have to pay another player and, after mortgaging everything they can and with no sale accepted, their cash is not enough.

- They pay the creditor **all their cash**.
- **All their countries pass to the creditor**, with their mortgages. Their troops are disbanded, so the countries reach the creditor with the militia.
- The part of the debt that is not covered is lost. **The bank does not make it up.**
- Left without countries, the player loses their government and asks for asylum or is eliminated (`victory-and-endgame.md` §3).
- **Disclosures:** the bankruptcy is public. The creditor knows how much cash they received, that is, the debtor's exact balance at that moment. This is accepted, because the debtor leaves the map.

## 7. Bilateral trade (phase 5)

In their phase 5, the player whose turn it is can carry out **one** deal with another player: a purchase, sale or exchange of countries, with or without money.

- Only countries **without real troops** and with no pending combat are handed over. The owner can demobilize their troops in the same deal, without a refund.
- No deal can leave a signatory without countries.
- Both signatories accept the same terms on their phone. Everything is validated before anything is applied; if something fails, nothing changes, not even the troops that were going to be demobilized.
- The error message is generic and does not reveal whether the balance fell short.
- Every transferred country is locked from new trade for one full round of turns ($t+P$, plan §6.2).
- **Disclosures:** the public sees the countries that change hands and that there was a deal. The money is seen only by the signatories (`partes_tratado`).
- A player without countries (a refugee, `victory-and-endgame.md` §3) **can** buy a country through trade: the “do not leave anyone without countries” limit protects the seller.

## 8. Acceptance criteria

- **AC-004.1:** a player with 3 countries, 4 troops and 7 in cash collects 10 + 15 − 4 = 21 at the start of their turn and ends with 28.
- **AC-004.2:** a player with 0 in cash, 2 countries and 14 troops (8 in `BRA`, 6 in `ARG`) collects 20 and owes 24 in upkeep. They pay 20, are left at 0 and demobilize the 2 troops not covered. Both come out of `BRA`, the country with the most troops at each moment, which is left with 6.
- **AC-004.3 (mortgage to pay):** a player with 4 in cash and `BRA` (price 20) lands on a country with a tariff of 10. They mortgage `BRA` and receive 10, pay the tariff and are left with 4. The owner receives 10. The public sees that `BRA` is now mortgaged.
- **AC-004.4:** a deal that would hand over a country with troops, without authorizing their demobilization, is rejected without changing anything.
- **AC-004.5:** a deal that would leave the seller without countries is rejected.
- **AC-004.6:** a country bought through trade in global turn $t$ with 4 players cannot be traded again before turn $t+4$.
- **AC-004.7:** no view other than the owner's contains their exact cash.
- **AC-004.8 (mortgaged country):** landing on a mortgaged country does not collect a tariff; the owner of a mortgaged country does not receive its per-country income.
- **AC-004.9 (recruiting):** a player with a complete bloc, one of whose countries is mortgaged, cannot recruit with that bloc until they pay off the mortgage.
- **AC-004.10 (paying off a mortgage):** paying off the mortgage on a country with a price of 30 costs 17 (15 + 10%, rounded up).
- **AC-004.11 (bankruptcy):** a player with 2 in cash and a single country, already mortgaged and with 3 troops, owes a tariff of 10 and nobody buys anything from them. They pay 2 to the creditor; their country passes to the creditor, mortgaged and with the militia; they lose their government and go on to ask for asylum.
- **AC-004.12 (no money from the bank):** in any payment between players, what the creditor receives equals what the debtor pays.

## 9. Questions for the creator

1. ~~Does the bank complete the tariff?~~ No (D-24): the player mortgages or sells, and if that is not enough, they go bankrupt (§5 and §6). The design of the mortgage, emergency sale and bankruptcy was approved with G1 (D-25).
2. ~~Does waiving a tariff have a cost?~~ No, it is free (D-24).
