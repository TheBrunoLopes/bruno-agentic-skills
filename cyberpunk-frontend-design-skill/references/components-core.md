# Core Components Reference

Buttons, cards, forms, tables, alerts, badges, and tabs. All CSS uses `var()` references to tokens in `tokens.md`.

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
  letter-spacing: var(--tracking-wider);
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
| `.sm` | Smaller padding (8px 20px), font-size `var(--text-xs)` (0.75rem), no min-width |
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

### Quiet Card (`.quiet-card`)

Supporting content wrapper — subtle border, no glow, no corner decorations. Defined in `patterns-layout.md`.

```html
<!-- Quiet card — structural / supporting -->
<div class="quiet-card" style="padding: var(--space-5);">
  ...content...
</div>

<!-- Ghost card — minimal stat (fainter background) -->
<div class="quiet-card" style="padding: var(--space-5); background: var(--bg-surface-faint);">
  <div class="stat-label">Requests</div>
  <div class="stat-value" style="color: var(--cyan);">2.4M</div>
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
  letter-spacing: var(--tracking-wider);
  color: var(--text-primary);
  margin-bottom: var(--space-2);
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
  font-size: var(--text-sm);
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
  font-size: var(--text-sm);
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
  letter-spacing: var(--tracking-normal);
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
  font-size: var(--text-sm);
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
  letter-spacing: var(--tracking-normal);
  font-size: var(--text-sm);
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
  <div style="font-size: var(--text-body); color: var(--text-primary);">All systems operating within normal parameters.</div>
</div>

<div class="cyber-alert success">
  <div class="alert-title">&#10003; Success</div>
  <div style="font-size: var(--text-body); color: var(--text-primary);">Deployment completed successfully.</div>
</div>

<div class="cyber-alert warning">
  <div class="alert-title">&#9888; Warning</div>
  <div style="font-size: var(--text-body); color: var(--text-primary);">Memory usage exceeding threshold.</div>
</div>

<div class="cyber-alert error">
  <div class="alert-title">&gt;_ Critical Error</div>
  <div style="font-size: var(--text-body); color: var(--text-primary);">Connection lost. Retrying...</div>
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
  font-size: var(--text-micro);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: var(--tracking-normal);
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
  letter-spacing: var(--tracking-normal);
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
