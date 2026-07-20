# Design Trends & Componenti UI — Settimana 20260720

## [Tailwind CSS v4.3 — Oxide Engine + Scrollbar Utilities](https://tailwindcss.com/blog)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Tailwind v4 ha riscritto l'engine in Rust (Oxide), portando build times 10× più veloci. v4.2 (febbraio 2026) ha aggiunto webpack plugin, 4 nuove palette (mauve, olive, mist, taupe) e logical property utilities. v4.3 ha introdotto la suite scrollbar completa nativa. Non si tratta di CSS ordinario: è un sistema di design tokens direttamente nell'HTML.

**Snippet minimo funzionante:**
```html
<!-- Scrollbar personalizzata in Tailwind v4.3 -->
<div class="h-64 overflow-y-auto scrollbar-thin 
            scrollbar-thumb-indigo-500 scrollbar-track-slate-800
            scrollbar-thumb-rounded-full">
  <!-- contenuto scrollabile -->
</div>

<!-- Logical properties per i18n/RTL -->
<div class="pbs-4 pbe-8 mbs-6">
  <!-- pbs = padding-block-start, pbe = padding-block-end -->
  <!-- mbs = margin-block-start → layout RTL-ready -->
</div>

<!-- Container queries (v4 nativo) -->
<div class="@container">
  <div class="@md:grid-cols-2 @lg:grid-cols-3 grid gap-4">
    <!-- si adatta al container, non alla viewport -->
  </div>
</div>

<!-- CSS-first config invece di tailwind.config.js -->
<!-- Nel tuo main.css: -->
@import "tailwindcss";
@theme {
  --color-brand: oklch(60% 0.2 270);
  --font-display: "Cal Sans", sans-serif;
  --radius-card: 1.25rem;
}
```

**Quando usarlo:** Qualsiasi progetto frontend moderno. La CSS-first configuration con `@theme` elimina il file .js di configurazione. Ora è il framework CSS più adottato nel 2026.

---

## [shadcn/ui → Base UI Migration (Luglio 2026)](https://ui.shadcn.com/docs/changelog)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti (React)

Da luglio 2026 shadcn/ui usa **Base UI come default** per i nuovi progetti, mantenendo supporto completo per Radix. Base UI (da MUI) offre componenti headless con migliore performance e API più pulita. La migrazione è progressiva: componente per componente, il progetto rimane funzionante durante il processo.

**Snippet minimo funzionante:**
```bash
# Nuovo progetto con shadcn (Base UI di default da luglio 2026)
npx shadcn@latest init

# Aggiungi componenti
npx shadcn@latest add button card dialog

# Migrazione progressiva da Radix a Base UI
npx shadcn@latest migrate button  # solo il Button, tutto il resto rimane Radix
```

```tsx
// Il codice componente rimane identico — solo l'import primitivo cambia
import { Button } from "@/components/ui/button";

export function Example() {
  return (
    <Button variant="outline" size="sm">
      Click me
    </Button>
  );
}
```

**Quando usarlo:** Design system React aziendale, dashboard admin, SaaS app. Per nuovi progetti partire direttamente con Base UI. Per progetti esistenti, migrare gradualmente durante i normali cicli di sviluppo.

---

## [Tactile Brutalism — Il Nuovo Aesthetic Premium](https://fireart.studio/blog/the-best-web-design-trends/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Il soft UI degli anni 2020-2024 viene sostituito dal **Tactile Brutalism**: bordi netti 1px, geometrie sharp, tipografia stark e contrasto elevato. Non è il brutalism grezzo degli anni '90 — è brutalism eseguito con precisione ingegneristica. I siti premium di agenzie e tech company adottano questo look per comunicare rigore tecnico.

