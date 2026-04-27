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

### Dark Mode (Complete Override)

When dark mode is activated, apply via `[data-theme="dark"]` on `<html>`. Override the **full** token set — never partially swap colors:

```css
[data-theme="dark"] {
  /* Backgrounds */
  --bg-page: #1a1a2e;
  --bg-card: rgba(255, 255, 255, 0.06);
  --bg-card-hover: rgba(255, 255, 255, 0.10);
  --bg-sidebar: rgba(255, 255, 255, 0.04);

  /* Text */
  --text-primary: #e8e6e1;
  --text-secondary: #9a9890;
  --text-tertiary: #6b6960;

  /* Accent — same hue, boost lightness for dark bg contrast */
  --accent: #eab34d;
  --accent-light: rgba(232, 168, 56, 0.15);
  --accent-dark: #d49a2e;

  /* Borders & Shadows */
  --border-glass: 1px solid rgba(255, 255, 255, 0.08);
  --shadow-card: 0 4px 24px rgba(0, 0, 0, 0.25);
  --shadow-card-hover: 0 8px 32px rgba(0, 0, 0, 0.35);
}
```

Dark mode rules:
- Glass borders drop to `0.08` opacity — structure comes from shadow contrast, not edge lines.
- Shadows deepen (`0.25–0.35` opacity) since there's no ambient light to soften them.
- Background gradient blobs shift to deeper tones (indigo `#2d1b69`, deep teal `#0d3b4a`, muted plum `#3d1f3d`) at `0.2` opacity.
- Verify all text passes **4.5:1 contrast** against `#1a1a2e` — `#e8e6e1` on `#1a1a2e` = 11.3:1 ✓.
- Never invert the accent color hue — only adjust lightness.

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

### Form Controls
The missing fundamental in most design systems. Glass-styled inputs that feel native to the system.

```css
/* Base Input */
.input {
  background: var(--bg-card);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1.5px solid rgba(0, 0, 0, 0.08);
  border-radius: var(--radius-sm);
  padding: 12px var(--space-md);
  font-size: var(--font-base);
  font-family: inherit;
  color: var(--text-primary);
  width: 100%;
  transition: all 0.2s ease;
}
.input:focus {
  outline: none;
  border-color: var(--accent);
  box-shadow: 0 0 0 3px var(--accent-light);
}
.input::placeholder {
  color: var(--text-tertiary);
}

/* Validation States */
.input--error { border-color: var(--status-error); }
.input--error:focus { box-shadow: 0 0 0 3px rgba(217, 79, 79, 0.12); }
.input--success { border-color: var(--status-success); }

/* Floating Label */
.field { position: relative; }
.field .input { padding-top: 20px; padding-bottom: 8px; }
.field-label {
  position: absolute;
  left: var(--space-md);
  top: 50%;
  transform: translateY(-50%);
  font-size: var(--font-base);
  color: var(--text-tertiary);
  pointer-events: none;
  transition: all 0.2s ease;
}
.field .input:focus ~ .field-label,
.field .input:not(:placeholder-shown) ~ .field-label {
  top: 12px;
  transform: translateY(0);
  font-size: var(--font-xs);
  color: var(--accent);
}

/* Validation Message */
.field-message {
  font-size: var(--font-xs);
  margin-top: var(--space-xs);
  padding-left: var(--space-md);
}
.field-message--error { color: var(--status-error); }
.field-message--success { color: var(--status-success); }

/* Select */
.select {
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' viewBox='0 0 24 24' fill='none' stroke='%236b6b6b' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right var(--space-md) center;
  padding-right: 40px;
  cursor: pointer;
}

/* Textarea */
.textarea {
  min-height: 120px;
  resize: vertical;
  border-radius: var(--radius-md);
}

/* Checkbox & Radio (custom) */
.checkbox,
.radio {
  width: 20px;
  height: 20px;
  appearance: none;
  border: 1.5px solid var(--text-tertiary);
  background: var(--bg-card);
  cursor: pointer;
  transition: all 0.2s ease;
  flex-shrink: 0;
}
.checkbox { border-radius: 6px; }
.radio { border-radius: 50%; }
.checkbox:checked,
.radio:checked {
  background: var(--accent);
  border-color: var(--accent);
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='14' height='14' viewBox='0 0 24 24' fill='none' stroke='white' stroke-width='3' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='20 6 9 17 4 12'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: center;
}
.radio:checked {
  background-image: none;
  box-shadow: inset 0 0 0 3px white;
}
```

Form rules:
- Every `.input`, `.select`, and `.textarea` inherits the glass card aesthetic — same blur, same border style.
- Focus rings always use `--accent-light` as a soft glow — never browser-default outlines.
- Floating labels transition from placeholder position to above-input on focus — never use raw `<label>` above input without the float animation.
- Validation states change border color only — never change the entire input background to red/green.
- Touch targets: all form elements are at least `44px` tall.

### Modal / Dialog
Glass modal over a blurred backdrop. Used for confirmations, detail views, and focused forms.

