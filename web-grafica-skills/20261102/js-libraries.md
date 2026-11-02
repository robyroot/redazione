# Librerie JavaScript per Grafica e Animazioni — Novembre 2026

## [GSAP 3.15 — GreenSock Animation Platform](https://gsap.com)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Lo standard industry per animazioni complesse. Dopo l'acquisizione da parte di Webflow il paywall storico è stato rimosso: ora completamente gratuito per usi commerciali. ScrollTrigger rimane il plugin più potente per scroll animation. Versione attuale: 3.15.

**Snippet minimo funzionante:**
```js
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

gsap.fromTo(".hero-title",
  { opacity: 0, y: 60 },
  {
    opacity: 1, y: 0, duration: 1, ease: "power3.out",
    scrollTrigger: {
      trigger: ".hero-title",
      start: "top 80%",
      end: "top 40%",
      scrub: true
    }
  }
);
```

**Quando usarlo:** animazioni di scroll complesse, timeline sincronizzate, effetti cinematici su landing page premium.

---

## [Anime.js v4.5 — Leggero e MIT](https://animejs.com)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

La v4 ha riscritto l'intera API in modo modulare e tree-shakeable. La v4.4 aggiunge `grid: true` per auto-grid animations; la v4.5 (ottobre 2026) consolida la stabilità. Include `ScrollObserver` nativo (non più solo GSAP). Licenza MIT pura.

**Snippet minimo funzionante:**
```js
import { animate, stagger } from "animejs";

animate(".card", {
  opacity:   [0, 1],
  translateY: [40, 0],
  duration:  600,
  delay:     stagger(80),
  easing:    "easeOutExpo"
});
```

**Snippet con ScrollObserver:**
```js
import { animate, onScroll } from "animejs";

animate(".section", {
  opacity: [0, 1],
  translateX: [-50, 0],
  autoplay: onScroll({ enter: "top 85%", leave: "top 20%" })
});
```

**Quando usarlo:** alternativa leggera a GSAP quando non servono timeline complesse; bundle più piccolo per siti con molte animazioni semplici.

---

## [Three.js r186 — WebGPU + WebXR](https://threejs.org)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Safari 26/Firefox (Windows/Apple Silicon)

r186 (settembre 2026) aggiunge WebXR su WebGPURenderer, illuminazione clusterizzata e un SunLight helper con ombre a cascata. WebGPU è ora baseline in tutti i principali browser; Three.js cade automaticamente su WebGL 2 dove non disponibile. L'Inspector integrato (da r181) facilita il debug in-browser.

**Snippet minimo funzionante:**
```js
import * as THREE from "three";
import { WebGPURenderer } from "three/webgpu";

const renderer = new WebGPURenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

const scene    = new THREE.Scene();
const camera   = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.z = 3;

const mesh = new THREE.Mesh(
  new THREE.TorusKnotGeometry(0.8, 0.3, 100, 16),
  new THREE.MeshPhysicalMaterial({ color: 0x6366f1, roughness: 0.2, metalness: 0.8 })
);
scene.add(mesh);
scene.add(new THREE.DirectionalLight(0xffffff, 2));

renderer.setAnimationLoop(() => {
  mesh.rotation.y += 0.01;
  renderer.render(scene, camera);
});
```

**Quando usarlo:** hero 3D, sfondi interattivi, product showcase, esperienze WebXR.

---

## [Rive — Animazioni State-Machine per il Web](https://rive.app)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Rive porta le state machine nell'animazione web: icone, mascot e bottoni reagiscono a hover, click, dati e scroll in real time con un peso file minimo. Da aprile 2026 si può controllare da Webflow tramite Interactions + GSAP con il sistema data binding delle view model.

**Snippet minimo funzionante:**
```html
<script src="https://unpkg.com/@rive-app/canvas@2"></script>
<canvas id="rive-canvas" width="400" height="400"></canvas>
<script>
  const r = new rive.Rive({
    src: "hero-animation.riv",
    canvas: document.getElementById("rive-canvas"),
    autoplay: true,
    stateMachines: "Main",
    onLoad: () => {
      const inputs = r.stateMachineInputs("Main");
      const hover = inputs.find(i => i.name === "isHovered");
      document.getElementById("rive-canvas").addEventListener("mouseenter", () => hover.value = true);
      document.getElementById("rive-canvas").addEventListener("mouseleave", () => hover.value = false);
    }
  });
</script>
```

**Quando usarlo:** icone animate interattive, loader, mascot/character, bottoni con microanimazioni state-driven.

---

## [Motion (ex Framer Motion) — Animazioni React](https://motion.dev)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

Scelta predefinita per animazioni di UI in React nel 2026. API dichiarativa, layout animations fluide e Framer-ready. Supporta anche vanilla JS con `@motionone/dom`.

**Snippet minimo funzionante:**
```jsx
import { motion } from "motion/react";

export function Card() {
  return (
    <motion.div
      initial={{ opacity: 0, scale: 0.9 }}
      animate={{ opacity: 1, scale: 1 }}
      exit={{ opacity: 0, scale: 0.9 }}
      whileHover={{ y: -4, boxShadow: "0 20px 40px rgba(0,0,0,0.15)" }}
      transition={{ duration: 0.3, ease: [0.25, 0.46, 0.45, 0.94] }}
      className="card"
    />
  );
}
```

**Quando usarlo:** app React/Next.js con transizioni di pagina, modal animati, liste con reorder drag-and-drop.

---

## [Lenis — Smooth Scroll Leggero](https://lenis.darkroom.engineering)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐ | **Browser:** Tutti

Sostituisce lo scroll nativo del browser con uno smooth scrolling inerzia-based. Si integra nativamente con GSAP ScrollTrigger. Bundle ~3KB.

**Snippet minimo funzionante:**
```js
import Lenis from "lenis";

const lenis = new Lenis({ lerp: 0.1, smoothWheel: true });

// Sync con GSAP ScrollTrigger
lenis.on("scroll", ScrollTrigger.update);
gsap.ticker.add((time) => lenis.raf(time * 1000));
gsap.ticker.lagSmoothing(0);
```

**Quando usarlo:** siti portfolio/agency che vogliono scroll fluido premium senza pesantezza di Locomotive Scroll.
