# Layout Patterns Reference

Composed layout patterns built from components. All CSS uses `var()` references to tokens in `tokens.md`.

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
  font-size: var(--text-xs);
  color: var(--text-primary);
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: var(--tracking-normal);
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
  letter-spacing: var(--tracking-widest);
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
  font-size: var(--text-micro);
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
  font-size: var(--text-xs);
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
        <div style="font-family: var(--font-pixel); font-size: var(--text-nano); color: var(--cyan);">NEXUS</div>
        <div style="font-family: var(--font-mono); font-size: var(--text-nano); color: var(--text-muted);">v2.4.1</div>
      </div>
    </div>
  </div>

  <!-- Search -->
  <div style="padding: 12px 16px;">
    <div style="position: relative;">
      <svg width="13" height="13" fill="none" stroke="var(--text-faint)" stroke-width="1.5" viewBox="0 0 24 24" style="position: absolute; left: 10px; top: 50%; transform: translateY(-50%);"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
      <div style="padding: 8px 10px 8px 32px; border: 1px solid var(--border-subtle); font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-faint); background: rgba(255,255,255,0.02);">Search...</div>
    </div>
  </div>

  <!-- Nav Group -->
  <div style="padding: 4px 8px;">
    <div style="padding: 6px 12px; font-family: var(--font-mono); font-size: var(--text-nano); text-transform: uppercase; letter-spacing: var(--tracking-wider); color: var(--text-faint);">Main</div>

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
      <span class="cyber-badge filled-green" style="margin-left: auto; font-size: var(--text-nano); padding: 2px 6px;">12</span>
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
        <div style="font-family: var(--font-mono); font-size: var(--text-label); color: var(--text-primary);">Operator</div>
        <div style="font-family: var(--font-mono); font-size: var(--text-nano); color: var(--text-muted);">admin@nexus.io</div>
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
      <span style="font-family: var(--font-pixel); font-size: var(--text-nano); color: var(--cyan);">NEXUS</span>
    </div>
    <!-- Nav links -->
    <a href="#" style="font-family: var(--font-mono); font-size: var(--text-xs); color: var(--cyan); text-decoration: none; padding: 4px 0; border-bottom: 1px solid var(--cyan);">Dashboard</a>
    <a href="#" style="font-family: var(--font-mono); font-size: var(--text-xs); color: var(--text-primary); text-decoration: none; padding: 4px 0; border-bottom: 1px solid transparent;">Projects</a>
    <a href="#" style="font-family: var(--font-mono); font-size: var(--text-xs); color: var(--text-primary); text-decoration: none; padding: 4px 0; border-bottom: 1px solid transparent;">Monitors</a>
  </div>

  <!-- Right: Search + Actions + User -->
  <div style="display: flex; align-items: center; gap: 16px;">
    <!-- Search trigger -->
    <div style="position: relative;">
      <svg width="13" height="13" fill="none" stroke="var(--text-faint)" stroke-width="1.5" viewBox="0 0 24 24" style="position: absolute; left: 10px; top: 50%; transform: translateY(-50%);"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
      <div style="padding: 7px 10px 7px 32px; border: 1px solid var(--border-subtle); font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-faint); background: rgba(255,255,255,0.02); width: 180px; display: flex; justify-content: space-between;">
        <span>Search...</span>
        <span style="border: 1px solid var(--border-medium); padding: 0 5px; font-size: var(--text-nano); color: var(--text-ghost);">&#8984;K</span>
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

## Shared Layout Classes

These classes eliminate inline style repetition across layouts. Copy them alongside the component CSS.

```css
/* ── Quiet Card — supporting content wrapper ── */
.quiet-card {
  border: 1px solid var(--border-subtle);
  background: var(--bg-surface-dim);
}

/* ── Panel Header — title bar with bottom divider ── */
.panel-header {
  padding: var(--space-4) var(--space-5);
  border-bottom: 1px solid var(--border-structural);
}
.panel-header-title {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  font-weight: 700;
  color: var(--text-primary);
  text-transform: uppercase;
  letter-spacing: var(--tracking-normal);
}

/* ── Stat Row ── */
.stat-row {
  display: grid;
  gap: 0;
  border: 1px solid var(--border-structural);
  background: var(--bg-surface-faint);
}
.stat-cell {
  padding: var(--space-5) var(--space-6);
  border-right: 1px solid var(--border-structural);
}
.stat-cell:last-child { border-right: none; }
.stat-label {
  font-family: var(--font-mono);
  font-size: var(--text-micro);
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: var(--tracking-wide);
  margin-bottom: 6px;
}
.stat-value {
  font-family: var(--font-mono);
  font-weight: 700;
  font-size: var(--text-stat);
}

/* ── Key-Value Pairs ── */
.kv-label {
  font-family: var(--font-mono);
  font-size: var(--text-micro);
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: var(--tracking-wide);
  margin-bottom: var(--space-1);
}
.kv-value {
  font-family: var(--font-mono);
  font-size: var(--text-sm);
  color: var(--text-primary);
}
```

