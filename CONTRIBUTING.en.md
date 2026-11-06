# How to contribute to Geoconquista

> This is the English translation of [CONTRIBUTING.md](CONTRIBUTING.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

Thank you for wanting to contribute! Geoconquista is a geopolitical strategy game played in person, with a board on a large screen, a tablet as the console and the players' phones. It runs on the local network, without Internet.

## Before you start

- **Code of conduct:** by taking part you accept the [code of conduct](CODE_OF_CONDUCT.en.md).
- **Licenses:** the code is AGPL-3.0-or-later and the content CC BY-SA 4.0 ([LICENCIAS.md](LICENCIAS.en.md)). By contributing, you agree that your contribution is published under those licenses.
- **Project status:** see [docs/README.md](docs/README.en.md), which shows the current stage and which gates are approved.

## The main rule: documentation first

**If it is not documented and approved, it is not implemented.** The game rules, the screens and the architecture are decided in `docs/` before any code is written.

- **Want to change a rule, a figure or a screen?** Open an *issue* or a *pull request* that modifies the corresponding document in `docs/`. Once the creator approves it, it is implemented.
- **Found a bug?** Open an *issue*. If the bug reveals a behavior that no document defines, it has to be documented before it is fixed.
- **Want to program something?** First find the approved spec that asks for it (`docs/gameplay/`, `docs/ux/`…) and cite its acceptance criteria (`AC-###.#`) in your *pull request*.
- **The game's figures** (prices, income, troops…) are in [docs/gameplay/parameters.md](docs/gameplay/parameters.en.md) and in the content data, never in the code.

The full rules for those who program, including if you use AI agents, are in [AGENTS.md](AGENTS.en.md).

### Languages

The documentation is in Spanish and English. Spanish is the reference version: each document `name.md` has its translation `name.en.md`. If you change a document, update both versions; if you only write in English, that's fine: say so in the *pull request* and it will be translated into Spanish during review. The game is native Spanish and has all its texts in English too. **Voices and images with text** are only produced in Spanish: if you want the English version to have an English narrator or English images, your contributions are welcome! See [docs/product/localization.md](docs/product/localization.en.md).

## Sign your commits (DCO)

We use the [Developer Certificate of Origin](DCO): with each commit you certify that you have the right to contribute that work under the project's license. Sign each commit with:

```bash
git commit -s -m "Description of the change"
```

That adds a `Signed-off-by: Your Name <you@example.com>` line to the message. *Pull requests* without that line in all their commits cannot be merged.

## Content: cards, dares and texts

- Each card follows the [docs/templates/card.md](docs/templates/card.en.md) template, with its modes and its editorial status.
- No ethnic, religious or national stereotypes, and no real political leaders.
- In Truth or Dare you can always pass, and no dare requires harm, mandatory alcohol or non-consensual contact.
- **18+ content:** contributions for the `familiar_18`, `party_18`, `party_extreme_18` and `parejas_18` modes go through editorial review before they are accepted. Content for `familiar_u18` must be suitable for minors.

## Art and audio

- Final assets go in `assets/` with their entry in `assets/manifest.json`: origin, tool, date, edits and license.
- If you used an AI tool, state which one, the model and the prompt, and confirm that its terms allow publishing it under the project's license.
- Do not use protected third-party material, or the identifiable style of a living artist.

## Security

Never include API keys or secrets in the code, the documentation or the commits. They go in `.env`, which is ignored by git.
