# 🍕 Topepizza – Carta Web

Proyecto web de carta digital para Topepizza.

## 🌐 Enlaces

- Carta web: https://carta.topepizza.com/
- Vercel: https://carta-web-amber.vercel.app
- Menú terraza: https://carta.topepizza.com/menu-terraza.jpeg

## 📂 Estructura

- `index.html` → Carta web
- `carta.png` → Carta visual principal
- `alergenos.pdf` → Información de alérgenos
- `menu-terraza.jpeg` → Menú terraza usado para QR
- `/docs` → Documentación y cambios

## 📱 QR Menú Terraza

El QR del menú terraza apunta directamente a:

`https://carta.topepizza.com/menu-terraza.jpeg`

Para actualizar el menú terraza, sustituir el archivo:

`menu-terraza.jpeg`

manteniendo exactamente el mismo nombre.  
Así la URL y el QR seguirán funcionando sin cambios.

## 📝 Cambios

Los cambios de precios y modificaciones están registrados en:

`/docs/CHANGELOG_CARTA_TOPEPIZZA.txt`

## ⚙️ Estado

Proyecto en producción y actualizado.

## Despliegue (kill-switch)

`git push` NO despliega. Vercel solo construye si el TÍTULO del commit
contiene el marker `[deploy]` (ver `ignoreCommand` en `vercel.json`).
Un push normal → build cancelado → 0€. Aplica a preview y a producción.
