# Layout Patterns Reference

Composed patterns built from components in `components.md`. All CSS uses `var()` references to tokens in `tokens.md`.

---

## Effects & Decorations

### Section Header (`.section-header`)

```css
.section-header {
  font-family: var(--font-pixel);
  text-transform: uppercase;
  display: flex;
  align-items: center;
  gap: 1.5rem;
}
.section-header::after {
  content: '';
  flex: 1;
  height: 1px;
  background: linear-gradient(to right, var(--line-color, var(--cyan)), transparent);
}
.section-header.pink::after   { --line-color: var(--pink); }
.section-header.yellow::after { --line-color: var(--yellow); }
.section-header.green::after  { --line-color: var(--green); }
.section-header.cyan::after   { --line-color: var(--cyan); }
```

```html
<h2 class="section-header cyan" style="font-size: clamp(0.8rem, 1.5vw, 1.1rem); margin-bottom: 32px;">
  <span>01_SECTION_NAME</span>
</h2>
<!-- Variants: .cyan .pink .yellow .green -->
```

### Glitch Text (`.glitch`)

```css
.glitch {
  position: relative;
  display: inline-block;
}
.glitch::before,
.glitch::after {
  content: attr(data-text);
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  overflow: hidden;
}
.glitch::before {
  animation: glitchTop 5s linear infinite;
  clip-path: inset(0 0 60% 0);
  text-shadow: -2px 0 var(--cyan);
}
.glitch::after {
  animation: glitchBottom 6s linear infinite;
  clip-path: inset(60% 0 0 0);
  text-shadow: 2px 0 var(--pink);
}
```

```html
<!-- Glitch text -->
<h1 class="glitch" data-text="SYSTEM_ONLINE" style="font-family: var(--font-pixel); font-size: 1.8rem;">SYSTEM_ONLINE</h1>

<!-- Combined: glitch + CRT flicker -->
<h1 class="glitch crt-flicker" data-text="TITLE" style="font-family: var(--font-pixel); font-size: 1.8rem;">TITLE</h1>
```

### CRT Flicker + Scanlines (`.crt-flicker`)

```css
.crt-flicker {
  position: relative;
  animation: crtFlicker 0.15s infinite alternate;
}
.crt-flicker:not(.glitch)::after {
  content: '';
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(0, 0, 0, 0.2) 2px,
    rgba(0, 0, 0, 0.2) 4px
  );
  opacity: 0.3;
  pointer-events: none;
  z-index: 1;
}
```

```html
<!-- CRT flicker (opt-in class) -->
<h1 class="crt-flicker" style="font-family: var(--font-pixel);">FLICKERING</h1>
```

### 3D Cyber Grid (`.cyber-grid`)

```css
.cyber-grid {
  position: fixed;
  top: 50%; left: 50%;
  width: 200vw; height: 200vh;
  transform: translate(-50%, -30%) perspective(500px) rotateX(60deg);
  background:
    linear-gradient(var(--cyan-05) 1px, transparent 1px),
    linear-gradient(90deg, var(--cyan-05) 1px, transparent 1px);
  background-size: 60px 60px;
  animation: gridScroll 20s linear infinite;
  z-index: 0;
  pointer-events: none;
}
```

```html
<div class="cyber-grid"></div>
```

### Japanese Background Text

```css
.jp-bg-left, .jp-bg-right {
  position: fixed;
  writing-mode: vertical-rl;
  font-family: var(--font-jp);
  font-weight: 900;
  font-size: 4rem;
  letter-spacing: 1rem;
  opacity: 0.04;
  color: var(--cyan);
  z-index: 0;
  pointer-events: none;
  top: 0;
  height: 100vh;
  line-height: 1;
  user-select: none;
}
.jp-bg-left  { left: 20px; }
.jp-bg-right { right: 20px; }
```

```html
<div class="jp-bg-left">デザインシステム仕様書コンポーネント</div>
<div class="jp-bg-right">サイバーパンク美学設計基準ネオン</div>
```

### Dividers

```css
/* Gradient fade — accent to transparent */
.cyber-divider {
  height: 1px;
  background: linear-gradient(to right, transparent, var(--cyan-30), transparent);
}
```

