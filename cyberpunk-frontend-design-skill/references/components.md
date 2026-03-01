# Component Reference

Exact CSS and HTML for every component. All CSS uses `var()` references to tokens defined in `tokens.md`.

---

## Buttons (`.cyber-btn`)

### CSS

```css
.cyber-btn {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 14px 32px;
  background: transparent;
  font-family: var(--font-mono);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.15em;
  font-size: var(--text-body);
  cursor: pointer;
  overflow: hidden;
  transition: var(--transition-button);
  min-width: 200px;
}
.cyber-btn::before {
  content: '';
  position: absolute;
  top: 0; left: -100%;
  width: 100%; height: 100%;
  transition: var(--transition-slide);
  z-index: 0;
}
.cyber-btn span { position: relative; z-index: 1; }
.cyber-btn:hover::before { left: 0; }

/* ── Color variants ── */
.cyber-btn.cyan {
  border: 1px solid var(--cyan);
  color: var(--cyan);
}
.cyber-btn.cyan::before { background: var(--cyan); }
.cyber-btn.cyan:hover { color: var(--bg-deep); box-shadow: var(--shadow-hover-cyan); }

.cyber-btn.pink {
  border: 1px solid var(--pink);
  color: var(--pink);
}
.cyber-btn.pink::before { background: var(--pink); }
.cyber-btn.pink:hover { color: var(--bg-deep); box-shadow: var(--shadow-hover-pink); }

.cyber-btn.yellow {
  border: 1px solid var(--yellow);
  color: var(--yellow);
}
.cyber-btn.yellow::before { background: var(--yellow); }
.cyber-btn.yellow:hover { color: var(--bg-deep); box-shadow: var(--shadow-hover-yellow); }

.cyber-btn.green {
  border: 1px solid var(--green);
  color: var(--green);
}
.cyber-btn.green::before { background: var(--green); }
.cyber-btn.green:hover { color: var(--bg-deep); box-shadow: var(--shadow-hover-green); }

/* ── Disabled ── */
.cyber-btn.disabled {
  opacity: 0.35;
  cursor: not-allowed;
  pointer-events: none;
}

/* ── Small variant ── */
.cyber-btn.sm {
  padding: 8px 20px;
  font-size: var(--text-xs);
  min-width: auto;
}
```

### HTML

```html
<!-- Primary button -->
<button class="cyber-btn cyan"><span>INITIALIZE</span></button>

<!-- Color variants: .cyan .pink .yellow .green -->
<!-- Size: add .sm for small -->
<!-- State: add .disabled -->

<!-- Button with icon -->
<button class="cyber-btn cyan">
  <span style="display: inline-flex; align-items: center; gap: 8px;">
    <svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">...</svg>
    SAVE
  </span>
</button>

<!-- Small with icon (gap: 6px) -->
<button class="cyber-btn green sm">
  <span style="display: inline-flex; align-items: center; gap: 6px;">
    <svg width="12" height="12" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">...</svg>
    CONFIRM
  </span>
</button>
```

### Icon Button (`.icon-btn`)

```css
.icon-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px; height: 36px;
  border: 1px solid var(--cyan-30);
  background: transparent;
  color: var(--cyan);
  cursor: pointer;
  transition: var(--transition-default);
}
.icon-btn:hover {
  background: var(--cyan-10);
  box-shadow: var(--shadow-glow-cyan);
}
```

```html
<!-- Icon-only button -->
<button class="icon-btn" title="Copy">
  <svg width="16" height="16" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">...</svg>
</button>

<!-- Colored icon-only (inline override) -->
<button class="icon-btn" style="border-color: var(--pink-30); color: var(--pink);">
  <svg width="16" height="16">...</svg>
</button>
```

### Variants

| Modifier | Effect |
|----------|--------|
| `.cyan` | Cyan border/text, cyan slide-fill, cyan hover glow |
| `.pink` | Pink border/text, pink slide-fill, pink hover glow |
| `.yellow` | Yellow border/text, yellow slide-fill, yellow hover glow |
| `.green` | Green border/text, green slide-fill, green hover glow |
| `.sm` | Smaller padding (8px 20px), font-size 0.7rem, no min-width |
| `.disabled` | Opacity 0.35, no pointer events |

---

## Cards

### Loud Card (`.cyber-card`)

