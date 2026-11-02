# CSS Avanzato, Animazioni ed Effetti Visivi — Novembre 2026

## [CSS Scroll-Driven Animations](https://developer.chrome.com/blog/scroll-triggered-animations)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Safari 26 (Firefox: flag)

Anima elementi in base alla posizione di scroll senza una riga di JavaScript. Con `animation-timeline: scroll()` o `view()` leghi l'avanzamento dell'animazione allo scroll della pagina. Safari 26 aggiunge finalmente supporto stabile; Firefox rimane dietro flag.

**Snippet minimo funzionante:**
```css
@keyframes fade-in {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}

.card {
  animation: fade-in linear both;
  animation-timeline: view();
  animation-range: entry 10% entry 50%;
}
```

**Quando usarlo:** landing page con sezioni che appaiono durante lo scroll, progress bar di lettura, parallax leggero senza dipendenze JS.

---

## [CSS @property — Proprietà Tipizzate e Animabili](https://moderncss.dev/providing-type-definitions-for-css-with-at-property/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Firefox 128+/Safari

Registra una custom property con tipo e valore iniziale, rendendola interpolabile. Il browser sa come animare da un colore a un altro o da un angolo a un altro — cosa impossibile con variabili CSS non tipizzate.

**Snippet minimo funzionante:**
```css
@property --gradient-angle {
  syntax: '<angle>';
  initial-value: 0deg;
  inherits: false;
}

@keyframes spin-gradient {
  to { --gradient-angle: 360deg; }
}

.hero {
  background: conic-gradient(from var(--gradient-angle), #6366f1, #ec4899, #6366f1);
  animation: spin-gradient 4s linear infinite;
}
```

**Quando usarlo:** gradienti animati, contatori CSS animati, transizioni di colore fluide senza JS.

---

## [CSS Carousels Nativi — ::scroll-button e ::scroll-marker](https://www.sitepoint.com/scrolldriven-css-in-2026-building-carousels-without-javascript/)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome (sperimentale)

La spec CSS Overflow Level 5 introduce pseudo-elementi per costruire carousel completamente in CSS: `::scroll-button()` per i controlli avanti/indietro e `::scroll-marker` per i pallini di navigazione.

**Snippet minimo funzionante:**
```css
.carousel {
  overflow-x: auto;
  scroll-snap-type: x mandatory;

  &::scroll-button(right) {
    content: '›';
  }
  &::scroll-button(left) {
    content: '‹';
  }
}

.slide {
  scroll-snap-align: start;

  &::scroll-marker {
    content: '';
    width: 8px; height: 8px;
    border-radius: 50%;
    background: #ccc;
  }

  &::scroll-marker:target-current {
    background: #6366f1;
  }
}
```

**Quando usarlo:** gallery di immagini, slider di card, hero con diapositive — senza librerie JS.

---

## [Glassmorphism con backdrop-filter](https://theplusaddons.com/blog/glassmorphism/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Safari/Firefox

L'effetto vetro smerigliato torna forte nel 2026, in particolare abbinato al Liquid Glass di Apple. Quattro ingredienti: blur, sfondo traslucido, bordo luminoso leggero, ombra morbida.

**Snippet minimo funzionante:**
```css
.glass-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(12px) saturate(1.8);
  -webkit-backdrop-filter: blur(12px) saturate(1.8);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12);
}
```

**Quando usarlo:** modali, sidebar, header che galleggiano su sfondi con gradienti o foto. Da evitare su sfondo piatto (l'effetto non si vede).

---

## [Micro-interazioni CSS con @starting-style](https://blog.nashtechglobal.com/enhancing-user-experience-with-micro-interactions-in-css/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Safari (Newly Available da agosto 2024)

`@starting-style` permette animazioni di entrata su elementi che appaiono nel DOM senza JS. Combinato con `prefers-reduced-motion` per rispettare le preferenze di accessibilità.

**Snippet minimo funzionante:**
```css
/* Bottone con ripple e animazione di entrata */
.btn {
  position: relative;
  overflow: hidden;
  transition: transform 0.15s ease, background 0.2s ease;
}

.btn:active {
  transform: scale(0.97);
}

/* Elemento che entra nel DOM */
.toast {
  transition: opacity 0.3s ease, transform 0.3s ease;

  @starting-style {
    opacity: 0;
    transform: translateY(-10px);
  }
}

@media (prefers-reduced-motion: reduce) {
  .toast { transition: none; }
}
```

**Quando usarlo:** toast, dropdown, popover, dialog — animazione di entrata nativa senza framer-motion o JS.
