# Forsys Concept Design System — Master

Source of truth for colors, typography, spacing, components, and interaction patterns extracted from the concept site at `forsys-website-concept.netlify.app`. This document covers the redesigned visual language: purple/teal, frosted-glass nav, light lavender surfaces, and dark rounded CTA blocks.

> **How to use:** Read the relevant sections, copy the tokens into your project, and apply the component patterns verbatim. All tokens are defined as CSS custom properties in `:root` inside `base.css`. Do not introduce new tokens without updating this file — consistency across pages is the whole point.

---

## 1. Brand foundations

### 1.1 Core palette

All colors are defined as CSS custom properties in `forsys-new-2/assets/css/base.css`.

| Token | Hex | Role |
|---|---|---|
| `--white` | `#FFFFFF` | Card base, primary background on sections |
| `--lavender` | `#ECEEFF` | Hero gradient start, badge/pill fill |
| `--lavender-mid` | `#E4E8FF` | Hero gradient mid-stop |
| `--bg` | `#F5F6FF` | Section surface background (equivalent of `--surface`) |
| `--border` | `#E2E6F3` | Card & divider borders on light sections |
| `--border-strong` | `#C9CEEB` | Ghost-button borders, stronger dividers |
| `--purple` | `#6B48FF` | Primary brand — CTAs, links, labels, active states |
| `--purple-dark` | `#4B2FD4` | Button hover, pressed state |
| `--purple-light` | `rgba(107,72,255,0.08)` | Chip/pill fills, icon badge bg |
| `--purple-glow` | `rgba(107,72,255,0.22)` | Button box-shadows, card hover glow |
| `--teal` | `#00B4D8` | AI gradient end-stop, secondary brand accent |
| `--text-primary` | `#0D0D2B` | Body copy on light |
| `--text-secondary` | `#4A4F6A` | Supporting copy, nav links, card body |
| `--text-muted` | `#8B90A7` | Captions, labels, meta on light |

> **Contrast rule:** `--text-primary #0D0D2B` on `--white #FFFFFF` = ≥ 15:1. `--text-secondary #4A4F6A` on white = ≈ 6:1. Both pass WCAG AA at any size. Never use `--text-muted` alone for body copy.

### 1.2 Gradient pairings

| Name | CSS | Use |
|---|---|---|
| **AI Gradient** | `linear-gradient(90deg, #6B48FF 0%, #00B4D8 100%)` | Logo mark, stat numbers, progress/bar fills, footer tagline, gradient-text spans, avatar circles |
| **Hero Surface** | `linear-gradient(160deg, #ECEEFF 0%, #E8EEFF 50%, #EAF4FF 100%)` | Hero section background, testimonial section background |
| **Dark / CTA** | `linear-gradient(135deg, #0D0D2B 0%, #1E1B4B 100%)` | Footer bg, CTA inner card bg |
| **Gradient clipped text** | `background: var(--gradient-ai); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;` | Hero headline gradient words, stat numbers, footer tagline |

### 1.3 Light / dark section rules

| Context | Body bg | Card bg | Border | Text | Muted |
|---|---|---|---|---|---|
| **Light section** | `var(--white)` or `var(--bg)` | `var(--white)` | `var(--border)` | `var(--text-primary)` | `var(--text-secondary)` |
| **Surface section** | `var(--bg) #F5F6FF` | `var(--white)` | `var(--border)` | `var(--text-primary)` | `var(--text-muted)` |
| **Dark section** (footer, CTA card) | `var(--gradient-dark)` | `rgba(255,255,255,0.03)` | `rgba(255,255,255,0.1)` | `#fff` | `rgba(255,255,255,0.45–0.65)` |
| **Frosted nav** | `rgba(236,238,255,0.92)` + backdrop-blur 20px | — | `var(--border)` | `var(--text-primary)` | `var(--text-secondary)` |

### 1.4 Section background sequencing

Every multi-section page uses a strict alternating background sequence after the hero:

| Position | Background | Token |
|---|---|---|
| **Hero** | Lavender gradient | `var(--gradient-hero)` |
| **Section 1** (first after hero) | White | `var(--white)` |
| **Section 2** | Lavender surface | `var(--bg)` |
| **Section 3** | White | `var(--white)` |
| **Section 4** | Lavender surface | `var(--bg)` |
| … | Alternates | — |
| **CTA section** (always last) | Dark gradient | `var(--gradient-dark)` |

> **Rule:** The CTA section always uses `var(--gradient-dark)` regardless of its position — it is never part of the alternating sequence. The hero wave `::after` is white, so Section 1 being white creates a seamless visual blend from the hero gradient into the page body.

---

## 2. Typography

### 2.1 Font stacks (Google Fonts)

Loaded in `<head>` on every page:

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=Space+Grotesk:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

| Font | Weights | Role |
|---|---|---|
| **Space Grotesk** (sans-serif) | 400–800 | Headlines, display text, stat numbers, testimonial quote, CTA title |
| **Inter** (sans-serif) | 300–900 | Body copy, nav, buttons, labels, captions — default `body { font-family }` |

> **Rule:** Only two font families are used. There is no serif font in this design system. Space Grotesk handles all display; Inter handles all body/UI.

### 2.2 Type scale

| Token | Selector exemplar | Size | Weight | Line-height | Letter-spacing | Family |
|---|---|---|---|---|---|---|
| **Display XL** | `.hero-headline` | `clamp(42px, 5.8vw, 80px)` | 800 | 1.04 | -0.038em | Space Grotesk |
| **Display L** | `.section-title` | `clamp(32px, 3.8vw, 54px)` | 800 | 1.08 | -0.03em | Space Grotesk |
| **Display M** | `.cta-title` | `clamp(28px, 3.5vw, 48px)` | 800 | — | -0.03em | Space Grotesk |
| **Display S** | `.test-quote` | `clamp(20px, 2.4vw, 32px)` | 600 | 1.45 | -0.015em | Space Grotesk |
| **Stat Number** | `.stat-number` | 40px | 800 | 1 | — | Space Grotesk (gradient-clipped) |
| **Partner Name** | `.partner-card-name` | 20px | 800 | — | — | Inter |
| **Body L** | `.section-sub`, `.hero-sub` | 17–18px | 400–500 | 1.65 | — | Inter |
| **Body M** | `.wwd-desc`, `.sol-desc`, `.split-card-desc` | 12.5–13.5px | 400 | 1.6 | — | Inter |
| **UI / Button** | `.btn-hero-primary`, `.nav-link` | 14–16px | 500–700 | — | — | Inter |
| **Section label** | `.section-label` | 11.5px | 600 | — | 0.1em | Inter UPPERCASE |
| **Tag / Chip** | `.tag`, `.sol-badge` | 10–10.5px | 700 | — | 0.06em | Inter UPPERCASE |
| **Mega-col title** | `.mega-col-title` | 10.5px | 700 | — | 0.08em | Inter UPPERCASE |
| **Nav link** | `.nav-link` | 14px | 500 | — | — | Inter |
| **Mega sub-link** | `.mega-col ul li a small` | 11px | 400 | — | — | Inter |
| **Footer heading** | `.footer-col h4` | 11px | 700 | — | 0.08em | Inter UPPERCASE |
| **Footer link** | `.footer-col ul a` | 13.5px | 400–500 | — | — | Inter |

### 2.3 Typography rules

- **Gradient text spans** — wrap words in `.gradient-text` inside `.hero-headline` to apply the AI gradient clip (purple→teal). These are block `<div>` children of `.hero-headline`, not inline `<em>` elements (unlike the current site which uses `<em>` + Newsreader italic).
- **UPPERCASE text** — always tracked (letter-spacing ≥ 0.06em). Used for: section labels, mega-col titles, tags/badges, footer headings.
- **Max line length** — `.section-sub` capped at `max-width: 560px`. Never raw prose wider than 720px.
- **Line height** — never below 1.6 for body; 1.04–1.08 for display. Hero sub at 1.65.
- **Letter-spacing** — negative on all display (−0.03 to −0.038em). Never negative on body.

---

## 3. Radii

Unlike the current site's asymmetric "brand shape" (sharp top-left), this design uses **fully symmetric radii** on all surfaces. There is no asymmetric motif.

