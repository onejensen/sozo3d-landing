# Sozo3D Icon System Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace all emoji characters in `index.html` with a consistent SVG icon system — filled white icons on orange backgrounds for cards, small inline icons for buttons, and two upgraded link-to-button conversions (email + 3Dcalc).

**Architecture:** A single `<svg style="display:none">` sprite block with 12 `<symbol>` definitions is placed as the first child of `<body>`. All icons are referenced with `<use href="#icon-name">`. CSS is updated to style icon containers and remove emoji-specific rules. No external dependencies added.

**Tech Stack:** HTML5 inline SVG sprite, CSS (existing file), no build step.

---

## File Structure

- **Modify only:** `index.html`
  - Body: add SVG sprite block before `.page` div
  - CSS `<style>`: update `.service-card__icon`, `.why__icon`; remove `.cta-contact__email` and `.social__calc-link`; add `.btn--email`, `.btn--calc`, `.btn--calc__icon`, `.btn--calc__label`, `.btn--calc__url`; update desktop overrides to remove `font-size` properties
  - HTML sections: replace emoji strings and upgrade two links to card/pill buttons

---

### Task 1: SVG Sprite Block

**Files:**
- Modify: `index.html`

Adds the hidden SVG sprite containing all 12 icon symbols. Place it immediately after the opening `<body>` tag, before `<nav class="navbar--desktop">`.

- [ ] **Step 1: Insert the sprite block**

Find the line `<body>` and immediately after it insert:

```html
<!-- ══ SVG Icon Sprite ══ -->
<svg style="display:none" xmlns="http://www.w3.org/2000/svg">
  <symbol id="icon-wa" viewBox="0 0 24 24">
    <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347zM12 0C5.373 0 0 5.373 0 12c0 2.136.558 4.14 1.534 5.876L0 24l6.31-1.518A11.934 11.934 0 0012 24c6.627 0 12-5.373 12-12S18.627 0 12 0zm0 21.818a9.797 9.797 0 01-4.997-1.371l-.358-.214-3.747.901.947-3.638-.234-.374A9.773 9.773 0 012.182 12C2.182 6.57 6.569 2.182 12 2.182S21.818 6.57 21.818 12 17.431 21.818 12 21.818z"/>
  </symbol>
  <symbol id="icon-envelope" viewBox="0 0 24 24">
    <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
  </symbol>
  <symbol id="icon-layers" viewBox="0 0 24 24">
    <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
  </symbol>
  <symbol id="icon-sparkle" viewBox="0 0 24 24">
    <path d="M12 2l2.4 7.4H22l-6.2 4.5 2.4 7.4L12 17l-6.2 4.3 2.4-7.4L2 9.4h7.6z"/>
  </symbol>
  <symbol id="icon-wrench" viewBox="0 0 24 24">
    <path d="M22.7 19l-9.1-9.1c.9-2.3.4-5-1.5-6.9-2-2-5-2.4-7.4-1.3L9 6 6 9 1.6 4.7C.4 7.1.9 10.1 2.9 12.1c1.9 1.9 4.6 2.4 6.9 1.5l9.1 9.1c.4.4 1 .4 1.4 0l2.3-2.3c.5-.4.5-1.1.1-1.4z"/>
  </symbol>
  <symbol id="icon-arrow-right" viewBox="0 0 24 24">
    <path d="M12 4l-1.41 1.41L16.17 11H4v2h12.17l-5.58 5.59L12 20l8-8z"/>
  </symbol>
  <symbol id="icon-bolt" viewBox="0 0 24 24">
    <path d="M7 2v11h3v9l7-12h-4l4-8z"/>
  </symbol>
  <symbol id="icon-crosshair" viewBox="0 0 24 24">
    <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-1 17.93V18h2v1.93c-3.06-.45-5.48-2.87-5.93-5.93H9v-2H7.07C7.52 8.94 9.94 6.52 13 6.07V8h2V6.07c3.06.45 5.48 2.87 5.93 5.93H19v2h1.93c-.45 3.06-2.87 5.48-5.93 5.93zM13 13h-2v-2h2v2z"/>
  </symbol>
  <symbol id="icon-chat" viewBox="0 0 24 24">
    <path d="M20 2H4c-1.1 0-2 .9-2 2v18l4-4h14c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2z"/>
  </symbol>
  <symbol id="icon-download" viewBox="0 0 24 24">
    <path d="M19 9h-4V3H9v6H5l7 7 7-7zm-8 2V5h2v6h1.17L12 13.17 9.83 11H11zm-6 7v2h14v-2H5z"/>
  </symbol>
  <symbol id="icon-instagram" viewBox="0 0 24 24">
    <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
  </symbol>
  <symbol id="icon-tiktok" viewBox="0 0 24 24">
    <path d="M19.59 6.69a4.83 4.83 0 01-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 01-2.88 2.5 2.89 2.89 0 01-2.89-2.89 2.89 2.89 0 012.89-2.89c.28 0 .54.04.79.1V9.01a6.27 6.27 0 00-.79-.05 6.34 6.34 0 00-6.34 6.34 6.34 6.34 0 006.34 6.34 6.34 6.34 0 006.33-6.34V8.69a8.18 8.18 0 004.78 1.52V6.76a4.85 4.85 0 01-1.01-.07z"/>
  </symbol>
</svg>
```

