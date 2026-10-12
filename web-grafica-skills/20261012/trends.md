# Design Trends & Componenti UI — Ottobre 2026

## [Tailwind CSS v4.3 — Scrollbar Utilities & Container Queries](https://tailwindcss.com)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅

v4.3 (maggio 2026) porta controllo nativo degli scrollbar e nuove utilities container. Engine Rust-based Oxide con ~10x compile speedup rispetto a v3. Le versioni v4.2 (febbraio 2026) hanno aggiunto 4 nuove palette colori: `mauve`, `olive`, `mist`, `taupe`.

**Snippet minimo funzionante:**
```html
<!-- Scrollbar custom -->
<div class="scrollbar-thin scrollbar-thumb-indigo-500 scrollbar-track-slate-100
            overflow-y-auto h-64">
  ...
</div>

<!-- Container query con height -->
<div class="@container">
  <div class="@sm:grid-cols-2 @lg:grid-cols-3">
    <!-- Risponde al container, non al viewport -->
  </div>
</div>

<!-- Nuove palette v4.2 -->
<div class="bg-mauve-500 text-mauve-50">...</div>
<div class="bg-mist-300 text-mist-900">...</div>

<!-- Logical properties -->
<div class="pbs-4 mbe-6">padding-block-start, margin-block-end</div>
```

**Quando usarlo:** Ogni nuovo progetto web. v4.x è il punto di arrivo del framework: CSS-first config via `@theme`, zero classi in JS, integrazione nativa con PostCSS e Vite.

---

## [shadcn/ui + Base UI — Il Cambio del 2026](https://ui.shadcn.com)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅

A luglio 2026 shadcn/ui ha spostato il layer primitivo di default da **Radix UI** a **Base UI** (v1.8.0 da settembre 2026). `npx shadcn init` ora usa Base UI; Radix rimane supportato e non è deprecated. CLI v4 aggiunge `--dry-run` e `--diff` per preview delle modifiche.

**Snippet minimo funzionante:**
```bash
# Nuovo progetto (usa Base UI di default)
npx shadcn@latest init

# Progetto esistente — forza Radix
npx shadcn@latest init -b radix

# Migrazione da vecchio Radix all-in-one
pnpm dlx shadcn@latest migrate radix

# Aggiungere componente
npx shadcn@latest add dialog
```

```tsx
// Differenza API Base UI vs Radix
// Radix: <Button asChild><a href="/">Link</a></Button>
// Base UI: <Button render={<a href="/" />}>Link</Button>
import { Dialog } from '@base-ui/react';

<Dialog.Root>
  <Dialog.Trigger>Apri</Dialog.Trigger>
  <Dialog.Portal>
    <Dialog.Overlay />
    <Dialog.Popup>
      <Dialog.Title>Titolo</Dialog.Title>
    </Dialog.Popup>
  </Dialog.Portal>
</Dialog.Root>
```

**Quando usarlo:** Design system React moderni. Nuovi progetti: Base UI. Progetti esistenti Radix: non migrare a meno che non sia necessario (breaking changes silenziosi).

---

## [Brutalism Tattico e Broken Grid](https://fireart.studio/blog/the-best-web-design-trends/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Universale

Trend dominante del 2026: geometria cruda, contrasto aggressivo, texture fisiche, border-radius=0, tipografia monospace, griglie asimmetriche. Reazione al soft UI e al minimalismo estremo degli anni precedenti. Adatto a brand che vogliono personalità forte.

**Snippet minimo funzionante:**
```css
/* Brutalist card */
.card-brutal {
  border: 3px solid #000;
  border-radius: 0;
  box-shadow: 6px 6px 0 #000;
  background: #fff;
  padding: 1.5rem;
  transition: transform 0.15s, box-shadow 0.15s;
}

.card-brutal:hover {
  transform: translate(-3px, -3px);
  box-shadow: 9px 9px 0 #000;
}

/* Typography brutalista */
.headline-brutal {
  font-family: 'Space Mono', monospace;
  font-size: clamp(2rem, 8vw, 6rem);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: -0.02em;
  color: #000;
  mix-blend-mode: multiply;
}

/* Broken grid */
.broken-grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
}
.item-1 { grid-column: 1 / 7; grid-row: 1; }
.item-2 { grid-column: 5 / 13; grid-row: 1 / 3; margin-top: -2rem; }
```

