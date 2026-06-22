# CSS Tricks & Animazioni — Settimana 20260622

## [CSS Scroll-Driven Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Scroll-driven_animations)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome 115+ / Edge / Firefox / Safari (parziale)

Animazioni legate al progresso dello scroll o della visibilità di un elemento, zero JavaScript. Chrome 145 ha aggiunto le **scroll-triggered animations**: si attivano quando si supera uno specifico offset, rimpiazzando IntersectionObserver per la maggior parte dei casi. Il compositor thread le gestisce indipendentemente dal main thread — mai un jank.

**Snippet minimo funzionante:**
```css
/* Barra di progresso che cresce con lo scroll */
@keyframes grow-bar {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}
.progress-bar {
  transform-origin: left;
  animation: grow-bar linear both;
  animation-timeline: scroll(root block);
}

/* Reveal on scroll (Chrome 115+) */
.reveal {
  animation: fade-in linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 30%;
}
@keyframes fade-in {
  from { opacity: 0; translate: 0 40px; }
  to   { opacity: 1; translate: 0 0; }
}
```

**Quando usarlo:** Hero parallax, progress bar di lettura, reveal on scroll, sticky header con cambio colore, carousel puro CSS senza JS.

---

## [timeline-scope: Timeline condivisa tra branch DOM diversi](https://developer.chrome.com/blog/scroll-triggered-animations)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome 116+ / Edge

`timeline-scope` espone la scroll/view timeline di un elemento a nodi DOM arbitrari — sblocca composizioni visive impossibili senza JS, come animare il testo hero in risposta allo scroll di una sidebar.

**Snippet minimo funzionante:**
```css
.container {
  timeline-scope: --card-reveal;
}
.sidebar {
  view-timeline: --card-reveal block;
}
.hero-text {
  animation: slide-in linear both;
  animation-timeline: --card-reveal;
  animation-range: entry 0% entry 50%;
}
@keyframes slide-in {
  from { translate: -60px 0; opacity: 0; }
  to   { translate: 0 0; opacity: 1; }
}
```

**Quando usarlo:** Layout complessi dove sidebar e contenuto devono animarsi in sincronia su scroll.

---

## [CSS @property: Animare le Custom Properties](https://css-tricks.com/exploring-property-and-its-animating-powers/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti (supporto universale dal 2026)

`@property` registra una custom property con tipo, valore iniziale ed ereditarietà. Permette al browser di interpolare colori, angoli e percentuali — sblocca transizioni di gradienti e progress bar impossibili con le `var()` classiche.

**Snippet minimo funzionante:**
```css
@property --c1 {
  syntax: '<color>';
  initial-value: #6366f1;
  inherits: false;
}
@property --c2 {
  syntax: '<color>';
  initial-value: #8b5cf6;
  inherits: false;
}

.card {
  background: linear-gradient(135deg, var(--c1), var(--c2));
  transition: --c1 0.6s ease, --c2 0.6s ease;
}
.card:hover {
  --c1: #f59e0b;
  --c2: #ef4444;
}

/* Progress bar animata con percentage tipizzata */
@property --progress {
  syntax: '<percentage>';
  initial-value: 0%;
  inherits: false;
}
.bar {
  background: linear-gradient(to right, #6366f1 var(--progress), #e5e7eb var(--progress));
  animation: fill 2s ease forwards;
}
@keyframes fill { to { --progress: 75%; } }
```

**Quando usarlo:** Hover card con cambio gradiente, progress bar animate, countdown visivi, theme switching fluido.

---

## [Glassmorphism 2.0 — Liquid Glass Effect](https://weblogtrips.com/technology/glassmorphism-2-0-css-techniques-2026/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Safari/Edge (Firefox parziale)

L'evoluzione 2026 del frosted glass punta sulla **surface transduction**: luce che interagisce con materiali digitali. Tecnica base: `backdrop-filter: blur()` + relative color syntax + mask-image. Non sovrapporre più di 3 pannelli glass per le performance. Aggiungere sempre un barrier layer per il contrasto (4.5:1).

**Snippet minimo funzionante:**
```css
.glass-card {
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: 16px;
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.18),
    inset 0 1px 0 rgba(255, 255, 255, 0.3);
  transform: translateZ(0); /* GPU offload */
}
/* Barrier layer per accessibilità testo */
.glass-card::before {
  content: '';
  position: absolute; inset: 0;
  background: rgba(0,0,0,0.25);
  border-radius: inherit;
  z-index: -1;
}
```

**Quando usarlo:** Hero overlay, modal, navbar sticky, card su sfondi colorati o foto.

---

## [CSS Micro-interactions: Hover & Button Effects](https://www.skillvalix.com/blog/css-animations-micro-interactions-guide)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Piccoli gesti CSS che trasformano un'interfaccia piatta in qualcosa di premium. Regola d'oro 2026: 3–5 micro-animazioni per pagina, ognuna con un unico scopo (conferma azione, cambio stato, guida attenzione).

**Snippet minimo funzionante:**
```css
/* Bottone con border draw on hover */
.btn-draw {
  position: relative;
  padding: 0.75rem 1.5rem;
  background: transparent;
  color: #6366f1;
  border: none;
  cursor: pointer;
}
.btn-draw::before, .btn-draw::after {
  content: '';
  position: absolute;
  width: 0; height: 2px;
  background: #6366f1;
  transition: width 0.3s ease;
}
.btn-draw::before { top: 0; left: 0; }
.btn-draw::after  { bottom: 0; right: 0; }
.btn-draw:hover::before,
.btn-draw:hover::after { width: 100%; }

/* Card con tilt 3D puro CSS */
.card-3d {
  transition: transform 0.3s ease;
  transform-style: preserve-3d;
}
.card-3d:hover {
  transform: perspective(600px) rotateX(4deg) rotateY(-4deg) translateY(-4px);
}
```

**Quando usarlo:** CTA, bottoni di navigazione, product card — qualsiasi elemento interattivo che deve comunicare reattività.
