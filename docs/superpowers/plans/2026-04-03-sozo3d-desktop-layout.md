# Sozo3D Desktop Layout Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a full-width desktop layout (`@media (min-width: 768px)`) to `index.html`, covering a sticky navbar, 2-column hero with circular logo, 4-column services, 3-column why cards, asymmetric CTA, 2-column social, and 3-column footer.

**Architecture:** All desktop CSS is appended inside a single `@media (min-width: 768px)` block at the end of the existing `<style>` tag. HTML receives minimal structural additions: wrapper divs for grid children, `id` attributes on sections for anchor nav, a new `<nav class="navbar--desktop">` element, and new class elements (`hero__content`, `hero__visual`, `hero__eyebrow-pill`). Mobile CSS is never removed or modified — all changes are additive.

**Tech Stack:** HTML5, CSS3 (Grid, Flexbox, `position: sticky`, `backdrop-filter`), Clash Display font (already loaded via Fontshare CDN), no build step, no framework.

---

## File Structure

- **Modify only:** `index.html`
  - HTML additions: `<nav class="navbar--desktop">` before hero; `id` attrs on 3 sections; wrapper divs in hero, CTA, social, footer; eyebrow pill element
  - CSS additions: mobile-base rules for new elements (e.g., `display: none` on `navbar--desktop`, `hero__visual`, `hero__eyebrow-pill`, `footer__left` flex setup); full `@media (min-width: 768px)` block at end of `<style>`

---

### Task 1: Foundation — Page Max-Width, Section IDs, Desktop Navbar

**Files:**
- Modify: `index.html`

Sets up the desktop skeleton: lifts `.page` to 1280px max-width, adds section `id` attributes for anchor links, inserts the sticky `<nav class="navbar--desktop">` element (hidden on mobile via `display: none`, shown as sticky flex bar on desktop).

- [ ] **Step 1: Add `id` attributes to three sections**

Find these three sections in the HTML and add the `id` attribute shown:

```html
<!-- ③ POR QUÉ SOZO3D -->
<section id="why" class="section">

<!-- ④ CTA CONTACTO -->
<section id="contact" class="cta-contact">

<!-- ⑤ REDES SOCIALES -->
<section id="social" class="section section--centered">
```

(`#servicios` already has its `id`.)

- [ ] **Step 2: Insert `<nav class="navbar--desktop">` as first child of `.page`**

Place immediately after `<div class="page">` and before `<!-- ① HERO -->`:

```html
<nav class="navbar--desktop">
  <div class="navbar--desktop__left">
    <img class="navbar--desktop__logo" src="assets/Logo_Sozo3D.jpg" alt="Sozo3D logo" />
    <span class="navbar--desktop__brand">Sozo<span>3D</span></span>
  </div>
  <div class="navbar--desktop__links">
    <a href="#servicios">Servicios</a>
    <a href="#why">¿Por qué nosotros?</a>
    <a href="#social">Síguenos</a>
    <a href="#contact">Contacto</a>
  </div>
  <a class="navbar--desktop__cta" href="https://wa.me/34623020424" target="_blank" rel="noopener noreferrer">
    💬 WhatsApp
  </a>
</nav>
```

- [ ] **Step 3: Add mobile-base rule for `navbar--desktop` inside `<style>`, just before the existing `@media (min-width: 500px)` block**

```css
/* ── Desktop navbar (hidden on mobile) ── */
.navbar--desktop { display: none; }
```

- [ ] **Step 4: Append the desktop media query block at the very end of `<style>` (after all existing rules)**

