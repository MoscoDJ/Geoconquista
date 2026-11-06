# Economía

| Campo | Valor |
|---|---|
| ID | FS-004 |
| Estado | **`APROBADO`** por el creador, 2026-11-06 (G1). Provisional para el slice: las cifras se ajustan con el simulador sin nueva aprobación; cambiar una regla exige actualizar este documento y aprobarlo otra vez |
| Fecha | 2026-11-06 |
| Fuentes | Plan de arranque H-03, H-04, §4.3 y §6.3 (matriz de revelaciones); D-07; D-24 (hipoteca y venta en lugar de que el banco complete pagos) |
| Aprobación | Creador, 2026-11-06 (G1, D-25) |

## 1. Tesorería

- La tesorería (el efectivo) de cada jugador es **privada** (D-07): solo la ve su dueño.
- Son **públicos** los países de cada uno, sus bloques y su ingreso territorial base.
- La tesorería nunca es negativa. No hay deuda.
- **El banco nunca pone dinero para cubrir el pago de un jugador** (D-24). Quien no puede pagar hipoteca o vende (§5); si aun así no alcanza, quiebra (§6).

## 2. Ingreso y mantenimiento (fase 1 del turno)

Al inicio de su turno, cada jugador cobra:

> `ingreso_base` + `ingreso_por_pais` × (países propios **sin hipoteca**) − mantenimiento

- **Mantenimiento:** `mantenimiento_por_tropa` por cada tropa real a partir de la tercera (`tropas_sin_mantenimiento` = 2).
- **Si no alcanza para el mantenimiento:** se cobra hasta dejar el efectivo en 0 y las tropas no cubiertas se disuelven, porque no hay con qué pagarlas. No interviene el banco. Se desmovilizan de una en una, siempre del país propio que tenga más tropas en ese momento; en empate, el de menor código de país en orden alfabético.
- **Qué se publica:** el ingreso territorial base (`ingreso_base` + `ingreso_por_pais` × países sin hipoteca). El mantenimiento y el desglose solo los ve el dueño. Una desmovilización forzosa solo se nota si cambia una banda de amenaza.

## 3. Compra (fase 4)

- Al caer en un **país libre**, el jugador puede comprarlo pagando su precio (`parameters.md` §2). No hay subasta: si no lo compra, sigue libre.
- El país comprado pasa a su color y solo tiene la milicia (`armies-and-fog-of-war.md` §1).

## 4. Arancel (fase 4)

- Al caer en un **país ajeno sin hipoteca**, el jugador paga el arancel de ese país a su dueño. El dueño puede perdonarlo desde su móvil, sin coste. Que lo perdonó es público.
- Un país **hipotecado** no cobra arancel.
- **Si no le alcanza el efectivo:** antes de pagar debe reunir el dinero hipotecando o vendiendo (§5). Si ni así alcanza, quiebra (§6).
- El acreedor siempre recibe exactamente lo que paga el deudor. Así no puede deducir su saldo, salvo en una quiebra.

## 5. Hipotecar y vender para pagar

### 5.1 Hipoteca

- El jugador puede **hipotecar** un país propio al banco y recibe su valor de hipoteca (`parameters.md` §2: la mitad del precio, redondeando hacia arriba).
- Puede hacerlo **cuando quiera durante su fase 5**, o **cuando tenga que pagar** algo que no cubre su efectivo. Que también se pueda hipotecar por gusto hace que una hipoteca no demuestre que el jugador no tenía dinero.
- **Un país hipotecado** sigue siendo de su dueño: cuenta para los bloques completos, para la victoria y para el recuento de países, y conserva sus tropas. Pero:
  - no da ingreso por país (§2) ni cobra arancel (§4);
  - mientras un bloque tenga algún país hipotecado, ese bloque **no permite reclutar** (`armies-and-fog-of-war.md` §2).
- **Levantar la hipoteca:** en su fase 5, el dueño paga al banco el valor de hipoteca más un 10 % (`parameters.md` §2). Hipotecar y levantar hipotecas no gastan la acción estratégica.
- Si un país hipotecado cambia de dueño (por comercio o conquista), **la hipoteca pasa al nuevo dueño**.
- La hipoteca es pública: el país se muestra hipotecado.

### 5.2 Venta de emergencia

- Cuando tiene que pagar y no le alcanza, el jugador también puede **vender** un país a otro jugador, en cualquier momento del pago y aunque no sea su fase 5.
- Sigue las reglas del comercio (§7): los dos aceptan los mismos términos, el país se entrega sin tropas (el vendedor puede desmovilizarlas) y no se puede vender el último país.
- No cuenta para el límite de un acuerdo por turno.

