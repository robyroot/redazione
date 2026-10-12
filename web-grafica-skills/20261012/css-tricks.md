# CSS Avanzato & Animazioni — Ottobre 2026

## [CSS Scroll-Driven Animations](https://developer.chrome.com/blog/scroll-triggered-animations)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome ✅ Safari ✅ Firefox ⚠️ (flag in stable, on in Nightly)

Animazioni CSS native guidate dallo scroll senza una riga di JavaScript. Con `animation-timeline: scroll()` o `view()` si ottengono parallax, progress bar, fade-in on scroll e carousel puri CSS. Chrome 145 ha aggiunto anche le *scroll-triggered animations* (si attivano una volta superata una soglia), eliminando il bisogno di `IntersectionObserver`.

**Snippet minimo funzionante:**
```css
/* Progress bar di lettura */
@keyframes grow {
  from { width: 0% }
  to   { width: 100% }
}

.progress-bar {
  animation: grow linear;
  animation-timeline: scroll(root);
}

/* Fade-in elemento quando entra nel viewport */
@keyframes fade-in {
  from { opacity: 0; translate: 0 40px }
  to   { opacity: 1; translate: 0 0 }
}

.card {
  animation: fade-in ease both;
  animation-timeline: view();
  animation-range: entry 0% entry 30%;
}

/* Accessibilità obbligatoria */
@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; }
}
```

**Quando usarlo:** Hero section con parallax, progress bar di lettura, reveal di card/sezioni, carousel puri CSS. Sostituisce GSAP ScrollTrigger e Framer Motion per il ~80% dei casi d'uso.

---

## [CSS @property — Variabili Tipizzate e Animabili](https://conffab.com/?p=6804)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ (supporto universale da metà 2024)

Permette di registrare custom properties con tipo, valore di default e controllo dell'ereditarietà. Il vantaggio killer: i gradienti diventano **animabili** perché la proprietà non è più una stringa opaca ma un valore numerico/colore interpolabile.

**Snippet minimo funzionante:**
```css
/* Gradiente animato via @property */
@property --hue {
  syntax: '<angle>';
  initial-value: 0deg;
  inherits: false;
}

.button {
  --hue: 0deg;
  background: linear-gradient(
    hsl(var(--hue), 80%, 60%),
    hsl(calc(var(--hue) + 60deg), 80%, 50%)
  );
  transition: --hue 0.4s ease;
}

.button:hover {
  --hue: 180deg;
}

/* Clip-path non ereditata per solo elemento */
@property --circle-size {
  syntax: '<percentage>';
  initial-value: 10%;
  inherits: false;
}
.avatar {
  clip-path: circle(var(--circle-size));
  transition: --circle-size 0.3s;
}
.avatar:hover { --circle-size: 50%; }
```

**Quando usarlo:** Animazione di gradienti, shape morphing con clip-path, border-radius fluido, contatori animati. Essenziale ogni volta che `transition` non funziona su una custom property.

---

## [Glassmorphism con backdrop-filter](https://theplusaddons.com/blog/glassmorphism/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Safari ✅ Firefox ✅

Effetto vetro smerigliato ispirato ad Apple Liquid Glass (rivitalizzato a giugno 2025). Si basa su `backdrop-filter: blur()` + sfondo semi-trasparente. Attenzione: problemi di leggibilità su testo lungo; usare solo per card/modal su sfondi colorati.

**Snippet minimo funzionante:**
```css
.glass-card {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow:
    0 4px 30px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.3);
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  .glass-card {
    background: rgba(0, 0, 0, 0.25);
    border-color: rgba(255, 255, 255, 0.1);
  }
}
```

**Quando usarlo:** Navbar floating, modal overlay, card su sfondi fotografici o a gradiente. Da evitare per blocchi di testo estesi.

---

## [Micro-interactions con @starting-style](https://htmlburger.com/blog/microinteractions-guide/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ (widely available da agosto 2024)

`@starting-style` definisce lo stato iniziale di un elemento *appena inserito nel DOM*, rendendo possibili animazioni di entrata senza JS. Combinato con `transition-behavior: allow-discrete`, gestisce anche le transizioni da/verso `display: none`.

**Snippet minimo funzionante:**
```css
/* Toast / notifica che appare con slide */
.toast {
  opacity: 1;
  translate: 0 0;
  transition:
    opacity 0.3s ease,
    translate 0.3s ease,
    display 0.3s allow-discrete;
}

@starting-style {
  .toast {
    opacity: 0;
    translate: 0 -20px;
  }
}

/* Button hover con feedback tattile */
.btn {
  transform: scale(1);
  transition: transform 0.15s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.btn:active { transform: scale(0.95); }

/* Hamburger → X (pure CSS) */
.bar-mid { transition: opacity 0.2s; }
.open .bar-mid { opacity: 0; }
.bar-top { transition: transform 0.3s; }
.open .bar-top { transform: rotate(45deg) translate(5px, 5px); }
.bar-bot { transition: transform 0.3s; }
.open .bar-bot { transform: rotate(-45deg) translate(5px, -5px); }
```

**Quando usarlo:** Entry animation di toast/notifiche, dropdown, modali; toggle menu; feedback su bottoni; form validation con transizioni fluide.

---

## [CSS Carousel con ::scroll-button() e ::scroll-marker()](https://www.sitepoint.com/scrolldriven-css-in-2026-building-carousels-without-javascript/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ (altri in sviluppo — CSS Overflow Level 5)

I nuovi pseudo-elementi `::scroll-button()` e `::scroll-marker()` dello spec CSS Overflow Level 5 permettono di costruire carousel con frecce e dots navigabili senza JavaScript.

**Snippet minimo funzionante:**
```css
.carousel {
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
}

.carousel::scroll-button(right) {
  content: '→';
  cursor: pointer;
}

.carousel::scroll-button(left) {
  content: '←';
  cursor: pointer;
}

.carousel-item {
  scroll-snap-align: start;
  min-width: 80%;
}
```

**Quando usarlo:** Gallerie immagini, testimonial slider, product showcase — ovunque si voglia zero JS nel bundle.