```css
/* ══════════════════════════════════════
   DESKTOP LAYOUT — min-width: 768px
   Additive only. Mobile CSS untouched.
   ══════════════════════════════════════ */
@media (min-width: 768px) {

  /* Page wrapper */
  .page {
    max-width: 1280px;
  }

  /* Desktop navbar */
  .navbar--desktop {
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: sticky;
    top: 0;
    z-index: 100;
    height: 64px;
    padding: 0 64px;
    background: rgba(15, 15, 15, 0.88);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    border-bottom: 1px solid #1e1e1e;
  }

  .navbar--desktop__left {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .navbar--desktop__logo {
    width: 44px;
    height: 44px;
    border-radius: 50%;
    object-fit: cover;
    border: 2px solid var(--orange);
    flex-shrink: 0;
  }

  .navbar--desktop__brand {
    font-size: 18px;
    font-weight: 700;
    color: var(--white);
  }
  .navbar--desktop__brand span { color: var(--orange); }

  .navbar--desktop__links {
    display: flex;
    gap: 32px;
  }

  .navbar--desktop__links a {
    color: rgba(255, 255, 255, 0.7);
    font-family: var(--font);
    font-size: 14px;
    font-weight: 500;
  }

  .navbar--desktop__links a:hover {
    color: var(--white);
  }

  .navbar--desktop__cta {
    display: inline-block;
    background: var(--orange);
    color: var(--white);
    font-family: var(--font);
    font-size: 13px;
    font-weight: 600;
    padding: 8px 20px;
    border-radius: 20px;
    white-space: nowrap;
  }

} /* end @media (min-width: 768px) */
```

- [ ] **Step 5: Verify in browser**

```bash
open "/Users/onejensen/Documents/MIS WEBS/Sozo3D/index.html"
```

Resize window to ≥768px.  
Expected: sticky navbar at top with circular logo (44px), "Sozo**3D**", four nav links, orange "💬 WhatsApp" pill on the right. Page content max-width expands to 1280px (no longer confined to the 480px mobile column).  
At <768px: navbar invisible, mobile hero nav still visible.

- [ ] **Step 6: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(desktop): foundation — page max-width, section IDs, sticky navbar"
```

---

### Task 2: Hero Desktop Layout

**Files:**
- Modify: `index.html`

Restructures the hero into a 2-column grid: left column (eyebrow pill + 72px headline + subtitle + single CTA), right column (Sozo3D logo 340×340px circular with orange glow). Mobile hero nav is hidden on desktop (replaced by `navbar--desktop`). Ghost "Ver trabajos" button hidden on desktop.

- [ ] **Step 1: Restructure hero HTML**

Replace the entire content of `<section class="hero">` with:

```html
<section class="hero">
  <!-- Mobile nav — hidden on desktop, replaced by navbar--desktop -->
  <nav class="hero__nav">
    <img class="hero__logo" src="assets/Logo_Sozo3D.jpg" alt="Sozo3D logo" />
    <span class="hero__brand">Sozo<span>3D</span></span>
    <a class="hero__nav-cta" href="https://wa.me/34623020424" target="_blank" rel="noopener noreferrer">
      📱 WhatsApp
    </a>
  </nav>

  <!-- Left column (desktop) / stacked content (mobile) -->
  <div class="hero__content">
    <p class="hero__eyebrow-pill">Impresión 3D Personalizada</p>
    <h1 class="hero__headline">
      IMPRIME<br><span>TU IDEA</span><br>EN 3D
    </h1>
    <p class="hero__sub">Impresión 3D personalizada para particulares y empresas</p>
    <div class="hero__btns">
      <a class="btn--primary" href="https://wa.me/34623020424" target="_blank" rel="noopener noreferrer">
        💬 Pedir presupuesto
      </a>
      <a class="btn--ghost" href="#servicios">Ver trabajos ↓</a>
    </div>
  </div>

  <!-- Right column — desktop only -->
  <div class="hero__visual">
    <img class="hero__logo-desktop" src="assets/Logo_Sozo3D.jpg" alt="Sozo3D" />
  </div>
