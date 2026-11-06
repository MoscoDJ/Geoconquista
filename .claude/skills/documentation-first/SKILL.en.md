---
name: documentation-first
description: Mandatory Geoconquista procedure for implementing features, changing rules, creating screens or flows, touching architecture, networking or persistence, fixing bugs that reveal undocumented behavior, creating content (cards, dares, decks) or adding art and audio assets. Document first, implement afterwards.
---

# Documentation First: procedure

> This is the English translation of [SKILL.md](SKILL.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

The rules are in `AGENTS.md` and their rationale in `docs/decisions/ADR-000-gobernanza.md`. This skill describes **how** to apply them step by step. If anything here contradicts `AGENTS.md`, `AGENTS.md` prevails and this skill is corrected.

## Phase 1. Documentation discovery

1. Check `docs/README.md` for the status of the gates (G0–G3) and the decision log.
2. Locate the documents that govern the task: gameplay, UX, architecture, `FS-###` specs and ADRs.
3. Check their status. Only `APROBADO` (approved) authorizes implementation.
4. List gaps, ambiguities and contradictions.
5. Declare the documentation status: `LISTO_PARA_IMPLEMENTAR`, `FALTA_DOCUMENTACION` or `HAY_CONFLICTO_DOCUMENTAL`.

## Phase 2. Documentation

If something is missing, create or update what is needed in `PROPUESTO` (proposed) state:

- The feature spec (`docs/templates/feature-spec.md`) with its verifiable ACs.
- An ADR (`docs/templates/adr.md`) if there is an architecture decision.
- The UX document, if a flow or a screen changes.
- The gameplay document and `docs/gameplay/parameters.md`, if a rule or a figure changes.
- The card sheet (`docs/templates/card.md`) or asset brief (`docs/templates/asset-brief.md`), if it is content or art.

Also update the `<nombre>.en.md` translation of every document you touch (D-29); if it is a new document, create it.

Then **stop** and ask for the creator's approval. Do not continue to Phase 3 on `PROPUESTO` documents.

## Phase 3. Implementation plan

Before editing code, present a short plan with:

- source documents and spec and AC IDs;
- modules and files to be created or edited;
- tests that will demonstrate each AC;
- risks.

## Phase 4. Implementation

- Implement only what is documented, with names aligned with the documentation.
- Respect the boundaries: engine (rules, no I/O) → protocol → server → client. The interface never decides a rule.
- Figures come from content data; texts, cards and dares, from structured content.
- If an undocumented decision comes up, **stop** and go back to Phase 2.

## Phase 5. Validation

- Each AC has at least one passing test.
- There is no behavior outside the spec.
- Filtered views do not expose data from a higher visibility level (`AC-PRIV` tests).
- The corresponding row of `docs/testing/acceptance-matrix.md` is updated.

## Phase 6. Closing

Deliver point 5 of the output contract: documents and files touched, tests added, open risks or debts, and confirmation that nothing went beyond the documented line.

## Signals to stop and go back to documenting

- “This isn't specified, but surely it's better this way.”
- “To make it work I added this extra behavior.”
- “The interface needs to decide a game rule.”
- “Two documents say different things.”
- “The feature affects several surfaces, but there is only a document for one.”
- “I'll hard-code this figure and we'll take it out later.”

## Bugs and refactors

- **Bug that contradicts an approved document:** it is fixed and the missing test is added.
- **Bug that reveals behavior that was never documented:** first the expected behavior is documented and approved; then it is fixed.
- **Refactor:** only if it preserves the documented behavior or is backed by an approved documentation change. It is never used to sneak in functional changes.

## Art and audio assets

1. The asset responds to a need written in a UX or content document.
2. It is explored in `exploracion/` following `docs/assets/pipeline.md`.
3. The creator chooses between variants.
4. The final asset is edited, optimized and copied to `assets/` with its complete entry in `assets/manifest.json`.