```css
/* Backdrop */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.25);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  animation: fadeIn 0.2s ease;
}

/* Modal Panel */
.modal {
  background: var(--bg-card);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  border: var(--border-glass);
  border-radius: var(--radius-lg);
  box-shadow: 0 24px 80px rgba(0, 0, 0, 0.12);
  padding: var(--space-xl);
  max-width: 480px;
  width: 90%;
  max-height: 85vh;
  overflow-y: auto;
  animation: modalIn 0.3s cubic-bezier(0.22, 1, 0.36, 1);
}

/* Modal Header */
.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: var(--space-lg);
}
.modal-title {
  font-size: var(--font-lg);
  font-weight: 600;
  color: var(--text-primary);
}
.modal-close {
  width: 32px;
  height: 32px;
  border-radius: var(--radius-full);
  border: none;
  background: transparent;
  color: var(--text-secondary);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.2s ease;
}
.modal-close:hover {
  background: rgba(0, 0, 0, 0.06);
}

/* Animations */
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}
@keyframes modalIn {
  from { opacity: 0; transform: scale(0.95) translateY(8px); }
  to   { opacity: 1; transform: scale(1) translateY(0); }
}
```

Modal rules:
- Overlay blur is lighter than card blur (`6px` vs `16px`) — just enough to defocus the background.
- Modal entrance uses `scale(0.95)` + `translateY(8px)` — subtle, never dramatic zoom.
- Always include a visible close button AND close-on-overlay-click.
- Focus trap: keyboard focus must stay inside the modal while open.
- Max width `480px` for simple dialogs, `640px` for forms, `800px` for complex content.

### Toast / Notification
Lightweight feedback messages that appear and auto-dismiss.

```css
.toast-container {
  position: fixed;
  top: var(--space-lg);
  right: var(--space-lg);
  z-index: 1100;
  display: flex;
  flex-direction: column;
  gap: var(--space-sm);
}

.toast {
  background: var(--bg-card);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: var(--border-glass);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-card);
  padding: var(--space-md) var(--space-lg);
  display: flex;
  align-items: center;
  gap: var(--space-sm);
  min-width: 280px;
  max-width: 400px;
  animation: toastIn 0.35s cubic-bezier(0.22, 1, 0.36, 1);
}

/* Status variants — left accent border */
.toast--success { border-left: 3px solid var(--status-success); }
.toast--error   { border-left: 3px solid var(--status-error); }
.toast--warning { border-left: 3px solid var(--status-warning); }
.toast--info    { border-left: 3px solid var(--status-info); }

.toast-message {
  font-size: var(--font-sm);
  color: var(--text-primary);
  flex: 1;
}

.toast-dismiss {
  background: none;
  border: none;
  color: var(--text-tertiary);
  cursor: pointer;
  padding: var(--space-xs);
}

@keyframes toastIn {
  from { opacity: 0; transform: translateX(24px); }
  to   { opacity: 1; transform: translateX(0); }
}
```

Toast rules:
- Position: top-right on desktop, bottom-center on mobile.
- Auto-dismiss after `4–6 seconds` for success/info. Error toasts persist until dismissed.
- Status is indicated by a left accent border — never color the entire background.
- Stack vertically with `8px` gap. Maximum 3 visible toasts — oldest auto-dismisses.
- Exit animation: fade out + slide right over `200ms`.

### Data Table
Glass-styled tables for dashboards and admin panels. Minimal lines, maximum readability.

```css
.table-wrapper {
  background: var(--bg-card);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: var(--border-glass);
  border-radius: var(--radius-md);
  overflow: hidden;
}

.table {
  width: 100%;
  border-collapse: collapse;
}

.table th {
  text-align: left;
  padding: var(--space-md) var(--space-lg);
  font-size: var(--font-xs);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-tertiary);
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
}

.table td {
  padding: var(--space-md) var(--space-lg);
  font-size: var(--font-sm);
  color: var(--text-primary);
  border-bottom: 1px solid rgba(0, 0, 0, 0.03);
}

.table tr:last-child td {
  border-bottom: none;
}

.table tr:hover td {
  background: rgba(0, 0, 0, 0.02);
}

/* Sortable column indicator */
.table th[data-sortable] {
  cursor: pointer;
  user-select: none;
}
.table th[data-sortable]:hover {
  color: var(--text-primary);
}

/* Pagination */
.table-pagination {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--space-md) var(--space-lg);
  border-top: 1px solid rgba(0, 0, 0, 0.06);
  font-size: var(--font-xs);
  color: var(--text-secondary);
}
```

Table rules:
- Wrap the `<table>` in a glass card — never let table edges float bare.
- No vertical borders. Horizontal separators only, at `0.03–0.06` opacity.
- Header text: uppercase, letter-spaced, `--text-tertiary` — it's metadata, not content.
- Row hover: barely-there background shift (`0.02` opacity) — not a highlight color.
- On mobile: horizontally scroll the wrapper, or switch to a stacked card layout per row.

### Loading / Skeleton States
Shimmer placeholders that match the glass aesthetic. Never use spinners.

