# Sozo3D — Icon System Design Spec

**Date:** 2026-04-03  
**Status:** Approved  
**Builds on:** `docs/superpowers/specs/2026-04-03-sozo3d-desktop-design.md`

---

## Overview

Replace all emoji characters in `index.html` with an SVG icon system. The goal is a more premium, consistent visual language. All icons are embedded via an **SVG sprite** (`<defs>` block) at the top of `<body>` and referenced with `<use href="#icon-name">`. Zero external dependencies.

---

## Icon Style

### Card / Section icons (Servicios, Why)
- White filled SVG on an orange square background
- Size: 40px × 40px container, `border-radius: 10px`, `background: #E87722`
- Icon size: 20px × 20px, `fill: white`

### Why section icons (desktop: 48px container)
- Same style as card icons but larger: 48px × 48px, `border-radius: 13px`
- Icon size: 24px × 24px, `fill: white`

### Button icons (inline, before text)
- 16px × 16px, `fill: white`, displayed as `<svg>` inline within button
- No background, no container — icon sits directly before the label text

### Social button icons (Instagram, TikTok)
- 20px × 20px, `fill: white`, no container

---

## Icon Mapping

### SVG Sprite IDs

| ID | Used for | SVG path description |
|---|---|---|
| `#icon-wa` | All WhatsApp buttons (×3) | WhatsApp brand logo |
| `#icon-envelope` | Email button | Envelope / mail |
| `#icon-layers` | Prototipos service card | Stacked layers |
| `#icon-sparkle` | Piezas decorativas card | 5-point star/sparkle |
| `#icon-wrench` | Piezas de repuesto card | Wrench/tool |
| `#icon-arrow-right` | Tu idea aquí card | Right-pointing arrow |
| `#icon-bolt` | Entrega rápida (Why) | Lightning bolt |
| `#icon-crosshair` | Alta precisión (Why) | Crosshair/target |
| `#icon-chat` | Atención directa (Why) | Filled speech bubble |
| `#icon-download` | 3Dcalc.app button | Download arrow |
| `#icon-instagram` | Instagram button | Instagram brand logo |
| `#icon-tiktok` | TikTok button | TikTok brand logo |

---

## Element-by-Element Changes

### Navbar desktop — WhatsApp CTA
**Before:** `💬 WhatsApp`  
**After:** `<svg use="#icon-wa" 16px> WhatsApp`

### Mobile hero nav — WhatsApp CTA
**Before:** `📱 WhatsApp`  
**After:** `<svg use="#icon-wa" 16px> WhatsApp`

### Hero — primary CTA button
**Before:** `💬 Pedir presupuesto`  
**After:** `<svg use="#icon-wa" 16px> Pedir presupuesto`

### Servicios — service card icons
Replace `.service-card__icon` emoji divs with SVG sprite references:

| Card | Before | After |
|---|---|---|
| Prototipos | `🏗️` | `<use href="#icon-layers">` in orange container |
| Piezas decorativas | `🎨` | `<use href="#icon-sparkle">` in orange container |
| Piezas de repuesto | `🔧` | `<use href="#icon-wrench">` in orange container |
| Tu idea aquí | `💡` | `<use href="#icon-arrow-right">` in orange container |

### Why Sozo3D — why__icon divs
Replace emoji content with SVG sprite references:

| Item | Before | After |
|---|---|---|
| Entrega rápida | `⚡` | `<use href="#icon-bolt">` |
| Alta precisión | `🎯` | `<use href="#icon-crosshair">` |
| Atención directa | `💬` | `<use href="#icon-chat">` |

### CTA Contacto — WhatsApp button
**Before:** `💬 Escribir por WhatsApp`  
**After:** `<svg use="#icon-wa" 16px> Escribir por WhatsApp`

### CTA Contacto — email link → button
**Before:** `<a class="cta-contact__email">✉️ info@sozo3d.es</a>` (underline text link)  
**After:** `<a class="btn--email">` pill button styled as:
- `display: inline-flex`, `align-items: center`, `gap: 8px`
- `background: rgba(255,255,255,0.15)`, `border: 1px solid rgba(255,255,255,0.35)`
- `color: #fff`, `padding: 13px 22px`, `border-radius: 30px`
- Contains `<svg use="#icon-envelope" 15px>` + `info@sozo3d.es`
- Remove old `.cta-contact__email` CSS rule (no longer needed)

