# Dirección de arte

| Campo | Valor |
|---|---|
| Estado | `PROPUESTO`. Dirección **A** (D-11); tablero, cartas y mapa estilizado decididos (D-16, D-19). Falta §9.4 |
| Fecha | 2026-11-05 |
| Fuentes | Visión (pilares 1, 2 y 7); brief §9 y §14; capturas de `Contexto/referencias-visuales/`; plan §4.4 (V-1 a V-13) |

Este documento fija los **criterios** y las **preguntas** de la dirección de arte. Las elecciones concretas (dirección elegida, paleta final y tipografías) se cierran después de la exploración A0, con imágenes reales a la vista.

## 1. Qué tomamos de las capturas y qué no

Las capturas son conceptos generados, no especificaciones (brief §14).

**Se conserva como punto de partida:**
- El tono de «sala de situación» oscura, con océano azul profundo y acentos dorados.
- Los colores saturados sobre fondo oscuro.
- La densidad de información de la tablet, organizada en paneles.
- La sensación de objeto físico: cartas con marco, fichas, tablero con borde.

**Se descarta** (plan §4.4):
- El nombre «Dominio Global» (V-1).
- Los siete bloques continentales (V-2). Los países actuales **sí** se usan (D-06), en bloques de 3.
- Las tropas de todos los jugadores en la tablet (V-4).
- Los botones de poder arbitrario (V-5) y el de «Tirar dados» de la consola (V-6): los dados los lanza el jugador desde su móvil (D-08).
- El logo de WhatsApp (V-10).
- Las cifras decorativas (V-11) y el teclado de dados (V-12), que ya no existe con D-08.

## 2. Problema central de legibilidad: propietario frente a bloque

En las capturas, el mapa se colorea **por continente**. En el juego, lo que importa de un vistazo es **de quién es cada país**, y en segundo lugar a qué bloque pertenece y qué amenaza tiene. Propuesta para validar en A0 y en `ux/public-display.md`:

| Información | Codificación propuesta |
|---|---|
| Propietario | **Relleno** del país con el color del jugador y su símbolo; países libres en un tono neutro (pergamino o gris pizarra) |
| Bloque | **Contorno** común de los tres países, más un emblema del bloque; al completarse, el contorno se enciende con el color del dueño |
| Banda de amenaza | Icono sobre el país con 0 a 3 marcas (milicia, baja, media o alta), nunca un número |
| Ficha en el recorrido | Peón del color y el símbolo del jugador |

## 3. Colores y símbolos de jugador

Seis colores pensados para personas con daltonismo, cada uno con su **símbolo**, porque el color nunca va solo (AC-UX-02). Punto de partida: la paleta de Okabe e Ito, que está diseñada para distinguirse con los tipos comunes de daltonismo. Hay que validarla sobre el fondo oscuro real y simulando cada tipo de daltonismo.

| Jugador | Color candidato | Símbolo candidato |
|---|---|---|
| 1 | Naranja `#E69F00` | Círculo |
| 2 | Azul cielo `#56B4E9` | Triángulo |
| 3 | Verde azulado `#009E73` | Cuadrado |
| 4 | Amarillo `#F0E442` | Estrella |
| 5 | Bermellón `#D55E00` | Rombo |
| 6 | Púrpura rojizo `#CC79A7` | Hexágono |

Para que funcione con mapas de cualquier estilo artístico, el océano y la tierra libre quedan fuera de estos seis tonos.

## 4. Tipografía

Las fuentes deben tener licencia abierta (SIL OFL), ir incluidas en la aplicación sin descargas externas (AC-NET-01) y tener todos los glifos del español.

- **Texto y cifras:** candidata Atkinson Hyperlegible, diseñada para lectores con baja visión. Es lo más importante a 2 m de distancia.
- **Títulos:** una condensada con carácter militar o editorial. Candidatas: Barlow Condensed y Oswald.
- **Logotipo:** «GEOCONQUISTA» como lettering vectorial propio, no como imagen generada. La IA no garantiza letras correctas y el logo debe ser escalable.

## 5. Tres direcciones para explorar en A0

Las tres se prueban con **los mismos tres sujetos** para compararlas en igualdad de condiciones: un fragmento del tablero (6 países del Mediterráneo y 4 casillas del recorrido), la carta «Filtración» del mazo de Correo y el emblema de una potencia.