```css
.cyber-card {
  position: relative;
  background: var(--bg-surface);
  backdrop-filter: blur(5px);
  border: 1px solid var(--cyan);
  box-shadow: var(--shadow-glow-cyan);
  padding: 2rem;
}
.cyber-card::before {
  content: '';
  position: absolute;
  top: -1px; left: -1px;
  width: 20px; height: 20px;
  border-top: 2px solid var(--pink);
  border-left: 2px solid var(--pink);
}
.cyber-card::after {
  content: '';
  position: absolute;
  bottom: -1px; right: -1px;
  width: 20px; height: 20px;
  border-bottom: 2px solid var(--pink);
  border-right: 2px solid var(--pink);
}
```

```html
<div class="cyber-card">
  <h3>Card Title</h3>
  <p>Description...</p>
</div>
```

### Quiet Card (inline styles — intentionally no class)

Use inline styles to prevent agents from adding glow/corners. This is the pattern for supporting content.

```html
<!-- Quiet card — structural / supporting -->
<div style="padding: 20px; border: 1px solid var(--border-subtle); background: var(--bg-surface-dim);">
  ...content...
</div>

<!-- Ghost card — minimal stat -->
<div style="padding: 20px; border: 1px solid var(--border-subtle); background: var(--bg-surface-faint);">
  <div>Label</div>
  <div>2.4M</div>
</div>
```

---

## Form Inputs

### Text Input (`.cyber-input`)

```css
.cyber-input {
  width: 100%;
  padding: 12px 16px;
  background: var(--bg-input);
  border: 1px solid var(--cyan-30);
  color: var(--text-primary);
  font-family: var(--font-mono);
  font-size: var(--text-body);
  outline: none;
  transition: var(--transition-default);
}
.cyber-input:focus {
  background: var(--bg-input-focus);
  border-color: var(--cyan);
  box-shadow: var(--shadow-glow-cyan);
}
.cyber-input::placeholder {
  color: var(--text-muted);
}
.cyber-input.error {
  border-color: var(--pink);
}
.cyber-input.error:focus {
  box-shadow: var(--shadow-glow-pink);
}
```

### Label (`.cyber-label`)

```css
.cyber-label {
  display: block;
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  text-transform: uppercase;
  letter-spacing: 0.15em;
  color: var(--text-primary);
  margin-bottom: 8px;
}
```

### Textarea (`.cyber-textarea`)

```css
.cyber-textarea {
  width: 100%;
  padding: 12px 16px;
  background: var(--bg-input);
  border: 1px solid var(--cyan-30);
  color: var(--text-primary);
  font-family: var(--font-mono);
  font-size: var(--text-body);
  outline: none;
  resize: vertical;
  min-height: 100px;
  transition: var(--transition-default);
}
.cyber-textarea:focus {
  background: var(--bg-input-focus);
  border-color: var(--cyan);
  box-shadow: var(--shadow-glow-cyan);
}
```

### Select (`.cyber-select`)

```css
.cyber-select {
  width: 100%;
  padding: 12px 16px;
  background: var(--bg-input);
  border: 1px solid var(--cyan-30);
  color: var(--text-primary);
  font-family: var(--font-mono);
  font-size: var(--text-body);
  outline: none;
  appearance: none;
  cursor: pointer;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%2300f0ff' stroke-width='1.5' fill='none'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 16px center;
}
.cyber-select:focus {
  background-color: var(--bg-input-focus);
  border-color: var(--cyan);
  box-shadow: var(--shadow-glow-cyan);
}
```

### Checkbox (`.cyber-checkbox`)

```css
.cyber-checkbox {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  font-family: var(--font-mono);
  font-size: 0.8rem;
  color: var(--text-primary);
}
.cyber-checkbox input { display: none; }
.cyber-checkbox .checkmark {
  width: 18px; height: 18px;
  border: 1px solid var(--cyan-40);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition-default);
  flex-shrink: 0;
}
.cyber-checkbox input:checked + .checkmark {
  border-color: var(--cyan);
  background: var(--cyan-15);
}
.cyber-checkbox input:checked + .checkmark::after {
  content: '\2713';
  color: var(--cyan);
  font-size: 12px;
}
```

### Toggle (`.cyber-toggle`)

