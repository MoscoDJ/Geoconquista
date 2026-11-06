# Visión de producto

| Campo | Valor |
|---|---|
| Estado | `APROBADO` por el creador, 2026-11-05 (G0). Actualizado con D-06 a D-09 (2026-11-05) y D-11 a D-13, D-28 y D-30 (2026-11-06) |
| Fecha | 2026-11-05 |
| Fuentes | Brief del creador (`Contexto/GEOCONQUISTA_BRIEF_DEBATE.md` §2, §3.1 y §20); plan de arranque §1–§3 |

## Qué es

**Geoconquista** es un juego social de estrategia geopolítica para jugar en persona, alrededor de una mesa. Cada jugador desarrolla una potencia: compra países, completa bloques regionales, recluta ejércitos secretos, invade, negocia, espía y enfrenta eventos imprevisibles.

Es un juego **híbrido**. Las conversaciones son cara a cara y los dados se lanzan con un gesto: el jugador desliza el dedo en su móvil y los dados caen en la tablet, a la vista de la mesa (D-08, D-13). Una pantalla grande muestra el tablero, una tablet hace de consola de mesa y cada jugador tiene en su móvil la información privada de su potencia. La tecnología calcula, guarda los secretos y pone el espectáculo; **no reemplaza la mesa**.

## Para quién

- Grupos de **3 a 6 personas** (hipótesis por validar) reunidas en casa, en partidas de 90 a 120 minutos.
- Familias, con contenido apto para menores (`familiar_u18`), y grupos de adultos con cuatro intensidades sociales: `familiar_18`, `party_18`, `party_extreme_18` y `parejas_18`.
- Personas que no quieren instalar nada: entran escaneando un QR.

## Pilares

1. **La mesa manda.** La negociación es en voz alta, los dados caen en la tablet en el centro de la mesa y el móvil se mira solo para consultar secretos, confirmar acciones y lanzar los dados.
2. **El secreto militar es real.** Nadie conoce las tropas exactas de un rival: ni la pantalla, ni la consola, ni los rankings, ni los registros, ni lo que se puede deducir de los gastos. Solo el espionaje revela cifras, y solo a quien espía.
3. **La diplomacia pesa tanto como la guerra.** Hay tratados formales que el motor hace cumplir, traición con consecuencias y varias formas de ganar.
4. **El azar está acotado.** Los dados emocionan sin decidir solos: combate con probabilidades auditables, comercio para desatascar bloques y reglas para quien se queda atrás.
5. **Funciona sin Internet.** Todo corre en la red local del anfitrión: sin cuentas, sin nube y sin dependencias ocultas.
6. **Contenido seguro por modo.** Siempre se puede pasar una verdad o un reto. Ningún reto exige daño, alcohol obligatorio ni contacto no consentido.
7. **Calidad de producción** (D-04). Arte, sonido y animación a la altura de un juego comercial, pensados para leerse a 2 m de distancia y para rendir en una Raspberry Pi y en móviles modestos.

## Superficies

| Superficie | Dispositivo | Qué hace | Qué nunca hace |
|---|---|---|---|
| Tablero público (`/tablero`) | Pantalla grande conectada por HDMI al host (Raspberry Pi 5 o laptop) | Recorrido, mapa de países reales (D-06), propietarios, bandas de amenaza, eventos, espectáculo y sonido | Mostrar tropas exactas, saldos privados o cartas privadas |
| Consola de mesa (`/consola`) | Tablet: app Android como plataforma principal (D-02, D-03) o navegador | Mostrar la caída de los dados, resolver casillas, mostrar cartas públicas, pausar | Ver secretos o ejecutar comandos arbitrarios del tipo «dar dinero» |
| Móvil privado (`/jugador`) | Navegador del móvil de cada jugador, desde un QR (D-02) | Dinero, países, tropas propias, cartas, tratados y gráficos públicos; confirmar acciones; lanzar los dados | Recibir datos privados de rivales o decidir el resultado de los dados: lo decide el host |

## Requisitos del creador

Son los R-01 a R-14 del plan de arranque §4.1. El creador modificó R-03 con D-08. Los más visibles:

- El nombre es Geoconquista. Las capturas dicen «Dominio Global», y ese nombre no se usa.
- Dados virtuales: el jugador desliza el dedo en su móvil y los dados caen en la tablet (D-08 y D-13, sustituye a los dados reales del brief). El resultado lo genera el host.
- Mapa de países reales y actuales (D-06).
- Tesorería privada (D-07).
- Países agrupados en bloques de tres; completar un bloque permite formar ejércitos.
- Ejércitos ocultos a los rivales.
- Casillas de Hacienda, Migración, Correo electrónico, Mensajería y Verdad o Reto. «WhatsApp» queda solo como referencia temática interna, sin su nombre ni su logo en pantalla (P-05).
- Cinco modos con el mismo núcleo.
- Nativo en español, con todos los textos también en inglés; las voces y las imágenes con texto en inglés las aporta la comunidad (D-28, D-30, `localization.md`).
- Open source y *Documentation First*.

## Metas de experiencia

Son los criterios CE-01 a CE-09 del plan de arranque §2.2. Los tres que definen el éxito del producto:

- **CE-01:** una partida dura entre 90 y 120 minutos con 3 o 4 jugadores.
- **CE-03:** menos del 30 % de los jugadores siente que miró el móvil más de lo que quería.
- **CE-04:** cero exposiciones no autorizadas de tropas rivales.

## Fuera de alcance del MVP

Juego en línea y cuentas; WhatsApp real; apps en tiendas para los jugadores; varios mapas o clases de unidades; tiempo real; IA rival jugable; kit físico extenso; idiomas distintos del español y el inglés; y cualquier servicio generativo en tiempo de partida, porque rompería el modo sin Internet. El detalle está en el plan de arranque §3.2.

## Preguntas abiertas que afectan a la visión

- **P-04:** ¿Parejas +18 se juega en duplas o de forma individual?
- **P-10:** respondida con D-26 (ADR-003).