| Token | Value | Use |
|---|---|---|
| `--radius-card` | `16px` | Standard cards: wwd-card, sol-card, split-card, ind-card, dropdown, mockup-card |
| `--radius-card-lg` | `18px` | Large cards: stats-bar, partner-card, wwd-card (18px variant) |
| **Nav mega-menu** | `16px` | Mega-menu popup panel |
| **Nav dropdown** | `12px` | Narrow dropdown popups |
| **CTA inner card** | `24px` | Dark rounded CTA section card |
| **Platform visual** | `20px` | Right-side sticky panel in platforms section |
| **Accordion items** | divider only, no radius | Bordered list style |
| **Icon badge** | `14px` | Split-card icon containers (52×52 px) |
| **Logo mark** | `8px` | Nav logo "F" square |
| `--radius-pill` | `100px` | Buttons (primary, secondary, ghost), section labels, tags, badge pills, platform tabs, slide dots |
| **Circle** | `50%` | Testimonial avatar, badge dot |

> **Rule:** The pill (`100px`) is the dominant interactive radius. Cards and panels always use one of the card radii above. No asymmetric corners anywhere in this system.

---

## 4. Spacing scale

| Token | px | Use |
|---|---|---|
| **2xs** | 4 | Tight icon gaps |
| **xs** | 8 | Badge dot gap, slide-dot gap, button icon gap |
| **sm** | 10–12 | Nav link gap, footer list gap |
| **md** | 14–16 | Section label margin, card internal gap |
| **lg** | 18–24 | Pill padding, card internal padding |
| **xl** | 28–32 | Platform-tab margin-bottom, section header margin |
| **2xl** | 36–48 | Hero-actions margin, section header margin-bottom |
| **3xl** | 52–56 | Stats-bar margin-bottom, ticker padding |
| **4xl** | 64 | Split-section column gap, footer padding-top |
| **section** | `96px 48px` | Default section vertical+horizontal padding |
| **hero top** | `calc(68px + 32px)` | Inner-page hero padding-top = nav height + 32px extra (compact, content-first) |
| **hero bottom** | `160px` desktop / `100px` mobile | Inner-page hero padding-bottom — leaves 80px of visible gradient above the 80px `::after` wave |

**Container widths:**
- `1120px` — default max-width (`--container-max`): all sections, footer grid
- `860px` — hero content column max-width
- `1000px` — hero mockup max-width
- `820px` — testimonial inner
- `700px` — stats bar max-width (centered)
- `560px` — section sub max-width

---

## 5. Shadows

| Token | Value | Use |
|---|---|---|
| **Subtle card** | `0 8px 32px rgba(13,13,43,0.08)` | Mockup cards, stats bar, platform visual |
| **Card hover** | `0 8px 32px rgba(107,72,255,0.10)` | Hover lift on wwd-card, sol-card, ind-card |
| **Split card hover** | `0 6px 24px rgba(107,72,255,0.09)` | Split-card and partner-card hover |
| **Nav** | `0 1px 24px rgba(13,13,43,0.10)` | Nav shadow when scrolled (JS-applied) |
| **Mega-menu** | `0 20px 60px rgba(13,13,43,0.12)` | Mega-menu popup depth |
| **Dropdown** | `0 12px 40px rgba(13,13,43,0.10)` | Narrow dropdown popup depth |
| **Primary button** | `0 6px 24px var(--purple-glow)` | Resting purple CTA buttons |
| **Primary button hover** | `0 10px 32px var(--purple-glow)` | Hovered purple CTA buttons |
| **Ghost button hover** | `0 8px 32px rgba(0,0,0,0.20)` | White CTA button hover (on dark sections) |
| **Nav CTA** | `0 4px 16px var(--purple-glow)` | Nav primary button resting |
| **Testimonial avatar** | `0 4px 16px var(--purple-glow)` | Avatar circle |
| **Platform visual** | `0 8px 40px rgba(13,13,43,0.07)` | Right panel in platform section |

> **Rule:** Colored shadows (`--purple-glow`) only appear on purple fill elements. Neutral dark shadows (`rgba(13,13,43,…)`) on structural containers like nav and dropdowns.

---

## 6. Motion

### 6.1 Durations

| Name | Duration | Easing | Use |
|---|---|---|---|
| **Micro** | 150 ms | ease / `linear` | Color, opacity, border-color on hover |
| **Standard** | 200–250 ms | ease | Nav shadow, nav-link color, button hover, mega-menu open, card hover lift |
| **Slide-dot expand** | 250 ms | ease | Dot width 8px → 24px on active |
| **Card entrance** | 450 ms | ease | Scroll-fade: `opacity 0→1`, `translateY 18px→0` |
| **Entrance stagger** | 70–80 ms per card | — | Cards stagger by index % 4 via `setTimeout` |
| **Ticker scroll** | 28 s | linear, infinite | `translateX(0 → -50%)` on `.ticker-track` |
| **Badge dot blink** | 2 s | — | `opacity 1→0.3`, `scale 1→0.65`, infinite |
| **Hero slideshow** | 4000 ms interval | — | Auto-advance hero slides (className swap) |
| **Hero entrance (all pages)** | 600 ms | `cubic-bezier(0.22, 0.61, 0.36, 1)` | `opacity 0→1` + `translateY(24px→0)` on page load, `animation-fill-mode: both`. Applies to home page (`.hero`) and all inner-page heroes. |
| **Hero entrance stagger** | — | — | Home: badge 0.05s → headline 0.15s → sub 0.25s → slide-dots 0.30s → actions 0.35s → mockup 0.50s. Inner pages: eyebrow 0.05s → title 0.15s → desc 0.25s → actions 0.35s. |

### 6.2 Reduced motion

