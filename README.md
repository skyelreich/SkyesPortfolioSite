# Skye Reich — Portfolio

A single-page portfolio for interdisciplinary artist **Skye Reich**, covering three projects — *Atlas*, *Woman in a Burning World*, and *A Community Garden Without Community* — built on Skye's own research & design system.

Plain static site: one HTML file, web fonts, and optimized images. No build step.

## Run locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Or just open `index.html` in a browser.

## Deploy to GitHub Pages

1. Upload every file/folder in this project to the repo, **keeping the `images/` folder intact** (so paths stay `images/…`).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
5. Wait ~1 minute. Your site publishes at:
   **https://skyelreich.github.io/SkyesPortfolioSite/**

Every push to `main` re-deploys automatically.

### Custom domain (skyereich.com)

A `CNAME` file containing `skyereich.com` is included, so Pages knows the domain. To finish:

1. In **Settings → Pages → Custom domain**, enter `skyereich.com` and Save (do this *before* the DNS step).
2. At your DNS provider (GoDaddy), point the apex domain at GitHub with four **A records** (`@` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`) and a **CNAME** for `www` → `skyelreich.github.io`.
3. After DNS propagates, check **Enforce HTTPS** in Settings → Pages.

## Structure

```
index.html          Site (HTML + inline CSS + inline JS)
images/             Optimized photography & graphics
DESIGN-SYSTEM.md    The research & design system behind the look
CLAUDE.md           Working context for edits with Claude Code
```

## To fill in

- Real contact email (currently a placeholder in the Contact section)
- CV PDF and Instagram links (currently `#`)

## Credits

Design & work: **Skye Reich**.
*Atlas* imagery courtesy of **Jen Lewin Studio**, photographs by **Nicki Evens**.
*A Community Garden Without Community* photographs by **Jenni Pietromonaco**.

© 2026 Skye Reich.
