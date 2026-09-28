# CSS Tricks & Tecniche Avanzate — Settimana 20260928

## [CSS Scroll-Driven Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Scroll-driven_animations)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Anima elementi CSS in base alla posizione di scroll, senza JavaScript. Il supporto è ora universale in tutti i browser moderni e le animazioni su `transform` e `opacity` girano sul compositor thread, garantendo 60fps+ anche su dispositivi mobile di fascia media.

**Snippet minimo funzionante:**
```css
/* Barra di progresso scroll */
@keyframes progress {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}

.progress-bar {
  position: fixed;
  top: 0;
  left: 0;
  height: 4px;
  background: linear-gradient(90deg, #6366f1, #ec4899);
  transform-origin: left;
  animation: progress linear;
  animation-timeline: scroll(root);
}

/* Reveal on scroll con view() */
@keyframes reveal {
  from { opacity: 0; translate: 0 40px; }
  to   { opacity: 1; translate: 0 0; }
}

.card {
  animation: reveal linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 30%;
}
```

**Quando usarlo:** Progress bar di lettura, parallax, reveal-on-scroll, storytelling scrollabile. Sostituisce completamente GSAP ScrollTrigger per casi d'uso semplici.

---

## [CSS @property — Custom Properties Tipizzate](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@property)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Registra custom properties con tipo, valore iniziale e controllo dell'ereditarietà. Il vero vantaggio: le custom properties registrate con `@property` possono essere animate via `transition` e `animation`, sbloccando effetti impossibili con variabili CSS standard (es. transizioni su gradienti).

**Snippet minimo funzionante:**
```css
/* Gradiente animabile via hover */
@property --angle {
  syntax: '<angle>';
  inherits: false;
  initial-value: 0deg;
}

.gradient-border {
  --angle: 0deg;
  border: 4px solid transparent;
  background:
    linear-gradient(white, white) padding-box,
    conic-gradient(from var(--angle), #6366f1, #ec4899, #6366f1) border-box;
  transition: --angle 0.6s ease;
}

.gradient-border:hover {
  --angle: 360deg;
}
```

**Quando usarlo:** Design system con token animabili, bordi gradiente animati, counter CSS, transizioni su colori di sfondo complessi.

---

## [Glassmorphism 2.0 — Liquid Glass](https://www.setproduct.com/blog/liquid-glass-vs-glassmorphism)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Evoluzione del glassmorphism classico: i pannelli vetro reagiscono dinamicamente alla luce e al movimento, simulando rifrazione che cambia al movimento del mouse. Il "Claymorphism" è la variante del neumorphism 2026, con inner glow morbido su sfondo pastello.

**Snippet minimo funzionante:**
```css
/* Glassmorphism classico production-ready */
.glass-card {
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 20px;
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.12),
    inset 0 1px 0 rgba(255, 255, 255, 0.4);
}

/* Claymorphism 2026 */
.clay-card {
  background: #c8d8ff;
  border-radius: 24px;
  box-shadow:
    8px 8px 20px rgba(100, 120, 200, 0.35),
    -4px -4px 12px rgba(255, 255, 255, 0.7),
    inset 2px 2px 6px rgba(255, 255, 255, 0.6),
    inset -2px -2px 6px rgba(100, 120, 200, 0.2);
}
```

**Quando usarlo:** Hero section su sfondi colorati o fotografici, cards overlay, nav glass per app mobile-first. Attenzione al contrasto testo su glassmorphism.

---

## [Micro-Interactions CSS Pure](https://css-tricks.com/a-complete-guide-to-custom-properties/)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Nel 2026 il 75% delle app consumer usa micro-interactions come standard UX. Le 4 più efficaci per conversion rate: state feedback, hover affordance, loading indicator, inline form validation. CSS puro è sempre preferibile a JavaScript per queste animazioni (off main thread, GPU-accelerated).

**Snippet minimo funzionante:**
```css
/* Button con feedback tattile */
.btn {
  background: #6366f1;
  color: white;
  padding: 12px 28px;
  border-radius: 10px;
  border: none;
  cursor: pointer;
  transition: transform 80ms ease, box-shadow 80ms ease, background 200ms ease;
  box-shadow: 0 4px 14px rgba(99, 102, 241, 0.4);
}

.btn:hover {
  box-shadow: 0 6px 20px rgba(99, 102, 241, 0.6);
  background: #4f46e5;
}

.btn:active {
  transform: scale(0.96) translateY(1px);
  box-shadow: 0 2px 8px rgba(99, 102, 241, 0.3);
}

/* Toggle switch animato */
.toggle {
  appearance: none;
  width: 52px;
  height: 28px;
  background: #d1d5db;
  border-radius: 14px;
  position: relative;
  cursor: pointer;
  transition: background 200ms ease;
}

.toggle::after {
  content: '';
  position: absolute;
  top: 3px;
  left: 3px;
  width: 22px;
  height: 22px;
  background: white;
  border-radius: 50%;
  transition: translate 200ms ease, box-shadow 200ms ease;
  box-shadow: 0 2px 6px rgba(0,0,0,0.2);
}

.toggle:checked { background: #6366f1; }
.toggle:checked::after { translate: 24px 0; }
```

**Quando usarlo:** Qualunque elemento interattivo: bottoni, form, toggle, card hover. Priorità al feedback immediato all'azione utente.
