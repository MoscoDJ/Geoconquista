# ADR-003 — Licencias y aportaciones de la comunidad

| Campo | Valor |
|---|---|
| Estado | **`APROBADO`** por el creador, 2026-11-06 (D-26 y D-27) |
| Fecha | 2026-11-06 |
| Origen | P-10; plan de arranque DEC-12; `docs/assets/pipeline.md` §6 |

## Contexto

El creador quiere que la comunidad aporte código, contenido y arte, y que esas mejoras vuelvan al proyecto. Hay cuatro tipos de material con condiciones distintas: el código, el contenido propio (reglas, cartas, mapa, ilustraciones), los activos de terceros (fuentes y datos geográficos) y el audio generado con ElevenLabs, cuyas condiciones de uso restringen la redistribución.

## Decisión

### 1. Licencias por tipo de material

| Material | Licencia | Archivo |
|---|---|---|
| **Código** (`apps/`, `packages/`, `tools/` y cualquier script) | **AGPL-3.0-or-later** | `LICENSE` |
| **Contenido propio**: documentación, reglas, cartas, textos, datos del mapa, ilustraciones, iconos y composiciones | **CC BY-SA 4.0** | `LICENSES/CC-BY-SA-4.0.txt` |
| **Audio generado con ElevenLabs**: voces, efectos y música | **Licencia de audio de Geoconquista** (§4) | `LICENSES/LicenseRef-Geoconquista-Audio.md` |
| **Fuentes tipográficas** | SIL OFL 1.1, la de cada fuente | Junto a cada fuente |
| **Geometría de Natural Earth** | Dominio público | — |

`LICENCIAS.md`, en la raíz, explica qué licencia aplica a cada carpeta. Cuando haya activos, `assets/manifest.json` indica la licencia de cada uno.

**Por qué AGPL y CC BY-SA:** ambas son *copyleft*. Quien modifique y distribuya el juego, o lo ofrezca como servicio en red, tiene que publicar sus cambios con la misma licencia. Así las mejoras vuelven a la comunidad.

### 2. Nombre y logotipo

«Geoconquista» y su logotipo **no** se licencian con el código ni con el contenido. Cualquiera puede hacer una versión derivada, pero con otro nombre (`MARCA.md`).

### 3. Aportaciones

- **DCO** (*Developer Certificate of Origin* 1.1, archivo `DCO`) en lugar de un acuerdo de cesión (CLA). Quien aporta firma cada commit con `git commit -s` y certifica que tiene derecho a aportarlo bajo la licencia del proyecto.
- **El creador no firma DCO** en sus propios commits, porque es el titular. Esto mantiene su regla de commits sin pie de firma (`AGENTS.md` §8).
- `CONTRIBUTING.md` explica el flujo *Documentation First* para quien aporta.
- **Código de conducta:** Contributor Covenant 2.1 en español (`CODE_OF_CONDUCT.md`).
- **Contenido +18:** las cartas y retos aportados para los modos +18 pasan revisión editorial antes de entrar (P-12).

### 4. Audio de ElevenLabs (D-27)

Lo que dicen las condiciones de ElevenLabs a 2026-11-06:

- [Términos de uso](https://elevenlabs.io/terms-of-use) (actualizados el 09-10-2026), §4(c)(ii): el usuario conserva los derechos sobre su audio generado. §1(c): con plan de pago se permite el uso comercial.
- [Anexo de la biblioteca de voces](https://elevenlabs.io/vla) (06-03-2026): si el autor retira una voz de la biblioteca, lo generado antes sigue siendo utilizable. No añade restricciones de redistribución para quien genera.
- [Condiciones de ElevenCreative](https://elevenlabs.io/creative-terms), anexo 4 (efectos de sonido): se permite incorporarlos a juegos, pero **no** distribuirlos por separado, «as isolated audio files or samples, or as part of any sound … library».

**Consecuencia:** el audio de ElevenLabs no se puede publicar con CC BY-SA, porque esa licencia permitiría a cualquiera extraer los archivos y redistribuirlos por separado. **Decisión del creador (D-27): todo el audio de ElevenLabs —voces, efectos y música— lleva la licencia cerrada.**

**Licencia de audio de Geoconquista** (`LICENSES/LicenseRef-Geoconquista-Audio.md`, versión 1.0): se permite redistribuir estos archivos, sin modificar, **solo como parte de Geoconquista o de un juego derivado de él** distribuido bajo las licencias del proyecto. No se permite extraerlos para usarlos por separado, ni incluirlos en bibliotecas o colecciones de sonidos, ni usar las voces fuera del juego.

**Comprobación pendiente antes de publicar el primer audio en `assets/`:** leer las condiciones OEM de ElevenLabs, que regulan «bundling, making available and sublicensing», y su política de usos prohibidos. Si exigen algo más, se publica una versión 1.1 de la licencia.

Las aportaciones de audio de la comunidad hechas sin ElevenLabs pueden ir con CC BY-SA 4.0.

### 5. Material generado con IA

- Las imágenes generadas con OpenAI son del usuario según sus condiciones; se publican con CC BY-SA 4.0.
- En varias jurisdicciones lo generado sin suficiente aportación humana podría no tener protección por derechos de autor. La licencia se declara igualmente; las ediciones y composiciones humanas, como el montaje de las cartas o el mapa vectorial, sí la tienen. Cada activo registra en el manifiesto qué parte es generada y qué parte editada (`AGENTS.md` §7).

## Consecuencias

- **Positivas:** las mejoras de la comunidad vuelven al proyecto; un DCO es sencillo para quien aporta; el nombre queda protegido.
- **Negativas:**
  - **App Store del iPad:** las condiciones de Apple chocan con la AGPL. Una vez haya código de la comunidad, publicar en la App Store sería complicado. Google Play no tiene ese problema, y Android es la plataforma principal (D-03).
  - Cualquiera puede distribuir gratis una versión compilada.
  - El audio tiene una licencia distinta del resto del contenido, que hay que explicar en `LICENCIAS.md`.

## Alternativas descartadas

- **MIT y CC BY 4.0:** máxima libertad, pero permiten versiones cerradas que no devuelven nada a la comunidad.
- **GPL-3.0 sin la A:** no obliga a publicar cambios a quien ofrece el juego como servicio en red.
- **CLA:** permitiría cambiar de licencia en el futuro, pero desanima a quien aporta.
