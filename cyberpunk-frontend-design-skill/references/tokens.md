# Design Tokens Reference

## Color Palette — Full Specification

### Backgrounds
| Token | Value | Use |
|-------|-------|-----|
| Page background | `#05050a` | `<body>`, main container |
| Surface (cards) | `rgba(10, 10, 15, 0.8)` | Loud cards, modal panels |
| Surface (quiet) | `rgba(10, 10, 15, 0.4–0.5)` | Info panels, KV panels, stat rows |
| Input fields | `rgba(0, 240, 255, 0.03)` | Form inputs, textareas, selects |
| Input focus | `rgba(0, 240, 255, 0.05)` | Focused form fields |
| Hover tint | `rgba(0, 240, 255, 0.04)` | Tab hover, nav hover |
| Active tint | `rgba(0, 240, 255, 0.06)` | Active nav items, selected states |

### Accent Colors
| Name | Hex | RGB | Role |
|------|-----|-----|------|
| Cyan | `#00f0ff` | `0, 240, 255` | Primary accent — focus, active, links, primary actions |
| Pink | `#ff003c` | `255, 0, 60` | Danger — errors, delete, destructive, corner decorations |
| Yellow | `#fcee0a` | `252, 238, 10` | Warning — caution states, active/pending status |
| Green | `#39ff14` | `57, 255, 20` | Success — healthy, confirmed, positive metrics |

### Accent Opacity Scale
Used for backgrounds, borders, and glows at different intensities:
```
0.03–0.04  → subtle background tint (inputs, hover)
0.06       → active background tint (selected nav)
0.08       → alert/status backgrounds
0.1        → card/component backgrounds
0.15       → medium borders
0.2        → glow shadows, focus rings
0.3        → default interactive borders
0.4        → hover borders
1.0        → solid text, active borders
```

### Text Colors
| Token | Value | Use |
|-------|-------|-----|
| Primary | `#ffffff` | Headings, active text, input values |
| Secondary | `rgba(255,255,255,0.8)` | Body text, descriptions, sub-labels |
| Muted | `rgba(255,255,255,0.55)` | Placeholders, metadata, labels |
| Faint | `rgba(255,255,255,0.45)` | Disabled text, subtle hints, nav group labels |
| Ghost | `rgba(255,255,255,0.35)` | Keyboard shortcut indicators |

### Border Colors
| Token | Value | Use |
|-------|-------|-----|
| Structural | `rgba(255,255,255,0.06)` | Row dividers, quiet separators |
| Subtle | `rgba(255,255,255,0.08)` | Card borders (quiet), section dividers |
| Medium | `rgba(255,255,255,0.15)` | Visible separators, tab underlines |
| Cyan default | `rgba(0,240,255,0.3)` | Input borders, interactive elements |
| Cyan hover | `rgba(0,240,255,0.4)` | Hover state borders |
| Cyan solid | `#00f0ff` | Active states, focus rings |
| Pink solid | `#ff003c` | Error borders, corner decorations |

---

## Typography — Full Specification

### Font Families
```css
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;700;900&display=swap');
```

### Press Start 2P — Pixel Headers
- **Weight**: 400 only (single weight font)
- **Sizes**: 2.2rem (page title), 1.1rem (section header), 0.85rem (card title), 0.7rem (small label), 0.6rem (nav item)
- **Use for**: Page titles, section headers, navigation labels, status text, UI accents
- **Avoid for**: Body text, long paragraphs, descriptions
- **Note**: Pixel-grid aligned — best at even px values

### Inter — Readable Body Text
- **Weights**: 400 (regular), 500 (medium), 600 (semibold), 700 (bold)
- **Sizes**: 1.4rem (hero subheading, bold), 1rem (card/dialog titles, semibold), 0.9rem (body primary, medium), 0.85rem (body default, regular), 0.8rem (small body/helper)
- **Line-height**: 1.6–1.8 for body, 1.2–1.4 for headings
- **Use for**: Paragraphs, descriptions, card content, dialog text, alert messages

### JetBrains Mono — Technical Workhorse
- **Weights**: 400 (regular), 700 (bold)
- **Sizes**: 1.4rem (bold stat values), 1.1rem (technical headers), 0.85rem (code/data), 0.75rem (table cells), 0.7rem (labels/buttons/metadata), 0.6rem (badges/micro labels)
- **Use for**: Code, data values, button text, labels, table headers, form labels, form values, badges, stats, KV panels, timestamps, metadata
- **Label pattern**: `text-transform: uppercase; letter-spacing: 0.12–0.15em`

### Noto Sans JP — Decorative Only
- **Weights**: 400, 700, 900 (black)
- **Opacity**: 4–15% for background elements, 50–70% for decorative inline
- **Use for**: Background decoration, vertical edge text, atmospheric overlays
- **Never use for**: Functional UI text, labels, body content

---

## Spacing Scale

| Value | Use |
|-------|-----|
| `4px` | Micro gaps, badge internal padding |
| `8px` | Tight spacing, inline gaps, small component padding |
| `12px` | Input padding (vertical), compact card padding |
| `16px` | Default gap, input padding (horizontal), standard spacing |
| `20px` | Card padding (compact), panel padding |
| `24px` | Card padding (standard), section padding, button padding (horizontal) |
| `32px` | Between component groups, larger gaps |
| `48px` | Major section breaks |
| `80px` | Page-level section margins |

### Container
- Max width: `1024px`
- Centered with auto margins
- Horizontal padding: `24px`

### Grid
- Standard grid: `display: grid`
- Common layouts: 2-column (`1fr 1fr`), 3-column, 4-column stat rows
- Gap: `16–24px` between grid items

---

## Shadows & Effects

```css
/* Card glow (loud cards only) */
box-shadow: 0 0 10px rgba(0, 240, 255, 0.2);

/* Focus glow */
box-shadow: 0 0 10px rgba(0, 240, 255, 0.2);

/* Error focus glow */
box-shadow: 0 0 10px rgba(255, 0, 60, 0.2);

/* Dropdown/popup shadow */
box-shadow: 0 8px 32px rgba(0, 0, 0, 0.6);

/* Backdrop blur (cards, modals) */
backdrop-filter: blur(5px);
```

### Transitions
- Default: `transition: all 0.2s ease`
- Buttons: `transition: color 0.3s ease, box-shadow 0.3s ease`
- Nav items: `transition: all 0.15s ease`

### CRT/Glitch Effects (optional decoration)
- Scanline overlay: repeating gradient, 2px lines
- Glitch animation: `clip-path` based text distortion
- Use sparingly for atmospheric elements, never on functional UI
