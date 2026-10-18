# Design review: home page (2026-10-18)

Target: `index.html` at `9999d43` (live at kalamntina-preview.vercel.app).
Method: rendered full page at 1440px and 390px, code audit, contrast maths, plus an
independent second reviewer (Claude subagent, cold read). Mode: marketing page (persuade).

## Pre-review audit

- UI scope: 6 sections (hero, who we are, solutions + method, client impact + logo wall, diagnostic CTA, footer).
- No DESIGN.md existed; tokens lived inline in `index.html`, redefined per section.
- No prior design reviews.

## Approved decisions

| # | Area | Decision |
|---|---|---|
| 1 | Hero proof | 1A: replace the hero control bar with "Trusted by" + 5 grayscale logos (Amazon, Deloitte, Samsung, Zain, MBC); arrows move beside the verb |
| 2 | Repetition | 2A: one job per section. Hero = promise (1 sentence). Who we are = headline + stats (paragraph cut to 2 lines, no service list). Solutions intro = the 4-stage method only |
| 3 | CTA naming | 3A: "Request a diagnostic" everywhere (nav may read "Get a diagnostic"); remove "Browse jobs" from hero, Jobs stays in nav |
| 4 | Form states | 4A: inline error text + `aria-invalid`/`aria-describedby` + error summary; validate on blur after first submit; "Sending…" disabled button; network error keeps input + "Try again"; focus moves to success message |
| 5 | Challenge field | 5A: optional textarea "What's the challenge? (optional)", 3 rows, below the select |
| 6 | Initial render | 6A: "hire." and final stat values in server HTML; JS only animates; reduced-motion shows final values |
| 7 | Stats trust | 7A: "100% 12-month retention" (client confirms window); replace MENA with a real figure (e.g. countries served / years); placeholders flagged for client |
| 8 | Photography | 8A: write a regional photo brief (GCC/Jordan boardrooms, Arab professionals, natural light, desaturated to navy palette); Creative Tim template photos are placeholders until delivered |
| 9 | Hero motion | 9A: play the 4 verbs once, then rest on "hire." (or the visitor's pick); pause/play toggle; pause on hover/focus; reduced motion = static |
| 10 | Section kickers | 10A: remove the orange eyebrow labels; headings carry sections; keep #anchors |
| 11 | Logo tone | 11A: monochrome Ink Navy SVG/raster versions at 55% opacity, full colour on hover; Orange uses its knocked-out wordmark |
| 12 | Orange text | 12A: new token `--orange-text: #C2520B` for orange text on light surfaces (4.4:1, large text); `#FF7722` stays for buttons, dark surfaces, logo |
| 13 | Muted grey | 13A: `--muted: #5F6D80` (5.0:1 on Off White, 5.3:1 on white) replaces `#7A879A` and `#6B7A8F` |
| 14 | Design system | 14A: write DESIGN.md and consolidate CSS onto one token set |
| 15 | Mobile menu | 15A: full-screen Ink Navy overlay: 5 links at 28px Bricolage, Arabic toggle, "Request a diagnostic" pinned bottom; `aria-expanded`, Esc closes, focus trap, scroll lock |
| 16 | Landmarks | 16A: `<main id="main">` + skip link visible on focus |
| 17 | Touch targets | 17A: 44px minimum hit area via padding/pseudo-element, no visual change; arrows 42→44px |
| 18 | Mobile logo wall | 18A: below 620px, 3 columns at 80% scale, 12 best-known logos + "Show all 20 clients" expander |
| 19 | Card services | 19A: service list always visible; hover keeps bar + image zoom; card accessible name = pillar name |
| 20 | Mobile cards | 20A: below 620px, stack the 4 cards vertically at 4:3 (no horizontal scroller) |
| 21 | Dead links | 21A: in-page anchors where content exists (cards → #start with pillar preselected, case studies → #impact); unbuilt pages get a "Soon" tag and no-op; Privacy/Terms stay until copy exists |
| 22 | Arabic | 22A: toggle shows "Soon"; RTL rules go into DESIGN.md (mirrored layout, Arabic font e.g. IBM Plex Sans Arabic, verb animates as whole word, numerals decision) |
| 23 | Impact layout | 23A: sticky left column (top 120px) at ≥980px |
| 24 | Method CTA | 24A: delete unused `.method .note` / `.method .btn` CSS |
| 25 | Email rule | 25A: accept any valid email; personal domains tagged in backend |

Existing decision honoured, not reopened: Client voices stays on hold until approved testimonials exist.

## Visitor journey (accepted)

| Step | Visitor does | Visitor feels | Supported by |
|---|---|---|---|
| 1 | Lands on hero (5 s) | "Who is this, are they credible?" | Verb + one-line promise + logo strip (1A) |
| 2 | Who we are | Scale and credibility | 700+, 500+, qualified retention, real 4th figure (7A) |
| 3 | Solutions | "Do they do what I need?" | 4 pillars with visible services (19A) + method |
| 4 | Client impact | "Have they done it for people like me?" | Results ledger, sector tags, logo wall |
| 5 | Diagnostic CTA | "What happens if I raise my hand?" | 3 steps, "Not a sales call", direct contact |
| 6 | Submits | Relief, then waiting | Designed success state with focus (4A); no invented reply-time promise |

## Litmus scorecard (primary + independent reviewer)

| Check | Primary | Independent | Result |
|---|---|---|---|
| Brand unmistakable in first screen? | NO | NO | CONFIRMED NO → 1A, 8A |
| One strong visual anchor? | YES | YES | CONFIRMED |
| Scannable by headlines only? | YES | YES | CONFIRMED |
| Each section one job? | NO | NO | CONFIRMED NO → 2A |
| Cards necessary? | YES | NO | DISAGREE → 19A, 20A address both concerns |
| Motion improves hierarchy? | YES | NO | DISAGREE → 6A, 9A |
| Premium without decorative shadows? | YES | YES | CONFIRMED |

## NOT in scope

- Real form backend / endpoint (only the UI states are specified here).
- Inner pages (Solutions, About, Industries, Insights, Jobs, legal).
- Performance budget / LCP target: flagged by the second reviewer; revisit once real photography exists.

## What already exists (reuse)

- Brand tokens and fonts per the Brand Guidelines PDF (Ink Navy, Navy Mid, Off White, Ignite Orange; Bricolage Grotesque + Hanken Grotesk).
- 6px radius buttons, hairline dividers, results ledger pattern, supergraphic CTA pattern, method timeline.
- `vercel.json` deploy rules (`dev` never deploys).

## Implementation Tasks

Status 2026-10-18: T1–T11 built on `dev`; T12 brief written (`PHOTO-BRIEF.md`), photo swap pending client delivery.

- [x] **T1 (P1, human: ~4h / CC: ~30min)** Mobile nav: build the full-screen overlay menu (15A).
  - Files: `index.html`. Verify: 390px, open/close via button and Esc, focus trapped, all links reachable.
- [x] **T2 (P1, human: ~1h / CC: ~10min)** Contrast tokens: add `--orange-text`, `--muted`; replace failing pairs (12A, 13A).
  - Verify: re-run contrast check, all text ≥4.5:1 (large ≥3:1).
- [x] **T3 (P1, human: ~3h / CC: ~25min)** Form: states, challenge textarea, any-email rule (4A, 5A, 25A).
  - Verify: submit empty, bad email, simulated network failure, success focus.
- [x] **T4 (P1, human: ~1h / CC: ~10min)** Accessibility structure: `<main>`, skip link, 44px targets (16A, 17A).
- [x] **T5 (P1, human: ~2h / CC: ~15min)** Hero: logo proof strip, one-sentence promise, single CTA, verb plays once + pause, server-rendered verb (1A, 2A, 3A, 6A, 9A).
- [x] **T6 (P2, human: ~2h / CC: ~15min)** Content: trim Who we are and Solutions intro, qualify stats with client placeholders, remove kickers, unify CTA labels in nav and CTA section (2A, 3A, 7A, 10A).
- [x] **T7 (P2, human: ~3h / CC: ~30min)** Logo wall: monochrome assets, mobile 3-col + "Show all 20" (11A, 18A).
- [x] **T8 (P2, human: ~1h / CC: ~10min)** Solutions cards: services always visible; mobile stacked (19A, 20A).
- [x] **T9 (P2, human: ~1h / CC: ~10min)** Links: anchors + "Soon" tags, Arabic "Soon" state (21A, 22A).
- [x] **T10 (P2, human: ~30min / CC: ~5min)** Layout cleanup: sticky impact column, delete unused method CSS (23A, 24A).
- [x] **T11 (P2, human: ~3h / CC: ~30min)** DESIGN.md + token consolidation incl. RTL rules (14A, 22A).
- [x] **T12 (P3, human: ~1h / CC: ~10min)** Photo brief for Kalamntina (8A); swap photos when delivered.

## Design Review Completion Summary

```
  +====================================================================+
  |         DESIGN PLAN REVIEW — COMPLETION SUMMARY                    |
  +====================================================================+
  | System Audit         | No DESIGN.md (gap), 6-section marketing page |
  | Step 0               | 7/10 initial; focus: all 7 passes            |
  | Pass 1  (Info Arch)  | 6/10 → 9/10 after fixes                      |
  | Pass 2  (States)     | 4/10 → 9/10 after fixes                      |
  | Pass 3  (Journey)    | 6/10 → 8/10 after fixes (voices on hold)     |
  | Pass 4  (AI Slop)    | 5/10 → 8/10 after fixes (photos pending)     |
  | Pass 5  (Design Sys) | 5/10 → 9/10 after fixes                      |
  | Pass 6  (Responsive) | 4/10 → 9/10 after fixes                      |
  | Pass 7  (Decisions)  | 5 resolved, 0 deferred                       |
  +--------------------------------------------------------------------+
  | NOT in scope         | written (3 items)                            |
  | What already exists  | written                                      |
  | TODOS.md updates     | 2 items added                                |
  | Approved Mockups     | 0 generated (designer unavailable)           |
  | Decisions made       | 25 added to plan                             |
  | Decisions deferred   | 0                                            |
  | Overall design score | 4/10 → 8/10                                  |
  +====================================================================+
```

Scores "after fixes" apply once T1–T12 ship. Passes 3 and 4 stay at 8 until the client
supplies testimonials and regional photography.

### Unresolved Decisions

None.

## GSTACK REVIEW REPORT

| Review | Trigger | Why | Runs | Status | Findings |
|--------|---------|-----|------|--------|----------|
| CEO Review | `/plan-ceo-review` | Scope & strategy | 0 | — | — |
| Outside Review | Claude subagent (Codex not installed) | Independent 2nd opinion | 1 | completed (native, not external) | 4 hard rejections flagged, 2 confirmed |
| Eng Review | `/plan-eng-review` | Architecture & tests (required) | 0 | — | — |
| Design Review | `/plan-design-review` | UI/UX gaps | 1 | issues_open (fixes approved, not built) | score: 4/10 → 8/10, 25 decisions |
| DX Review | `/plan-devex-review` | Developer experience gaps | 0 | — | — |

- **OUTSIDE COVERAGE:** Codex unavailable (not installed); native Claude subagent completed. No external-provider coverage.
- **VERDICT:** No review CLEARED. Design decisions are complete; implementation of T1–T12 pending; eng review not run.

NO UNRESOLVED DECISIONS
