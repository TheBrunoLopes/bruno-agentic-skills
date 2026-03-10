---
name: cyberpunk-frontend-design-skill
description: Cyberpunk UI design system for building dark-themed, terminal-inspired interfaces. Use this skill whenever the user asks to build any frontend UI — pages, dashboards, components, forms, apps, landing pages, widgets, or any visual interface. Always apply this design system's aesthetic unless the user explicitly requests a different style. Triggers on any mention of UI, frontend, web page, dashboard, component, form, layout, app shell, or design work. Even partial UI tasks like "add a table" or "style this form" should use this system.
---

# Cyberpunk Design System

Apply this design system to ALL frontend/UI work. These are strong defaults — you may extend creatively but never contradict the core tokens or aesthetic.

## Technology Stack

When bootstrapping a new project or adding to an existing one, use this stack:

- **React + TypeScript** with **Vite** as the build tool and dev server
- **Tailwind CSS** via Vite's official integration (`@tailwindcss/vite`)
- **zustand** for client state management — lightweight, no boilerplate
- **@tanstack/react-query** for all server/async state — fetching, caching, mutations, loading and error states
- **lucide-react** for icons
- **motion** (formerly Framer Motion) for animations

Use `fetch` (or `ky` if already installed) for HTTP requests inside query/mutation functions — never raw `useEffect` + `fetch` patterns.

Follow Vite's conventions and project structure. Use `npm create vite@latest` with the `react-ts` template as the baseline. Install Tailwind via its Vite plugin (`@tailwindcss/vite`) — **not PostCSS**.

When adding UI to an existing project, adapt to whatever stack is already in place rather than re-scaffolding.

## CSS Architecture

The design system has **two CSS layers** that coexist:

1. **Custom CSS classes** (`.cyber-btn`, `.cyber-card`, `.cyber-input`, etc.) — the design system components. These use `var()` references to `:root` tokens. Copy them from the component and pattern reference files.
2. **Tailwind utilities** (`flex`, `gap-4`, `text-cyan`, `bg-pink`, etc.) — for layout, spacing, and quick one-off styling. These are powered by the `@theme` bridge below.

### CSS file setup (`app.css` or `index.css`)

```css
@import "tailwindcss";
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;700&family=Noto+Sans+JP:wght@700;900&display=swap');

/* ── Bridge tokens into Tailwind so utilities work ── */
@theme {
  --color-cyan:    #00f0ff;
  --color-pink:    #ff003c;
  --color-yellow:  #fcee0a;
  --color-green:   #39ff14;

  --color-bg-deep:     #05050a;
  --color-bg-surface:  rgba(10, 10, 15, 0.8);
  --color-bg-panel:    #0a0a0f;

  --color-text-primary:   #ffffff;
  --color-text-secondary: rgba(255, 255, 255, 0.8);
  --color-text-muted:     rgba(255, 255, 255, 0.55);

  --color-border-subtle:  rgba(255, 255, 255, 0.08);
  --color-border-medium:  rgba(255, 255, 255, 0.15);

  --font-pixel: 'Press Start 2P', cursive;
  --font-body:  'Inter', sans-serif;
  --font-mono:  'JetBrains Mono', monospace;
}

/* ── Full design system tokens (source of truth — from tokens.md) ── */
:root {
  /* ...paste full :root block from references/tokens.md... */
}

/* ── Shared @keyframes (from tokens.md) ── */
/* ...paste @keyframes from references/tokens.md... */

/* ── Component CSS (from components-core.md + components-extended.md) ── */
/* ...paste .cyber-btn, .cyber-card, .cyber-input, etc... */

/* ── Pattern CSS (from patterns-layout.md + patterns-effects.md) ── */
/* ...paste .section-header, .ds-nav, .cyber-timeline, etc... */
```

### When to use which