```css
.cyber-toggle {
  display: flex;
  align-items: center;
  gap: 12px;
  cursor: pointer;
  font-family: var(--font-mono);
  font-size: 0.8rem;
}
.cyber-toggle input { display: none; }
.cyber-toggle .track {
  width: 42px; height: 22px;
  border: 1px solid rgba(240, 240, 240, 0.6);
  position: relative;
  transition: all 0.3s ease;
}
.cyber-toggle .track::after {
  content: '';
  position: absolute;
  width: 14px; height: 14px;
  top: 3px; left: 3px;
  background: rgba(240, 240, 240, 0.85);
  transition: all 0.3s ease;
}
.cyber-toggle input:checked + .track {
  border-color: var(--cyan);
  background: var(--cyan-10);
}
.cyber-toggle input:checked + .track::after {
  left: 23px;
  background: var(--cyan);
  box-shadow: 0 0 8px rgba(0, 240, 255, 0.5);
}
```

### HTML

```html
<!-- Text input -->
<label class="cyber-label">Hostname</label>
<input type="text" class="cyber-input" placeholder="Enter target hostname...">

<!-- Error state: add .error -->
<input type="text" class="cyber-input error" value="Invalid value">

<!-- Textarea -->
<label class="cyber-label">Notes</label>
<textarea class="cyber-textarea" placeholder="Enter notes..."></textarea>

<!-- Select -->
<label class="cyber-label">Region</label>
<select class="cyber-select">
  <option>AP-NORTHEAST-1 (Tokyo)</option>
  <option>EU-WEST-1 (Ireland)</option>
</select>

<!-- Checkbox -->
<label class="cyber-checkbox">
  <input type="checkbox" checked>
  <span class="checkmark"></span>
  Enable monitoring
</label>

<!-- Toggle -->
<label class="cyber-toggle">
  <input type="checkbox" checked>
  <span class="track"></span>
  Dark mode
</label>

<!-- Disabled input -->
<input type="text" class="cyber-input" value="LOCKED" disabled style="opacity: 0.35; cursor: not-allowed;">
```

---

## Tables (`.cyber-table`)

### CSS

```css
.cyber-table {
  position: relative;
  width: 100%;
  border: 1px solid var(--cyan);
  box-shadow: 0 0 10px var(--cyan-15);
  overflow: visible;
}
.cyber-table::before {
  content: '';
  position: absolute;
  top: -1px; left: -1px;
  width: 20px; height: 20px;
  border-top: 2px solid var(--pink);
  border-left: 2px solid var(--pink);
  z-index: 2;
}
.cyber-table::after {
  content: '';
  position: absolute;
  bottom: -1px; right: -1px;
  width: 20px; height: 20px;
  border-bottom: 2px solid var(--pink);
  border-right: 2px solid var(--pink);
  z-index: 2;
}
.cyber-table table {
  width: 100%;
  border-collapse: collapse;
  font-family: var(--font-mono);
  font-size: var(--text-body);
}
.cyber-table thead th {
  text-align: left;
  padding: 16px 20px;
  color: var(--cyan);
  text-transform: uppercase;
  font-weight: 700;
  font-size: var(--text-sm);
  letter-spacing: 0.1em;
  border-bottom: 1px solid var(--cyan-30);
}
.cyber-table tbody td {
  padding: 16px 20px;
  border-bottom: 1px solid var(--cyan-10);
  color: var(--text-primary);
}
.cyber-table tbody tr {
  transition: background 0.2s ease;
}
.cyber-table tbody tr:hover {
  background: var(--cyan-05);
}

/* ── Status classes ── */
.cyber-table .status-active    { color: var(--yellow); }
.cyber-table .status-completed { color: var(--cyan); }
.cyber-table .status-success   { color: var(--green); }
.cyber-table .status-error     { color: var(--pink); }
```

### Pagination Button (`.pagination-btn`)

```css
.pagination-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px; height: 36px;
  border: 1px solid rgba(240, 240, 240, 0.6);
  background: transparent;
  color: var(--text-primary);
  font-family: var(--font-mono);
  font-size: 0.8rem;
  cursor: pointer;
  transition: var(--transition-default);
}
.pagination-btn:hover {
  border-color: var(--cyan);
  color: var(--cyan);
}
.pagination-btn.active {
  border-color: var(--cyan);
  color: var(--cyan);
  box-shadow: 0 0 10px var(--cyan-30);
}
```

### HTML

```html
<div class="cyber-table">
  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Status</th>
        <th>Date</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Item name</td>
        <td class="status-success">COMPLETED</td>
        <td>2026-02-24</td>
      </tr>
    </tbody>
  </table>
</div>

<!-- Pagination -->
<div style="display: flex; align-items: center; gap: 4px;">
  <button class="pagination-btn">&lt;</button>
  <button class="pagination-btn active">1</button>
  <button class="pagination-btn">2</button>
  <button class="pagination-btn">3</button>
  <button class="pagination-btn">&gt;</button>
</div>
```

