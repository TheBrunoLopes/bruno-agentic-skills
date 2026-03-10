# Design Tokens Reference

All design tokens as CSS custom properties. Copy the `:root` block into your stylesheet — every component in `components.md` and `patterns.md` references these via `var()`.

## Google Fonts Import

```html
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;700&family=Noto+Sans+JP:wght@700;900&display=swap" rel="stylesheet">
```

Or via CSS `@import`:
```css
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;700&family=Noto+Sans+JP:wght@700;900&display=swap');
```

---

## `:root` Token Block

```css
:root {
  /* ── Accent Colors (solid) ── */
  --cyan:    #00f0ff;
  --pink:    #ff003c;
  --yellow:  #fcee0a;
  --green:   #39ff14;

  /* ── Backgrounds ── */
  --bg-deep:         #05050a;
  --bg-surface:      rgba(10, 10, 15, 0.8);
  --bg-surface-dim:  rgba(10, 10, 15, 0.5);
  --bg-surface-faint:rgba(10, 10, 15, 0.4);
  --bg-input:        rgba(0, 240, 255, 0.03);
  --bg-input-focus:  rgba(0, 240, 255, 0.05);
  --bg-panel:        #0a0a0f;

  /* ── Text Hierarchy ── */
  --text-primary:    #ffffff;
  --text-secondary:  rgba(255, 255, 255, 0.8);
  --text-tertiary:   rgba(255, 255, 255, 0.7);
  --text-muted:      rgba(255, 255, 255, 0.55);
  --text-faint:      rgba(255, 255, 255, 0.45);
  --text-ghost:      rgba(255, 255, 255, 0.35);

  /* ── Borders ── */
  --border-structural: rgba(255, 255, 255, 0.06);
  --border-subtle:     rgba(255, 255, 255, 0.08);
  --border-medium:     rgba(255, 255, 255, 0.15);

  /* ── Cyan Opacity Scale ── */
  --cyan-03: rgba(0, 240, 255, 0.03);
  --cyan-05: rgba(0, 240, 255, 0.05);
  --cyan-08: rgba(0, 240, 255, 0.08);
  --cyan-10: rgba(0, 240, 255, 0.1);
  --cyan-15: rgba(0, 240, 255, 0.15);
  --cyan-20: rgba(0, 240, 255, 0.2);
  --cyan-30: rgba(0, 240, 255, 0.3);
  --cyan-40: rgba(0, 240, 255, 0.4);

  /* ── Pink Opacity Scale ── */
  --pink-03: rgba(255, 0, 60, 0.03);
  --pink-05: rgba(255, 0, 60, 0.05);
  --pink-08: rgba(255, 0, 60, 0.08);
  --pink-10: rgba(255, 0, 60, 0.1);
  --pink-15: rgba(255, 0, 60, 0.15);
  --pink-20: rgba(255, 0, 60, 0.2);
  --pink-30: rgba(255, 0, 60, 0.3);
  --pink-40: rgba(255, 0, 60, 0.4);

  /* ── Yellow Opacity Scale ── */
  --yellow-03: rgba(252, 238, 10, 0.03);
  --yellow-05: rgba(252, 238, 10, 0.05);
  --yellow-08: rgba(252, 238, 10, 0.08);
  --yellow-10: rgba(252, 238, 10, 0.1);
  --yellow-15: rgba(252, 238, 10, 0.15);
  --yellow-20: rgba(252, 238, 10, 0.2);
  --yellow-30: rgba(252, 238, 10, 0.3);
  --yellow-40: rgba(252, 238, 10, 0.4);

  /* ── Green Opacity Scale ── */
  --green-03: rgba(57, 255, 20, 0.03);
  --green-05: rgba(57, 255, 20, 0.05);
  --green-08: rgba(57, 255, 20, 0.08);
  --green-10: rgba(57, 255, 20, 0.1);
  --green-15: rgba(57, 255, 20, 0.15);
  --green-20: rgba(57, 255, 20, 0.2);
  --green-30: rgba(57, 255, 20, 0.3);
  --green-40: rgba(57, 255, 20, 0.4);

  /* ── Font Stacks ── */
  --font-pixel: 'Press Start 2P', cursive;
  --font-body:  'Inter', sans-serif;
  --font-mono:  'JetBrains Mono', monospace;
  --font-jp:    'Noto Sans JP', sans-serif;

  /* ── Type Scale — Display (rare: hero/landing pages, large stat values) ── */
  --text-display: 2.2rem;
  --text-stat:    1.4rem;

  /* ── Type Scale — Headings ── */
  --text-h2:    1.1rem;
  --text-h3:    1rem;
  --text-title: 0.9rem;  /* Same value as --text-body — use for Press Start 2P titles and section headers */

  /* ── Type Scale — Working Range (used in most UI) ── */
  --text-body:  0.9rem;
  --text-sm:    0.8rem;
  --text-xs:    0.75rem;
  --text-label: 0.7rem;
  --text-micro: 0.65rem;
  --text-nano:  0.6rem;

  /* ── Letter Spacing (pair with uppercase JetBrains Mono) ── */
  --tracking-normal:  0.1em;
  --tracking-wide:    0.12em;
  --tracking-wider:   0.15em;
  --tracking-widest:  0.2em;

  /* ── Line Heights ── */
  --leading-tight:  1.2;
  --leading-normal: 1.6;
  --leading-loose:  1.8;

  /* ── Spacing Scale ── */
  --space-1:   4px;
  --space-2:   8px;
  --space-3:  12px;
  --space-4:  16px;
  --space-5:  20px;
  --space-6:  24px;
  --space-8:  32px;
  --space-12: 48px;
  --space-20: 80px;

  /* ── Layout ── */
  --container-max: 1024px;
  --container-pad: 24px;
  --sidebar-width: 260px;
  --topbar-height: 56px;

  /* ── Transitions ── */
  --transition-fast:    all 0.12s ease;
  --transition-default: all 0.2s ease;
  --transition-button:  color 0.3s ease, box-shadow 0.3s ease;
  --transition-nav:     all 0.15s ease;
  --transition-slide:   left 0.3s ease;

  /* ── Shadows ── */
  --shadow-glow-cyan:   0 0 10px rgba(0, 240, 255, 0.2);
  --shadow-glow-pink:   0 0 10px rgba(255, 0, 60, 0.2);
  --shadow-glow-yellow: 0 0 10px rgba(252, 238, 10, 0.2);
  --shadow-glow-green:  0 0 10px rgba(57, 255, 20, 0.2);
  --shadow-hover-cyan:  0 0 20px rgba(0, 240, 255, 0.4);
  --shadow-hover-pink:  0 0 20px rgba(255, 0, 60, 0.4);
  --shadow-hover-yellow:0 0 20px rgba(252, 238, 10, 0.4);
  --shadow-hover-green: 0 0 20px rgba(57, 255, 20, 0.4);
  --shadow-dropdown:    0 8px 32px rgba(0, 0, 0, 0.6);

  /* ── Z-Index Scale ── */
  --z-base:     0;
  --z-dropdown: 100;
  --z-sticky:   200;
  --z-overlay:  300;
  --z-modal:    400;
  --z-tooltip:  500;
  --z-toast:    600;
  --z-modal-backdrop: 1000;
}
```