- **`.cyber-*` classes** for design system components (buttons, cards, forms, tables, alerts, badges, tabs, modals, toasts, progress bars, etc.)
- **Layout classes** (`.quiet-card`, `.panel-header`, `.stat-row`, `.stat-cell`, `.stat-label`, `.stat-value`, `.kv-label`, `.kv-value`) for recurring structural patterns — see `patterns-layout.md`
- **Tailwind utilities** for layout (`flex`, `grid`, `gap-*`), spacing (`p-*`, `m-*`), and one-off styles where creating a custom class isn't worth it
- **Inline `style` attributes** only for one-off structural adjustments (max-width, unique padding, color overrides). Never for recurring patterns — if you write the same inline block twice, make it a class

The `@theme` block is a slim bridge — it maps key tokens into Tailwind's namespace so utilities like `text-cyan`, `bg-bg-deep`, `font-mono` work. The `:root` block is the full source of truth for all component CSS.

## Aesthetic Direction

Dark, terminal-inspired cyberpunk. Think sci-fi command interfaces, not gaming neon. The tone is **technical and precise** — clean grids, monospaced data, subtle glows. Restraint over spectacle.

Key principles:
- **Dark-first**: Near-black backgrounds, no light themes
- **Cyan as primary accent**: Used for focus, active states, links, primary actions
- **Pink for danger/decoration**: Errors, destructive actions, corner accents
- **Yellow for warnings/highlights**: Caution states, active status
- **Green for success**: Confirmation, healthy states, positive metrics
- **Loud vs Quiet hierarchy**: Every page should have **one loud focal element** — the main content the user came to see (a data table, a primary card, or the sole form on a page). That element gets `.cyber-card` with cyan border, glow, and pink corners. Everything else — supporting panels, secondary cards, metadata sections — uses quiet styling (inline styles, subtle borders). When a page has many panels, only the most important one is loud. Sidebar, topbar, and structural layout are always quiet

## Design Thinking — Before You Code

Before writing any code, pause and understand what you're building:

1. **Purpose**: What is this interface for? Data monitoring, content management, configuration, onboarding? The answer shapes which components to reach for.
2. **Information density**: Is this data-heavy (dashboards, tables, stats) or task-focused (forms, wizards)? Data-heavy pages use more loud cards and stat rows. Task-focused pages use quieter layouts with clear form hierarchy.
3. **User attention**: What's the single most important thing on the page? That element gets the loudest treatment (cyan glow, corner decorations, largest type). Everything else supports it.
4. **Hierarchy plan**: Pick the **one element** per page that deserves the spotlight — typically a data table or the main content card — and make it loud (`.cyber-card`). Supporting panels, metadata cards, stat rows, and ancillary content stay quiet. On a dashboard with a single table, the table is loud. On a detail page with many panels, the header card is loud and the rest are quiet. A page with too many glowing panels looks as bad as one with none.

This system is opinionated but flexible — the aesthetic is fixed, but how you compose components should respond to the specific problem.

## Core Tokens

All tokens are defined as CSS custom properties in `references/tokens.md`. Copy the full `:root` block from that file into your stylesheet — every component and pattern references these via `var()`.

**Key variable groups**: `--bg-*` (backgrounds), `--cyan`/`--pink`/`--yellow`/`--green` (accents + opacity scales at 03–40), `--text-*` (hierarchy), `--border-*` (structural), `--font-*` (4 families), `--text-display` through `--text-nano` (type scale), `--tracking-*` (letter-spacing), `--space-*` (spacing), `--transition-*`, `--shadow-*`, `--z-*`.

Shared `@keyframes` animations (`spin`, `pulse`, `blink`, `skeletonShimmer`, `crtFlicker`, `glitchTop`, `glitchBottom`, `gridScroll`) are also in tokens.md.

### Key Patterns

**Labels**: JetBrains Mono, uppercase, letter-spacing `var(--tracking-wide)` to `var(--tracking-wider)`, muted color
**Hover states**: Always include transition (0.15–0.2s ease). Pattern: cyan bg tint + border hint + text color shift to #00f0ff
**Focus states**: Cyan border + box-shadow glow `0 0 10px rgba(0,240,255,0.2)`
**Corner decorations** (loud cards only): `::before` top-left pink, `::after` bottom-right pink, 20px × 20px

### Typography — Readable and Dense

This system is dense and terminal-inspired, but **readability comes first**. The working type scale is deliberately bumped up from ultra-small pixel aesthetics to ensure comfortable reading.

