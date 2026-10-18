# Kalamntina design system

The source of truth for every Kalamntina page. The home page (`index.html`) implements it;
new pages reuse these tokens and components rather than redefining them.
Brand basis: *Kalamntina Brand Guidelines, "Precision Fire · Ink Navy"*.

## Colour

All colours are CSS custom properties on `:root`. Sections never redefine colours.

| Token | Value | Use | Contrast |
|---|---|---|---|
| `--ink` | `#0F1E35` | Ink Navy. Dark sections, footer, text on light | 16.9:1 on Off White |
| `--navy-mid` | `#1E3A5F` | Navy Mid. Secondary dark section (diagnostic CTA) | |
| `--navy-line` | `#284870` | Supergraphic shapes on Navy Mid | decorative |
| `--off` | `#F7F9FC` | Off White. Light sections | |
| `--white` | `#FFFFFF` | Cards, form surface, logo tiles | |
| `--orange` | `#FF7722` | Ignite Orange. Buttons, accents on dark, logo mark | 2.5:1 on Off White: **never as text on light** |
| `--orange-hover` | `#FF8A40` | Button hover | |
| `--orange-ink` | `#1F0D00` | Text on orange buttons | 8.4:1 on orange |
| `--orange-text` | `#C2520B` | Orange text on light surfaces, **large text only** (≥24px, or ≥18.66px bold) | 4.4:1 on Off White |
| `--text-body` | `#4E5D72` | Body copy on light | 6.4:1 |
| `--muted` | `#5F6D80` | Supporting text on light (descriptions, tags, small print) | 5.0:1 on Off White, 5.3:1 on white |
| `--line` | `#DCE3EC` | Hairlines on light | decorative |
| `--field` | `#D6DEE8` | Input borders | |
| `--error` | `#B42318` | Form errors | 6.5:1 on white |
| `--soft` | `rgba(247,249,252,.78)` | Body copy on dark | 10:1 on Ink |
| `--dim` | `rgba(247,249,252,.6)` | Supporting text on dark | ≥4.9:1 on Ink |
| `--hair` | `rgba(247,249,252,.2)` | Hairlines on dark | decorative |
| `--soft-mid` | `#B9C8D9` | Body copy on Navy Mid | 6.8:1 |

Rules
- Orange is never a large background (brand rule). It appears as buttons, the hero verb, step markers and small accents.
- Never Ink Navy text on Navy Mid. Never pure black.
- Body text ≥ 4.5:1, large text ≥ 3:1. Check every new pairing against this table.

## Typography

