# Audio direction

> This is the English translation of [audio-direction.md](audio-direction.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| Status | `PROPUESTO`. Hybrid music (D-18), narrator El Faraón (D-17), Spanish only (D-30), and exploration effects chosen (D-21, D-23) |
| Date | 2026-11-05 |
| Sources | Vision (pillars 1, 5 and 7); brief §4.3 (narrative phases) and §9.4 |

## 1. Principle: sound supports the table, it doesn't drown it out

The game is a conversation: people negotiate, argue and laugh. Audio gives weight to the important moments and steps back during conversation.

- Sound comes **mainly from the board**, through the speakers of the screen connected to the host. It is the same sound for everyone and reveals nothing private.
- **Phones are silent by default.** At most, a vibration or a short alert when it is your turn or when you receive something private. A sound on a player's phone would reveal to the table that they received something (pillar 2).
- The **tablet** plays a sound when the dice land (D-08), because the roll is public. Otherwise it only gives tactile and audio feedback to its own taps, at low volume.
- Rolling the dice (swipe) is a public gesture, so that phone may give a short vibration on the roll. It still makes no sound for anything private.

## 2. Adaptive music by phase

The brief describes three stages of experience: expansion, consolidation and world crisis. The proposal is one piece per stage, built in **layers (stems)** that are added according to the tension of the game, instead of abrupt cuts between themes.

| Moment | Character | Layers |
|---|---|---|
| Lobby | Invitation, mystery, “the situation room opens” | Single looping theme |
| Expansion | Curiosity, optimism, markets | Base + melody |
| Consolidation | Diplomatic tension, first clashes | + percussion and a more insistent bass |
| World crisis | Urgency, drums, brass | + war percussion layer |
| Victory | Resolution | Short fanfare and final theme |

Rules: music sits **below** effects and voice and ducks automatically when a voice plays. There are independent volume controls for music, effects and voice. Default volume is moderate, because the table talks over it.

## 3. Sound effects

Every public event with weight has its own sound signature: country purchase, complete bloc, threat band change (“something moved”), attack declaration, combat result (attacker wins or defense holds), conquest, treaty signed, treaty broken, end of round and end of game.

Each of the five decks has its own signature when a card is drawn (Tax Office, Immigration, Mail, Messaging and Truth or Dare), so the table knows what is coming before reading it.

**Privacy constraint:** an effect must not reveal private information. For example, it cannot sound different when recruiting 1 troop than when recruiting 5, nor play on the board when a player takes a private action that changes nothing public.

## 4. Voices

A **narrator** or “international news announcer” announces public events.

- **No-Internet mode constraint:** voice cannot be generated during the game. Every line is generated in advance and bundled with the application.
- **Consequence:** the narrator cannot say the free-text name each player typed. There are two options:
  - (a) generic lines (“A power has completed a bloc!”);
  - (b) a fixed catalog of power names tied to the color or the emblem (for example, “the Amber Power”), combined with pre-recorded segments: power + action + region. With 6 powers and 24 regions the catalog is manageable.

  Recommendation: (b) for the main actions and (a) for the rest. For this, power names have to be fixed content, and that is decided in `ux/lobby.md`.
- **Languages (D-30):** the project only produces voices in Spanish. If the community contributes a catalog of lines in English, it is used in English rooms; otherwise the Spanish one plays (`product/localization.md` §4).
- **Spanish voice (D-17):** “El Faraón – Powerful and Mysterious”, Latin American Spanish, deep and epic (ElevenLabs, library voice `Rl2JPHsuEWSfwCD4ZHIQ`, model `eleven_v4`). It is the same voice in every mode; the tone can be more theatrical in the party modes if the text calls for it.
- **License:** it is a voice from the ElevenLabs shared library, generated on a Pro plan (commercial use). If its author removes it from the library, audio already generated remains usable, but no new lines could be generated with it. That is why the line catalog is generated in full in one go, once it is closed.

## 5. A0 exploration

- **Music (decided, D-18): hybrid.** Two directions were explored:
  - **Cinematic orchestral:** strings, brass and war percussion.
  - **Situation-room electronic:** synthesizers, pulses and thriller tension.
- **Effects:** a batch of 5 key effects (purchase, bloc, attack, conquest, card draw) in both directions.
- **Voice:** 3 candidate voices reading the same 5 lines.

## 6. Technical requirements (provisional until S1 and S2)

- **Normalized loudness:** all tracks are matched to the same perceived level so that no effect “shouts”. Target value to be set in A1.
- **Seamless loops** in the music. Effects last under 2 s, except those for major events.
- **Format** compatible with Chromium on the Pi and with Safari on iOS. Confirmed in S1 and S2.
- **No external dependencies:** all files are served from the host.

## 7. Process limitation

The agent that generates the audio **cannot listen to it**. It can measure level, duration, silences, loop cuts and spectrum, and organize and compare variants. But the choice of what sounds good is made by **the creator**, on a local review page with all the variants (`docs/assets/pipeline.md` §4).