```css
.skeleton {
  background: linear-gradient(
    90deg,
    rgba(0, 0, 0, 0.04) 25%,
    rgba(0, 0, 0, 0.08) 50%,
    rgba(0, 0, 0, 0.04) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s ease infinite;
  border-radius: var(--radius-sm);
}

.skeleton--text {
  height: 16px;
  width: 80%;
  margin-bottom: var(--space-sm);
}
.skeleton--text-short {
  height: 12px;
  width: 40%;
}
.skeleton--circle {
  width: 48px;
  height: 48px;
  border-radius: 50%;
}
.skeleton--card {
  height: 160px;
  border-radius: var(--radius-md);
}

@keyframes shimmer {
  0%   { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

Loading rules:
- Skeleton shapes must match the real content they replace — same height, width, and border-radius.
- Shimmer gradient uses near-transparent blacks — never colored shimmer.
- Stagger skeleton entrance with the same `fadeUp` animation used for real cards.
- Never show a loading spinner. Spinners break the calm, minimal aesthetic.
- If loading takes > 3 seconds, add a subtle text hint below: "Loading..." in `--text-tertiary`.

### Empty & Error States
Blank screens are missed opportunities. Every empty or error state should guide the user forward.

```css
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: var(--space-3xl) var(--space-xl);
  text-align: center;
}
.empty-state-icon {
  width: 64px;
  height: 64px;
  color: var(--text-tertiary);
  margin-bottom: var(--space-lg);
  opacity: 0.5;
}
.empty-state-title {
  font-size: var(--font-lg);
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: var(--space-sm);
}
.empty-state-description {
  font-size: var(--font-sm);
  color: var(--text-secondary);
  max-width: 360px;
  margin-bottom: var(--space-lg);
}
/* Follow with a .btn-primary CTA */
```

Empty & error state rules:
- Always include: icon + title + description + CTA button.
- Icon uses stroke style, `64px`, at `0.5` opacity — present but not dramatic.
- Title is direct: "No projects yet" not "Oops! Nothing here!" — no fake enthusiasm.
- Description offers one clear next step: "Create your first project to get started."
- Error states swap the icon to a warning symbol and use `--status-error` for the title color only.
- Never leave a blank white area — it looks broken.

### Breadcrumbs
Lightweight wayfinding for multi-level navigation.

```css
.breadcrumbs {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
  font-size: var(--font-xs);
  color: var(--text-tertiary);
  margin-bottom: var(--space-lg);
}
.breadcrumbs a {
  color: var(--text-secondary);
  text-decoration: none;
  transition: color 0.2s ease;
}
.breadcrumbs a:hover {
  color: var(--accent);
}
.breadcrumbs-separator {
  font-size: 10px;
  opacity: 0.4;
}
.breadcrumbs-current {
  color: var(--text-primary);
  font-weight: 500;
}
```

- Separators use `/` or `›` at reduced opacity — never `>`.
- Current page is non-linked, `--text-primary`, `font-weight: 500`.
- Maximum 4 levels deep. If deeper, collapse middle levels to `...`.

### Top Navigation Bar
Alternative to the sidebar for simpler pages and marketing sites.

```css
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--bg-card);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-bottom: var(--border-glass);
  padding: var(--space-md) var(--space-xl);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.navbar-brand {
  font-size: var(--font-lg);
  font-weight: 700;
  color: var(--text-primary);
}

.navbar-links {
  display: flex;
  gap: var(--space-lg);
  list-style: none;
}
.navbar-links a {
  font-size: var(--font-sm);
  font-weight: 500;
  color: var(--text-secondary);
  text-decoration: none;
  transition: color 0.2s ease;
  position: relative;
}
.navbar-links a:hover,
.navbar-links a.active {
  color: var(--text-primary);
}
.navbar-links a.active::after {
  content: '';
  position: absolute;
  bottom: -6px;
  left: 0;
  right: 0;
  height: 2px;
  background: var(--accent);
  border-radius: 1px;
}

/* Mobile: collapse to hamburger */
@media (max-width: 639px) {
  .navbar-links { display: none; }
  .navbar-links.open {
    display: flex;
    flex-direction: column;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: var(--bg-card);
    backdrop-filter: blur(16px);
    padding: var(--space-md);
    border-bottom: var(--border-glass);
    box-shadow: var(--shadow-card);
  }
}
```

Navbar rules:
- Always sticky with glass blur — it floats as you scroll.
- Active link indicated by a `2px` accent underline — not background color change.
- Mobile: links collapse into a dropdown panel (glass background, same blur). Trigger with a hamburger icon.
- Never put more than 6 links in the navbar. If more, group into dropdowns.

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
- [ ] Form inputs have glass styling with accent focus rings
- [ ] Modals use backdrop blur overlay with focus trap
- [ ] Toast notifications use left-border status colors, not full-background color
- [ ] Data tables are wrapped in glass cards with minimal horizontal borders
- [ ] Loading states use skeleton shimmer — never spinners
- [ ] Empty states include icon + title + description + CTA
- [ ] Dark mode overrides all CSS variables (if applicable)