## 6. Quiebra

Un jugador quiebra cuando tiene que pagar a otro jugador y, después de hipotecar todo lo que puede y sin ninguna venta aceptada, su efectivo no alcanza.

- Paga al acreedor **todo su efectivo**.
- **Todos sus países pasan al acreedor**, con sus hipotecas. Sus tropas se disuelven, así que los países llegan al acreedor con la milicia.
- La parte de la deuda que no se cubre se pierde. **El banco no la completa.**
- Al quedarse sin países, el jugador pierde su gobierno y pide asilo o queda eliminado (`victory-and-endgame.md` §3).
- **Revelaciones:** la quiebra es pública. El acreedor sabe cuánto efectivo recibió, es decir, el saldo exacto del deudor en ese momento. Se acepta, porque el deudor sale del mapa.

## 7. Comercio bilateral (fase 5)

En su fase 5, el jugador en turno puede ejecutar **un** acuerdo con otro jugador: compraventa o intercambio de países, con o sin dinero.

- Solo se entregan países **sin tropas reales** y sin combate pendiente. El dueño puede desmovilizar sus tropas en el mismo acuerdo, sin reembolso.
- Ningún acuerdo puede dejar a un firmante sin países.
- Ambos firmantes aceptan los mismos términos en su móvil. Se valida todo antes de aplicar nada; si algo falla, no cambia nada, ni siquiera las tropas que se iban a desmovilizar.
- El mensaje de error es genérico y no revela si faltó saldo.
- Todo país transferido queda bloqueado para nuevo comercio durante una vuelta completa de turnos ($t+P$, plan §6.2).
- **Revelaciones:** el público ve los países que cambian de manos y que hubo acuerdo. El dinero solo lo ven los firmantes (`partes_tratado`).
- Un jugador sin países (asilado, `victory-and-endgame.md` §3) **sí** puede comprar un país por comercio: el límite de «no dejar a nadie sin países» protege al que vende.

## 8. Criterios de aceptación

- **AC-004.1:** un jugador con 3 países, 4 tropas y 7 de efectivo cobra al inicio de su turno 10 + 15 − 4 = 21 y termina con 28.
- **AC-004.2:** un jugador con 0 de efectivo, 2 países y 14 tropas (8 en `BRA`, 6 en `ARG`) cobra 20 y debe 24 de mantenimiento. Paga 20, queda en 0 y desmoviliza las 2 tropas no cubiertas. Las dos salen de `BRA`, el país con más tropas en cada momento, que queda con 6.
- **AC-004.3 (hipoteca para pagar):** un jugador con 4 de efectivo y `BRA` (precio 20) cae en un país con arancel 10. Hipoteca `BRA` y recibe 10, paga el arancel y queda con 4. El dueño recibe 10. El público ve que `BRA` quedó hipotecado.
- **AC-004.4:** un acuerdo que entregaría un país con tropas, sin autorizar su desmovilización, se rechaza sin cambiar nada.
- **AC-004.5:** un acuerdo que dejaría al vendedor sin países se rechaza.
- **AC-004.6:** un país comprado por comercio en el turno global $t$ con 4 jugadores no puede volver a comerciarse antes del turno $t+4$.
- **AC-004.7:** ninguna vista que no sea la del dueño contiene su efectivo exacto.
- **AC-004.8 (país hipotecado):** caer en un país hipotecado no cobra arancel; el dueño de un país hipotecado no recibe su ingreso por país.
- **AC-004.9 (reclutar):** un jugador con un bloque completo, uno de cuyos países está hipotecado, no puede reclutar con ese bloque hasta levantar la hipoteca.
- **AC-004.10 (levantar hipoteca):** levantar la hipoteca de un país de precio 30 cuesta 17 (15 + 10 %, redondeando hacia arriba).
- **AC-004.11 (quiebra):** un jugador con 2 de efectivo y un solo país, ya hipotecado y con 3 tropas, debe 10 de arancel y nadie le compra nada. Paga 2 al acreedor; su país pasa al acreedor, hipotecado y con la milicia; pierde su gobierno y pasa a pedir asilo.
- **AC-004.12 (sin dinero del banco):** en cualquier pago entre jugadores, lo que recibe el acreedor es igual a lo que paga el deudor.

## 9. Preguntas para el creador

1. ~~¿El banco completa el arancel?~~ No (D-24): se hipoteca o se vende, y si no alcanza, quiebra (§5 y §6). El diseño de hipoteca, venta de emergencia y quiebra se aprobó con G1 (D-25).
2. ~~¿Perdonar un arancel tiene coste?~~ No, es gratis (D-24).
