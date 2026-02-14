---
name: clarity-ui
description: Build clean, minimalist, professional website UIs with light color palettes, glassmorphism, generous whitespace, and polished micro-interactions. Use this skill when the user asks to create web pages, dashboards, landing pages, admin panels, components, or any website interface that should look modern, airy, and refined.
---

This skill produces clean, light-themed, minimalist yet professional website UIs — inspired by modern smart-home dashboards and glassmorphic design language. Every output must be production-grade HTML/CSS/JS (or React/Vue/Svelte) that looks intentionally designed, never generic.

The user provides a website UI requirement: a page, dashboard, component, or full layout. They may include context about purpose, audience, or tech stack.

---

## Design Philosophy

**Core identity: Clean. Light. Minimal. Professional.**

Before writing any code, commit to these non-negotiable principles:

1. **Light comes from above** — Shadows fall downward. Top edges of cards/buttons catch light (slightly brighter). Bottom edges cast subtle shadows. This creates natural depth on flat screens.
2. **Grayscale first, color second** — Structure the layout in neutrals. Only then introduce 1–2 accent colors with clear purpose (status indicators, CTAs, active states). Never scatter color randomly.
3. **Double your whitespace** — When you think there's enough spacing, double it. Generous padding inside cards, between sections, and around text. Cramped UI is the enemy.
4. **Glassmorphism as signature** — Translucent card backgrounds (`background: rgba(255,255,255,0.6)`) with `backdrop-filter: blur(16px)`, soft rounded corners (`border-radius: 16px–24px`), and subtle `1px solid rgba(255,255,255,0.3)` borders. This is the defining visual layer.
5. **Restraint is elegance** — Every element must earn its place. If it doesn't serve the user, remove it.

---

## 7 UI Principles (Figma-Aligned)

Apply these on every build:

### 1. Hierarchy
- Use font size, weight, and color to create 3 clear levels: **primary** (large/bold headings), **secondary** (medium labels/values), **tertiary** (small metadata/captions).
- The most important information is the largest and highest-contrast element on screen.
- Example: On a dashboard, the time "09:00" is 48px bold; the date "17 July, 2023" is 14px regular.

### 2. Progressive Disclosure
- Show only what's needed at the current level. Details live behind clicks, hovers, or expansions.
- Use cards as containers that summarize at a glance but can expand for detail.
- Multi-step flows show a progress indicator so users know where they are.

### 3. Consistency
- Same component = same appearance everywhere. A card is always the same border-radius, shadow, padding.
- Use CSS custom properties (variables) for every repeated value. No magic numbers.
- Buttons, icons, and spacing follow a strict system.

### 4. Contrast (Strategic)
- Primary actions get the accent color. Secondary actions stay neutral/gray.
- Active/selected states use a filled accent chip (e.g., `12 watt` highlighted in amber). Inactive states are outlined or muted.
- Destructive actions get a distinct warning color (red/orange), never the accent color.

### 5. Accessibility
- Minimum 4.5:1 contrast ratio for all text.
- All interactive elements are keyboard-navigable with visible focus rings.
- Images and icons have `alt` text or `aria-label`.
- Touch targets are at least 44×44px.
- Never rely on color alone to convey information — pair with icons or text.

### 6. Proximity
- Related controls are grouped together inside a shared card or section.
- Unrelated elements have clear visual separation (whitespace or dividers).
- Example: "Swing" and "Auto" toggles sit together in the Thermostat card because they're both HVAC controls.

### 7. Alignment
- Use a consistent grid system (8px base unit recommended).
- All elements snap to the grid. No arbitrary offsets.
- Left-align text by default. Center-align only for hero sections or single-line labels inside cards.

---

## Color System

### Palette Philosophy
Light, warm, and muted. Never harsh. Never neon.