</section>
```

- [ ] **Step 2: Add mobile-base CSS for new hero elements (inside `<style>`, just before the desktop `@media` block)**

```css
/* ── Hero new elements (mobile base) ── */
.hero__visual    { display: none; }
.hero__eyebrow-pill { display: none; }
```

- [ ] **Step 3: Add hero desktop CSS inside the `@media (min-width: 768px)` block, after the navbar rules**

```css
  /* Hero */
  .hero {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 64px;
    padding: 100px 64px 80px;
    min-height: 520px;
    align-items: center;
  }

  .hero__nav {
    display: none;
  }

  .hero__content {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .hero__visual {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .hero__eyebrow-pill {
    display: inline-block;
    background: rgba(232, 119, 34, 0.15);
    color: var(--orange);
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    padding: 6px 16px;
    border-radius: 20px;
    border: 1px solid rgba(232, 119, 34, 0.3);
    margin-bottom: 20px;
    align-self: flex-start;
  }

  .hero__headline {
    font-size: 72px;
    text-align: left;
    margin-bottom: 16px;
  }

  .hero__sub {
    text-align: left;
    font-size: 16px;
    margin-bottom: 32px;
  }

  .hero__btns {
    justify-content: flex-start;
  }

  .hero .btn--ghost {
    display: none;
  }

  .hero__logo-desktop {
    width: 340px;
    height: 340px;
    border-radius: 50%;
    object-fit: cover;
    box-shadow: 0 0 80px rgba(232, 119, 34, 0.3);
    border: 3px solid rgba(232, 119, 34, 0.4);
  }
```

- [ ] **Step 4: Verify in browser**

Resize to ≥768px.  
Expected:
- Sticky navbar visible above hero.
- Left column: orange eyebrow pill ("IMPRESIÓN 3D PERSONALIZADA"), headline "IMPRIME TU IDEA EN 3D" at ~72px left-aligned, subtitle, single orange "💬 Pedir presupuesto" button. No ghost button.
- Right column: Sozo3D logo 340×340px circular, soft orange glow around it.

At <768px: mobile layout unchanged — headline centered, ghost button visible, no right column, no eyebrow pill.

- [ ] **Step 5: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(desktop): hero 2-column grid with circular logo and eyebrow pill"
```

---

### Task 3: Servicios Desktop Layout

**Files:**
- Modify: `index.html`

Changes the services grid from 2×2 to 4×1 on desktop. Updates card descriptions to slightly longer text (works on both mobile and desktop). Increases padding and card sizing.

- [ ] **Step 1: Update card descriptions in the `#servicios` section HTML**

Replace the four `.service-card` blocks with:

```html
<div class="service-card">
  <div class="service-card__icon">🏗️</div>
  <div class="service-card__name">Prototipos</div>
  <div class="service-card__desc">Para empresas, startups y makers</div>
</div>
<div class="service-card">
  <div class="service-card__icon">🎨</div>
  <div class="service-card__name">Piezas decorativas</div>
  <div class="service-card__desc">Para el hogar y regalos únicos</div>
</div>
<div class="service-card">
  <div class="service-card__icon">🔧</div>
  <div class="service-card__name">Piezas de repuesto</div>
  <div class="service-card__desc">Fabricadas a tu medida exacta</div>
</div>
<div class="service-card service-card--highlight">
  <div class="service-card__icon">💡</div>
  <div class="service-card__name">Tu idea aquí</div>
  <div class="service-card__desc">Cuéntanos qué necesitas imprimir</div>
</div>
```

- [ ] **Step 2: Add Servicios desktop CSS inside the `@media (min-width: 768px)` block**

```css
  /* Servicios */
  #servicios {
    padding: 80px 64px;
  }

  #servicios .services__grid {
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
  }

  .service-card {
    border-radius: 16px;
    padding: 28px 24px;
    text-align: left;
  }

  .service-card__icon {
    font-size: 32px;
    margin-bottom: 10px;
  }

  .service-card__name {
    font-size: 14px;
    margin-bottom: 6px;
  }

  .service-card__desc {
    font-size: 13px;
  }
```

- [ ] **Step 3: Verify in browser**

Resize to ≥768px.  
Expected: 4 cards in a single row, each with 28px padding, left-aligned text, 32px icon, 16px border-radius.  
At <768px: 2×2 grid, centered text, unchanged.

- [ ] **Step 4: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(desktop): servicios 4-column grid with expanded descriptions"
```

---

### Task 4: ¿Por qué Sozo3D? Desktop Layout

**Files:**
- Modify: `index.html`

Changes the why section from stacked rows to a 3-column card grid. Each card gets `background: #111`, rounded-square icons (52×52px, `border-radius: 14px`) instead of circles.

- [ ] **Step 1: Add Why desktop CSS inside the `@media (min-width: 768px)` block**

```css
  /* Why Sozo3D */
  #why {
    padding: 80px 64px;
  }

  #why .why__list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }

  #why .why__item {
    flex-direction: column;
    align-items: flex-start;
    gap: 16px;
    background: #111;
    border-radius: 16px;
    padding: 28px 24px;
  }

  #why .why__icon {
    width: 52px;
    height: 52px;
    border-radius: 14px;
    font-size: 22px;
  }

  #why .why__text-title {
    font-size: 16px;
  }

  #why .why__text-sub {
    font-size: 13px;
  }
```

- [ ] **Step 2: Verify in browser**

Resize to ≥768px.  
Expected: Three cards side by side with `#111` background. Each card: orange rounded-square icon (52×52, `border-radius: 14px`), bold title, muted subtitle. Column layout within each card (icon on top, text below).  
At <768px: original stacked rows with circular icons, unchanged.

- [ ] **Step 3: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(desktop): why section 3-column cards with square icons"
```

---

### Task 5: CTA Contacto Desktop Layout

**Files:**
- Modify: `index.html`

Restructures CTA into a 2-column grid: large headline+subtitle on the left (`1fr`), WhatsApp button + email stacked and right-aligned (`auto`).

- [ ] **Step 1: Restructure CTA HTML**

The section already has `id="contact"` from Task 1. Replace the full section with:

```html
<section id="contact" class="cta-contact">
  <div class="cta-contact__text">
    <h2 class="cta-contact__title">¿Listo para imprimir?</h2>
    <p class="cta-contact__sub">Escríbenos y te damos presupuesto sin compromiso</p>
  </div>
  <div class="cta-contact__actions">
    <a class="btn--wa" href="https://wa.me/34623020424" target="_blank" rel="noopener noreferrer">
      💬 Escribir por WhatsApp
    </a>
    <a class="cta-contact__email" href="mailto:info@sozo3d.es">✉️ info@sozo3d.es</a>
  </div>
</section>
```

(`cta-contact__text` and `cta-contact__actions` are plain block wrappers on mobile — no mobile CSS needed for them; the section's existing `text-align: center` and button styles still apply.)

- [ ] **Step 2: Add CTA desktop CSS inside the `@media (min-width: 768px)` block**

```css
  /* CTA Contacto */
  #contact {
    display: grid;
    grid-template-columns: 1fr auto;
    align-items: center;
    gap: 64px;
    padding: 80px 64px;
    text-align: left;
  }

  .cta-contact__title {
    font-size: 44px;
    margin-bottom: 12px;
  }

  .cta-contact__sub {
    font-size: 16px;
    margin-bottom: 0;
  }

  .cta-contact__actions {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 16px;
  }

  .cta-contact .btn--wa {
    margin-bottom: 0;
  }
```

- [ ] **Step 3: Verify in browser**

Resize to ≥768px.  
Expected: Left side shows "¿Listo para imprimir?" at 44px and subtitle. Right side shows "💬 Escribir por WhatsApp" (green) and "✉️ info@sozo3d.es" stacked, right-aligned.  
At <768px: centered layout with buttons stacked, unchanged.

- [ ] **Step 4: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(desktop): CTA contacto asymmetric 2-column grid"
```

---

### Task 6: Redes Sociales Desktop Layout

**Files:**
- Modify: `index.html`

Restructures the social section into a 2-column grid: info text + 3Dcalc link on the left, two tall social buttons on the right. Overrides the mobile `text-align: center` on desktop.

- [ ] **Step 1: Restructure social section HTML**

The section already has `id="social"` from Task 1. Replace the full section with:

```html
<section id="social" class="section section--centered">
  <div class="social__info">
    <p class="section__eyebrow">Síguenos</p>
    <h2 class="section__title">Mira lo que hacemos</h2>
    <p class="social__sub">Trabajos, procesos y novedades cada semana</p>
    <a class="social__calc-link" href="https://www.3Dcalc.app" target="_blank" rel="noopener noreferrer">
      🔗 www.3Dcalc.app
    </a>
  </div>
  <div class="social__btns">
    <a class="btn--instagram" href="https://instagram.com/sozo__3d" target="_blank" rel="noopener noreferrer">
      📸 @sozo__3d
    </a>
    <a class="btn--tiktok" href="https://www.tiktok.com/@sozo__3d" target="_blank" rel="noopener noreferrer">
      🎵 @sozo__3d
    </a>
  </div>
</section>
```

(`social__info` is a plain block wrapper on mobile — inherits section's `text-align: center`; no mobile CSS needed for it.)

- [ ] **Step 2: Add social desktop CSS inside the `@media (min-width: 768px)` block**

```css
  /* Redes Sociales */
  #social {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 64px;
    padding: 80px 64px;
    text-align: left;
  }

  #social .social__info {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  #social .section__title {
    font-size: 36px;
    margin-bottom: 12px;
  }

  #social .social__sub {
    font-size: 14px;
    margin-bottom: 16px;
  }

  #social .social__btns {
    display: flex;
    flex-direction: column;
    gap: 16px;
    justify-content: center;
    align-items: stretch;
  }

  #social .btn--instagram,
  #social .btn--tiktok {
    display: block;
    padding: 24px 28px;
    border-radius: 16px;
    font-size: 16px;
    text-align: left;
  }
```

- [ ] **Step 3: Verify in browser**

Resize to ≥768px.  
Expected: Left column — eyebrow "SÍGUENOS", heading "Mira lo que hacemos" (36px), description, 3Dcalc link. Right column — two tall stacked buttons (Instagram gradient, TikTok dark), full-width, left-aligned text.  
At <768px: centered layout with side-by-side social buttons, unchanged.

- [ ] **Step 4: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(desktop): social section 2-column grid with tall buttons"
```

---

### Task 7: Footer Desktop Layout

**Files:**
- Modify: `index.html`

Restructures the footer into a 3-column grid: logo+brand on the left, copyright centered, email right-aligned.

- [ ] **Step 1: Restructure footer HTML**

Replace the full `<footer class="footer">` content with:

```html
<footer class="footer">
  <div class="footer__left">
    <img class="footer__logo" src="assets/Logo_Sozo3D.jpg" alt="Sozo3D" />
    <p class="footer__brand">Sozo<span>3D</span></p>
  </div>
  <p class="footer__copy">© 2026 Sozo3D · Impresión 3D personalizada</p>
  <a class="footer__email" href="mailto:info@sozo3d.es">info@sozo3d.es</a>
</footer>
```

- [ ] **Step 2: Add mobile-base CSS for `footer__left` (inside `<style>`, before the desktop `@media` block)**

```css
/* ── Footer left wrapper (mobile) ── */
.footer__left {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}
```

- [ ] **Step 3: Add footer desktop CSS inside the `@media (min-width: 768px)` block**

```css
  /* Footer */
  .footer {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    align-items: center;
    padding: 48px 64px;
    text-align: left;
  }

  .footer__left {
    flex-direction: row;
    gap: 12px;
  }

  .footer__copy {
    text-align: center;
  }

  .footer__email {
    text-align: right;
    justify-self: end;
  }
```

- [ ] **Step 4: Verify in browser**

Resize to ≥768px.  
Expected: Footer in 3 columns — left: circular logo + "Sozo**3D**" inline; center: "© 2026 Sozo3D · Impresión 3D personalizada"; right: "info@sozo3d.es" right-aligned.  
At <768px: stacked centered layout unchanged.

- [ ] **Step 5: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(desktop): footer 3-column grid"
```
