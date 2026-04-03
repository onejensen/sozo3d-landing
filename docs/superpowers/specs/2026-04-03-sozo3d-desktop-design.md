# Sozo3D — Desktop Layout Design Spec

**Date:** 2026-04-03  
**Status:** Approved  
**Builds on:** `docs/superpowers/specs/2026-04-03-sozo3d-landing-design.md`

---

## Overview

Add a full desktop layout to the existing `index.html` using CSS media queries (`min-width: 768px`). The mobile layout remains unchanged. All desktop styles are additive — no mobile CSS is modified.

The chosen approach is **Editorial Full-Width (Option A)**: wide content sections (max-width 1280px), two-column hero, horizontal why-section, asymmetric CTA and social layouts.

---

## Desktop Breakpoint

`@media (min-width: 768px)` — applies to all desktop/tablet layouts.  
Content max-width: `1280px`, centered with `margin: 0 auto`, padding `0 64px`.

---

## Section-by-Section Desktop Layout

### Navbar (new on desktop)
- Sticky, `backdrop-filter: blur(12px)`, height `64px`, padding `0 64px`
- Left: logo circular (44px) + brand name "Sozo**3D**"
- Center/right: nav links — Servicios · ¿Por qué nosotros? · Síguenos · Contacto
- Far right: "💬 WhatsApp" pill button (orange)
- On mobile: navbar stays as current (logo + brand + WhatsApp pill, no nav links)

### ① Hero
- Grid `1fr 1fr`, gap `64px`, padding `100px 64px 80px`, min-height `520px`
- **Left:** eyebrow pill badge · headline 72px · subtitle · single CTA button "💬 Pedir presupuesto"
  - Ghost "Ver trabajos ↓" button **removed**
- **Right:** Logo `Logo_Sozo3D.jpg`, 340×340px circular, `box-shadow: 0 0 80px rgba(232,119,34,0.3)`, border `3px solid rgba(232,119,34,0.4)`

### ② Servicios
- Padding `80px 64px`
- Section header: eyebrow + h2 (left-aligned)
- Cards grid: `repeat(4, 1fr)`, gap `16px` — same 4 cards, expanded with longer descriptions
- Cards: `border-radius: 16px`, padding `28px 24px`, icon `32px`

### ③ ¿Por qué Sozo3D?
- Padding `80px 64px`
- 3-column grid (`repeat(3, 1fr)`) instead of stacked rows
- Icons change from circles to `border-radius: 14px` squares (52×52px)
- Each item in its own card with background `#111`

### ④ CTA Contacto
- Grid `1fr auto`, padding `80px 64px`
- **Left:** large headline "¿Listo para imprimir?" (44px) + subtitle
- **Right:** WhatsApp button + email link (stacked, right-aligned)

### ⑤ Redes Sociales
- Grid `1fr 1fr`, gap `64px`, padding `80px 64px`
- **Left:** eyebrow + h2 + description + 3Dcalc.app link
- **Right:** two tall social buttons (Instagram + TikTok) with icon · handle · label · arrow

### ⑥ Footer
- 3-column grid: logo+brand (left) · copyright (center) · email (right)
- Padding `48px 64px`

---

## Technical Approach

- **Single file** — all desktop CSS added inside `<style>` in `index.html` within a `@media (min-width: 768px)` block
- **Additive only** — no mobile CSS removed or modified
- **`.page` wrapper** — on desktop, `max-width` lifted to `1280px`; the existing `480px` limit only applies on mobile
- **Navbar** — hidden on mobile (current navbar stays), shown on desktop via a new `<nav class="navbar--desktop">` element that is `display: none` on mobile and `display: flex` on desktop

---

## Out of Scope

- Animations or scroll effects
- Dark/light mode toggle
- Any changes to mobile layout
