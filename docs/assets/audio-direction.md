# Dirección de audio

| Campo | Valor |
|---|---|
| Estado | `PROPUESTO`. Música híbrida (D-18), narrador El Faraón (D-17) y efectos de exploración elegidos (D-21, D-23) |
| Fecha | 2026-11-05 |
| Fuentes | Visión (pilares 1, 5 y 7); brief §4.3 (fases narrativas) y §9.4 |

## 1. Principio: el sonido acompaña a la mesa, no la tapa

La partida es una conversación: se negocia, se discute y se ríe. El audio da peso a los momentos importantes y se aparta durante la conversación.

- El sonido sale **sobre todo del tablero**, por los altavoces de la pantalla conectada al host. Es el mismo sonido para todos y no revela nada privado.
- Los **móviles van en silencio por defecto**. Como mucho, una vibración o un aviso breve cuando es tu turno o cuando te llega algo privado. Un sonido en el móvil de un jugador revelaría a la mesa que recibió algo (pilar 2).
- La **tablet** suena cuando caen los dados (D-08), porque la tirada es pública. Para el resto solo da respuesta táctil y sonora a sus propias pulsaciones, a volumen bajo.
- Lanzar los dados (deslizar el dedo) es un gesto público, así que ese móvil puede dar una vibración breve al lanzar. Sigue sin sonar para nada privado.

## 2. Música adaptativa por fase

El brief describe tres etapas de experiencia: expansión, consolidación y crisis mundial. La propuesta es una pieza por etapa, construida en **capas (stems)** que se suman según la tensión de la partida, en lugar de cortes bruscos entre temas.

| Momento | Carácter | Capas |
|---|---|---|
| Lobby | Invitación, misterio, «se abre la sala de situación» | Tema único en bucle |
| Expansión | Curiosidad, optimismo, mercados | Base + melodía |
| Consolidación | Tensión diplomática, primeros choques | + percusión y un bajo más insistente |
| Crisis mundial | Urgencia, tambores, metales | + capa de percusión de guerra |
| Victoria | Resolución | Fanfarria corta y tema final |

Reglas: la música queda **por debajo** de los efectos y de la voz y se atenúa automáticamente cuando suena una voz. Hay un control de volumen independiente para música, efectos y voz. Volumen por defecto moderado, porque la mesa habla encima.

## 3. Efectos de sonido

Cada evento público con peso tiene su firma sonora: compra de país, bloque completo, cambio de banda de amenaza («algo se movió»), declaración de ataque, resultado de combate (victoria del atacante o defensa), conquista, tratado firmado, tratado roto, fin de ronda y fin de partida.

Cada uno de los cinco mazos tiene su propia firma al robar una carta (Hacienda, Migración, Correo, Mensajería y Verdad o Reto), para que la mesa sepa qué viene antes de leerlo.

**Restricción de privacidad:** un efecto no puede revelar información privada. Por ejemplo, no puede sonar distinto al reclutar 1 tropa que 5, ni sonar en el tablero cuando un jugador hace una acción privada que no cambia nada público.

## 4. Voces

Un **narrador** o «locutor de noticias internacionales» anuncia los eventos públicos.

- **Restricción del modo sin Internet:** no se puede generar voz durante la partida. Todas las frases se generan antes y se incluyen en la aplicación.
- **Consecuencia:** el narrador no puede decir el nombre libre que escribió cada jugador. Hay dos opciones:
  - (a) frases genéricas («¡Una potencia ha completado un bloque!»);
  - (b) un catálogo fijo de nombres de potencia ligados al color o al emblema (por ejemplo, «la Potencia Ámbar»), combinado con segmentos pregrabados: potencia + acción + región. Con 6 potencias y 24 regiones el catálogo es manejable.

  Recomendación: (b) para las acciones principales y (a) para el resto. Para esto los nombres de potencia tienen que ser contenido fijo, y eso se decide en `ux/lobby.md`.
- **Voz (D-17):** «El Faraón – Powerful and Mysterious», español latinoamericano, grave y épico (ElevenLabs, voz de biblioteca `Rl2JPHsuEWSfwCD4ZHIQ`, modelo `eleven_v4`). Es la misma voz en todos los modos; el tono puede ser más teatral en los modos party si el texto lo pide.
- **Licencia:** es una voz de la biblioteca compartida de ElevenLabs, generada con plan Pro (uso comercial). Si su autor la retira de la biblioteca, los audios ya generados siguen siendo utilizables, pero no se podrían generar frases nuevas con ella. Por eso el catálogo de frases se genera completo de una vez, cuando esté cerrado.

## 5. Exploración A0

- **Música (decidido, D-18): híbrida.** Se exploraron dos direcciones:
  - **Orquestal cinematográfico:** cuerdas, metales y percusión de guerra.
  - **Electrónico de sala de situación:** sintetizadores, pulsos y tensión de thriller.
- **Efectos:** una tanda de 5 efectos clave (compra, bloque, ataque, conquista, robo de carta) en ambas direcciones.
- **Voz:** 3 voces candidatas leyendo las mismas 5 frases.

## 6. Requisitos técnicos (provisionales hasta S1 y S2)

- **Sonoridad normalizada:** todas las pistas se igualan a un mismo nivel percibido para que ningún efecto «grite». Valor objetivo por fijar en A1.
- **Bucles sin cortes** en la música. Los efectos duran menos de 2 s, salvo los de los grandes eventos.
- **Formato** compatible con Chromium en la Pi y con Safari en iOS. Se confirma en S1 y S2.
- **Sin dependencias externas:** todos los archivos se sirven desde el host.

## 7. Limitación del proceso

El agente que genera el audio **no puede escucharlo**. Puede medir el nivel, la duración, los silencios, los cortes en los bucles y el espectro, y organizar y comparar variantes. Pero la elección de qué suena bien la hace **el creador**, en una página de revisión local con todas las variantes (`docs/assets/pipeline.md` §4).
