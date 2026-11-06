# Pipeline de activos: herramientas, flujo y licencias

| Campo | Valor |
|---|---|
| Estado | `PROPUESTO` |
| Fecha | 2026-11-05 |
| Fuentes | D-04; ADR-000 §10 y §11; dirección de arte y de audio |

## 1. Herramientas

| Necesidad | Herramienta | Uso previsto |
|---|---|---|
| Generación de imagen | OpenAI, modelo por defecto `gpt-image-2.6-sunburst` | Ilustraciones y variantes; edición con máscara |
| Generación de imagen | Google AI Studio (Gemini / Imagen) | Ilustraciones y edición conversacional con referencias |
| Modelos abiertos | Replicate | Modelos de imagen abiertos, entrenamiento de un estilo propio (LoRA) cuando haya cientos de cartas, eliminación de fondo y escalado |
| Escalado y detalle | Magnific | Escalado de las piezas finales del tablero y de los eventos grandes |
| Música, efectos y voces | ElevenLabs (API o MCP) | Música por capas, efectos y narrador |
| Edición raster | ImageMagick, GIMP, Python (Pillow) | Recorte, composición, color, plantillas de carta, hojas de sprites y optimización |
| Vectorial | Inkscape, SVG escrito a mano, `rsvg-convert` | Mapa, iconos, logotipo y emblemas redibujados |
| Audio | ffmpeg, sox | Normalización, cortes, bucles, fundidos y conversión de formato |
| Datos geográficos | Natural Earth (dominio público) | Geometría base del mapa de 24 regiones |

Los identificadores exactos de modelo y sus versiones se anotan en cada entrada del manifiesto, no aquí, porque cambian con frecuencia.

## 2. Accesos

Las claves van en `.env`, en la raíz del repositorio. Al 2026-11-05 hay acceso a **OpenAI** y **ElevenLabs** (variables `OPENAI` y `ELEVENLABS`). Google AI Studio, Replicate y Magnific se añaden cuando hagan falta. Está ignorado por git, y su plantilla es `.env.example`. Nunca se escriben en documentos, prompts guardados ni commits. Los scripts de generación leen `.env` y fallan con un mensaje claro si falta una clave.

## 3. Flujo de un activo

```text
necesidad escrita (UX o contenido)
  → ficha de activo (templates/asset-brief.md)
  → variantes en exploracion/<línea>/<activo>/   (ignorado por git)
  → revisión del creador en la página local de comparación
  → edición final + optimización
  → assets/<ruta>  +  entrada en assets/manifest.json
```

- **Coherencia de estilo:** cada línea visual tiene un «prompt de estilo» fijo e imágenes de referencia aprobadas, que se reutilizan en todas las generaciones. Si el volumen lo justifica (los mazos de A2), se entrena un estilo propio en Replicate con las piezas aprobadas.
- **Nada sale de la IA sin edición:** se revisan las manos y los textos falsos, se corrige el color con la paleta y se recorta al formato y al peso que pide su destino.
- **Texto dentro de imágenes:** nunca se genera. Los textos de cartas y de la interfaz se componen encima con las fuentes del proyecto. Así se pueden traducir, son legibles y no hay faltas de ortografía generadas.

## 4. Revisión por el creador

Cada tanda de exploración produce una página HTML local en `exploracion/` que muestra las variantes una al lado de la otra, con reproductores para el audio y la información de cada una. El creador marca qué se aprueba y qué se descarta. Solo lo aprobado avanza.

## 5. Manifiesto (`assets/manifest.json`)

Cada activo de `assets/` tiene una entrada con:

| Campo | Contenido |
|---|---|
| `id`, `ruta`, `tipo` | Identificador estable, ruta del archivo e imagen, vector, música, efecto o voz |
| `requerido_por` | Documento de UX o de contenido que lo pide |
| `origen` | `construido`, `generado` o `mixto` |
| `herramienta`, `modelo`, `fecha` | Con qué se generó y cuándo |
| `prompt`, `referencias`, `semilla` | Lo necesario para reproducirlo o regenerarlo |
| `ediciones` | Pasos posteriores (escalado, recorte, retoque, normalización) |
| `terminos` | Términos de uso del proveedor y del plan de cuenta en la fecha de generación |
| `aprobado_por`, `fecha_aprobacion` | Creador y fecha |

## 6. Licencias (D-26, ADR-003)

Las licencias están decididas en ADR-003: CC BY-SA 4.0 para imágenes y composiciones, y la licencia cerrada `LicenseRef-Geoconquista-Audio` (D-27) para todo lo generado con ElevenLabs, porque sus condiciones no permiten distribuir los efectos por separado. El campo `terminos` del manifiesto registra además la licencia de cada activo.

### Puntos que siguen abiertos

Antes de publicar (E7) hay que verificar, con los términos vigentes y el plan de cada cuenta, tres cosas:

1. **Uso comercial y redistribución.** Si cada proveedor permite distribuir sus salidas dentro de un proyecto open source. En algunos servicios, como ElevenLabs, depende del plan contratado.
2. **Licencia que se puede declarar.** En varias jurisdicciones, el material generado sin suficiente aportación humana podría no tener protección por derechos de autor. Eso afecta a la licencia que se puede declarar sobre el contenido (por ejemplo, CC BY-SA). `[PEND: revisar antes de E7]`
3. **Material de terceros.** Que ninguna referencia usada en un prompt o como imagen de entrada sea material protegido de terceros.

Por eso el manifiesto registra los términos **en la fecha de generación**.

## 7. Costes

Cada generación tiene un coste. Durante A0 las tandas son pequeñas: pocas variantes por sujeto, y se amplía solo la dirección que promete. Se lleva un registro aproximado del gasto por tanda en `exploracion/costes.md`, para que el creador vea en qué se va el dinero.