```html
<!-- Center fade divider -->
<div class="cyber-divider"></div>

<!-- Directional dividers (inline) -->
<div style="height: 1px; background: linear-gradient(to right, var(--cyan), transparent);"></div>
<div style="height: 1px; background: linear-gradient(to right, var(--pink), transparent);"></div>
<div style="height: 1px; background: linear-gradient(to right, var(--yellow), transparent);"></div>
<div style="height: 1px; background: linear-gradient(to right, var(--green), transparent);"></div>
```

### Entrance Animations

```css
.fade-in {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}
```

---

## Sidebar Navigation

### CSS (`.ds-nav`, `.ds-nav-link`, `.sidebar-nav-item`)

```css
.ds-nav {
  position: fixed;
  top: 0; left: 0;
  width: var(--sidebar-width);
  height: 100vh;
  background: rgba(5, 5, 10, 0.95);
  border-right: 1px solid var(--cyan-10);
  z-index: var(--z-dropdown);
  overflow-y: auto;
  padding: 24px 0;
  backdrop-filter: blur(10px);
}
.ds-nav::-webkit-scrollbar { width: 4px; }
.ds-nav::-webkit-scrollbar-thumb { background: var(--cyan-20); }

.ds-nav-link {
  display: block;
  padding: 10px 24px;
  font-family: var(--font-mono);
  font-size: 0.72rem;
  color: var(--text-primary);
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  transition: var(--transition-default);
  border-left: 2px solid transparent;
}
.ds-nav-link:hover {
  color: var(--cyan);
  background: var(--cyan-03);
  border-left-color: var(--cyan);
}
.ds-nav-link.active-link {
  color: var(--cyan);
  border-left-color: var(--cyan);
}

.ds-nav-section-label {
  padding: 16px 24px 6px;
  font-family: var(--font-mono);
  font-size: var(--text-micro);
  text-transform: uppercase;
  letter-spacing: 0.2em;
  color: var(--text-secondary);
}
```

### Sidebar Nav Item (`.sidebar-nav-item`)

Used in app-shell sidebars (not the design system nav).

```css
.sidebar-nav-item {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 10px;
  text-decoration: none;
  border-left: 2px solid transparent;
  font-family: var(--font-mono);
  font-size: 0.65rem;
  color: var(--text-primary);
  transition: var(--transition-nav);
}
.sidebar-nav-item svg { transition: stroke 0.15s ease; }
.sidebar-nav-item span:not(.cyber-badge) { transition: color 0.15s ease; }

.sidebar-nav-item:hover {
  background: rgba(0, 240, 255, 0.04);
  border-left-color: var(--cyan-40);
  color: var(--cyan);
}
.sidebar-nav-item:hover svg { stroke: var(--cyan); }
.sidebar-nav-item:hover span:not(.cyber-badge) { color: var(--cyan); }

.sidebar-nav-item.active {
  background: rgba(0, 240, 255, 0.06);
  border-left-color: var(--cyan);
  color: var(--cyan);
}
.sidebar-nav-item.active svg { stroke: var(--cyan); }

/* ── Large variant ── */
.sidebar-nav-item.lg {
  gap: 10px;
  padding: 10px 12px;
  font-size: 0.72rem;
}
```

### Full Sidebar HTML

