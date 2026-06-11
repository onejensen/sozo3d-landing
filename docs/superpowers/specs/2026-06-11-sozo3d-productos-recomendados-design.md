# Sozo3D — Sección de Productos Recomendados (afiliados)

**Fecha:** 2026-06-11
**Estado:** Aprobado, listo para plan de implementación

## Resumen

Añadir a la home (`index.html`) una sección nueva de **productos recomendados** para impresión 3D, monetizada con los enlaces de afiliado de Amazon y AliExpress del usuario. Debe verse profesional y ser sencilla de navegar, siguiendo el lenguaje visual existente (naranja `#E87722` sobre negro, tipografía Clash Display, tarjetas).

La gestión de productos se hace mediante un archivo de datos `productos.json` que la web lee y pinta automáticamente; añadir un producto = añadir una entrada a una lista.

## Decisiones tomadas (brainstorming)

| Decisión | Elección |
|---|---|
| Modelo de datos | Archivo `productos.json` + render con JS vanilla |
| Estilo de tarjeta | Foto protagonista (vertical: foto, sello, nombre, descripción, botón) |
| Fotos | Propias (en `assets/productos/`), con fallback de degradado |
| Organización | Cuadrícula única curada (ideal 6–12 productos) |
| Ubicación en la página | Entre `#contact` (Contacto) y `#social` (Síguenos) |
| Contenido de la tarjeta | Sello editorial + descripción corta. **Sin precio ni estrellas** (cumplimiento de políticas de Amazon) |

## Arquitectura

El sitio es estático (GitHub Pages, dominio `sozo3d.es`), una sola página `index.html` con CSS y JS en línea. La sección sigue ese patrón:

1. **Markup HTML** — un `<section id="recomendados">` con cabecera, aviso de afiliados y un contenedor de cuadrícula vacío (`<div class="reco__grid">`).
2. **Datos** — `productos.json` en la raíz del proyecto.
3. **Render** — un pequeño script en línea (junto al del logo) que hace `fetch('productos.json')`, construye el HTML de cada tarjeta e inyecta en `.reco__grid`.
4. **Estilos** — clases nuevas (`.reco*`, `.product-card*`) añadidas al bloque `<style>` existente, reutilizando los tokens (`--orange`, `--black2`, etc.) y añadiendo el layout de escritorio dentro del `@media (min-width: 768px)` ya presente.
5. **Navegación** — nuevo enlace "Recomendados" (`#recomendados`) en `.navbar--desktop__links`, entre "Contacto" y "Síguenos".

No se toca el JSON-LD de Schema.org: los productos de afiliado no son ofertas del negocio y no deben mezclarse con el `OfferCatalog` de servicios.

## Modelo de datos — `productos.json`

```json
{
  "productos": [
    {
      "nombre": "Filamento PLA 1.75mm · 1kg",
      "tienda": "amazon",
      "enlace": "https://www.amazon.es/dp/XXXX?tag=TU-TAG",
      "imagen": "assets/productos/pla.jpg",
      "sello": "Recomendado",
      "descripcion": "El que usamos a diario: fiable y sin atascos."
    }
  ]
}
```

Campos por producto:

- `nombre` *(obligatorio)* — título del producto.
- `tienda` *(obligatorio)* — `"amazon"` o `"aliexpress"`. Determina el texto del botón ("Ver en Amazon" / "Ver en AliExpress") y el color del chip de tienda.
- `enlace` *(obligatorio)* — URL de afiliado completa.
- `imagen` *(opcional)* — ruta a la foto propia. Si falta o no carga, se muestra un degradado de marca.
- `sello` *(opcional)* — texto del sello editorial (ej. "Recomendado", "Imprescindible", "Calidad", "Económico"). Si falta, no se muestra sello.
- `descripcion` *(opcional)* — una línea explicando por qué se recomienda.

El archivo se entrega con 4–6 entradas de ejemplo (con enlaces e imágenes de marcador) para que el usuario las sustituya.

## Anatomía de la tarjeta

```
┌──────────────────────────┐
│ [chip tienda]            │  ← media: foto propia o degradado, aspect 4/3
│         (foto)           │
├──────────────────────────┤
│ [SELLO]                  │  ← badge editorial naranja
│ Nombre del producto      │
│ Descripción corta…       │
│ [  Ver en Amazon →  ]    │  ← botón naranja, etiqueta según tienda
└──────────────────────────┘
```

- Enlace de la tarjeta/botón: `target="_blank"` y `rel="sponsored nofollow noopener"`.
- Chip de tienda: Amazon `#FF9900` (texto oscuro), AliExpress `#E62E04` (texto blanco).
- `alt` de la imagen = `nombre`.

## Cumplimiento (afiliados)

- **Aviso obligatorio** visible bajo el título: *"Algunos enlaces son de afiliados: si compras a través de ellos podemos llevarnos una pequeña comisión, sin coste extra para ti."*
- **Sin precios ni valoraciones fijas**: Amazon solo permite mostrarlos en vivo vía su Product Advertising API (que un sitio estático no tiene). Por eso usamos sello editorial en su lugar.
- Atributos `rel="sponsored nofollow noopener"` en todos los enlaces de afiliado.

## Responsive

- **Móvil** (base): cuadrícula de 2 columnas, igual que `.services__grid`.
- **Escritorio** (`min-width: 768px`): 3 columnas, con el mismo padding centrado `max(48px, calc((100% - 1280px) / 2))` que el resto de secciones. La foto se ve más grande que en una rejilla de 4.
- **Móviles pequeños** (`max-width: 359px`): se mantiene la rejilla de 2 columnas (igual que `.services__grid`, que tampoco se reapila a esa anchura). No se añade regla especial.

## Manejo de errores y casos límite

- **`fetch` falla** (sin conexión, o abierto con `file://` en local): se captura el error, se hace `console.warn`, y la cuadrícula queda vacía o muestra un mensaje discreto "Pronto añadiremos recomendaciones". No rompe el resto de la página. (En GitHub Pages el `fetch` funciona con normalidad.)
- **Lista vacía** (`productos: []`): la sección muestra el mensaje "Pronto…" en vez de una rejilla vacía.
- **Imagen ausente o que no carga**: `onerror` oculta el `<img>` y se ve el degradado de marca del contenedor `media`.
- **`tienda` desconocida**: el botón cae a un texto genérico "Ver producto" y chip neutro.

## Archivos afectados

- `index.html` — nueva `<section id="recomendados">`, enlace en el navbar de escritorio, clases CSS nuevas en el `<style>`, y script de render en el `<script>` existente.
- `productos.json` — **nuevo**, con entradas de ejemplo.
- `assets/productos/` — **nueva carpeta** para las fotos propias (incluir un `.gitkeep` o una imagen de ejemplo).

## Verificación

1. Servir en local (`python3 -m http.server`) y abrir `index.html`.
2. Las tarjetas se pintan desde `productos.json`.
3. Cada botón abre la tienda correcta en pestaña nueva; el chip coincide con la tienda.
4. El aviso de afiliados es visible.
5. Responsive: 2 columnas en móvil, 3 en escritorio; navbar muestra "Recomendados" y el ancla funciona.
6. Fallback: un producto sin `imagen` muestra el degradado; `productos: []` muestra el mensaje "Pronto…".
7. Sin errores en la consola.
8. Validar también en el deploy de GitHub Pages.

## Fuera de alcance (YAGNI)

- Filtros/categorías por pestañas, buscador, paginación.
- Precios o valoraciones en vivo (API de Amazon).
- Página separada de productos.
- Carrito o checkout (es solo redirección por afiliado).
