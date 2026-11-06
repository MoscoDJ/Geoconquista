# Idiomas del juego

| Campo | Valor |
|---|---|
| ID | FS-009 |
| Estado | `PROPUESTO` |
| Fecha | 2026-11-06 |
| Fuentes | D-28 (juego bilingüe); D-30 (nativo en español; textos en los dos idiomas; voces e imágenes con texto en inglés, de la comunidad); D-17 (narrador); `AGENTS.md` §6 (textos en contenido estructurado) |
| Aprobación | Pendiente del creador |

**Geoconquista es un juego nativo en español** (D-30). El proyecto produce **todos los textos en español y en inglés**. Las **voces y las imágenes con texto** se producen solo en español; sus versiones en inglés las aporta la comunidad.

## 1. Idiomas

| Idioma | Papel | Quién lo produce |
|---|---|---|
| `es` (español) | Idioma nativo y de referencia | El proyecto: textos, voces e imágenes |
| `en` (inglés) | Idioma completo en textos | El proyecto, los textos. La comunidad, las voces y las imágenes con texto |

- El idioma **nunca** cambia las reglas, las cifras ni el estado de la partida: solo cómo se presentan.
- Se podrán añadir otros idiomas si la comunidad los aporta, incluidos sus textos.

## 2. Cuándo se ofrece un idioma

- **Textos:** español e inglés están siempre completos, porque el proyecto mantiene los dos. Todo texto nuevo se escribe en los dos idiomas en el mismo cambio. Un idioma aportado por la comunidad solo aparece como opción si su **paquete de textos está completo**: interfaz, casillas, mazos y las cartas de los modos que se van a jugar.
- **Audio e imágenes:** pueden faltar. Lo que no tenga versión en ese idioma usa la española (§4 y §5).

## 3. Idioma de cada superficie

| Superficie | Idioma | Quién lo elige |
|---|---|---|
| Tablero público, consola y narrador | El **idioma de la sala** | Quien crea la sala. Se puede cambiar en el lobby, antes de empezar |
| Móvil de cada jugador | El **suyo** | Cada jugador, en su móvil. Por defecto, el del navegador si está disponible; si no, el de la sala |

Así, en una mesa mixta, lo público sale en un idioma y cada persona lee lo privado en el suyo.

## 4. Textos y contenido

- **Interfaz:** todos los textos visibles viven en catálogos por idioma, nunca escritos en el código.
- **Contenido estructurado** (cartas, retos, nombres de mazos y casillas): cada texto tiene una entrada por idioma. El español y el inglés son obligatorios; los demás, opcionales.
- **Verdad o Reto** se adapta culturalmente, no se traduce palabra por palabra. Cada idioma tiene su propia revisión editorial (P-12).
- **Países:** el ID es el código ISO (`MEX`) en todos los idiomas; el nombre se traduce («México» / «Mexico»).
- **Potencias:** el nombre fijo de cada color se traduce («Potencia Ámbar» / «Amber Power»).
- **«Geoconquista» no se traduce.**
- **Números:** formato por idioma (separador de miles y decimales).

## 5. Narrador y audio

- El proyecto solo produce **voces en español**: El Faraón (D-17, D-30).
- Si la comunidad aporta un **catálogo de frases del narrador en otro idioma**, se usa en las salas de ese idioma. Si no existe, o le falta una frase, **suena la frase en español**.
- Los efectos y la música no dependen del idioma.
- El audio aportado por la comunidad se publica con CC BY-SA 4.0 si no se generó con ElevenLabs, o con la licencia de audio de Geoconquista si sí (ADR-003).

## 6. Arte

- Las ilustraciones no llevan texto (`assets/pipeline.md` §3): las cartas y la interfaz se componen en cada idioma sobre la misma imagen.
- Las **imágenes que sí llevan texto** (logotipo, lettering, algunos fondos) se producen **en español**. Si la comunidad aporta la versión en otro idioma, se usa; si no, se muestra la española.

## 7. Criterios de aceptación

- **AC-009.1:** con la misma semilla y los mismos comandos, una partida con sala en `es` y otra en `en` dan exactamente el mismo estado.
- **AC-009.2:** un jugador con el móvil en `en` en una sala `es` ve sus textos privados en inglés, y el tablero sigue en español.
- **AC-009.3:** la validación de contenido rechaza una carta, casilla o texto de interfaz sin entrada en español o en inglés, e indica cuál falta. Un idioma de la comunidad al que le falte una entrada no aparece como opción.
- **AC-009.4:** en una sala en inglés sin catálogo de narrador en inglés, el narrador dice la frase en español.
- **AC-009.5:** ningún texto visible de la interfaz está escrito directamente en el código: una prueba recorre las pantallas y no encuentra claves sin traducir en ningún idioma ofrecido.

## 8. Preguntas para el creador

1. ¿Te parece bien el reparto: idioma de sala para lo público e idioma propio en cada móvil?
2. ~~¿Exploramos voces en inglés?~~ No: solo voces en español; las demás las aporta la comunidad (D-30).