```html
<nav style="width: 260px; background: rgba(5,5,10,0.95); border-right: 1px solid var(--border-subtle); height: 100vh; display: flex; flex-direction: column;">
  <!-- Brand -->
  <div style="padding: 20px 20px 16px; border-bottom: 1px solid var(--border-subtle);">
    <div style="display: flex; align-items: center; gap: 10px;">
      <div style="width: 28px; height: 28px; border: 1px solid var(--cyan); display: flex; align-items: center; justify-content: center;">
        <svg width="14" height="14" fill="none" stroke="var(--cyan)" stroke-width="1.5" viewBox="0 0 24 24"><path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/></svg>
      </div>
      <div>
        <div style="font-family: var(--font-pixel); font-size: 0.55rem; color: var(--cyan);">NEXUS</div>
        <div style="font-family: var(--font-mono); font-size: 0.55rem; color: var(--text-muted);">v2.4.1</div>
      </div>
    </div>
  </div>

  <!-- Search -->
  <div style="padding: 12px 16px;">
    <div style="position: relative;">
      <svg width="13" height="13" fill="none" stroke="var(--text-faint)" stroke-width="1.5" viewBox="0 0 24 24" style="position: absolute; left: 10px; top: 50%; transform: translateY(-50%);"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
      <div style="padding: 8px 10px 8px 32px; border: 1px solid var(--border-subtle); font-family: var(--font-mono); font-size: 0.65rem; color: var(--text-faint); background: rgba(255,255,255,0.02);">Search...</div>
    </div>
  </div>

  <!-- Nav Group -->
  <div style="padding: 4px 8px;">
    <div style="padding: 6px 12px; font-family: var(--font-mono); font-size: 0.55rem; text-transform: uppercase; letter-spacing: 0.15em; color: var(--text-faint);">Main</div>

    <!-- Active item -->
    <a href="#" class="sidebar-nav-item active lg">
      <svg width="16" height="16" fill="none" stroke="var(--cyan)" stroke-width="1.5" viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/></svg>
      <span>Dashboard</span>
    </a>

    <!-- Normal item -->
    <a href="#" class="sidebar-nav-item lg">
      <svg width="16" height="16" fill="none" stroke="var(--text-tertiary)" stroke-width="1.5" viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
      <span>Searches</span>
    </a>

    <!-- Item with badge -->
    <a href="#" class="sidebar-nav-item lg">
      <svg width="16" height="16" fill="none" stroke="var(--text-tertiary)" stroke-width="1.5" viewBox="0 0 24 24"><path d="M22 12h-4l-3 9L9 3l-3 9H2"/></svg>
      <span>Monitors</span>
      <span class="cyber-badge filled-green" style="margin-left: auto; font-size: 0.5rem; padding: 2px 6px;">12</span>
    </a>
  </div>

  <!-- Footer (push to bottom with margin-top: auto) -->
  <div style="margin-top: auto; border-top: 1px solid var(--border-subtle); padding: 8px;">
    <a href="#" class="sidebar-nav-item lg">
      <svg width="16" height="16" fill="none" stroke="var(--text-tertiary)" stroke-width="1.5" viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-2.82 1.18V21a2 2 0 0 1-4 0v-.09a1.65 1.65 0 0 0-1.08-1.51 1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06a1.65 1.65 0 0 0-.33-1.82H3a2 2 0 0 1 0-4h.09a1.65 1.65 0 0 0 1.51-1.08"/></svg>
      <span>Settings</span>
    </a>
    <!-- User -->
    <div style="display: flex; align-items: center; gap: 10px; padding: 10px 12px;">
      <div class="cyber-avatar sm">AK</div>
      <div>
        <div style="font-family: var(--font-mono); font-size: 0.68rem; color: var(--text-primary);">Operator</div>
        <div style="font-family: var(--font-mono); font-size: 0.55rem; color: var(--text-muted);">admin@nexus.io</div>
      </div>
    </div>
  </div>
</nav>
```

---

## Top Bar