**Quando usarlo:** Portfolio creativi, brand giovani/tech, landing page di prodotti innovativi. Evitare per e-commerce mainstream o istituzioni.

---

## [Bento Grid Layout](https://www.webfx.com/blog/web-design/ux-ui-trends/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Universale (CSS Grid)

Layout a moduli di dimensioni variabili ispirato all'Apple Keynote 2023 — consolidato come standard 2026 per feature page e dashboard. Ogni cella ha dimensioni diverse ma si inscrive in una griglia armoniosa.

**Snippet minimo funzionante:**
```css
.bento {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 200px;
  gap: 1rem;
}

.bento-item { border-radius: 1rem; overflow: hidden; }
.bento-wide  { grid-column: span 2; }
.bento-tall  { grid-row: span 2; }
.bento-large { grid-column: span 2; grid-row: span 2; }

/* Responsive */
@media (max-width: 768px) {
  .bento { grid-template-columns: repeat(2, 1fr); }
  .bento-wide, .bento-large { grid-column: span 2; }
}
```

```html
<div class="bento">
  <div class="bento-item bento-large">Feature principale</div>
  <div class="bento-item bento-wide">Feature secondaria</div>
  <div class="bento-item">Stat</div>
  <div class="bento-item">Stat</div>
  <div class="bento-item bento-tall">Feature verticale</div>
</div>
```

**Quando usarlo:** Feature page SaaS, about page con statistiche, portfolio fotografico, dashboard con KPI.

---

## [Variable Fonts & Tipografia Cinetica](https://elements.envato.com/learn/web-design-trends)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅

I variable font (un singolo file con infiniti pesi/larghezze) sono il cornerstone tipografico del 2026. Combinati con animazioni CSS o scroll, creano tipografia cinetica che si deforma, ruota o reagisce al cursore.

**Snippet minimo funzionante:**
```css
/* Variable font con animazione peso */
@import url('https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,100..900;1,9..144,100..900&display=swap');

.variable-heading {
  font-family: 'Fraunces', serif;
  font-variation-settings: 'wght' 300, 'opsz' 9;
  transition: font-variation-settings 0.4s ease;
}

.variable-heading:hover {
  font-variation-settings: 'wght' 900, 'opsz' 144;
}

/* Titolo che si deforma sullo scroll con @property */
@property --font-weight {
  syntax: '<number>';
  initial-value: 100;
  inherits: false;
}

.kinetic-title {
  font-weight: var(--font-weight);
  animation: weight-morph linear;
  animation-timeline: scroll(root);
}

@keyframes weight-morph {
  from { --font-weight: 100 }
  to   { --font-weight: 900 }
}
```

**Quando usarlo:** Hero heading, titoli sezione, pull quote. Performance bonus: un variable font sostituisce 6-8 file statici riducendo le richieste HTTP.

---

## [Palette Colori 2026 — Neutri Caldi e Accenti Elettrici](https://www.wearetg.com/?p=14146)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Universale

Tendenza 2026: abbandono del bianco puro in favore di **neutri "non sbiancati"** (off-white, crema, sabbia), accenti elettrici (teal, indigo, lime acido), e accenti profondi (prugna, terra, verde fumo). I gradienti sono tornati come strumento di profondità.

**Snippet minimo funzionante:**
```css
:root {
  /* Neutri caldi 2026 */
  --bg-primary:   #F7F3EF; /* off-white caldo */
  --bg-secondary: #EDE8E0; /* sabbia */
  --text-primary: #1A1714; /* quasi-nero caldo */
  --text-muted:   #6B6460;

  /* Accenti elettrici */
  --accent-teal:  #0D9488;
  --accent-indigo:#6366F1;
  --accent-lime:  #84CC16;

  /* Accenti profondi */
  --deep-plum:    #581C87;
  --smoky-green:  #365314;
  --earthy-red:   #7C2D12;

  /* Gradiente hero */
  --gradient-hero: linear-gradient(
    135deg,
    #667eea 0%,
    #764ba2 100%
  );
}

body {
  background: var(--bg-primary);
  color: var(--text-primary);
}
```

**Quando usarlo:** Come base per qualsiasi design system 2026. Sostituisce white (#fff) con off-white e black (#000) con quasi-nero per un look più sofisticato e leggibile.
