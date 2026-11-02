# Design Trends e Componenti UI — Novembre 2026

## [Tailwind CSS v4.3 — Scrollbar, Container Height, Zoom](https://tailwindcss.com/blog/tailwindcss-v4-3)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

v4.3 (maggio 2026) porta utilità native per scrollbar, il nuovo `@container-size` per container query su altezza, e le utilities `zoom-*`. L'architettura CSS-first di v4 elimina `tailwind.config.js`: tutto si configura via `@theme` nel CSS.

**Snippet — Scrollbar custom:**
```css
/* tailwind.config via @theme */
@import "tailwindcss";

@theme {
  --color-primary: #6366f1;
}
```

```html
<!-- Scrollbar stilizzata -->
<div class="overflow-y-auto scrollbar scrollbar-thin scrollbar-thumb-primary scrollbar-track-transparent h-64">
  <!-- contenuto lungo -->
</div>

<!-- Container query su altezza (novità v4.3) -->
<div class="@container">
  <div class="@[200px_height]:hidden text-sm">
    Visibile solo se il container è alto almeno 200px
  </div>
</div>
```

**Quando usarlo:** qualsiasi nuovo progetto React/Next.js/Astro nel 2026. La v4 è lo standard de facto.

---

## [shadcn/ui — Base UI come Default + React Aria](https://ui.shadcn.com)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Da luglio 2026 Base UI sostituisce Radix come libreria predefinita in shadcn/ui, pur mantenendo pieno supporto per entrambe. React Aria aggiunto come terza opzione. CLI v4 permette di scegliere la base con `--base radix|base|aria`.

**Snippet — Init con scelta della base:**
```bash
# Nuovo progetto con Base UI (default)
pnpm dlx shadcn@latest init

# Mantenere Radix su progetto esistente
pnpm dlx shadcn@latest init -b radix

# Migrare da @radix-ui/* singoli al pacchetto unificato
npx shadcn@latest migrate radix
```

**Import aggiornato (da v4.2):**
```ts
// Prima
import * as Dialog from "@radix-ui/react-dialog";

// Adesso (unified package)
import { Dialog } from "radix-ui";
```

**Quando usarlo:** tutti i nuovi progetti con design system — shadcn rimane lo standard per componenti React accessibili e customizzabili.

---

## [Brutalism Digitale / Anti-Soft UI](https://fireart.studio/blog/the-best-web-design-trends/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

I siti premium si allontanano da blur e ombre morbide verso geometria netta, bordi da 1px e layout non convenzionali. Il movimento "broken grid" rompe deliberatamente le griglie regolari per creare tensione visiva. Tipografia in sovrimpressione.

**Snippet — Card brutalist:**
```css
.card-brutal {
  background: #fff;
  border: 2px solid #000;
  box-shadow: 4px 4px 0px #000;
  border-radius: 0;
  transition: box-shadow 0.15s ease, transform 0.15s ease;
}

.card-brutal:hover {
  box-shadow: 6px 6px 0px #6366f1;
  transform: translate(-2px, -2px);
}
```

**Quando usarlo:** portfolio creativi, brand giovani/tech, siti artistici, startup che vogliono distinguersi dal look "corporate soft".

---

## [Variable Fonts — Performance e Espressività](https://blog.openreplay.com/web-typography--the-impact-of-variable-fonts/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Un singolo file `.woff2` sostituisce tutti i pesi e stili del font, migliorando drasticamente i Core Web Vitals. CSS `font-variation-settings` o le nuove proprietà ad alto livello (`font-weight`, `font-stretch`) controllano l'interpolazione continua.

**Snippet — Variable font con animazione:**
```css
@font-face {
  font-family: "InterVariable";
  src: url("inter-variable.woff2") format("woff2-variations");
  font-weight: 100 900;
  font-display: swap;
}

.headline {
  font-family: "InterVariable", sans-serif;
  font-weight: 400;
  transition: font-weight 0.3s ease;
}

.headline:hover {
  font-weight: 800; /* Interpolazione fluida senza caricare un altro file */
}
```

**Quando usarlo:** sempre — preferire variable fonts su qualsiasi font con più pesi. Google Fonts 2026 ne offre centinaia gratis in formato variabile.

---

## [Kinetic Typography — Testo come Elemento Visivo](https://elements.envato.com/learn/web-design-trends)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Il testo in movimento è il trend dominante 2026: headline che scorrono in marquee, parole che si rivelano lettera per lettera, testo che cambia con lo scroll. Combinato con `font-size: clamp()` e viewport units.

**Snippet — Testo in marquee CSS puro:**
```css
.marquee-track {
  display: flex;
  overflow: hidden;
  user-select: none;
}

.marquee-content {
  display: flex;
  gap: 2rem;
  animation: marquee 20s linear infinite;
  white-space: nowrap;
}

@keyframes marquee {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}
```

**Snippet — Fluid typography:**
```css
h1 {
  font-size: clamp(2rem, 5vw + 1rem, 8rem);
  line-height: 1.1;
  letter-spacing: -0.02em;
}
```

**Quando usarlo:** hero section, sezioni di quote, separatori di sezione su siti portfolio e brand.

---

## [Bento Grid Layout](https://graphicdesignjunction.com/2025/12/web-design-trends-of-2026/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Layout ispirato all'interfaccia di Apple con card di dimensioni diverse su una griglia CSS. Ogni cella ha proporzioni diverse e mostra una feature distinta. Molto usato per sezioni "features" di SaaS.

**Snippet — Bento Grid CSS:**
```css
.bento {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto;
  gap: 1rem;
}

.bento-wide  { grid-column: span 2; }
.bento-tall  { grid-row: span 2; }
.bento-large { grid-column: span 2; grid-row: span 2; }
```

```html
<div class="bento">
  <div class="bento-card bento-large">Feature principale</div>
  <div class="bento-card">Feature 2</div>
  <div class="bento-card bento-tall">Feature 3</div>
  <div class="bento-card">Feature 4</div>
  <div class="bento-card">Feature 5</div>
</div>
```

**Quando usarlo:** sezioni feature/pricing di SaaS, portfolio con lavori eterogenei, dashboard informative.