```html
<header style="display: flex; align-items: center; justify-content: space-between; padding: 0 20px; height: 56px; background: rgba(5,5,10,0.95); border-bottom: 1px solid var(--border-subtle);">
  <!-- Left: Brand + Nav -->
  <div style="display: flex; align-items: center; gap: 24px;">
    <!-- Brand -->
    <div style="display: flex; align-items: center; gap: 10px; padding-right: 20px; border-right: 1px solid var(--border-subtle);">
      <div style="width: 24px; height: 24px; border: 1px solid var(--cyan); display: flex; align-items: center; justify-content: center;">
        <svg width="12" height="12" fill="none" stroke="var(--cyan)" stroke-width="1.5" viewBox="0 0 24 24"><path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/></svg>
      </div>
      <span style="font-family: var(--font-pixel); font-size: 0.5rem; color: var(--cyan);">NEXUS</span>
    </div>
    <!-- Nav links -->
    <a href="#" style="font-family: var(--font-mono); font-size: 0.72rem; color: var(--cyan); text-decoration: none; padding: 4px 0; border-bottom: 1px solid var(--cyan);">Dashboard</a>
    <a href="#" style="font-family: var(--font-mono); font-size: 0.72rem; color: var(--text-primary); text-decoration: none; padding: 4px 0; border-bottom: 1px solid transparent;">Projects</a>
    <a href="#" style="font-family: var(--font-mono); font-size: 0.72rem; color: var(--text-primary); text-decoration: none; padding: 4px 0; border-bottom: 1px solid transparent;">Monitors</a>
  </div>

  <!-- Right: Search + Actions + User -->
  <div style="display: flex; align-items: center; gap: 16px;">
    <!-- Search trigger -->
    <div style="position: relative;">
      <svg width="13" height="13" fill="none" stroke="var(--text-faint)" stroke-width="1.5" viewBox="0 0 24 24" style="position: absolute; left: 10px; top: 50%; transform: translateY(-50%);"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
      <div style="padding: 7px 10px 7px 32px; border: 1px solid var(--border-subtle); font-family: var(--font-mono); font-size: 0.65rem; color: var(--text-faint); background: rgba(255,255,255,0.02); width: 180px; display: flex; justify-content: space-between;">
        <span>Search...</span>
        <span style="border: 1px solid var(--border-medium); padding: 0 5px; font-size: 0.55rem; color: var(--text-ghost);">&#8984;K</span>
      </div>
    </div>
    <!-- Notification bell -->
    <div style="position: relative;">
      <button class="icon-btn" style="width: 32px; height: 32px; border-color: var(--border-subtle);">
        <svg width="15" height="15" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/></svg>
      </button>
      <div style="position: absolute; top: 4px; right: 4px; width: 7px; height: 7px; background: var(--pink); border-radius: 50%;"></div>
    </div>
    <!-- Divider -->
    <div style="width: 1px; height: 24px; background: var(--border-subtle);"></div>
    <!-- User avatar -->
    <div style="display: flex; align-items: center; gap: 8px; cursor: pointer;">
      <div class="cyber-avatar sm">AK</div>
      <svg width="12" height="12" fill="none" stroke="var(--text-muted)" stroke-width="1.5" viewBox="0 0 24 24"><path d="M6 9l6 6 6-6"/></svg>
    </div>
  </div>
</header>
```

---

## Breadcrumbs

```html
<nav style="font-family: var(--font-mono); font-size: var(--text-sm); display: flex; align-items: center; gap: 8px;">
  <a href="#" style="color: var(--text-secondary); text-decoration: none;">HOME</a>
  <span style="color: var(--text-muted);">/</span>
  <a href="#" style="color: var(--text-secondary); text-decoration: none;">SYSTEMS</a>
  <span style="color: var(--text-muted);">/</span>
  <span style="color: var(--cyan);">NODE-042</span>
</nav>
```

---

## App Shell (composed)

Sidebar + top bar + content area composed together.

```html
<div style="display: flex; height: 100vh;">
  <!-- Sidebar (260px) -->
  <nav style="width: 260px; background: rgba(5,5,10,0.95); border-right: 1px solid var(--border-subtle); flex-shrink: 0; display: flex; flex-direction: column;">
    <!-- ...sidebar content (see Sidebar pattern above)... -->
  </nav>

  <!-- Main area -->
  <div style="flex: 1; display: flex; flex-direction: column; overflow: hidden;">
    <!-- Top bar (56px) -->
    <header style="height: 56px; flex-shrink: 0; display: flex; align-items: center; justify-content: space-between; padding: 0 20px; background: rgba(5,5,10,0.95); border-bottom: 1px solid var(--border-subtle);">
      <!-- ...top bar content (see Top Bar pattern above)... -->
    </header>

    <!-- Content area -->
    <main style="flex: 1; overflow-y: auto; padding: 24px 32px;">
      <!-- Page content goes here -->
    </main>
  </div>
</div>
```