---

## Alerts (`.cyber-alert`)

### CSS

```css
.cyber-alert {
  padding: 20px 24px;
  border-left: 3px solid;
  font-family: var(--font-body);
}
.cyber-alert.info {
  border-color: var(--cyan);
  background: var(--cyan-08);
}
.cyber-alert.warning {
  border-color: var(--yellow);
  background: var(--yellow-08);
}
.cyber-alert.error {
  border-color: var(--pink);
  background: var(--pink-08);
}
.cyber-alert.success {
  border-color: var(--green);
  background: var(--green-08);
}

.cyber-alert .alert-title {
  font-family: var(--font-mono);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  font-size: 0.8rem;
  margin-bottom: 6px;
}
.cyber-alert.info .alert-title    { color: var(--cyan); }
.cyber-alert.warning .alert-title { color: var(--yellow); }
.cyber-alert.error .alert-title   { color: var(--pink); }
.cyber-alert.success .alert-title { color: var(--green); }
```

### HTML

```html
<div class="cyber-alert info">
  <div class="alert-title">&#9432; System Info</div>
  <div style="font-size: 0.9rem; color: var(--text-primary);">All systems operating within normal parameters.</div>
</div>

<div class="cyber-alert success">
  <div class="alert-title">&#10003; Success</div>
  <div style="font-size: 0.9rem; color: var(--text-primary);">Deployment completed successfully.</div>
</div>

<div class="cyber-alert warning">
  <div class="alert-title">&#9888; Warning</div>
  <div style="font-size: 0.9rem; color: var(--text-primary);">Memory usage exceeding threshold.</div>
</div>

<div class="cyber-alert error">
  <div class="alert-title">&gt;_ Critical Error</div>
  <div style="font-size: 0.9rem; color: var(--text-primary);">Connection lost. Retrying...</div>
</div>
```

### Variants

| Modifier | Border color | Background |
|----------|-------------|------------|
| `.info` | `var(--cyan)` | `var(--cyan-08)` |
| `.warning` | `var(--yellow)` | `var(--yellow-08)` |
| `.error` | `var(--pink)` | `var(--pink-08)` |
| `.success` | `var(--green)` | `var(--green-08)` |

---

## Badges (`.cyber-badge`)

### CSS

```css
.cyber-badge {
  display: inline-flex;
  align-items: center;
  padding: 4px 12px;
  font-family: var(--font-mono);
  font-size: 0.65rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  border: 1px solid;
}

/* ── Outline variants ── */
.cyber-badge.cyan   { border-color: var(--cyan);   color: var(--cyan); }
.cyber-badge.pink   { border-color: var(--pink);   color: var(--pink); }
.cyber-badge.yellow { border-color: var(--yellow); color: var(--yellow); }
.cyber-badge.green  { border-color: var(--green);  color: var(--green); }

/* ── Filled variants (solid bg, dark text) ── */
.cyber-badge.filled-cyan   { background: var(--cyan);   color: var(--bg-deep); border-color: var(--cyan); }
.cyber-badge.filled-pink   { background: var(--pink);   color: var(--bg-deep); border-color: var(--pink); }
.cyber-badge.filled-yellow { background: var(--yellow); color: var(--bg-deep); border-color: var(--yellow); }
.cyber-badge.filled-green  { background: var(--green);  color: var(--bg-deep); border-color: var(--green); }
```

### HTML

```html
<!-- Outline badges -->
<span class="cyber-badge cyan">ONLINE</span>
<span class="cyber-badge green">SUCCESS</span>
<span class="cyber-badge pink">CRITICAL</span>
<span class="cyber-badge yellow">PENDING</span>

<!-- Filled badges (solid background, dark text) -->
<span class="cyber-badge filled-cyan">ACTIVE</span>
<span class="cyber-badge filled-green">DEPLOYED</span>
<span class="cyber-badge filled-pink">ERROR</span>
<span class="cyber-badge filled-yellow">WARNING</span>
```

### Variants

| Modifier | Style |
|----------|-------|
| `.cyan` | Outline — cyan border + cyan text |
| `.pink` | Outline — pink border + pink text |
| `.yellow` | Outline — yellow border + yellow text |
| `.green` | Outline — green border + green text |
| `.filled-cyan` | Solid cyan bg, dark text (`#05050a`) |
| `.filled-pink` | Solid pink bg, dark text |
| `.filled-yellow` | Solid yellow bg, dark text |
| `.filled-green` | Solid green bg, dark text |

