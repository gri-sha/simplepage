# simplepage — CLAUDE.md

## Project

Landing page for **simplegrad**, a deep learning framework. The page lives at [simplegrad.org](https://simplegrad.org).

## About simplegrad

- DL framework focused on code clarity and educational value
- Includes: autograd engine, nn stuff, and an experiment tracker + web dashboard (simpleboard)
- Completely open-source and non-commercial

## Stack

- Plain HTML + CSS + JS (no frameworks, no build tools)
- Web files live in `public/`: `index.html`, `styles.css`, `script.js`, `assets/`
- Only `public/` is deployed — repo files (README, CLAUDE.md, etc.) are not served

## Design

### Style

"Startup pitch" style, flat design. No drop shadows. Clean borders. Bold, punchy copy.

### Colors

All color values must be defined as CSS custom properties in `:root` in `styles.css`. **No hardcoded color values anywhere else** — this is the single source of truth.

| Variable | Value | Usage |
|---|---|---|
| `--bg` | `#F5F5F5` | Page background |
| `--fg` | `#151718` | Primary text |
| `--white` | `#ffffff` | Button backgrounds, surfaces |
| `--green` | `#34B87E` | Primary accent (docs CTA, labels) |
| `--green-dark` | `#2da870` | Green hover state |
| `--blue` | `#4474B8` | Secondary accent (section links) |
| `--border` | `rgba(21,23,24,0.11)` | Default borders and dividers |
| `--border-strong` | `rgba(21,23,24,0.35)` | Hover border states |
| `--muted` | `rgba(21,23,24,0.48)` | Secondary/body text |
| `--bg-glass` | `rgba(245,245,245,0.88)` | Frosted glass surfaces |
| `--surface-hover` | `rgba(21,23,24,0.04)` | Hover background tint |
| `--dot-pattern` | `rgba(21,23,24,0.15)` | Hero dot-grid dots |
| `--btn-border` | `rgba(21,23,24,0.2)` | Outline button border |
| `--btn-border-hover` | `rgba(21,23,24,0.45)` | Outline button hover border |
| `--btn-bg-hover` | `rgba(21,23,24,0.03)` | Outline button hover bg |

### Typography

Exactly **2 fonts** on the page — no others:

- **JetBrains Mono** — all headings (hero `<h1>`, section `<h2>`). Weights 700 and 800.
- **Plus Jakarta Sans** — all body text, buttons, nav. Loaded as variable font (`wght@200..800`) to enable smooth bold transitions on hover.

### Assets

All in `assets/`. Always reference via `<img src="assets/...">` — **never inline SVG `<path>` elements** directly in HTML.

- `simplegrad_logo_hor.svg` — horizontal simplegrad logo (desktop)
- `simplegrad_logo_ver.svg` — vertical simplegrad logo (mobile, ≤600px breakpoint)
- `simpleboard_logo_hor.svg` — horizontal simpleboard logo (used as section heading)
- `simpleboard_logo_ver.svg` — vertical simpleboard logo
- `favicon.svg` — favicon
- `github.svg` — GitHub octocat icon (`fill="#151718"`), used in header and hero buttons

### Layout

```
header          (60px, scrolls with page — not sticky)
hero section    (min-height: 100vh)
content-group   (min-height: calc(100vh - 52px))
footer          (height: 52px desktop / auto mobile)
```

**Two visual "screens":**
1. Header + hero fill exactly one viewport height — user must scroll to see more
2. Content group + footer fill exactly one viewport height — leftover space sits between the last section and the footer (not between the top divider and simpleboard)

### Header

- Not sticky — scrolls with the page
- Logo left, GitHub link (with icon) right
- Mobile: same layout

### Hero section

- Full viewport height (`min-height: 100vh`), flex-centered
- Background: subtle dot-grid pattern (`1.5px` dots, `26px` grid) that fades out toward the bottom
- Desktop: `simplegrad_logo_hor.svg` | Mobile (≤600px): `simplegrad_logo_ver.svg`
- Heading in JetBrains Mono 800, second line in `--green`
- Three buttons: **Tutorials** (outline/white bg) · **Documentation →** (primary green, main CTA) · **GitHub** (outline/white bg, with icon)
- Mobile buttons: equal width (`clamp(200px, 72vw, 260px)`), centered column, not full-width

### Content group (second section)

- Contains 3 sections: Simpleboard, Open Source, Contact
- Full-width top border separates it from the hero
- Inset dividers between sections: `min(640px, 100%)` wide, centered — just wider than the `580px` text block
- Section content max-width: `580px`, centered

**Section structure:**
- **Simpleboard**: `simpleboard_logo_hor.svg` as heading (no text heading), description, link
- **Open Source**: plain `<h2>` heading, description, link
- **Contact**: plain `<h2>` heading, description, link
- No colored label tags ("Built-in", etc.) on any section

**Section links (`.section-cta`):** use `font-variation-settings: 'wght'` to animate `600 → 800` on hover for a smooth bold effect (no layout shift). Color is `--blue`.

### Buttons

| Class | Background | Border | Text |
|---|---|---|---|
| `.btn-primary` | `--green` | `--green` | `--white` |
| `.btn-outline` | `--white` | `--btn-border` | `--fg` |

### Footer

- Copyright left: `© 2026 simplegrad.org`
- Email right: `contact@simplegrad.org` (clickable `mailto:`)

### Animations

- Hero elements: staggered `fadeUp` on page load (logo → heading → desc → buttons)
- Sections below hero: `IntersectionObserver` scroll-reveal (`opacity + translateY`) in `script.js`

## Links

| Destination   | URL                                       |
|---------------|-------------------------------------------|
| Landing page  | https://simplegrad.org                    |
| Docs          | https://docs.simplegrad.org               |
| GitHub        | https://github.com/gri-sha/simplegrad     |
| Tutorials     | https://tutorials.simplegrad.org          |
| Contact email | contact@simplegrad.org                    |

## Conventions

- HTML semantic and accessible
- All colors via CSS custom properties — no hardcoded values outside `:root`
- All SVG assets via `<img>` tags — no inline `<path>` in HTML
- JavaScript vanilla only — no libraries
- Mobile breakpoint: `600px`