**Working range** (95% of your UI):
- **Page titles**: Press Start 2P at `clamp(0.8rem, 1.5vw, 1.1rem)`
- **Section headers**: Press Start 2P at `0.85–0.9rem`
- **Body text / inputs**: `var(--text-body)` (0.9rem) — Inter for prose, JetBrains Mono for data
- **Table cells / code**: `var(--text-sm)` (0.8rem) JetBrains Mono
- **Labels / table headers**: `var(--text-xs)` (0.75rem) uppercase JetBrains Mono
- **Badges / metadata**: `var(--text-label)` (0.7rem) JetBrains Mono
- **Nav items / micro text**: `var(--text-micro)` (0.65rem) / `var(--text-nano)` (0.6rem)

**Display range** (rare — hero sections, landing pages, large stat values):
- `--text-display` (2.2rem) — standalone hero/landing page titles only
- `--text-stat` (1.4rem) — large dashboard stat values (JetBrains Mono bold)

**Font roles**:
- **JetBrains Mono** is the dominant UI font — buttons, labels, inputs, tables, badges, nav, stats, all technical chrome. **Important**: the global `body` is set to Inter, so you must explicitly set `font-family: var(--font-mono)` on every technical element — nothing inherits Mono automatically
- **Inter** is for readable prose only — body paragraphs, descriptions, dialog messages, helper text
- **Press Start 2P** is for display titles only — page headings, section headers, brand. Always small (never above 1.1rem in app UI, exception: decorative glitch text on landing pages). Always uppercase.

**Letter-spacing tiers** (always paired with uppercase JetBrains Mono):
- `var(--tracking-normal)` (0.1em) — table headers, tabs, alert titles
- `var(--tracking-wide)` (0.12em) — stat labels, KV keys, metadata
- `var(--tracking-wider)` (0.15em) — buttons, form labels, nav items
- `var(--tracking-widest)` (0.2em) — nav section/group labels

## Component Quick Reference

Read `references/components-core.md` and `references/components-extended.md` for full specs. Key classes:

| Component | Class | Notes |
|-----------|-------|-------|
| Card (loud) | `.cyber-card` | Cyan border, glow, pink corner decorations via `::before`/`::after`. Use for **the main focal element** of each page — the primary table, hero card, or sole form |
| Card (quiet) | `.quiet-card` | Supporting/secondary panels, metadata, multi-panel layouts. Subtle border, dim surface bg, no glow |
| Button | `.cyber-btn` | Color: `.cyan` `.pink` `.yellow` `.green`. Size: `.sm`. Also `.icon-btn` for icon-only |
| Input | `.cyber-input` | Cyan-tinted bg, `.error` for red border. Pair with `.cyber-label` |
| Textarea | `.cyber-textarea` | Same as input, `min-height: 100px` |
| Select | `.cyber-select` | Custom chevron, same bg tint |
| Table | `.cyber-table` | Cyan header border, row hover, corner decorations, `.pagination-btn` |
| Alert | `.cyber-alert` | Variants: `.info` `.warning` `.error` `.success` |
| Badge | `.cyber-badge` | Outline: `.cyan` `.pink` `.yellow` `.green`. Filled: `.filled-cyan` etc. (solid bg, dark text) |
| Code | `.cyber-code` | `data-lang` attribute, syntax classes: `.comment` `.keyword` `.string` `.function` `.variable` |
| Tabs | `.cyber-tabs` > `.cyber-tab` | Bottom border active state, hover animation |
| Modal | `.cyber-modal` | Centered, backdrop blur, `.cyber-modal-backdrop` overlay |
| Toast | `.cyber-toast` | Variants: `.toast-success` `.toast-error` `.toast-warning` `.toast-info` |
| Tooltip | `.cyber-tooltip-wrap` | Dark bg, cyan accent bar, `.bottom` variant |
| Progress | `.cyber-progress` | `.fill` with `.cyan`/`.pink`/`.yellow`/`.green` |
| Spinner | `.cyber-spinner` | Cyan default, `.pink`/`.green` variants |
| Avatar | `.cyber-avatar` | Text-initials, sizes `.xs`–`.xl`, colors `.pink`/`.yellow`/`.green` |
| Timeline | `.cyber-timeline` | Vertical line with dot markers via `::before` |
| Toggle | `.cyber-toggle` | Custom switch with cyan active |
| Checkbox | `.cyber-checkbox` | Custom check with accent colors |
| Context menu | `.context-menu` | `.context-menu-item`, `.context-menu-divider`, `.danger` variant |
| Skeleton | `.skeleton` | `.skeleton-text` (`.sm`/`.md`/`.lg`), `.skeleton-heading`, `.skeleton-avatar`, `.skeleton-btn` |