---

## Code Blocks (`.cyber-code`)

### CSS

```css
.cyber-code {
  background: var(--bg-surface);
  border: 1px solid var(--cyan-15);
  padding: 20px;
  font-family: var(--font-mono);
  font-size: 0.8rem;
  line-height: 1.8;
  overflow-x: auto;
  position: relative;
}
.cyber-code::before {
  content: attr(data-lang);
  position: absolute;
  top: 0; right: 0;
  padding: 4px 12px;
  font-size: var(--text-micro);
  text-transform: uppercase;
  color: var(--bg-deep);
  background: var(--cyan);
  letter-spacing: 0.1em;
}

/* ── Syntax highlighting ── */
.cyber-code .comment  { color: var(--text-muted); }
.cyber-code .keyword  { color: var(--pink); }
.cyber-code .string   { color: var(--yellow); }
.cyber-code .function { color: var(--cyan); }
.cyber-code .variable { color: var(--text-primary); }
```

### Inline Code (no class — inline style)

```css
/* Inline code pattern */
code {
  font-family: var(--font-mono);
  font-size: 0.8rem;
  color: var(--cyan);
  background: var(--cyan-08);
  padding: 2px 8px;
  border: 1px solid var(--cyan-15);
}
```

### HTML

```html
<!-- Code block -->
<div class="cyber-code" data-lang="TypeScript">
  <span class="comment">// Initialize monitor</span>
  <span class="keyword">import</span> { <span class="function">NeuralMonitor</span> }
  <span class="keyword">from</span> <span class="string">'@cyber/core'</span>;
  <span class="keyword">const</span> <span class="variable">monitor</span> = <span class="keyword">new</span> <span class="function">NeuralMonitor</span>();
</div>

<!-- Inline code -->
<code style="font-family: var(--font-mono); font-size: 0.8rem; color: var(--cyan); background: var(--cyan-08); padding: 2px 8px; border: 1px solid var(--cyan-15);">cyber-card</code>
```

---

## Tabs (`.cyber-tabs`)

### CSS

```css
.cyber-tabs {
  display: flex;
  gap: 0;
  border-bottom: 1px solid var(--border-medium);
}
.cyber-tab {
  padding: 12px 24px;
  font-family: var(--font-mono);
  font-size: var(--text-sm);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--text-secondary);
  border-bottom: 2px solid transparent;
  cursor: pointer;
  transition: var(--transition-default);
  background: none;
  border-top: none;
  border-left: none;
  border-right: none;
}
.cyber-tab:hover {
  color: var(--cyan);
  background: var(--cyan-05);
  border-bottom-color: var(--cyan-40);
}
.cyber-tab.active {
  color: var(--cyan);
  border-bottom-color: var(--cyan);
}
```

### HTML

```html
<div class="cyber-tabs">
  <button class="cyber-tab active">Overview</button>
  <button class="cyber-tab">Metrics</button>
  <button class="cyber-tab">Logs</button>
  <button class="cyber-tab">Config</button>
</div>
```

---

## Loading States

### Spinner (`.cyber-spinner`)

```css
.cyber-spinner {
  width: 40px; height: 40px;
  border: 2px solid var(--cyan-15);
  border-top-color: var(--cyan);
  animation: spin 0.8s linear infinite;
}
.cyber-spinner.pink {
  border-color: var(--pink-15);
  border-top-color: var(--pink);
}
.cyber-spinner.green {
  border-color: var(--green-15);
  border-top-color: var(--green);
}
```

### Pulse Dots (`.cyber-pulse`)

```css
.cyber-pulse {
  display: flex;
  gap: 6px;
  align-items: center;
}
.cyber-pulse span {
  width: 8px; height: 8px;
  background: var(--cyan);
  animation: pulse 1.2s ease infinite;
}
.cyber-pulse span:nth-child(2) { animation-delay: 0.15s; }
.cyber-pulse span:nth-child(3) { animation-delay: 0.3s; }
```

### Typing Cursor (`.typing-cursor`)

```css
.typing-cursor {
  display: inline-block;
  width: 8px; height: 18px;
  background: var(--cyan);
  animation: blink 1s step-end infinite;
  vertical-align: text-bottom;
}
```

### HTML

