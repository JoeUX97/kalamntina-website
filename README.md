# Kalamntina website

Corporate website for Kalamntina, a workforce transformation firm based in Amman.
Static HTML/CSS/JS, hosted on Vercel. Current status: **design preview** (`noindex`).

## Structure

```
index.html                 Home page (hero, who we are, solutions, client impact, CTA, footer)
favicon.svg
assets/brand/              Kalamntina logo
assets/clients/            Client logos for the "Client impact" wall
vercel.json                Hosting config (headers, deploy rules)
DESIGN.md                  Design system: tokens, components, motion, a11y, RTL rules
DESIGN-REVIEW.md           Home page design review (2026-10-18) and task status
PHOTO-BRIEF.md             Brief for regional photography
TODOS.md                   Deferred work (Arabic page, client voices)
assets/clients/mono/       Monochrome client logos (default state of the wall)
```

## Branches and publishing

| Branch | Purpose | Deploys? |
|---|---|---|
| `dev` | Day-to-day work. Commit as often as needed. | No. Disabled in `vercel.json`. |
| `main` | What the client sees. | Yes, to production on every push. |

Publishing = merge `dev` into `main` (or open a PR from `dev` to `main` and merge it).

```bash
git checkout dev
# ...edit, commit, repeat...
git push origin dev            # saved on GitHub, nothing goes live
git checkout main && git merge dev && git push origin main   # goes live
```

## Client logos

| Source | Logos |
|---|---|
| Wikimedia Commons / Wikipedia (vector) | Amazon, Deloitte, MetLife, Orange, Zain, MBC Group, Grand Hyatt, Four Seasons, LG, Vileda |
| Simple Icons (vector) | Samsung |
| Company website (vector) | Bank al Etihad (Arabic lockup), Alfanar, Mawdoo3, malomatia |
| Company website (raster) | GIG, Fine Hygienic Holding, Jordan Bromine |
| Client screenshot, low-res (replace) | ICCI, Arabtech Jardaneh |

Before launch: confirm with Kalamntina that each client has approved logo use, and get
official files for ICCI, Arabtech Jardaneh and an English Bank al Etihad lockup.

## Pending before launch

- Replace stock photography (currently loaded from a public CDN) with licensed or commissioned images.
- Connect the diagnostic form to a real endpoint.
- Remove the "Design preview" tag and `noindex` headers.

## Vercel project

- Project: `kalamntina-preview` (connected to this repo)
- Production branch: `main` · Framework preset: Other · No build command · Output: repo root
- Preview URL: https://kalamntina-preview.vercel.app
