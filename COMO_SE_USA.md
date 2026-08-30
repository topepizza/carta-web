# Cómo se usa — Carta web TopePizza

> Qué tocar para operarlo. Para el "por qué" → `COMO_FUNCIONA.md`.

## Requisitos previos

- Nada para VER la web o imprimir listas: son páginas públicas.
- Para CAMBIAR la carta: acceso al repo `topepizza/carta-web` (lo normal es
  pedírselo a Claude, que edita, enseña el cambio y publica con OK de José).

## Accesos rápidos

- Carta pública → `https://carta.topepizza.com`
- Listas de precios por tienda:
  - Palencia → `https://carta.topepizza.com/lista/?t=topecastilla`
  - Parquesol → `https://carta.topepizza.com/lista/?t=topeparquesol`
  - Dueñas → `https://carta.topepizza.com/lista/?t=zagales-duenas`

## Operaciones comunes

### Cambiar un precio / añadir o quitar un producto
Decírselo a Claude en lenguaje natural («sube la Carnívora a 12,50», «añade
Helado de fresa 120 ml a 2,50 en postres», «quita la Cabrita») o pasarle la
foto del folleto nuevo. Claude enseña el cambio exacto, José confirma, y se
publica solo. A mano: editar `carta.json`, commit con `[deploy]` en el
título, push a `main`.

### Imprimir la lista de precios de una tienda (el encargado)
1. Abrir el enlace de SU tienda (favorito o QR de la trastienda).
2. Pulsar «Imprimir esta hoja» (o Ctrl+P / compartir → imprimir en el móvil).
3. Colgarla. Cuando cambien precios, el aviso es solo «reimprimid la lista».

### Añadir una tienda nueva
Una entrada más en `locales.json` (id, razón social, dirección, CIF) → su
enlace `/lista/?t=<id>` existe automáticamente.

### Probar antes de publicar
Push a una rama (sin tocar `main`) con `[deploy]` en el commit → Vercel crea
una preview con URL propia. A producción solo por merge a `main` con OK de José.

### Volver atrás
```bash
git revert <commit>   # y un commit con [deploy] para publicar la vuelta
```

## Problemas frecuentes

- **Hice push y la web no cambia** → al título del commit le falta `[deploy]`
  (kill-switch, ver README). Es lo esperado, no un fallo.
- **La página sale vacía** → `carta.json` roto (sintaxis JSON). Validar con
  `node -e "JSON.parse(require('fs').readFileSync('carta.json'))"`.
- **Un producto sin foto** → falta el fichero en `fotos/` o el campo `foto`
  no coincide con el nombre del fichero (sin `.png`).
