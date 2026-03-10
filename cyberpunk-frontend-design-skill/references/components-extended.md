# Extended Components Reference

Code blocks, loading states, progress bars, tooltips, toasts, skeletons, avatars, and context menus. All CSS uses `var()` references to tokens in `tokens.md`.

---

## Code Blocks (`.cyber-code`)

### CSS

```css
.cyber-code {
  background: var(--bg-surface);
  border: 1px solid var(--cyan-15);
  padding: 20px;
  font-family: var(--font-mono);
  font-size: var(--text-sm);
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
  letter-spacing: var(--tracking-normal);
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
  font-size: var(--text-sm);
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
<code>cyber-card</code>
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
  font-size: var(--text-micro);
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
  font-size: var(--text-xs);
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 3px;
}
.cyber-toast .toast-message {
  font-size: var(--text-micro);
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
  font-size: var(--text-h3);
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
/* skeletonShimmer keyframe is defined in tokens.md — do not duplicate here */

.skeleton {
  background: linear-gradient(90deg,
    rgba(255, 255, 255, 0.04) 25%,
    rgba(255, 255, 255, 0.08) 50%,
    rgba(255, 255, 255, 0.04) 75%
  );
  background-size: 200% 100%;
  animation: skeletonShimmer 1.8s ease-in-out infinite;
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
.cyber-avatar.md { width: 36px; height: 36px; font-size: var(--text-micro); }
.cyber-avatar.lg { width: 48px; height: 48px; font-size: var(--text-sm); }
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