```css
:root {
  /* Backgrounds */
  --bg-page: #f0ece4;              /* Warm off-white / linen */
  --bg-card: rgba(255, 255, 255, 0.55); /* Frosted glass */
  --bg-card-hover: rgba(255, 255, 255, 0.75);
  --bg-sidebar: rgba(255, 255, 255, 0.4);

  /* Text */
  --text-primary: #1a1a1a;         /* Near-black, never pure #000 */
  --text-secondary: #6b6b6b;       /* Muted gray */
  --text-tertiary: #9a9a9a;        /* Lightest readable gray */

  /* Accent — Warm Amber/Gold */
  --accent: #e8a838;               /* Primary accent (amber/gold) */
  --accent-light: #fdf0d5;         /* Accent tint for backgrounds */
  --accent-dark: #c48820;          /* Accent shade for hover */

  /* Status */
  --status-success: #4caf7d;
  --status-warning: #e8a838;
  --status-error: #d94f4f;
  --status-info: #5b8def;

  /* Borders & Shadows */
  --border-glass: 1px solid rgba(255, 255, 255, 0.35);
  --shadow-card: 0 4px 24px rgba(0, 0, 0, 0.06);
  --shadow-card-hover: 0 8px 32px rgba(0, 0, 0, 0.1);

  /* Radius */
  --radius-sm: 12px;
  --radius-md: 16px;
  --radius-lg: 24px;
  --radius-full: 9999px;

  /* Spacing (8px base) */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  --space-2xl: 48px;
  --space-3xl: 64px;
}
```

### Rules
- **Background**: Always a soft, warm off-white or muted pastel — never stark `#fff`.
- **Cards**: Frosted glass with blur. White at 50–70% opacity. Subtle white border.
- **Accent usage**: Sparingly. Used for active states, CTAs, progress rings, and important indicators. Max ~10% of screen area.
- **Gradients**: Allowed only as page backgrounds (soft multi-color blobs/mesh gradients behind the glass layer). Never on buttons or cards.
- **Dark mode**: If requested, invert to `--bg-page: #1a1a2e` with glass cards at `rgba(255,255,255,0.08)`. Keep the same accent color.

---

## Typography

### Font Strategy
Clean, modern, geometric sans-serifs. Never decorative or serif for body text.

**Recommended pairings** (pick one pair per project, do NOT reuse across projects):

| Headings | Body | Vibe |
|---|---|---|
| `Outfit` | `DM Mono` | Tech-forward, dashboard |
| `Work Sans` | `Instrument Sans` | Warm professional |
| `Bricolage Grotesque` | `Jura` | Modern editorial |
| `Smooch Sans` | `Crimson Pro` | Elegant, luxury |
| `Red Hat Mono` | `Libre Baskerville` | Data-rich, analytical |

### Scale (8px rhythm)
```
--font-xs:   12px / 16px    /* Captions, metadata */
--font-sm:   14px / 20px    /* Secondary labels */
--font-base: 16px / 24px    /* Body text */
--font-lg:   20px / 28px    /* Section headers */
--font-xl:   28px / 36px    /* Page titles */
--font-2xl:  40px / 48px    /* Hero numbers / big stats */
--font-3xl:  56px / 64px    /* Dashboard clock / hero */
```

### Rules
- Headings: `font-weight: 600–700`. Body: `font-weight: 400`.
- Letter-spacing: slightly tighten headings (`-0.02em`), slightly loosen small caps/labels (`0.05em`).
- Never use more than 2 font families per page.
- Load fonts via Google Fonts `<link>` — always include `display=swap`.

---

## Component Patterns

### Glass Card
The fundamental building block:
```css
.card {
  background: var(--bg-card);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: var(--border-glass);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-card);
  padding: var(--space-lg);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.card:hover {
  background: var(--bg-card-hover);
  box-shadow: var(--shadow-card-hover);
  transform: translateY(-2px);
}
```

### Sidebar Navigation
- Vertical icon-only sidebar (left edge), frosted glass background.
- Active icon gets a filled circle indicator or accent-colored background pill.
- Icons use `stroke` style (not filled) for inactive, filled for active.
- Tooltips on hover showing the label.