### Redes Sociales — 3Dcalc.app link → card button
**Before:** `<a class="social__calc-link">🔗 www.3Dcalc.app</a>` (underline text link)  
**After:** `<a class="btn--calc">` card button styled as:
- `display: flex`, `align-items: center`, `gap: 12px`
- `background: #1a1a1a`, `border: 1px solid #2a2a2a`, `border-radius: 14px`
- `padding: 18px 22px`, `width: 100%` (on desktop, `align-self: flex-start`)
- Left: icon container (36×36px, `background: rgba(232,119,34,0.18)`, `border-radius: 8px`) with `<svg use="#icon-download" 18px fill:#E87722>`
- Right: two text lines stacked:
  - Line 1 (label): `"Descarga nuestra app"` — `font-size: 14px`, `font-weight: 600`, `color: #fff`
  - Line 2 (url): `"www.3Dcalc.app"` — `font-size: 11px`, `color: #E87722`
- Remove old `.social__calc-link` CSS rule (no longer needed)

### Redes Sociales — Instagram button
**Before:** `📸 @sozo__3d`  
**After:** `<svg use="#icon-instagram" 20px> @sozo__3d`

### Redes Sociales — TikTok button
**Before:** `🎵 @sozo__3d`  
**After:** `<svg use="#icon-tiktok" 20px> @sozo__3d`

---

## CSS Changes

### New rules to add
```css
/* ── Email button (CTA section) ── */
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

/* ── 3Dcalc card button (social section) ── */
.btn--calc {
  display: flex;
  align-items: center;
  gap: 12px;
  background: var(--black2);
  border: 1px solid #2a2a2a;
  border-radius: 14px;
  padding: 18px 22px;
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
  font-size: 14px;
  font-weight: 600;
  color: var(--white);
}

.btn--calc__url {
  font-size: 11px;
  color: var(--orange);
  margin-top: 1px;
}

/* ── Card / Why icon container ── */
.service-card__icon {
  width: 40px;
  height: 40px;
  background: var(--orange);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 10px;  /* was: 6px */
}
.service-card__icon svg {
  width: 20px;
  height: 20px;
  fill: var(--white);
}

.why__icon svg {
  width: 20px;
  height: 20px;
  fill: var(--white);
}
```

### Rules to remove or update
- `.cta-contact__email` — remove entirely (replaced by `.btn--email`)
- `.social__calc-link` — remove entirely (replaced by `.btn--calc`)
- `.why__icon` — remove `font-size: 17px` from mobile CSS (emoji sizing); keep `width`, `height`, `background`, `border-radius`, flex properties
- `#why .why__icon` in desktop `@media` block — remove `font-size: 22px` (SVG size is controlled by `svg { width; height }` inside the container, not `font-size`)
- `.service-card__icon` in desktop `@media` block — remove `font-size: 32px` (same reason); `margin-bottom: 10px` can stay
- `.btn--wa` mobile rule has `margin-bottom: 16px` — this was used to space the WA button from the underline email link below it in the CTA section. Now both elements are pill buttons, spacing is handled by `.cta-contact__actions { gap: 16px }` on desktop. On mobile, the WA button's `margin-bottom: 16px` still provides separation between the two buttons. No change needed here.

---

## Technical Approach

- **SVG sprite** — single `<svg style="display:none">` block with `<defs>` containing all 12 `<symbol>` definitions, placed immediately after `<body>`.
- **Usage pattern** — `<svg class="icon"><use href="#icon-name"></use></svg>` everywhere.
- **No external CDN** — all SVG paths inline in the HTML.
- **Single file** — all changes in `index.html` only.
- **Additive** — new CSS classes added; old emoji-only styles replaced where needed.

---

## Out of Scope

- Changing icon colors other than white/orange
- Hover animations on icons
- Dark/light mode variants
- Any layout changes beyond what's described above
