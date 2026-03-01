# Effects & Visual Patterns Reference

Visual effects, decorations, and interactive patterns. All CSS uses `var()` references to tokens in `tokens.md`.

---

## Section Header (`.section-header`)

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

---

## Glitch Text (`.glitch`)

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

---

## CRT Flicker + Scanlines (`.crt-flicker`)

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

---

## 3D Cyber Grid (`.cyber-grid`)

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

---

## Japanese Background Text

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

---

## Dividers

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

---

## Entrance Animations

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
