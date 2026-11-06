# Rules for coding agents — Geoconquista

> This is the English translation of [AGENTS.md](AGENTS.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

This file is the **single source** of rules for any agent working in the repository (Claude Code in Visual Studio Code or others). `CLAUDE.md` only points here. The rationale for each rule is in [ADR-000](docs/decisions/ADR-000-gobernanza.en.md).

## 1. Documentation First

**If it is not documented and approved, it is not implemented.**

- Do not invent rules, figures, effects, screens, buttons, error texts, states or contracts. Whatever is missing is recorded as a question or proposal in `docs/`; it is not resolved by intuition in the code.
- Changing a rule, a flow or the architecture requires updating and approving the document first, and the code afterwards.
- A conflict between documents **blocks** implementation until it is resolved (see §3).

## 2. What can be created and when

| What | When | Where |
|---|---|---|
| Documentation | Always, in `PROPUESTO` (proposed) state | `docs/` |
| Technical spikes (throwaway code from E2) | After G0 is approved | Branch `spike/<id>`; never merged. Only its conclusions go into an ADR |
| Art and audio exploration | After G0 is approved | `exploracion/` (ignored by git). Only what is approved moves to `assets/`, with its entry in the manifest |
| `apps/`, `packages/`, `tools/` (product code) | **Only after gate G3** | Structure from `docs/roadmap/plan-de-arranque.md` §6.3 |
| `assets/` (final assets) | When the art or audio direction is `APROBADO` (approved) and a UX document requests the asset | `assets/` + `assets/manifest.json` |

Current gate status: see `docs/README.md`.

## 3. States and precedence

- Document states: `PROPUESTO`, `PENDIENTE`, `APROBADO` (with approver and date) and `OBSOLETO`.
- Only the creator approves. An agent never marks anything as `APROBADO` on its own.
- In a conflict: `APROBADO` prevails over `PROPUESTO`. Between two approved documents, the more recent one prevails **only if it explicitly cites** the earlier one. In any other case, `HAY_CONFLICTO_DOCUMENTAL` is declared and nothing is implemented.

## 4. Conventions

- **IDs:** `FS-###` (feature spec), `AC-###.#` (acceptance criterion of spec `###`), `ADR-###`, `D-###` (creator's decision), `CARD-<tipo>-###` (card), `EVT-###` (event).
- **Modes:** `familiar_u18`, `familiar_18`, `party_18`, `party_extreme_18`, `parejas_18`. Never `couples_18`.
- **Visibility:** `público`, `propietario`, `partes_tratado` and `sistema`. The console (tablet) does **not** have its own level of secrets.
- **Languages (D-29):** documentation is written and approved in Spanish, which is the canonical version. Each document has its English translation in `<nombre>.en.md`, which is updated **in the same commit** as the original. If they differ, the Spanish version prevails. States, IDs and data identifiers are not translated. Exception: the startup plan is only in Spanish.
- **Documentation paths:** the tree in `docs/README.md`. Do not create documents with alternative names (`game-loop.md`, `modes.md`, `host-screen.md`, etc.).
- **Stack and hardware:** no technology is assumed. Refer to ADR-001 (stack and clients) and ADR-002 (public screen).

## 5. Output contract

Any task that creates or modifies code, specs, content or assets starts with these five points. Questions and explanations do not need it.

1. **Source documents:** files and sections that govern the task.
2. **Documentation status:** `LISTO_PARA_IMPLEMENTAR`, `FALTA_DOCUMENTACION` or `HAY_CONFLICTO_DOCUMENTAL`.
3. **Immediate action:** `VOY_A_DOCUMENTAR`, `VOY_A_IMPLEMENTAR` or `VOY_A_ACTUALIZAR_DOCS_Y_LUEGO_IMPLEMENTAR`.
4. **Traceability:** spec, AC and ADR IDs, and affected modules or assets.
5. **Result:** at closing, what changed and why, which tests cover it and what was left pending.

The full procedure is in the `documentation-first` skill (`.claude/skills/documentation-first/SKILL.md`).

## 6. Technical invariants (valid with any stack)

- The host is the only authority: clients send commands and never decide the state.
- The server filters each view. No client receives the full state or other players' private data.
- No essential function depends on the Internet: no CDNs, remote fonts, analytics or AI during a game.
- Rules live in the engine and figures in content data, never in the interface or as loose constants.
- Cards, dares and texts live in structured content with an ID, modes and editorial status.

## 7. Secrets and generated assets

- API keys go **only** in `.env` (ignored by git; template in `.env.example`). Never in code, documents, saved prompts or commit messages.
- Every AI-generated asset records in `assets/manifest.json` the tool, the model, the date, the prompt, the edits and the applicable license terms. Without that entry it does not go into `assets/`.

## 8. Git

- Commits and PR descriptions **carry no attribution** to any assistant: no `Co-Authored-By`, no “Generated with”, and no variant of them. The message ends on its last line of content.
- Commits or pushes are made only when the creator asks for them.
- The creator's commits, including those an agent makes on their behalf, do **not** carry `Signed-off-by`: the creator is the rights holder and does not sign the DCO. The DCO (`git commit -s`) is for external contributions (ADR-003, `CONTRIBUTING.md`).
