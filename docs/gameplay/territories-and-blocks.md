# Países y bloques

| Campo | Valor |
|---|---|
| ID | FS-003 |
| Estado | **`APROBADO`** por el creador, 2026-11-06 (G1). Provisional para el slice: las cifras se ajustan con el simulador sin nueva aprobación; cambiar una regla exige actualizar este documento y aprobarlo otra vez |
| Fecha | 2026-11-06 |
| Fuentes | R-04 (bloques de 3); D-06 (países reales y actuales); D-12 (24 países en 8 bloques); D-15 (cambio de lista); D-16 (mapa estilizado); plan de arranque DEC-10 y H-03 |
| Aprobación | Creador, 2026-11-06 (G1, D-25) |

## 1. Reglas del mapa

- **24 países jugables en 8 bloques de 3** (D-12). Cada país pertenece a un solo bloque.
- El **resto del mundo** se dibuja en gris y no es jugable: no se compra, no se ocupa y no tiene tropas.
- **Identificadores:** el código de país de Natural Earth (`ADM0_A3`), que coincide con ISO 3166-1 alfa-3 para los 24 países (`MEX`, `TWN`…). Son los IDs estables del motor y de los datos de contenido.
- **Geometría:** Natural Earth, capa *Admin 0 – Countries* a escala 1:50m (dominio público), con sus fronteras por defecto. Francia se representa solo con su territorio europeo. Cisjordania y Gaza se dibujan aparte, en gris (D-15).
- **Mapa estilizado (D-16):** se aplican lupas continuas que agrandan los países jugables pequeños sin romper las fronteras. Europa y Medio Oriente comparten una lupa amplia; Asia oriental tiene otra; Israel y Taiwán llevan dos lupas apiladas cada uno, porque necesitan unas 5 veces de aumento. La versión automática es la base; la definitiva se retoca a mano en vectorial (A1).
- **Sin banderas reales** (`assets/art-direction.md` §7).
- La lista, los bloques y las vecindades son **datos de contenido**, no constantes del código (`AGENTS.md` §6). El borrador está en `exploracion/mapa/territorios-v0.json` y pasará a los datos de contenido después de G3.

## 2. Los 24 países

| Bloque | Países |
|---|---|
| Latinoamérica | México (`MEX`), Brasil (`BRA`), Argentina (`ARG`) |
| Pacífico Norte | Estados Unidos (`USA`), Japón (`JPN`), Taiwán (`TWN`) |
| Europa occidental | Reino Unido (`GBR`), Francia (`FRA`), España (`ESP`) |
| Europa oriental | Alemania (`DEU`), Polonia (`POL`), Rusia (`RUS`) |
| Asia oriental | China (`CHN`), Corea del Norte (`PRK`), Corea del Sur (`KOR`) |
| Medio Oriente | Turquía (`TUR`), Israel (`ISR`), Arabia Saudita (`SAU`) |
| África | Egipto (`EGY`), Nigeria (`NGA`), Sudáfrica (`ZAF`) |
| Asia del Sur | Irán (`IRN`), India (`IND`), Indonesia (`IDN`) |

**Criterios del reparto:** al quitar Canadá, Colombia y Australia y añadir Corea del Norte, Taiwán e Israel (D-15), en América quedaban solo cuatro países, que no forman bloques de 3. Por eso Estados Unidos pasa a un bloque del Pacífico con Japón y Taiwán, y México, Brasil y Argentina forman Latinoamérica. Cada bloque está conectado (sección 3), para que completarlo tenga sentido militar además de económico.

**Quedan fuera** y se dibujan en gris, entre otros: Canadá, Colombia, Australia, Italia y Ucrania.

**Sensibilidad:** la lista incluye países en conflictos activos o de soberanía disputada (Rusia, Israel, Taiwán, Corea del Norte, Irán). Es una decisión del creador (D-06, D-15). Queda registrado para la revisión editorial de los modos, sobre todo `familiar_u18` (P-12), y para los textos del narrador y de las cartas: se nombran países, nunca pueblos, religiones ni líderes reales.

## 3. Vecindades

Dos países son vecinos si existe una vecindad entre ellos. La vecindad decide a qué países se puede atacar y mover tropas. Hay tres tipos:

- **Terrestre:** frontera real.
- **Marítima:** ruta por mar.
- **Corredor:** une dos países jugables a través de países no jugables.

