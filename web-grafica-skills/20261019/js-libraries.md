# Librerie JavaScript per Grafica e Animazioni — Settimana 20261019

## [GSAP (GreenSock Animation Platform)](https://gsap.com)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

La libreria di animazione più potente del web. Dal 2024 **completamente gratuita** (inclusi tutti i plugin premium) dopo l'acquisizione da parte di Webflow. ScrollTrigger, SplitText, MorphSVG, Draggable: tutto free per uso commerciale, zero licenze o token richiesti.

**Snippet minimo funzionante:**
```js
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

gsap.from('.hero-title', {
  y: 60,
  opacity: 0,
  duration: 1,
  ease: 'power3.out',
  scrollTrigger: {
    trigger: '.hero-title',
    start: 'top 80%',
  }
});
```

**Quando usarlo:** Animazioni complesse, storie interattive, landing page premium, qualsiasi animazione che richiede controllo preciso della timeline.

---

## [Anime.js v4](https://animejs.com)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

La v4 (2025-2026) è una riscrittura modulare: puro ES Module, tree-shakeable, ~40KB gzipped ma ridotto a pochi KB se si importa solo `animate`. Sintassi semplificata e nomi di easing più corti.

**Snippet minimo funzionante:**
```js
import { animate, stagger } from 'animejs';

animate('.item', {
  translateX: [0, 200],
  opacity: [0, 1],
  duration: 800,
  ease: 'inOutQuad',
  delay: stagger(100),
});
```

**Quando usarlo:** Animazioni leggere in progetti dove il bundle size conta. Ottimo per micro-interazioni, animazioni di lista, UI state transitions.

---

## [Motion (ex Framer Motion)](https://motion.dev)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

La scelta default per React. Ora esiste anche la versione vanilla `motion/dom` per progetti senza framework. API dichiarativa con `<motion.div>` in React, o `animate()` per il DOM nativo.

**Snippet minimo funzionante (React):**
```jsx
import { motion } from 'motion/react';

export function Card() {
  return (
    <motion.div
      initial={{ opacity: 0, y: 20 }}
      whileInView={{ opacity: 1, y: 0 }}
      transition={{ duration: 0.5 }}
      viewport={{ once: true }}
    >
      Contenuto card
    </motion.div>
  );
}
```

**Quando usarlo:** Qualsiasi progetto React che necessita di animazioni UI — hover states, page transitions, reveal on scroll.

---

## [Rive](https://rive.app)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

Strumento per animazioni vettoriali interattive (simile a Lottie ma con state machine). Si crea il file `.riv` nell'editor Rive e si integra con un runtime leggero. Perfetto per mascotte animate, icone interattive, micro-animazioni complesse che reagiscono all'input utente.

**Snippet minimo funzionante:**
```html
<canvas id="rive-canvas" width="400" height="300"></canvas>

<script type="module">
import Rive from 'https://cdn.jsdelivr.net/npm/@rive-app/canvas@2/rive.mjs';

const r = new Rive({
  src: 'mascot.riv',
  canvas: document.getElementById('rive-canvas'),
  autoplay: true,
  stateMachines: 'State Machine 1',
});

document.getElementById('rive-canvas').addEventListener('click', () => {
  r.stateMachineInputs('State Machine 1')
    .find(i => i.name === 'Clicked')
    .fire();
});
</script>
```

**Quando usarlo:** Icone animate, mascotte interattive, CTA con animazione complessa, onboarding flows.

---

## [AOS (Animate On Scroll)](https://michalsnik.github.io/aos/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐ | **Browser:** Chrome/Firefox/Safari/Edge

La soluzione zero-config per reveal on scroll. Basta aggiungere attributi `data-aos` agli elementi. Ideale per landing page veloci senza complessità.

**Snippet minimo funzionante:**
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aos@2.3.4/dist/aos.css"/>

<div data-aos="fade-up" data-aos-delay="100">Card 1</div>
<div data-aos="fade-up" data-aos-delay="200">Card 2</div>
<div data-aos="zoom-in" data-aos-duration="800">Card 3</div>

<script src="https://cdn.jsdelivr.net/npm/aos@2.3.4/dist/aos.js"></script>
<script>AOS.init({ once: true, offset: 80 });</script>
```

**Quando usarlo:** Landing page, siti vetrina, CMS-based websites dove non si vuole scrivere JavaScript personalizzato.
