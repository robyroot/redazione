# Web Grafica Skills — Settimana 20260720

## 🏆 Top 3 scoperte della settimana

1. **CSS Scroll-Triggered Animations (Chrome 145)** — La svolta più importante: animazioni on-scroll senza IntersectionObserver, senza JavaScript, compositing GPU. Combinato con View Transitions API, copre il 90% degli use case per cui prima serviva GSAP/AOS. Il browser ha vinto.

2. **Three.js r171 + WebGPU Baseline** — WebGPU è ora ufficialmente supportato da *tutti* i major browser (Baseline 2026). Una riga per migrare da WebGL a WebGPU, 10× performance in scene complesse, shader system TSL cross-renderer. La 3D sul web entra finalmente nell'era moderna.

3. **Recraft AI — SVG Nativi da Prompt** — L'unico generatore AI che produce veri file SVG editabili (non PNG). Icone, illustrazioni, brand assets pronti per Figma e per il web, scalabili infinitamente. Classificato #1 su HuggingFace per text-to-image. Game changer per i workflow di design.

---

## Contenuto questa settimana

- [css-tricks.md](css-tricks.md) — 4 tecniche CSS
  - Scroll-Triggered Animations (Chrome 145)
  - CSS @property per gradient border animati
  - Glassmorphism 2.0 / Liquid Glass
  - View Transitions API per micro-interactions

- [js-libraries.md](js-libraries.md) — 4 librerie JS
  - GSAP (ora MIT, gold standard timeline)
  - Motion (ex Framer Motion, React/Vue)
  - Three.js r171 + WebGPURenderer
  - Lottie + integrazione GSAP Webflow

- [ai-tools.md](ai-tools.md) — 4 tool AI
  - Recraft AI (SVG nativi, #1 HuggingFace)
  - Figma Make (prompt → UI + codice)
  - Freepik AI Suite (200M assets + 39 modelli)
  - Midjourney v7 (qualità estetica massima)

- [trends.md](trends.md) — 5 trend design
  - Tailwind CSS v4.3 (Oxide engine, scrollbar utilities)
  - shadcn/ui → Base UI (default da luglio 2026)
  - Tactile Brutalism (il nuovo aesthetic premium)
  - Bento Grid Layout (Apple/Linear/Vercel pattern)
  - Variable Fonts (performance + tipografia adattiva)

---

## Highlight della settimana

Il web design di luglio 2026 è segnato da una dicotomia interessante: da un lato il browser diventa sempre più potente con API native (View Transitions, Scroll-Driven Animations, WebGPU Baseline) che riducono la dipendenza dalle librerie JS; dall'altro l'AI entra stabilmente nel workflow con strumenti come Figma Make e Recraft che accelerano la produzione di asset e prototipi. Sul fronte aesthetico, il Tactile Brutalism sta scalzando il soft UI degli anni 2020-24, portando bordi netti, tipografia stark e contrasto elevato come segnali di qualità ingegneristica. shadcn/ui completa la transizione verso Base UI come default, mentre Tailwind v4.3 consolida la sua dominanza con l'engine Rust e le utility scrollbar. Il messaggio chiave: meno librerie, più piattaforma; meno tempo su asset, più AI generativa.
