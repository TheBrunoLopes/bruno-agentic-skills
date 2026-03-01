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

Follow Vite's conventions and project structure. Use `npm create vite@latest` with the `react-ts` template as the baseline. Install Tailwind via its Vite plugin — not PostCSS. Use CSS variables in `@theme` for the design tokens so Tailwind utilities can reference them.

When adding UI to an existing project, adapt to whatever stack is already in place rather than re-scaffolding.

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

## Core Tokens — Always Use These

### Colors
```css
/* Backgrounds */
--bg-deep:    #05050a;                    /* page background */
--bg-surface: rgba(10, 10, 15, 0.8);     /* cards, panels */
--bg-subtle:  rgba(10, 10, 15, 0.4-0.5); /* quiet containers */
--bg-input:   rgba(0, 240, 255, 0.03);   /* form inputs */

/* Accent palette */
--cyan:    #00f0ff;     /* primary — focus, active, links */
--pink:    #ff003c;     /* danger — errors, delete, decorations */
--yellow:  #fcee0a;     /* warning — caution, active status */
--green:   #39ff14;     /* success — healthy, confirmed */

/* Text hierarchy */
--text-primary:   #ffffff;
--text-secondary: rgba(255,255,255,0.8);
--text-muted:     rgba(255,255,255,0.55);
--text-faint:     rgba(255,255,255,0.45);

/* Borders */
--border-subtle:  rgba(255,255,255,0.08); /* structural dividers */
--border-medium:  rgba(255,255,255,0.15); /* visible separators */
--border-cyan:    rgba(0,240,255,0.3);    /* interactive elements */
```

### Typography
```css
/* Font stacks — 4 families */
--font-pixel: 'Press Start 2P', cursive;       /* titles, headers, nav labels */
--font-body:  'Inter', sans-serif;              /* paragraphs, descriptions */
--font-mono:  'JetBrains Mono', monospace;      /* EVERYTHING technical — code, data, labels, buttons, forms, tables, badges, stats */
--font-jp:    'Noto Sans JP', sans-serif;       /* decorative Japanese text only */

/* Type scale */
--text-hero:   2.2rem;   /* Press Start 2P — page titles */
--text-h1:     1.4rem;   /* Inter Bold or JBM Bold — hero subheadings, large stats */
--text-h2:     1.1rem;   /* Press Start 2P — section headers */
--text-h3:     1rem;     /* Inter SemiBold — card/dialog titles */
--text-body:   0.85rem;  /* Inter Regular — paragraphs */
--text-sm:     0.75rem;  /* JBM — table data, small text */
--text-xs:     0.7rem;   /* JBM — labels, buttons, metadata */
--text-micro:  0.6rem;   /* JBM — badges, category tags, micro labels */
```

### Spacing
```
4px → micro gaps
8px → tight spacing (badge padding, small gaps)
16px → default gap
24px → section padding, card padding
32px → between groups
48px → major section breaks
80px → page-level section margins
```

### Key Patterns

**Labels**: JetBrains Mono, uppercase, letter-spacing 0.12–0.15em, muted color
**Hover states**: Always include transition (0.15–0.2s ease). Pattern: cyan bg tint + border hint + text color shift to #00f0ff
**Focus states**: Cyan border + box-shadow glow `0 0 10px rgba(0,240,255,0.2)`
**Corner decorations** (loud cards only): `::before` top-left pink, `::after` bottom-right cyan, 20px × 20px

## Component Quick Reference

Read `references/components.md` for full specs. Key classes:

| Component | Class | Notes |
|-----------|-------|-------|
| Card (loud) | `.cyber-card` | Cyan border, glow, corner decorations |
| Card (quiet) | inline styles | Subtle border `rgba(255,255,255,0.08)`, no glow |
| Button | `.cyber-btn` | Variants: default (cyan), `.danger` (pink), `.success` (green), `.warning` (yellow) |
| Input | `.cyber-input` | Cyan-tinted bg `rgba(0,240,255,0.03)`, `.error` for red border |
| Textarea | `.cyber-textarea` | Same as input, `min-height: 100px` |
| Select | `.cyber-select` | Custom chevron, same bg tint |
| Table | `.cyber-table` | Cyan header border, row hover states |
| Alert | `.cyber-alert` | Variants: `.info` `.warning` `.error` `.success` |
| Badge | `.cyber-badge` | Variants: `filled-cyan`, `filled-green`, `filled-yellow`, `filled-pink` |
| Tabs | `.cyber-tabs` > `.cyber-tab` | Bottom border active state, hover animation |
| Modal | `.cyber-modal` | Centered, backdrop blur |
| Toast | `.cyber-toast` | Variants: `-success`, `-error`, `-warning`, `-info` |
| Tooltip | `.cyber-tooltip-wrap` | Dark bg, cyan accent bar |
| Progress | `.cyber-progress` | Animated fill with glow |
| Spinner | `.cyber-spinner` | Cyan border animation |
| Avatar | `.cyber-avatar` | Grayscale filter + cyan/pink frame |
| Timeline | `.cyber-timeline` | Vertical line with dot markers |
| Toggle | `.cyber-toggle` | Custom switch with cyan active |
| Checkbox | `.cyber-checkbox` | Custom check with accent colors |

## Layout Quick Reference

Read `references/patterns.md` for full specs.

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
- **Corner decorations**: The `::before`/`::after` pink-cyan corner marks on loud cards create a "targeting reticle" effect — use on focal elements only.

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
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;700&family=Noto+Sans+JP:wght@400;700;900&display=swap" rel="stylesheet">
```

## When to Read Reference Files

- Building **forms, tables, buttons, cards, alerts, modals, toasts** → Read `references/components.md`
- Building **page layouts, app shells, dashboards, navigation** → Read `references/patterns.md`
- Need **exact color values, typography specs, spacing** → Read `references/tokens.md`