```html
<!-- Spinner (default cyan, .pink, .green) -->
<div class="cyber-spinner"></div>
<div class="cyber-spinner pink"></div>
<div class="cyber-spinner green"></div>

<!-- Pulse dots -->
<div class="cyber-pulse">
  <span></span><span></span><span></span>
</div>

<!-- Typing cursor -->
<span style="font-family: var(--font-mono); font-size: var(--text-body);">
  Initializing<span class="typing-cursor"></span>
</span>
```

---

## Progress Bars (`.cyber-progress`)

### CSS

```css
.cyber-progress {
  width: 100%;
  height: 6px;
  background: var(--border-medium);
  position: relative;
  overflow: hidden;
}
.cyber-progress .fill {
  height: 100%;
  transition: width 0.5s ease;
  position: relative;
}
.cyber-progress .fill.cyan   { background: var(--cyan);   box-shadow: var(--shadow-glow-cyan); }
.cyber-progress .fill.pink   { background: var(--pink);   box-shadow: var(--shadow-glow-pink); }
.cyber-progress .fill.yellow { background: var(--yellow); box-shadow: var(--shadow-glow-yellow); }
.cyber-progress .fill.green  { background: var(--green);  box-shadow: var(--shadow-glow-green); }
```

### HTML

```html
<div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
  <span style="font-family: var(--font-mono); font-size: var(--text-xs); text-transform: uppercase;">CPU Usage</span>
  <span style="font-family: var(--font-mono); font-size: var(--text-xs); color: var(--cyan);">72%</span>
</div>
<div class="cyber-progress">
  <div class="fill cyan" style="width: 72%;"></div>
</div>
```

### Variants

| Fill class | Color | Glow |
|-----------|-------|------|
| `.fill.cyan` | `var(--cyan)` | cyan 50% opacity |
| `.fill.pink` | `var(--pink)` | pink 50% opacity |
| `.fill.yellow` | `var(--yellow)` | yellow 50% opacity |
| `.fill.green` | `var(--green)` | green 50% opacity |

---

## Tooltips (`.cyber-tooltip-wrap`)

### CSS

```css
.cyber-tooltip-wrap {
  position: relative;
  display: inline-flex;
}
.cyber-tooltip {
  position: absolute;
  bottom: calc(100% + 8px);
  left: 50%;
  transform: translateX(-50%);
  background: var(--bg-panel);
  border: 1px solid var(--cyan-20);
  padding: 6px 12px;
  font-family: var(--font-mono);
  font-size: 0.65rem;
  color: var(--text-primary);
  white-space: nowrap;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.15s ease;
  z-index: var(--z-tooltip);
}
.cyber-tooltip::after {
  content: '';
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  border: 5px solid transparent;
  border-top-color: var(--cyan-20);
}

/* ── Bottom variant ── */
.cyber-tooltip.bottom {
  bottom: auto;
  top: calc(100% + 8px);
}
.cyber-tooltip.bottom::after {
  top: auto;
  bottom: 100%;
  border-top-color: transparent;
  border-bottom-color: var(--cyan-20);
}

.cyber-tooltip-wrap:hover .cyber-tooltip {
  opacity: 1;
}
```

### HTML

```html
<!-- Tooltip (default: above) -->
<div class="cyber-tooltip-wrap">
  <button class="icon-btn">
    <svg>...</svg>
  </button>
  <div class="cyber-tooltip">Tooltip text</div>
</div>

<!-- Tooltip below -->
<div class="cyber-tooltip-wrap">
  <button class="icon-btn">
    <svg>...</svg>
  </button>
  <div class="cyber-tooltip bottom">Below tooltip</div>
</div>
```

---

## Toasts (`.cyber-toast`)

### CSS

```css
.cyber-toast {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  padding: 14px 16px;
  background: var(--bg-panel);
  border: 1px solid var(--border-subtle);
  border-left: 3px solid var(--cyan);
  min-width: 320px;
  max-width: 420px;
  box-shadow: var(--shadow-dropdown);
  font-family: var(--font-mono);
}
.cyber-toast .toast-icon {
  flex-shrink: 0;
  width: 18px; height: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 1px;
}
.cyber-toast .toast-content { flex: 1; }
.cyber-toast .toast-title {
  font-size: 0.72rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 3px;
}
.cyber-toast .toast-message {
  font-size: 0.65rem;
  color: var(--text-tertiary);
  line-height: 1.5;
}
.cyber-toast .toast-close {
  flex-shrink: 0;
  background: none;
  border: none;
  color: var(--text-ghost);
  cursor: pointer;
  padding: 0;
  font-size: 1rem;
  line-height: 1;
  transition: color 0.12s ease;
}
.cyber-toast .toast-close:hover { color: var(--text-primary); }

/* ── Variant accent bars ── */
.cyber-toast.toast-success { border-left-color: var(--green); }
.cyber-toast.toast-error   { border-left-color: var(--pink); }
.cyber-toast.toast-warning { border-left-color: var(--yellow); }
.cyber-toast.toast-info    { border-left-color: var(--cyan); }
```

