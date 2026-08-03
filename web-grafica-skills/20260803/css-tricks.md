# CSS Tricks & Effetti Visivi — Aggiornamento 20260803

## [CSS Scroll-Driven Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_scroll-driven_animations)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome 115+ / Firefox 132+ / Safari 18+ / Edge 115+

Animazioni CSS legate allo scroll senza una riga di JavaScript. Il browser aggiorna i valori sul compositor thread, rendendole fluide anche con il main thread occupato. Supporto globale ~84% a metà 2026.

**Snippet minimo funzionante:**
```css
/* Barra di progresso scroll */
@keyframes progress-grow {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}

.progress-bar {
  position: fixed;
  top: 0; left: 0;
  height: 4px;
  background: #6366f1;
  transform-origin: left;
  animation: progress-grow linear;
  animation-timeline: scroll(root);
}

/* Fade-in on scroll (view timeline) */
.card {
  animation: fade-in linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 30%;
}

@keyframes fade-in {
  from { opacity: 0; translate: 0 40px; }
  to   { opacity: 1; translate: 0 0; }
}
```

**Quando usarlo:** Barre di progresso lettura, parallax, reveal-on-scroll, sticky headers animati. Sostituisce ScrollMagic e AOS senza dipendenze.

---

## [CSS @property — Custom Properties con Tipo](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@property)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome 85+ / Firefox 128+ / Safari 16.4+ / Edge 85+

Aggiunge un sistema di tipi alle variabili CSS: il browser sa che `--angle` è un `<angle>`, quindi può interpolarlo nelle animazioni. In 2026 ha supporto universale e permette gradient transition e token scoped senza hack.

**Snippet minimo funzionante:**
```css
/* Gradiente animato senza JavaScript */
@property --angle {
  syntax: '<angle>';
  initial-value: 0deg;
  inherits: false;
}

@property --color-stop {
  syntax: '<color>';
  initial-value: #6366f1;
  inherits: false;
}

.animated-border {
  --angle: 0deg;
  background: conic-gradient(from var(--angle), #6366f1, #ec4899, #f59e0b, #6366f1);
  animation: rotate-gradient 3s linear infinite;
}

@keyframes rotate-gradient {
  to { --angle: 360deg; }
}

/* Token scoped: non eredita nei figli */
@property --card-bg {
  syntax: '<color>';
  initial-value: white;
  inherits: false;
}
```

**Quando usarlo:** Bordi animati con conic-gradient, transizioni tra colori di design token, animazione di gradienti complessi senza pseudo-elementi.

---

## [Glassmorphism 2.0](https://weblogtrips.com/technology/glassmorphism-2-0-css-techniques-2026/)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome / Firefox / Safari / Edge (tutti)

Il "vetro smerigliato" CSS è ancora vivissimo nel 2026, ma usato come accento (card, badge, nav) su sfondi controllati piuttosto che come fondamento dell'intera UI. L'accessibilità si gestisce rilevando `prefers-reduced-transparency` e rimuovendo il blur.

**Snippet minimo funzionante:**
```css
.glass-card {
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow:
    0 4px 24px rgba(0, 0, 0, 0.12),
    inset 0 1px 0 rgba(255, 255, 255, 0.4);
}

/* Accessibilità: rimuovi blur per chi lo richiede */
@media (prefers-reduced-transparency: reduce) {
  .glass-card {
    background: rgba(30, 30, 40, 0.9);
    backdrop-filter: none;
  }
}
```

**Quando usarlo:** Card hero, modal overlay, navigation bar su sfondi colorati/fotografici. Regola 70/30: 70% flat o glass, 30% neumorphic al massimo.

---

## [Micro-interactions con @starting-style](https://medium.com/@alexdev82/css-micro-animations-in-2026-7-pure-css-techniques-that-replace-javascript-efd374b6e8a4)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐ (3/5) | **Browser:** Chrome 117+ / Firefox 129+ / Safari 17.5+

`@starting-style` definisce lo stile iniziale prima del primo render, permettendo animazioni di entrata su elementi che appaiono nel DOM senza JavaScript. Combinato con `transition`, crea micro-interazioni fluide che durano 150–250ms.

**Snippet minimo funzionante:**
```css
/* Bottone con feedback tattile */
.btn {
  padding: 0.6em 1.4em;
  background: #6366f1;
  color: white;
  border-radius: 8px;
  transition: transform 150ms ease, box-shadow 150ms ease;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(99, 102, 241, 0.4);
}

.btn:active {
  transform: translateY(0);
  box-shadow: none;
}

/* Animazione entrata dialog con @starting-style */
dialog {
  opacity: 1;
  translate: 0 0;
  transition: opacity 200ms, translate 200ms, display 200ms allow-discrete;
}

@starting-style {
  dialog[open] {
    opacity: 0;
    translate: 0 20px;
  }
}
```

**Quando usarlo:** Animazioni entrata/uscita di dialog, dropdown, tooltip. Zero JS per feedback hover/active su bottoni e form.

---

## [CSS scroll-triggered Animations (Chrome 145)](https://developer.chrome.com/blog/scroll-triggered-animations)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome 145+ (in rollout 2026)

Animazioni che si *triggherano* (partono una volta) quando l'elemento entra nella viewport, distinte da quelle legate continuamente allo scroll. Sono time-based ma attivate da un offset di scroll specifico.

**Snippet minimo funzionante:**
```css
.hero-title {
  animation: slide-up 0.6s cubic-bezier(0.16, 1, 0.3, 1) both paused;
  animation-timeline: view();
  /* Trigger al 10% dell'entrata in viewport */
  animation-range: entry 10%;
}

@keyframes slide-up {
  from {
    opacity: 0;
    transform: translateY(60px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

**Quando usarlo:** Landing page con sezioni animate al primo scroll, storytelling sequenziale, animazioni one-shot su elementi importanti.
