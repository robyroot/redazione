# Tool AI per Grafica Web — Aggiornamento 20260803

## [Recraft — SVG Nativo da Testo](https://recraft.ai/)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Web app

Il modello di diffusione di Recraft genera SVG nativi — non raster convertiti in vettore — capendo curve di Bézier e topologia dei path. Nel 2026, produce SVG puliti ed editabili che competono con quelli disegnati a mano. Punto di svolta rispetto al workflow Midjourney → vectorizzatore → pulizia manuale.

**Come usarlo:**
```
# Prompt efficaci per Recraft SVG:
"minimal flat icon of a coffee cup, single color, clean paths, SVG style"
"abstract geometric background pattern, navy and gold, SVG, scalable"
"isometric illustration of a server rack, vector style, clean lines"

# Export workflow:
1. Genera su recraft.ai scegliendo output "SVG"
2. Scarica il file .svg
3. Ottimizza con SVGO: npx svgo input.svg -o output.svg
4. Incorpora inline in HTML o usa come <img src="...svg">
```

**Snippet di integrazione:**
```html
<!-- SVG inline per animazioni CSS -->
<div class="icon-wrapper">
  <!-- Incolla qui l'SVG generato da Recraft -->
  <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path d="M12 2L2 7l10 5 10-5-10-5z" fill="currentColor"/>
    <!-- ... altri path generati da AI ... -->
  </svg>
</div>

<style>
/* L'SVG inline è animabile via CSS */
.icon-wrapper:hover svg path {
  fill: #6366f1;
  transition: fill 200ms ease;
}
</style>
```

**Quando usarlo:** Icone di prodotto, pattern decorativi, illustrazioni hero, asset grafici per UI. Sostituisce il workflow png→trace in Illustrator risparmiando ore di lavoro.

---

## [Spline AI — Modelli 3D Web da Testo](https://spline.design/)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Web app + embed via `<iframe>` o SDK

Spline AI genera modelli 3D interattivi e web-ready da prompt testuali. Si descrive la scena ("a floating isometric server rack with glowing neon cables") e l'AI costruisce modello, materiali e luci. Esporta direttamente come componente React o snippet `<iframe>` embeddabile.

**Come usarlo:**
```
# Workflow Spline AI:
1. Vai su spline.design e crea un nuovo file
2. Usa AI Generate: "a glossy 3D abstract blob, purple gradient, floating"
3. Aggiungi interazioni hover/click nell'editor visuale
4. Esporta → React Component o Public URL

# React Component export:
npm install @splinetool/react-spline @splinetool/runtime
```

**Snippet di integrazione:**
```jsx
// React embed (da export Spline)
import Spline from '@splinetool/react-spline';

export default function HeroBackground() {
  return (
    <div style={{ position: 'absolute', inset: 0, zIndex: -1 }}>
      <Spline
        scene="https://prod.spline.design/YOUR-SCENE-ID/scene.splinecode"
        style={{ width: '100%', height: '100%' }}
      />
    </div>
  );
}

// Oppure iframe semplice:
// <iframe src='https://my.spline.design/YOUR-SCENE-ID/' frameborder='0'
//   width='100%' height='100%'></iframe>
```

**Quando usarlo:** Hero section con oggetti 3D interattivi, sfondi animati, product visualizer, qualsiasi sito che voglia l'effetto "wow" 3D senza scrivere Three.js da zero.

---

## [Workik — AI CSS Animation Generator](https://workik.com/css-animation-code-generator)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Web app

Genera animazioni CSS complete (keyframes, transition, scroll-driven) partendo da una descrizione testuale. Output pronto per la produzione con opzioni per timing, easing, e target CSS specifici. Utile per prototipare rapidamente micro-interazioni.

**Come usarlo:**
```
# Esempi di prompt efficaci:
"button with ripple effect on click, CSS only, no JavaScript"
"card flip animation on hover, 3D perspective, front and back"
"loading spinner with gradient stroke, 1.5s loop"
"text scramble reveal animation, monospace font, hacker style"
```

**Snippet di output tipico:**
```css
/* Esempio output per "glowing button" */
@keyframes pulse-glow {
  0%, 100% {
    box-shadow:
      0 0 5px rgba(99, 102, 241, 0.4),
      0 0 20px rgba(99, 102, 241, 0.2);
  }
  50% {
    box-shadow:
      0 0 15px rgba(99, 102, 241, 0.8),
      0 0 40px rgba(99, 102, 241, 0.4);
  }
}

.glow-btn {
  background: #6366f1;
  color: white;
  border: none;
  padding: 12px 28px;
  border-radius: 8px;
  cursor: pointer;
  animation: pulse-glow 2s ease-in-out infinite;
}
```

**Quando usarlo:** Prototipazione rapida di micro-interazioni, generazione di keyframes complessi da testare, ispirazione per effetti CSS avanzati.

---

## [AI SVG Vector Models — Diffusione Nativa 2026](https://www.svggenie.com/)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** API + Web tools

Nel 2026, i modelli di diffusione "vector-native" generano path SVG direttamente — capendo topologia Bézier — invece di convertire raster in vettore. L'output è pulito, editabile, e pronto per animazioni CSS/JS.

**Workflow consigliato:**
```bash
# 1. Genera SVG con tool AI (Recraft, SVGenie, ecc.)
# 2. Ottimizza con SVGO
npm install -g svgo
svgo input.svg --multipass -o output.svg

# 3. Analizza i path (utile per animazioni)
# Ogni <path> avrà un ID per animarlo indipendentemente

# 4. Aggiungi animazione CSS ai path
```

**Snippet per animare SVG generato da AI:**
```css
/* Animazione "draw" su path SVG generato da AI */
.ai-svg path {
  stroke-dasharray: 1000;
  stroke-dashoffset: 1000;
  animation: draw-path 2s ease forwards;
}

@keyframes draw-path {
  to { stroke-dashoffset: 0; }
}

/* Stagger per path multipli */
.ai-svg path:nth-child(1) { animation-delay: 0ms; }
.ai-svg path:nth-child(2) { animation-delay: 200ms; }
.ai-svg path:nth-child(3) { animation-delay: 400ms; }
```

**Quando usarlo:** Logo animation, illustrazioni hero animate, icone con effetti "reveal drawing", qualsiasi asset SVG che deve essere animato dopo la generazione AI.

---

## [Canva Magic Studio — Full Suite AI Design](https://www.canva.com/magic-studio/)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Web app

La suite AI di Canva (Magic Design, Magic Layers, Magic Resize) genera template completi per social, landing page e marketing. Nel 2026 supporta output vettoriale nativo, tipografia production-ready e stile personalizzato. Piano free disponibile, pro a $15/mese.

**Workflow per web:**
```
# Asset generation workflow:
1. Magic Design: descrivi il brand → genera varianti layout
2. Magic Layers: separa elementi in layer editabili
3. Esporta come SVG (elementi grafici) o PNG @3x (foto/texture)
4. Per animazioni: usa Magic Animate → esporta come MP4/GIF/Lottie
5. Importa in Figma/codice per integrazione finale

# Nota: gli export SVG di Canva spesso contengono testo come path
# → converte font prima dell'export per massima compatibilità
```

**Quando usarlo:** Generazione rapida di asset marketing (OG images, hero illustrations, icone decorative), mockup di sezioni UI, placeholder grafici professionali durante il development.