| Role | Font | Size | Weight | Tracking |
|---|---|---|---|---|
| Hero verb | Bricolage Grotesque | `clamp(84px,15vw,232px)` | 700 | -0.06em (keep `padding-inline-end:.12em` so the final glyph isn't clipped) |
| Hero lead | Bricolage Grotesque | `clamp(28px,3.4vw,52px)` | 500 | -0.03em |
| Section title (`h2.title`) | Bricolage Grotesque | `clamp(34px,4.4vw,64px)` | 600 | -0.04em |
| Sub-heading (`h3`) | Bricolage Grotesque | `clamp(22px,2vw,28px)` | 600 | -0.02em |
| Big numbers | Bricolage Grotesque | `clamp(44px,5.6vw,84px)`, tabular | 600 | -0.045em |
| Lede | Hanken Grotesk | `clamp(17px,1.3vw,19px)`, lh 1.65 | 300–400 | 0 |
| Body / UI | Hanken Grotesk | 15–16px | 400–600 | 0 |
| Supporting | Hanken Grotesk | 14px minimum | 400–500 | 0 |
| Overline (cards, footer headings) | Hanken Grotesk | 12px caps | 600 | 0.16em |

No section eyebrows/kickers above headings (review decision 10A). Headings carry the section.

## Space and shape

- Gutter: `--gutter: clamp(20px,5vw,80px)`. Max content width 1440px.
- Section padding: `--pad-top: clamp(72px,11vw,144px)`, `--pad-bottom: clamp(64px,9vw,120px)`.
- Radius: `--radius: 6px` (buttons, inputs, cards); `--radius-lg: 8px` (form panel). Pills only for status chips.
- No drop shadows. Depth comes from surface colour and hairlines.
- Breakpoints: 1100 (cards 2-up), 1000 (desktop nav hides), 980 (two-column layouts stack), 900 (hero controls move under verb), 640 (mobile header), 620 (single column).

## Components

**Primary button** `.btn` / `.sub-btn`: orange, `--orange-ink` text, 56px tall, 6px radius, trailing arrow that nudges 3px on hover. One label for the conversion everywhere: **"Request a diagnostic"** (nav may read "Get a diagnostic"). Hero pairs it with a secondary text link "Browse jobs" (`.link`).

**Text link** `.more`: 16px/600, orange 2px underline on the label, arrow, 44px hit area.

**"Soon" chip** `.soon`: 10px caps chip next to links whose page isn't built; the item is not focusable and has `aria-disabled="true"`.

**Placeholder chip** `.tbc`: dashed orange outline; marks client-supplied figures still to confirm. Remove before launch.

**Solution card** `.card`: photo, top-to-bottom navy gradient, overline, title + arrow, description, service list (always visible). Hover: orange top bar, photo zoom 1.06. Link name = pillar name. Stacks single-column below 620px.

**Results ledger** `.res`: big number + statement + meta tags (sector · pillar · country). Hairline rows.

**Logo wall** `.logo-grid`: white tiles, hairline grid; monochrome Ink Navy logos at 55% opacity (`/assets/clients/mono/`), colour version cross-fades on hover. Optical sizing by area (≈3900px², max 150×58px). 5 columns, 4 under 980px, 3 under 620px with the first 12 shown and a "Show all 20 clients" toggle.

**Form**: visible labels above fields (never placeholder-as-label); 16px inputs; inline error text with icon + `aria-invalid` + `aria-describedby`; error summary with links, focused on submit; validate on blur after the first submit; "Sending…" disabled state; network error keeps input and offers "Try again"; success replaces the form and receives focus. Any valid email is accepted.

**Mobile menu**: full-screen Ink Navy dialog, 28px links at 60px rows, Arabic toggle, CTA pinned bottom; `aria-expanded`, Esc closes, focus trapped, background `inert`, scroll locked.

## Motion

- One signature moment: the hero verb, revealed letter by letter, rotates **continuously** (hire → build → advise → operate, ~4.2s each; client choice 2026-10-18). No pause button (client choice): using the prev/next arrows stops autoplay; keyboard focus inside the hero pauses it; there is no hover pause because the hero fills the viewport.
- Entrance: `rise` (16px, 1s, ease-out) on hero elements only.
- Count-up on numbers is enhancement only: final values are in the HTML; only numbers below the fold animate.
- `prefers-reduced-motion`: all animation and smooth scroll off; the verb is static.

## Accessibility baseline

- `<main id="main">` + "Skip to content" link; header outside `main`.
- 44×44px minimum hit area for every interactive element (padding, no visual change).
- Visible focus: 2px orange outline, 4px offset. Selection colour themed.
- Decorative images `alt=""`; logos carry the client name as `alt`.

## Arabic / RTL (planned, review decision 22A)

- `dir="rtl"` on `<html>`; mirror layout with logical properties (`margin-inline`, `padding-inline`, `inset-inline`); flip directional arrows.
- Arabic typeface: IBM Plex Sans Arabic (body and display) paired with Bricolage for Latin numerals and brand words; check weights 400/600/700.
- Hero verb: Arabic letters join, so the letter-by-letter reveal must animate the **whole word** (fade/slide), never split into glyphs.
- Numerals: decide Western (1, 2, 3) vs Arabic-Indic (١، ٢، ٣) with Kalamntina before build; keep `font-variant-numeric: tabular-nums` for stats.
- Until the Arabic page exists, the toggle shows a "Soon" chip.

## Assets

- Brand: `/assets/brand/kalamntina-logo.svg`, `/favicon.svg`.
- Clients: colour in `/assets/clients/`, monochrome in `/assets/clients/mono/`. Sources in README.
- Photography: placeholders until the regional shoot (see `PHOTO-BRIEF.md`).