### HTML

```html
<div class="cyber-toast toast-success">
  <div class="toast-icon">
    <svg width="16" height="16" fill="none" stroke="var(--green)" stroke-width="1.5" viewBox="0 0 24 24"><polyline points="20 6 9 17 4 12"/></svg>
  </div>
  <div class="toast-content">
    <div class="toast-title">Deployment Complete</div>
    <div class="toast-message">All services restarted successfully.</div>
  </div>
  <button class="toast-close">&times;</button>
</div>

<div class="cyber-toast toast-error">
  <div class="toast-icon">
    <svg width="16" height="16" fill="none" stroke="var(--pink)" stroke-width="1.5" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><line x1="15" y1="9" x2="9" y2="15"/><line x1="9" y1="9" x2="15" y2="15"/></svg>
  </div>
  <div class="toast-content">
    <div class="toast-title">Connection Failed</div>
    <div class="toast-message">Unable to reach the server.</div>
  </div>
  <button class="toast-close">&times;</button>
</div>
```

### Variants

| Modifier | Left border color |
|----------|------------------|
| `.toast-info` | `var(--cyan)` |
| `.toast-success` | `var(--green)` |
| `.toast-warning` | `var(--yellow)` |
| `.toast-error` | `var(--pink)` |

---

## Skeleton Loading

### CSS

```css
@keyframes skeletonShimmer {
  0%   { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}

.skeleton {
  background: linear-gradient(90deg,
    rgba(255, 255, 255, 0.04) 25%,
    rgba(255, 255, 255, 0.08) 50%,
    rgba(255, 255, 255, 0.04) 75%
  );
  background-size: 200% 100%;
  animation: skeletonShimmer 1.8s ease-in-out infinite;
  border-radius: 2px;
}

.skeleton-text {
  height: 12px;
  margin-bottom: 8px;
}
.skeleton-text.sm { width: 40%; }
.skeleton-text.md { width: 70%; }
.skeleton-text.lg { width: 100%; }

.skeleton-heading {
  height: 18px;
  width: 50%;
  margin-bottom: 12px;
}

.skeleton-avatar {
  width: 36px;
  height: 36px;
}

.skeleton-btn {
  height: 32px;
  width: 100px;
}
```

### HTML

```html
<!-- Skeleton card -->
<div style="padding: 20px; border: 1px solid var(--border-subtle); background: var(--bg-surface-dim);">
  <div class="skeleton skeleton-heading"></div>
  <div class="skeleton skeleton-text lg"></div>
  <div class="skeleton skeleton-text md"></div>
  <div class="skeleton skeleton-text sm"></div>
  <div style="display: flex; gap: 8px; margin-top: 16px;">
    <div class="skeleton skeleton-avatar"></div>
    <div style="flex: 1;">
      <div class="skeleton skeleton-text md"></div>
      <div class="skeleton skeleton-text sm"></div>
    </div>
  </div>
  <div class="skeleton skeleton-btn" style="margin-top: 16px;"></div>
</div>
```

### Variants

| Class | Size |
|-------|------|
| `.skeleton-text.sm` | 40% width, 12px height |
| `.skeleton-text.md` | 70% width, 12px height |
| `.skeleton-text.lg` | 100% width, 12px height |
| `.skeleton-heading` | 50% width, 18px height |
| `.skeleton-avatar` | 36x36px |
| `.skeleton-btn` | 100x32px |

---

## Avatars (`.cyber-avatar`)

Text-initials avatars with color variants and sizing.

### CSS

