# Art direction

> This is the English translation of [art-direction.md](art-direction.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| Status | `PROPUESTO`. Direction **A** (D-11); board, cards and stylized map decided (D-16, D-19). §9.4 is still open |
| Date | 2026-11-05 |
| Sources | Vision (pillars 1, 2 and 7); brief §9 and §14; screenshots in `Contexto/referencias-visuales/`; plan §4.4 (V-1 to V-13) |

This document sets the **criteria** and the **questions** for the art direction. The concrete choices (chosen direction, final palette and typefaces) are settled after the A0 exploration, with real images in front of us.

## 1. What we take from the screenshots and what we don't

The screenshots are generated concepts, not specifications (brief §14).

**Kept as a starting point:**
- The tone of a dark “situation room”, with a deep blue ocean and gold accents.
- Saturated colors on a dark background.
- The information density of the tablet, organized in panels.
- The feel of a physical object: framed cards, tokens, a board with a border.

**Discarded** (plan §4.4):
- The name “Dominio Global” (V-1).
- The seven continental blocs (V-2). Present-day countries **are** used (D-06), in blocs of 3.
- All players' troops on the tablet (V-4).
- The arbitrary-power buttons (V-5) and the console's “Roll dice” button (V-6): the player rolls the dice from their phone (D-08).
- The WhatsApp logo (V-10).
- The decorative figures (V-11) and the dice keypad (V-12), which no longer exists with D-08.

## 2. Core legibility problem: owner versus bloc

In the screenshots, the map is colored **by continent**. In the game, what matters at a glance is **who owns each country**, and second, which bloc it belongs to and what threat it holds. Proposal to validate in A0 and in `ux/public-display.md`:

| Information | Proposed encoding |
|---|---|
| Owner | **Fill** of the country with the player's color and symbol; free countries in a neutral tone (parchment or slate gray) |
| Bloc | A shared **outline** around the three countries, plus a bloc emblem; when the bloc is complete, the outline lights up in the owner's color |
| Threat band | Icon over the country with 0 to 3 marks (militia, low, medium or high), never a number |
| Token on the track | Pawn in the player's color and symbol |

## 3. Player colors and symbols

Six colors designed for people with color blindness, each with its own **symbol**, because color never stands alone (AC-UX-02). Starting point: the Okabe and Ito palette, which is designed to stay distinguishable for the common types of color blindness. It must be validated on the real dark background and by simulating each type of color blindness.

| Player | Candidate color | Candidate symbol |
|---|---|---|
| 1 | Orange `#E69F00` | Circle |
| 2 | Sky blue `#56B4E9` | Triangle |
| 3 | Bluish green `#009E73` | Square |
| 4 | Yellow `#F0E442` | Star |
| 5 | Vermilion `#D55E00` | Diamond |
| 6 | Reddish purple `#CC79A7` | Hexagon |

So that it works with maps in any art style, the ocean and free land stay outside these six hues.

## 4. Typography

Fonts must have an open license (SIL OFL), be bundled with the application with no external downloads (AC-NET-01) and include every Spanish glyph.

- **Text and figures:** candidate Atkinson Hyperlegible, designed for low-vision readers. This is what matters most at 2 m.
- **Headings:** a condensed face with a military or editorial character. Candidates: Barlow Condensed and Oswald.
- **Logotype:** “GEOCONQUISTA” as custom vector lettering, not as a generated image. AI does not guarantee correct letters, and the logo must be scalable.

## 5. Three directions to explore in A0

All three are tested with **the same three subjects** so they can be compared on equal terms: a fragment of the board (6 Mediterranean countries and 4 track spaces), the “The Leak” card from the Mail deck, and the emblem of a power.

| Direction | Description | For | Against |
|---|---|---|---|
| **A. Cinematic war room** | Realistic and dramatic, in line with the screenshots: map textures, metal, warm light | Immediate impact; it is the reference that already exists | Hard to keep consistent across hundreds of cards; detail is lost at 2 m; heavier on modest devices |
| **B. Geopolitical poster** | Flat illustration with limited inks, screen-print or period-poster style, with strong shapes | Very legible at a distance; high consistency across cards; light files; works for humor as well as for tension | Less “spectacular” in a screenshot |
| **C. Illustrated satire** | Editorial caricature with humor, exaggerated characters and situations | Fits the party modes and Truth or Dare; gives personality | Risk of caricaturing peoples or cultures (brief §6.2); may clash with the tension of war |

**Creator's decision (D-11, 2026-11-06): A for the whole game.** B and C are discarded.

For A to work, its three risks must be contained:
- **Legibility at 2 m.** The background (desk, metal, light) is generated, but the map is drawn on top as vectors, with flat, saturated player fills. The map's relief and texture are kept at low intensity so they don't compete with the ownership colors. Round 2 of A0 tests this.
- **Consistency across hundreds of cards.** A fixed style prompt and a set of approved reference images are defined. For A2, training a custom style on Replicate will be considered.
- **Performance.** Backgrounds and cards in WebP or AVIF, at each screen's resolution. Animated light and particles are measured on the Pi 5 (S2).

## 6. What is generated with AI and what is built

| Piece | Method | Reason |
|---|---|---|
| Map geometry (playable countries and adjacencies, D-06) | **Built** as vectors from Natural Earth (public domain), with magnifiers that enlarge small countries (D-16) and a final manual touch-up | Requires precision and must match the engine's data |
| Interface icons, spaces, threat bands and dice faces | **Built** in SVG | Sharp at any size, consistent and minimal weight |
| Logotype and lettering | **Built** as vectors | Generated letters are not reliable |
| Map, ocean and frame textures | Generated and edited | Visual richness in the background |
| Illustrations for cards, events and lobby backgrounds | Generated and edited | High volume with consistent style |
| Power emblems | Generated as a base and redrawn as vectors | Must read at very small sizes |

## 7. Visual content limits

- No real flags, official coats of arms or faces of real political leaders. Confirmed with D-12: not even with real countries.
- No third-party logos or trademarks (WhatsApp, Monopoly, Risk), and not the style of an identifiable living artist.
- No ethnic, religious or national stereotypes.
- The art for `familiar_u18` is suitable for minors. The visual tone of the 18+ modes depends on P-04 and P-12 and remains `PENDIENTE`.

## 8. Technical budgets (provisional until S1 and S2)

- **Phone:** the art in the player view counts toward the target of ≤ 5 MB of initial transfer (DEC-04). Illustrations load only when they are about to be shown.
- **Board:** it is served locally, so it can take more weight, but it must stay smooth on the Pi 5 (AC-HW-01).
- **Candidate formats:** SVG for vectors; WebP or AVIF for illustrations, with sizes per screen density. Confirmed in S1.

## 9. Questions to close A0

1. ~~Which direction is adopted?~~ A (D-11).
2. ~~Physical object or flat interface?~~ Physical object: a war table with a brass frame; the vector map goes on top (D-19).
3. ~~Full-page illustration or vignette?~~ Full page with the text on top, like “The Leak” (D-19).
4. How much does the art change between `familiar_u18` and the 18+ modes?
