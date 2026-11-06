---
name: documentation-first
description: Procedimiento obligatorio de Geoconquista para implementar funcionalidades, cambiar reglas, crear pantallas o flujos, tocar arquitectura, red o persistencia, corregir bugs que revelan comportamiento no documentado, crear contenido (cartas, retos, mazos) o incorporar activos de arte y audio. Documenta primero, implementa después.
---

# Documentation First: procedimiento

Las reglas están en `AGENTS.md` y su justificación en `docs/decisions/ADR-000-gobernanza.md`. Esta skill describe **cómo** aplicarlas paso a paso. Si algo de aquí contradijera `AGENTS.md`, manda `AGENTS.md` y se corrige esta skill.

## Fase 1. Descubrimiento documental

1. Consulta en `docs/README.md` el estado de las puertas (G0–G3) y el registro de decisiones.
2. Localiza los documentos que gobiernan la tarea: gameplay, UX, arquitectura, specs `FS-###` y ADR.
3. Comprueba su estado. Solo `APROBADO` autoriza implementar.
4. Lista huecos, ambigüedades y contradicciones.
5. Declara el estado documental: `LISTO_PARA_IMPLEMENTAR`, `FALTA_DOCUMENTACION` o `HAY_CONFLICTO_DOCUMENTAL`.

## Fase 2. Documentación

Si falta algo, crea o actualiza lo necesario en estado `PROPUESTO`:

- La spec de funcionalidad (`docs/templates/feature-spec.md`) con sus AC verificables.
- Un ADR (`docs/templates/adr.md`) si hay una decisión de arquitectura.
- El documento de UX, si cambia un flujo o una pantalla.
- El documento de gameplay y `docs/gameplay/parameters.md`, si cambia una regla o una cifra.
- La ficha de carta (`docs/templates/card.md`) o de activo (`docs/templates/asset-brief.md`), si es contenido o arte.

Actualiza también la traducción `<nombre>.en.md` de cada documento que toques (D-29); si es un documento nuevo, créala.

Después **detente** y pide la aprobación del creador. No continúes a la Fase 3 sobre documentos `PROPUESTO`.

## Fase 3. Plan de implementación

Antes de editar código, presenta un plan breve con:

- documentos fuente e IDs de spec y AC;
- módulos y archivos que se van a crear o editar;
- pruebas que demostrarán cada AC;
- riesgos.

## Fase 4. Implementación

- Implementa solo lo documentado, con nombres alineados con la documentación.
- Respeta los límites: motor (reglas, sin E/S) → protocolo → servidor → cliente. La interfaz nunca decide una regla.
- Las cifras salen de datos de contenido; los textos, cartas y retos, de contenido estructurado.
- Si aparece una decisión no documentada, **para** y vuelve a la Fase 2.

## Fase 5. Validación

- Cada AC tiene al menos una prueba que pasa.
- No hay comportamiento fuera de la spec.
- Las vistas filtradas no exponen datos de un nivel de visibilidad superior (pruebas `AC-PRIV`).
- La fila correspondiente de `docs/testing/acceptance-matrix.md` está actualizada.

## Fase 6. Cierre

Entrega el punto 5 del contrato de salida: documentos y archivos tocados, pruebas añadidas, riesgos o deudas abiertas y la confirmación de que no se salió de la línea documentada.

## Señales para detenerse y volver a documentar

- «Esto no está especificado, pero seguro conviene así.»
- «Para que funcione agregué este comportamiento extra.»
- «La interfaz necesita decidir una regla del juego.»
- «Dos documentos dicen cosas distintas.»
- «La función afecta a varias superficies, pero solo hay documento de una.»
- «Pongo esta cifra a mano y luego la sacamos.»

## Bugs y refactors

- **Bug que contradice un documento aprobado:** se corrige y se agrega la prueba que faltaba.
- **Bug que revela comportamiento nunca documentado:** primero se documenta el comportamiento esperado y se aprueba; después se corrige.
- **Refactor:** solo si preserva el comportamiento documentado o lo respalda un cambio documental aprobado. Nunca se usa para colar cambios funcionales.

## Activos de arte y audio

1. El activo responde a una necesidad escrita en un documento de UX o de contenido.
2. Se explora en `exploracion/` siguiendo `docs/assets/pipeline.md`.
3. El creador elige entre variantes.
4. El activo final se edita, se optimiza y se copia a `assets/` con su entrada completa en `assets/manifest.json`.