---

## Stat Row

Full-width grid displaying key metrics, used below page headers.

```html
<div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 0; border: 1px solid var(--border-structural); background: var(--bg-surface-faint);">
  <div style="padding: 20px 24px; border-right: 1px solid var(--border-structural);">
    <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 6px;">GPU Nodes</div>
    <div style="font-family: var(--font-mono); font-weight: 700; font-size: var(--text-h1); color: var(--cyan);">8</div>
  </div>
  <div style="padding: 20px 24px; border-right: 1px solid var(--border-structural);">
    <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 6px;">Utilization</div>
    <div style="font-family: var(--font-mono); font-weight: 700; font-size: var(--text-h1); color: var(--yellow);">87%</div>
  </div>
  <div style="padding: 20px 24px; border-right: 1px solid var(--border-structural);">
    <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 6px;">Active Jobs</div>
    <div style="font-family: var(--font-mono); font-weight: 700; font-size: var(--text-h1); color: var(--green);">24</div>
  </div>
  <div style="padding: 20px 24px;">
    <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 6px;">Errors (24h)</div>
    <div style="font-family: var(--font-mono); font-weight: 700; font-size: var(--text-h1); color: var(--pink);">2</div>
  </div>
</div>
```

Color guide for stat values:
- **Cyan** — primary metrics (uptime, score, node count)
- **Yellow** — active/in-progress (utilization, latency)
- **Green** — positive numbers (growth, healthy)
- **Pink** — negative numbers (errors, failures)

---

## Key-Value Info Panel

### Variant A — Flat (inline title)

```html
<div style="border: 1px solid var(--border-subtle); background: var(--bg-surface-dim); padding: 20px;">
  <div style="font-family: var(--font-mono); font-size: var(--text-xs); font-weight: 700; color: var(--text-primary); text-transform: uppercase; letter-spacing: 0.1em; margin-bottom: 16px;">Cluster Info</div>
  <div style="display: flex; flex-direction: column; gap: 14px;">
    <div>
      <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 4px;">Region</div>
      <div style="font-family: var(--font-mono); font-size: 0.8rem; color: var(--text-primary);">AP-Northeast-1 (Tokyo)</div>
    </div>
    <div>
      <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 4px;">GPU Type</div>
      <div style="font-family: var(--font-mono); font-size: 0.8rem; color: var(--text-primary);">NVIDIA H100 80GB</div>
    </div>
  </div>
</div>
```

### Variant B — Header divider

```html
<div style="border: 1px solid var(--border-subtle); background: var(--bg-surface-dim);">
  <div style="padding: 16px 20px; border-bottom: 1px solid var(--border-structural);">
    <div style="font-family: var(--font-mono); font-size: var(--text-xs); font-weight: 700; color: var(--text-primary); text-transform: uppercase; letter-spacing: 0.1em;">Configuration</div>
  </div>
  <div style="padding: 20px; display: flex; flex-direction: column; gap: 14px;">
    <div>
      <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 4px;">Endpoint</div>
      <div style="font-family: var(--font-mono); font-size: 0.8rem; color: var(--cyan);">https://api.nexus.io/health</div>
    </div>
    <div>
      <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 4px;">Alert Threshold</div>
      <div style="font-family: var(--font-mono); font-size: 0.8rem; color: var(--yellow);">200ms</div>
    </div>
    <div>
      <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 4px;">Regions</div>
      <div style="display: flex; gap: 4px; flex-wrap: wrap; margin-top: 4px;">
        <span class="cyber-badge" style="font-size: 0.55rem; padding: 2px 7px;">AP-NE-1</span>
        <span class="cyber-badge" style="font-size: 0.55rem; padding: 2px 7px;">US-E-1</span>
      </div>
    </div>
  </div>
</div>
```

---

## Timeline (`.cyber-timeline`)

### CSS

