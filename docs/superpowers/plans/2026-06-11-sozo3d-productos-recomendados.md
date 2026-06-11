# Sección de Productos Recomendados (afiliados) — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Añadir a `index.html` una sección de productos recomendados de impresión 3D, monetizada con enlaces de afiliado de Amazon y AliExpress, alimentada por un `productos.json` editable.

**Architecture:** Sitio estático de un solo archivo (GitHub Pages). La sección es un `<section id="recomendados">` con CSS añadido al bloque `<style>` existente y un script en línea que hace `fetch('productos.json')`, construye las tarjetas e inyecta el HTML. Reutiliza los tokens y patrones de diseño existentes (`--orange`, `.section`, rejilla tipo `.services__grid`).

**Tech Stack:** HTML + CSS + JavaScript vanilla. Sin build, sin framework de tests. Verificación por validación de JSON (`python3 -m json.tool`), `grep` de estructura, y navegador con `python3 -m http.server`.

**Nota de testing:** El proyecto no tiene runner de tests. Donde el esquema TDD pide "test que falla", aquí se usa una verificación equivalente: comando de shell con salida esperada o comprobación visual en navegador. Las verificaciones se hacen **antes** del cambio (para confirmar que aún no existe) y **después** (para confirmar que funciona).

---

## File Structure

- `productos.json` — **nuevo**, raíz del proyecto. Fuente de datos editable: lista de productos. Responsabilidad única: contenido.
- `assets/productos/` — **nueva carpeta** para las fotos propias. Incluye `.gitkeep` para versionar la carpeta vacía.
- `index.html` — **modificado** en tres zonas independientes:
  - Bloque `<style>`: clases CSS de la sección (móvil y, dentro del `@media (min-width:768px)`, escritorio).
  - `.navbar--desktop__links`: nuevo enlace "Recomendados".
  - Cuerpo: nueva `<section id="recomendados">` entre `#contact` y `#social`.
  - Bloque `<script>`: IIFE de render que lee `productos.json`.

---

## Task 1: Archivo de datos y carpeta de imágenes

**Files:**
- Create: `productos.json`
- Create: `assets/productos/.gitkeep`

- [ ] **Step 1: Confirmar que aún no existe**

Run: `ls productos.json 2>&1`
Expected: `ls: productos.json: No such file or directory`

- [ ] **Step 2: Crear `productos.json` con datos de ejemplo**

Crear `productos.json` con este contenido exacto (2 entradas llevan `imagen` vacía a propósito, para probar el fallback de degradado):

```json
{
  "productos": [
    {
      "nombre": "Filamento PLA 1.75mm · 1kg",
      "tienda": "amazon",
      "enlace": "https://www.amazon.es/dp/REEMPLAZAR?tag=TU-TAG-21",
      "imagen": "assets/productos/filamento-pla.jpg",
      "sello": "Recomendado",
      "descripcion": "El que usamos a diario: fiable y sin atascos."
    },
    {
      "nombre": "Set de boquillas 0.4mm (10 uds)",
      "tienda": "aliexpress",
      "enlace": "https://es.aliexpress.com/item/REEMPLAZAR.html",
      "imagen": "assets/productos/boquillas.jpg",
      "sello": "Imprescindible",
      "descripcion": "Repuesto barato que conviene tener siempre a mano."
    },
    {
      "nombre": "Lámina PEI magnética para cama",
      "tienda": "amazon",
      "enlace": "https://www.amazon.es/dp/REEMPLAZAR?tag=TU-TAG-21",
      "imagen": "assets/productos/lamina-pei.jpg",
      "sello": "Calidad",
      "descripcion": "Adhesión perfecta y piezas fáciles de soltar."
    },
    {
      "nombre": "Adhesivo en barra para cama",
      "tienda": "aliexpress",
      "enlace": "https://es.aliexpress.com/item/REEMPLAZAR.html",
      "imagen": "assets/productos/adhesivo.jpg",
      "sello": "Económico",
      "descripcion": "Truco sencillo para que la primera capa agarre bien."
    },
    {
      "nombre": "Pinzas y espátula de retirada",
      "tienda": "amazon",
      "enlace": "https://www.amazon.es/dp/REEMPLAZAR?tag=TU-TAG-21",
      "imagen": "",
      "sello": "Útil",
      "descripcion": "Para limpiar soportes y retirar piezas sin dañarlas."
    },
    {
      "nombre": "Calibre digital 150mm",
      "tienda": "aliexpress",
      "enlace": "https://es.aliexpress.com/item/REEMPLAZAR.html",
      "imagen": "",
      "sello": "Precisión",
      "descripcion": "Mide tolerancias al milímetro antes de imprimir."
    }
  ]
}
```

- [ ] **Step 3: Crear la carpeta de imágenes**

Run: `mkdir -p assets/productos && touch assets/productos/.gitkeep`

