# Librerie JavaScript per Grafica e Animazioni — Aggiornamento 20260803

## [GSAP 3 (GreenSock) — ora 100% gratuito](https://gsap.com/)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome / Firefox / Safari / Edge

Il gold standard per animazioni web complesse: timeline sequenziali, SVG morphing, ScrollTrigger per scroll-driven avanzato. In 2026 è completamente free (inclusi plugin premium precedentemente a pagamento come MorphSVG e DrawSVG).

**Snippet minimo funzionante:**
```js
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

// Timeline scroll-driven
gsap.timeline({
  scrollTrigger: {
    trigger: '.hero',
    start: 'top top',
    end: 'bottom top',
    scrub: 1,
  }
})
.to('.hero-title', { y: -100, opacity: 0 })
.to('.hero-bg', { scale: 1.2 }, '<');

// SVG Morphing (MorphSVGPlugin ora free)
gsap.to('#shape', {
  duration: 1,
  morphSVG: '#target-shape',
  ease: 'power2.inOut',
});
```

**Quando usarlo:** Siti portfolio con storytelling via scroll, hero section complesse, animazioni SVG, qualsiasi sequenza temporale avanzata che CSS da solo non può gestire.

---

## [Three.js r184 + WebGPU](https://threejs.org/)
**Facilità:** ⭐⭐ (2/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome / Edge / Firefox / Safari (WebGPU universale 2025)

Three.js r184 (aprile 2026) porta WebGPU in produzione su tutti i browser. Il nuovo Three Shading Language (TSL) scrive shader una volta sola e compila in GLSL (WebGL) o WGSL (WebGPU). RenderPipeline sostituisce EffectComposer per post-processing.

**Snippet minimo funzionante:**
```js
import * as THREE from 'three';
import { WebGPURenderer } from 'three/addons/renderers/WebGPURenderer.js';
import { bloom } from 'three/addons/tsl/display/BloomNode.js';

const renderer = new WebGPURenderer({ antialias: true });
await renderer.init(); // WebGPU init asincrono

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, innerWidth / innerHeight, 0.1, 100);
camera.position.z = 3;

// Materiale con TSL (compila su WebGL e WebGPU)
const geometry = new THREE.IcosahedronGeometry(1, 4);
const material = new THREE.MeshStandardNodeMaterial();
const mesh = new THREE.Mesh(geometry, material);
scene.add(mesh);

// Post-processing con RenderPipeline
const postProcessing = new THREE.PostProcessing(renderer);
postProcessing.outputNode = bloom(scene, camera, { strength: 0.5 });

renderer.setAnimationLoop(() => {
  mesh.rotation.y += 0.005;
  postProcessing.render();
});
```

**Quando usarlo:** Hero section 3D interattive, product viewer, background generativi, esperienze immersive WebGL/WebGPU. Fino a 10× più veloce di WebGL in scenari draw-call-heavy.

---

## [Motion (ex Framer Motion) — React & framework-agnostic](https://motion.dev/)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome / Firefox / Safari / Edge

~6M download settimanali nel 2026, footprint di 8KB. Copre il 90% dei casi d'uso React con gesture support e layout animations. La versione framework-agnostic (`motion one`) funziona su qualsiasi stack.

**Snippet minimo funzionante:**
```jsx
// React (Framer Motion)
import { motion, useScroll, useTransform } from 'motion/react';

function HeroCard() {
  const { scrollYProgress } = useScroll();
  const y = useTransform(scrollYProgress, [0, 1], [0, -150]);

  return (
    <motion.div
      style={{ y }}
      initial={{ opacity: 0, scale: 0.9 }}
      animate={{ opacity: 1, scale: 1 }}
      transition={{ duration: 0.5, ease: [0.16, 1, 0.3, 1] }}
      whileHover={{ scale: 1.03 }}
      whileTap={{ scale: 0.98 }}
    >
      <h1>Ciao mondo!</h1>
    </motion.div>
  );
}

// Framework-agnostic (Motion One)
import { animate } from 'motion';
animate('.card', { opacity: [0, 1], y: [40, 0] }, { duration: 0.6 });
```

**Quando usarlo:** App React/Next.js che necessitano di transizioni di route, layout animations, gesture drag, e reveal-on-scroll senza configurazione complessa.

---

## [ThorVG 1.0 — Vector Graphics Engine](https://thorvg.org/)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome / Firefox / Safari / Edge (via WebCanvas)

Rilasciato stable il 31 gennaio 2026, ThorVG è un engine open-source per grafica vettoriale e animazioni (SVG, Lottie). Versione 1.0 include supporto ufficiale per WebCanvas — un Lottie/SVG renderer alternativo ultraleggero.

**Snippet minimo funzionante:**
```html
<!-- Lottie via ThorVG WASM (alternativa a lottie-player) -->
<canvas id="canvas" width="400" height="400"></canvas>
<script type="module">
  import { ThorVG } from './thorvg-wasm.js';

  const tvg = await ThorVG.init();
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');

  // Carica SVG
  await tvg.load('animation.svg');
  tvg.render(ctx, { width: 400, height: 400 });

  // Oppure Lottie
  await tvg.load('lottie.json');
  let frame = 0;
  function loop() {
    tvg.frame(frame++ % tvg.totalFrames);
    tvg.render(ctx, { width: 400, height: 400 });
    requestAnimationFrame(loop);
  }
  loop();
</script>
```

**Quando usarlo:** Alternativa leggera a Lottie Web quando si vuole controllo diretto su canvas, renderer SVG custom, o app che già gestiscono un canvas condiviso.

---

## [Rough.js — Stile Hand-Drawn](https://roughjs.com/)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome / Firefox / Safari / Edge

Libreria grafica <9KB che disegna forme in stile "disegnato a mano" su Canvas e SVG. Perfetta per infografiche informali, dashboard con tono playful, e illustrazioni generative.

**Snippet minimo funzionante:**
```html
<canvas id="canvas" width="600" height="400"></canvas>
<script type="module">
  import rough from 'https://cdn.skypack.dev/roughjs';

  const canvas = document.getElementById('canvas');
  const rc = rough.canvas(canvas);

  // Rettangolo
  rc.rectangle(10, 10, 200, 150, {
    fill: '#f59e0b',
    fillStyle: 'hachure',
    roughness: 1.5,
    stroke: '#1e293b',
    strokeWidth: 2,
  });

  // Cerchio
  rc.circle(400, 200, 120, {
    fill: '#6366f1',
    fillStyle: 'cross-hatch',
    roughness: 2,
  });

  // Linea
  rc.line(10, 380, 590, 380, { roughness: 1 });

  // Stessa API su SVG
  const svgEl = document.querySelector('svg');
  const rsvg = rough.svg(svgEl);
  svgEl.appendChild(rsvg.circle(100, 100, 80, { fill: '#ec4899' }));
</script>
```

**Quando usarlo:** Infografiche con tono informale, wireframe interattivi, data visualization "artistica", landing page per prodotti creativi e artigianali.

---

## [Anime.js v4 — Tweening Leggero](https://animejs.com/)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐ (3/5) | **Browser:** Chrome / Firefox / Safari / Edge

La v4 porta le performance allo stesso livello di GSAP con un API più semplice. Ideale per animazioni CSS, SVG e DOM senza la complessità di Three.js o la dipendenza da React di Motion.

**Snippet minimo funzionante:**
```js
import anime from 'animejs';

// Staggered reveal
anime({
  targets: '.grid-item',
  translateY: [40, 0],
  opacity: [0, 1],
  duration: 600,
  delay: anime.stagger(80), // 80ms tra ogni elemento
  easing: 'cubicBezier(0.16, 1, 0.3, 1)',
});

// SVG path drawing
anime({
  targets: 'path',
  strokeDashoffset: [anime.setDashoffset, 0],
  duration: 1500,
  easing: 'easeInOutSine',
  direction: 'alternate',
  loop: true,
});

// Timeline
const tl = anime.timeline({ easing: 'easeOutExpo', duration: 750 });
tl.add({ targets: '.el', translateX: 250 })
  .add({ targets: '.el', scale: 2 }, '-=400')
  .add({ targets: '.el', rotate: '1turn' });
```

**Quando usarlo:** Animazioni staggered di liste/griglie, path drawing SVG, sequenze temporali semplici. Ottima alternativa a GSAP quando non serve ScrollTrigger.