```css
.cyber-timeline {
  border-left: 1px solid var(--yellow-30);
  padding-left: 2rem;
  position: relative;
}
.cyber-timeline-item {
  position: relative;
  margin-bottom: 2rem;
}
.cyber-timeline-item::before {
  content: '';
  position: absolute;
  left: calc(-2rem - 5px);
  top: 6px;
  width: 10px; height: 10px;
  background: var(--yellow);
  border-radius: 50%;
  transition: box-shadow 0.3s ease;
}
.cyber-timeline-item:hover::before {
  box-shadow: 0 0 12px rgba(252, 238, 10, 0.8);
}
```

### HTML

```html
<div class="cyber-timeline">
  <div class="cyber-timeline-item">
    <div style="font-family: var(--font-mono); font-size: 0.65rem; color: var(--yellow); text-transform: uppercase; letter-spacing: 0.15em; margin-bottom: 4px;">Phase 04 // Live</div>
    <div style="font-family: var(--font-body); font-weight: 600; margin-bottom: 4px;">Public Launch</div>
    <div style="font-family: var(--font-body); font-size: var(--text-body); color: var(--text-secondary);">Product goes live. Monitoring dashboards active.</div>
    <div style="margin-top: 8px; display: flex; gap: 6px;">
      <span class="cyber-badge filled-green">DEPLOYED</span>
      <span class="cyber-badge cyan">v1.0.0</span>
    </div>
  </div>
  <div class="cyber-timeline-item">
    <div style="font-family: var(--font-mono); font-size: 0.65rem; color: var(--yellow); text-transform: uppercase; letter-spacing: 0.15em; margin-bottom: 4px;">Phase 03 // Beta</div>
    <div style="font-family: var(--font-body); font-weight: 600; margin-bottom: 4px;">Closed Beta</div>
    <div style="font-family: var(--font-body); font-size: var(--text-body); color: var(--text-secondary);">Invite-only access for testing.</div>
  </div>
</div>
```

---

## Image Treatment (Portrait)

Cyberpunk-filtered portrait with offset frames, overlays, decorative bars, and corner brackets.

```html
<div style="width: 220px; height: 220px; position: relative; margin: 24px;">
  <!-- Offset frame: Cyan (back-right) -->
  <div style="position: absolute; inset: 0; border: 2px solid var(--cyan); transform: translate(16px, 16px);"></div>
  <!-- Offset frame: Pink (back-left) -->
  <div style="position: absolute; inset: 0; border: 2px solid var(--pink); transform: translate(-16px, -16px);"></div>

  <!-- Main image container -->
  <div style="position: absolute; inset: 0; background: var(--bg-deep); z-index: 10; overflow: hidden; border: 1px solid var(--border-medium);">
    <!-- Cyan overlay -->
    <div style="position: absolute; inset: 0; background: var(--cyan); mix-blend-mode: overlay; opacity: 0.2; z-index: 20; pointer-events: none;"></div>
    <!-- Bottom gradient fade -->
    <div style="position: absolute; inset: 0; background: linear-gradient(to bottom, transparent 50%, rgba(5,5,10,0.8)); z-index: 20; pointer-events: none;"></div>
    <!-- Image -->
    <img src="photo.jpg" style="width: 100%; height: 100%; object-fit: cover; filter: grayscale(100%) contrast(125%) brightness(117%); position: relative; z-index: 10;" />
  </div>

  <!-- Decorative bars -->
  <div style="position: absolute; right: -32px; top: 48px; width: 64px; height: 3px; background: var(--yellow); z-index: 20;"></div>
  <div style="position: absolute; left: -32px; bottom: 48px; width: 64px; height: 3px; background: var(--cyan); z-index: 20;"></div>

  <!-- Corner brackets -->
  <div style="position: absolute; top: 0; right: 0; width: 16px; height: 16px; border-top: 2px solid white; border-right: 2px solid white; z-index: 20; transform: translate(8px, -8px);"></div>
  <div style="position: absolute; bottom: 0; left: 0; width: 16px; height: 16px; border-bottom: 2px solid white; border-left: 2px solid white; z-index: 20; transform: translate(-8px, 8px);"></div>

  <!-- Status indicator -->
  <div style="position: absolute; bottom: 12px; right: 12px; z-index: 30; display: flex; align-items: center; gap: 6px; background: rgba(5,5,10,0.8); padding: 4px 10px; border: 1px solid var(--cyan-30); backdrop-filter: blur(4px);">
    <div style="width: 7px; height: 7px; background: var(--cyan); border-radius: 50%; animation: pulse 1.5s ease infinite;"></div>
    <span style="font-family: var(--font-mono); font-size: 9px; color: var(--cyan); text-transform: uppercase; letter-spacing: 0.15em;">Online</span>
  </div>
</div>
```