## Layout Quick Reference

Read `references/patterns-layout.md` for full specs.

- **App shell**: Sidebar (260px) + top bar (56px height) + content area
- **Sidebar nav items**: `border-left` active indicator, cyan highlight
- **Top bar**: Brand left, search + actions right, `border-bottom` separator
- **Stat rows**: `.stat-row` > `.stat-cell` > `.stat-label` + `.stat-value`. 4-column grid, accent-colored values
- **KV panels**: `.quiet-card` > `.kv-label` + `.kv-value`. Stacked pairs, typically supporting role
- **Panel headers**: `.panel-header` > `.panel-header-title`. Title bar with bottom divider
- **Breadcrumbs**: JBM, slash-separated, current item in cyan

## Motion & Animation

Every interactive element needs a transition. But also think about larger motion patterns:

- **Transitions on all interactive elements**: `0.15–0.2s ease` for nav/tabs, `0.2s ease` for inputs, `0.3s ease` for buttons. Never ship a hover/focus state without a transition.
- **Page-load reveals**: Use staggered `animation-delay` for cards and sections appearing on load. A `fade-in` with `translateY(10px)` at 0.05s intervals creates a satisfying cascade.
- **Scroll-triggered entrances**: For long pages, trigger `fade-in` animations as sections enter the viewport. Use `IntersectionObserver` — not scroll event listeners.
- **Skeleton loading**: Show `.skeleton` placeholders before data arrives. The shimmer animation (1.5s infinite) signals "loading" without spinners.
- **Micro-interactions**: Progress bar glow pulses, spinner rotations, toast slide-ins. Keep these CSS-only when possible.
- **Atmospheric effects (optional)**: CRT scanline overlays, glitch text animations, typing cursor effects. Use sparingly — these are decoration, not function. Never apply glitch effects to text the user needs to read.

**Principle**: One well-orchestrated page load with staggered reveals creates more impact than scattered micro-interactions everywhere.

## Atmosphere & Depth

This system creates depth through layered transparency and environmental details — not drop shadows or gradients:

- **Background layers**: Page bg (`#05050a`) → subtle card surface (`rgba(10,10,15,0.4–0.8)`) → input fields (`rgba(0,240,255,0.03)`). Each layer is slightly more visible.
- **Backdrop blur**: `backdrop-filter: blur(5px)` on cards and modals creates glass-over-dark depth.
- **Japanese decorative text**: Noto Sans JP at 4–15% opacity, large sizes, vertical `writing-mode`. Creates atmosphere in margins/backgrounds without competing with content.
- **Glow as depth cue**: Cyan `box-shadow` on loud cards makes them feel "closer". Quiet cards with no glow recede. This is the primary depth mechanism.
- **Border as structure**: Subtle borders (`rgba(255,255,255,0.06–0.08)`) create panel edges. They define space without being visually heavy.
- **Corner decorations**: The `::before`/`::after` pink corner marks on loud cards create a "targeting reticle" effect — use on focal elements only.

## Code Practices

This system's tokens and classes exist so that every page looks consistent without duplicating code. Follow these rules:

