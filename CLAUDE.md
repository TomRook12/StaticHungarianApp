# Magyar Otthon — Project Constitution

A family Hungarian language learning PWA. The goal is natural, daily language use between a parent and their children and partner, not academic study.

## What this app is

- Phrase-based lessons organised by daily-life situations (morning, outings, food, bedtime, etc.)
- Quiz engine that reinforces weak phrases and adapts to time of day
- Deployed as a mobile-first PWA to GitHub Pages; used offline

## What this app is not

- A general-purpose language course
- Multi-user / server-connected
- Monetised

## Key files

| Path | Purpose |
|------|---------|
| `src/App.jsx` | Entire app — data, logic, and UI (single file by design) |
| `public/manifest.json` | PWA manifest |
| `vite.config.js` | Build config; `base` must match GitHub Pages path |
| `docs/architecture.md` | Deeper architecture notes |
| `docs/conventions.md` | Coding standards |
| `docs/specs/` | One spec file per planned feature |
| `docs/decisions/` | Lightweight ADRs |

## Working with Claude

1. **Before implementing a feature**, write a spec in `docs/specs/` using `_template.md` and get approval.
2. **Reference the spec** throughout implementation; check off tasks as they complete.
3. **Don't split `App.jsx`** into multiple files without a decision record in `docs/decisions/`.
4. **Don't add dependencies** without discussing trade-offs first; the app is intentionally zero-dependency beyond React and Vite.

## Deploy

```bash
npm run deploy   # builds and pushes to gh-pages branch
```
