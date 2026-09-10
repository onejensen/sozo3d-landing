# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

Static single-file site: `index.html` carries markup, CSS tokens and JS inline; no build step, no framework, no package manager. Assets live in `assets/`. Affiliate products are data-driven from `productos.json`, fetched at runtime. Deployed from `main` to GitHub Pages on the custom domain `www.sozo3d.es` (`CNAME`); a push to `main` is a live deploy.

## Users

Primary, confirmed: **empresas y makers** who need 3D printing done for them — prototypes, short runs, technical parts. Higher ticket, longer decision cycle, and they judge a supplier on precision, tolerances and demonstrated capability before they write an email.

Secondary, served but not the target: particulares looking for decorative pieces, gifts and hard-to-find replacement parts. They stay in the service list; they no longer set the hierarchy.

## Product Purpose

Sozo3D is a custom 3D printing service operating in Spain. The site's only conversion is an email to `info@sozo3d.es` asking for a quote. Success is a qualified quote request from a company or maker, not raw traffic.

## Positioning

Currently undecided and unproven on the site — the live copy ("entrega rápida", "alta precisión", "atención directa") is the category's generic claim set and any competitor could publish it verbatim. Establishing a defensible mechanism is open work. Real differentiators available to draw on: direct one-to-one contact with the person who runs the printers, and an operator who builds and publishes his own tooling (3Dcalc.app, Makerworld models).

## Operating Context

Customers arrive from Instagram and TikTok, from the Linktree, or from search. They evaluate on a phone in most cases. The decision they are making is "can this person actually make my part correctly" — an evaluation of craft, not of a brand.

## Capabilities and Constraints

- Services offered: prototipos, piezas decorativas, piezas de repuesto, proyectos personalizados a medida.
- Contact is email only: `info@sozo3d.es`. WhatsApp and phone were deliberately removed (commit f305fb1); `llms.txt` still lists a stale phone number.
- Language is Spanish; service area is Spain.
- No pricing, no lead times, no material list, no printer models, no tolerances are published. None of these may be invented.
- SEO scaffolding is already in place and must survive: canonical, Open Graph, Twitter card, `LocalBusiness` JSON-LD with an offer catalog, `llms.txt`, `app-ads.txt`.

## Brand Commitments

- The Sozo3D logo (`assets/Logo_Sozo3D.jpg`) stays.
- The orange `#E87722` stays as the brand color.
- The **Recomendados** affiliate section stays on the page. Its visual weight may change; its presence may not. It carries a required affiliate disclosure.
- Owned properties that must keep their links: Instagram `@sozo__3d`, TikTok `@sozo__3d`, Linktree `Sozo3DLabs`, Makerworld collection, and the 3Dcalc.app app (`assets/logo_3dcalc.png`).

## Evidence on Hand

**Open and unconfirmed — must not be fabricated.** The repository contains no photograph of a single printed part, no photograph of the workshop or printer, and no video. The only images are the logo, the 3Dcalc logo, and seven affiliate product photos supplied by Amazon/AliExpress listings.

Whether the owner holds usable photos of his own work (Instagram, TikTok, timelapses) was asked and left unanswered. Until it is confirmed, design work assumes no real imagery exists, authors placeholder material at production fidelity, labels it as placeholder, and hands over a shot list of what to photograph. No claim about clients, volumes, tolerances, delivery times or prices may be written.

## Product Principles

1. **Proof outranks adjectives.** For a craft service, showing the object made is the argument; "alta precisión" as text is not.
2. **The affiliate section is a supporting act.** It may never carry more visual weight than the printing service that pays the bills.
3. **The email is the only conversion.** Every screen keeps that one action reachable and unambiguous.
4. **The site must hold up on a phone first** — that is where the Instagram and TikTok traffic lands.
5. **Nothing is claimed that cannot be shown.** No invented prices, lead times, client names or capabilities.

## Accessibility & Inclusion

No product-specific requirement was established. The incumbent site's small type (13px body) and low-contrast muted grays are a known defect to correct rather than a constraint to preserve.