Image filter specs:
- `filter: grayscale(100%) contrast(125%) brightness(117%)`
- Cyan overlay: `mix-blend-mode: overlay; opacity: 0.2`
- Bottom gradient: `transparent 50%` to `rgba(5,5,10,0.8)`
- Offset frames: `translate(16px, 16px)` for cyan, `translate(-16px, -16px)` for pink

---

## Modals (`.cyber-modal`)

### CSS

```css
.cyber-modal-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(5, 5, 10, 0.85);
  backdrop-filter: blur(4px);
  z-index: var(--z-modal-backdrop);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}
.cyber-modal-backdrop.active {
  opacity: 1;
  pointer-events: all;
}
.cyber-modal {
  width: 90%;
  max-width: 500px;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}
.cyber-modal-backdrop.active .cyber-modal {
  transform: translateY(0);
}
```

### HTML

```html
<!-- Modal backdrop + panel -->
<div id="myModal" class="cyber-modal-backdrop" onclick="if(event.target===this) this.classList.remove('active')">
  <div class="cyber-modal">
    <div class="cyber-card" style="padding: 32px;">
      <div style="font-family: var(--font-pixel); font-size: 0.7rem; color: var(--pink); margin-bottom: 16px;">&#9888; CONFIRM_ACTION</div>
      <div style="font-family: var(--font-body); font-size: 0.9rem; color: var(--text-primary); margin-bottom: 24px; line-height: 1.6;">
        Are you sure you want to proceed? This action cannot be undone.
      </div>
      <div style="display: flex; gap: 12px; justify-content: flex-end;">
        <button class="cyber-btn cyan sm" onclick="document.getElementById('myModal').classList.remove('active')"><span>CANCEL</span></button>
        <button class="cyber-btn pink sm" onclick="document.getElementById('myModal').classList.remove('active')"><span>CONFIRM</span></button>
      </div>
    </div>
  </div>
</div>

<!-- Open modal -->
<script>document.getElementById('myModal').classList.add('active');</script>
<!-- Close modal -->
<script>document.getElementById('myModal').classList.remove('active');</script>
```

---

## Page Layout (composed detail page)

Full detail page: page header with breadcrumb + title + badge + actions, stat row, tabs, content grid with table + info panel.

