# Cómo funciona — Carta web TopePizza

> Qué hace por detrás. Para **entender**, no para operar (eso va en `COMO_SE_USA.md`).

## En 30 segundos

`carta.topepizza.com` muestra la carta de TopePizza y las listas de precios
oficiales de cada tienda. Todo sale de **una sola lista de datos** (`carta.json`):
las páginas se pintan solas leyéndola. Cambiar un precio = cambiar un número en
esa lista; la web y las hojas de todas las tiendas se actualizan a la vez.

## Qué corre solo (automatismos)

| Cuándo | Qué pasa | Quién lo hace | Para qué |
|--------|----------|---------------|----------|
| Commit en `main` con `[deploy]` en el título | Vercel construye y publica | Vercel (GitHub → Vercel) | Actualizar la web pública |
| Commit/push SIN `[deploy]` | Build cancelado (0 €) | `ignoreCommand` de `vercel.json` | Que un push normal no despliegue por accidente |
| Al abrir la web | La página lee `carta.json` y `locales.json` y se pinta | JavaScript de `index.html` y `lista/index.html` | Que el dato viva separado del diseño |
| Al abrir `/lista/?t=<tienda>` | Se calcula el precio de lista: carta **+20 %**, redondeado hacia arriba al múltiplo de 0,05 | JavaScript de `lista/index.html` | La lista publica un techo por si algún día suben los precios |

## Si NO se hace X → pasa Y (consecuencias)

- Si un commit no lleva `[deploy]` en el TÍTULO → GitHub lo guarda pero la web NO cambia.
- Si se edita `carta.json` con un error de sintaxis (una coma de más) → la página sale VACÍA. Probar en local o en preview antes de desplegar a producción.
- Si se borra una foto de `fotos/` que un producto referencia → esa tarjeta sale sin imagen (no rompe la página).
- Si una tienda no está en `locales.json` → su enlace `/lista/?t=...` enseña la primera tienda de la lista, no un error.

## Piezas y quién es quién

- **`carta.json`** — la pizarra: productos, descripciones, precios, extras y observaciones. La única fuente.
- **`locales.json`** — una línea por tienda: razón social, dirección, CIF. El membrete de su lista de precios.
- **`index.html`** — la carta pública (móvil primero, buscador, secciones).
- **`lista/index.html`** — la lista de precios imprimible (A4, membrete por tienda, +20 % calculado).
- **`fotos/`** — logotipo y fotos de producto (hoy extraídas del folleto; se sustituyen por originales en alta sin tocar nada más).
- **`vercel.json`** — el kill-switch de despliegue.
- **`carta-png-anterior.html` + `carta.png`** — la web antigua (la foto del folleto), guardada por si hay que volver atrás.

## Flujo principal (paso a paso)

1. José dicta un cambio a Claude (o pasa foto del folleto nuevo).
2. Claude edita `carta.json`/`locales.json`, enseña el diff y José confirma.
3. Commit con `[deploy]` → push → Vercel publica (~1 min).
4. La carta y las listas de todas las tiendas quedan actualizadas a la vez.

## Dónde mirar cada cosa

- Web pública → `https://carta.topepizza.com`
- Lista de una tienda → `https://carta.topepizza.com/lista/?t=<id>` (ids en `locales.json`)
- Estado de despliegues → panel de Vercel (proyecto `carta-web`)
- Historial de cambios de la carta → `git log carta.json`
- Plan y decisiones del proyecto → vault: `knowledge/proyectos/carta-web/plan.md`