- [ ] **Step 2: Verify sprite is hidden**

Open `index.html` in browser. The page should look identical to before — no visible SVG block at top.

- [ ] **Step 3: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(icons): add SVG sprite with 12 icon symbols"
```

---

### Task 2: CSS Updates

**Files:**
- Modify: `index.html`

Updates existing CSS rules to support SVG icons (remove emoji font-size rules, add flex containers) and adds new classes for `.btn--email` and `.btn--calc`.

- [ ] **Step 1: Replace `.service-card__icon` mobile CSS**

Find and replace (lines ~177–180):
```css
    .service-card__icon {
      font-size: 24px;
      margin-bottom: 6px;
    }
```
Replace with:
```css
    .service-card__icon {
      width: 40px;
      height: 40px;
      background: var(--orange);
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 10px;
    }
    .service-card__icon svg {
      width: 20px;
      height: 20px;
      fill: var(--white);
    }
```

- [ ] **Step 2: Update `.why__icon` mobile CSS — remove `font-size`, add svg rule**

Find (lines ~212–222):
```css
    .why__icon {
      width: 38px;
      height: 38px;
      background: var(--orange);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 17px;
      flex-shrink: 0;
    }
```
Replace with:
```css
    .why__icon {
      width: 38px;
      height: 38px;
      background: var(--orange);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
    }
    .why__icon svg {
      width: 20px;
      height: 20px;
      fill: var(--white);
    }
```

- [ ] **Step 3: Replace `.cta-contact__email` with `.btn--email`**

Find (lines ~270–277):
```css
    .cta-contact__email {
      display: inline-block;
      color: rgba(255,255,255,0.85);
      font-size: 13px;
      font-weight: 500;
      border-bottom: 1px solid rgba(255,255,255,0.5);
      padding-bottom: 2px;
    }
```
Replace with:
```css
    .btn--email {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: rgba(255, 255, 255, 0.15);
      border: 1px solid rgba(255, 255, 255, 0.35);
      color: var(--white);
      font-family: var(--font);
      font-size: 13px;
      font-weight: 600;
      padding: 13px 22px;
      border-radius: 30px;
    }
    .btn--email svg {
      width: 15px;
      height: 15px;
      fill: var(--white);
      flex-shrink: 0;
    }
```

- [ ] **Step 4: Replace `.social__calc-link` with `.btn--calc` and children**

Find (lines ~292–300):
```css
    .social__calc-link {
      display: inline-block;
      color: var(--orange);
      font-size: 13px;
      font-weight: 600;
      border-bottom: 1px solid var(--orange);
      padding-bottom: 2px;
      margin-bottom: 18px;
    }
```
Replace with:
```css
    .btn--calc {
      display: flex;
      align-items: center;
      gap: 12px;
      background: var(--black2);
      border: 1px solid #2a2a2a;
      border-radius: 14px;
      padding: 18px 22px;
      margin-bottom: 18px;
    }
    .btn--calc__icon {
      width: 36px;
      height: 36px;
      background: rgba(232, 119, 34, 0.18);
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
    }
    .btn--calc__icon svg {
      width: 18px;
      height: 18px;
      fill: var(--orange);
    }
    .btn--calc__label {
      display: block;
      font-size: 14px;
      font-weight: 600;
      color: var(--white);
    }
    .btn--calc__url {
      display: block;
      font-size: 11px;
      color: var(--orange);
      margin-top: 1px;
    }
```

- [ ] **Step 5: Clean up desktop `@media` overrides — remove emoji font-size rules**

Inside the `@media (min-width: 768px)` block, find:
```css
      .service-card__icon {
        font-size: 32px;
        margin-bottom: 10px;
      }
```
Replace with (remove `font-size`, keep `margin-bottom`):
```css
      .service-card__icon {
        margin-bottom: 10px;
      }
```

Then find:
```css
      #why .why__icon {
        width: 52px;
        height: 52px;
        border-radius: 14px;
        font-size: 22px;
      }