```html
<div style="border: 1px solid var(--border-subtle); background: var(--bg-deep); overflow: hidden;">
  <!-- Page header -->
  <div style="padding: 24px 32px; border-bottom: 1px solid var(--border-subtle);">
    <div style="display: flex; align-items: center; justify-content: space-between;">
      <div>
        <!-- Breadcrumb -->
        <div style="font-family: var(--font-mono); font-size: 0.65rem; color: var(--text-muted); display: flex; align-items: center; gap: 8px; margin-bottom: 8px;">
          <a href="#" style="color: var(--text-muted); text-decoration: none;">CLUSTERS</a>
          <span style="color: var(--text-faint);">/</span>
          <span style="color: var(--cyan);">AP-NORTHEAST-1</span>
        </div>
        <!-- Title -->
        <h3 style="font-family: var(--font-pixel); font-size: 0.85rem; color: var(--text-primary);">GPU_CLUSTER_042</h3>
      </div>
      <div style="display: flex; align-items: center; gap: 10px;">
        <span class="cyber-badge filled-green">HEALTHY</span>
        <button class="cyber-btn cyan sm" style="padding: 8px 16px; min-width: auto;"><span>EDIT</span></button>
        <button class="icon-btn" style="width: 32px; height: 32px;">
          <svg width="14" height="14" fill="currentColor" viewBox="0 0 24 24"><circle cx="12" cy="5" r="1.5"/><circle cx="12" cy="12" r="1.5"/><circle cx="12" cy="19" r="1.5"/></svg>
        </button>
      </div>
    </div>
  </div>

  <!-- Stat row -->
  <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 0; border-bottom: 1px solid var(--border-subtle);">
    <!-- ...stat cells (see Stat Row pattern)... -->
  </div>

  <!-- Tabs -->
  <div style="padding: 0 32px;">
    <div class="cyber-tabs">
      <button class="cyber-tab active" style="padding: 14px 20px;">Overview</button>
      <button class="cyber-tab" style="padding: 14px 20px;">Nodes</button>
      <button class="cyber-tab" style="padding: 14px 20px;">Jobs</button>
      <button class="cyber-tab" style="padding: 14px 20px;">Logs</button>
    </div>
  </div>

  <!-- Content area: 2-column grid -->
  <div style="padding: 24px 32px;">
    <div style="display: grid; grid-template-columns: 2fr 1fr; gap: 24px;">
      <!-- Left: Table -->
      <div>
        <div class="cyber-table">
          <table>
            <thead><tr><th>Job</th><th>Status</th><th>Duration</th></tr></thead>
            <tbody>
              <tr><td>llama-finetune-v3</td><td class="status-success">DONE</td><td>4h 23m</td></tr>
              <tr><td>embedding-gen</td><td class="status-active">RUNNING</td><td>1h 52m</td></tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- Right: KV info panel -->
      <div style="border: 1px solid var(--border-subtle); background: var(--bg-surface-dim); padding: 20px;">
        <!-- ...KV pairs (see KV Panel pattern)... -->
      </div>
    </div>
  </div>
</div>
```

---

## Form Layout (composed)

Settings/create form inside a quiet card with header, 2-column grid, toggles, and action footer.

```html
<div style="max-width: 480px; border: 1px solid var(--border-subtle); background: var(--bg-surface-dim);">
  <!-- Header -->
  <div style="padding: 20px 24px; border-bottom: 1px solid var(--border-structural);">
    <div style="font-family: var(--font-pixel); font-size: 0.7rem; color: var(--text-primary); margin-bottom: 4px;">MONITOR_CONFIG</div>
    <div style="font-family: var(--font-body); font-size: 0.8rem; color: var(--text-muted);">Configure endpoint monitoring settings</div>
  </div>

  <!-- Form body -->
  <div style="padding: 24px; display: flex; flex-direction: column; gap: 20px;">
    <!-- Full-width field -->
    <div>
      <label class="cyber-label">Endpoint URL <span style="color: var(--pink);">*</span></label>
      <input type="text" class="cyber-input" placeholder="https://api.example.com/health">
    </div>

    <!-- 2-column row -->
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 16px;">
      <div>
        <label class="cyber-label">Method</label>
        <select class="cyber-select"><option>GET</option><option>POST</option></select>
      </div>
      <div>
        <label class="cyber-label">Interval</label>
        <select class="cyber-select"><option>30s</option><option selected>60s</option></select>
      </div>
    </div>

    <!-- Error field -->
    <div>
      <label class="cyber-label">Alert Threshold (ms)</label>
      <input type="text" class="cyber-input error" value="50">
      <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--pink); margin-top: 4px;">&#9888; Value too low</div>
    </div>

    <!-- Divider -->
    <div style="height: 1px; background: var(--border-structural);"></div>

    <!-- Toggles -->
    <label class="cyber-toggle">
      <input type="checkbox" checked>
      <span class="track"></span>
      Enable alerts
    </label>
    <label class="cyber-toggle">
      <input type="checkbox">
      <span class="track"></span>
      SSL verification
    </label>
  </div>

  <!-- Footer actions -->
  <div style="padding: 16px 24px; border-top: 1px solid var(--border-structural); display: flex; justify-content: flex-end; gap: 10px;">
    <button class="cyber-btn cyan sm" style="border-color: var(--border-medium); color: var(--text-primary);"><span>Cancel</span></button>
    <button class="cyber-btn cyan sm"><span>Save Changes</span></button>
  </div>
</div>
```