### Stat/Metric Display
- Large number (font-2xl or 3xl, bold, primary color).
- Small label below or above (font-xs, uppercase, letter-spaced, secondary color).
- Optional circular progress ring (SVG `<circle>` with `stroke-dasharray`) for percentages.

### Buttons
```css
.btn-primary {
  background: var(--accent);
  color: white;
  border: none;
  border-radius: var(--radius-full);
  padding: 10px 24px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
}
.btn-primary:hover {
  background: var(--accent-dark);
  box-shadow: 0 4px 12px rgba(232, 168, 56, 0.3);
}
.btn-secondary {
  background: transparent;
  color: var(--text-primary);
  border: 1.5px solid var(--text-tertiary);
  border-radius: var(--radius-full);
  padding: 10px 24px;
}
```

### Tab Bar / Room Selector
- Horizontal pill-shaped tabs at the bottom or top.
- Active tab: filled with white background, subtle shadow, bold text.
- Inactive tabs: transparent, regular weight, secondary text color.
- Include a `+` icon button at the end for adding items.

### Toggle / Switch
- Rounded track (`height: 24px; border-radius: 12px`).
- ON state: accent-colored track with white circle thumb.
- OFF state: light gray track with white circle thumb.
- Smooth `0.3s` transition on toggle.

### Charts & Data Viz
- Use simple bar charts with rounded tops (`border-radius: 4px 4px 0 0`).
- Bars use muted colors; the highlighted/current period gets the accent color.
- Axis labels in `font-xs`, `text-tertiary`.
- No unnecessary gridlines — one horizontal baseline at most.

### Circular Progress / Gauge
- Use SVG circles with `stroke-dasharray` and `stroke-dashoffset`.
- Ring thickness: `6–10px`. Background ring: light gray. Active ring: accent color with `stroke-linecap: round`.
- Center the percentage value in `font-xl`, bold.

---

## Layout Rules

### Page Structure
```
┌──────────────────────────────────────────────┐
│  [Sidebar]  │         Main Content           │
│   (icons)   │  ┌─────┐ ┌─────┐ ┌─────────┐  │
│             │  │Card │ │Card │ │  Card   │  │
│             │  └─────┘ └─────┘ └─────────┘  │
│             │  ┌───────────┐ ┌───────────┐  │
│             │  │   Card    │ │   Card    │  │
│             │  └───────────┘ └───────────┘  │
│             │        [Tab Bar]              │
└──────────────────────────────────────────────┘
```

- Use CSS Grid for main layout (`grid-template-columns: 64px 1fr`).
- Cards grid: `auto-fill` with `minmax(280px, 1fr)` or explicit column spans for larger cards.
- Gap between cards: `var(--space-lg)` (24px).
- Page padding: `var(--space-2xl)` (48px) on desktop, `var(--space-md)` on mobile.

### Responsive Breakpoints
```css
/* Mobile first */
@media (min-width: 640px)  { /* sm: 2-column card grid */ }
@media (min-width: 1024px) { /* lg: sidebar visible, 3-column grid */ }
@media (min-width: 1440px) { /* xl: wider cards, more breathing room */ }
```

- Sidebar collapses to bottom tab bar on mobile.
- Cards stack to single column on mobile.
- Font sizes scale down ~15% on mobile.

---

## Animation & Micro-Interactions

### Principles
- **Purposeful only** — every animation communicates something (state change, feedback, spatial relationship).
- **Fast and smooth** — durations between `150ms–400ms`. Use `cubic-bezier(0.4, 0, 0.2, 1)` (Material ease) or `cubic-bezier(0.22, 1, 0.36, 1)` (smooth decel).
- **CSS-first** — use CSS transitions and `@keyframes`. Only reach for JS animation libraries for complex orchestration.

