# Component Reference

## Cards

### Loud Card (`.cyber-card`)
Primary content containers — hero elements, focal data, primary tables.
```css
.cyber-card {
    background: rgba(10, 10, 15, 0.8);
    backdrop-filter: blur(5px);
    border: 1px solid #00f0ff;
    box-shadow: 0 0 10px rgba(0, 240, 255, 0.2);
    padding: 2rem;
}
/* Corner decorations */
.cyber-card::before {
    /* top-left: 20×20px pink corner */
    border-top: 2px solid #ff003c;
    border-left: 2px solid #ff003c;
}
.cyber-card::after {
    /* bottom-right: 20×20px cyan corner */
    border-bottom: 2px solid #00f0ff;
    border-right: 2px solid #00f0ff;
}
```

### Quiet Card (inline styles)
Supporting containers — sidebars, info panels, stat rows, structural grouping.
```css
background: rgba(10, 10, 15, 0.4–0.5);
border: 1px solid rgba(255,255,255,0.08);
padding: 20px;
/* NO glow, NO corner decorations */
```

---

## Buttons (`.cyber-btn`)

```css
.cyber-btn {
    padding: 14px 32px;
    background: transparent;
    font-family: 'JetBrains Mono', monospace;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.15em;
    font-size: 0.85rem;
    min-width: 200px;
    border: 1px solid;
    transition: color 0.3s ease, box-shadow 0.3s ease;
}
```

### Variants
| Variant | Border | Text | Hover glow |
|---------|--------|------|------------|
| Default (cyan) | `#00f0ff` | `#00f0ff` | `rgba(0,240,255,0.3)` |
| `.danger` | `#ff003c` | `#ff003c` | `rgba(255,0,60,0.3)` |
| `.success` | `#39ff14` | `#39ff14` | `rgba(57,255,20,0.3)` |
| `.warning` | `#fcee0a` | `#fcee0a` | `rgba(252,238,10,0.3)` |

### Icon Button (`.icon-btn`)
Compact square button for toolbar actions:
```css
width: 36px; height: 36px;
border: 1px solid rgba(0,240,255,0.3);
background: transparent;
color: rgba(255,255,255,0.8);
/* hover: border-color #00f0ff, color #00f0ff */
```

---

## Form Inputs

### Text Input (`.cyber-input`)
```css
.cyber-input {
    width: 100%;
    padding: 12px 16px;
    background: rgba(0, 240, 255, 0.03);
    border: 1px solid rgba(0, 240, 255, 0.3);
    color: #ffffff;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.85rem;
    transition: all 0.2s ease;
}
.cyber-input:focus {
    background: rgba(0, 240, 255, 0.05);
    border-color: #00f0ff;
    box-shadow: 0 0 10px rgba(0, 240, 255, 0.2);
}
.cyber-input.error {
    border-color: #ff003c;
}
.cyber-input::placeholder {
    color: rgba(255,255,255,0.55);
}
```

### Label (`.cyber-label`)
```css
font-family: 'JetBrains Mono', monospace;
font-size: 0.7rem;
text-transform: uppercase;
letter-spacing: 0.15em;
color: #ffffff;
margin-bottom: 8px;
```

### Textarea (`.cyber-textarea`)
Same styles as `.cyber-input` plus:
```css
resize: vertical;
min-height: 100px;
```

### Select (`.cyber-select`)
Same background/border as `.cyber-input` plus:
```css
appearance: none;
cursor: pointer;
/* Custom cyan chevron SVG as background-image */
background-image: url("data:image/svg+xml,..."); /* cyan down-arrow */
background-position: right 16px center;
```

### Checkbox (`.cyber-checkbox`)
Custom styled with accent color fills. JBM label text.

### Toggle (`.cyber-toggle`)
Custom switch: track + thumb, cyan when active.

### Disabled inputs
```css
opacity: 0.35;
cursor: not-allowed;
```

---

## Table (`.cyber-table`)

```css
.cyber-table {
    background: rgba(10, 10, 15, 0.5);
    border: 1px solid rgba(0, 240, 255, 0.15);
    box-shadow: 0 0 10px rgba(0, 240, 255, 0.08);
}
/* Corner decorations like loud card */

thead th {
    font-family: 'JetBrains Mono';
    font-size: 0.75rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: #00f0ff;
    padding: 16px 20px;
    border-bottom: 1px solid rgba(0, 240, 255, 0.3);
}
tbody td {
    font-family: 'JetBrains Mono';
    font-size: 0.75rem;
    padding: 14px 20px;
    border-bottom: 1px solid rgba(255,255,255,0.06);
}
tbody tr:hover {
    background: rgba(0, 240, 255, 0.04);
}
```

### Status classes for table cells
```css
.status-active    { color: #fcee0a; }
.status-completed { color: #00f0ff; }
.status-success   { color: #39ff14; }
.status-error     { color: #ff003c; }
```

---

## Alerts (`.cyber-alert`)

```css
.cyber-alert {
    padding: 20px 24px;
    border-left: 3px solid;
    font-family: 'Inter', sans-serif;
}
```

