# Design Trends & Componenti UI — Settimana 20261019

## [Tailwind CSS v4.x](https://tailwindcss.com)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

Tailwind v4 (2025) ha completamente rimpiazzato il file config JS con un sistema `@theme` in CSS. L'engine Oxide (basato su Lightning CSS) è 5-10× più veloce su build completa, 100× sugli incrementali. La v4.3 (giugno 2026) aggiunge nuove palette colori (mauve, olive, mist, taupe) e utility per scrollbar.

**Snippet minimo — tema personalizzato:**
```css
@import "tailwindcss";

@theme {
  --color-brand: oklch(55% 0.2 250);
  --color-brand-light: oklch(75% 0.15 250);
  --font-display: "Inter Variable", sans-serif;
  --spacing-section: 5rem;
}
```

```html
<!-- Container query nativa (no plugin) -->
<div class="@container">
  <div class="@md:grid @md:grid-cols-2 p-[spacing-section]">...</div>
</div>
```

**Quando usarlo:** Qualsiasi nuovo progetto web. La migrazione da v3 è ben documentata e vale il tempo.

---

## [Liquid Glass UI](https://theplusaddons.com/blog/liquid-glass-ui/)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge (fallback su Safari/Firefox)

Il trend UI del 2026 per eccellenza: superfici translucide con vera rifrazione del contenuto sottostante, ispirata al redesign Apple WWDC25. Evoluzione matura del glassmorphism, con edge highlight e profondità.

**Snippet card componente:**
```css
.liquid-glass-card {
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(16px) saturate(1.8) brightness(1.05);
  -webkit-backdrop-filter: blur(16px) saturate(1.8) brightness(1.05);
  border: 1px solid rgba(255, 255, 255, 0.25);
  box-shadow: 
    inset 0 1px 0 rgba(255, 255, 255, 0.6),
    inset 0 -1px 0 rgba(0, 0, 0, 0.08),
    0 8px 32px rgba(0, 0, 0, 0.12);
  border-radius: 20px;
  padding: 24px;
}
```

**Quando usarlo:** Navigation floating, modal overlay, card su sfondi ricchi di colore o fotografie.

---

## [Bento Box Layout](https://musemind.agency/blog/ui-design-trends)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

Il layout modulare a blocchi di dimensioni diverse. Ogni blocco ha contenuto diverso (KPI, grafico, testo, immagine) ma fa parte di una griglia coerente. Adottato massicciamente per dashboard, feature sections, pricing.

**Snippet CSS Grid bento:**
```css
.bento-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
}

.bento-hero  { grid-column: span 2; grid-row: span 2; }
.bento-small { grid-column: span 1; }
.bento-wide  { grid-column: span 3; }
.bento-tall  { grid-column: span 1; grid-row: span 2; }
```

**Quando usarlo:** Feature sections di SaaS, portfolio, dashboard, pricing tables con visual emphasis variabile.

---

## [Tactile Brutalism](https://fireart.studio/blog/the-best-web-design-trends/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

Counter-trend 2026: geometria netta, bordi `1px solid`, ombre solide offset (senza blur), tipografia massiccia. Un antidoto al minimalismo anonimo — comunicano autenticità e personalità.

**Snippet card brutalista:**
```css
.brutal-card {
  background: #fff;
  border: 2px solid #000;
  box-shadow: 4px 4px 0 #000;
  border-radius: 0;
  padding: 24px;
  transition: transform 0.1s, box-shadow 0.1s;
}

.brutal-card:hover {
  transform: translate(-2px, -2px);
  box-shadow: 6px 6px 0 #000;
}

.brutal-button {
  background: #f0ff44;
  border: 2px solid #000;
  box-shadow: 3px 3px 0 #000;
  font-weight: 900;
  text-transform: uppercase;
  padding: 12px 24px;
}
```

**Quando usarlo:** Brand con personalità forte, portfolio creativi, startup che vogliono distinguersi dal minimal omogeneo.

---

## [Command Palette Component](https://www.gleamstudio.design/blog-post/ui-design-trends-2026)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

Le command palette (⌘K) sono diventate un pattern standard per SaaS e dev tools nel 2026. Permettono navigazione power-user, ricerca globale, azioni rapide — tutto da tastiera.

**Snippet con cmdk (React):**
```jsx
import { Command } from 'cmdk';

function CommandMenu() {
  return (
    <Command.Dialog open={open} onOpenChange={setOpen}>
      <Command.Input placeholder="Cerca o inserisci un comando..." />
      <Command.List>
        <Command.Group heading="Pagine">
          <Command.Item onSelect={() => navigate('/dashboard')}>Dashboard</Command.Item>
          <Command.Item onSelect={() => navigate('/settings')}>Impostazioni</Command.Item>
        </Command.Group>
      </Command.List>
    </Command.Dialog>
  );
}
```

**Quando usarlo:** SaaS con molte funzioni, tool per developer, dashboard con navigazione complessa.

---

## [Motion come linguaggio funzionale](https://tubikstudio.com/blog/ui-design-trends-2026)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

Nel 2026 la motion design non è più decorazione ma linguaggio UI primario: comunica stato, guida l'attenzione, conferma azioni. Principi: velocità (150-300ms), easing naturale, direzione coerente.

**Snippet sistema easing CSS:**
```css
:root {
  --ease-out: cubic-bezier(0.0, 0, 0.2, 1);
  --ease-in: cubic-bezier(0.4, 0, 1, 1);
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
}

.interactive {
  transition: transform 200ms var(--ease-out),
              box-shadow 200ms var(--ease-out);
}

.interactive:hover  { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(0,0,0,0.15); }
.interactive:active { transform: translateY(0); transition-duration: 80ms; }
```

**Quando usarlo:** Ovunque — ogni elemento interattivo dovrebbe avere feedback visivo appropriato per comunicare chiaramente lo stato.