---

## Global Reset

```css
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body {
  background: var(--bg-deep);
  color: var(--text-primary);
  font-family: var(--font-body);
  overflow-x: hidden;
}
::selection { background: var(--pink); color: white; }
```

---

## Shared `@keyframes`

```css
/* ── Spinner rotation ── */
@keyframes spin {
  to { transform: rotate(360deg); }
}

/* ── Pulse dots ── */
@keyframes pulse {
  0%, 80%, 100% { opacity: 0.2; transform: scale(0.8); }
  40% { opacity: 1; transform: scale(1.2); }
}

/* ── Typing cursor blink ── */
@keyframes blink {
  50% { opacity: 0; }
}

/* ── Skeleton shimmer ── */
@keyframes skeletonShimmer {
  0%   { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}

/* ── CRT flicker (opt-in via .crt-flicker) ── */
@keyframes crtFlicker {
  0%   { opacity: 0.88; }
  100% { opacity: 1.0; }
}

/* ── Glitch text — top half ── */
@keyframes glitchTop {
  0%, 90%, 100% { transform: translate(0); }
  92% { transform: translate(-2px, -1px); }
  94% { transform: translate(2px, 1px); }
  96% { transform: translate(-1px, 2px); }
  98% { transform: translate(1px, -1px); }
}

/* ── Glitch text — bottom half ── */
@keyframes glitchBottom {
  0%, 88%, 100% { transform: translate(0); }
  90% { transform: translate(2px, 1px); }
  93% { transform: translate(-2px, -2px); }
  95% { transform: translate(1px, 2px); }
  97% { transform: translate(-1px, -1px); }
}

/* ── 3D grid scroll ── */
@keyframes gridScroll {
  0%   { background-position: 0 0; }
  100% { background-position: 0 60px; }
}
```

