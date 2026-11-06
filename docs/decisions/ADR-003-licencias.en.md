# ADR-003 — Licenses and community contributions

> This is the English translation of [ADR-003-licencias.md](ADR-003-licencias.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| Status | **`APROBADO`** (approved) by the creator, 2026-11-06 (D-26 and D-27) |
| Date | 2026-11-06 |
| Origin | P-10; startup plan DEC-12; `docs/assets/pipeline.md` §6 |

## Context

The creator wants the community to contribute code, content and art, and wants those improvements to come back to the project. There are four kinds of material with different conditions: the code, the project's own content (rules, cards, map, illustrations), third-party assets (fonts and geographic data), and the audio generated with ElevenLabs, whose terms of use restrict redistribution.

## Decision

### 1. Licenses by kind of material

| Material | License | File |
|---|---|---|
| **Code** (`apps/`, `packages/`, `tools/` and any script) | **AGPL-3.0-or-later** | `LICENSE` |
| **Own content**: documentation, rules, cards, texts, map data, illustrations, icons and compositions | **CC BY-SA 4.0** | `LICENSES/CC-BY-SA-4.0.txt` |
| **Audio generated with ElevenLabs**: voices, effects and music | **Geoconquista audio license** (§4) | `LICENSES/LicenseRef-Geoconquista-Audio.md` |
| **Fonts** | SIL OFL 1.1, each font's own | Next to each font |
| **Natural Earth geometry** | Public domain | — |

`LICENCIAS.md`, at the root, explains which license applies to each folder. Once there are assets, `assets/manifest.json` states the license of each one.

**Why AGPL and CC BY-SA:** both are *copyleft*. Whoever modifies and distributes the game, or offers it as a network service, must publish their changes under the same license. That way improvements come back to the community.

### 2. Name and logo

“Geoconquista” and its logo are **not** licensed with the code or the content. Anyone can make a derivative version, but under another name (`MARCA.md`).

### 3. Contributions

- **DCO** (*Developer Certificate of Origin* 1.1, file `DCO`) instead of an assignment agreement (CLA). Contributors sign off each commit with `git commit -s` and certify that they have the right to contribute it under the project's license.
- **The creator does not sign the DCO** on their own commits, because they are the rights holder. This keeps their rule of commits without a sign-off footer (`AGENTS.md` §8).
- `CONTRIBUTING.md` explains the *Documentation First* workflow for contributors.
- **Code of conduct:** Contributor Covenant 2.1, in Spanish (`CODE_OF_CONDUCT.md`) and in its original English version (`CODE_OF_CONDUCT.en.md`).
- **+18 content:** cards and dares contributed for the +18 modes go through editorial review before they are accepted (P-12).

### 4. ElevenLabs audio (D-27)

What the ElevenLabs terms say as of 2026-11-06:

- [Terms of use](https://elevenlabs.io/terms-of-use) (updated on 2026-10-09), §4(c)(ii): the user keeps the rights to their generated audio. §1(c): commercial use is allowed with a paid plan.
- [Voice library addendum](https://elevenlabs.io/vla) (2026-03-06): if the author removes a voice from the library, what was generated before remains usable. It adds no redistribution restrictions for whoever generates.
- [ElevenCreative terms](https://elevenlabs.io/creative-terms), annex 4 (sound effects): incorporating them into games is allowed, but distributing them separately is **not**, “as isolated audio files or samples, or as part of any sound … library”.

**Consequence:** ElevenLabs audio cannot be published under CC BY-SA, because that license would allow anyone to extract the files and redistribute them separately. **Creator's decision (D-27): all ElevenLabs audio —voices, effects and music— carries the restrictive license.**

**Geoconquista audio license** (`LICENSES/LicenseRef-Geoconquista-Audio.md`, version 1.0): these files may be redistributed, unmodified, **only as part of Geoconquista or of a game derived from it** distributed under the project's licenses. Extracting them for separate use, including them in sound libraries or collections, or using the voices outside the game is not allowed.

**Pending check before publishing the first audio in `assets/`:** read the ElevenLabs OEM terms, which govern “bundling, making available and sublicensing”, and its prohibited use policy. If they require anything more, version 1.1 of the license is published.

Community audio contributions made without ElevenLabs may be released under CC BY-SA 4.0.

### 5. AI-generated material

- Images generated with OpenAI belong to the user under its terms; they are published under CC BY-SA 4.0.
- In several jurisdictions, material generated without enough human contribution might not be protected by copyright. The license is declared anyway; human edits and compositions, such as the card layouts or the vector map, are protected. Each asset records in the manifest which part is generated and which part is edited (`AGENTS.md` §7).

## Consequences

- **Positive:** community improvements come back to the project; a DCO is simple for contributors; the name is protected.
- **Negative:**
  - **iPad App Store:** Apple's terms clash with the AGPL. Once there is community code, publishing on the App Store would be complicated. Google Play does not have that problem, and Android is the main platform (D-03).
  - Anyone can distribute a compiled version for free.
  - The audio has a license different from the rest of the content, which has to be explained in `LICENCIAS.md`.

## Rejected alternatives

- **MIT and CC BY 4.0:** maximum freedom, but they allow closed versions that give nothing back to the community.
- **GPL-3.0 without the A:** it does not require whoever offers the game as a network service to publish their changes.
- **CLA:** it would allow changing the license in the future, but it discourages contributors.
