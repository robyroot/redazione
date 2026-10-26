# Design Trends & Componenti UI — Settimana 20261026

## [Tailwind CSS v4.3 — Scrollbars, Container Queries, Nuovi Colori](https://tailwindcss.com/blog)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Tailwind v4 (uscito gen 2025) continua ad aggiornarsi. Le novità 2026 più rilevanti: v4.2 porta nuove palette neutral (mauve, olive, mist, taupe), v4.3 aggiunge utility per scrollbar customizzate, zoom e `@container-size` per height-based queries. La config ora è in CSS con `@theme`.

**Snippet minimo funzionante:**
```css
/* tailwind.config via CSS (v4) */
@import "tailwindcss";

@theme {
  --color-brand: oklch(65% 0.22 250);
  --color-brand-light: oklch(90% 0.12 250);
  --radius-lg: 16px;
  --font-display: 'Inter', sans-serif;
}
```

```html
<!-- Scrollbar personalizzata (Tailwind v4.3) -->
<div class="overflow-y-auto scrollbar-thin scrollbar-thumb-brand scrollbar-track-transparent">
  ...
</div>

<!-- Container query height-based (v4.3) -->
<div class="@container">
  <div class="@container-size/h-[600px]:text-2xl text-base">
    Testo grande quando il container è alto almeno 600px
  </div>
</div>
```

**Quando usarlo:** Ogni progetto frontend moderno. La CSS-first config riduce il boilerplate, i nuovi colori neutral completano le palette.

---

## [shadcn/ui — Migrazione a Base UI (luglio 2026)](https://ui.shadcn.com)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Da luglio 2026, `npx shadcn init` usa Base UI come default invece di Radix. I progetti Radix esistenti continuano a funzionare. La novità più interessante per i workflow con AI: il **CLI v4** con dry-run e diff, e i **Design System Presets** per token portabili.

**Snippet minimo funzionante:**
```bash
# Nuovo progetto con Base UI (default luglio 2026)
npx shadcn@latest init

# Mantieni Radix se preferisci
npx shadcn@latest init -b radix

# Ispeziona le modifiche prima di applicarle (CLI v4)
npx shadcn@latest add button --dry-run
npx shadcn@latest add button --diff
```

```tsx
// Componente Button shadcn/ui con varianti
import { Button } from "@/components/ui/button"

export function HeroActions() {
  return (
    <div className="flex gap-3">
      <Button size="lg">Inizia gratis</Button>
      <Button variant="outline" size="lg">Guarda demo</Button>
    </div>
  )
}
```

**Quando usarlo:** Qualsiasi app React/Next.js — shadcn rimane il riferimento per componenti accessibili e personalizzabili. La switch a Base UI semplifica l'API (meno props, più composability).

---

## [Tactile Brutalism — Estetica Bold 2026](https://fireart.studio/blog/the-best-web-design-trends/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** tutti ✅

Il "Tactile Brutalism" è il contrend 2026: geometrie nette, contrasto massimo, bordi da 1-2px, sans-serif bold al posto di blur e sfumature morbide. Funziona bene per brand tech che vogliono differenziarsi dall'estetica AI-smooth omologata.

**Snippet minimo funzionante:**
```css
/* Card stile brutalist */
.brutal-card {
  background: #fff;
  border: 2px solid #000;
  border-radius: 0;
  box-shadow: 4px 4px 0 #000;
  padding: 24px;
  transition: transform 0.1s, box-shadow 0.1s;
}

.brutal-card:hover {
  transform: translate(-2px, -2px);
  box-shadow: 6px 6px 0 #000;
}

/* Button brutalist */
.brutal-btn {
  background: #ff0;  /* giallo neon o colore brand */
  color: #000;
  border: 2px solid #000;
  box-shadow: 3px 3px 0 #000;
  padding: 12px 24px;
  font-weight: 700;
  text-transform: uppercase;
  cursor: pointer;
  transition: all 0.1s;
}

.brutal-btn:active {
  transform: translate(3px, 3px);
  box-shadow: none;
}
```

**Quando usarlo:** Startup tech, portfolio di developer/designer, brand che vogliono uno stile riconoscibile e anticonvenzionale rispetto al "SaaS look".

---

## [Bento Grid Layout — Componente Trend 2026](https://www.gleamstudio.design/blog-post/ui-design-trends-2026)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** tutti ✅

Il Bento Grid (griglia asimmetrica con celle di dimensioni diverse) è diventato il layout standard per le sezioni "features" dei siti SaaS nel 2026. Sostituisce i classici 3-column feature grid con qualcosa di più visivamente interessante.

**Snippet minimo funzionante:**
```css
.bento-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: auto;
  gap: 16px;
}

.bento-grid .card-large   { grid-column: span 2; grid-row: span 2; }
.bento-grid .card-wide    { grid-column: span 2; }
.bento-grid .card-tall    { grid-row: span 2; }
.bento-grid .card-normal  { grid-column: span 1; }

/* Responsive: collassa su mobile */
@media (max-width: 768px) {
  .bento-grid { grid-template-columns: 1fr; }
  .bento-grid [class*="card-"] { grid-column: 1; grid-row: auto; }
}
```

```html
<section class="bento-grid">
  <div class="card card-large">Feature principale</div>
  <div class="card card-wide">Feature secondaria</div>
  <div class="card card-normal">Stat 1</div>
  <div class="card card-normal">Stat 2</div>
  <div class="card card-tall">Feature verticale</div>
  <div class="card card-normal">Feature 4</div>
</section>
```

**Quando usarlo:** Sezioni feature di landing page SaaS, page "about" con stats + info, portfolio di progetti.

---

## [Kinetic Typography & Broken Grid](https://elements.envato.com/learn/web-design-trends)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** tutti ✅

Due trend legati: **kinetic type** (testo che si muove, scorre, ruota come parte del design) e **broken grid** (elementi che escono dai confini del layout, si sovrappongono, seguono diagonali). Danno "personalità" visiva ai siti che altrimenti sembrano tutti uguali.

**Snippet minimo funzionante:**
```css
/* Testo che scorre in loop (marquee moderno) */
.marquee-track {
  display: flex;
  overflow: hidden;
  white-space: nowrap;
}

.marquee-content {
  display: flex;
  gap: 48px;
  animation: marquee 20s linear infinite;
}

@keyframes marquee {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}

/* Broken grid: titolo che esce dal container */
.broken-hero {
  position: relative;
}

.broken-hero h1 {
  position: relative;
  z-index: 2;
  margin-left: -8%;   /* esce a sinistra */
  font-size: clamp(3rem, 8vw, 8rem);
  font-weight: 900;
  line-height: 0.9;
}

.broken-hero .bg-image {
  position: absolute;
  top: 20%;
  right: -5%;         /* esce a destra */
  z-index: 1;
}
```

**Quando usarlo:** Hero section di portfolio e siti creativi, agenzie, musicisti, brand fashion — ovunque vuoi un impatto visivo forte che rompa la monotonia dei layout "a box".
