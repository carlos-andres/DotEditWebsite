# DotEdit Website

Marketing website and documentation for [DotEdit](https://github.com/carlos-andres/DotEdit), a native macOS app for comparing `.env` files side by side.

## Links

- **Live site:** [dotedit.app](https://dotedit.app)
- **Documentation:** [dotedit.app/docs](https://dotedit.app/docs)

## Tech Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| Framework | Astro | 5.17.1 |
| CSS | Tailwind CSS | 4.1.18 |
| Language | TypeScript | 5.9.3 (strict) |
| Docs | mdBook | 0.5.2 |
| Fonts | Google Fonts CDN | Bricolage Grotesque, Inter, JetBrains Mono |
| Output | Static HTML/CSS/JS | Zero runtime |

## Requirements

- Node.js 18+
- npm
- [mdBook](https://rust-lang.github.io/mdBook/) (for documentation build)

## Development

```bash
# Install dependencies
npm install

# Start dev server (http://localhost:4321)
npm run dev
```

## Build for Production

```bash
# 1. Build docs (mdBook → public/docs/)
npm run build:docs

# 2. Build site (Astro → dist/)
npm run build

# 3. Preview production build locally
npm run preview

# Type check
npm run check
```

The `dist/` folder contains the final static files ready for upload.

## Main Features

### Landing Page
- Single-page marketing site with 6 sections: Nav, Hero, Screenshot, Features, TrustStrip, DownloadCTA, Footer
- Dark mode toggle with `prefers-color-scheme` respect and no-flash inline script
- Micro-interactions: custom cursor, parallax screenshot, scroll reveals — all gated behind `prefers-reduced-motion`

### Documentation
- 22-page mdBook documentation (decoupled build pipeline)
- Covers: getting started, features, file format reference, settings, FAQ
- Built separately via `npm run build:docs` → served at `/docs/`

### Accessibility & Performance
- WCAG AAA compliance — all text/bg pairs at 7:1+ contrast ratio
- Semantic HTML with landmarks, ARIA labels, skip-to-content, focus-visible
- Lighthouse: 98 / 100 / 100 / 100
- Zero client-side JS libraries — vanilla JS only

## Project Structure

```
DotEditWebsite/
├── src/
│   ├── layouts/BaseLayout.astro     # HTML shell, fonts, meta, dark mode
│   ├── components/                  # 9 Astro components
│   │   ├── Nav.astro
│   │   ├── Hero.astro
│   │   ├── Screenshot.astro
│   │   ├── Features.astro
│   │   ├── TrustStrip.astro
│   │   ├── DownloadCTA.astro
│   │   ├── Footer.astro
│   │   └── DarkModeToggle.astro
│   ├── pages/
│   │   ├── index.astro              # Landing page
│   │   └── 404.astro                # Custom 404
│   ├── styles/global.css            # Color system, animations, cursor
│   └── assets/                      # Screenshots, demo envs, logo
├── docs-src/                        # mdBook source (22 pages, ~2,392 lines)
│   ├── src/SUMMARY.md
│   ├── src/{getting-started,features,file-format,settings,reference,faq}/
│   └── book.toml
├── public/
│   ├── screenshots/                 # WebP + PNG fallback
│   ├── docs/                        # mdBook build output (gitignored)
│   └── favicon, icons
├── scripts/build-docs.sh            # mdBook build + copy
├── astro.config.mjs
├── tsconfig.json
└── package.json
```

## Design

| Aspect | Detail |
|--------|--------|
| Colors | 3 only — Blue accent (`#2563EB` / `#60A5FA`) + neutrals + white/black |
| Typography | Bricolage Grotesque (headlines) + Inter (body) + JetBrains Mono (code) |
| Contrast | WCAG AAA — 7:1+ all text/bg pairs |
| Dark mode | Class-based (`html.dark`) + CSS custom properties |
| Motion | All animations gated behind `prefers-reduced-motion` |
| Lighthouse | 98 / 100 / 100 / 100 |

## Security

- **npm audit:** 5 moderate (lodash in `@astrojs/check` — dev-only, not shipped)
- **No secrets** in source code
- **No `eval()`, `innerHTML`, or `document.write`** in client code
- **Zero client-side JS libraries** — only inline vanilla JS
- **No forms, APIs, or user input** — static HTML only
- **External resources:** Google Fonts CDN only

## Related

- **DotEdit App** — Native macOS app: [github.com/carlos-andres/DotEdit](https://github.com/carlos-andres/DotEdit)
