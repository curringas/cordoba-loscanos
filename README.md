# Roadbook Córdoba – Caños de Meca

Sitio estático de un solo fichero HTML más el manifiesto, el service worker y los iconos.
No necesita build, ni Node, ni base de datos. Sirve la carpeta tal cual.

## Contenido

Todos los ficheros van en la raíz del repositorio, sin subcarpetas.

```
index.html              La página completa: CSS y JS embebidos
manifest.webmanifest    Metadatos de instalación (nombre, iconos, color, standalone)
sw.js                   Service worker: cachea la página y funciona sin cobertura
icon-192.png            Icono de pantalla de inicio
icon-512.png            Icono grande
icon-maskable-512.png   Icono adaptable para Android
```

## Publicación

Cualquier hosting estático con HTTPS vale. El service worker solo se registra bajo HTTPS
o en `localhost`, así que por HTTP plano la página funciona pero pierde el modo offline.

**Hosting propio**: sube los seis ficheros a un subdominio o a una subcarpeta. Si va en
subcarpeta, las rutas son relativas y no hay que tocar nada.

**Cloudflare Pages**: crear proyecto, «Direct Upload», arrastrar la carpeta.

**GitHub Pages**: repositorio nuevo con estos ficheros en la raíz, Settings → Pages →
Deploy from a branch → `main` / `/ (root)`.

**Netlify**: arrastrar la carpeta en el panel de Sites.

## Probar en local

```bash
python3 -m http.server 8080
```

Y abrir `http://localhost:8080`.

## Después de cada cambio

El service worker sirve de caché, así que al actualizar `index.html` hay que subir también
la versión de la caché: cambiar `roadbook-canos-v1` por `roadbook-canos-v2` en `sw.js`.
Sin eso, los móviles que ya tengan la página instalada seguirán viendo la versión antigua.

## Datos guardados

Las marcas de «hecho» se guardan en `localStorage` con la clave `roadbook-canos-v1`.
Son locales de cada navegador: no se sincronizan ni salen del dispositivo.
