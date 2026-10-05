# Design Trends & Componenti UI — Settimana 20261005

## [Tailwind CSS v4 — CSS-First Framework](https://tailwindcss.com/blog/tailwindcss-v4)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti i browser

La versione 4 elimina `tailwind.config.js` e porta i token di design direttamente nel CSS. Motore Rust-based (Lightning CSS): build complete in <100ms (vs 3.5s in v3). Include container queries native, 3D transforms, e logical properties RTL.

**Snippet minimo funzionante:**
```css
/* Nuova config CSS-first — niente più tailwind.config.js */
@import "tailwindcss";

@theme {
  --color-brand: oklch(60% 0.25 260);
  --color-surface: oklch(98% 0 0);
  --font-display: "Geist", system-ui;
  --radius-card: 16px;
}
```

```html
<!-- 3D transforms (novità v4) -->
<div class="hover:rotate-y-12 hover:perspective-500 transition-transform duration-300
            bg-white/10 backdrop-blur-md rounded-card p-6">
  Card con 3D tilt
</div>

<!-- Container queries native -->
<div class="@container">
  <div class="@lg:grid-cols-2 @xl:grid-cols-3 grid gap-4">
    <!-- Si adatta al container, non al viewport -->
  </div>
</div>
```

**Quando usarlo:** Qualsiasi nuovo progetto web — v4 è lo standard 2026 per utility-first CSS, specialmente con React/Next.js.

---

## [Bento Grid Layout](https://studiomeyer.io/en/blog/bento-grid-layouts)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti i browser (CSS Grid)

Layout asimmetrico a celle di dimensioni diverse, ispirato alle lunch box giapponesi. Adottato da Apple (WWDC), Google, Microsoft, Spotify. Dwell time 35% superiore ai grid uniformi. Ideale per feature showcase, portfolio, pricing page.

**Snippet minimo funzionante:**
```css
.bento-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: auto;
  gap: 16px;
}

/* Card grande in evidenza */
.card-hero {
  grid-column: span 2;
  grid-row: span 2;
}

/* Card media */
.card-wide {
  grid-column: span 2;
}

/* Card piccola standard */
.card-sm {
  grid-column: span 1;
}

/* Responsive */
@media (max-width: 768px) {
  .bento-grid { grid-template-columns: repeat(2, 1fr); }
  .card-hero  { grid-column: span 2; grid-row: span 1; }
}
```

```html
<div class="bento-grid">
  <div class="card-hero card">Feature principale</div>
  <div class="card-sm card">Feature 2</div>
  <div class="card-sm card">Feature 3</div>
  <div class="card-wide card">Feature 4 — wide</div>
  <div class="card-sm card">Feature 5</div>
  <div class="card-sm card">Feature 6</div>
</div>
```

**Quando usarlo:** Feature section su landing page, portfolio progetti, pricing page, dashboard di statistiche, app showcase.

---

## [Liquid Glass Design System](https://codefronts.com/design-styles/css-liquid-glass-effects/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome / Safari / Edge

Il trend visivo dominante del 2026: interfacce traslucide con profondità fisica, refrazione e riflessi. Eleva il glassmorphism tradizionale con qualità materica. Usato da Apple come linguaggio visivo del sistema operativo e ora adottato ovunque.

**Snippet minimo funzionante:**
```css
/* Liquid Glass card con rim-light e specular highlight */
.liquid-glass-card {
  position: relative;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(24px) saturate(200%) brightness(1.1);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.15);
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.5),
    inset 0 -1px 0 rgba(255, 255, 255, 0.05);
  overflow: hidden;
}

/* Specular sweep su hover */
.liquid-glass-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    135deg,
    rgba(255,255,255,0.15) 0%,
    transparent 50%
  );
  opacity: 0;
  transition: opacity 0.3s;
}

.liquid-glass-card:hover::before { opacity: 1; }
```

**Quando usarlo:** Navbar floating, modal overlay su sfondi ricchi, card su gradienti o foto, widget sidebar, qualsiasi UI che vive "sopra" un background vivace.

---

## [Kinetic Typography & Broken Grid](https://elements.envato.com/learn/web-design-trends)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti i browser

Due trend opposti che convivono nel 2026: la tipografia cinetica (testo che si muove, ruota, scorre come elemento grafico) e i broken grid (layout volutamente asimmetrici che rompono la griglia per comunicare personalità). Entrambi reagiscono all'estetica "troppo pulita" degli anni scorsi.

**Snippet — Tipografia cinetica con Scroll-Driven:**
```css
@keyframes slide-text {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}

.marquee-text {
  display: flex;
  white-space: nowrap;
  font-size: clamp(3rem, 8vw, 8rem);
  font-weight: 900;
  animation: slide-text 12s linear infinite;
}

/* Testo rotante come elemento decorativo */
.rotating-badge {
  width: 120px;
  height: 120px;
  animation: spin 8s linear infinite;
}

@keyframes spin { to { transform: rotate(360deg); } }
```

**Snippet — Broken Grid:**
```css
.broken-grid-section {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  position: relative;
}

.break-left  { transform: translateX(-24px) rotate(-1deg); }
.break-right { transform: translateX(24px) rotate(0.5deg); }
.overlap {
  grid-column: 2 / 4;
  grid-row: 1;
  margin-top: -60px;
  z-index: 2;
}
```

**Quando usarlo:** Portfolio creativi, siti di agenzia, pagine about/manifesto, hero section per brand con forte personalità visiva.
