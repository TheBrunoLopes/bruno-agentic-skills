# Layout Patterns Reference

## App Shell — Sidebar + Top Bar + Content

The standard application layout uses a sidebar for navigation and a top bar for search/actions.

### Structure
```
┌─────────────────────────────────────────────────┐
│  ☰  ⚡ NEXUS    [Search... ⌘K]  🔔  [AK ▾]    │  ← Top Bar (56px)
├──────────┬──────────────────────────────────────┤
│ MAIN     │  Breadcrumb / path                   │
│ Dashboard│  PAGE_TITLE [BADGE]                  │
│ Searches │  ┌───────┬───────┬───────┬───────┐   │
│ Monitors │  │ Stat  │ Stat  │ Stat  │ Stat  │   │  ← Stat Row
│          │  └───────┴───────┴───────┴───────┘   │
│ SYSTEM   │  ┌─────────────────┬─────────────┐   │
│ Team     │  │                 │  Info Panel  │   │
│ Usage    │  │  Main Content   │  KV pairs    │   │
│          │  │  (table/chart)  │              │   │
│──────────│  └─────────────────┴─────────────┘   │
│ Settings │                                      │
│ [User]   │                                      │
└──────────┴──────────────────────────────────────┘
  260px                    flex: 1
```

---

## Top Bar

```css
height: 56px;
background: rgba(5,5,10,0.95);
border-bottom: 1px solid rgba(255,255,255,0.08);
display: flex;
align-items: center;
justify-content: space-between;
padding: 0 20px;
```

### Left side
- Brand: icon (24×24 cyan border box) + Press Start 2P name (0.5rem cyan)
- Separator: `1px solid rgba(255,255,255,0.08)`, 24px height
- Nav links: JBM 0.72rem, active = cyan + bottom border, inactive = white

### Right side
- Search: icon + input mock + `⌘K` shortcut badge
- Icon buttons (notification bell): 32×32, subtle border
- Divider: vertical 1px line
- User avatar: 28×28 cyan border box with initials

---

## Sidebar Navigation

```css
width: 260px;
background: rgba(5,5,10,0.95);
border-right: 1px solid rgba(255,255,255,0.08);
height: 100vh;
display: flex;
flex-direction: column;
```

### Sections (top to bottom)
1. **Brand** — Logo + name + version, `border-bottom` separator, padding `20px`
2. **Search** — Compact input with icon, padding `12px 16px`
3. **Nav groups** — Uppercase micro label + nav items
4. **Footer** — `border-top` separator, Settings + user profile, `margin-top: auto`

### Nav Item (`.sidebar-nav-item`)
```css
display: flex;
align-items: center;
gap: 10px;
padding: 10px 12px;
border-left: 2px solid transparent;
font-family: 'JetBrains Mono';
font-size: 0.72rem;
color: #ffffff;
transition: all 0.15s ease;
```

### Nav Item States
| State | Border-left | Background | Text + Icon |
|-------|-------------|------------|-------------|
| Default | `transparent` | none | white / `rgba(…0.7)` |
| Hover | `rgba(0,240,255,0.4)` | `rgba(0,240,255,0.04)` | `#00f0ff` |
| Active | `#00f0ff` (solid) | `rgba(0,240,255,0.06)` | `#00f0ff` |

### Nav Group Label
```css
font-family: 'JetBrains Mono';
font-size: 0.55rem;
text-transform: uppercase;
letter-spacing: 0.15em;
color: rgba(255,255,255,0.45);
padding: 6px 12px;
```

### Nav Item with Badge
Badge sits at `margin-left: auto` inside the flex row:
```html
<a class="sidebar-nav-item">
    <svg>…</svg>
    <span>Monitors</span>
    <span class="cyber-badge filled-green" style="margin-left: auto;">12</span>
</a>
```

---

## Breadcrumb Navigation

```css
font-family: 'JetBrains Mono';
font-size: 0.75rem;
display: flex;
align-items: center;
gap: 8px;
```
- Ancestor links: `rgba(255,255,255,0.8)`, no underline
- Separator: `/` in `rgba(255,255,255,0.55)`
- Current page: `#00f0ff`

---

