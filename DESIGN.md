---
name: Sozo3D
description: A flat-printed product sleeve for a Spanish 3D printing service — absolute black, one orange, and density as the material.
colors:
  ink: "#000000"
  ink-2: "#171717"
  ink-3: "#080808"
  orange: "#E87722"
  white: "#FFFFFF"
  muted: "#8C8C8C"
  rule: "#2E2E2E"
typography:
  display:
    fontFamily: "Big Shoulders Display, Arial Narrow, sans-serif"
    fontSize: "clamp(5.2rem, 25vw, 20rem)"
    fontWeight: 900
    lineHeight: 0.78
    letterSpacing: "-0.005em"
  display-2:
    fontFamily: "Big Shoulders Display, Arial Narrow, sans-serif"
    fontSize: "clamp(2.1rem, 8.4vw, 6.6rem)"
    fontWeight: 800
    lineHeight: 0.84
    letterSpacing: "0.005em"
  headline:
    fontFamily: "Big Shoulders Display, Arial Narrow, sans-serif"
    fontSize: "clamp(2.1rem, 6vw, 4.2rem)"
    fontWeight: 800
    lineHeight: 0.88
    letterSpacing: "0.005em"
  title:
    fontFamily: "Big Shoulders Display, Arial Narrow, sans-serif"
    fontSize: "clamp(1.35rem, 2.4vw, 1.85rem)"
    fontWeight: 800
    lineHeight: 1
    letterSpacing: "0.01em"
  mark-code:
    fontFamily: "Martian Mono, ui-monospace, monospace"
    fontSize: "clamp(15px, 1.5vw, 19px)"
    fontWeight: 700
    lineHeight: 1
    letterSpacing: "-0.01em"
  body:
    fontFamily: "Archivo, system-ui, sans-serif"
    fontSize: "16px"
    fontWeight: 400
    lineHeight: 1.55
    letterSpacing: "normal"
  small:
    fontFamily: "Archivo, system-ui, sans-serif"
    fontSize: "14px"
    fontWeight: 400
    lineHeight: 1.55
    letterSpacing: "normal"
  label:
    fontFamily: "Martian Mono, ui-monospace, monospace"
    fontSize: "11px"
    fontWeight: 500
    lineHeight: 1.55
    letterSpacing: "0.04em"
  code:
    fontFamily: "Martian Mono, ui-monospace, monospace"
    fontSize: "10.5px"
    fontWeight: 400
    lineHeight: 1.55
    letterSpacing: "0.02em"
rounded:
  none: "0px"
spacing:
  hair: "1px"
  pad: "16px"
  pad-md: "22px"
  pad-lg: "30px"
  rail: "46px"
  bay: "52px"
  bay-lg: "60px"
  bay-sm: "64px"
components:
  control-fill:
    backgroundColor: "{colors.orange}"
    textColor: "{colors.ink}"
    typography: "{typography.label}"
    rounded: "{rounded.none}"
    padding: "13px 22px"
  control-fill-hover:
    backgroundColor: "{colors.white}"
    textColor: "{colors.ink}"
  control-outline:
    backgroundColor: "transparent"
    textColor: "{colors.orange}"
    typography: "{typography.label}"
    rounded: "{rounded.none}"
    padding: "13px 22px"
  control-outline-hover:
    backgroundColor: "{colors.orange}"
    textColor: "{colors.ink}"
  cell:
    backgroundColor: "{colors.ink-2}"
    textColor: "{colors.white}"
    rounded: "{rounded.none}"
    padding: "22px 20px 24px"
  part-card:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.white}"
    rounded: "{rounded.none}"
    padding: "13px 14px 16px"
  nav-link:
    textColor: "{colors.muted}"
    typography: "{typography.label}"
    padding: "5px 0"
  nav-link-hover:
    textColor: "{colors.white}"
---

# Design System: Sozo3D

## Overview

**Creative North Star: "The Printed Sleeve"**

