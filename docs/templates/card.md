# CARD-<tipo>-### — Título de la carta

| Campo | Valor |
|---|---|
| Tipo | `hacienda` / `migracion` / `correo` / `mensajeria` / `verdad` / `reto` |
| Modos | `familiar_u18`, `familiar_18`, `party_18`, `party_extreme_18`, `parejas_18` (los que apliquen) |
| Intensidad | 1 / 2 / 3 |
| Visibilidad | `público` / `propietario` |
| Estado editorial | `borrador` / `revisado` / `aprobado` |
| Revisado por | |

## Texto
Lo que lee la mesa o el jugador. Sin datos privados si es pública.

## Efecto
Referencia a un efecto **definido en la spec** (`EVT-###` o efecto tipado). Nunca lógica libre.

- Objetivo válido:
- Duración (rondas):
- Acumulable con efectos del mismo tipo: no

## Verdad o Reto (solo esos tipos)
- Permite pasar: **sí**, siempre
- Penalización al pasar (fija y visible antes de aceptar):
- Comprobación de seguridad: sin daño, sin alcohol obligatorio, sin contacto no consentido, sin exponer datos privados.

## Revelaciones
Qué ve el público y qué ve el afectado. Si el efecto es proporcional al efectivo, el importe nunca es público.

## Arte
Ficha de activo asociada (`templates/asset-brief.md`), si la carta lleva ilustración.
