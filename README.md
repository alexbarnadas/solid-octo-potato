# La guía de la bici

Guía de compra de bicicleta para Blanca y Axel. Una sola página, formato diapositivas,
sin dependencias ni build.

## Ver en local

```bash
python3 -m http.server 8000
# abrir http://localhost:8000
```

## Estructura

| Archivo | Qué es |
|---|---|
| `index.html` | Todo: contenido, estilos y navegación |
| `img/` | Capturas de los anuncios de Wallapop |
| `vercel.json` | Cabeceras de caché |

## Cómo editar los textos

Todo el contenido está en `index.html`, dentro de `<main class="stage">`. Cada diapositiva
es una `<section class="slide">` con su `id` y su `data-chap` (el capítulo al que pertenece).
**El índice lateral y la cronología se generan solos** a partir de esas secciones: para
añadir, quitar o reordenar una diapositiva basta con mover la `<section>`, no hay que tocar
el JavaScript.

Piezas que se repiten:

```html
<!-- Caja de opinión personal -->
<div class="tio">
  <div class="tio__label">El tío dice</div>
  <p>…</p>
</div>

<!-- Aviso o dato al margen -->
<div class="callout">
  <div class="callout__label">Título del aviso</div>
  <p>…</p>
</div>

<!-- Detalle plegable, para que la diapositiva no se desborde -->
<details>
  <summary>Si queréis profundizar</summary>
  <p>…</p>
</details>
```

Los bloques con borde discontinuo naranja (`class="pendiente"`) son **marcadores de texto
pendiente**: se sustituyen por el texto definitivo y se borra la clase.

### Regla de oro al editar

Cada diapositiva tiene que **caber en pantalla sin scroll**. Si al añadir texto aparece
barra de desplazamiento dentro de la diapositiva, hay que mover ese contenido a un
`<details>` o partir la diapositiva en dos.

## Añadir los anuncios de Wallapop

1. Guardar las capturas en `img/` como `anuncio-1.jpg`, `anuncio-2.jpg`…
2. En la diapositiva `#wallapop`, sustituir el `<div class="ad__shot">…</div>` por:

```html
<a class="ad__shot" href="ENLACE_DEL_ANUNCIO" target="_blank" rel="noopener noreferrer">
  <img src="img/anuncio-1.jpg" alt="Anuncio de una bici de gravel en Wallapop">
</a>
```

## Desplegar en Vercel

1. Entrar en [vercel.com/new](https://vercel.com/new)
2. Importar este repositorio de GitHub
3. Framework preset: **Other**. Sin build command, sin output directory
4. Deploy

Cada push a la rama vuelve a desplegar solo.

### Dominio propio

En el proyecto de Vercel: **Settings → Domains → Add**. Vercel indica los registros DNS
(normalmente un `A` a `76.76.21.21` o un `CNAME` a `cname.vercel-dns.com`) que hay que
poner en el panel del registrador. El certificado HTTPS lo emite Vercel solo.

## Notas

- Sin dependencias, sin `node_modules`, sin build. Es un HTML y ya está.
- Modo claro y oscuro: sigue al sistema y se puede forzar con el botón del índice.
- El checklist y la preferencia de tema se guardan en el navegador de quien lo lee
  (`localStorage`). No se comparte entre dispositivos.
- Lleva `<meta name="robots" content="noindex">` porque es una página familiar, no pública.
