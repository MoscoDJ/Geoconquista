# Economía

| Campo | Valor |
|---|---|
| ID | FS-004 |
| Estado | `PROPUESTO` (reglas v0, E1) |
| Fecha | 2026-11-06 |
| Fuentes | Plan de arranque H-03, H-04, §4.3 y §6.3 (matriz de revelaciones); D-07; observación 2 de la revisión del 2026-11-04 |
| Aprobación | Pendiente del creador, en G1 |

## 1. Tesorería

- La tesorería (el efectivo) de cada jugador es **privada** (D-07): solo la ve su dueño.
- Son **públicos** los países de cada uno, sus bloques y su ingreso territorial base.
- La tesorería nunca es negativa. No hay deuda.

## 2. Ingreso y mantenimiento (fase 1 del turno)

Al inicio de su turno, cada jugador cobra:

> `ingreso_base` + `ingreso_por_pais` × (países propios) − mantenimiento

- **Mantenimiento:** `mantenimiento_por_tropa` por cada tropa real a partir de la tercera (`tropas_sin_mantenimiento` = 2).
- **Si no alcanza para el mantenimiento:** se cobra hasta dejar el efectivo en 0 y se desmovilizan las tropas no cubiertas, de una en una, siempre del país propio que tenga más tropas en ese momento; en empate, el de menor código de país en orden alfabético.
- **Qué se publica:** el ingreso territorial base (`ingreso_base` + `ingreso_por_pais` × países). El mantenimiento y el desglose solo los ve el dueño. Una desmovilización forzosa solo se nota si cambia una banda de amenaza.

## 3. Compra (fase 4)

- Al caer en un **país libre**, el jugador puede comprarlo pagando su precio (`parameters.md` §2). No hay subasta: si no lo compra, sigue libre.
- El país comprado pasa a su color y solo tiene la milicia (`armies-and-fog-of-war.md` §1).

## 4. Arancel (fase 4)

- Al caer en un **país ajeno**, el jugador paga el arancel de ese país a su dueño. El dueño puede perdonarlo desde su móvil.
- **Si no le alcanza:** paga lo que tiene, hasta 0, y **el banco completa el arancel** al dueño.
  - Así el acreedor siempre cobra el importe completo y no puede deducir el saldo del deudor.
  - Lo que se publica es «pago parcial por insolvencia», que revela que el deudor quedó en 0. Es la única fuga aceptada.
  - Esto corrige la observación 2 de la revisión del 2026-11-04. El dinero que inyecta el banco lo mide el simulador.

## 5. Comercio bilateral (fase 5)

En su fase 5, el jugador en turno puede ejecutar **un** acuerdo con otro jugador: compraventa o intercambio de países, con o sin dinero.

- Solo se entregan países **sin tropas reales** y sin combate pendiente. El dueño puede desmovilizar sus tropas en el mismo acuerdo, sin reembolso.
- Ningún acuerdo puede dejar a un firmante sin países.
- Ambos firmantes aceptan los mismos términos en su móvil. Se valida todo antes de aplicar nada; si algo falla, no cambia nada, ni siquiera las tropas que se iban a desmovilizar.
- El mensaje de error es genérico y no revela si faltó saldo.
- Todo país transferido queda bloqueado para nuevo comercio durante una vuelta completa de turnos ($t+P$, plan §6.2).
- **Revelaciones:** el público ve los países que cambian de manos y que hubo acuerdo. El dinero solo lo ven los firmantes (`partes_tratado`).
- Un jugador sin países (asilado, `victory-and-endgame.md` §3) **sí** puede comprar un país por comercio: el límite de «no dejar a nadie sin países» protege al que vende.

## 6. Criterios de aceptación

- **AC-004.1:** un jugador con 3 países, 4 tropas y 7 de efectivo cobra al inicio de su turno 10 + 15 − 4 = 21 y termina con 28.
- **AC-004.2:** un jugador con 0 de efectivo, 2 países y 14 tropas (8 en `BRA`, 6 en `ARG`) cobra 20 y debe 24 de mantenimiento. Paga 20, queda en 0 y desmoviliza las 2 tropas no cubiertas. Las dos salen de `BRA`, el país con más tropas en cada momento, que queda con 6.
- **AC-004.3:** un jugador con 4 de efectivo que cae en un país con arancel 10 queda en 0. El dueño recibe 10. El público ve «pago parcial por insolvencia».
- **AC-004.4:** un acuerdo que entregaría un país con tropas, sin autorizar su desmovilización, se rechaza sin cambiar nada.
- **AC-004.5:** un acuerdo que dejaría al vendedor sin países se rechaza.
- **AC-004.6:** un país comprado por comercio en el turno global $t$ con 4 jugadores no puede volver a comerciarse antes del turno $t+4$.
- **AC-004.7:** ninguna vista que no sea la del dueño contiene su efectivo exacto.

## 7. Preguntas para el creador

1. ¿Te parece bien que el banco complete el arancel cuando el deudor no puede pagarlo? Es lo que evita revelar saldos.
2. ¿Perdonar un arancel debe ser libre, como propone el plan, o tener algún coste?
