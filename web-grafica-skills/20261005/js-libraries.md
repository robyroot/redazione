# Librerie JavaScript per Grafica & Animazioni — Settimana 20261005

## [GSAP — GreenSock Animation Platform](https://gsap.com/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti i browser

Lo standard industriale per animazioni professionali web. Da aprile 2025 (acquisizione da Webflow) è completamente **gratuito**, inclusi tutti i plugin premium come SplitText e MorphSVG. Oltre 18,7 milioni di download npm solo ad agosto 2026.

**Snippet minimo funzionante:**
```javascript
// Import (CDN o npm)
// <script src="https://cdn.jsdelivr.net/npm/gsap@3.12/dist/gsap.min.js"></script>
// <script src="https://cdn.jsdelivr.net/npm/gsap@3.12/dist/ScrollTrigger.min.js"></script>

gsap.registerPlugin(ScrollTrigger);

// Animazione scroll-triggered con pin
gsap.timeline({
  scrollTrigger: {
    trigger: ".hero",
    start: "top top",
    end: "+=500",
    scrub: 1,
    pin: true,
  }
})
.from(".hero-title", { y: 60, opacity: 0, duration: 1 })
.from(".hero-subtitle", { y: 40, opacity: 0, duration: 0.8 }, "-=0.5");

// SplitText (ora gratuito!) per animazioni lettera per lettera
const split = new SplitText(".headline", { type: "chars" });
gsap.from(split.chars, {
  opacity: 0,
  y: 20,
  stagger: 0.03,
  duration: 0.5,
  ease: "power2.out"
});
```

**Quando usarlo:** Siti portfolio con effetti wow, landing page con storytelling scroll-based, animazioni SVG complesse, transizioni di pagina.

---

## [Anime.js v4.5](https://animejs.com/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti i browser

Riscrittura completa con architettura modulare ES Module. Tree-shakeable: importi solo quello che usi. Solo ~10KB gzipped. La v4.5 (giugno 2026) aggiunge `registerAdapter()` per animare target non-DOM e un adapter nativo per Three.js.

**Snippet minimo funzionante:**
```javascript
// Import solo le funzioni necessarie (tree-shaking)
import { animate, stagger, createTimeline } from 'animejs';

// Animazione con stagger
animate('.card', {
  opacity: [0, 1],
  translateY: [30, 0],
  delay: stagger(100),
  duration: 600,
  ease: 'out(3)',
});

// Timeline sequenziale
const tl = createTimeline({ defaults: { duration: 400 } });
tl
  .add('.logo', { scale: [0, 1], ease: 'spring(1, 80, 10)' })
  .add('.nav-item', { opacity: [0, 1], translateX: [-20, 0], delay: stagger(60) })
  .add('.cta-btn', { scale: [0.8, 1], opacity: [0, 1] }, '-=200');

// Adapter Three.js (novità v4.5)
import { createThreeAdapter } from 'animejs/adapters/three';
registerAdapter(createThreeAdapter());
animate(mesh.position, { x: 2, y: 1, duration: 1000 });
```

**Quando usarlo:** Micro-animazioni UI, loading states, animazioni sequenziali leggere, integrazione con Three.js senza il peso di GSAP.

---

## [Motion for React (ex Framer Motion)](https://motion.dev/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti i browser

La libreria definitiva per React. Rebrandata come "Motion for React", offre animazioni dichiarative con gesture, layout animations e shared element transitions. Usatissima con Next.js e shadcn/ui.

**Snippet minimo funzionante:**
```jsx
import { motion, AnimatePresence } from 'motion/react';

// Animazione base con varianti
const cardVariants = {
  hidden: { opacity: 0, y: 20, scale: 0.95 },
  visible: { opacity: 1, y: 0, scale: 1 },
  exit: { opacity: 0, scale: 0.9 }
};

function ProductCard({ isVisible }) {
  return (
    <AnimatePresence>
      {isVisible && (
        <motion.div
          variants={cardVariants}
          initial="hidden"
          animate="visible"
          exit="exit"
          transition={{ type: "spring", stiffness: 300, damping: 30 }}
          whileHover={{ y: -4, boxShadow: "0 20px 40px rgba(0,0,0,0.15)" }}
          whileTap={{ scale: 0.98 }}
          className="card"
        >
          Card content
        </motion.div>
      )}
    </AnimatePresence>
  );
}

// Layout animation (riordino fluido di liste)
<motion.ul layout>
  {items.map(item => (
    <motion.li key={item.id} layout layoutId={item.id}>
      {item.name}
    </motion.li>
  ))}
</motion.ul>
```

**Quando usarlo:** App React/Next.js, dashboard interattive, liste filtrabili, modal con animazioni fluide, qualsiasi UI component React che necessita di motion.

---

## [Lottie Web](https://airbnb.design/lottie/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti i browser

Renderizza animazioni After Effects (JSON) sul web con qualità vettoriale perfetta. Market share dell'8,1% — la più usata per animazioni decorative. Perfetta per illustrazioni animate, icone interattive e loader.

**Snippet minimo funzionante:**
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/lottie-web/5.12.2/lottie.min.js"></script>

<div id="lottie-container" style="width:200px;height:200px"></div>

<script>
const animation = lottie.loadAnimation({
  container: document.getElementById('lottie-container'),
  renderer: 'svg',
  loop: true,
  autoplay: true,
  path: 'animation.json' // file JSON da LottieFiles.com
});

// Controllo interattivo (play on hover)
const el = document.getElementById('lottie-container');
el.addEventListener('mouseenter', () => animation.play());
el.addEventListener('mouseleave', () => animation.stop());
</script>
```

**Quando usarlo:** Icone animate per hover/click, illustrazioni hero animate, empty states, loader/spinner premium, onboarding animato.