- [ ] **Step 4: Verificar que el JSON es válido**

Run: `python3 -m json.tool productos.json > /dev/null && echo OK`
Expected: `OK` (si imprime un error de parseo, corregir la coma/comilla indicada)

- [ ] **Step 5: Verificar el número de productos**

Run: `python3 -c "import json; print(len(json.load(open('productos.json'))['productos']))"`
Expected: `6`

- [ ] **Step 6: Commit**

```bash
git add productos.json assets/productos/.gitkeep
git commit -m "feat: add productos.json data file and product images folder"
```

---

## Task 2: CSS de la sección (móvil + escritorio)

**Files:**
- Modify: `index.html` (bloque `<style>`)

- [ ] **Step 1: Confirmar que las clases aún no existen**

Run: `grep -c "product-card" index.html`
Expected: `0`

- [ ] **Step 2: Añadir el CSS base (móvil)**

En `index.html`, dentro del bloque `<style>`, justo **antes** del comentario `/* ── Footer ── */` (alrededor de la línea 540), insertar:

```css
    /* ── Recomendados (productos afiliados) ── */
    .reco__disclaimer {
      color: var(--muted);
      font-size: 11px;
      line-height: 1.5;
      margin-bottom: 18px;
    }
    .reco__disclaimer strong {
      color: #aaa;
      font-weight: 500;
    }

    .reco__grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }

    .reco__empty {
      color: var(--muted);
      font-size: 12px;
      grid-column: 1 / -1;
    }

    .product-card {
      background: var(--black2);
      border: 1px solid #2a2a2a;
      border-radius: 14px;
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }

    .product-card__media {
      position: relative;
      aspect-ratio: 4 / 3;
      background: linear-gradient(135deg, #241a12, #3a2410);
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .product-card__media img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .product-card__store {
      position: absolute;
      top: 8px;
      left: 8px;
      font-size: 9px;
      font-weight: 700;
      padding: 3px 7px;
      border-radius: 5px;
    }
    .product-card__store--amazon     { background: #FF9900; color: #111; }
    .product-card__store--aliexpress { background: #E62E04; color: #fff; }
    .product-card__store--otra       { background: #555;    color: #fff; }

    .product-card__body {
      padding: 12px;
      display: flex;
      flex-direction: column;
      flex: 1;
    }

    .product-card__badge {
      align-self: flex-start;
      background: rgba(232, 119, 34, 0.16);
      color: var(--orange);
      font-size: 9px;
      font-weight: 700;
      letter-spacing: 0.5px;
      text-transform: uppercase;
      padding: 3px 8px;
      border-radius: 5px;
      margin-bottom: 7px;
    }

    .product-card__name {
      color: var(--white);
      font-size: 13px;
      font-weight: 600;
      line-height: 1.25;
    }

    .product-card__desc {
      color: var(--muted);
      font-size: 11px;
      line-height: 1.4;
      margin-top: 4px;
    }

    .product-card__btn {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      margin-top: auto;
      padding: 9px;
      background: var(--orange);
      color: var(--white);
      font-size: 11px;
      font-weight: 600;
      border-radius: 20px;
    }
    .product-card__desc { margin-bottom: 11px; }
```

> Nota: `margin-top: auto` empuja el botón al fondo de la tarjeta para que queden alineados aunque las descripciones tengan distinta longitud (las tarjetas de una misma fila comparten altura por `align-items: stretch` del grid). El `margin-bottom` en `.product-card__desc` garantiza una separación mínima sobre el botón cuando el texto es corto.

- [ ] **Step 3: Añadir el CSS de escritorio**

Dentro del `@media (min-width: 768px)`, justo **antes** del comentario `/* Footer */` (alrededor de la línea 911, antes de `.footer {`), insertar:

```css
      /* Recomendados */
      #recomendados {
        padding: 48px max(48px, calc((100% - 1280px) / 2));
      }
      #recomendados .reco__grid {
        grid-template-columns: repeat(3, 1fr);
        gap: 16px;
      }
      #recomendados .product-card { border-radius: 16px; }
      #recomendados .product-card__body { padding: 16px; }
      #recomendados .product-card__name { font-size: 14px; }
      #recomendados .product-card__desc { font-size: 12px; }
      #recomendados .product-card__btn { font-size: 12px; padding: 11px; }
```

- [ ] **Step 4: Verificar que el CSS está presente y el HTML sigue bien formado**

Run: `grep -c "product-card__btn" index.html`
Expected: `>= 2` (una definición base + una en el media query de escritorio; el `.product-card__body > .product-card__btn` también cuenta)