---

## Stat Row

Full-width grid displaying key metrics, used below page headers.

```html
<div class="stat-row" style="grid-template-columns: repeat(4, 1fr);">
  <div class="stat-cell">
    <div class="stat-label">GPU Nodes</div>
    <div class="stat-value" style="color: var(--cyan);">8</div>
  </div>
  <div class="stat-cell">
    <div class="stat-label">Utilization</div>
    <div class="stat-value" style="color: var(--yellow);">87%</div>
  </div>
  <div class="stat-cell">
    <div class="stat-label">Active Jobs</div>
    <div class="stat-value" style="color: var(--green);">24</div>
  </div>
  <div class="stat-cell">
    <div class="stat-label">Errors (24h)</div>
    <div class="stat-value" style="color: var(--pink);">2</div>
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
<div class="quiet-card" style="padding: var(--space-5);">
  <div class="panel-header-title" style="margin-bottom: var(--space-4);">Cluster Info</div>
  <div style="display: flex; flex-direction: column; gap: 14px;">
    <div>
      <div class="kv-label">Region</div>
      <div class="kv-value">AP-Northeast-1 (Tokyo)</div>
    </div>
    <div>
      <div class="kv-label">GPU Type</div>
      <div class="kv-value">NVIDIA H100 80GB</div>
    </div>
  </div>
</div>
```

### Variant B — Header divider

```html
<div class="quiet-card">
  <div class="panel-header">
    <div class="panel-header-title">Configuration</div>
  </div>
  <div style="padding: var(--space-5); display: flex; flex-direction: column; gap: 14px;">
    <div>
      <div class="kv-label">Endpoint</div>
      <div class="kv-value" style="color: var(--cyan);">https://api.nexus.io/health</div>
    </div>
    <div>
      <div class="kv-label">Alert Threshold</div>
      <div class="kv-value" style="color: var(--yellow);">200ms</div>
    </div>
    <div>
      <div class="kv-label">Regions</div>
      <div style="display: flex; gap: var(--space-1); flex-wrap: wrap; margin-top: var(--space-1);">
        <span class="cyber-badge sm">AP-NE-1</span>
        <span class="cyber-badge sm">US-E-1</span>
      </div>
    </div>
  </div>
</div>
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
        <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--text-muted); display: flex; align-items: center; gap: 8px; margin-bottom: 8px;">
          <a href="#" style="color: var(--text-muted); text-decoration: none;">CLUSTERS</a>
          <span style="color: var(--text-faint);">/</span>
          <span style="color: var(--cyan);">AP-NORTHEAST-1</span>
        </div>
        <!-- Title -->
        <h3 style="font-family: var(--font-pixel); font-size: var(--text-title); color: var(--text-primary);">GPU_CLUSTER_042</h3>
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

Settings/create form with header, 2-column grid, toggles, and action footer. This example uses a quiet card (appropriate when the form is one of several panels on a page). When the form is the **sole content** of a page, wrap it in `.cyber-card` instead for the loud treatment.

```html
<div class="quiet-card" style="max-width: 480px;">
  <!-- Header -->
  <div class="panel-header">
    <div style="font-family: var(--font-pixel); font-size: var(--text-label); color: var(--text-primary); margin-bottom: var(--space-1);">MONITOR_CONFIG</div>
    <div style="font-family: var(--font-body); font-size: var(--text-sm); color: var(--text-muted);">Configure endpoint monitoring settings</div>
  </div>

  <!-- Form body -->
  <div style="padding: var(--space-6); display: flex; flex-direction: column; gap: var(--space-5);">
    <!-- Full-width field -->
    <div>
      <label class="cyber-label">Endpoint URL <span style="color: var(--pink);">*</span></label>
      <input type="text" class="cyber-input" placeholder="https://api.example.com/health">
    </div>

    <!-- 2-column row -->
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: var(--space-4);">
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
      <div style="font-family: var(--font-mono); font-size: var(--text-micro); color: var(--pink); margin-top: var(--space-1);">&#9888; Value too low</div>
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
  <div style="padding: var(--space-4) var(--space-6); border-top: 1px solid var(--border-structural); display: flex; justify-content: flex-end; gap: 10px;">
    <button class="cyber-btn cyan sm" style="border-color: var(--border-medium); color: var(--text-primary);"><span>Cancel</span></button>
    <button class="cyber-btn cyan sm"><span>Save Changes</span></button>
  </div>
</div>
```
