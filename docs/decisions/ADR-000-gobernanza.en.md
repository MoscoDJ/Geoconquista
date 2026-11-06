# ADR-000 — Documentation governance and rules for agents

> This is the English translation of [ADR-000-gobernanza.md](ADR-000-gobernanza.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| Status | `APROBADO` (approved) |
| Date | 2026-11-05 |
| Approver | Creator, 2026-11-05 (G0) |
| Origin | Startup plan, DEC-09 and §4.4 (G-1 to G-9) |

## Context

The project inherited three sets of conventions that contradict each other: the brief (`Contexto/GEOCONQUISTA_BRIEF_DEBATE.md` §11), the supplement `Contexto/gobernanza/extras.md` and the Cursor pack (`Contexto/gobernanza/cursor-doc-first-skill-pack-original/`). The startup plan (`docs/roadmap/plan-de-arranque.md` §4.4) recorded nine conflicts, G-1 to G-9, and recommended adopting the corrected Cursor pack (DEC-09).

There are three more facts that this ADR must also cover:

- Development is done with coding agents from Visual Studio Code: Claude Code and any other that reads `AGENTS.md` (D-05). Rules repeated across several files would end up diverging.
- The creator decided not to make a paper prototype (D-01). That brings the engine code forward and makes it even more important that no unapproved rules are programmed.
- The creator asked the agent to generate and edit the graphics and sound kit (D-04). That introduces AI-generated assets, which need traceability and licensing.

## Decision

### 1. A single source of rules for agents
`AGENTS.md`, at the root, contains all the rules. `CLAUDE.md` imports it. The procedure lives in a single skill, `.claude/skills/documentation-first/SKILL.md`. There is no Cursor configuration: the creator works in Visual Studio Code (D-05), and the one from the inherited pack is not installed. The `AGENTS.md` and `CLAUDE.md` files of the debate app were moved to `Contexto/debate-app/`, because they are instructions for the debate participants and not for working in this repository.

### 2. Precedence by status (resolves G-1)
Both fixed orders by folder are discarded: the one in `extras.md` (gameplay first) and the one in the pack (specs first). The criterion in `AGENTS.md` §3 applies: `APROBADO` prevails over `PROPUESTO`, and between two approved documents the more recent one prevails only if it cites the earlier one. Any other conflict blocks implementation.

### 3. IDs (resolves G-2)
`FS-###`, `AC-###.#`, `ADR-###`, `D-###`, `CARD-<tipo>-###` and `EVT-###`.

**Adjustment to DEC-09:** cards use the **type** (`hacienda`, `migracion`, `correo`, `mensajeria`, `verdad`, `reto`) and not the mode. A card can belong to several modes (field `modos[]`), and one ID per mode would duplicate it. The plan's provisional ACs (`AC-CORE-01`, `AC-PRIV-01`, etc.) are renumbered as `AC-###.#` in E3, when each one is assigned to its spec.

### 4. Documentation tree (resolves G-3)
The tree from the brief §11.2, plus the following documents:

- `docs/decisions/ADR-000-gobernanza.md` (this document).
- `docs/gameplay/parameters.md`: all the figures of the v0 rules (D-01).
- `docs/testing/acceptance-matrix.md`.
- `docs/assets/art-direction.md`, `audio-direction.md` and `pipeline.md` (D-04).
- `docs/roadmap/plan-de-arranque.md`: current copy of the plan. The original from the debate stays archived in `Contexto/plan.md` and is not edited again.

The stub files from the Cursor pack (`game-loop.md`, `modes.md`, `host-screen.md`, `system-overview.md`, etc.) are not copied.

### 5. Couples mode (resolves G-4)
`parejas_18`.

### 6. Visibility (resolves G-5)
Four levels: `público`, `propietario`, `partes_tratado` and `sistema`. The `public/private/admin` levels of `extras.md` and the `moderador` level of the brief §9.4 are discarded, because moderating does not grant access to secrets (DEC-06).

### 7. Code structure (resolves G-6, G-7 and the consolidator's observation 1)
The structure of `apps/`, `packages/` and `tools/` is the one in the plan §6.3. **It is created only after gate G3.** This resolves the difference between “after ADR-001” (§6.3) and “until G3” (§7.1): the later condition applies. The pack's instruction “If they do not exist yet, propose and create this base structure” is removed.

### 8. No technical assumptions in the rules (resolves G-8)
The rules for agents do not take Flutter or the Raspberry Pi for granted. The stack is decided in ADR-001 and the public screen in ADR-002.

### 9. A single output contract (resolves G-9)
The five points of `AGENTS.md` §5 are used, with the states `LISTO_PARA_IMPLEMENTAR`, `FALTA_DOCUMENTACION` and `HAY_CONFLICTO_DOCUMENTAL`. The four-block format of the original `.mdc` rule disappears. The contract applies to tasks that change code, specs, content or assets, not to questions or explanations.

### 10. Authorized exceptions before G3
- **Technical spikes (E2):** throwaway code in `spike/<id>` branches that are never merged. Only their measurements and conclusions go into ADR-001 and ADR-002.
- **Art and audio exploration:** style tests and variants in `exploracion/`, a folder ignored by git. Nothing there is used in the product until the art or audio direction is approved and a UX document asks for the asset.

### 11. Secrets and generated assets
API keys go only in `.env`, which is ignored by git. Each asset in `assets/` has an entry in `assets/manifest.json` with its origin and the applicable license terms (`docs/assets/pipeline.md`).

### 12. Bilingual documentation (D-29, added on 2026-11-06)

- **Spanish is the canonical version**: documents are written, reviewed and approved in Spanish. If the translation says something different, Spanish prevails.
- Each document has its English translation in a sibling file: `core-loop.md` → `core-loop.en.md`. The translation starts with a note that links the original and reminds the reader that Spanish prevails.
- Every change to a Spanish document updates its `.en.md` **in the same commit**. An outdated translation is treated as a documentation defect.
- States (`APROBADO`, `PROPUESTO`…), IDs and data identifiers are not translated.
- Everything is translated except `docs/roadmap/plan-de-arranque.md`, which remains as a historical file in Spanish, and `Contexto/`.

### 13. Definition of Ready and Definition of Done
- **DoR:** the one in `extras.md` §1, plus two conditions: the spec is `APROBADO`, and it cites the v0 rule, or the simulator or session result, that backs it.
- **DoD:** the code implements only what is documented, each AC has a passing test, the `acceptance-matrix.md` row is updated, and no decision is left “only in code”.

## Alternatives considered

- **Adopting `extras.md` as the base.** It lacks the operational workflow for the agent and its visibility model is insufficient.
- **Adopting the Cursor pack without correcting it.** It would lead the agent to create the structure too early, to use `couples_18` and to assume Flutter, contrary to the brief.
- **Keeping separate rules per tool (one copy per agent).** Duplicating them guarantees they diverge over time.

## Consequences

- **Positive:** a single place to change the rules; agents cannot create product code before G3; generated assets remain traceable for the open source release.
- **Negative:** the five-point contract adds friction to every task. Assets require maintaining the manifest.

## Approval

- The creator approved G0 on 2026-11-05: this ADR, `docs/product/vision.md` and `docs/roadmap/milestones.md`.
- `Contexto/` (brief, debate and screenshots) stays **local only** and is not published (D-10). It remains ignored by git.
