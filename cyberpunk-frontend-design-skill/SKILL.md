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

- **`.cyber-*` classes** for any design system component (buttons, cards, forms, tables, alerts, badges, tabs, modals, toasts, progress bars, etc.)
- **Tailwind utilities** for layout (`flex`, `grid`, `gap-*`), spacing (`p-*`, `m-*`), and one-off styles where creating a custom class isn't worth it
- **Inline `style` attributes** for quiet cards and one-off structural styling (this is intentional — see quiet card pattern)

The `@theme` block is a slim bridge — it maps key tokens into Tailwind's namespace so utilities like `text-cyan`, `bg-bg-deep`, `font-mono` work. The `:root` block is the full source of truth for all component CSS.

## Aesthetic Direction

Dark, terminal-inspired cyberpunk. Think sci-fi command interfaces, not gaming neon. The tone is **technical and precise** — clean grids, monospaced data, subtle glows. Restraint over spectacle.

Key principles:
- **Dark-first**: Near-black backgrounds, no light themes
- **Cyan as primary accent**: Used for focus, active states, links, primary actions
- **Pink for danger/decoration**: Errors, destructive actions, corner accents
- **Yellow for warnings/highlights**: Caution states, active status
- **Green for success**: Confirmation, healthy states, positive metrics
- **Loud vs Quiet hierarchy**: Primary content gets glowing borders + corner decorations. Supporting content (sidebars, info panels, stat rows) uses subtle borders with no glow

## Design Thinking — Before You Code

Before writing any code, pause and understand what you're building:

1. **Purpose**: What is this interface for? Data monitoring, content management, configuration, onboarding? The answer shapes which components to reach for.
2. **Information density**: Is this data-heavy (dashboards, tables, stats) or task-focused (forms, wizards)? Data-heavy pages use more loud cards and stat rows. Task-focused pages use quieter layouts with clear form hierarchy.
3. **User attention**: What's the single most important thing on the page? That element gets the loudest treatment (cyan glow, corner decorations, largest type). Everything else supports it.
4. **Hierarchy plan**: Decide the loud/quiet split before building. A page with everything glowing is as bad as a page with nothing glowing. Typically: 1 loud hero element, 2–4 quiet supporting panels.

This system is opinionated but flexible — the aesthetic is fixed, but how you compose components should respond to the specific problem.

## Core Tokens

All tokens are defined as CSS custom properties in `references/tokens.md`. Copy the full `:root` block from that file into your stylesheet — every component and pattern references these via `var()`.

**Key variable groups**: `--bg-*` (backgrounds), `--cyan`/`--pink`/`--yellow`/`--green` (accents + opacity scales at 03–40), `--text-*` (hierarchy), `--border-*` (structural), `--font-*` (4 families), `--text-hero` through `--text-micro` (type scale), `--space-*` (spacing), `--transition-*`, `--shadow-*`, `--z-*`.

Shared `@keyframes` animations (`spin`, `pulse`, `blink`, `skeletonShimmer`, `crtFlicker`, `glitchTop`, `glitchBottom`, `gridScroll`) are also in tokens.md.

### Key Patterns

**Labels**: JetBrains Mono, uppercase, letter-spacing 0.12–0.15em, muted color
**Hover states**: Always include transition (0.15–0.2s ease). Pattern: cyan bg tint + border hint + text color shift to #00f0ff
**Focus states**: Cyan border + box-shadow glow `0 0 10px rgba(0,240,255,0.2)`
**Corner decorations** (loud cards only): `::before` top-left pink, `::after` bottom-right pink, 20px × 20px

## Component Quick Reference

Read `references/components-core.md` and `references/components-extended.md` for full specs. Key classes:

| Component | Class | Notes |
|-----------|-------|-------|
| Card (loud) | `.cyber-card` | Cyan border, glow, pink corner decorations via `::before`/`::after` |
| Card (quiet) | inline styles | Subtle border `rgba(255,255,255,0.08)`, no glow, no class |
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
- **Stat rows**: 4-column grid, accent-colored values, muted uppercase labels
- **KV panels**: Stacked label/value pairs, quiet card container
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

## Production Quality

The code you generate must work, not just look right:

- **Functional interactivity**: Buttons should have click handlers (even if placeholder). Forms should have labels wired to inputs. Tabs should switch. Modals should open/close.
- **Semantic HTML**: Use `<nav>`, `<main>`, `<section>`, `<button>`, `<label>`. Don't `<div>` everything.
- **Responsive awareness**: Use `clamp()` for font sizes on headings. Flex-wrap for card grids. The sidebar should collapse on narrow viewports.
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
- Overuse glow effects — reserve for focus states and loud cards
- Mix accent colors randomly — each has a semantic role
- Forget the `transition` property on interactive elements
- Use rounded corners (border-radius) — this system uses sharp edges throughout

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