Always respect the user preference:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
  .ticker-track { animation: none; }
}
```

### 6.3 Interaction primitives

- **Hover lift:** `transform: translateY(-3px)` on cards (wwd-card, sol-card, ind-card, partner-card). `translateY(-2px)` on primary buttons. Never scale on cards — it causes layout shifts.
- **Nav button hover:** `translateY(-1px)` only on `.btn-nav-primary`.
- **Chevron rotate:** nav `<svg>` rotates `180deg` on `.nav-item:hover > .nav-link svg`.
- **Sol-card arrow:** `.sol-arrow` transitions from `opacity: 0` + `translate(0)` → `opacity: 1` + `translate(3px, -3px)` on card hover.
- **Badge dot:** Uses `@keyframes blink` — scale + opacity pulse, 2s infinite.
- **Ticker pause:** `.ticker-track:hover { animation-play-state: paused; }`.

---

## 7. Breakpoints

Desktop-first authoring.

| Range | Behavior |
|---|---|
| ≥ 1025 px | Full desktop. All grids multi-column, nav mega-menus and dropdowns visible |
| ≤ 1024 px | Tablet. `.nav-center` hides (hamburger needed), hero-mockup 2-col, wwd-grid 2-col, split-grid 1-col, platform-layout 1-col, footer 2-col |
| ≤ 768 px | Mobile. Nav padding collapses to 20px, sections to 64px 24px, cta-inner to 48px 24px, stats-bar 2-col, solutions-grid 1-col, partner-grid 1-col, wwd/hero-mockup/ind-grid all 1-col, split-cards 1-col, footer 1-col |

---

## 8. Components

### 8.1 Navigation (`<nav>`)

- **Position:** fixed, 68px tall (`--nav-h`), `z-index: 200`.
- **Base state (always):** frosted glass — `background: rgba(236,238,255,0.92)`, `backdrop-filter: blur(20px)`, `border-bottom: 1px solid var(--border)`. This nav is always "light" — no dark/transparent mode, no logo swap needed.
- **Scrolled state:** JS adds `box-shadow: 0 1px 24px rgba(13,13,43,0.10)` when `scrollY > 20`.
- **Logo:** `.nav-logo-mark` — 34×34 box, 8px radius, AI gradient fill, bold "F" white text. `.nav-logo-text` — 18px/800, `--text-primary`.
- **Nav links:** 14px/500, `--text-secondary` → `--text-primary` on hover. No underline. 8px border-radius on the link itself.
- **Mega menu:** Triggered on `.nav-item:hover`. 4-column grid (`repeat(4, 1fr)`) with column dividers. Min-width 860px. 16px radius, `box-shadow: 0 20px 60px rgba(13,13,43,0.12)`. Opens with `opacity 0→1` + `translateY(-6px→0)` over 180ms.
- **Dropdown:** Narrow single-column, min-width 210px, 12px radius. Same show animation.
- **Link hover:** `color: var(--purple)`, `background: var(--purple-light)`, 6–8px radius.
- **Right buttons:**
  - `.btn-nav-ghost` — white bg, 1.5px `--border-strong` border, pill radius, hover: border → purple.
  - `.btn-nav-primary` — purple fill, pill radius, `box-shadow: 0 4px 16px var(--purple-glow)`, hover: dark-purple + `translateY(-1px)`.

### 8.2 Section label + header

```html
<div class="section-label">Label Text</div>
<h2 class="section-title">Headline <span class="gradient-text">Gradient Word</span></h2>
<p class="section-sub">Supporting subhead, max 560px.</p>
```

- `.section-label` — outlined pill: `border: 1.5px solid var(--purple)`, `color: var(--purple)`, pill radius, 11.5px/600, uppercase, letter-spacing 0.1em.
- `.section-title` — Space Grotesk, `clamp(32px, 3.8vw, 54px)`, 800, letter-spacing −0.03em, `--text-primary`.
- `.section-sub` — Inter 17px, `--text-secondary`, line-height 1.65, max-width 560px.
- Centered variant: add `.text-center` to `.section-header` wrapper; `.section-sub` gets `margin: 0 auto`.

### 8.3 Hero section

**Home page hero (`.hero`)**
- Full-viewport, `min-height: 100vh`, centered flex column.
- Background: `var(--gradient-hero)` — lavender-to-pale-blue (`linear-gradient(160deg, #ECEEFF 0%, #E8EEFF 50%, #EAF4FF 100%)`).
- Bottom edge: CSS `::after` wave — `clip-path: ellipse(55% 100% at 50% 100%)` with `var(--white)` fill, 80px tall.
- **Hero badge:** outlined pill with blinking dot. Dot is 7×7 circle using `@keyframes blink`.
- **Headline slideshow:** 5 slides rotate every 4s via `setInterval`. Each `.slide-title` is `display: none`; only `.active` shows. Gradient word uses `.gradient-text`. No CSS transition — instant class swap.
- **Slide dots:** pill-shaped dots (`border-radius: 100px`). Inactive: 8×8, `--border-strong`. Active: 24×8, `--purple`.
- **Hero CTA row:** `.btn-hero-primary` (purple fill) + `.btn-hero-secondary` (ghost with glass bg `rgba(255,255,255,0.7)`).
- **Stats bar:** 4-col grid, white card, `--radius-card-lg`, subtle shadow. Stat numbers are gradient-clipped Space Grotesk/800/30px.
- **Mockup cards:** 4-col grid below the copy; `aria-hidden="true"`. 14px radius, white bg, subtle shadow. Shows product UI data (progress bars, tags, stats).
- **Entrance animation:** Staggered `@keyframes heroFadeUp` (`opacity: 0, translateY(24px)` → `opacity: 1, translateY(0)`), 0.6s, `cubic-bezier(0.22, 0.61, 0.36, 1)`, `animation-fill-mode: both`. Delays: `.hero-badge` 0.05s → `.hero-headline` 0.15s → `.hero-sub` 0.25s → `.slide-dots` 0.30s → `.hero-actions` 0.35s → `.hero-mockup` 0.50s. `.hero-badge` is scoped as `.page-home .hero-badge` since the class is defined in `base.css`. Disabled automatically by the global `prefers-reduced-motion` rule in `base.css`.

**Inner page heroes (`.svc-hero`, `.sol-hero`, `.fs-hero`, `.ind-hero`, `.par-hero`, `.res-hero`, `.co-hero`)**
- Background: `var(--gradient-hero)` — same light lavender as home hero. **Not dark** — `var(--gradient-dark)` is reserved for the footer and CTA inner card only.
- Padding: `calc(var(--nav-h) + 32px) 48px 160px` (desktop); `calc(var(--nav-h) + 16px) 24px 100px` (mobile ≤768px). The 160px bottom padding ensures 80px of visible gradient background is visible below the last content element before the 80px `::after` wave begins — never reduce below 160px or buttons will clip the wave. Bottom-edge wave: same `::after` clip-path wave as home.
- Decorative `::before`: `radial-gradient(ellipse 60% 50% at 50% 0%, rgba(107,72,255,0.07) 0%, transparent 70%)` — very subtle purple glow.
- **Content alignment:** Always centered — `text-align: center`, `align-items: center`, `flex-direction: column` on the inner wrapper.
- **Eyebrow tag/badge:** `background: var(--purple-light)`, `border: 1px solid rgba(107,72,255,0.25)`, `color: var(--purple)` — pill, 11.5px/600, uppercase.
- **Title:** Space Grotesk `clamp(42px, 5.8vw, 80px)` / 800 / line-height 1.04 / letter-spacing −0.038em / `color: var(--text-primary)`. Max-width 860px, `margin: 0 auto 20px`. Gradient word uses `.gradient-text`.
- **Description:** Inter 18px / `color: var(--text-secondary)` / `max-width: 580px` / `margin: 0 auto 36px`.
- **CTA row:** `justify-content: center`. `.btn-hero-primary` scoped override: purple fill, `var(--purple-glow)` shadow. `.btn-hero-secondary` scoped override: `rgba(255,255,255,0.7)` bg, `--border-strong` border, `--text-secondary` color.
- **Partner/product logos** (solutions & partnerships pages): `filter: none`, `opacity: 0.85–0.9` (natural colors on light bg). Logo separator: `background: var(--border-strong)`.
- **Product icon** (forsys-solutions pages): `background: var(--purple-light)`, `border: 1px solid rgba(107,72,255,0.25)`, `color: var(--purple)`.
- **Entrance animation:** Staggered fade-up — each hero child uses a named `@keyframes` (`opacity: 0, translateY(24px)` → `opacity: 1, translateY(0)`), 0.6s, `cubic-bezier(0.22, 0.61, 0.36, 1)`, delays: logos/eyebrow 0.05–0.1s → title 0.15–0.18s → desc 0.25–0.28s → actions 0.35–0.38s. The global `prefers-reduced-motion` rule in `base.css` disables this automatically.

### 8.4 Card patterns

**Service / Solution card (`.wwd-card`, `.sol-card`)**
- Background: `var(--bg)`, border: `var(--border)`. On hover: `var(--white)`, border → `var(--purple)`, shadow, `translateY(-3px)`.
- Sol-card adds `.sol-arrow` (↗) at `opacity: 0` top-right, reveals on hover with offset translate.
- `.sol-badge` — small outlined pill, purple, uppercase, 10.5px.

**Split card (`.split-card`)**
- White bg, `--radius-card`, `--border`. Hover: purple border + shadow.
- Icon container: 44×44, 12px radius, `var(--purple-light)` bg with `rgba(107,72,255,0.15)` border, `--purple` icon stroke.

**Industry card (`.ind-card`)**
- `var(--bg)`, `--radius-card`, centered text+icon. Hover: white bg, purple border, shadow, `translateY(-3px)`.

**Partner card (`.partner-card`)**
- White bg, `--radius-card-lg`, centered. Name: 20px/800. Hover: purple border + shadow + `translateY(-3px)`.
- `.partner-card-link` — inline purple link, gap expands on hover (8px → 10px).

**Partnership ecosystem overview panel (`.par-overview-panel`)**

Used on all 5 technology partner pages (RocketLane, Provus, m3ter, ServiceNow, Flosum) as the right-column "Partnership Highlights" card.

- Background: `var(--white)`, `--radius-card-lg` border-radius, `border-top: 3px solid var(--purple)` accent, `box-shadow: 0 4px 24px rgba(107,72,255,0.07)`. Add `aria-label="Partnership highlights"`.
- Panel label (`.par-overview-panel-title`): 11.5px/700 Inter uppercase, `color: var(--purple)` (not muted).
- **Company logo (`.par-partner-logo`):** `<img>` element, `height: 36px; width: auto; max-width: 160px; object-fit: contain; display: block; margin-bottom: 16px;`. Use the partner SVG from `assets/images/`. **Never** use `.par-partner-name` text in place of the logo on technology partner pages.
- Tagline (`.par-partner-tagline`): Inter 13.5px, `--text-muted`, left-aligned (no `text-align: center`).
- Stats list (`.par-panel-stats`): `role="list"`. Each row is `.par-panel-stat-row` (`role="listitem"`) — flex, `justify-content: space-between`, `align-items: baseline`, `gap: 12px`, `padding: 13px 0`, `border-top: 1px solid var(--border)` dividers. First child: `border-top: none`.
  - `.par-panel-stat-label`: 11px/700 Inter, uppercase, letter-spacing 0.07em, `--text-muted`, `white-space: nowrap`.
  - `.par-panel-stat-value`: 13.5px/500 Inter, `--text-primary`, `text-align: right`, line-height 1.4.

**Canonical `par-overview-panel` HTML structure:**
```html
<div class="par-overview-panel" aria-label="Partnership highlights">
  <div class="par-overview-panel-title">Partnership Highlights</div>
  <img src="../assets/images/CompanyName_logo.svg" alt="Company Name" class="par-partner-logo">
  <div class="par-partner-tagline">Company tagline</div>
  <div class="par-panel-stats" role="list">
    <div class="par-panel-stat-row" role="listitem">
      <span class="par-panel-stat-label">Focus</span>
      <span class="par-panel-stat-value">Short value</span>
    </div>
    <!-- repeat for each stat -->
  </div>
</div>
```

**Partnership "Why It Matters" card (`.par-value-card`)**
- White bg, `--radius-card`, `--border`, padding `28px 24px`. Hover: purple border + `0 6px 24px rgba(107,72,255,0.09)` shadow + `translateY(-3px)`.
- Icon container (`.par-value-icon`): 44×44px, 12px radius, `var(--purple-light)` bg, `rgba(107,72,255,0.15)` border. **SVG inside must be constrained to `width: 20px; height: 20px;`** — do not let SVG fill the full container.
- Card title (`.par-value-title`): Space Grotesk **17px**/700, `--text-primary`, line-height 1.3.
- Card body (`.par-value-desc`): Inter **14px**, `--text-secondary`, line-height 1.65.

**Partnership ecosystem bullet list (`.par-overview-points`)**
- Each `<li>` contains an inline SVG checkmark — **no `::before` pseudo-element** (CSS suppresses it with `display: none`).
- SVG: 18×18px, `color: var(--purple)`, `stroke-width: 2`, `margin-top: 2px`.
- Item text: Inter 15px, `--text-secondary`, line-height 1.55, flex gap 12px.

**Strategic partnership "Solutions We Deliver" grid (`.par-solutions-grid`)**

> **Rule:** The grid always produces exactly **2 rows**. Column count = `numberOfCards ÷ 2`.

| Cards | Columns | Class to use |
|---|---|---|
| 6 (e.g. Salesforce page) | 3 | `.par-solutions-grid` (default — `repeat(3, 1fr)`) |
| 4 (e.g. Conga, Oracle pages) | 2 | `.par-solutions-grid par-solutions-grid--2col` |

- `.par-solutions-grid--2col` overrides to `grid-template-columns: repeat(2, 1fr)` and is defined in `partnerships.css`.
- Responsive breakpoints on the base class handle both variants: ≤1024px → `repeat(2, 1fr)`, ≤768px → `1fr`.
- **Never** use `repeat(4, 1fr)` or a single row layout. **Never** use an inline `<style>` block in `<head>` to override the grid — use the modifier class only.

### 8.5 Stats bar (`.stats-bar`)

4-column grid, max-width 700px, centered. White bg, `--radius-card-lg`, `box-shadow: 0 8px 32px rgba(13,13,43,0.08)`. Each column separated by `border-right: 1px solid var(--border)`.

- `.stat-number` — Space Grotesk 30px/800, gradient-clipped (AI gradient).
- `.stat-label` — Inter 11.5px, `--text-muted`.

### 8.6 Platform tabs + accordion

**Tabs (`.ptab`) — Home page pill-track + sliding indicator**
- Container (`.platform-tabs`) is `position: relative` to anchor the absolute-positioned slider.
- A `<div class="ptab-slider" aria-hidden="true">` sits as the first child of `.platform-tabs`. It is `position: absolute; top: 4px; bottom: 4px; background: var(--purple); border-radius: var(--radius-pill); box-shadow: 0 2px 10px var(--purple-glow); pointer-events: none; z-index: 0; will-change: left, width`. JS drives `left` and `width` via inline styles; CSS provides `transition: left 0.22s cubic-bezier(0.4, 0, 0.2, 1), width 0.22s cubic-bezier(0.4, 0, 0.2, 1)`.
- Each `.ptab` is `position: relative; z-index: 1` so it renders above the slider.
- **Font:** `.ptab` always sets `font-family: Inter, sans-serif` explicitly — `<button>` elements do not inherit `font-family` from `body` in most browsers (UA resets it to system-ui). Without this, tabs render in a different font than the accordion headers and CTA in the same section.
- **No-JS fallback:** `.platforms .ptab.active` retains `background: var(--purple); color: #fff` in CSS. Once JS initialises, it adds `.tabs-js-ready` to `.platforms`; then `.platforms.tabs-js-ready .ptab.active { background: transparent; box-shadow: none; }` removes the duplicate fill so only the slider shows it.
- **Init without flash:** JS sets `slider.style.transition = 'none'`, positions the slider over the default active tab, adds `.tabs-js-ready`, then re-enables transition after two `requestAnimationFrame` calls to prevent the slider from animating from `left: 0` on page load.
- **Tab switch:** JS removes `.active` from all tabs, adds it to the clicked tab, calls `moveSlider(tab)` (sets `left = tab.offsetLeft`, `width = tab.offsetWidth`), and updates `aria-selected`. Also calls `platform-content` class swap — the old content loses `.active`, the new gains it (triggering `@keyframes platformContentIn`).
- `role="tablist"` / `role="tab"` / `aria-selected` / `aria-controls` — ARIA kept in sync on every click.

**Accordion (`.accord-list` / `.accord-item`) — animated open/close**
- **Opening/closing:** Body uses `max-height: 0; overflow: hidden; padding: 0 12px; transition: max-height 0.28s ease, padding-bottom 0.28s ease` (closed) → `max-height: 280px; padding-bottom: 16px` (open). This replaces the former `display: none/block` approach and gives a smooth slide-down/up on all pages globally (`base.css`).
- On the home page `.platforms` section, each item also gets a **3px left accent border**: `border-left: 3px solid transparent`. Active item: `background: rgba(107,72,255,0.04); border-left-color: var(--purple)`. Hover (inactive): `background: rgba(107,72,255,0.025); border-left-color: var(--border-strong)`.
- **Toggle behaviour:** JS allows closing an already-open item (click on active header → closes it). Previously clicking an active header re-opened it silently.
- Header: flex row, 15px/600, `--text-secondary`. Active header: `--purple`.
- Toggle indicator: CSS `::after` — shows `+` (inactive) or `−` (active), purple when active.
- Items use `·` (dot) before each list entry via `::before`.
- Each platform panel ends with a `.ptab-cta` anchor: `inline-flex; gap: 6px; font-size: 13.5px; font-weight: 600; color: var(--purple)`. Hover: `gap: 10px`. Links to the relevant partnership page. Includes a right-arrow SVG.
- The "Other" tab uses individual accordion items per partner (RocketLane, Provus, M3ter, ServiceNow, Flosum) — never a single flat list.

**Tab content transition (`@keyframes platformContentIn`)**
- When a new `.platform-content` receives `.active`, it plays `opacity: 0 + translateY(5px)` → `opacity: 1 + translateY(0)` over 0.22s ease. Defined in `home.css` scoped to `.platforms .platform-content.active`.

### 8.7 Platform visual panel (`.platform-visual`)

Sticky right panel (top: 96px) in the platform section. 20px radius, `box-shadow: 0 8px 40px rgba(13,13,43,0.07)`. **Background follows section surface inversion:** on a white section (`.platforms`), panel uses `var(--bg)`. Contains:
- `.pv-header` — Space Grotesk 14px/700, `--text-primary`. Has `border-bottom: 1px solid var(--border)` and `padding-bottom: 14px` to visually separate from the data rows.
- `.pv-row` — key-value rows. On `var(--bg)` panel → `background: var(--white); box-shadow: 0 1px 4px rgba(13,13,43,0.04)`. 10px radius.
- `.pv-row-val` — Space Grotesk 16px/800, **gradient-clipped** (AI gradient). Never use ad-hoc hex colors (e.g. `color:#16A34A`) — the gradient is used for all stat values consistently.
- `.pv-bar` / `.pv-bar-fill` — progress bars with AI gradient fill; bar track uses `background: var(--border)`; height 6px; pill radius; `margin-bottom: 10px`.

### 8.8 Tag / badge chips

```css
.tag { border-radius: var(--radius-pill); padding: 3px 10px; font-size: 10.5px; font-weight: 700; letter-spacing: 0.06em; text-transform: uppercase; }
.tag-purple { background: var(--purple-light); color: var(--purple); border: 1px solid rgba(107,72,255,0.2); }
.tag-green  { background: #DCFCE7; color: #16A34A; }
.tag-blue   { background: #DBEAFE; color: #2563EB; }
```

Used inside mockup cards to show status labels. Section labels (`.section-label`) use the same pill shape with a `1.5px solid var(--purple)` border and transparent background.

### 8.9 Ticker (`.ticker-section`)

Infinite-scroll horizontal logo ticker.

- White bg, top/bottom `1px solid var(--border)`, `padding: 52px 0`.
- `.ticker-track` animates `translateX(0 → -50%)` over 28s linear infinite. Pauses on hover.
- Edge fade: `::before` (left) and `::after` (right) use `linear-gradient` from white → transparent, width 120px, `z-index: 2`.
- Each `.ticker-item`: 44px tall, `--border` right divider, 15px/700, `--text-muted`.
- Items duplicated in HTML for seamless loop.
- Mark the container `aria-hidden="true"` — purely decorative.

### 8.10 Trusted strip (`.trusted-strip`)

Static partner logo row. White bg, `border-bottom`. Logos as text badges (`.trusted-badge`) at `opacity: 0.45`, hover → `0.85`.

### 8.11 Testimonial

Background: `var(--gradient-hero)` (same as hero), `border-top: 1px solid var(--border)`.

- Max-width 820px, centered.
- Star row: Unicode stars `★★★★★`, purple color, 20px, letter-spacing 4px.
- Quote: `<blockquote class="test-quote">` — Space Grotesk `clamp(20px, 2.4vw, 32px)` / 600 / line-height 1.45 / letter-spacing −0.015em.
- Author row: 52×52 circle avatar (AI gradient fill + purple-glow shadow, initial letters), name 15px/700, role 13px/`--text-muted`.

### 8.12 CTA section (canonical pattern)

> **Rule:** All 53 non-home pages use `cta-section`/`cta-inner`. The legacy `cta-strip`/`cta-strip-inner` pattern is **fully retired** — do **not** use it. It is flat, unstyled, and inconsistent with the design system. All `cta-strip` CSS has been removed from the stylesheets.

#### Canonical HTML structure

```html
<section class="cta-section" aria-labelledby="cta-page-title">
  <div class="cta-inner">
    <div class="cta-glow" aria-hidden="true"></div>
    <h2 class="cta-title" id="cta-page-title">Ready to [verb] your <span class="gradient-text">[Key Noun]</span>?</h2>
    <p class="cta-sub">1–2 sentences describing what happens when they click. Max ~100 chars per line.</p>
    <div class="cta-btns">
      <a href="mailto:info@forsysinc.com" class="btn-cta-white">Get Started &rarr;</a>
      <a href="../resources/customer-stories.html" class="btn-cta-outline">View Customer Stories</a>
    </div>
  </div>
</section>
```

#### Layout & visual rules

- `.cta-section` — white bg, `96px 48px` padding (collapses to `64px 24px` at ≤768px).
- `.cta-inner` — dark gradient bg (`var(--gradient-dark)`), `24px` radius, `80px 64px` inner padding (collapses to `48px 24px` at ≤768px), centered text, `overflow: hidden`.
- Dot-grid overlay: `cta-inner::after` with `radial-gradient(rgba(107,72,255,0.12) 1.5px, transparent 1.5px)`, `background-size: 24px 24px`.
- `.cta-glow` — always present. 600×600 radial gradient purple orb, absolutely centered inside `cta-inner`, `pointer-events: none`, `aria-hidden="true"`.
- `.btn-cta-white` — white bg, purple text, pill radius, shadow `0 4px 20px rgba(0,0,0,0.15)`. Hover: `translateY(-2px)` + heavier shadow.
- `.btn-cta-outline` — transparent bg, `1.5px solid rgba(255,255,255,0.3)`, white text at 85% opacity. Hover: border → 70%, text → 100%.

#### Content guidelines

**`cta-title`**
- Pattern: "Ready to [verb] your [Key Noun]?" — always a question or strong declarative.
- The key noun (product name, topic, or page subject) must be wrapped in `<span class="gradient-text">` to apply the AI gradient clip.
- Examples: "Ready to transform your **Revenue Operations**?", "Ready to accelerate your **Salesforce ROI**?", "Ready to modernize your **Oracle stack**?"

**`cta-sub`**
- 1–2 sentences of supporting copy. Describe what happens when they click (e.g., schedule a consultation, request an assessment, speak with an expert).
- Max ~100 characters per line. Keep it tight — this is not body copy.
- Example: "Our experts are ready to build a roadmap tailored to your business. Let's talk."

**Primary button (`.btn-cta-white`)**
- Action-oriented verb phrase followed by `&rarr;` (→ arrow entity).
- Links to `mailto:info@forsysinc.com` for the vast majority of pages.
- **Exceptions:**
  - `company/culture.html` → links to `careers.html`
  - `company/careers.html` → links to `mailto:info@forsysinc.com` (standard)
  - `company/news-press.html` → links to `mailto:info@forsysinc.com` (standard)

**Secondary button (`.btn-cta-outline`)**
- Default label: "View Customer Stories" — links to `../resources/customer-stories.html`.
- **Exceptions (label changes):**
  - `resources/customer-stories.html` → "About Forsys" (links to `../company/about.html`)
  - `company/culture.html` → "Learn About Forsys" (links to `about.html`)
  - `company/careers.html` → "Explore Our Culture" (links to `culture.html`)
  - `company/about.html` → "Meet the Team" (links to `leadership.html`)
  - `company/leadership.html` → stays "View Customer Stories" (standard)

### 8.13 Footer

Dark gradient bg (`var(--gradient-dark)`), `padding: 64px 48px 36px`.

- Grid: `1.8fr 1fr 1fr 1fr 1fr` — brand column wider than link columns.
- Brand column: logo + descriptor copy at `rgba(255,255,255,0.45)`, max-width 240px.
- Link columns: heading `11px/700 uppercase rgba(255,255,255,0.4)`, links `13.5px rgba(255,255,255,0.6)` → `#fff` on hover.
- Bottom bar: `border-top: 1px solid rgba(255,255,255,0.1)`, flex row with copyright, gradient-clipped tagline, and links.

### 8.14 Scroll-fade card entrance

Applied to all card grids on homepage and inner pages:

```js
const obs = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const i = Array.from(fadeEls).indexOf(entry.target) % 4;
      setTimeout(() => {
        entry.target.style.opacity = '1';
        entry.target.style.transform = 'translateY(0)';
      }, i * 70); // stagger by position in group of 4
      obs.unobserve(entry.target);
    }
  });
}, { threshold: 0.08 });

fadeEls.forEach(el => {
  el.style.opacity = '0';
  el.style.transform = 'translateY(18px)';
  el.style.transition = 'opacity 0.45s ease, transform 0.45s ease';
  obs.observe(el);
});
```

Start state: `opacity: 0; translateY(18px)`. End state: `opacity: 1; translateY(0)`. Duration: 450ms ease. Stagger: 70–80ms per card, cycling in groups of 4.

### 8.15 Section Surface System

Every content section falls into one of three surface types. All element styles below are dictated by which surface type the section uses. Following these rules consistently is what makes the site look polished and coherent everywhere.

#### Surface type overview

| Surface | Section bg | Card bg | When used |
|---|---|---|---|
| **White** | `var(--white)` `#FFFFFF` | `var(--bg)` `#F5F6FF` | Odd-numbered sections after hero (1st, 3rd, 5th…) |
| **Lavender** | `var(--bg)` `#F5F6FF` | `var(--white)` `#FFFFFF` | Even-numbered sections after hero (2nd, 4th, 6th…) |
| **Dark** | `var(--gradient-dark)` | `rgba(255,255,255,0.03)` | Footer and CTA inner card only — never for content sections |

> **Inversion rule:** The card surface always contrasts with its parent section surface. White section → lavender (`var(--bg)`) cards. Lavender section → white (`var(--white)`) cards. This creates visual depth on both alternating backgrounds without using drop shadows on every card.

---

#### Text elements on light surfaces (white and lavender sections)

| Element | CSS class | Font | Size | Weight | Color | Notes |
|---|---|---|---|---|---|---|
| **Section label** | `.section-label` | Inter | 11.5px | 600 | `var(--purple)` | Uppercase, 0.1em tracking, outlined pill border |
| **Section title** | `.section-title` | Space Grotesk | `clamp(32px, 3.8vw, 54px)` | 800 | `var(--text-primary)` | −0.03em letter-spacing, line-height 1.08 |
| **Gradient word** | `.section-title .gradient-text` | Space Grotesk | inherits title | 800 | AI gradient clip | Wrap 1–3 key words — never full title |
| **Section sub** | `.section-sub` | Inter | 17px | 400 | `var(--text-secondary)` | Max-width 560px, line-height 1.65 |
| **Section subheading** | `.section-subheading` | Space Grotesk | `clamp(20px, 2.4vw, 28px)` | 700 | `var(--text-primary)` | Introduces a card group below section-title |
| **Card title** | `.card-title` | Space Grotesk | 17px | 700 | `var(--text-primary)` | Line-height 1.3 |
| **Card body** | `.card-body` | Inter | 13.5px | 400 | `var(--text-secondary)` | Line-height 1.6 |
| **Card meta / caption** | `.card-meta` | Inter | 11.5px | 500 | `var(--text-muted)` | Never alone for body copy — only non-critical labels |
| **Card column label** | `.card-label` | Inter | 10.5px | 700 | `var(--text-muted)` | Uppercase, 0.07em tracking |
| **Stat number (large)** | `.stat-display` | Space Grotesk | 40px | 800 | AI gradient clip | Standalone outcomes, hero stats |
| **Stat number (small)** | `.stat-display-sm` | Space Grotesk | 28px | 800 | AI gradient clip | Supporting stats inside cards |
| **Stat label** | `.stat-label` | Inter | 11.5px | 500 | `var(--text-muted)` | Pairs with `.stat-display` or `.stat-number` |
| **Tag / badge** | `.tag.tag-purple` | Inter | 10.5px | 700 | `var(--purple)` | Uppercase, 0.06em tracking, pill radius |
| **Inline link** | `.content-link` | Inter | inherits | 600 | `var(--purple)` | Border-bottom appears on hover only |

---

#### Card elements by surface

**Cards on white sections** — class: `.card-on-white`

| State | Background | Border | Shadow | Transform |
|---|---|---|---|---|
| Rest | `var(--bg)` `#F5F6FF` | `1.5px solid var(--border)` | none | none |
| Hover | `var(--white)` `#FFFFFF` | `1.5px solid var(--purple)` | `0 8px 32px rgba(107,72,255,0.10)` | `translateY(-3px)` |

**Cards on lavender sections** — class: `.card-on-bg`

| State | Background | Border | Shadow | Transform |
|---|---|---|---|---|
| Rest | `var(--white)` `#FFFFFF` | `1.5px solid var(--border)` | none | none |
| Hover | `var(--white)` `#FFFFFF` | `1.5px solid var(--purple)` | `0 8px 32px rgba(107,72,255,0.10)` | `translateY(-3px)` |

> **Note:** `.card-on-white` and `.card-on-bg` are utility classes in `base.css`. Existing component classes (`.wwd-card`, `.sol-card`, `.ind-card`, `.split-card`, `.partner-card`) already implement this logic per their specific grids — use those for known components. Use `.card-on-white` / `.card-on-bg` only when adding a new card pattern not covered by an existing component class.

---

#### Icon badge specification

| Variant | CSS class | Size | Radius | Background | Border | SVG size | Padding each side | Fill ratio |
|---|---|---|---|---|---|---|---|---|
| **Standard** | `.icon-badge` | 52 × 52 px | 14px | `var(--purple-light)` | `1px solid rgba(107,72,255,0.15)` | 26 × 26 px | 13 px | 50% |
| **Large** | `.icon-badge.icon-badge--lg` | 64 × 64 px | 16px | `var(--purple-light)` | `1px solid rgba(107,72,255,0.15)` | 32 × 32 px | 16 px | 50% |
| **Inline list** | *(component-specific)* | 40 × 40 px | 10px | `rgba(107,72,255,0.08)` | `1px solid rgba(107,72,255,0.18)` | 20 × 20 px | 10 px | 50% |

> **Breathing room rule (50% fill):** SVG icons must fill exactly 50% of their container in each dimension — so the gap between the icon edge and the container border equals exactly 25% of the container size on each side. This "just right" ratio ensures the purple-light background is clearly visible as a badge without leaving the icon looking small or floating. Formula: SVG size = container size × 0.50, padding each side = (container − SVG) / 2.

SVG icons inside icon badges:
- `viewBox="0 0 24 24"`, `stroke="currentColor"`, `stroke-width="1.5"`, `fill="none"`, `aria-hidden="true"`.
- Color inherits `color: var(--purple)` from the `.icon-badge` parent — never set explicit stroke on the SVG.
- Always add `svg { width: 26px; height: 26px; flex-shrink: 0; }` (standard) or `svg { width: 32px; height: 32px; }` (large) or `svg { width: 20px; height: 20px; }` (inline list) next to each icon class definition so the SVG cannot overflow or float in the container.

---

#### Spacing within sections

| Gap | Value | Applied to |
|---|---|---|
| Section label → section title | `margin-bottom: 18px` on `.section-label` | All section headers |
| Section title → section sub | `margin-bottom: 14px` on `.section-title` | All section headers |
| Section header → card grid | `margin-bottom: 52px` on `.section-header` wrapper | All section headers |
| Card icon → card title | `gap: 16px` in card flex column | All icon+text cards |
| Card title → card body | `margin-bottom: 8px` on `.card-title` | All cards |
| Card internal padding | `24px` (standard), `32px` (feature / large cards) | Per card variant |
| Grid column gap | `24px` (3-col), `20px` (4-col) | Card grids |
| Grid row gap | `24px` standard, `28px` feature cards | Card grids |
| Section padding — desktop | `96px 48px` | All `<section>` elements |
| Section padding — mobile ≤768px | `64px 24px` | All `<section>` elements |

---

#### Gradient subheading usage rules

The `.gradient-text` class applies the AI gradient (`linear-gradient(90deg, #6B48FF 0%, #00B4D8 100%)`) as a background-clip to text. Rules:

1. **Allowed on:** `.section-title`, `.hero-headline`, `.cta-title`, `.section-subheading` — Space Grotesk display elements only.
2. **Never on:** Body copy, `.card-title`, `.card-body`, captions, labels, nav links, footer text.
3. **Scope:** 1–3 words maximum. The gradient loses impact on long strings.
4. **Pattern:** Wrap the key noun or action verb — e.g., `<span class="gradient-text">Revenue Operations</span>`, `<span class="gradient-text">AI Agents</span>`.
5. **Frequency:** One gradient-text span per section heading maximum. Repeated gradient spans on the same page create visual noise.
6. **Dark backgrounds:** Never use `.gradient-text` on dark sections — the purple→teal gradient disappears. Use plain `color: #fff` for emphasis instead.
7. **Mandatory coverage:** Every `<h2 class="section-title">` on every page MUST have at least one `.gradient-text` span on the meaningful keyword. This is non-negotiable for visual consistency. If a heading has no natural keyword, highlight the last noun. Example: "Our Core **Services**", "Proven **Results**", "The **Forsys** Difference".

---

## 9. SVG icon style

All icons follow these rules:

- **viewBox:** `0 0 24 24` standard.
- **Style:** stroke-based, never filled.
- **Stroke:** `currentColor`, `stroke-width: 1.5` (slightly lighter than the current site's 2–2.5), `stroke-linecap` / `stroke-linejoin` as needed, `fill: none`.
- **Sizes in context:**
  - In nav chevron (dropdown indicator): 12 px
  - In card icons (`.wwd-icon`, `.ind-icon`): 24 px (default viewBox size)
  - In split-card icons: 22 px
  - In button arrows: via HTML entities (`→`, `↗`) not SVG
- **Never use emojis as icons.**
- **Sources:** Heroicons / Lucide stroke library — must follow `stroke-width: 1.5` grammar used across this system.
- **Decorative icons:** always `aria-hidden="true"`.

---

## 10. Accessibility (non-negotiable)

### 10.1 Color contrast

- `--text-primary #0D0D2B` on `--white` ≥ 15:1. Always safe.
- `--text-secondary #4A4F6A` on `--white` ≈ 6:1. Safe for body.
- `--text-muted #8B90A7` on `--white` ≈ 3.6:1. **Fails** for body copy — use only for metadata/captions at large sizes (≥ 14px).
- White text on `--purple #6B48FF` ≈ 4.6:1. Passes AA for normal text.
- White text on dark gradient (`#0D0D2B`) ≥ 15:1. Safe.

### 10.2 Interactive elements

- **Touch target:** ≥ 44×44 px. Nav buttons, slide dots, tab buttons all meet this.
- **Focus-visible:** Render always. Use `outline: 2px solid var(--purple); outline-offset: 2px` — never `outline: none` without a replacement.
- **Semantic HTML:** `<button>` for actions (nav triggers, slide dots, platform tabs, accordion headers), `<a>` for navigation, `<nav>`, `<section>`, `<main>`, `<footer>` for structure.
- **ARIA tab pattern:** nav mega-menus use `role="menubar"` / `role="menu"` / `role="menuitem"` / `aria-haspopup` / `aria-expanded`. Platform tabs use `role="tablist"` / `role="tab"` / `role="tabpanel"` / `aria-selected` / `aria-controls`.
- **Live regions:** `.hero-headline` and `.hero-sub` use `aria-live="polite"` for the rotating slideshow.
- **Skip link:** `<a class="skip-link" href="#main">Skip to main content</a>` — absolute positioned, slides in on `:focus`.

### 10.3 Decorative vs meaningful

- All decorative SVGs, mockup cards, ticker strips, and glow orbs: `aria-hidden="true"`.
- Stats bar uses `role="list"` / `role="listitem"`.
- Testimonial star row gets `aria-label="5 stars"`.
- Trusted strip and ticker: `aria-hidden="true"` — decorative.
- Every content image gets descriptive `alt`; empty when decorative.

### 10.4 Motion and preferences

- Honor `prefers-reduced-motion: reduce` on all animations. The global rule in `base.css` sets all durations to `0.01ms` and disables the ticker.
- No autoplay content other than the hero slideshow (which is content-driven, not video).
- Entrance animations are scroll-triggered one-shots (unobserve after fire).

---

## 11. Code & naming conventions

### 11.1 Class naming

| Prefix | Used for |
|---|---|
| `hero-` | Hero section elements |
| `slide-` | Hero slideshow slides and dots |
| `wwd-` | "What We Do" section |
| `sol-` | Forsys AI Solutions cards |
| `split-` | Split (2-col) section and cards |
| `ind-` | Industries section and cards |
| `partner-` | Partnerships section and cards |
| `stat-` | Stats bar items |
| `mockup-` | Hero mockup UI cards |
| `ptab` | Platform tab buttons |
| `accord-` | Accordion list/item/header/body |
| `pv-` | Platform visual panel |
| `ticker-` | Ticker/logo strip |
| `test-` | Testimonial section |
| `cta-` | CTA strip section |
| `footer-` | Footer grid and elements |
| `nav-`, `mega-`, `dropdown` | Navigation |
| `btn-` | Buttons (all variants) |
| `tag`, `tag-purple/green/blue` | Status chips |
| `section-label`, `section-title`, `section-sub`, `section-header` | Shared section heading pattern |
| `gradient-text` | Gradient-clipped text span |
| `badge-dot` | Hero badge blinking dot |

**State classes:** `.active` (open accordion, active slide dot, active platform tab, active platform-content panel). `is-active` (stage nodes on inner pages).

### 11.2 File layout

```
forsys-new-2/
├── index.html
├── assets/
│   ├── css/
│   │   ├── base.css      ← tokens, resets, nav, footer, shared components
│   │   └── home.css      ← homepage-specific sections
│   └── js/
│       └── script.js     ← per-page IIFE guards
```

### 11.3 JavaScript pattern

Single `script.js` loaded by every HTML page. One global block (nav shadow), then page-guarded IIFEs:

```js
if (document.querySelector('.page-home')) {
  (function () {
    // hero slideshow, platform tabs, accordion, scroll-fade
  })();
}

if (document.querySelector('.page-services')) {
  (function () {
    // stage rail, card scroll-fade
  })();
}
```

Body tag carries the page class: `<body class="page-home">`, `<body class="page-services">`, etc.

---

## 12. Pre-delivery checklist

Before shipping any new page or component, verify:

- [ ] All CSS custom properties match token values in §1 — no ad-hoc hex codes.
- [ ] Only Space Grotesk (display) and Inter (body/UI) used. No other fonts.
- [ ] All radii are symmetric — no asymmetric corners; pill or `16–24px` only.
- [ ] Hover state provides visible cue: color + border + `translateY(-3px)` + shadow.
- [ ] Focus-visible ring renders: `2px solid var(--purple)` offset 2px.
- [ ] Color contrast ≥ 4.5:1 for body copy (never use `--text-muted` alone).
- [ ] Decorative SVGs have `aria-hidden="true"`; all meaningful images have `alt`.
- [ ] Semantic HTML: real `<button>` for actions, `<a>` for links, `<main>`, `<section>`, `<nav>`.
- [ ] ARIA roles on nav (menubar/menu/menuitem), tabs (tablist/tab/tabpanel), live regions.
- [ ] Skip link present and functional.
- [ ] `prefers-reduced-motion` honored for all animations > 150ms.
- [ ] Responsive tested at 1280, 1024, 768, 375 px widths.
- [ ] No console errors in browser dev tools.
- [ ] No emoji in rendered UI — SVG stroke icons only, entities (`→`, `·`) for decorative characters.
- [ ] Touch targets ≥ 44×44 px on all interactive elements.

---

## 13. Key differences from current site (MASTER.md)

This table documents the intentional divergences between the concept system and the existing production design system. Reference it when porting decisions between the two codebases.

| Dimension | Current site (MASTER.md) | Concept site (this file) |
|---|---|---|
| **Primary color** | `#0367FB` (blue) | `#6B48FF` (purple) |
| **Accent color** | `#F7941D` (orange) — CTA fill | None. Purple doubles as CTA fill. |
| **Display font** | Newsreader (serif), italic emphasis | Space Grotesk (sans-serif), no italic |
| **Body font** | Plus Jakarta Sans | Inter |
| **UI / label font** | Inter Tight | Inter (same family as body) |
| **Brand shape** | Asymmetric `0 X X X` (sharp top-left) | Fully symmetric. Pill or `16–24px`. |
| **Nav background** | Transparent on dark hero → white scrolled | Always frosted-glass lavender. No dark state. |
| **Logo treatment** | `.logo-dark` / `.logo-white` swap | Single logo mark (gradient "F" square). |
| **Section bg** | `#F4F6FB` surface | `#F5F6FF` bg (bluer tint) |
| **Dark bg** | `#0B1226 → #141E3C` | `#0D0D2B → #1E1B4B` (same family, slightly different stops) |
| **Hero type** | Newsreader display, `<em>` gradient | Space Grotesk, `.gradient-text` div |
| **FAQ / accordion** | Trigger-button + max-height animation | Simple `display: none → block` (no max-height) |
| **Stage rail** | 6-node tab rail with SVG connector line | Not present; replaced by platform-tabs + accordion |
| **Entrance animation** | Scroll-triggered SVG line draw | Scroll-triggered card fade-in with `translateY` stagger |
| **CTA fill** | Accent orange (`#F7941D`) | White on dark gradient card |
| **Focus ring color** | `--accent` orange | `--purple` `#6B48FF` |

---

## 14. Change log

| Date | Author | Change |
|---|---|---|
| 2026-04-22 | Forsys | Initial concept design system published, extracted from `forsys-website-concept.netlify.app` |
| 2026-04-23 | Forsys | Stat numbers bumped site-wide: `.stat-number` 30px→40px; section-level stat classes (`.svc-outcome-stat`, `.sol-result-stat`, `.fs-outcome-stat`, `.ind-stat-num`, `.par-why-stat-num`, `.co-stat-num`, etc.) increased ~30% proportionally. |
| 2026-04-23 | Forsys | Inner-page hero padding revised: top offset `+80px→+32px`; bottom `80px→160px` desktop / `48px→100px` mobile. Gives 80px breathing room between last CTA button and the `::after` wave. |
| 2026-04-23 | Forsys | Added §1.4 section background sequencing rule: sections after hero alternate white/`var(--bg)` strictly; CTA always dark. Applied to all 8 stylesheet categories. |
| 2026-04-23 | Forsys | Partnership ecosystem partner pages redesigned: overview panel now white bg with purple top-accent border; bullet list uses inline SVG checkmarks (no `::before` dot); `.par-value-title` 14.5px→17px; `.par-value-desc` 13px→14px; `.par-value-icon` SVG constrained to 20×20px. See §8.4. |
| 2026-04-23 | Forsys | Added §8.15 Section Surface System: comprehensive per-element style rules for white and lavender surfaces covering card inversion, typography hierarchy (`.card-title`, `.card-body`, `.card-meta`, `.card-label`), icon badge spec (`.icon-badge`, `.icon-badge--lg`), stat display variants (`.stat-display`, `.stat-display-sm`), spacing scale, and gradient-text usage rules. New utility classes added to `base.css`: `.card-on-white`, `.card-on-bg`, `.card-title`, `.card-body`, `.card-meta`, `.card-label`, `.section-subheading`, `.icon-badge`, `.icon-badge--lg`, `.stat-display`, `.stat-display-sm`, `.content-link`. |
| 2026-04-23 | Forsys | Icon badge breathing room: all icon containers increased to 52×52px (standard, 15px each side) and 64×64px (large, 19px each side) so the SVG never touches the container border. Explicit `svg { width: 22px; }` constraints added to all component icon classes across all 8 CSS files. Minimum padding rule (≥14px each side) codified in §8.15. |
| 2026-04-23 | Forsys | Icon SVG enlarged to 50% fill ratio for "just right" breathing room: standard containers (52px) → SVG 22→26px (13px each side); large containers (64px) → SVG 26→32px (16px each side); inline list containers (40px) → SVG 18→20px (10px each side). Updated across `base.css` and all 7 page-category CSS files. §8.15 icon spec table updated with fill-ratio column. |
| 2026-04-23 | Forsys | Gradient text enforcement: rule updated in §8.15 — every `<h2 class="section-title">` on every page MUST include a `.gradient-text` span on the meaningful keyword. Applied across all 54 pages. |
| 2026-04-23 | Forsys | Card background inversion fixes: `home.css` — `.ind-card` bg `var(--bg)`→`var(--white)` (on bg section), `.resource-card` bg `var(--white)`→`var(--bg)` (on white section), `.company-nav-card` bg `var(--bg)`→`var(--white)` (on bg section). `partnerships.css` — `.par-why-stat` bg `var(--white)`→`var(--bg)` (on white section). |
| 2026-04-23 | Forsys | Home page hero entrance animation added (`@keyframes heroFadeUp`) matching the inner-page staggered fade-up pattern. Elements and delays: `.hero-badge` 0.05s, `.hero-headline` 0.15s, `.hero-sub` 0.25s, `.slide-dots` 0.30s, `.hero-actions` 0.35s, `.hero-mockup` 0.50s. All use 0.6s `cubic-bezier(0.22, 0.61, 0.36, 1)` with `animation-fill-mode: both`. §6.1 motion table and §8.3 home hero spec updated. |
| 2026-04-23 | Forsys | Platform Solutions section (home page) redesigned for consistency and usability: (1) Tabs now use a pill-track container (`var(--bg)` bg, `1px var(--border)` border, `4px` padding); (2) Accordion items get left accent border (3px transparent → purple on active, `--border-strong` on hover); (3) Platform visual panel background changed to `var(--bg)` (section surface inversion), `pv-row` to `var(--white)`, `pv-row-val` to gradient-clipped Space Grotesk 16px/800; (4) Each platform panel gets a `.ptab-cta` link to its partnership page; (5) "Other" tab restructured from flat list into individual per-partner accordion items (RocketLane, Provus, M3ter, ServiceNow, Flosum); (6) Section header centered; (7) Inline ad-hoc hex `#16A34A` removed. §8.6 and §8.7 updated. |
| 2026-04-23 | Forsys | Platform Solutions section — animations: (1) Accordion open/close: `display:none/block` replaced globally (`base.css`) with `max-height: 0→280px` + `padding-bottom: 0→16px` transition (0.28s ease) for smooth slide-down/up on all pages. Toggle also allows closing an open item. (2) Tab sliding indicator: `<div class="ptab-slider">` added as absolute-positioned element inside `.platform-tabs`; JS (`script.js`) moves it via `left`/`width` inline styles on every tab click with `0.22s cubic-bezier(0.4, 0, 0.2, 1)` transition; init runs without transition (double-rAF) then adds `.tabs-js-ready` to strip static bg from `.ptab.active`. (3) Tab content fade-in: `@keyframes platformContentIn` (opacity+translateY 5px, 0.22s) on `.platforms .platform-content.active`. §6.1 motion table and §8.6 updated. |
| 2026-04-23 | Forsys | Technology partner pages "Partnership Highlights" card standardized: company text name replaced with `<img class="par-partner-logo">` SVG (36px height, max-width 160px) from `assets/images/`; stat rows updated to flex label/value layout (`.par-panel-stat-label` 11px uppercase muted + `.par-panel-stat-value` 13.5px/500 primary, right-aligned); `par-partner-logo-block` wrapper removed; `aria-label`/`role` attributes added to all 5 pages. CSS: `par-partner-logo-block`, `par-partner-logo-img`, `par-partner-name` replaced by `.par-partner-logo`; `par-partner-tagline` `text-align:center` removed. §8.4 updated. |
| 2026-04-23 | Forsys | Platform tab font fixed: `font-family: Inter, sans-serif` added explicitly to `.ptab` in `base.css`. `<button>` elements do not inherit `font-family` from `body` in most browsers — without this the tab labels rendered in the UA system font, inconsistent with the Inter accordion headers and CTA in the same section. §8.6 `.ptab` Font note added. |
| 2026-04-23 | Forsys | Strategic partnership pages "Solutions We Deliver" grid: enforced always-2-rows rule. Column count = numberOfCards ÷ 2. Salesforce (6 cards) → 3-col default; Conga (4 cards) → `par-solutions-grid--2col` added; Oracle (4 cards) → `par-solutions-grid--4col` replaced with `par-solutions-grid--2col`, inline `<style>` grid override removed from `<head>`. `.par-solutions-grid--2col { grid-template-columns: repeat(2, 1fr); }` added to `partnerships.css`. §8.4 updated. |

---

*This document is the source of truth for the concept redesign. When the code and this file disagree, update this file to match the code — then share the change.*
