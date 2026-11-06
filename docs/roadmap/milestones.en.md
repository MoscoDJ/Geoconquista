# Milestones and gates

> This is the English translation of [milestones.md](milestones.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| Status | `APROBADO` (approved) by the creator, 2026-11-05 (G0). The country map was added later, with D-06 and D-12 |
| Date | 2026-11-05 |
| Source | Startup plan §6.1 and §7, with D-01 to D-10 |

There are no dates, because no justified estimates exist. Each stage ends at a **gate** with exit criteria. The full detail (deliverables, dependencies and resources) is in the [startup plan](plan-de-arranque.md) §7.

## Main line

```text
E0 ──┬─► E1: v0 rules / G1 ──────────────────┐
     ├─► E2: S1, S3, S4 / G2a (laptop) ─────┴─► E3 / G3 ─► E4 ─► E5 (development + sessions) ─┐
     └─► E2: S2, S4 on Pi / G2b ───────────────────────────────────────────────────────────┴─► E5 close ─► E6 ─► E7
```

| Stage | What it produces | Exit gate | Status |
|---|---|---|---|
| **E0. Governance and vision** | ADR-000, `AGENTS.md`, skill, `docs/README.md`, `vision.md` and this document | **G0:** the creator approves ADR-000 and the vision; the spikes and the art and audio exploration are authorized | **Completed:** G0 approved on 2026-11-05 |
| **E1. v0 rules** | Gameplay documents for the slice, `parameters.md`, the country map (D-06) as data, political asylum (D-09) and the edge-case scenarios as executable cases | **G1:** the creator approves the v0 rules as provisional for the slice | **Completed:** G1 approved on 2026-11-06 (FS-001 to FS-008) |
| **E2. Spikes** | S1 (phones and Android tablet app on the local network), S2 (Pi 5 and kiosk), S3 (router without WAN), S4 (durable SQLite) | **G2a:** ADR-001 with evidence on a laptop. **G2b:** ADR-002 with evidence on the Pi | Authorized |
| **E3. Slice documentation** | Architecture, protocol, UX of the three surfaces, minimum content, test strategy and acceptance matrix | **G3:** code authorization | Pending G2a |
| **E4. Engine, simulator and viewer** | `engine`, `protocol` and `content` with tests; simulator with bots; development viewer | Engine ACs green and a simulator report that sets the variant and the parameters | — |
| **E5. Vertical slice** | Server, client with 3 routes and Android console app; sessions with people | Acceptance session with 4 people on the Pi 5, without WAN | — |
| **E6. MVP** | Five modes, treaties, the 5 spaces, victories and exile | Complete games with 3 to 6 players | — |
| **E7. Release** | Licenses, installation guide, CI and separate +18 packages | Clean installation on the Pi following only the guide | — |

## Art and audio line (D-04)

It advances in parallel and hooks into the main line through the UX documents: **no final asset is produced unless a UX document asks for it.**

| Stage | What it produces | Depends on | Exit criterion |
|---|---|---|---|
| **A0. Direction** | Exploration of three visual directions and two sound directions in `exploracion/`; style frames for the board, a card and an emblem; palette, typefaces and sound palette | G0 and access to the tools | `art-direction.md` and `audio-direction.md` in `APROBADO`. **In progress** |
| **A1. Slice kit** | Vector country map (D-06), virtual dice and their animation, player emblems and colors, space icons, the espionage card, basic effects, and lobby and in-game music | A0 and the E3 UX documents | Assets in `assets/` with a manifest; legibility at 2 m (AC-UX-02) checked on the real screen |
| **A2. MVP kit** | Illustrations for the five decks per mode, music per narrative phase, narrator voices in Spanish (D-30) and event animations | A1 and the E6 specs | Complete catalog with editorial status `aprobado` |
| **A3. Release** | Android app icon and resources, asset licenses and separate +18 packages | A2 and E7 | Complete manifest and verified licenses |

## Next step

1. E2: spikes S1 (phones and Android app on the local network), S3 (router without WAN) and S4 (durable SQLite) in `spike/*` branches, to close G2a.
2. A0 and A1: stylized map hand-retouched in vector, and the track of spaces around the map.
3. E3, after G2a: architecture, protocol, UX of the three surfaces and acceptance matrix, to close G3.