- **Always use tokens via `var()`** — never hardcode a value that has a token equivalent. Use `var(--text-sm)` not `0.8rem`, `var(--tracking-wide)` not `0.12em`, `var(--space-6)` not `24px`. If a value doesn't match any token, that's fine — hardcode it. But if a token exists, use it
- **Use CSS classes for repeated patterns** — the system provides classes for common patterns: `.quiet-card`, `.panel-header`, `.stat-cell`, `.stat-label`, `.stat-value`, `.kv-label`, `.kv-value` (see `patterns-layout.md`). Use them instead of writing inline styles for the same structure repeatedly
- **Create new CSS classes** when you find yourself writing the same inline style block on 2+ elements. Add them to the project's stylesheet alongside the design system classes. A dashboard with 8 KV pairs should not have 8 identical inline style blocks
- **Inline styles are for one-offs only** — a unique layout tweak, a responsive override, a position adjustment. Not for defining font-family, font-size, color, or letter-spacing that a class or token should handle
- **Use `var(--space-*)` for spacing** — `var(--space-2)` not `8px`, `var(--space-6)` not `24px`. The spacing scale: 4/8/12/16/20/24/32/48/80px. Values outside the scale (10px, 6px, 14px) can be hardcoded

## Production Quality

The code you generate must work, not just look right:

- **Functional interactivity**: Buttons should have click handlers (even if placeholder). Forms should have labels wired to inputs. Tabs should switch. Modals should open/close.
- **Semantic HTML**: Use `<nav>`, `<main>`, `<section>`, `<button>`, `<label>`. Don't `<div>` everything.
- **Responsive awareness**: Use `clamp()` for headings — e.g., `clamp(0.8rem, 1.5vw, 1.1rem)` for page titles in Press Start 2P. Flex-wrap for card grids. The sidebar should collapse on narrow viewports.
- **CSS variables**: Define tokens as custom properties at `:root` level. Reference them throughout. This makes the system maintainable.
- **No dead code**: Every class, every rule should be used. Don't generate styles "just in case".
- **Accessible contrasts**: The color palette is designed for dark backgrounds — text at `rgba(255,255,255,0.55)` on `#05050a` passes AA contrast. Don't drop text opacity below 0.45.

## Dos and Don'ts

**DO:**
- Use JetBrains Mono for anything technical (data, labels, buttons, forms, code, stats)
- Use Inter for readable body text and descriptions
- Use Press Start 2P sparingly for titles and section headers
- Include hover/focus transitions on all interactive elements
- Use the loud/quiet card hierarchy intentionally
- Keep backgrounds dark — layer subtle transparency, never use light backgrounds
- Use accent colors semantically (cyan=primary, pink=danger, yellow=warning, green=success)

**DON'T:**
- Use light themes or white backgrounds
- Use generic fonts (Arial, Roboto, system-ui)
- Make everything quiet — every page needs at least one loud focal element (`.cyber-card` or `.cyber-table`). The main table or primary content card should glow
- Make everything loud either — too many glowing panels fight for attention. Pick one focal element per page view
- Mix accent colors randomly — each has a semantic role
- Forget the `transition` property on interactive elements
- Use rounded corners (border-radius) — this system uses sharp edges throughout. Exception: tiny status indicator dots (`border-radius: 50%` on `≤8px` circles) are fine
- Use `--text-display` or `--text-stat` for normal page headings — those are rare display sizes. Page titles use Press Start 2P at `clamp(0.8rem, 1.5vw, 1.1rem)`
- Forget that the global `body` font is Inter — JetBrains Mono is the dominant UI font, but you must explicitly set `font-family: var(--font-mono)` on every technical element. Anything without an explicit font-family inherits Inter

## Google Fonts Import

```html
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;700&family=Noto+Sans+JP:wght@700;900&display=swap" rel="stylesheet">
```

## When to Read Reference Files

- **Starting any UI work** → Read `references/tokens.md` first — it has the full `:root` block (copy into your stylesheet) and all shared `@keyframes` animations
- Building **buttons, cards, forms, tables, alerts, badges, tabs** → Read `references/components-core.md`
- Building **code blocks, spinners, progress bars, tooltips, toasts, skeletons, avatars, context menus** → Read `references/components-extended.md`
- Building **page layouts, app shells, sidebars, top bars, breadcrumbs, stat rows, KV panels, form layouts** → Read `references/patterns-layout.md`
- Building **section headers, glitch text, CRT effects, cyber grid, timelines, image treatments, modals, dividers** → Read `references/patterns-effects.md`