```
Replace with (remove `font-size`, add svg sizing for desktop):
```css
      #why .why__icon {
        width: 52px;
        height: 52px;
        border-radius: 14px;
      }
      #why .why__icon svg {
        width: 24px;
        height: 24px;
      }
```

- [ ] **Step 6: Update `.btn--wa` to use `inline-flex` (needed for icon alignment)**

Find:
```css
    .btn--wa {
      display: inline-block;
```
Replace with:
```css
    .btn--wa {
      display: inline-flex;
      align-items: center;
      gap: 8px;
```

Do the same for `.btn--primary` and `.btn--ghost` — change `display: inline-block` to `display: inline-flex; align-items: center; gap: 8px;` on each.

- [ ] **Step 7: Verify in browser**

Open `index.html` — page should look the same as before this task (no icons visible yet since HTML still has emoji). Orange-background squares should appear on service cards once Task 3 is done.

- [ ] **Step 8: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(icons): update CSS — icon containers, btn--email, btn--calc"
```

---

### Task 3: Card and Section Icons

**Files:**
- Modify: `index.html`

Replaces the 4 service card emoji icon divs and 3 why section emoji icon divs with SVG `<use>` references.

- [ ] **Step 1: Replace service card icon divs**

In `#servicios`, find and replace all four `.service-card__icon` divs:

```html
<!-- Prototipos — was: <div class="service-card__icon">🏗️</div> -->
<div class="service-card__icon">
  <svg aria-hidden="true"><use href="#icon-layers"></use></svg>
</div>

<!-- Piezas decorativas — was: <div class="service-card__icon">🎨</div> -->
<div class="service-card__icon">
  <svg aria-hidden="true"><use href="#icon-sparkle"></use></svg>
</div>

<!-- Piezas de repuesto — was: <div class="service-card__icon">🔧</div> -->
<div class="service-card__icon">
  <svg aria-hidden="true"><use href="#icon-wrench"></use></svg>
</div>

<!-- Tu idea aquí — was: <div class="service-card__icon">💡</div> -->
<div class="service-card__icon">
  <svg aria-hidden="true"><use href="#icon-arrow-right"></use></svg>
</div>
```

Note: the `<svg>` here has no explicit width/height — those are set by `.service-card__icon svg { width: 20px; height: 20px; }` from Task 2.

- [ ] **Step 2: Replace why section icon divs**

In `#why`, find and replace all three `.why__icon` divs:

```html
<!-- Entrega rápida — was: <div class="why__icon">⚡</div> -->
<div class="why__icon">
  <svg aria-hidden="true"><use href="#icon-bolt"></use></svg>
</div>

<!-- Alta precisión — was: <div class="why__icon">🎯</div> -->
<div class="why__icon">
  <svg aria-hidden="true"><use href="#icon-crosshair"></use></svg>
</div>

<!-- Atención directa — was: <div class="why__icon">💬</div> -->
<div class="why__icon">
  <svg aria-hidden="true"><use href="#icon-chat"></use></svg>
</div>
```

- [ ] **Step 3: Verify in browser**

Open `index.html`. Service cards should show white icons (layers, sparkle, wrench, arrow) on orange 40px rounded squares. Why section should show bolt, crosshair, chat bubble on orange circles (mobile) or orange rounded squares (desktop ≥768px).

- [ ] **Step 4: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(icons): replace card and why section emojis with SVG icons"
```

---

### Task 4: Buttons, Email, and 3Dcalc

**Files:**
- Modify: `index.html`

Replaces all remaining emoji occurrences: WhatsApp icons in 3 buttons, Instagram/TikTok icons in social buttons, email link upgraded to `.btn--email` pill, 3Dcalc link upgraded to `.btn--calc` card.

The inline SVG pattern for buttons is:
```html
<svg aria-hidden="true"><use href="#icon-name"></use></svg>
```
(Size controlled by CSS on the parent button's `svg` selector, or inline width/height where needed.)

- [ ] **Step 1: Add `svg` sizing rules to button classes**

Inside `<style>`, after `.btn--wa { ... }`, add:
```css
    .btn--wa svg,
    .btn--primary svg {
      width: 16px;
      height: 16px;
      fill: var(--white);
      flex-shrink: 0;
    }
```

After `.btn--instagram { ... }` and `.btn--tiktok { ... }`, add:
```css
    .btn--instagram svg,
    .btn--tiktok svg {
      width: 18px;
      height: 18px;
      fill: var(--white);
      flex-shrink: 0;
    }
```

Also add inside the navbar CTA selector area (the `.navbar--desktop__cta` is a plain anchor — add a rule for its svg):
```css
    .navbar--desktop__cta svg {
      width: 14px;
      height: 14px;
      fill: var(--white);
      flex-shrink: 0;
    }
```

- [ ] **Step 2: Replace desktop navbar WhatsApp CTA**

Find:
```html
    💬 WhatsApp
```
(inside `<a class="navbar--desktop__cta">`)

Replace with:
```html
    <svg aria-hidden="true"><use href="#icon-wa"></use></svg>
    WhatsApp
```

- [ ] **Step 3: Replace mobile hero nav WhatsApp CTA**

Find:
```html
      📱 WhatsApp
```
(inside `<a class="hero__nav-cta">`)

Replace with:
```html
      <svg aria-hidden="true"><use href="#icon-wa"></use></svg>
      WhatsApp
```

- [ ] **Step 4: Replace hero primary CTA button**

Find:
```html
        💬 Pedir presupuesto
```
(inside `<a class="btn--primary">`)

Replace with:
```html
        <svg aria-hidden="true"><use href="#icon-wa"></use></svg>
        Pedir presupuesto
```

- [ ] **Step 5: Replace CTA section WhatsApp button**

Find:
```html
      💬 Escribir por WhatsApp
```
(inside `<a class="btn--wa">` in `#contact`)

Replace with:
```html
      <svg aria-hidden="true"><use href="#icon-wa"></use></svg>
      Escribir por WhatsApp
```

- [ ] **Step 6: Upgrade email link to `.btn--email`**

Find the entire `<a class="cta-contact__email" ...>` element:
```html
        <a class="cta-contact__email" href="mailto:info@sozo3d.es">✉️ info@sozo3d.es</a>
```

Replace with:
```html
        <a class="btn--email" href="mailto:info@sozo3d.es">
          <svg aria-hidden="true"><use href="#icon-envelope"></use></svg>
          info@sozo3d.es
        </a>
```

- [ ] **Step 7: Replace Instagram button emoji**

Find:
```html
      📸 @sozo__3d
```
(inside `<a class="btn--instagram">`)

Replace with:
```html
      <svg aria-hidden="true"><use href="#icon-instagram"></use></svg>
      @sozo__3d
```

- [ ] **Step 8: Replace TikTok button emoji**

Find:
```html
      🎵 @sozo__3d
```
(inside `<a class="btn--tiktok">`)

Replace with:
```html
      <svg aria-hidden="true"><use href="#icon-tiktok"></use></svg>
      @sozo__3d
```

- [ ] **Step 9: Upgrade 3Dcalc link to `.btn--calc` card**

Find the entire `<a class="social__calc-link" ...>` element:
```html
    <a class="social__calc-link" href="https://www.3Dcalc.app" target="_blank" rel="noopener noreferrer">
      🔗 www.3Dcalc.app
    </a>
```

Replace with:
```html
    <a class="btn--calc" href="https://www.3Dcalc.app" target="_blank" rel="noopener noreferrer">
      <div class="btn--calc__icon">
        <svg aria-hidden="true"><use href="#icon-download"></use></svg>
      </div>
      <div>
        <span class="btn--calc__label">Descarga nuestra app</span>
        <span class="btn--calc__url">www.3Dcalc.app</span>
      </div>
    </a>
```

- [ ] **Step 10: Verify — no emoji remaining**

Run this to confirm zero emoji left in the HTML:

```bash
grep -P "[\x{1F300}-\x{1F9FF}]|[\x{2600}-\x{26FF}]|📱|💬|🏗|🎨|🔧|💡|⚡|🎯|📸|🎵|🔗|✉" "/Users/onejensen/Documents/MIS WEBS/Sozo3D/index.html"
```

Expected: no output (zero matches).

Open `index.html` in browser and verify:
- All buttons show icon + text (no emoji, no broken SVG squares)
- CTA section: green WA button with icon + frosted white email button with envelope icon
- Social section: calc card button (dark, download icon, "Descarga nuestra app" + orange URL), then Instagram + TikTok buttons with brand icons

- [ ] **Step 11: Commit**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git add index.html
git commit -m "feat(icons): replace all button emojis, upgrade email and 3Dcalc to SVG buttons"
```

---

### Task 5: Push to GitHub

**Files:**
- No file changes

- [ ] **Step 1: Push to deploy**

```bash
cd "/Users/onejensen/Documents/MIS WEBS/Sozo3D"
git push origin main
```

Expected: push succeeds, GitHub Pages auto-deploys within ~60 seconds to `https://onejensen.github.io/sozo3d-landing/`.