| Variant | Border | Background |
|---------|--------|------------|
| `.info` | `#00f0ff` | `rgba(0, 240, 255, 0.08)` |
| `.warning` | `#fcee0a` | `rgba(252, 238, 10, 0.08)` |
| `.error` | `#ff003c` | `rgba(255, 0, 60, 0.08)` |
| `.success` | `#39ff14` | `rgba(57, 255, 20, 0.08)` |

Alert title: JBM, 0.85rem, bold, white.
Alert body: Inter, 0.85rem, secondary color.

---

## Badges (`.cyber-badge`)

```css
font-family: 'JetBrains Mono';
font-size: 0.6rem;
font-weight: 700;
text-transform: uppercase;
letter-spacing: 0.1em;
padding: 4px 10px;
```

| Variant | Background | Text |
|---------|------------|------|
| `.filled-cyan` | `rgba(0,240,255,0.15)` | `#00f0ff` |
| `.filled-green` | `rgba(57,255,20,0.15)` | `#39ff14` |
| `.filled-yellow` | `rgba(252,238,10,0.15)` | `#fcee0a` |
| `.filled-pink` | `rgba(255,0,60,0.15)` | `#ff003c` |

---

## Tabs (`.cyber-tabs`)

```css
.cyber-tabs {
    display: flex;
    border-bottom: 1px solid rgba(240,240,240,0.15);
}
.cyber-tab {
    padding: 12px 24px;
    font-family: 'JetBrains Mono';
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: rgba(255,255,255,0.8);
    border-bottom: 2px solid transparent;
    transition: all 0.2s ease;
}
.cyber-tab:hover {
    color: #00f0ff;
    background: rgba(0,240,255,0.04);
    border-bottom-color: rgba(0,240,255,0.4);
}
.cyber-tab.active {
    color: #00f0ff;
    border-bottom-color: #00f0ff;
}
```

---

## Modal (`.cyber-modal`)

- Backdrop: `rgba(5,5,10,0.85)` with `backdrop-filter: blur(4px)`
- Panel: Same as loud card (cyan border, corner decorations, glow)
- Header: padding `24px 28px`, border-bottom separator, Press Start 2P title at 0.75rem
- Body: padding `28px`
- Footer: padding `20px 28px`, border-top separator, right-aligned buttons

---

## Toasts (`.cyber-toast`)

Fixed position notifications, bottom-right.
```css
background: #0a0a0f;
border: 1px solid rgba(0,240,255,0.15);
min-width: 180px;
box-shadow: 0 8px 32px rgba(0,0,0,0.6);
/* 20px cyan accent bar at top-right corner */
```

| Variant | Accent bar color |
|---------|-----------------|
| `.toast-success` | `#39ff14` |
| `.toast-error` | `#ff003c` |
| `.toast-warning` | `#fcee0a` |
| `.toast-info` | `#00f0ff` |

Title: JBM 0.72rem bold. Message: JBM 0.65rem, `rgba(255,255,255,0.7)`.

---

## Tooltips (`.cyber-tooltip-wrap`)

```css
background: #0a0a0f;
border: 1px solid rgba(0,240,255,0.2);
padding: 8px 12px;
font-family: 'JetBrains Mono';
font-size: 0.65rem;
/* Small cyan accent bar on top edge */
```

---

## Progress Bar (`.cyber-progress`)

Track: `rgba(255,255,255,0.08)`, height 6px.
Fill: accent-colored with `box-shadow` glow animation.
Label: JBM 0.7rem above the track.

---

## Avatars (`.cyber-avatar`)

```css
img {
    filter: grayscale(100%) contrast(125%) brightness(110%);
}
```
Frame variants: `.frame-cyan` (cyan border + glow), `.frame-pink` (pink border + glow).
Sizes: `.xs` (24px), `.sm` (32px), `.md` (48px), `.lg` (64px), `.xl` (96px).

---

## Context Menu / Dropdown

```css
background: #0a0a0f;
border: 1px solid rgba(0,240,255,0.15);
min-width: 180px;
box-shadow: 0 8px 32px rgba(0,0,0,0.6);
/* 20px cyan accent bar at top-right */
```

Items: JBM 0.7rem, padding `9px 14px`, icon 14×14 at 60% opacity.
Hover: cyan bg tint + text/icon → `#00f0ff`.
Danger item: `rgba(255,0,60,0.8)` text, red hover bg.
Divider: `1px solid rgba(255,255,255,0.06)` — separates destructive actions.

---

## Skeleton Loading

```css
background: linear-gradient(90deg,
    rgba(255,255,255,0.03) 25%,
    rgba(255,255,255,0.08) 50%,
    rgba(255,255,255,0.03) 75%
);
background-size: 200% 100%;
animation: shimmer 1.5s infinite;
```
Variants: `.skeleton-heading` (h 20px), `.skeleton-text` (h 12px), `.skeleton-avatar` (circle), `.skeleton-btn` (w 120px, h 36px).
