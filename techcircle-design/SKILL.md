---
name: techcircle-design
description: TechCircle Design System — HT Digital's tech news brand. Editorial serif-and-mono aesthetic on white, sharp corners, orange (#f99d1c) accent bar, blue (#0069ff) links, black header with mono secondary nav. Use whenever the user asks to create, design, build, mock up, audit, or extend any TechCircle UI — pages, hero blocks, news cards, event cards, podcast/video sections, polls, or brand assets. Triggers on "TechCircle", "tech circle", "design a TechCircle page/section/component", "in TechCircle style".
---

# TechCircle Design System

Design language extracted from TechCircle homepage builds v6.3 (primary) and v5.7 (cross-checked). It is an editorial news aesthetic: white surface, sharp corners everywhere (border-radius: 0), Young Serif headlines, IBM Plex Mono metadata, a 3px orange section bar, and restrained hover motion.

## How to use this skill

1. Read `references/tokens.css` and copy the `:root` block into every page you generate. Never invent new colors or fonts.
2. For component markup, copy patterns from `references/components.md` and adapt content.
3. `references/tokens.json` is the machine-readable token source for design-tool or code-gen workflows.
4. Follow the rules below — they are what make output look like TechCircle rather than a generic news site.

## Core identity rules (non-negotiable)

- **Sharp corners.** `border-radius: 0` on every card, button, input, image frame. The ONLY circles are play badges (50%).
- **Four typefaces, fixed roles.** Young Serif (weight 400) for ALL headings h1–h4; Inter for body; IBM Plex Mono for meta, badges, secondary nav, buttons, numbers; Poppins for primary nav and dropdowns; Lato 800 only for the logo wordmark.
- **Headings are never bold.** Young Serif ships at 400 — do not add font-weight.
- **Orange is an accent, not a surface.** `--mint: #f99d1c` appears as the 3px section-head bar, hover states, poll fills, and the outlined report/play button. Never use it as a large background.
- **Blue is for interaction.** `--blue: #0069ff` = author names, link hovers, focus rings.
- **Black header.** `#000` top bar; grey (`--neutral-200`) secondary nav in uppercase IBM Plex Mono.
- **1px hairline borders** (`--border: #e0e2e7`) divide everything; cards separate with borders, not shadows. Shadows only on dropdowns, drawers, and the hero-v3 frame.
- **Tinted full-bleed section bands** break the white page: video `#e5f5e5`, events cream `#f4f0e8` (cards `#fbf8f1`), dark panels `#0b0f14 → #111827`.

## Layout

- Content max-width **1280px** (`.wrap`), page max 1440px.
- Gutter: 0 at ≥1280px → 40px ≤1279px → 24px ≤860px → 16px ≤560px.
- Section rhythm: `padding-top: 110px` desktop → 36px mobile. Full-bleed bands use `padding: 80px 0` → 40–48px mobile.
- Grid gap is almost always **24px**.
- Section head: flex row, 3px `#F99D1C` bar + 40px Young Serif h2 (letter-spacing −1px), optional caption sub, `.view-all` outlined button right-aligned.
- Breakpoints: 1279, 1200, 1024, 900, 860, 560, 380. At ≤560px nav collapses to hamburger + slide-in drawer (`#0b0f14`), grids go single column, thumbs become 16/10 on top.

## Type scale (desktop → mobile)

Section h2 40→24 · hero h2 36–42→24 · card h3 24→20 · list h3 18–22 · poll question 32→22 · badges/meta 12–14px mono. Body 16/1.6. Headline letter-spacing is tight (−1 to +0.4px); badges wide (1.44px).

## Motion & hover grammar

Every interactive card gets exactly this, nothing more:

- Image zoom `scale(1.05)` (small thumbs 1.08), `transition: transform .35s ease`, cropped by the sharp frame.
- Headline underline: `text-decoration: underline; text-underline-offset: 3px; text-decoration-thickness: 1.5px`.
- Top-down background fill `#f6f7f9` (deeper cream `#efe8da` inside events band) via a `::before` growing `height: 0 → 100%` in .35s.
- Dark-panel items hover to `#13203a`; play badges hover to `--mint`.
- Always include `@media (hover:none)` and `@media (prefers-reduced-motion: reduce)` resets (see components.md).
- Focus: `*:focus-visible { outline: 2px solid var(--blue); outline-offset: 2px; }`.

## Component inventory

See `references/components.md` for copy-paste markup + CSS: header & secondary nav, mobile drawer, badges & meta row, section head, hero variants (classic split, v3 bordered + dark panel, v5 dark feature + list, v6 image-grid), CIO video band, podcast block, report CTA, opinion grid, media/POV cards, minutes rows, event cards, newsletter rows, hub grid, reader poll, footer.

## Google Fonts import

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Poppins:wght@400;500;600&family=Lato:wght@700;800;900&family=Young+Serif&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
```

## Don'ts

- No rounded corners, pill buttons, or card drop-shadows.
- No bold serif headings, no Young Serif in body copy or buttons.
- No gradients except image-overlay shades and the dark hero panel.
- No orange text on white except `--mint-600: #c47b14` (accessible variant).
- Don't replace the hover grammar with opacity fades or lift shadows.