Los tres tipos **solo se distinguen visualmente** y tienen el mismo efecto en las reglas (D-24).

### Dentro de cada bloque

| Bloque | Vecindades |
|---|---|
| Latinoamérica | `MEX`–`BRA` corredor (a través de Centroamérica y Colombia) · `BRA`–`ARG` terrestre (frontera) |
| Pacífico Norte | `USA`–`JPN` marítima (Océano Pacífico) · `JPN`–`TWN` marítima (islas Ryukyu) |
| Europa occidental | `GBR`–`FRA` marítima (Canal de la Mancha) · `FRA`–`ESP` terrestre (frontera) |
| Europa oriental | `DEU`–`POL` terrestre (frontera) · `POL`–`RUS` terrestre (frontera (Kaliningrado)) |
| Asia oriental | `CHN`–`PRK` terrestre (frontera) · `PRK`–`KOR` terrestre (frontera (zona desmilitarizada)) · `CHN`–`KOR` marítima (Mar Amarillo) |
| Medio Oriente | `TUR`–`ISR` marítima (Mediterráneo oriental) · `ISR`–`SAU` corredor (a través de Jordania) · `TUR`–`SAU` corredor (a través de Siria e Irak) |
| África | `EGY`–`NGA` corredor (a través del Sahel) · `NGA`–`ZAF` corredor (a través de África central) |
| Asia del Sur | `IRN`–`IND` corredor (a través de Pakistán) · `IND`–`IDN` marítima (Océano Índico) |

### Entre bloques

| Vecindad | Tipo | Por dónde |
|---|---|---|
| `USA`–`MEX` | Terrestre | frontera |
| `USA`–`GBR` | Marítima | Atlántico Norte |
| `USA`–`RUS` | Marítima | Estrecho de Bering |
| `BRA`–`NGA` | Marítima | Atlántico Sur |
| `ARG`–`ZAF` | Marítima | Atlántico Sur |
| `FRA`–`DEU` | Terrestre | frontera |
| `GBR`–`DEU` | Marítima | Mar del Norte |
| `ESP`–`EGY` | Marítima | Mediterráneo |
| `DEU`–`TUR` | Corredor | a través de los Balcanes |
| `RUS`–`TUR` | Marítima | Mar Negro |
| `RUS`–`IRN` | Marítima | Mar Caspio |
| `RUS`–`CHN` | Terrestre | frontera |
| `RUS`–`PRK` | Terrestre | frontera |
| `EGY`–`ISR` | Terrestre | frontera (Sinaí) |
| `SAU`–`EGY` | Marítima | Mar Rojo |
| `SAU`–`IRN` | Marítima | Golfo Pérsico |
| `TUR`–`IRN` | Terrestre | frontera |
| `CHN`–`IND` | Terrestre | frontera |
| `CHN`–`TWN` | Marítima | Estrecho de Taiwán |
| `KOR`–`JPN` | Marítima | Estrecho de Corea |
| `CHN`–`IDN` | Marítima | Mar de China Meridional |
| `IDN`–`ZAF` | Marítima | Océano Índico |

En total son 40 vecindades, y el grafo está conectado: desde cualquier país se llega a cualquier otro. Vecinos por país:

- **6:** China, Rusia.
- **5:** Turquía.
- **4:** Alemania, Arabia Saudita, Egipto, Estados Unidos, Irán.
- **3:** Brasil, Corea del Norte, Corea del Sur, Francia, India, Indonesia, Israel, Japón, Nigeria, Reino Unido, Sudáfrica.
- **2:** Argentina, España, México, Polonia, Taiwán.

Con 2 vecinos un país es fácil de defender; con 6, difícil. El simulador de E4 medirá si eso desequilibra.

## 4. Lo que este documento no fija

- **Precios, ingresos y aranceles** de cada país: van en `parameters.md`.
- **Posición de los países en el recorrido** y casillas especiales: van en `board-and-map.md`, con las variantes A y B del plan (DEC-10 / §6.2).
- **Movimiento militar:** sigue abierto (plan §8.3). Este documento solo define quién es vecino de quién.

## 5. Preguntas para el creador

1. ~~¿Apruebas el reparto en bloques?~~ Aprobado (D-20).
2. ~~¿Los tipos de vecindad cambian las reglas?~~ No, solo el dibujo (D-24).
