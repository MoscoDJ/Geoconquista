# Asset pipeline: tools, flow and licenses

> This is the English translation of [pipeline.md](pipeline.md). The Spanish version is canonical: if they differ, the Spanish version prevails (D-29).

| Field | Value |
|---|---|
| Status | `PROPUESTO` |
| Date | 2026-11-05 |
| Sources | D-04; ADR-000 §10 and §11; art direction and audio direction |

## 1. Tools

| Need | Tool | Intended use |
|---|---|---|
| Image generation | OpenAI, default model `gpt-image-2.6-sunburst` | Illustrations and variants; masked editing |
| Image generation | Google AI Studio (Gemini / Imagen) | Illustrations and conversational editing with references |
| Open models | Replicate | Open image models, training a custom style (LoRA) once there are hundreds of cards, background removal and upscaling |
| Upscaling and detail | Magnific | Upscaling of the final pieces for the board and the major events |
| Music, effects and voices | ElevenLabs (API or MCP) | Layered music, effects and narrator |
| Raster editing | ImageMagick, GIMP, Python (Pillow) | Cropping, compositing, color, card templates, sprite sheets and optimization |
| Vector | Inkscape, hand-written SVG, `rsvg-convert` | Map, icons, logotype and redrawn emblems |
| Audio | ffmpeg, sox | Normalization, cuts, loops, fades and format conversion |
| Geographic data | Natural Earth (public domain) | Base geometry for the 24-region map |

The exact model identifiers and their versions are recorded in each manifest entry, not here, because they change often.

## 2. Access

The keys go in `.env`, at the root of the repository. As of 2026-11-05 there is access to **OpenAI** and **ElevenLabs** (variables `OPENAI` and `ELEVENLABS`). Google AI Studio, Replicate and Magnific are added when needed. It is ignored by git, and its template is `.env.example`. Keys are never written in documents, saved prompts or commits. The generation scripts read `.env` and fail with a clear message if a key is missing.

## 3. Flow of an asset

```text
written need (UX or content)
  → asset brief (templates/asset-brief.md)
  → variants in exploracion/<línea>/<activo>/   (ignored by git)
  → creator review on the local comparison page
  → final editing + optimization
  → assets/<ruta>  +  entry in assets/manifest.json
```

- **Style consistency:** each visual line has a fixed “style prompt” and approved reference images, reused in every generation. If the volume justifies it (the A2 decks), a custom style is trained on Replicate with the approved pieces.
- **Nothing leaves the AI without editing:** hands and fake text are checked, color is corrected against the palette, and the piece is cropped to the format and weight its destination requires.
- **Text inside images:** never generated. Card and interface text is composed on top with the project's fonts. That way it can be translated, it is legible and there are no generated spelling mistakes.

## 4. Review by the creator

Each exploration batch produces a local HTML page in `exploracion/` that shows the variants side by side, with players for the audio and the information for each one. The creator marks what is approved and what is discarded. Only what is approved moves forward.

## 5. Manifest (`assets/manifest.json`)

Each asset in `assets/` has an entry with:

| Field | Content |
|---|---|
| `id`, `ruta`, `tipo` | Stable identifier, file path, and image, vector, music, effect or voice |
| `requerido_por` | UX or content document that requests it |
| `origen` | `construido`, `generado` or `mixto` |
| `herramienta`, `modelo`, `fecha` | What it was generated with and when |
| `prompt`, `referencias`, `semilla` | What is needed to reproduce or regenerate it |
| `ediciones` | Later steps (upscaling, cropping, touch-up, normalization) |
| `terminos` | Terms of use of the provider and of the account plan on the generation date |
| `aprobado_por`, `fecha_aprobacion` | Creator and date |

## 6. Licenses (D-26, ADR-003)

The licenses are decided in ADR-003: CC BY-SA 4.0 for images and compositions, and the closed license `LicenseRef-Geoconquista-Audio` (D-27) for everything generated with ElevenLabs, because its terms do not allow distributing the effects separately. The manifest's `terminos` field also records each asset's license.

### Points still open

Before publishing (E7), three things must be verified against the current terms and each account's plan:

1. **Commercial use and redistribution.** Whether each provider allows distributing its outputs inside an open source project. For some services, such as ElevenLabs, it depends on the subscribed plan.
2. **License that can be declared.** In several jurisdictions, material generated without enough human contribution might not be protected by copyright. That affects the license that can be declared over the content (for example, CC BY-SA). `[PEND: review before E7]`
3. **Third-party material.** That no reference used in a prompt or as an input image is protected third-party material.

That is why the manifest records the terms **on the generation date**.

## 7. Costs

Every generation has a cost. During A0 the batches are small: few variants per subject, and only the promising direction is expanded. An approximate log of spending per batch is kept in `exploracion/costes.md`, so the creator can see where the money goes.
