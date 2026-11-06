# Cómo aportar a Geoconquista

¡Gracias por querer aportar! Geoconquista es un juego de estrategia geopolítica para jugar en persona, con un tablero en una pantalla grande, una tablet como consola y los móviles de los jugadores. Funciona en la red local, sin Internet.

## Antes de empezar

- **Código de conducta:** al participar aceptas el [código de conducta](CODE_OF_CONDUCT.md).
- **Licencias:** el código es AGPL-3.0-or-later y el contenido CC BY-SA 4.0 ([LICENCIAS.md](LICENCIAS.md)). Al aportar, aceptas que tu aportación se publique con esas licencias.
- **Estado del proyecto:** consulta [docs/README.md](docs/README.md), que indica la etapa actual y qué puertas están aprobadas.

## La regla principal: primero la documentación

**Si no está documentado y aprobado, no se implementa.** Las reglas del juego, las pantallas y la arquitectura se deciden en `docs/` antes de escribir código.

- **¿Quieres cambiar una regla, una cifra o una pantalla?** Abre un *issue* o un *pull request* que modifique el documento correspondiente de `docs/`. Cuando el creador lo apruebe, se implementa.
- **¿Encontraste un error?** Abre un *issue*. Si el error revela un comportamiento que ningún documento define, hay que documentarlo antes de corregirlo.
- **¿Quieres programar algo?** Busca primero la spec aprobada que lo pide (`docs/gameplay/`, `docs/ux/`…) y cita sus criterios de aceptación (`AC-###.#`) en tu *pull request*.
- **Las cifras del juego** (precios, ingresos, tropas…) están en [docs/gameplay/parameters.md](docs/gameplay/parameters.md) y en los datos de contenido, nunca en el código.

Las reglas completas para quien programa, también si usas agentes de IA, están en [AGENTS.md](AGENTS.md).

### Idiomas

La documentación está en español y en inglés. El español es la versión de referencia: cada documento `nombre.md` tiene su traducción `nombre.en.md`. Si cambias un documento, actualiza las dos versiones; si solo escribes en inglés, no pasa nada: indícalo en el *pull request* y se traduce al español durante la revisión. El juego es nativo en español y tiene todos sus textos también en inglés. Las **voces y las imágenes con texto** solo se producen en español: si quieres que la versión en inglés tenga narrador o imágenes en inglés, ¡tus aportaciones son bienvenidas! Ver [docs/product/localization.md](docs/product/localization.md).

## Firma tus commits (DCO)

Usamos el [Developer Certificate of Origin](DCO): con cada commit certificas que tienes derecho a aportar ese trabajo bajo la licencia del proyecto. Firma cada commit con:

```bash
git commit -s -m "Descripción del cambio"
```

Eso añade una línea `Signed-off-by: Tu Nombre <tu@correo>` al mensaje. Los *pull requests* sin esa línea en todos sus commits no se pueden fusionar.

## Contenido: cartas, retos y textos

- Cada carta sigue la plantilla [docs/templates/card.md](docs/templates/card.md), con sus modos y su estado editorial.
- Nada de estereotipos étnicos, religiosos ni nacionales, ni líderes políticos reales.
- En Verdad o Reto siempre se puede pasar, y ningún reto exige daño, alcohol obligatorio ni contacto no consentido.
- **Contenido +18:** las aportaciones para los modos `familiar_18`, `party_18`, `party_extreme_18` y `parejas_18` pasan revisión editorial antes de entrar. El contenido de `familiar_u18` debe ser apto para menores.

## Arte y audio

- Los activos definitivos van en `assets/` con su entrada en `assets/manifest.json`: origen, herramienta, fecha, ediciones y licencia.
- Si usaste una herramienta de IA, indica cuál, el modelo y el prompt, y confirma que sus condiciones permiten publicarlo con la licencia del proyecto.
- No uses material de terceros protegido, ni el estilo identificable de un artista vivo.

## Seguridad

Nunca incluyas claves de API ni secretos en el código, la documentación o los commits. Van en `.env`, que está ignorado por git.
