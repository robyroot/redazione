# Librerie JavaScript per Grafica — Settimana 20260622

## [GSAP (GreenSock Animation Platform)](https://gsap.com/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Lo standard de facto per animazioni complesse, timeline sequenziali e SVG morphing. Dal 2024 è **100% gratuito** grazie al supporto di Webflow. Novità 2026: `Set` action nelle timeline (cambiamenti istantanei, toggle classi) e integrazione Lottie nativa in Webflow. ScrollTrigger domina per lo storytelling brand.

**Snippet minimo funzionante:**
```js
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

const tl = gsap.timeline({
  scrollTrigger: {
    trigger: '.hero',
    start: 'top center',
    end: 'bottom top',
    scrub: 1,
  }
});
tl.fromTo('.hero-title',
  { opacity: 0, y: 60 },
  { opacity: 1, y: 0, duration: 1 }
).fromTo('.hero-subtitle',
  { opacity: 0, x: -40 },
  { opacity: 1, x: 0, duration: 0.8 },
  '-=0.5'
);
```

**Quando usarlo:** Siti brand con narrative animate, landing page complesse, SVG morphing, sequenze coordinate tra più elementi.

---

## [Motion (ex Framer Motion)](https://motion.dev/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Standard 2026 per animazioni React. Motore ibrido GPU-accelerato a 120fps. API dichiarativa integrata con stato React. La versione non-React (`motion/dom`) funziona su qualsiasi stack.

**Snippet minimo funzionante:**
```jsx
import { motion, AnimatePresence } from 'motion/react';

function Card({ children }) {
  return (
    <motion.div
      layout
      initial={{ opacity: 0, scale: 0.9 }}
      animate={{ opacity: 1, scale: 1 }}
      exit={{ opacity: 0, scale: 0.9 }}
      whileHover={{ y: -4, boxShadow: '0 20px 40px rgba(0,0,0,0.15)' }}
      transition={{ type: 'spring', stiffness: 300, damping: 20 }}
    >
      {children}
    </motion.div>
  );
}

// Stagger su lista
const container = { hidden: {}, show: { transition: { staggerChildren: 0.08 } } };
const item = { hidden: { opacity: 0, y: 20 }, show: { opacity: 1, y: 0 } };
```

**Quando usarlo:** Tutto ciò che cambia stato in React — modal, list reorder, page transition, hover interattivo.

---

## [Rive](https://rive.app/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti (WASM/JS runtime)

Editor grafico + runtime per animazioni vettoriali **interattive** con state machine integrate. File fino al 90% più piccoli di video/GIF. AI-assisted in 2026: auto-animate genera frame intermedi. Un file .riv gira su web, iOS, Android, Unity.

**Snippet minimo funzionante:**
```html
<script src="https://unpkg.com/@rive-app/canvas@latest/rive.js"></script>
<canvas id="rive-canvas" width="500" height="500"></canvas>
<script>
  const r = new rive.Rive({
    src: 'hero-animation.riv',
    canvas: document.getElementById('rive-canvas'),
    autoplay: true,
    stateMachines: 'MainMachine',
    onLoad: () => r.resizeDrawingSurfaceToCanvas(),
  });

  document.querySelector('canvas').addEventListener('mouseenter', () => {
    const inputs = r.stateMachineInputs('MainMachine');
    const hover = inputs.find(i => i.name === 'isHovered');
    hover.value = true;
  });
</script>
```

**Quando usarlo:** Loader animati, mascotte interattive, illustrazioni che reagiscono all'utente, onboarding step-by-step.

---

## [Three.js con WebGPU](https://threejs.org/)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge (WebGPU), tutti (fallback WebGL 2)

Dal release r171 (settembre 2025) Three.js supporta WebGPU in produzione con fallback automatico a WebGL 2. WebGPU porta compute shaders e fino a 10× miglioramento nei draw-call. 2.7M download settimanali: ecosistema maturo.

**Snippet minimo funzionante:**
```js
import * as THREE from 'three';
import WebGPURenderer from 'three/addons/renderers/WebGPURenderer.js';

const renderer = new WebGPURenderer({ antialias: true });
await renderer.init();
document.body.appendChild(renderer.domElement);

const scene  = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, innerWidth / innerHeight, 0.1, 1000);
camera.position.z = 3;

const geo  = new THREE.SphereGeometry(1, 64, 64);
const mat  = new THREE.MeshStandardMaterial({ color: 0x6366f1, roughness: 0.3 });
const mesh = new THREE.Mesh(geo, mat);
scene.add(mesh, new THREE.AmbientLight(0xffffff, 0.5));

renderer.setAnimationLoop(() => {
  mesh.rotation.y += 0.005;
  renderer.render(scene, camera);
});
```

**Quando usarlo:** Prodotti 3D interattivi, sfondi WebGL, data visualization 3D. WebGPU per progetti Chrome/Edge-only ad alte performance.

---

## [Anime.js v4](https://animejs.com/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Libreria leggera (< 17KB gzip) per animare CSS, SVG, DOM e oggetti JS. La v4 ha raggiunto le performance di GSAP in scenari concorrenti. Zero dipendenze, ottima per progetti che non vogliono la complessità di GSAP.

**Snippet minimo funzionante:**
```js
import anime from 'animejs';

// SVG path drawing
anime({
  targets: 'path.logo',
  strokeDashoffset: [anime.setDashoffset, 0],
  easing: 'easeInOutSine',
  duration: 1500,
  delay: (_el, i) => i * 250,
  direction: 'alternate',
  loop: true,
});

// Stagger su griglia
anime({
  targets: '.grid-item',
  scale: [0, 1],
  opacity: [0, 1],
  delay: anime.stagger(50, { grid: [4, 4], from: 'center' }),
  easing: 'spring(1, 80, 10, 0)',
});
```

**Quando usarlo:** SVG path drawing, stagger grid, animazioni UI vanilla JS senza dipendenze React.

---

## [Lottie Web](https://airbnb.io/lottie/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Render di animazioni After Effects come JSON vettoriale scalabile. Stack 2026: designer esporta .json da AE con plugin Bodymovin, developer usa `@lottiefiles/lottie-player`. GSAP ora ha integrazione Lottie nativa nelle Interactions Webflow.

**Snippet minimo funzionante:**
```html
<script src="https://unpkg.com/@lottiefiles/lottie-player@latest/dist/lottie-player.js"></script>

<lottie-player
  src="https://assets.lottiefiles.com/packages/lf20_animation.json"
  background="transparent"
  speed="1"
  style="width: 300px; height: 300px;"
  autoplay
  loop>
</lottie-player>
```

**Quando usarlo:** Loader, icone animate, illustrazioni hero, empty state, onboarding.
