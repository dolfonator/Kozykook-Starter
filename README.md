# Kozykook Diner & Bar — Website

A fast, mobile-first, SEO-optimized one-page site for **Kozykook Diner & Bar** (Korean diner + bar, Katipunan Ave., Quezon City). Built with plain HTML/CSS/JS — no build step, no framework, **zero dependencies**. Scrolling is crisp and native. This is also the **reusable restaurant template** for the DDM project; see `TEMPLATE-GUIDE.md` to clone it for a new restaurant.

The design is **cohesively themed** in an editorial style — alternating warm cream and dark espresso sections with a brand-orange feature strip and CTA band, numbered section labels, italic heading accents, clear dividers between sections, and bordered/framed text areas — so there are no "dead" white zones and no need for a dark mode. **The full menu and pricing live on foodpanda** (linked from the site); the on-page "House favorites" section is a no-price showcase that drives orders to foodpanda/Messenger.

---

## What's inside

```
Kozykook-website/
├── index.html          ← the site (all content, clearly marked for swapping)
├── styles.css          ← styling; brand tokens at the very top (:root) for 1-line rebrand
├── script.js           ← nav toggle, scroll-reveal, active nav, today's-hours highlight
├── thanks.html         ← form success page (Formspree redirect)
├── netlify.toml        ← Netlify config: publish dir, security headers, redirects
├── site.webmanifest    ← PWA / installable metadata
├── robots.txt          ← search-engine crawl rules
├── sitemap.xml         ← sitemap for Google
├── favicon.ico         ← favicon
├── TEMPLATE-GUIDE.md   ← how to reuse this for another restaurant
└── assets/             ← logo, photos, favicons, OG social card
```

No `package.json`, no `node_modules`, nothing to compile. **The folder IS the site.**

---

## Deploy to Netlify (pick one)

### Option A — Drag & drop (fastest, ~60 seconds)
1. Go to <https://app.netlify.com/drop>.
2. Drag the **`Kozykook-website` folder** onto the page.
3. Netlify gives you a live URL like `https://random-name-123.netlify.app` — your **status check** is the green "Published" state + the URL loading.
4. (Optional) **Site settings → Change site name** to something like `kozykook` → `https://kozykook.netlify.app`.

### Option B — Connect a Git repo (best for ongoing edits)
1. Push this folder to a GitHub repo.
2. Netlify → **Add new site → Import an existing project** → pick the repo.
3. Build command: *(leave blank)* · Publish directory: `.` (already set in `netlify.toml`).
4. Every `git push` auto-deploys.

### Option C — Vercel
Import the folder/repo at [vercel.com/new](https://vercel.com/new) (framework preset: **Other**, no build command). `vercel.json` adds the same security + caching headers as `netlify.toml`. The site is currently live at **https://kozykook.vercel.app/**.

> If you move to a different domain, update the live URL in: `index.html` (canonical + og:url + JSON-LD `@id`/`url`/`image`), `robots.txt`, and `sitemap.xml`. They currently point to `https://kozykook.vercel.app/`.

---

## Contact / reservation form

The **Book** section uses **Formspree** — works on Vercel (or any static host), no backend needed.
- **One-time setup:** create a free form at <https://formspree.io> → copy its ID → in `index.html`, replace `YOUR_FORM_ID` in the form's `action="https://formspree.io/f/YOUR_FORM_ID"`.
- Submissions are emailed to you (and appear in the Formspree dashboard). Confirm the form once on first submit.
- After submit, visitors are redirected to `/thanks.html` via the hidden `_next` field.
- Includes a `_gotcha` honeypot for basic spam protection.
- The form does nothing useful over local `file://` — that's expected; it activates once `YOUR_FORM_ID` is set and the page is deployed.

---

## Local preview

```bash
cd Kozykook-website
python3 -m http.server 8080
# open http://localhost:8080
```

Use a local server (above), **not** double-clicking `index.html`, so that root-absolute paths (`/styles.css`, `/assets/...`) resolve correctly.

---

## Before going live (owner sign-off)

- [ ] Confirm **hours** and **phone** with the owner (sources showed minor discrepancies). Menu/prices are kept on foodpanda, linked from the site.
- [ ] Get **permission to use the logo and photos**, and request a **transparent PNG/SVG logo** for crisp display.
- [ ] Verify the exact **Google Maps pin** and the **Messenger `m.me` link**.
- [ ] Swap interior/ambiance photos when the owner supplies originals.

---

*Built for the DDM local-business website project. Tech: plain HTML/CSS/JS · Host: Vercel · Currency: PHP.*