Run: `grep -c "#recomendados" index.html`
Expected: `1` (solo en el CSS de escritorio por ahora)

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add CSS for recommended products section (mobile + desktop)"
```

---

## Task 3: Markup de la sección y enlace del navbar

**Files:**
- Modify: `index.html` (navbar y cuerpo)

- [ ] **Step 1: Confirmar que la sección aún no existe en el cuerpo**

Run: `grep -c 'id="recomendados"' index.html`
Expected: `0` (el `#recomendados` del CSS no lleva comillas en `id=`, así que esto debe dar 0)

- [ ] **Step 2: Añadir el enlace al navbar de escritorio**

En `index.html`, dentro de `.navbar--desktop__links` (alrededor de la línea 986-991), insertar el enlace "Recomendados" **entre** Contacto y Síguenos. El bloque debe quedar exactamente así:

```html
      <div class="navbar--desktop__links">
        <a href="#servicios">Servicios</a>
        <a href="#why">¿Por qué nosotros?</a>
        <a href="#contact">Contacto</a>
        <a href="#recomendados">Recomendados</a>
        <a href="#social">Síguenos</a>
      </div>
```

- [ ] **Step 3: Añadir la sección entre Contacto y Síguenos**

En `index.html`, justo **después** del cierre `</section>` de `#contact` (línea 1107) y **antes** del comentario `<!-- ⑤ REDES SOCIALES -->` (línea 1109), insertar:

```html
    <!-- ⑥ RECOMENDADOS (productos afiliados) -->
    <section id="recomendados" class="section">
      <p class="section__eyebrow">Recomendados</p>
      <h2 class="section__title">Lo que usamos y recomendamos</h2>
      <p class="reco__disclaimer"><strong>Material, herramientas y accesorios para impresión 3D.</strong> Algunos enlaces son de afiliados: si compras a través de ellos podemos llevarnos una pequeña comisión, sin coste extra para ti.</p>
      <div class="reco__grid" id="reco-grid">
        <p class="reco__empty">Cargando recomendaciones…</p>
      </div>
    </section>
```

- [ ] **Step 4: Verificar la estructura insertada**

Run: `grep -c 'id="recomendados"' index.html`
Expected: `1`

Run: `grep -c 'id="reco-grid"' index.html`
Expected: `1`

Run: `grep -c 'href="#recomendados"' index.html`
Expected: `1`

- [ ] **Step 5: Verificar visualmente la cabecera (aún sin tarjetas)**

Run: `python3 -m http.server 8000` (en segundo plano) y abrir `http://localhost:8000` en el navegador.
Expected:
- Entre la sección "¿Listo para imprimir?" (Contacto) y "Síguenos" aparece la cabecera "Recomendados" + "Lo que usamos y recomendamos" + el aviso de afiliados.
- La rejilla muestra "Cargando recomendaciones…" (todavía no hay JS de render).
- En escritorio, el navbar muestra el enlace "Recomendados" y al pulsarlo hace scroll a la sección.

