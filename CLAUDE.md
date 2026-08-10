# Skye Reich — Portfolio Site

Context for working on this repo with Claude Code. Read this first, then skim `DESIGN-SYSTEM.md` before changing anything visual.

## What this is

A single-page portfolio for **Skye Reich**, an interdisciplinary artist working at the intersection of ecology, materials, and public interaction. It presents three projects: **Atlas**, **Woman in a Burning World**, and **A Community Garden Without Community**, plus an About section and contact.

It is a **plain static site** — one HTML file, no framework, no build step, no dependencies to install. Fonts load from Google Fonts; everything else is self-contained. This is deployed on **GitHub Pages**.

## File structure

```
index.html          — the entire site (HTML + CSS in <style> + JS in <script>)
images/             — all photography and graphics, web-optimized JPEGs
DESIGN-SYSTEM.md    — Skye's full research & design system (the source of truth for look/feel)
README.md           — public repo readme + deploy steps
CLAUDE.md           — this file
```

There is intentionally no `src/`, no bundler, no package.json. Keep it that way unless Skye asks to add tooling — the simplicity is a feature for a Pages deploy.

## How to preview locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Open `index.html` directly with a `file://` URL also works, but a local server is closer to how Pages serves it.

## Design system — the rules that matter

Full detail is in `DESIGN-SYSTEM.md`. The essentials, encoded as CSS variables in `:root` at the top of `index.html`:

**Color** (warm, material-derived; let photography carry the strongest color)
- `--color-paper #F5F1E8` background · `--color-paper-deep #ECE6D8` alt band
- `--color-ink #232321` text · `--color-stone #8E8A82` secondary/dividers
- `--color-moss #5C6B58` links & ecological accent · `--color-amber #C18A4A` highlights · `--color-mineral #6C8791` diagrams/focus

**Type** (four roles, already wired as variables)
- Display → **Fraunces** (`--font-display`). *Note: the design system specifies Canela, which isn't freely licensable; Fraunces is the approved-style substitute — a refined editorial serif with organic curves. Don't swap to a generic fashion serif.*
- Editorial → **Cormorant Garamond** (`--font-editorial`) — leads, statements, quotes
- Interface → **IBM Plex Sans** (`--font-interface`) — nav, body
- Scientific → **IBM Plex Mono** (`--font-mono`) — metadata, dates, labels, captions

**Hard constraints** (from the design system — please preserve):
- Minimal border-radius (2px / 6px). No large rounded corners.
- No heavy/default box-shadows. Separate content with borders, spacing, and background shifts.
- Motion should reveal / unfold / fade — never bounce, spin, or parallax hard. Always keep the `prefers-reduced-motion` handling.
- Accessibility is mandatory: semantic HTML, keyboard focus (`:focus-visible`), meaningful `alt` text, captions tied to figures, AA contrast. Don't regress these.
- Let the work lead. The interface is a quiet curator, not the exhibit.

## How the HTML is organized

Sections in order: masthead nav → `#main` → hero → `#about` → `#atlas` → `#burning` → `#garden` → `#contact` → footer. Nav links are in-page anchors.

Reusable patterns (class names are semantic — reuse before inventing new ones):
- `.wrap` — max-width page gutter. `.reading` — narrow prose column.
- `.phero` — full-bleed project hero (background image + `01`/title + credit overlay).
- `.metablock` — the 4-column archive metadata strip under each project hero (`<dl>`).
- `.mark` + `.meta` — small mono section label with a hairline rule.
- `.lead` (editorial) / `.prose` (body) — text blocks.
- `.row` / `.row--textfirst` / `.row--top` — two-column text+image layouts.
- `.figure` + `.cap` — image with mono caption. `.feature` — full-bleed figure.
- `.g2 .g3 .g4` — image grids. `.mothgrid` — the 6-up specimen grid. `.seq` — the activation sequence strip.
- `.timeline` / `.tnode` — the branching garden timeline (moss = private phase, amber = public phase).
- `.reveal` — scroll-in fade. It's gated behind a `.js` class on `<html>` so content stays visible if JS is off — keep that pattern.

The JS at the bottom does four things: mobile nav toggle, scroll-reveal observer, and the animated dendritic **growth pattern** in the hero (an SVG that draws itself branch-by-branch — this is the site's signature element; treat it gently).

## Images

Naming is by section + purpose, e.g. `atlas-hero.jpg`, `burning-render-03.jpg`, `garden-timeline`… They were extracted from Skye's portfolio PDF and optimized (long edge capped ~2200px for heroes / ~900–1200px elsewhere, JPEG q82, progressive). Total ~13 MB.

When adding or replacing images: keep them optimized (JPEG, progressive, sensible dimensions), give every `<img>` real `alt` text, and add `loading="lazy"` to anything below the first screen. Credit lines for Atlas imagery read "Courtesy of Jen Lewin Studio · Photo by Nicki Evens"; garden photos are by Jenni Pietromonaco — preserve those credits.

## Placeholders to replace (Skye should confirm these)

- **Email** in `#contact` is `hello@skyereich.com` — a guess. Replace with the real address.
- **Download CV (PDF)** and **Instagram** links are `#` placeholders. Drop a `cv.pdf` in the repo and point the link at it; add the real Instagram URL.
- Copy was lightly **typo-corrected** from the PDF (e.g. "ignite", "emanating", "Apprentice", "Associate", "Burning", "Temperature", "thermochromic"). Meaning was preserved — worth a proofread against Skye's intent.
- The garden **Timeline** is a rebuilt on-brand branching layout, not the original diagram image. If Skye prefers her original, it can be swapped in.

## Good first tasks

- Wire up the real email / CV / social links.
- Add a browser tab favicon (a small dendrite or moth mark).
- Add `<meta property="og:*">` tags + a share image for link previews.
- Optionally split each project into its own page if the archive grows (the design system anticipates growth — keep components reusable).

## Deploy

GitHub Pages, from the `main` branch root. See `README.md`. Because all asset paths are **relative** (`images/…`), the site works unchanged whether served from a domain root or a project subpath like `/SkyesPortfolioSite/`.