The page is a piece of flat industrial print: a product sleeve for a printing service, where density itself is the material. Every surface behaves like ink on stock — hairline rules that run to the page edges, cells that butt against their neighbours with a 1px gutter, marks stamped into the margins, and one enormous condensed word shouting through the middle of it. Nothing here imitates a screen appliance. There are no gradients anywhere in the build, no glow, no shadow, no rounded corner, and no illuminated surface; depth is made only by tone and by rule.

The palette is closed and inherited: the site's own black, its own `#171717`, its own brand orange, white, and one grey. The build's source world carried a magenta and a safety orange; both were collapsed into the single pinned brand orange before a line was written, so the page has exactly one hot colour and it never competes with itself. Ornament is a system rather than decoration: hazard stripes, halftone screens, ruler scales, registration crosses, roundels and barcodes are all drawn SVG in one consistent weight, and every barcode on a cell is generated deterministically from that cell's own ID string, so no two marks repeat and none of them is arbitrary.

The world it explicitly refuses is the one it replaced: the dark hero with an orange gradient wash and a grid of soft icon cards. That arrangement is not a style option here; it is the anti-reference. The offer and the action must survive the density — the email control is present in the sticky strip, in the first viewport, and in the CTA band, and it never gets buried by ornament.

**Key Characteristics:**
- Absolute black ground, never flat: a low-density orange halftone grain runs fixed behind the whole sheet.
- Exactly one accent colour, `#E87722`, on marks, codes, controls and second lines.
- Zero radius, zero gradient, zero glow, zero shadow. 1px hairlines build the entire frame.
- Three type roles with hard boundaries: condensed display shouts, Archivo speaks, mono measures.
- All ornament is drawn SVG at one weight; hazard, tone and scale are `<pattern>` fills.
- Ornament drops in declared density tiers as the viewport narrows; the display word never drops below its floor.

## Colors

A closed, inherited palette: two blacks, one grey, white, and a single brand orange that carries every accent on the page.

