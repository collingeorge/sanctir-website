# sanctir.com

Static website for Sanctir — an independent defense compliance practice. Production source for the sanctir.com domain.

## Stack

- Pure HTML/CSS, no build step, no JavaScript framework
- Self-hosted WOFF2 web fonts (Libre Baskerville + IBM Plex Sans + IBM Plex Mono)
- Inline SVG wordmark with outlined paths (no runtime font dependency for brand mark)
- Formspree for contact form submission
- No analytics, no tracking, no third-party cookies

## Structure

```
/
├── index.html              Main page
├── privacy.html            Privacy notice
├── terms.html              Terms & disclaimer
├── 404.html                Not-found page
├── CNAME                   Custom domain (sanctir.com)
├── robots.txt              Crawler directives
├── sitemap.xml             XML sitemap
├── og-image.png            Open Graph social card (1200×630)
├── favicon.svg             Primary favicon (vector)
├── favicon.ico             Legacy favicon (16/32/48 bundle)
├── favicon-*.png           Sized PNGs (16, 32, 48, 180, 192, 512)
└── fonts/
    ├── LibreBaskerville-Bold.woff2          Wordmark + serif headings
    ├── LibreBaskerville-BoldItalic.woff2    Hero italic em
    ├── IBMPlexSans-Regular.woff2            Body text
    ├── IBMPlexSans-Bold.woff2               UI bold, buttons, card titles
    ├── IBMPlexMono-Bold.woff2               Section labels, tags
    ├── LICENSE-LibreBaskerville.txt         SIL OFL
    └── LICENSE-IBMPlex.txt                  MIT
```

Total deploy weight: ~340KB.

## Local preview

```bash
# Python
python3 -m http.server 8000
# Then visit http://localhost:8000

# Or Node
npx serve .
```

Web fonts require an HTTP server to load (CORS prevents `file://` font loading on most browsers).

## Deployment

**GitHub Pages** — push to `main`, then Settings → Pages → Source: `main` / `/ (root)` → Custom domain: `sanctir.com`. The `CNAME` file is already in the repo.

**Cloudflare Pages** — connect this repo, leave build command empty, build output directory: `/`. Add custom domain in Cloudflare Pages settings.

**Self-hosted** (nginx / Caddy / Apache) — copy contents to web root.

## DNS configuration

For **GitHub Pages**, point `sanctir.com` to GitHub's IPs at your DNS provider:

```
A    @     185.199.108.153
A    @     185.199.109.153
A    @     185.199.110.153
A    @     185.199.111.153
CNAME www  collingeorge.github.io.
```

(Replace `collingeorge` with your GitHub username if different.)

For **Cloudflare Pages**, Cloudflare handles DNS automatically when you add the custom domain.

## Recommended HTTP headers

```
/fonts/*
  Cache-Control: public, max-age=31536000, immutable
  Access-Control-Allow-Origin: *

/og-image.png
  Cache-Control: public, max-age=86400

/favicon*
  Cache-Control: public, max-age=2592000
```

Long-cache the fonts (they're immutable once deployed). The CORS header on `/fonts/*` is required for `<link rel="preload" crossorigin>` to work cleanly.

## Form submissions

The contact form posts to Formspree at `https://formspree.io/f/mojpwljz`. Destination email and routing configuration are managed in the Formspree dashboard, not in code. Subject line is fixed to "Sanctir — engagement inquiry".

## Color tokens

| Token | Hex | Use |
|---|---|---|
| NAVY | `#1A3A5C` | Wordmark, headings, emphasis |
| GOLD | `#B8860B` | Wordmark plinth, hero italic em, accent rules |
| DARK | `#222222` | Body text |
| GRAY | `#666666` | Secondary text |
| BG-LIGHT | `#F4F4F4` | Table headers, panels |
| BORDER | `#CCCCCC` | All structural borders |

## Maintenance

HTML files inline their CSS for portability. Edit changes need to be applied to all four pages (`index.html`, `privacy.html`, `terms.html`, `404.html`).

The wordmark SVG is inlined in `<nav>` and `<footer>` of every page. If the wordmark design changes, the master at `/sanctir-brand-assets/sanctir-wordmark.svg` (kept outside this repo) regenerates from the same Python source. Update all four pages consistently.

## License

Site content © 2026 Sanctir. All rights reserved.
Font licenses: see `fonts/LICENSE-LibreBaskerville.txt` (SIL OFL) and `fonts/LICENSE-IBMPlex.txt` (MIT).