### Standard Animations
```css
/* Card entrance — staggered fade-up */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}
.card {
  animation: fadeUp 0.5s cubic-bezier(0.22, 1, 0.36, 1) both;
}
.card:nth-child(1) { animation-delay: 0.05s; }
.card:nth-child(2) { animation-delay: 0.10s; }
.card:nth-child(3) { animation-delay: 0.15s; }
/* ... stagger by 50ms increments */

/* Hover lift */
.card:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-card-hover);
}

/* Button press */
.btn:active {
  transform: scale(0.97);
}

/* Toggle slide */
.toggle-thumb {
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

/* Progress ring fill */
.progress-ring__circle {
  transition: stroke-dashoffset 0.8s cubic-bezier(0.22, 1, 0.36, 1);
}
```

### What NOT to animate
- No bouncing, wobbling, or elastic effects.
- No parallax scrolling.
- No animations longer than 600ms.
- No animation on page-critical content that blocks readability.

---

## Background Treatment

The page background creates atmosphere behind the glass cards:

```css
body {
  background: var(--bg-page);
  position: relative;
  overflow-x: hidden;
}

/* Soft gradient blobs behind everything */
body::before,
body::after {
  content: '';
  position: fixed;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.35;
  z-index: -1;
}
body::before {
  width: 500px; height: 500px;
  background: linear-gradient(135deg, #c8b6ff, #ffc8dd);
  top: -100px; right: -100px;
}
body::after {
  width: 400px; height: 400px;
  background: linear-gradient(135deg, #bde0fe, #a2d2ff);
  bottom: -80px; left: -80px;
}
```

- Blobs should be **very soft** (high blur, low opacity). They add warmth without competing with content.
- Vary blob colors per project — pastels only (lavender, mint, peach, sky blue).
- Never make blobs sharp or saturated.

---

## Icon Guidelines

- Use **stroke-style** icon sets: Lucide, Phosphor (light), Heroicons (outline), or Tabler Icons.
- Consistent size: 20–24px for UI icons, 16px for inline/small.
- Stroke width: 1.5–2px.
- Color: `var(--text-secondary)` default, `var(--accent)` for active.
- Never mix icon sets within a project.

---

## NEVER Do These

| Violation | Why |
|---|---|
| Pure white `#ffffff` background | Too harsh. Use warm off-whites like `#f0ece4` or `#f5f3ef` |
| Heavy drop shadows | Breaks the soft, airy feel. Keep shadows at `0.06–0.1` opacity |
| More than 2 accent colors | Creates visual chaos. One accent + neutrals |
| Filled/solid icon style | Too heavy for minimalist aesthetic. Use outline/stroke icons |
| Sharp corners (`border-radius: 0–4px`) | Feels rigid. Minimum `12px` radius on cards |
| Dense, tight spacing | Defeats minimalism. Double your whitespace, always |
| Decorative fonts or serif headings | Conflicts with clean/modern identity |
| Busy patterns or textures | Noise competes with glass effect. Keep backgrounds clean |
| Generic AI palette (purple gradient + white) | Cliché. Use warm neutrals with amber/gold accent |
| Auto-playing or looping animations | Distracting. Animations are triggered, not ambient |

---

## Output Checklist

Before delivering any UI code, verify:

- [ ] Glass card effect is present with `backdrop-filter: blur`
- [ ] Color palette uses warm off-whites, not stark white
- [ ] Maximum 2 font families loaded
- [ ] All spacing follows 8px grid
- [ ] Accent color used sparingly (~10% of visual area)
- [ ] Cards have hover states with subtle lift + shadow
- [ ] Page has soft gradient blob background
- [ ] Responsive: works at 375px, 768px, 1440px
- [ ] Contrast ratios pass WCAG AA (4.5:1 minimum)
- [ ] Animations are under 500ms, CSS-only, purposeful
- [ ] No pure black (`#000`) or pure white (`#fff`) used anywhere
- [ ] Icons are consistent in style, size, and stroke weight