### Primary
- **Brand Orange** (#E87722): The only hot colour in the system. It carries the marking layer (codes, refs, labels, hazard stripes, halftone dots, registration crosses, roundels, barcodes in the rails), the second line of the headline, the emphasis span inside every section heading, the filled and outlined controls, and every browser surface the page themes (selection, caret, `accent-color`, focus ring, scrollbar thumb hover). Its ubiquity is structural, not decorative: it is the ink the marks are printed in.

### Neutral
- **Absolute Black** (#000000): The ground. Body background, the sticky code strip, the vertical rails, affiliate cards, channel rows, and the reversed text colour inside filled orange controls.
- **Second Black** (#171717): The site's own incumbent dark. The panel surface — service and reason cells, the CTA band, and the hover state of affiliate and channel rows. It is the only lift the system has.
- **Reserve Black** (#080808): Declared in the palette as part of the pinned inherited set and held closed against new colours; it is not applied anywhere in this build.
- **Rule Grey** (#2E2E2E): Every hairline. Section borders, cell gutters, grid backgrounds, chip outlines, and the scrollbar thumb. It is a line colour, never a fill for content.
- **Mark White** (#FFFFFF): Body prose, the shouting word, headings, cell names and values, and the hover state of the filled control. It reads as the page's paper, not as a highlight.
- **Muted Grey** (#8C8C8C): Secondary prose — cell descriptions, disclosure text, footer meta, nav links at rest, vertical rail type, and dimmed codes. Raised from the incumbent site's grey specifically to clear 4.5:1 on black.

### Named Rules
**The Closed Palette Rule.** These are the only colours in this system. The palette is the incumbent site's own tokens, pinned by the owner; no second hot colour, no secondary accent, and no new hue may enter a future surface. If a new state needs distinguishing, distinguish it with tone, rule weight, or mark — not with a colour.

**The One Ink Rule.** Orange is the marking ink. It prints codes, rules, patterns and controls. It never fills a large field, never sits behind body prose, and never appears as a gradient, tint ramp or glow.

## Typography

**Display Font:** Big Shoulders Display (with Arial Narrow fallback)
**Body Font:** Archivo (with system-ui fallback)
**Label/Mono Font:** Martian Mono (with ui-monospace fallback)

**Character:** A heavy condensed grotesque that shouts, a neutral workhorse that explains, and a wide mono that measures. The pairing reads as industrial packaging: the display face is the screen-printed word on the sleeve, the mono is the stamped batch marking, and Archivo is the only voice permitted to speak in sentences.

### Hierarchy

The ramp is exactly ten steps. Every size on the page is one of them, each with a distinct job and no near-duplicates; a new size is a ramp change, not a local adjustment.

- **Display** (900, `clamp(5.2rem, 25vw, 20rem)`, 0.78): The single shouting word in the first viewport, uppercase, white.
- **Display Second Line** (800, `clamp(2.1rem, 8.4vw, 6.6rem)`, 0.84): The orange line beneath the shout. A distinct step between the shout and the section headings — it must read as the same utterance as the word above it, and as larger than any heading below it.
- **Headline** (800, `clamp(2.1rem, 6vw, 4.2rem)`, 0.88–0.9): Section headings and the CTA band title, uppercase, white with one orange emphasis phrase. The CTA title shares this step rather than carrying its own.
- **Lockup** (800, 22px, 1): The brand wordmark, in the sticky strip and in the footer. Both instances share the step because they are the same role.
- **Title** (800, `clamp(1.35rem, 2.4vw, 1.85rem)`, 1): Cell names inside service and reason cells, uppercase.
- **Mark Code** (700, `clamp(15px, 1.5vw, 19px)`, -0.01em, orange, tabular numerals): Martian Mono. The opening code mark of every record (`SZ/01`, `MT/01`) — the element that introduces a cell now that pictograms are gone. It sits deliberately below the cell heading: snapped onto the heading step it competes with the name it introduces.
- **Body** (400, 16px, 1.55): Archivo, sentence case, capped at 54ch in the hero sub and 46ch in the CTA sub.
- **Small** (400–500, 14px, 1.35–1.6): Archivo. The small-text step and the most-used size in the file: cell descriptions, channel values, the affiliate disclosure (78ch) and product names. It is one step, not a family of near-identical values.
- **Label** (500, 11px, 0.04–0.06em, uppercase): Martian Mono. Channel keys, controls, nav links.
- **Code** (400, 10.5px, 0.02–0.22em, uppercase, tabular numerals): Martian Mono. REF strings, class words, `LOTE`, `TIPO`, `ÁREA`, part codes and source tags, rail type (0.22em, vertical), footer meta.

### Named Rules
**The Mono-Is-Measurement Rule.** Martian Mono is reserved for codes, labels, values and identifiers. It never sets a sentence. A mono paragraph is the system wearing a costume; prose belongs to Archivo, in sentence case, even though every mark around it is uppercase.

**The Ten-Step Rule.** The ramp is closed at ten steps. Before adding a size, check whether an existing step already does the job — three near-identical small values are one step, not three. A step earns its place by having a role no other step can hold: the hero second line, the cell mark code and the small-text step each do.

**The Floor Rule.** The shouting word scales with the viewport but never falls below its floor (5.2rem). Density layers are removed to make room for it; it is never shrunk to make room for them.

**The Marks-Not-Claims Rule.** Marking strings (REF/SZ/MT codes, class words, `LOTE`, `TIPO`, `ÁREA`) may be authored freely — they are the system's ornament and carry no assertion. Page copy may not. No claim about prices, lead times, tolerances, materials, clients or volumes may be introduced as type, and no photograph of a printed part exists to support one.

## Layout

The page is a single sheet: a full-height container padded by the rail width, opened with a hairline top rule, with content centred in a 1420px max-width wrap. Horizontal padding steps 16px → 22px (≥700px) → 30px (≥1080px); vertical band rhythm (`--bay`) runs 64px → 52px (≥700px) → 60px (≥1080px), so the mobile view is deliberately the airiest per band while the desktop view earns its density from ornament instead of whitespace. Every band is separated by a 1px rule, and a tick-marked ruler scale is drawn along the top edge of each band's content so no section appears without measurement beside it.

Grids are butt-joined: a 1px gap over a rule-grey background, with a 1px rule-grey border, so cells appear to share a single drawn line rather than float apart. Service cells run 1 → 2 (≥620px) → 4 (≥1000px); reason cells run 1 → 3 (≥760px); affiliate cards run 2 → 3 (≥780px) → 4 (≥1060px); channel rows run 1 → 2 (≥640px) → 5 (≥1040px). The sticky code strip pins to the top at all widths.

**Declared density tiers.** Ornament layers drop in named steps as the viewport narrows, and each step is a deliberate removal, not a reflow:
- **≥1080px** — fixed vertical rails on both margins (46px), carrying roundel, vertical set type, hazard block, barcode and target.
- **≥900px** — the section nav appears in the code strip; the strip hazard shortens to a fixed 90px block.
- **≥860px** — the registration bay: the hero's sub-panel gains its border, halftone field and four corner registration crosses.
- **≥700px** — the strip's flexible hazard block.
Below 700px only the strip, the word, the bands and the page grain remain. The offer and the email control are present at every tier.

## Elevation & Depth

**This system has no shadows and no elevation.** There is not one `box-shadow` in the build, no blur, no glow, no gradient and no translucency. Depth is made two ways: by tone (absolute black ground, `#171717` panels for cells and the CTA band) and by rule (1px hairlines that separate every band, cell and chip). Layering is expressed by stacking order and by pattern density, never by light.

The whole sheet carries a fixed, low-density orange halftone grain (5% pattern coverage at 16% opacity) behind all content, so no region is ever flat black; opaque bands cover it and the gutters between them let it show. Denser halftone fields at 30% and a screen at 55% mark the registration bay and the CTA band. Printed material has tone even where nothing is printed — flat black reads as absence, and this system never ships absence.

### Named Rules
**The No-Light Rule.** Nothing on this page emits. No shadow, no glow, no gradient, no glass. If an element needs to separate from its neighbour, give it a rule or a different black.

**The Tone-Not-Void Rule.** Every large black region carries grain or halftone. If a gutter or band measures as pure `#000000` across its whole area, it is unfinished.

## Shapes

Zero radius everywhere. Every control, cell, card, chip and media frame is a hard rectangle; the only curves in the system are inside drawn marks (roundel, target, halftone dots) and the one inherited Instagram glyph. Borders are always exactly 1px in rule grey, or 1px in orange when an element is a control or the CTA band.

The recurring silhouette is the **marked rectangle**: a hard-edged box whose corners are annotated rather than softened. Two devices do that work — corner brackets (7px, 2px stroke, offset -4px, drawn on the primary control at rest and on any control at hover or focus) and registration crosses (13px, offset -7px, sitting on the corners of the registration bay and the CTA band). Both read as print alignment marks, not as decoration.

Ornament is a fixed vocabulary of drawn SVG at one weight (1.5–1.7px stroke): hazard stripes as a -45° pattern in orange (white for an unassigned slot), halftone screens, the ruler scale, registration crosses, the roundel, the target, vertical rail barcodes, and per-cell barcodes whose bar widths and gaps are derived deterministically from the cell's own ID string.

## Components

### Controls (Buttons)
Hard-edged instrument controls, mono-set and uppercase; they read as switches on a panel rather than as web buttons.
- **Shape:** Square corners (0 radius), 1px orange border, 13px/22px padding, mono label step (11px).
- **Primary (filled):** Orange fill on black text, corner brackets visible at rest. Hover inverts to white fill with a white border. Used for the email action in the strip, the hero, and the CTA band.
- **Secondary (outlined):** Transparent fill, orange border and orange text; hover fills orange with black text. Carries the address itself.
- **Focus:** 2px orange outline at 2px offset, plus the corner brackets fading in (120ms linear). All state transitions are 120ms linear — there is no easing curve on hover in this system.

### Cells (Service / Reason Cards)
Data records, not marketing cards. Each is a filing entry with a header, a body and a footer of marks.
- **Corner Style:** Square (0 radius). No border of its own; the 1px grid gutter draws the edge.
- **Background:** Second black (#171717) on a rule-grey grid.
- **Structure:** A top row with an orange mono ID code and a dimmed right-aligned class word over a hairline; a display-face name; a muted description; a footer above a hairline carrying a generated barcode, its code string, and (in the service grid) a small hazard block.
- **Internal Padding:** 22px 20px 24px.
- **Interactive variant:** When a cell is a link, hover and focus draw a 1px orange outline inset by -1px (a rule of ink, no new colour) and its name turns orange.

### Affiliate Cards
The supporting shelf. Deliberately lighter than the service cells: black ground rather than panel black, so they never outweigh the service the page sells.
- **Media:** 4:3 white plate with contained, padded imagery — the only white field in the system — overprinted top-left with a black source tag in orange mono.
- **Body:** A label-step mono line (merchant seal or a `CN/NN` reference), a name at the small step clamped to 3 lines, and an orange mono action line with a drawn arrow.
- **Hover:** Background lifts to the second black.

### Navigation
The sticky code strip: roundel, wordmark (display face, orange `3D`), a REF code, a flexible hazard block, section links, and the email control pushed right.
- **Links:** Mono, 11px, uppercase, muted at rest; hover turns white with a 2px orange bottom border.
- **Mobile:** Links are removed below 900px and the hazard block below 700px; the wordmark and the email control always survive.

### Channel Rows
Flat rows in a butt-joined grid: a 21px drawn mark or the 3Dcalc logo, a mono key, and a white value at the small step. Hover lifts to the second black. No radius, no icon container, no chip.

### The Marking Layer (signature)
The system's defining component is not an element but a layer. Every band carries a REF string in its heading, every cell carries an ID code and a barcode generated from that ID, band boundaries carry a ruler scale, margins carry rails, and panels carry registration crosses. New surfaces inherit this layer: a section without a REF, a scale and at least one drawn mark is not in this system.

### Browser Surfaces
The page themes the browser chrome from the palette: selection is orange on black, caret and `accent-color` are orange, focus is a 2px orange ring at 2px offset, and the scrollbar is a rule-grey thumb on a black track that turns orange on hover. Any new surface keeps these.

## Do's and Don'ts

### Do:
- **Do** ground every surface in absolute black (#000000) with the fixed halftone grain behind it, and use the second black (#171717) for panels only.
- **Do** give every new section a REF code in its heading, a ruler scale at its top edge, and at least one drawn mark.
- **Do** draw all ornament as inline SVG at the established weight (1.5–1.7px stroke; patterns for hazard, tone and scale).
- **Do** give every full-bleed SVG field an explicit `width`/`height` (or a measured `width: calc(...)`). An inline `<svg>` is a replaced element: `position: absolute` with `left`/`right` or `inset: 0` will not stretch it. This bit the build three times.
- **Do** keep prose in Archivo, sentence case, capped at 54–78ch, in white or the muted grey (#8C8C8C, chosen to clear 4.5:1 on black).
- **Do** remove ornament layers in the declared density steps (rails at 1080px, registration bay at 860px, nav at 900px, strip hazard at 700px) rather than compressing them.
- **Do** keep the email action reachable at every breakpoint and every density tier.
- **Do** ship one orchestrated entrance stamp — marks first (40/120/200ms delays), the word landing last as a flat opacity fade — with a real `prefers-reduced-motion` branch that renders the stamped state with no animation.

### Don't:
- **Don't** introduce a second accent colour, a tint ramp, or any hue outside the closed palette.
- **Don't** use a gradient, a glow, a shadow, a blur or a translucent surface anywhere. Depth is tone and rule.
- **Don't** round a corner. Radius is 0 across the system.
- **Don't** add a font size outside the ten-step ramp, and don't set prose in Martian Mono, and don't set body copy in caps — the mono is for codes, labels and values only.
- **Don't** let a large black region sit flat: grain or halftone belongs behind every band and gutter.
- **Don't** add a claim as copy. Marks may be authored; claims may not. No price, lead time, tolerance, material, client or volume may be written, and no image may imply a printed part the project does not have.
- **Don't** float cells apart with gaps and shadows — grids butt-join over a 1px rule-grey gutter.
- **Don't** return to the replaced world: a dark hero with an orange gradient wash and a grid of soft icon cards is the anti-reference, not a fallback.
- **Don't** let the affiliate shelf outweigh the service grid in surface, size or colour.
