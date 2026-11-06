# Geoconquista documentation

> This is the English translation of [README.md](README.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

The approved documentation is the contract between design, implementation and testing. **If it is not documented and approved, it is not implemented.** The rules for agents are in [`AGENTS.md`](../AGENTS.en.md) and their rationale is in [ADR-000](decisions/ADR-000-gobernanza.en.md).

## Gate status

| Gate | What it authorizes | Status |
|---|---|---|
| G0 | Kickoff: governance, vision, spikes and art and audio exploration | **`APROBADO`** (approved) by the creator, 2026-11-05 |
| G1 | v0 rules approved (E1) | **`APROBADO`** by the creator, 2026-11-06 |
| G2a | Stack, local network and persistence validated on a laptop (ADR-001) | Not started |
| G2b | Raspberry Pi 5 hardware validated (ADR-002) | Not started |
| G3 | **Product code** (`apps/`, `packages/`, `tools/`) | Not started |

Stages and exit criteria: [roadmap/milestones.md](roadmap/milestones.en.md).

## Creator decision log

| ID | Date | Decision |
|---|---|---|
| D-01 | 2026-11-04 | There is no paper prototype. The v0 rules are written and approved; pacing and balance are measured with the simulator; fun is measured in sessions with people on the digital slice. |
| D-02 | 2026-11-04 | Players join by QR from the browser, without installing anything. The tablet uses a native app. |
| D-03 | 2026-11-05 | The console tablet is **Android** as the main platform. The creator also has an iPad and Google and Apple developer accounts; the iPad remains a secondary platform. |
| D-04 | 2026-11-05 | The graphics and sound kit (illustrations, icons, map, music, effects and voices) is generated and edited by the agent with generative tools (OpenAI, Google AI Studio, Replicate, Magnific, ElevenLabs) and local tools. The creator provides access and approves the results. The goal is production quality. |
| D-05 | 2026-11-05 | The creator works in **Visual Studio Code**, not in Cursor. The rules for agents are `AGENTS.md`, `CLAUDE.md` and the skill in `.claude/`; no Cursor configuration is maintained. |
| D-06 | 2026-11-05 | **P-02:** the map uses **real, present-day countries**, in blocs of 3 (R-04). How many are playable and how the rest of the world and disputed territories are handled is left to P-15. |
| D-07 | 2026-11-05 | **P-08:** each player's treasury is **private**. Countries, blocs and base territorial income are public (plan §4.3). |
| D-08 | 2026-11-05 | **P-11:** the dice are not physical. The player throws virtual dice that land on the tablet. Replaces R-03 and makes DEC-11 obsolete. **Refined by D-13.** |
| D-09 | 2026-11-05 | **P-13:** whoever loses their last country can **request political asylum** in a country held by another player, as long as they keep some power (wildcards or *counters*) that is useful to whoever takes them in. Replaces H-10A and H-10B as the baseline. **Refined by D-14.** |
| D-10 | 2026-11-05 | `Contexto/` stays **local only**: it is not published in the repository. |
| D-11 | 2026-11-06 | **Art direction A, cinematic war room, for the whole game.** B and C are discarded, also for the party decks. |
| D-12 | 2026-11-06 | **P-15:** **24 playable countries in 8 blocs of 3.** The other P-15 recommendations are accepted: the rest of the world in gray and not playable, no disputed territory playable, Natural Earth borders and no real flags. The concrete list is a proposal in `gameplay/territories-and-blocks.md`. **Modified by D-15.** |
| D-13 | 2026-11-06 | **P-16:** the dice are thrown **only by swiping** on the phone; there is no shaking. Reason: the game is open source and must not require anyone to have a domain or certificates. Everything stays HTTP on the local network, and spike S5 is dropped. |
| D-14 | 2026-11-06 | **P-17:** if **nobody takes in** the player who requests asylum, **they are eliminated** from the game. |
| D-15 | 2026-11-06 | **Change to the country list:** Canada, Colombia and Australia are out; **North Korea, Taiwan and Israel** are in. For these three, this replaces the D-12 rule that no disputed territory is playable. The West Bank and Gaza remain in gray, not playable. The blocs are redone in `gameplay/territories-and-blocks.md`. |
| D-16 | 2026-11-06 | **Stylized map:** small playable countries are enlarged so they are not lost at 2 m (option b of the scale question). |
| D-17 | 2026-11-06 | **Narrator:** the voice “El Faraón – Powerful and Mysterious” from the ElevenLabs library, for all the narrator's lines. |
| D-18 | 2026-11-06 | **Music:** a **hybrid** electronic-orchestral direction. |
| D-19 | 2026-11-06 | **Board and cards:** the board composition (generated war-table background + vector map with flat player colors) and the “The Leak” card format (full-page illustration with a frame, deck badge and text on top) are approved. Both are the style reference. |
| D-20 | 2026-11-06 | The **list of 24 countries and their split into 8 blocs** in `gameplay/territories-and-blocks.md` is approved. |
| D-21 | 2026-11-06 | **Sound effects (A0 exploration):** the dice, purchase, complete bloc and Mail card effects are accepted. The attack declaration and conquest effects must be redone. |
| D-22 | 2026-11-06 | **v0 rules:** to request asylum only **held cards** count, not cash; the protector **cannot expel** the refugee; free countries **can only be bought**, not attacked; the **console can throw the dice** for a player who does not, with a public log entry. |
| D-23 | 2026-11-06 | **Redone effects:** **variant 3** of the attack declaration (radar ping, pulse and taiko hit) and **variant 3** of conquest (“braam” with a final stamp hit) are chosen. |
| D-24 | 2026-11-06 | **Closing the v0 rules questions:** “move” is one transfer per turn between neighbors; the track and its prices stay as they are; doubles do nothing; retreat is automatic in v0; at most 3 cards in hand and 1 per turn; waiving a tariff is free; adjacency types only change the drawing; the refugee only wins if they return to the map; **secret objectives are out of the MVP** for now. **The bank never puts up a player's money:** whoever cannot pay must mortgage or sell, and if that is still not enough, they go bankrupt (`gameplay/economy.md` §5 and §6). |
| D-25 | 2026-11-06 | **G1 approved:** the v0 rules (FS-001 to FS-008), including the design of mortgage, emergency sale and bankruptcy, are approved as provisional for the slice. |
| D-26 | 2026-11-06 | **Licenses (P-10):** code AGPL-3.0-or-later; content CC BY-SA 4.0; name and logo reserved; contributions with DCO, no CLA; Contributor Covenant code of conduct. Voices may have a more restrictive license. See ADR-003. |
| D-27 | 2026-11-06 | **Audio under a restrictive license:** voices, effects and music generated with ElevenLabs carry the Geoconquista audio license (`LICENSES/LicenseRef-Geoconquista-Audio.md`): they are only redistributed as part of the game or of a derivative. |
| D-28 | 2026-11-06 | **Bilingual game, Spanish and English:** interface, cards, dares, names and narrator. Localization rules in `product/localization.md`. **Refined by D-30.** |
| D-29 | 2026-11-06 | **Bilingual documentation:** **Spanish is the canonical version** (it is written and approved in Spanish; if they differ, Spanish prevails). Each document has its English translation in a sibling file `<name>.en.md`, updated in the same change. Everything is translated except the startup plan, which remains as a historical file in Spanish, and `Contexto/`. |
| D-30 | 2026-11-06 | **The game is native Spanish.** The project produces **all texts in Spanish and English** (interface, cards, dares and names). **Voices and images with text** are produced only in Spanish; the English versions are contributed by the community. The documentation remains bilingual (D-29). |

### Virtual dice: technical note (D-08 and D-13, `PROPUESTO` until G1)

- **The result is generated by the host,** with a seeded random generator whose seed is logged. The swipe gesture only **triggers** the throw: its strength does not change the result, and the tablet animation ends on the value already decided. This satisfies the invariant “the host is the only authority” (`AGENTS.md` §6), and a game can be replayed.
- **Who throws:** in combat, attacker and defender from their own phones; in movement, the player whose turn it is.
- **Where it is seen:** the dice land on the tablet and the board repeats the result with a short animation. This last point is still a proposal; the creator has not confirmed it.

### Political asylum: proposal (D-09 and D-14, `PROPUESTO` until G1)

“Held cards” do not exist yet: today each card is applied when drawn (H-08). Asylum needs some cards that are kept in hand.

- Asylum is requested from a specific player and is a **treaty** that the engine enforces (H-11). The protector can **accept or reject it**.
- **The refugee** keeps their turn and the exile subsidy, and lives in one of the protector's countries. From there they can re-enter by buying a free country or with the civil re-entry of H-10B.
- **The protector**, on accepting, receives the held cards that were agreed. Breaking the asylum counts as breaking a treaty.
- **If nobody takes them in, they are eliminated** (D-14). Proposal: whoever has no power to offer cannot request asylum, so they are also eliminated. An early elimination leaves a person watching the rest of the game. This is measured in the E5 and E6 sessions (CE-08).

The recommendations that are not yet decisions (DEC-01 to DEC-12) are in the [startup plan](roadmap/plan-de-arranque.md) §5.

## Document states

`PROPUESTO` → `APROBADO` (with approver and date) → `OBSOLETO`.

**Languages (D-29):** each document is in Spanish, which is the canonical version, and has its English translation next to it, `<name>.en.md`. If they differ, Spanish prevails. The startup plan is only in Spanish. `PENDIENTE` marks something waiting for an answer from the creator. Only the creator approves.

## Index

Legend: ✅ exists · ⏳ planned for the stage shown.

### Governance and product
- ✅ [decisions/ADR-000-gobernanza.md](decisions/ADR-000-gobernanza.en.md): documentation and agent rules. `APROBADO`
- ✅ [decisions/ADR-003-licencias.md](decisions/ADR-003-licencias.en.md): licenses and contributions. `APROBADO` (D-26, D-27)
- ✅ [product/localization.md](product/localization.en.md) (FS-009): game languages. `PROPUESTO`
- ✅ [product/vision.md](product/vision.en.md): vision, pillars, requirements and limits. `APROBADO`
- ✅ [roadmap/milestones.md](roadmap/milestones.en.md): stages, gates and status. `APROBADO`
- ✅ [roadmap/plan-de-arranque.md](roadmap/plan-de-arranque.md): consolidated plan from the debate, with the revisions of 2026-11-04 and 2026-11-05. Reference, not a spec; the D-## decisions prevail over it.

### Gameplay (E1, v0 rules)
- ✅ [gameplay/core-loop.md](gameplay/core-loop.en.md) (FS-001): setup, turn, virtual dice and cards. `APROBADO` (G1)
- ✅ [gameplay/board-and-map.md](gameplay/board-and-map.en.md) (FS-002): track, variants A and B, spaces. `APROBADO` (G1)
- ✅ [gameplay/territories-and-blocks.md](gameplay/territories-and-blocks.en.md) (FS-003): 24 countries, 8 blocs and adjacencies. `APROBADO` (D-20, G1)
- ✅ [gameplay/economy.md](gameplay/economy.en.md) (FS-004): treasury, income, purchase, tariff and trade. `APROBADO` (G1)
- ✅ [gameplay/armies-and-fog-of-war.md](gameplay/armies-and-fog-of-war.en.md) (FS-005): troops, recruit, move, bands and espionage. `APROBADO` (G1)
- ✅ [gameplay/combat.md](gameplay/combat.en.md) (FS-006): attack, roll, casualties and retreat. `APROBADO` (G1)
- ✅ [gameplay/victory-and-endgame.md](gameplay/victory-and-endgame.en.md) (FS-007): domination, round limit and political asylum. `APROBADO` (G1)
- ✅ [gameplay/parameters.md](gameplay/parameters.en.md) (FS-008): all the figures. `APROBADO` (G1)
- ⏳ `gameplay/diplomacy.md`, `game-modes.md` and `truth-or-dare.md` (E3/E6)

### Architecture (E2/E3)
- ⏳ `decisions/ADR-001-stack-y-clientes.md` and `ADR-002-pantalla-publica.md` (with evidence from the spikes)
- ⏳ `architecture/system-context.md`, `authority-and-privacy.md`, `protocol.md`, `persistence.md`, `offline-lan.md` and `deployment.md`

### UX (E3)
- ⏳ `ux/public-display.md`, `admin-tablet.md`, `player-mobile.md` and `lobby.md`

### Content (E3/E6)
- ⏳ `content/card-catalog-and-governance.md`

### Art and audio (line A, in parallel)
- ✅ [assets/art-direction.md](assets/art-direction.en.md): art direction. `PROPUESTO`
- ✅ [assets/audio-direction.md](assets/audio-direction.en.md): audio direction. `PROPUESTO`
- ✅ [assets/pipeline.md](assets/pipeline.en.md): tools, workflow, manifest and licenses. `PROPUESTO`

### Testing (E3)
- ⏳ `testing/test-strategy.md`, `acceptance-matrix.md` and `playtest-plan.md`

### Templates
- ✅ [templates/feature-spec.md](templates/feature-spec.en.md), [templates/adr.md](templates/adr.en.md), [templates/card.md](templates/card.en.md), [templates/asset-brief.md](templates/asset-brief.en.md) and [templates/session-report.md](templates/session-report.en.md)

## Source material

`Contexto/` contains the creator's brief, the debate transcript, the inherited governance and the concept screenshots. It is reference material: **nothing in it is implemented without first moving into an approved document in `docs/`.** `Contexto/` stays local only and is ignored by git (D-10).