---

## Typography Usage Guide

This system prioritizes **readability** within a dense, terminal-inspired aesthetic. The working range for most UI is **0.6rem–0.9rem**. Display sizes (`--text-display`, `--text-stat`) are rare — use only for hero sections and large stat values.

### Press Start 2P — Pixel Headers

This font renders large — **always use it smaller than you'd expect**. Never above `1.1rem` in application UI.

| Size | Token | Use | Example |
|------|-------|-----|---------|
| `clamp(0.8rem, 1.5vw, 1.1rem)` | — | Page titles (responsive) | `PAGE_TITLE` |
| `0.9rem` | `--text-title` | Section headers, card titles | `SECTION_HEADER` |
| `0.7rem` | `--text-label` | Small labels, modal titles | `SMALL_LABEL` |
| `0.65rem` | `--text-micro` | Nav items, brand labels | `NAV_ITEM` |
| `0.6rem` | `--text-nano` | Brand name (topbar) | `NEXUS` |

- **Weight**: 400 only (single weight font)
- **Avoid**: Body text, descriptions — poor readability at length
- Pixel-grid aligned — best at even px values

### Inter — Readable Body Text

| Size | Token | Weight | Use |
|------|-------|--------|-----|
| `1.4rem` | `--text-stat` | 700 (bold) | Hero subheading (rare — Inter is used here only on landing/hero pages) |
| `1rem` | `--text-h3` | 600 (semibold) | Card/dialog titles |
| `0.95rem` | — | 500 (medium) | Body primary (emphasis) |
| `0.9rem` | `--text-body` | 400 (regular) | Body default, descriptions |
| `0.85rem` | — | 400 (regular) | Small body, helper text |

- **Line-height**: `var(--leading-normal)` (1.6) for body, `var(--leading-tight)` (1.2) for headings
- Primary readable font — use for anything requiring comfortable reading

### JetBrains Mono — Technical Workhorse (dominant UI font)

This is the **most-used font** in the system — buttons, labels, inputs, tables, badges, nav, stats, and all technical chrome.

| Size | Token | Weight | Use |
|------|-------|--------|-----|
| `2rem` | — | 700 (bold) | Large stat values (rare) |
| `1.4rem` | `--text-stat` | 700 (bold) | Stat row values |
| `1.1rem` | `--text-h2` | 700 (bold) | Technical headers |
| `0.9rem` | `--text-body` | 400 | Code blocks, data, button text |
| `0.8rem` | `--text-sm` | 400 | Table cells, inline code |
| `0.75rem` | `--text-xs` | 400 | Table headers, breadcrumbs, tabs |
| `0.7rem` | `--text-label` | 400 | Labels, metadata, timestamps |
| `0.65rem` | `--text-micro` | 400/700 | Badges, small labels, toast messages |
| `0.6rem` | `--text-nano` | 400/700 | Micro labels, category tags |

- **Label pattern**: `text-transform: uppercase; letter-spacing: var(--tracking-wide)` to `var(--tracking-wider)`
- **Letter-spacing tiers**:
  - `var(--tracking-normal)` (0.1em) — table headers, tabs, alert titles
  - `var(--tracking-wide)` (0.12em) — stat labels, KV keys, metadata
  - `var(--tracking-wider)` (0.15em) — buttons, form labels, nav items
  - `var(--tracking-widest)` (0.2em) — nav section/group labels
- Use for: code, data, buttons, labels, tables, forms, badges, stats, KV panels

### Noto Sans JP — Decorative Only (optional)

This font is purely atmospheric. If not using Japanese decorative text, you can omit it from the Google Fonts import to save a network request.

| Size | Weight | Opacity | Use |
|------|--------|---------|-----|
| `3–4rem` | 900 (black) | 4–8% | Background vertical text |
| `2rem` | 900 | 8–12% | Decorative overlay |
| `1.2rem` | 700 (bold) | 50–55% | Decorative inline |

- `writing-mode: vertical-rl` for edge text, `letter-spacing: 0.5–1rem`
- **Never** use for functional UI text
