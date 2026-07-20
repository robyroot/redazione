# CSS Tricks & Tecniche Avanzate — Settimana 20260720

## [CSS Scroll-Triggered Animations](https://www.frontendhorizon.com/blog/view-transitions-api-and-css-scroll-driven-animations-the-browser-wins-of-2026)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Safari 17+ (Firefox flag)

Animazioni che si attivano al passaggio dello scroll senza una riga di JavaScript. Chrome 145 ha introdotto le scroll-triggered animations: diversamente dalle scroll-driven (che avanzano in proporzione allo scroll), queste si attivano come normali animazioni CSS quando un elemento entra nel viewport. Addio IntersectionObserver.

**Snippet minimo funzionante:**
```css
@keyframes slide-in {
  from { opacity: 0; translate: 0 40px; }
  to   { opacity: 1; translate: 0 0; }
}

.card {
  animation: slide-in 0.6s ease both;
  animation-timeline: scroll();
  animation-range: entry 0% entry 30%;
}
```

**Quando usarlo:** Rivelazioni di sezioni, liste di feature, portfolio item che appaiono allo scroll — tutto senza dipendenze JS.

---

## [CSS @property — Animated Gradients & Design Tokens](https://www.giorgiosaud.io/notebook/css-custom-properties-2026)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Safari/Firefox (supporto universale 2026)

`@property` dà un tipo alle variabili CSS (color, angle, length) rendendole interpolabili dal browser. Risultato: gradienti animati, border rotanti, token di design scoped — tutto in CSS puro, offloading sulla GPU.

**Snippet minimo funzionante:**
```css
/* Gradient border rotante */
@property --angle {
  syntax: '<angle>';
  initial-value: 0deg;
  inherits: false;
}

.card {
  background: conic-gradient(from var(--angle), #6366f1, #ec4899, #6366f1);
  animation: spin-gradient 3s linear infinite;
  padding: 2px;
}

@keyframes spin-gradient {
  to { --angle: 360deg; }
}

.card-inner {
  background: #0f172a;
  border-radius: inherit;
}
```

**Quando usarlo:** Border animati su card premium, badge "NEW", pulsanti CTA con effetto aurora. Scoped design tokens per componenti riutilizzabili che non devono ereditare valori dai parent.

---

## [Glassmorphism 2.0 / Liquid Glass](https://weblogtrips.com/technology/glassmorphism-2-0-css-techniques-2026/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Safari (backdrop-filter supportato)

Evoluzione del frosted glass: Glassmorphism 2.0 usa `relative color syntax`, `mask-image` graduati e multi-layer backdrop-filter per simulare la rifrazione della luce. Liquid Glass va oltre aggiungendo reattività dinamica al mouse/gyroscope. Neumorphism invece è in declino e sopravvive solo come texture accent.

**Snippet minimo funzionante:**
```css
.glass-card {
  /* Base trasparenza */
  background: rgba(255, 255, 255, 0.08);

  /* Il "frost" — cuore del glassmorphism */
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);

  /* Bordo luminoso sottile */
  border: 1px solid rgba(255, 255, 255, 0.18);

  /* Ombra per profondità */
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);

  border-radius: 16px;
  padding: 2rem;
}

/* Glassmorphism 2.0: gradiente di opacità sul bordo */
.glass-card-v2 {
  background: rgba(255, 255, 255, 0.06);
  backdrop-filter: blur(20px);
  border: 1px solid transparent;
  background-clip: padding-box;
  mask-image: linear-gradient(135deg, rgba(255,255,255,0.15), rgba(255,255,255,0.03));
}
```

**Quando usarlo:** Header navigazione, modal dialog, card su sfondi con immagini o gradienti. Evitare su sfondi piatti monocromatici (l'effetto non si vede).

---

## [View Transitions API — Micro-Interactions Native](https://dev.to/krish_kakadiya_5f0eaf6342/mastering-smooth-page-transitions-with-the-view-transitions-api-in-2026-31of)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Safari (Firefox in sviluppo)

Due feature native browser hanno sostituito il 90% degli use case delle librerie JS di animazione: View Transitions API e CSS scroll-driven animations. La View Transitions API fa snapshotting del vecchio stato DOM e anima automaticamente verso il nuovo stato. Zero JavaScript per la maggior parte dei pattern, compositing GPU.

**Snippet minimo funzionante:**
```css
/* Il browser gestisce automaticamente il crossfade */
/* Assegna view-transition-name agli elementi da morphare */

.product-card {
  view-transition-name: product-card;
}

.product-detail-image {
  view-transition-name: product-card; /* stesso nome → morph automatico! */
}

/* Personalizza il crossfade default */
::view-transition-old(product-card) {
  animation: fade-out 0.3s ease;
}
::view-transition-new(product-card) {
  animation: fade-in 0.3s ease;
}
```

```javascript
// Triggering lato JS
document.startViewTransition(() => {
  // qualsiasi cambiamento DOM
  updatePageContent();
});
```

**Quando usarlo:** Transizioni pagina in SPA, espansione card → dettaglio, gallery che morphano da thumbnail a fullscreen. Su dispositivi low-end, app percepite 2-3× più veloci rispetto all'equivalente GSAP.
