# Reusable Restaurant Template — Clone & Swap Guide

This site doubles as your **reusable restaurant template** for the DDM project. To spin up a demo for a new restaurant client, copy the folder and swap content in a handful of clearly marked places. Target time: **30–60 minutes**.

```bash
cp -r Kozykook-website  NewClient-website
```

There are only **4 files** you ever touch for content: `index.html`, `styles.css`, the `assets/` images, and the 3 SEO files.

---

## 1. Rebrand the look — `styles.css` (≈30 seconds)

Everything visual keys off the tokens at the very top of `styles.css`:

```css
:root {
  --brand:      #E95C00;   /* ← change to the new restaurant's color   */
  --brand-dark: #C44C00;   /* ← a darker shade of the same color       */
  --brand-tint: #FFF3EA;   /* ← a very light shade of the same color   */
  --font-head: "Raleway", ...   /* headings — elegant/modern, full italics (Google Fonts) */
  --font-body: "Open Sans", ... /* body/menu — top screen readability */
}
```

Change `--brand` and its two shades and the whole site re-themes — buttons, headings, badges, hover states, the hero overlay, everything. If you change fonts, also update the `<link href="https://fonts.googleapis.com/...">` tag in `index.html`.

---

## 2. Swap the content — `index.html`

Search the file for **`SWAP:`** comments — they flag every editable block. Work top to bottom:

| Where | What to change |
|---|---|
| `<title>` + `<meta description>` | Business name, cuisine, area, key dishes |
| `og:*` / `twitter:*` meta | Social-card title, description, image URL |
| `<link rel="canonical">` + `og:url` | The site's final URL |
| **JSON-LD block** (`application/ld+json`) | Name, address, geo, phone, email, hours, cuisine, socials, rating — this is what powers Google rich results, so fill it accurately |
| Header `.brand-name` | Business name + sub-label |
| Hero `.eyebrow / .hero-title / .hero-sub` | Tagline + one-line pitch |
| `.strip` items | 4 highlights (flavors, vibe, delivery, etc.) |
| About copy | 2 short paragraphs + the tag pills |
| Flavors / specialties cards | Rename or repurpose (e.g. "Signature drinks" for a café) |
| **Menu** (`.featured-grid` + `.menu-cols`) | Featured dishes + every category & price |
| Visit: `.hours` table | Day-by-day hours (keep the `data-day` numbers: 0=Sun … 6=Sat) |
| Visit: `.contact-list` + map `iframe` | Address, phone (`tel:`), email (`mailto:`), Messenger, map query |
| Footer | Name, address, phone, socials |

**Links to update everywhere they appear:** foodpanda URL, `m.me/...` Messenger link, `tel:+63...`, `mailto:...`, Facebook / Instagram / TikTok, and the Google Maps `?q=` query.

> Tip: most fields appear 2–3 times (header, body, footer, JSON-LD). A find-and-replace on the **phone number, email, and business name** catches the bulk in one pass.

---

## 3. Swap the images — `assets/`

Replace these files (keep the same filenames so no HTML edits are needed), or update the `src=` paths:

| File | Used for | Ideal size |
|---|---|---|
| `kozykook-logo.jpg` | header, footer, favicon source | square, ≥512×512 |
| `kozykook-storefront.jpg` | hero background + about | landscape, ≥1200px wide |
| `kozykook-duo-deal-chicken.jpg` | featured dish 1 | ~800×580 |
| `kozykook-solo-meal-chicken.jpg` | featured dish 2 | ~800×580 |

Then regenerate the favicons + social card from the new logo (any image tool, or re-run the same Pillow snippet used to build them): `favicon.ico`, `favicon-16/32.png`, `apple-touch-icon.png`, `icon-192/512.png`, `og-image.jpg`.

---

## 4. Update the SEO files

- `robots.txt` → change the `Sitemap:` URL
- `sitemap.xml` → change `<loc>` + `<lastmod>`
- `site.webmanifest` → change `name`, `short_name`, `description`, `theme_color`

---

## 5. Deploy

See `README.md`. Drag-and-drop the folder onto <https://app.netlify.com/drop> for an instant live URL to use as your demo link.

---

## Design principles this template follows

- **Plain HTML/CSS/JS, zero dependencies** — clone → swap → deploy in under an hour. Scrolling is native and crisp (no scroll-hijacking library).
- **Static content for SEO** — the whole pitch is "show up on Google," so all text is real HTML (not rendered by JS), plus JSON-LD structured data for rich results.
- **One rebrand surface** — colors/fonts live in one `:root` block.
- **Cohesive editorial theming, no dead zones** — sections alternate warm/dark backgrounds with dividers, numbered labels (`01 —`), italic heading accents (`<em>`), and bordered/framed text areas instead of floating text on white. To re-tone a section, give it `section--dark` (espresso) or `section--brand` (orange gradient).
- **Grounded-panel design system (v2)** — *no text ever floats on a bare background.* One panel recipe (`.panel`: surface + 1.5px border + radius + shadow + `--panel-pad`) is re-skinned for light / `section--dark` / `section--brand` tones. Every section header is itself a centered grounded card (`.section-head`) with a top accent bar (`--accent-bar`) that visually ties it to the content cards below. All padding, grid gaps and section rhythm come from one spacing scale (`--space-*`, `--gap`, `--panel-pad`, `--section-pad`, `--head-gap`) in `:root`, so spacing stays consistent everywhere and is tunable in one place. When adding any new block, wrap its text in `.panel` (or reuse `.section-head`) — never drop raw text onto a section background.
- **Typography & tier separation (v2)** — headings use **Raleway**, body/menu use **Open Sans** (swap both in `:root` + the `<link>` tags in `index.html` and `thanks.html`). Each text group is tiered: the kicker (`.eyebrow`) renders as a shaded **chip**, and a hairline divider separates heading from body inside panels — so header / sub-header / body always read as distinct. The hero is flex-centred in a viewport-responsive band (`min-height: …svh`) so its vertical placement adapts to any screen.
- **Menu/pricing on foodpanda** — the on-page section is a no-price "House favorites" showcase; the full menu and prices stay on the restaurant's foodpanda page, which the CTAs link to. (To put a full menu back on-site, restore a `menu-panel` list.)
- **Zero-backend features** — Formspree for inquiries; `tel:` / `mailto:` / `m.me` / maps links need no API keys.
- **Mobile-first** — most local restaurant traffic is phones.
