# Librerie JavaScript per Grafica & Animazioni — Settimana 20260720

## [GSAP 3 — Gold Standard Animazioni Web](https://gsap.com)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

GSAP è diventato **completamente gratuito** nel 2024 (licenza MIT) e rimane lo standard de-facto per animazioni complesse in produzione. In 2026 è il riferimento per timeline sequenziali, SVG morphing, scroll scrubbing avanzato. Integrazione nativa con Webflow e Lottie tramite nuovi action type.

**Snippet minimo funzionante:**
```javascript
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

// Timeline con scroll scrubbing
const tl = gsap.timeline({
  scrollTrigger: {
    trigger: '.hero',
    start: 'top top',
    end: '+=600',
    scrub: 1,
    pin: true,
  }
});

tl.from('.hero-title', { y: 100, opacity: 0, duration: 1 })
  .from('.hero-subtitle', { y: 60, opacity: 0, duration: 0.8 }, '-=0.4')
  .from('.hero-cta', { scale: 0.8, opacity: 0, duration: 0.6 }, '-=0.3');
```

**Quando usarlo:** Siti portfolio/agenzia con storytelling scrollytelling, landing page premium, SVG morphing complesso, sequenze animate multi-step. Prima scelta quando il controllo granulare è prioritario.

---

## [Motion (ex Framer Motion) — Animazioni React/Vue](https://motion.dev)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Motion (l'evoluzione di Framer Motion) è la libreria dominante nell'ecosistema React nel 2026, con supporto Vue aggiunto. Motore ibrido che esegue a 120fps con GPU acceleration. API dichiarativa che si integra nativamente con state e props React — nessuna gestione manuale di keyframe.

**Snippet minimo funzionante:**
```jsx
import { motion, AnimatePresence } from 'motion/react';

// Card con hover e tap feedback
export function AnimatedCard({ children }) {
  return (
    <motion.div
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      exit={{ opacity: 0, scale: 0.95 }}
      whileHover={{ scale: 1.03, boxShadow: '0 20px 40px rgba(0,0,0,0.2)' }}
      whileTap={{ scale: 0.97 }}
      transition={{ type: 'spring', stiffness: 400, damping: 25 }}
    >
      {children}
    </motion.div>
  );
}

// Lista con stagger automatico
export function StaggeredList({ items }) {
  return (
    <motion.ul
      variants={{ show: { transition: { staggerChildren: 0.08 } } }}
      initial="hidden"
      animate="show"
    >
      {items.map(item => (
        <motion.li
          key={item.id}
          variants={{ hidden: { opacity: 0, x: -20 }, show: { opacity: 1, x: 0 } }}
        >
          {item.label}
        </motion.li>
      ))}
    </motion.ul>
  );
}
```

**Quando usarlo:** App React/Next.js, dashboard interactive, e-commerce con transizioni prodotto, qualsiasi interfaccia che necessita di animazioni sincronizzate con lo state dell'app.

---

## [Three.js r171 + WebGPU Renderer](https://www.utsubo.com/blog/threejs-2026-what-changed)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Firefox/Safari 26 (WebGPU Baseline 2026)

WebGPU è diventato Baseline nel 2026 (tutti i major browser lo supportano di default). Three.js r171 ha introdotto `WebGPURenderer` con fallback automatico a WebGL 2 — una riga per migrare. Il nuovo shader system TSL (Three Shading Language) compila sia GLSL che WGSL, eliminando la dualità WebGL/WebGPU. Fino a 10× miglioramento nelle scene draw-call-heavy.

**Snippet minimo funzionante:**
```javascript
import * as THREE from 'three';
import WebGPURenderer from 'three/addons/renderers/webgpu/WebGPURenderer.js';

// Una riga per passare a WebGPU (con fallback automatico a WebGL 2)
const renderer = new WebGPURenderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);

// Sfera con material standard
const geometry = new THREE.SphereGeometry(1, 64, 64);
const material = new THREE.MeshStandardMaterial({
  color: 0x6366f1,
  roughness: 0.2,
  metalness: 0.8,
});
const mesh = new THREE.Mesh(geometry, material);
scene.add(mesh);

// Luce
scene.add(new THREE.DirectionalLight(0xffffff, 2));
scene.add(new THREE.AmbientLight(0x404040));

camera.position.z = 3;

function animate() {
  requestAnimationFrame(animate);
  mesh.rotation.x += 0.005;
  mesh.rotation.y += 0.01;
  renderer.render(scene, camera);
}
animate();
```

**Quando usarlo:** Hero section con oggetti 3D interattivi, product configurator, visualizzazioni dati 3D, esperienze immersive. React Three Fiber (r3f) è l'astrazione React consigliata sopra Three.js.

---

## [Lottie — After Effects sul Web](https://lottiefiles.com)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Lottie converte animazioni After Effects in JSON leggero riproducibile a qualsiasi risoluzione senza perdita qualità. Nel 2026 Webflow ha integrato Lottie direttamente nelle Interactions con GSAP, permettendo scrubbing, play/pause, e trigger scroll senza codice custom. Market share: 8.1% tra le librerie di animazione.

**Snippet minimo funzionante:**
```html
<!-- Via CDN -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/lottie-web/5.12.2/lottie.min.js"></script>

<div id="lottie-container" style="width: 200px; height: 200px;"></div>

<script>
const anim = lottie.loadAnimation({
  container: document.getElementById('lottie-container'),
  renderer: 'svg',
  loop: true,
  autoplay: true,
  path: '/animations/my-animation.json', // file AE esportato
});

// Controllo programmatico
document.querySelector('.btn').addEventListener('click', () => {
  anim.playSegments([0, 30], true); // suona solo i frame 0-30
});
</script>
```

**Quando usarlo:** Icone animate (loading, success, error), illustrazioni interattive, mascotte animate, micro-interazioni su bottoni e toggle. Risorse gratuite su LottieFiles.com. Ideale quando il designer lavora in After Effects.
