# Tool AI per Grafica Web — Settimana 20260720

## [Recraft AI — SVG Nativo da Prompt](https://www.recraft.ai)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Web App

Recraft è l'unico generatore AI che produce **veri file SVG** (non raster PNG/JPG): scalabili infinitamente, editabili in Figma o Illustrator, pronti per il web. Eccelle in icone, brand assets, illustrazioni vettoriali e mockup. Classificato #1 su HuggingFace per text-to-image in 2026, con supporto stili custom e brand consistency.

**Come usarlo:**
```
Prompt esempio: "Flat vector icon, minimal, isometric cube with gradient fill 
from indigo to violet, clean lines, no background, SVG style"

Output: file .svg editabile — importa direttamente in Figma o nel codebase

Workflow consigliato:
1. Genera icona/illustrazione su recraft.ai
2. Scarica come SVG
3. Ottimizza con SVGO: npx svgo input.svg -o output.svg
4. Incorpora inline nell'HTML per animarlo con CSS/GSAP
```

**Snippet integrazione SVG animato:**
```html
<!-- SVG generato da Recraft, animato con CSS -->
<svg class="hero-icon" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
  <!-- contenuto generato da Recraft -->
  <path class="icon-path" d="..." fill="url(#gradient)"/>
  <defs>
    <linearGradient id="gradient" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#6366f1"/>
      <stop offset="100%" stop-color="#ec4899"/>
    </linearGradient>
  </defs>
</svg>

<style>
.hero-icon { animation: float 3s ease-in-out infinite; }
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}
</style>
```

**Quando usarlo:** Icone UI personalizzate, illustrazioni hero section, asset per design system, loghi concept. Prima scelta quando il brand richiede scalabilità vettoriale.

---

## [Figma Make — Da Prompt a UI Funzionante](https://www.figma.com/solutions/ai-web-design/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Web App (Figma)

Figma Make trasforma prompt in testo in layout UI completi con HTML/CSS/JavaScript, senza handoff designer→developer. Il 72% dei designer ora usa AI generativo nel workflow (Figma State of Design 2026), e Make è il punto di partenza più adottato. Genera codice pulito ed editabile direttamente in Figma.

**Come usarlo:**
```
Prompt esempio: "Design a SaaS pricing page with 3 tiers: Starter, Pro, Enterprise.
Dark theme, purple accent color, feature comparison table, 
highlight the Pro tier, include a toggle for monthly/annual billing"

Figma Make genera:
- Layout completo con componenti
- HTML + Tailwind CSS esportabile
- Varianti responsive mobile/desktop

Workflow consigliato:
1. Prompt iniziale → layout grezzo
2. Raffina visualmente nel canvas Figma
3. Esporta codice con il plugin DesignFast per HTML/CSS/React/Tailwind
```

**Quando usarlo:** Prototipazione rapida di landing page, generazione wireframe strutturati, iterazione veloce su varianti di design UI prima di investire nel codice.

---

## [Freepik AI Creative Suite — 200M Assets + 39 Modelli](https://www.freepik.com)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Web App

Freepik si è trasformata in una suite AI completa: 200M+ asset (foto, vettori, illustrazioni, template) combinati con AI generativa powered da 39+ modelli (Flux, Google Imagen, Kling per video). È il toolkit all-in-one per chi deve produrre grafica web in volume con coerenza stilistica.

**Come usarlo:**
```
Casi d'uso principali:

1. IMMAGINI HERO: prompt → immagine fotorealistica ottimizzata web
   "Modern coworking space, natural light, minimal design, wide shot, 
   photorealistic, web hero banner 1920x600"

2. ASSET UI: cerca in libreria vettori + personalizza con AI
   Workflow: cerca "gradient background" → seleziona → ricolora con AI Match

3. VARIANTI: genera 4-8 varianti di un'immagine per A/B test
   (funzione Variations integrata)

4. VIDEO LOOP: genera background video con Kling
   "Abstract flowing purple gradient particles, seamless loop, 4K"
```

**Quando usarlo:** Produzione asset in volume (blog, social, landing page multiple), quando si ha bisogno di fotografie + illustrazioni + template in un unico abbonamento. Piano gratuito generoso, Pro da €9/mese.

---

## [Midjourney — Qualità Estetica Massima](https://www.midjourney.com)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Discord + Web App

Midjourney produce le immagini AI esteticamente più raffinate disponibili nel 2026 per concept art, mood board, fotografie hero e illustrazioni. Non genera SVG o codice, ma è insuperabile per la qualità dell'output visivo. Usato come primo step nel workflow: Midjourney → esportazione → ottimizzazione → web.

**Come usarlo:**
```
Prompt avanzato per hero web:
"/imagine prompt: minimalist hero banner for a fintech app, 
abstract geometric shapes, gradient from deep navy to electric blue,
floating glass cards with blur effect, ultra clean, editorial photography style,
high contrast, 16:9 aspect ratio --ar 16:9 --style raw --v 7"

Parametri chiave 2026:
--ar 16:9    → aspect ratio per banner web
--style raw  → meno post-processing, più fedele al prompt  
--v 7        → versione più recente (maggiore coerenza)
--no text    → rimuove testo dall'immagine generata

Workflow web:
1. Genera in Midjourney
2. Ottimizza con Squoosh/ImageOptim (WebP)
3. Implementa con lazy loading + srcset
```

**Quando usarlo:** Immagini hero di alto impatto, mood board per presentazioni cliente, concept visualization, marketing imagery premium. Lo stack comune 2026: Midjourney (generate) + Canva (layout) + Figma (product design).
