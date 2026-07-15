# sanctir.com

Static site for Sanctir — an independent national security research and advisory practice.
Decision support across threat finance, export controls, sanctions, strategic sourcing, and cybersecurity.

## Architecture

Hub-and-spoke. The homepage (`index.html`) is the institutional hub; each section summarizes and
links to a detail page (spoke). Spokes are expanded as content justifies.

## Structure

```
index.html                                  Homepage (hub)
styles.css                                  Centralized design system (versioned: ?v=N)
methodology/index.html                      Methodology (spoke)
research/index.html                         Research library (spoke — to be expanded per-paper)
supply-chain/index.html                     Strategic supply-chain intelligence (spoke)
services/financial-sanctions-risk/          Advisory spoke
services/export-controls/                   Advisory spoke
services/controlled-information/            Advisory spoke (holds current CMMC/attestation analysis)
services/national-security-policy/          Advisory spoke
privacy.html, terms.html, 404.html          Legal + error
fonts/                                       Self-hosted WOFF2 (no third-party requests)
```

## Design system

- Colors: navy `#1A3A5C`, gold `#B8860B`, white, on the locked v1.1 token set
- Type: Libre Baskerville (display), IBM Plex Sans (body), IBM Plex Mono (labels)
- All styles centralized in `styles.css`. Bump the `?v=N` query string on change to bust cache.
- Self-hosted fonts, no external requests, CSP set via meta tag on every page.

## Editing

- Content is hand-authored HTML against `styles.css` classes.
- The homepage "Current Analysis" panel is a deliberately replaceable module for time-sensitive
  content — update it without touching structural copy.
- To add a research paper page: build against the stub template pattern in `research/`.

## Hosting

GitHub Pages + custom domain (`CNAME`) + Fastly edge. HTTPS enforced. DNSSEC enabled at registrar.