Parar el servidor al terminar (Ctrl-C o `kill`).

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: add recommended products section markup and navbar link"
```

---

## Task 4: Script de render desde `productos.json`

**Files:**
- Modify: `index.html` (bloque `<script>`)

- [ ] **Step 1: Confirmar que el render aún no existe**

Run: `grep -c "reco-grid" index.html`
Expected: `1` (solo el `id` del markup de la Tarea 3; el script lo añadirá una segunda referencia)

- [ ] **Step 2: Añadir el IIFE de render**

En `index.html`, dentro del bloque `<script>` existente, justo **antes** del cierre `</script>` (línea 1181), insertar:

```javascript

    /* ── Productos recomendados ── */
    (function () {
      const grid = document.getElementById('reco-grid');
      if (!grid) return;

      const TIENDAS = {
        amazon:     { etiqueta: 'Amazon',     boton: 'Ver en Amazon' },
        aliexpress: { etiqueta: 'AliExpress', boton: 'Ver en AliExpress' }
      };

      function escapeHTML(str) {
        return String(str == null ? '' : str)
          .replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;')
          .replace(/"/g, '&quot;').replace(/'/g, '&#39;');
      }

      function cardHTML(p) {
        const tienda = TIENDAS[p.tienda] || { etiqueta: 'Ver', boton: 'Ver producto' };
        const claseTienda = TIENDAS[p.tienda] ? p.tienda : 'otra';
        const nombre = escapeHTML(p.nombre);
        const media = p.imagen
          ? '<img src="' + escapeHTML(p.imagen) + '" alt="' + nombre + '" loading="lazy" onerror="this.remove()">'
          : '';
        const sello = p.sello ? '<span class="product-card__badge">' + escapeHTML(p.sello) + '</span>' : '';
        const desc = p.descripcion ? '<p class="product-card__desc">' + escapeHTML(p.descripcion) + '</p>' : '';
        return ''
          + '<a class="product-card" href="' + escapeHTML(p.enlace) + '" target="_blank" rel="sponsored nofollow noopener">'
          +   '<div class="product-card__media">'
          +     media
          +     '<span class="product-card__store product-card__store--' + claseTienda + '">' + escapeHTML(tienda.etiqueta) + '</span>'
          +   '</div>'
          +   '<div class="product-card__body">'
          +     sello
          +     '<div class="product-card__name">' + nombre + '</div>'
          +     desc
          +     '<span class="product-card__btn">' + escapeHTML(tienda.boton) + ' →</span>'
          +   '</div>'
          + '</a>';
      }

      fetch('productos.json')
        .then(function (r) {
          if (!r.ok) throw new Error('HTTP ' + r.status);
          return r.json();
        })
        .then(function (data) {
          const items = (data && Array.isArray(data.productos)) ? data.productos : [];
          if (!items.length) {
            grid.innerHTML = '<p class="reco__empty">Pronto añadiremos recomendaciones.</p>';
            return;
          }
          grid.innerHTML = items.map(cardHTML).join('');
        })
        .catch(function (err) {
          console.warn('No se pudieron cargar los productos:', err);
          grid.innerHTML = '<p class="reco__empty">Pronto añadiremos recomendaciones.</p>';
        });
    })();
```

- [ ] **Step 3: Verificar que el script está presente**

Run: `grep -c "fetch('productos.json')" index.html`
Expected: `1`

- [ ] **Step 4: Verificación funcional en navegador**

Run: `python3 -m http.server 8000` (en segundo plano) y abrir `http://localhost:8000`.
Expected:
- La rejilla "Recomendados" muestra **6 tarjetas** (ya no "Cargando…").
- Cada tarjeta: chip de tienda arriba a la izquierda (Amazon naranja / AliExpress rojo), sello editorial naranja, nombre, descripción y botón.
- El botón dice **"Ver en Amazon →"** o **"Ver en AliExpress →"** según `tienda`.
- Las 2 tarjetas con `imagen` vacía ("Pinzas y espátula", "Calibre digital") muestran el **degradado de marca** sin imagen rota.
- Al hacer clic en una tarjeta, abre el enlace en **pestaña nueva**.
- Consola del navegador **sin errores**.

- [ ] **Step 5: Verificar atributos de afiliado en el DOM renderizado**

En la consola del navegador (con la página abierta en `http://localhost:8000`):

Run (en la consola del navegador): `document.querySelector('.product-card').getAttribute('rel')`
Expected: `"sponsored nofollow noopener"`

Run (en la consola del navegador): `document.querySelectorAll('.product-card').length`
Expected: `6`

- [ ] **Step 6: Verificar fallback de error / lista vacía**

Editar temporalmente `productos.json` y dejar `{ "productos": [] }`, recargar la página.
Expected: la rejilla muestra "Pronto añadiremos recomendaciones." sin errores.
Después **revertir** el cambio: `git checkout productos.json`.

- [ ] **Step 7: Verificar responsive**

Con la página abierta, usar las DevTools (modo dispositivo) o redimensionar la ventana:
Expected:
- Móvil (< 768px): rejilla de **2 columnas**.
- Escritorio (≥ 768px): rejilla de **3 columnas** con padding centrado, fotos más grandes.

Parar el servidor al terminar.

- [ ] **Step 8: Commit**

```bash
git add index.html
git commit -m "feat: render recommended products from productos.json"
```

---

## Verificación final (contra el spec)

- [ ] Las tarjetas se pintan desde `productos.json` — Tarea 4.
- [ ] Botón abre la tienda correcta en pestaña nueva; chip coincide — Tarea 4, Steps 4-5.
- [ ] Aviso de afiliados visible — Tarea 3, Step 3.
- [ ] `rel="sponsored nofollow noopener"` en todos los enlaces — Tarea 4, Step 5.
- [ ] Responsive 2 col móvil / 3 col escritorio — Tarea 4, Step 7.
- [ ] Navbar muestra "Recomendados" y el ancla funciona — Tarea 3, Step 5.
- [ ] Fallback: imagen ausente → degradado; lista vacía → mensaje "Pronto…" — Tarea 4, Steps 4 y 6.
- [ ] Sin errores en consola — Tarea 4, Step 4.
- [ ] No se toca el JSON-LD de Schema.org — confirmado: ninguna tarea modifica el bloque `<script type="application/ld+json">`.

## Notas para el despliegue

- Es GitHub Pages: tras hacer `git push`, esperar 1-2 min y validar en `https://sozo3d.es`. El `fetch('productos.json')` funciona en producción (mismo origen).
- El usuario debe sustituir los `enlace` de ejemplo por sus URLs de afiliado reales (con su `tag` de Amazon) y subir las fotos a `assets/productos/`.
- Abrir `index.html` con doble clic (`file://`) hará que `fetch` falle por CORS y se vea "Pronto…"; eso es esperado. Probar siempre con `python3 -m http.server`.
