# Game languages

> This is the English translation of [localization.md](localization.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| ID | FS-009 |
| Status | `PROPUESTO` |
| Date | 2026-11-06 |
| Sources | D-28 (bilingual game); D-30 (native Spanish; texts in both languages; English voices and images with text from the community); D-17 (narrator); `AGENTS.md` §6 (texts in structured content) |
| Approval | Pending the creator |

**Geoconquista is a native Spanish game** (D-30). The project produces **all texts in Spanish and English**. **Voices and images with text** are produced only in Spanish; their English versions are contributed by the community.

## 1. Languages

| Language | Role | Who produces it |
|---|---|---|
| `es` (Spanish) | Native and reference language | The project: texts, voices and images |
| `en` (English) | Complete in texts | The project, the texts. The community, the voices and the images with text |

- The language **never** changes the rules, the figures or the state of the game: only how they are presented.
- Other languages can be added if the community contributes them, including their texts.

## 2. When a language is offered

- **Texts:** Spanish and English are always complete, because the project maintains both. Every new text is written in both languages in the same change. A language contributed by the community only appears as an option if its **text pack is complete**: interface, spaces, decks and the cards of the modes being played.
- **Audio and images:** may be missing. Anything without a version in that language uses the Spanish one (§4 and §5).

## 3. Language of each surface

| Surface | Language | Who chooses it |
|---|---|---|
| Public board, console and narrator | The **room language** | Whoever creates the room. It can be changed in the lobby, before starting |
| Each player's phone | **Their own** | Each player, on their phone. By default, the browser's language if available; otherwise, the room's |

So, at a mixed table, public information appears in one language and each person reads their private information in their own.

## 4. Texts and content

- **Interface:** all visible texts live in per-language catalogs, never written in the code.
- **Structured content** (cards, dares, deck and space names): each text has one entry per language. Spanish and English are mandatory; the others are optional.
- **Truth or Dare** is adapted culturally, not translated word for word. Each language has its own editorial review (P-12).
- **Countries:** the ID is the ISO code (`MEX`) in every language; the name is translated (“México” / “Mexico”).
- **Powers:** the fixed name of each color is translated (“Potencia Ámbar” / “Amber Power”).
- **“Geoconquista” is not translated.**
- **Numbers:** formatted per language (thousands and decimal separators).

## 5. Narrator and audio

- The project only produces **voices in Spanish**: El Faraón (D-17, D-30).
- If the community contributes a **catalog of narrator lines in another language**, it is used in rooms in that language. If it does not exist, or a line is missing, **the Spanish line plays**.
- Effects and music do not depend on the language.
- Audio contributed by the community is published under CC BY-SA 4.0 if it was not generated with ElevenLabs, or under the Geoconquista audio license if it was (ADR-003).

## 6. Art

- Illustrations carry no text (`assets/pipeline.md` §3): cards and the interface are composed in each language over the same image.
- **Images that do carry text** (logo, lettering, some backgrounds) are produced **in Spanish**. If the community contributes the version in another language, it is used; otherwise, the Spanish one is shown.

## 7. Acceptance criteria

- **AC-009.1:** with the same seed and the same commands, a game with the room in `es` and another in `en` produce exactly the same state.
- **AC-009.2:** a player with their phone in `en` in an `es` room sees their private texts in English, and the board stays in Spanish.
- **AC-009.3:** content validation rejects a card, space or interface text without a Spanish or English entry, and says which one is missing. A community language missing an entry does not appear as an option.
- **AC-009.4:** in an English room without an English narrator catalog, the narrator says the line in Spanish.
- **AC-009.5:** no visible interface text is written directly in the code: a test goes through the screens and finds no untranslated keys in any offered language.

## 8. Questions for the creator

1. Is this split OK: room language for public information and each player's own language on their phone?
2. ~~Do we explore English voices?~~ No: only Spanish voices; the others are contributed by the community (D-30).
