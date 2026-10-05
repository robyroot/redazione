# CSS Avanzato & Animazioni — Settimana 20261005

## [CSS Scroll-Driven Animations](https://csstools.io/blog/css-scroll-driven-animations)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome 115+ / Firefox 126+ / Safari 17.2+ / Edge 115+

Animazioni legate allo scroll completamente native in CSS, senza JavaScript. Baseline 2026 su tutti i browser principali, eseguono sul compositor thread per performance ottimali.

**Snippet minimo funzionante:**
```css
/* Fade-in on scroll con view() timeline */
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(40px); }
  to   { opacity: 1; transform: translateY(0); }
}

.card {
  animation: fadeInUp linear;
  animation-timeline: view();
  animation-range: entry 0% entry 40%;
}
```

**Quando usarlo:** Reveal di sezioni, parallax leggero, progress bar di lettura, caroselli senza JS.

---

## [CSS Liquid Glass / Glassmorphism](https://glasscss.com/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome / Safari / Edge (Firefox parziale)

Effetto vetro liquido con profondità fisica, refrazione e riflessi. Apple lo ha adottato come linguaggio visivo principale nel 2025–2026, ora è il trend dominante per card, modal e navbar.

**Snippet minimo funzionante:**
```css
.glass-card {
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow:
    0 4px 24px rgba(0, 0, 0, 0.15),
    inset 0 1px 0 rgba(255, 255, 255, 0.4);
}

/* Versione avanzata con distorsione liquida SVG */
.liquid-glass {
  filter: url(#liquid-distort);
}
```

```html
<!-- SVG filter per distorsione organica -->
<svg style="position:absolute;width:0;height:0">
  <filter id="liquid-distort">
    <feTurbulence type="fractalNoise" baseFrequency="0.65" numOctaves="3" seed="2"/>
    <feDisplacementMap in="SourceGraphic" scale="8"/>
  </filter>
</svg>
```

**Quando usarlo:** Hero sections, card prodotti, modal overlay, navbar floating su immagini o gradienti vivaci.

---

## [CSS @property — Custom Properties Animabili](https://dev.to/jh3y/css-animation-superpowers-with-property-5cc)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti i browser moderni (universale nel 2026)

Permette di registrare custom property con tipo, valore iniziale e regola di ereditarietà, rendendole animabili. Sblocca animazioni di gradienti, rotazioni, colori HSL che con le `--var` normali non erano possibili.

**Snippet minimo funzionante:**
```css
/* Registra la custom property come angolo animabile */
@property --gradient-angle {
  syntax: "<angle>";
  initial-value: 0deg;
  inherits: false;
}

.gradient-border {
  --gradient-angle: 0deg;
  background: linear-gradient(var(--gradient-angle), #6366f1, #ec4899, #f59e0b);
  animation: spin-gradient 4s linear infinite;
}

@keyframes spin-gradient {
  to { --gradient-angle: 360deg; }
}

/* Animazione colore HSL */
@property --hue {
  syntax: "<number>";
  initial-value: 0;
  inherits: false;
}

.color-cycle {
  --hue: 0;
  background: hsl(var(--hue), 80%, 60%);
  animation: cycle-hue 3s linear infinite;
}

@keyframes cycle-hue {
  to { --hue: 360; }
}
```

**Quando usarlo:** Bordi con gradiente animato, background color shift, progress indicator con colore dinamico, effetti aurora.

---

## [CSS Scroll-Marker & Carousel Nativo](https://www.sitepoint.com/scrolldriven-css-in-2026-building-carousels-without-javascript/)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome 135+ (in arrivo su altri)

CSS Overflow Level 5 introduce `::scroll-button()` e `::scroll-marker()` per creare caroselli e slider completamente in CSS, senza una riga di JavaScript.

**Snippet minimo funzionante:**
```css
.carousel {
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  display: flex;
  gap: 16px;
}

.carousel::scroll-button(inline-start),
.carousel::scroll-button(inline-end) {
  content: "›";
  font-size: 2rem;
  cursor: pointer;
  background: rgba(255,255,255,0.8);
  border-radius: 50%;
  width: 40px;
  height: 40px;
}

.carousel-item {
  scroll-snap-align: start;
  flex: 0 0 300px;
}

/* Indicatori di posizione */
.carousel::scroll-marker-group {
  display: flex;
  gap: 8px;
  justify-content: center;
}

.carousel-item::scroll-marker {
  content: "";
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #ccc;
}

.carousel-item::scroll-marker:target-current {
  background: #6366f1;
}
```

**Quando usarlo:** Gallerie foto, card prodotti in slider, testimonial, qualsiasi slideshow che prima richiedeva librerie JS.