## Stat Row

Full-width grid displaying key metrics.

```css
display: grid;
grid-template-columns: repeat(4, 1fr);
border: 1px solid rgba(255,255,255,0.06);
background: rgba(10,10,15,0.4);
```

### Each stat cell
```css
padding: 20px 24px;
border-right: 1px solid rgba(255,255,255,0.06); /* except last */
```

- **Label**: JBM 0.6rem, `rgba(255,255,255,0.55)`, uppercase, `letter-spacing: 0.12em`, `margin-bottom: 8px`
- **Value**: JBM 1.4rem bold, accent-colored
  - Use cyan for primary metrics (uptime, score)
  - Use yellow for active/in-progress counts
  - Use green for positive numbers
  - Use pink/red for errors, failures

### Example
```
┌─────────────┬─────────────┬─────────────┬─────────────┐
│ GPU NODES   │ UTILIZATION │ ACTIVE JOBS │ ERRORS      │
│ 8           │ 87%         │ 24          │ 2           │
│ (cyan)      │ (yellow)    │ (green)     │ (pink)      │
└─────────────┴─────────────┴─────────────┴─────────────┘
```

---

## Key-Value Info Panel

Used for configuration details, metadata, cluster info.

### Variant A — Flat (inline title)
```css
border: 1px solid rgba(255,255,255,0.08);
background: rgba(10,10,15,0.5);
padding: 20px;
```
Title: JBM 0.7rem bold, uppercase, `letter-spacing: 0.1em`, `margin-bottom: 16px`.

### Variant B — Header divider
Same border/background. Header in separate section:
```css
/* header */
padding: 16px 20px;
border-bottom: 1px solid rgba(255,255,255,0.06);

/* body */
padding: 20px;
```

### KV Pair Pattern
```css
/* label */
font-family: 'JetBrains Mono';
font-size: 0.6rem;
text-transform: uppercase;
letter-spacing: 0.12em;
color: rgba(255,255,255,0.55);
margin-bottom: 4px;

/* value */
font-family: 'JetBrains Mono';
font-size: 0.8rem;
color: #ffffff;
```
- Accent values: URLs in cyan, thresholds in yellow
- Badge chips can be used as values (e.g., region tags)
- Stack pairs with `14px` gap between them

---

## Form Layout — Composed

Standard form layout for create/edit pages:

```
┌─ LOUD CARD ──────────────────────────────────────┐
│ ╔══════════════════════════════════════════════╗  │
│ ║  ☰ SECTION ICON + TITLE (Press Start 2P)    ║  │
│ ╚══════════════════════════════════════════════╝  │
│                                                   │
│  LABEL                    LABEL                   │
│  [ input ____________ ]   [ input ____________ ]  │
│                                                   │
│  LABEL                    LABEL                   │
│  [ select ▾          ]   [ input ____________ ]  │
│                                                   │
│  LABEL                                            │
│  [ textarea                                   ]   │
│  [                                            ]   │
│                                                   │
│  ── divider ──────────────────────────────────── │
│                                                   │
│  [DELETE]                              [✓ SAVE]   │
└───────────────────────────────────────────────────┘
```

- Grid: `grid-template-columns: 1fr 1fr; gap: 24px`
- Full-width fields: `grid-column: span 2`
- Actions row: `display: flex; justify-content: space-between` below a divider
- DELETE = `.cyber-btn.danger`, SAVE = `.cyber-btn.success`

---

## Page Title Pattern

```html
<h1 style="font-family: 'Press Start 2P'; font-size: 1.8rem;">
    API_HEALTH_CHECK
</h1>
<span class="cyber-badge filled-green">PASSING</span>
<!-- Action buttons inline -->
<button class="cyber-btn" style="padding: 8px 16px; min-width: auto;">
    ✎ EDIT
</button>
```

Title + badge + action buttons on the same row using flexbox with `align-items: center; gap: 16px`.

---

## Pagination

```css
display: flex;
align-items: center;
gap: 8px;
```
- Page buttons: 32×32, JBM 0.7rem, subtle border
- Active: cyan border + text
- Info text: JBM 0.7rem, muted color, "1–5 of 1,440"
