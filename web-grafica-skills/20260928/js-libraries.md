# Librerie JavaScript per Grafica e Animazioni — Settimana 20260928

## [GSAP (GreenSock Animation Platform)](https://gsap.com)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

L'industry-standard per animazioni timeline complesse, SVG morphing e scroll choreography. Dal 2024 è 100% gratuito, plugin inclusi (ScrollTrigger, MorphSVG, SplitText). Usato da Google, Nike, Netflix per esperienze web premium.

**Snippet minimo funzionante:**
```js
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

// Timeline con scrub
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

// Stagger reveal
gsap.from('.card', {
  opacity: 0,
  y: 60,
  stagger: 0.1,
  duration: 0.7,
  ease: 'power3.out',
  scrollTrigger: { trigger: '.cards-grid', start: 'top 80%' }
});
```

**Quando usarlo:** Scroll storytelling complesso, animazioni timeline multi-step, SVG morphing, text split animations. La scelta professionale per siti agency e landing page premium.

---

## [Anime.js v4](https://animejs.com)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Completamente riscritto in v4 con architettura modulare ES modules: importi solo quello che usi, il bundle rimane minuscolo. Raggiunge ora le performance di GSAP per use case comuni. La scelta ideale quando il bundle size è un vincolo.

**Snippet minimo funzionante:**
```js
// Import modulare — solo i moduli necessari
import { animate, stagger, createTimeline } from 'animejs';

// Tween semplice
animate('.box', {
  translateX: 250,
  rotate: '1turn',
  backgroundColor: '#6366f1',
  duration: 800,
  ease: 'outElastic(1, .6)',
});

// Stagger su lista
animate('.list-item', {
  opacity: [0, 1],
  translateY: [20, 0],
  delay: stagger(80),
  duration: 500,
});

// Timeline
const tl = createTimeline({ loop: true });
tl.add('.circle', { scale: [1, 1.5], duration: 400 })
  .add('.circle', { scale: [1.5, 1], duration: 400 });
```

**Quando usarlo:** Progetti con vincoli di bundle size, tweens semplici/medi, animazioni UI senza dipendenza da ScrollTrigger. Preferibile a GSAP per piccoli progetti.

---

## [Three.js r186 con WebGPU](https://threejs.org)
**Facilità:** ⭐⭐ (2/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Release r186 (settembre 2026): il renderer WebGPU è production-ready con fallback automatico a WebGL 2 su browser older. Fino a 10x più veloce di WebGL in scenari draw-call-heavy. Usa il nuovo shader language TSL (Three Shading Language) invece di GLSL.

**Snippet minimo funzionante:**
```js
// WebGPU con fallback automatico a WebGL 2
import * as THREE from 'three/webgpu';

const renderer = new THREE.WebGPURenderer({ antialias: true });
await renderer.init(); // init asincrono obbligatorio
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 100);
camera.position.z = 5;

// Material con TSL node system
import { color, normalWorld } from 'three/tsl';
const material = new THREE.MeshBasicNodeMaterial();
material.colorNode = normalWorld; // shader procedurale

const mesh = new THREE.Mesh(new THREE.IcosahedronGeometry(2, 4), material);
scene.add(mesh);

renderer.setAnimationLoop(() => {
  mesh.rotation.y += 0.005;
  renderer.render(scene, camera);
});
```

**Quando usarlo:** Hero 3D interattivi, background particellari, product visualization, esperienze immersive. React Three Fiber rimane la scelta per progetti React.

---

## [Motion (ex Framer Motion)](https://motion.dev)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

8KB footprint, ottimizzato per React e Next.js. Nel 2026 è la scelta standard per animazioni UI in applicazioni React. Gestisce layout animations, exit animations e gesture con una API dichiarativa.

**Snippet minimo funzionante:**
```jsx
import { motion, AnimatePresence } from 'motion/react';

// Card con hover e tap
function AnimatedCard({ children }) {
  return (
    <motion.div
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      whileHover={{ scale: 1.02, boxShadow: '0 20px 40px rgba(0,0,0,0.15)' }}
      whileTap={{ scale: 0.98 }}
      transition={{ type: 'spring', stiffness: 300, damping: 20 }}
      className="card"
    >
      {children}
    </motion.div>
  );
}

// Exit animation con AnimatePresence
<AnimatePresence>
  {isVisible && (
    <motion.div
      key="modal"
      initial={{ opacity: 0, scale: 0.9 }}
      animate={{ opacity: 1, scale: 1 }}
      exit={{ opacity: 0, scale: 0.9 }}
    />
  )}
</AnimatePresence>
```

**Quando usarlo:** Qualunque progetto React/Next.js che necessita di animazioni UI. Sostituisce CSS transitions per interazioni complesse e layout animations.

---

## [Lottie Web](https://airbnb.io/lottie)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Market share dell'8.1% — la libreria di animazione più usata. Riproduce animazioni After Effects esportate in JSON. Nel 2026 si integra con Rive per animazioni interattive controllate da variabili di codice.

**Snippet minimo funzionante:**
```js
import lottie from 'lottie-web';

const animation = lottie.loadAnimation({
  container: document.getElementById('lottie-container'),
  renderer: 'svg',
  loop: false,
  autoplay: false,
  path: '/animations/success.json',
});

// Controllato da evento
document.getElementById('submit-btn').addEventListener('click', () => {
  animation.play();
});

// Interattivo con scroll
window.addEventListener('scroll', () => {
  const progress = window.scrollY / (document.body.scrollHeight - window.innerHeight);
  animation.goToAndStop(Math.floor(progress * animation.totalFrames), true);
});
```

**Quando usarlo:** Illustrazioni animate, icone interattive, loading states, onboarding flow. Ideale quando il designer lavora in After Effects.