```css
.cyber-avatar {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: 1px solid var(--cyan-30);
  font-family: var(--font-mono);
  color: var(--cyan);
  flex-shrink: 0;
}

/* ── Sizes ── */
.cyber-avatar.xs { width: 22px; height: 22px; font-size: 0.45rem; }
.cyber-avatar.sm { width: 28px; height: 28px; font-size: 0.55rem; }
.cyber-avatar.md { width: 36px; height: 36px; font-size: 0.65rem; }
.cyber-avatar.lg { width: 48px; height: 48px; font-size: 0.8rem; }
.cyber-avatar.xl { width: 64px; height: 64px; font-size: 1rem; }

/* ── Color variants ── */
.cyber-avatar.pink   { border-color: var(--pink-30);   color: var(--pink); }
.cyber-avatar.yellow { border-color: var(--yellow-30); color: var(--yellow); }
.cyber-avatar.green  { border-color: var(--green-30);  color: var(--green); }

/* ── Avatar group (stacked) ── */
.avatar-group {
  display: flex;
}
.avatar-group .cyber-avatar {
  margin-left: -8px;
  background: var(--bg-deep);
}
.avatar-group .cyber-avatar:first-child {
  margin-left: 0;
}
```

### HTML

```html
<!-- Single avatar -->
<div class="cyber-avatar sm">AK</div>
<div class="cyber-avatar md">BL</div>
<div class="cyber-avatar lg pink">JD</div>
<div class="cyber-avatar xl green">NN</div>

<!-- Avatar group -->
<div class="avatar-group">
  <div class="cyber-avatar sm">AK</div>
  <div class="cyber-avatar sm pink">BL</div>
  <div class="cyber-avatar sm green">JD</div>
  <div class="cyber-avatar sm yellow">NN</div>
</div>
```

### Variants

| Size | Dimensions | Font size |
|------|-----------|-----------|
| `.xs` | 22x22 | 0.45rem |
| `.sm` | 28x28 | 0.55rem |
| `.md` | 36x36 | 0.65rem |
| `.lg` | 48x48 | 0.8rem |
| `.xl` | 64x64 | 1rem |

| Color | Border | Text |
|-------|--------|------|
| default | `var(--cyan-30)` | `var(--cyan)` |
| `.pink` | `var(--pink-30)` | `var(--pink)` |
| `.yellow` | `var(--yellow-30)` | `var(--yellow)` |
| `.green` | `var(--green-30)` | `var(--green)` |

---

## Context Menu (`.context-menu`)

### CSS

```css
.context-menu {
  position: absolute;
  right: 0;
  top: 100%;
  margin-top: 4px;
  background: var(--bg-panel);
  border: 1px solid var(--cyan-15);
  min-width: 180px;
  padding: 4px 0;
  z-index: var(--z-dropdown);
  box-shadow: var(--shadow-dropdown);
}
.context-menu::before {
  content: '';
  position: absolute;
  top: -1px;
  right: 12px;
  width: 20px;
  height: 1px;
  background: var(--cyan);
}

.context-menu-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 9px 14px;
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  color: var(--text-primary);
  cursor: pointer;
  text-decoration: none;
  border: none;
  background: none;
  width: 100%;
  text-align: left;
  transition: var(--transition-fast);
}
.context-menu-item svg {
  flex-shrink: 0;
  opacity: 0.6;
  transition: opacity 0.12s ease;
}
.context-menu-item:hover {
  background: var(--cyan-08);
  color: var(--cyan);
}
.context-menu-item:hover svg {
  opacity: 1;
  stroke: var(--cyan);
}

/* ── Danger item ── */
.context-menu-item.danger {
  color: var(--pink-40);
}
.context-menu-item.danger:hover {
  background: var(--pink-08);
  color: var(--pink);
}
.context-menu-item.danger:hover svg {
  stroke: var(--pink);
}

.context-menu-divider {
  height: 1px;
  background: var(--border-structural);
  margin: 4px 0;
}
```

### HTML

```html
<div class="context-menu">
  <button class="context-menu-item">
    <svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
      <path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/>
      <path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/>
    </svg>
    Edit
  </button>
  <button class="context-menu-item">
    <svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
      <rect x="9" y="9" width="13" height="13" rx="0"/>
      <path d="M5 15H4a1 1 0 0 1-1-1V4a1 1 0 0 1 1-1h10a1 1 0 0 1 1 1v1"/>
    </svg>
    Duplicate
  </button>
  <div class="context-menu-divider"></div>
  <button class="context-menu-item danger">
    <svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
      <polyline points="3 6 5 6 21 6"/>
      <path d="M19 6l-1 14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2L5 6"/>
      <path d="M10 11v6"/><path d="M14 11v6"/>
      <path d="M9 6V4h6v2"/>
    </svg>
    Delete
  </button>
</div>
```
