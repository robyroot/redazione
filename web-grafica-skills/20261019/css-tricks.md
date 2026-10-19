# CSS Tricks & Animazioni Avanzate — Settimana 20261019

## [CSS Scroll-Triggered Animations](https://developer.chrome.com/blog/scroll-triggered-animations)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome 146+

Nuova proprietà `animation-trigger` che lancia animazioni temporali (non legate allo scroll progress) quando un elemento entra nel viewport. Differente dalle scroll-driven animations: qui l'animazione si avvia una volta sola, con durata fissa.

**Snippet minimo funzionante:**
```css
.card {
  animation: fadeSlideIn 0.6s ease forwards paused;
  animation-trigger: view();
}

@keyframes fadeSlideIn {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

**Quando usarlo:** Animazioni di entrata su card, sezioni hero, liste di prodotti — senza JavaScript.

---

## [CSS Scroll-Driven Animations (animation-timeline)](https://www.joshwcomeau.com/animation/scroll-driven-animations/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge (Firefox con flag)

Mappa il progresso dello scroll a qualsiasi proprietà CSS animabile. Supporta `scroll()` per lo scrollbar globale e `view()` per la posizione relativa al viewport. Nel 2026 ha raggiunto ~90% di copertura browser.

**Snippet minimo funzionante:**
```css
@keyframes grow-progress {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}

.progress-bar {
  animation: grow-progress auto linear;
  animation-timeline: scroll();
  transform-origin: left;
}
```

**Quando usarlo:** Barre di progresso lettura, parallax leggero, reveal di elementi basato sullo scroll senza GSAP.

---

## [CSS @property — Animare Gradienti e Valori Tipizzati](https://smashingmagazine.com/2024/05/times-need-custom-property-instead-css-variable/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge (baseline 2024)

Registra custom properties con un tipo esplicito (`<color>`, `<angle>`, `<percentage>`) così il browser può interpolarle. Permette di animare gradienti, clip-path e qualsiasi valore che i CSS variables normali non interpolano.

**Snippet minimo funzionante:**
```css
@property --hue {
  syntax: '<number>';
  initial-value: 0;
  inherits: false;
}

.rainbow-text {
  animation: spin-hue 3s linear infinite;
  color: hsl(var(--hue), 80%, 50%);
}

@keyframes spin-hue {
  to { --hue: 360; }
}
```

**Quando usarlo:** Pulsanti con luce rotante, testi arcobaleno, transizioni di gradienti complesse senza JavaScript.

---

## [Liquid Glass Effect (CSS + SVG Filter)](https://www.cssscript.com/liquid-glass-ios-refraction/)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge (fallback blur su Safari/Firefox)

Evoluzione del glassmorphism: usa `backdrop-filter` + filtri SVG con `feTurbulence` + `feDisplacementMap` per creare una vera rifrazione del contenuto sottostante, ispirata al design liquid glass di Apple WWDC25.

**Snippet minimo funzionante:**
```html
<svg style="position:absolute;width:0;height:0">
  <defs>
    <filter id="glass-filter">
      <feTurbulence type="fractalNoise" baseFrequency="0.015" numOctaves="3" result="noise"/>
      <feGaussianBlur stdDeviation="3" in="noise" result="blurNoise"/>
      <feDisplacementMap in="SourceGraphic" in2="blurNoise" scale="18" xChannelSelector="R" yChannelSelector="G"/>
    </filter>
  </defs>
</svg>

<div class="glass-card">Contenuto</div>
```
```css
.glass-card {
  backdrop-filter: blur(12px) brightness(1.1);
  filter: url(#glass-filter);
  background: rgba(255,255,255,0.15);
  border: 1px solid rgba(255,255,255,0.3);
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.85), 0 8px 32px rgba(0,0,0,0.15);
  border-radius: 20px;
}

@media (prefers-reduced-transparency: reduce) {
  .glass-card { backdrop-filter: none; background: rgba(240,240,240,0.95); }
}
```

**Quando usarlo:** Modali, toast, navigation bar floating — dove si vuole l'effetto premium vetro liquido di iOS/macOS.

---

## [CSS Corner-Shape Animata](https://css-tricks.com/experimenting-with-scroll-driven-corner-shape-animations/)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome only (sperimentale)

La proprietà `corner-shape` (Chrome experimental) permette angoli a squircle, notched, bevel, round. Combinata con scroll-driven animations permette di morphare la forma dei contenitori allo scroll.

**Snippet minimo funzionante:**
```css
@property --corner {
  syntax: '<number>';
  initial-value: 0;
  inherits: false;
}

.morphing-box {
  corner-shape: squircle;
  border-radius: calc(var(--corner) * 1%);
  animation: morph-corners auto linear;
  animation-timeline: scroll();
}

@keyframes morph-corners {
  from { --corner: 5; }
  to   { --corner: 50; }
}
```

**Quando usarlo:** Effetti sperimentali e cutting-edge per siti portfolio, non ancora per produzione cross-browser.