| Dirección | Descripción | A favor | En contra |
|---|---|---|---|
| **A. Sala de guerra cinematográfica** | Realista y dramática, en la línea de las capturas: texturas de mapa, metal, luz cálida | Impacto inmediato; es la referencia que ya existe | Difícil de mantener coherente en cientos de cartas; detalle que se pierde a 2 m; pesa más en dispositivos modestos |
| **B. Cartel geopolítico** | Ilustración plana de tintas limitadas, estilo serigrafía o cartel de época, con formas fuertes | Muy legible a distancia; coherencia alta entre cartas; archivos ligeros; sirve igual para humor que para tensión | Menos «espectacular» en una captura de pantalla |
| **C. Sátira ilustrada** | Caricatura editorial con humor, personajes y situaciones exageradas | Encaja con los modos party y con Verdad o Reto; da personalidad | Riesgo de caricaturizar pueblos o culturas (brief §6.2); puede chocar con la tensión de la guerra |

**Decisión del creador (D-11, 2026-11-06): A para todo el juego.** B y C se descartan.

Para que A funcione hay que contener sus tres riesgos:
- **Legibilidad a 2 m.** El fondo (escritorio, metal, luz) es generado, pero el mapa se dibuja encima en vectorial, con rellenos de jugador planos y saturados. El relieve y la textura del mapa van a baja intensidad para que no compitan con los colores de propiedad. La ronda 2 de A0 lo prueba.
- **Coherencia en cientos de cartas.** Se fija un prompt de estilo y un juego de imágenes de referencia aprobadas. Para A2 se valora entrenar un estilo propio en Replicate.
- **Rendimiento.** Fondos y cartas en WebP o AVIF, a la resolución de cada pantalla. La luz y las partículas animadas se miden en la Pi 5 (S2).

## 6. Qué se genera con IA y qué se construye

| Pieza | Método | Motivo |
|---|---|---|
| Geometría del mapa (países jugables y adyacencias, D-06) | **Construida** en vectorial a partir de Natural Earth (dominio público), con lupas que agrandan los países pequeños (D-16) y retoque manual final | Exige precisión y debe coincidir con los datos del motor |
| Iconos de interfaz, casillas, bandas de amenaza y caras de los dados | **Construidos** en SVG | Nitidez a cualquier tamaño, coherencia y peso mínimo |
| Logotipo y lettering | **Construidos** en vectorial | Las letras generadas no son fiables |
| Texturas del mapa, del océano y del marco | Generadas y editadas | Riqueza visual de fondo |
| Ilustraciones de cartas, eventos y fondos del lobby | Generadas y editadas | Volumen alto con coherencia de estilo |
| Emblemas de potencias | Generados como base y redibujados en vectorial | Deben leerse muy pequeños |

## 7. Límites de contenido visual

- No se usan banderas reales, escudos oficiales ni rostros de líderes políticos reales. Confirmado con D-12: tampoco con países reales.
- No se usan logos ni marcas de terceros (WhatsApp, Monopoly, Risk) ni el estilo de un artista vivo identificable.
- No se usan estereotipos étnicos, religiosos ni nacionales.
- El arte de `familiar_u18` es apto para menores. El tono visual de los modos +18 depende de P-04 y P-12 y queda `PENDIENTE`.

## 8. Presupuestos técnicos (provisionales hasta S1 y S2)

- **Móvil:** el arte de la vista de jugador cuenta dentro de la meta de ≤ 5 MB de transferencia inicial (DEC-04). Las ilustraciones se cargan solo cuando se van a mostrar.
- **Tablero:** se sirve en local, así que admite más peso, pero debe mantener la fluidez en la Pi 5 (AC-HW-01).
- **Formatos candidatos:** SVG para vectores; WebP o AVIF para ilustraciones, con tamaños por densidad de pantalla. Se confirman en S1.

## 9. Preguntas para cerrar A0

1. ~~¿Qué dirección se adopta?~~ A (D-11).
2. ~~¿Objeto físico o interfaz plana?~~ Objeto físico: mesa de guerra con marco de latón; el mapa vectorial va encima (D-19).
3. ~~¿Ilustración a página completa o viñeta?~~ Página completa con el texto encima, como «Filtración» (D-19).
4. ¿Cuánto cambia el arte entre `familiar_u18` y los modos +18?
