# Librerie JavaScript per Grafica e Animazioni — Ottobre 2026

## [GSAP 3.12+ (ora MIT License)](https://gsap.com)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Il motore di animazione professionale per eccellenza. Da fine 2024 è **MIT-licensed** dopo l'acquisizione da parte di Webflow — core e plugin inclusi gratuitamente. Unico sul mercato per timeline complesse, morphing SVG, scroll-driven e sincronizzazione audio/video. I plugin premium (ScrollTrigger, MorphSVG, DrawSVG) restano commerciali per progetti a pagamento.

**Snippet minimo funzionante:**
```javascript
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

// Timeline con stagger su card
gsap.from('.card', {
  opacity: 0,
  y: 60,
  duration: 0.6,
  stagger: 0.1,
  ease: 'power3.out',
  scrollTrigger: {
    trigger: '.cards-section',
    start: 'top 80%',
  }
});

// Animazione testo lettera per lettera
const chars = document.querySelectorAll('.hero-title span');
gsap.from(chars, {
  opacity: 0, rotateX: 90,
  transformOrigin: '0% 50% -50',
  duration: 0.5,
  stagger: 0.03,
  ease: 'back.out(1.7)'
});
```

**Quando usarlo:** Landing page con animazioni coordinate, storytelling interattivo, transizioni di pagina avanzate. Standard de facto nell'industry creativa.

---

## [Motion (ex Framer Motion) — v12+](https://motion.dev)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Libreria di animazione per React (e ora anche vanilla JS via `motion` package) focalizzata su transizioni di layout e state. Gestisce animate-in/out, drag, scroll e gesture in modo dichiarativo. In 2026 il pacchetto si è unificato: `motion` funziona sia con React che senza.

**Snippet minimo funzionante:**
```jsx
import { motion, AnimatePresence } from 'motion/react';

// Card con layout animation
<motion.div
  layout
  initial={{ opacity: 0, scale: 0.8 }}
  animate={{ opacity: 1, scale: 1 }}
  exit={{ opacity: 0, scale: 0.8 }}
  whileHover={{ y: -4, boxShadow: '0 20px 40px rgba(0,0,0,0.15)' }}
  transition={{ type: 'spring', stiffness: 300, damping: 20 }}
/>

// Vanilla JS
import { animate } from 'motion';
animate('.hero', { opacity: [0, 1], y: [-20, 0] }, { duration: 0.5 });
```

**Quando usarlo:** App React con UI reattive, transizioni di stato, liste ordinate/filtrate, drag & drop animato.

---

## [Anime.js v4 — Riscrittura TypeScript](https://animejs.com)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Leggera (< 15kb), MIT, riscritta da zero in TypeScript in v4 con architettura modulare. Perfetta per animare CSS, SVG, attributi DOM e oggetti JavaScript. Nessuna dipendenza.

**Snippet minimo funzionante:**
```javascript
import anime from 'animejs';

// SVG path draw animation
anime({
  targets: '.svg-path',
  strokeDashoffset: [anime.setDashoffset, 0],
  easing: 'easeInOutSine',
  duration: 1500,
  delay: (el, i) => i * 250,
  direction: 'alternate',
  loop: true
});

// Stagger con layout grid
anime({
  targets: '.dot',
  translateX: anime.stagger(10, { grid: [14, 5], from: 'center', axis: 'x' }),
  translateY: anime.stagger(10, { grid: [14, 5], from: 'center', axis: 'y' }),
  rotateZ: anime.stagger([0, 90], { grid: [14, 5], from: 'center' }),
  delay: anime.stagger(200, { grid: [14, 5], from: 'center' }),
  easing: 'easeInOutQuad',
  loop: true, direction: 'alternate'
});
```

**Quando usarlo:** Animazioni SVG, visualizzazioni dati animate, effetti di loading eleganti, qualsiasi progetto che non usa React e vuole leggerezza.

---

## [Three.js r186 — WebGPU + Gaussian Splats](https://threejs.org)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome ✅ Safari ✅ (iOS da sett. 2025) Firefox ✅

Il motore 3D del web ha raggiunto maturità WebGPU in 2026: supporto universale su tutti i browser principali. r186 aggiunge un renderer nativo per Gaussian Splatting e il TSL (Three Shading Language) che compila sia GLSL che WGSL. Import zero-config via `three/webgpu`.

**Snippet minimo funzionante:**
```javascript
// WebGPU renderer (zero config)
import * as THREE from 'three/webgpu';
import { WebGPURenderer } from 'three/webgpu';

const renderer = new WebGPURenderer({ antialias: true });
await renderer.init(); // WebGPU async init

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, innerWidth / innerHeight, 0.1, 100);

// TSL material (compila per WebGL e WebGPU)
import { color, positionLocal, sin, time, uniform } from 'three/tsl';
const material = new THREE.MeshStandardNodeMaterial();
material.colorNode = sin(positionLocal.x.add(time)).mix(color(0xff0000), color(0x0000ff));
```

**Quando usarlo:** Hero section 3D, product configurator, portfolio immersivi, visualizzazioni scientifiche. Con r3f (React Three Fiber) per integrazione React.

---

## [Lenis — Smooth Scroll](https://lenis.darkroom.engineering)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Scrolling con inerzia/momentum elegante in < 4kb. Zero dipendenze, si integra perfettamente con GSAP ScrollTrigger. Standard de facto per siti creativi e portfolio.

**Snippet minimo funzionante:**
```javascript
import Lenis from 'lenis';

const lenis = new Lenis({
  duration: 1.2,
  easing: t => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
  smoothWheel: true,
});

// Sync con GSAP ScrollTrigger
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

lenis.on('scroll', ScrollTrigger.update);
gsap.ticker.add(time => lenis.raf(time * 1000));
gsap.ticker.lagSmoothing(0);

function raf(time) {
  lenis.raf(time);
  requestAnimationFrame(raf);
}
requestAnimationFrame(raf);
```

**Quando usarlo:** Ogni sito/portfolio che vuole scrolling premium; sempre in coppia con GSAP per animazioni scroll-driven.

---

## [Lottie / dotLottie](https://lottiefiles.com)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Player di animazioni vettoriali esportate da After Effects (formato JSON/dotLottie compresso). Perfetto per icone animate, illustrazioni e loader. La libreria ufficiale è `lottie-web` v5.x; dotLottie è il formato compresso di nuova generazione.

**Snippet minimo funzionante:**
```html
<!-- Via CDN -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/bodymovin/5.12.2/lottie.min.js"></script>

<div id="lottie-anim"></div>

<script>
lottie.loadAnimation({
  container: document.getElementById('lottie-anim'),
  renderer: 'svg',
  loop: true,
  autoplay: true,
  path: '/animations/loading.json'
});
</script>

<!-- oppure dotLottie (più leggero) -->
<dotlottie-player
  src="/animations/hero.lottie"
  autoplay loop
  style="width: 300px;"
></dotlottie-player>
```

**Quando usarlo:** Icone animate, illustrazioni hero, loader/spinner, onboarding interattivo. Più leggero e scalabile dei GIF animati.
