# JS Libraries per Grafica — Settimana 20261026

## [GSAP 3.15 — ora 100% gratuito](https://gsap.com)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Da quando Webflow ha acquisito GSAP (2024), tutti i plugin (ScrollTrigger, SplitText, MorphSVG, Flip, Draggable) sono free anche per uso commerciale. GSAP rimane lo standard de facto per animazioni complesse su timeline e per scroll-driven di alto livello.

**Snippet minimo funzionante:**
```html
<script src="https://cdn.jsdelivr.net/npm/gsap@3.15.0/dist/gsap.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.15.0/dist/ScrollTrigger.min.js"></script>
<script>
gsap.registerPlugin(ScrollTrigger);

// Parallax su una sezione hero
gsap.to(".hero-image", {
  yPercent: -30,
  ease: "none",
  scrollTrigger: {
    trigger: ".hero",
    start: "top top",
    end: "bottom top",
    scrub: true,
  }
});

// Reveal di cards in sequenza
gsap.from(".card", {
  opacity: 0,
  y: 60,
  duration: 0.8,
  stagger: 0.15,
  ease: "power2.out",
  scrollTrigger: {
    trigger: ".cards-grid",
    start: "top 80%",
  }
});
</script>
```

**Quando usarlo:** Landing page con storytelling complesso, hero parallax, testo che si rivela lettera per lettera, scroll-pin con animazione sincronizzata.

---

## [Lenis — Smooth Scroll Library](https://lenis.darkroomengineering.com/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Lenis è la libreria per lo smooth scroll nei siti premium del 2026. Rimpiazza la ruota dello scroll "a scatti" con un momentum fluido. Si integra perfettamente con GSAP ScrollTrigger per effetti scroll avanzati.

**Snippet minimo funzionante:**
```html
<script src="https://cdn.jsdelivr.net/npm/lenis@1.3.26/dist/lenis.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.15.0/dist/gsap.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.15.0/dist/ScrollTrigger.min.js"></script>
<script>
gsap.registerPlugin(ScrollTrigger);

const lenis = new Lenis({
  duration: 1.2,
  easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
});

// Integrazione con GSAP ticker
gsap.ticker.add((time) => {
  lenis.raf(time * 1000);
});
gsap.ticker.lagSmoothing(0);

// ScrollTrigger legge lo scroll di Lenis
lenis.on('scroll', ScrollTrigger.update);
</script>
```

**Quando usarlo:** Qualsiasi sito premium o portfolio dove vuoi un feel "agenzia", abbinato a GSAP per effetti scroll complessi.

---

## [Motion (ex Framer Motion) — React Animations](https://motion.dev/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Motion è la libreria di animazione standard per React. Dopo il rebrand da Framer Motion offre anche `motion/vanilla` per progetti non-React. Le features killer: `AnimatePresence` per exit animations e layout animations automatiche.

**Snippet minimo funzionante:**
```jsx
import { motion, AnimatePresence } from 'motion/react';

// Transizione di pagina con fade
function PageTransition({ children, key }) {
  return (
    <AnimatePresence mode="wait">
      <motion.div
        key={key}
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        exit={{ opacity: 0, y: -20 }}
        transition={{ duration: 0.3 }}
      >
        {children}
      </motion.div>
    </AnimatePresence>
  );
}

// Card con hover e tap
function Card() {
  return (
    <motion.div
      className="card"
      whileHover={{ scale: 1.04, y: -4 }}
      whileTap={{ scale: 0.98 }}
      transition={{ type: "spring", stiffness: 400, damping: 17 }}
    />
  );
}
```

**Quando usarlo:** App React, Next.js, transizioni di pagina, liste che si riordinano, modal con animazione di entrata/uscita.

---

## [Rive — Animazioni Interattive Vettoriali](https://rive.app/)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Rive è il sostituto moderno di Lottie per animazioni vettoriali su web. Permette state machine interattive (l'animazione risponde all'input dell'utente in real-time), ha un editor visivo, ed è molto più performante di SVG animato.

**Snippet minimo funzionante:**
```html
<script src="https://unpkg.com/@rive-app/canvas@2.26.0/rive.js"></script>
<canvas id="canvas" width="400" height="400"></canvas>
<script>
const r = new rive.Rive({
  src: 'hero-animation.riv',
  canvas: document.getElementById('canvas'),
  autoplay: true,
  stateMachines: 'State Machine 1',
  onLoad: () => {
    const inputs = r.stateMachineInputs('State Machine 1');
    const hoverInput = inputs.find(i => i.name === 'isHover');

    document.getElementById('canvas').addEventListener('mouseover', () => {
      hoverInput.value = true;
    });
    document.getElementById('canvas').addEventListener('mouseout', () => {
      hoverInput.value = false;
    });
  }
});
</script>
```

**Quando usarlo:** Hero section interattiva, illustrazioni che reagiscono al mouse/touch, loader animati, icone con hover state, mascotte/character animation.

---

## [Anime.js 4 — Lightweight Animation](https://animejs.com/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Anime.js rimane la scelta "zero-config" per chi vuole animazioni fluide senza imparare GSAP. Leggera (~18KB), nessuna dipendenza, funziona su qualsiasi elemento DOM, SVG e CSS property.

**Snippet minimo funzionante:**
```html
<script src="https://cdn.jsdelivr.net/npm/animejs@4.0.0/lib/anime.min.js"></script>
<script>
// Animazione SVG path (fill progressivo)
anime({
  targets: '.svg-path',
  strokeDashoffset: [anime.setDashoffset, 0],
  easing: 'easeInOutSine',
  duration: 1500,
  delay: (el, i) => i * 250,
  direction: 'alternate',
  loop: true
});

// Stagger su una griglia
anime({
  targets: '.grid-item',
  scale: [0, 1],
  opacity: [0, 1],
  delay: anime.stagger(50, { grid: [5, 5], from: 'center' }),
  easing: 'easeOutElastic(1, .8)',
  duration: 800
});
</script>
```

**Quando usarlo:** Animazioni SVG, counter numerici, stagger su griglie, animazioni leggere senza il peso di GSAP.