**Snippet minimo funzionante:**
```css
/* Card in stile Tactile Brutalism */
.card-brutalist {
  background: #f5f0e8;      /* off-white, mai puro bianco */
  border: 1px solid #000;   /* bordo netto, non rounded */
  box-shadow: 4px 4px 0 #000;  /* ombra geometrica, signature del trend */
  padding: 1.5rem;
  border-radius: 0;         /* no arrotondamenti */
  transition: transform 0.1s, box-shadow 0.1s;
}

.card-brutalist:hover {
  transform: translate(-2px, -2px);
  box-shadow: 6px 6px 0 #000;
}

/* Tipografia brutalist */
.heading-brutalist {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 800;
  font-size: clamp(2rem, 6vw, 5rem);
  letter-spacing: -0.03em;
  text-transform: uppercase;
  line-height: 0.95;
}

/* Tag / badge */
.badge-brutalist {
  display: inline-block;
  background: #000;
  color: #fff;
  padding: 0.25rem 0.75rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  border: 1px solid #000;
}
```

**Quando usarlo:** Portfolio sviluppatori/designer, siti per tech startup, agenzie creative, SaaS B2B che vogliono comunicare competenza tecnica e serietà. Evitare per brand consumer/lifestyle.

---

## [Bento Grid Layout — Information Dense & Beautiful](https://tubikstudio.com/blog/ui-design-trends-2026/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Il Bento Grid (ispirato ai lunch box giapponesi) organizza contenuti in card modulari asimmetriche con CSS Grid. Permette di presentare informazioni dense senza sovraccarico visivo — Apple, Linear e Vercel lo usano come pattern primario per le feature page.

**Snippet minimo funzionante:**
```html
<div class="bento-grid">
  <div class="bento-card bento-wide">Feature principale</div>
  <div class="bento-card">Stat 1</div>
  <div class="bento-card">Stat 2</div>
  <div class="bento-card bento-tall">Preview</div>
  <div class="bento-card">Feature</div>
</div>
```

```css
.bento-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 200px;
  gap: 1rem;
}

.bento-card {
  background: #0f172a;
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 1.25rem;
  padding: 1.5rem;
  overflow: hidden;
}

.bento-wide  { grid-column: span 2; }
.bento-tall  { grid-row: span 2; }

/* Tailwind equivalente */
/* grid grid-cols-3 auto-rows-[200px] gap-4 */
/* col-span-2 / row-span-2 */
```

**Quando usarlo:** Feature page per SaaS, pricing page, "about" page con statistiche, landing page che devono comunicare valore in modo visivamente ricco. Ottimo su viewport desktop, richiede adattamento mobile attento.

---

## [Variable Fonts — Tipografia Adattiva & Performance](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_fonts/Variable_fonts_guide)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Un Variable Font è un singolo file che contiene tutti i pesi/larghezze/stili, drasticamente più leggero di più file statici. In 2026 sono diventati standard: permetti animazioni tipografiche fluide (peso che cambia su hover), responsive typography, e dark mode con font leggermente più sottili.

**Snippet minimo funzionante:**
```css
/* Importa variable font */
@font-face {
  font-family: 'InterVariable';
  src: url('/fonts/InterVariable.woff2') format('woff2-variations');
  font-weight: 100 900;          /* range supportato */
  font-style: normal;
  font-display: swap;
}

/* Animazione peso su hover */
.nav-link {
  font-family: 'InterVariable', sans-serif;
  font-weight: 400;
  transition: font-weight 0.2s ease;
}
.nav-link:hover { font-weight: 700; }

/* Font responsivo che si adatta */
.heading-responsive {
  font-family: 'InterVariable', sans-serif;
  font-size: clamp(1.5rem, 5vw, 4rem);
  font-weight: clamp(600, calc(600 + (900 - 600) * ((100vw - 320px) / (1200 - 320))), 900);
}

/* Dark mode: peso leggermente più leggero per leggibilità */
@media (prefers-color-scheme: dark) {
  body { font-weight: 350; } /* vs 400 in light mode */
}
```

**Quando usarlo:** Qualsiasi sito con tipografia come elemento di design primario. Google Fonts offre molti variable fonts gratuiti (Inter, Roboto Flex, Outfit). Risparmio medio: 60-80% sul peso font rispetto a caricare 4-5 pesi statici.
