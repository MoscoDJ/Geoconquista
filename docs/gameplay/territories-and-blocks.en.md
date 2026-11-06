# Countries and blocs

> This is the English translation of [territories-and-blocks.md](territories-and-blocks.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| ID | FS-003 |
| Status | **`APROBADO`** (approved) by the creator, 2026-11-06 (G1). Provisional for the slice: the figures are tuned with the simulator without a new approval; changing a rule requires updating this document and approving it again |
| Date | 2026-11-06 |
| Sources | R-04 (blocs of 3); D-06 (real, present-day countries); D-12 (24 countries in 8 blocs); D-15 (change to the list); D-16 (stylized map); startup plan DEC-10 and H-03 |
| Approval | Creator, 2026-11-06 (G1, D-25) |

## 1. Map rules

- **24 playable countries in 8 blocs of 3** (D-12). Each country belongs to a single bloc.
- The **rest of the world** is drawn in gray and is not playable: it cannot be bought or occupied and has no troops.
- **Identifiers:** the Natural Earth country code (`ADM0_A3`), which matches ISO 3166-1 alpha-3 for the 24 countries (`MEX`, `TWN`…). These are the stable IDs of the engine and of the content data.
- **Geometry:** Natural Earth, *Admin 0 – Countries* layer at 1:50m scale (public domain), with its default borders. France is shown with its European territory only. The West Bank and Gaza are drawn separately, in gray (D-15).
- **Stylized map (D-16):** continuous magnifying lenses are applied to enlarge the small playable countries without breaking the borders. Europe and the Middle East share one wide lens; East Asia has another; Israel and Taiwan each get two stacked lenses, because they need about 5 times magnification. The automatic version is the base; the final one is retouched by hand in vector form (A1).
- **No real flags** (`assets/art-direction.md` §7).
- The list, the blocs and the adjacencies are **content data**, not code constants (`AGENTS.md` §6). The draft is in `exploracion/mapa/territorios-v0.json` and will move to the content data after G3.

## 2. The 24 countries

| Bloc | Countries |
|---|---|
| Latin America | Mexico (`MEX`), Brazil (`BRA`), Argentina (`ARG`) |
| North Pacific | United States (`USA`), Japan (`JPN`), Taiwan (`TWN`) |
| Western Europe | United Kingdom (`GBR`), France (`FRA`), Spain (`ESP`) |
| Eastern Europe | Germany (`DEU`), Poland (`POL`), Russia (`RUS`) |
| East Asia | China (`CHN`), North Korea (`PRK`), South Korea (`KOR`) |
| Middle East | Turkey (`TUR`), Israel (`ISR`), Saudi Arabia (`SAU`) |
| Africa | Egypt (`EGY`), Nigeria (`NGA`), South Africa (`ZAF`) |
| South Asia | Iran (`IRN`), India (`IND`), Indonesia (`IDN`) |

**Allocation criteria:** after removing Canada, Colombia and Australia and adding North Korea, Taiwan and Israel (D-15), only four countries were left in the Americas, which do not form blocs of 3. That is why the United States moves to a Pacific bloc with Japan and Taiwan, and Mexico, Brazil and Argentina form Latin America. Each bloc is connected (section 3), so that completing it makes military sense as well as economic sense.

**Left out** and drawn in gray, among others: Canada, Colombia, Australia, Italy and Ukraine.

**Sensitivity:** the list includes countries in active conflicts or with disputed sovereignty (Russia, Israel, Taiwan, North Korea, Iran). This is the creator's decision (D-06, D-15). It is recorded for the editorial review of the modes, especially `familiar_u18` (P-12), and for the narrator and card texts: countries are named, never peoples, religions or real leaders.

## 3. Adjacencies

Two countries are neighbors if there is an adjacency between them. Adjacency decides which countries can be attacked and which countries troops can move to. There are three types:

- **Land:** a real border.
- **Sea:** a sea route.
- **Corridor:** joins two playable countries through non-playable countries.

The three types **are only distinguished visually** and have the same effect in the rules (D-24).

### Within each bloc

| Bloc | Adjacencies |
|---|---|
| Latin America | `MEX`–`BRA` corridor (through Central America and Colombia) · `BRA`–`ARG` land (border) |
| North Pacific | `USA`–`JPN` sea (Pacific Ocean) · `JPN`–`TWN` sea (Ryukyu Islands) |
| Western Europe | `GBR`–`FRA` sea (English Channel) · `FRA`–`ESP` land (border) |
| Eastern Europe | `DEU`–`POL` land (border) · `POL`–`RUS` land (border (Kaliningrad)) |
| East Asia | `CHN`–`PRK` land (border) · `PRK`–`KOR` land (border (demilitarized zone)) · `CHN`–`KOR` sea (Yellow Sea) |
| Middle East | `TUR`–`ISR` sea (Eastern Mediterranean) · `ISR`–`SAU` corridor (through Jordan) · `TUR`–`SAU` corridor (through Syria and Iraq) |
| Africa | `EGY`–`NGA` corridor (through the Sahel) · `NGA`–`ZAF` corridor (through Central Africa) |
| South Asia | `IRN`–`IND` corridor (through Pakistan) · `IND`–`IDN` sea (Indian Ocean) |

### Between blocs

| Adjacency | Type | Via |
|---|---|---|
| `USA`–`MEX` | Land | border |
| `USA`–`GBR` | Sea | North Atlantic |
| `USA`–`RUS` | Sea | Bering Strait |
| `BRA`–`NGA` | Sea | South Atlantic |
| `ARG`–`ZAF` | Sea | South Atlantic |
| `FRA`–`DEU` | Land | border |
| `GBR`–`DEU` | Sea | North Sea |
| `ESP`–`EGY` | Sea | Mediterranean |
| `DEU`–`TUR` | Corridor | through the Balkans |
| `RUS`–`TUR` | Sea | Black Sea |
| `RUS`–`IRN` | Sea | Caspian Sea |
| `RUS`–`CHN` | Land | border |
| `RUS`–`PRK` | Land | border |
| `EGY`–`ISR` | Land | border (Sinai) |
| `SAU`–`EGY` | Sea | Red Sea |
| `SAU`–`IRN` | Sea | Persian Gulf |
| `TUR`–`IRN` | Land | border |
| `CHN`–`IND` | Land | border |
| `CHN`–`TWN` | Sea | Taiwan Strait |
| `KOR`–`JPN` | Sea | Korea Strait |
| `CHN`–`IDN` | Sea | South China Sea |
| `IDN`–`ZAF` | Sea | Indian Ocean |

In total there are 40 adjacencies, and the graph is connected: from any country you can reach any other. Neighbors per country:

- **6:** China, Russia.
- **5:** Turkey.
- **4:** Germany, Saudi Arabia, Egypt, United States, Iran.
- **3:** Brazil, North Korea, South Korea, France, India, Indonesia, Israel, Japan, Nigeria, United Kingdom, South Africa.
- **2:** Argentina, Spain, Mexico, Poland, Taiwan.

With 2 neighbors a country is easy to defend; with 6, hard. The E4 simulator will measure whether this causes an imbalance.

## 4. What this document does not set

- **Prices, income and tariffs** for each country: they go in `parameters.md`.
- **Position of the countries on the track** and special spaces: they go in `board-and-map.md`, with the plan's variants A and B (DEC-10 / §6.2).
- **Military movement:** still open (plan §8.3). This document only defines who is a neighbor of whom.

## 5. Questions for the creator

1. ~~Do you approve the allocation into blocs?~~ Approved (D-20).
2. ~~Do the adjacency types change the rules?~~ No, only the drawing (D-24).
