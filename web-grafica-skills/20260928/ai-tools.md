# Tool AI per Grafica Web — Settimana 20260928

## [Recraft V4.1 — AI Vector Generator](https://www.recraft.ai)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Web app

Il tool AI di riferimento per grafica vettoriale nel 2026. A differenza di Midjourney/Stable Diffusion che generano solo raster, Recraft produce SVG nativi con output vettoriale production-ready. Supporta stili coerenti, brand kit e animazioni.

**Come usarlo:**
```
1. Vai su recraft.ai → crea un progetto
2. Scegli output type: "Vector SVG"
3. Prompt: "minimal icon set, line style, tech startup, indigo color palette"
4. Esporta come SVG ottimizzato
5. Integra direttamente nel codice senza conversioni
```

**Snippet di integrazione:**
```html
<!-- SVG generato da Recraft, ottimizzato con SVGO -->
<img src="icon-hero.svg" alt="Hero icon" width="120" height="120"
     loading="lazy" decoding="async">

<!-- Come background CSS per performance -->
<style>
  .hero-icon {
    background-image: url('hero-illustration.svg');
    background-size: contain;
    background-repeat: no-repeat;
  }
</style>
```

**Quando usarlo:** Illustrazioni hero, icone custom, mascotte brand, pattern di sfondo, elementi decorativi. L'alternativa a Figma per chi non è designer.

---

## [Adobe Firefly — Generazione Asset Web](https://firefly.adobe.com)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Web app + integrazione Photoshop/Illustrator

Firefly nel 2026 integra un modello vettoriale nativo dentro Illustrator con training su contenuti licensed. Genera immagini legally safe per uso commerciale, con stili coerenti e controllo fine dei colori brand.

**Come usarlo per web:**
```
1. Adobe Express → "Genera immagine" → scegli aspect ratio web (16:9, 1:1)
2. Prompt: "flat design hero image, fintech app, blue purple gradient, clean minimal"
3. Usa Generative Fill per estendere immagini esistenti
4. Esporta come WebP ottimizzato per web performance
5. In Illustrator: Text to Vector per icone e illustrazioni SVG
```

**Workflow CSS:**
```css
/* Immagine hero generata con Firefly, ottimizzata */
.hero-bg {
  background-image:
    linear-gradient(135deg, rgba(99, 102, 241, 0.85), rgba(168, 85, 247, 0.85)),
    url('/images/hero-firefly.webp');
  background-size: cover;
  background-position: center;
}
```

**Quando usarlo:** Immagini hero, background section, thumbnail per blog/social, visual per landing page. Ideale per team che già usa Creative Cloud.

---

## [Midjourney v7 — Concept Art e Moodboard](https://midjourney.com)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Web app + Discord

Il migliore per immagini esteticamente raffinate nel 2026. Produce concept art, marketing imagery, mood board e illustrazioni realistiche. Non genera vettori — output solo raster PNG/JPEG ad alta risoluzione.

**Prompting per web design:**
```
Prompt ideale per hero image:
"ultra minimalist web hero section, floating 3D shapes, glass morphism panels,
indigo purple gradient background, soft volumetric lighting, 16:9 --style raw --v 7"

Per componenti UI:
"mobile app UI screen, dark mode, fintech dashboard, clean typography,
data visualization charts, frosted glass cards --ar 9:19.5 --v 7"
```

**Post-processing per web:**
```bash
# Ottimizza per web con sharp (Node.js)
const sharp = require('sharp');

await sharp('midjourney-hero.png')
  .resize(1440, 810)
  .webp({ quality: 85 })
  .toFile('hero.webp');
```

**Quando usarlo:** Concept visivi, moodboard di progetto, immagini background decorative, social media assets. Richiede sempre revisione per adattamento al brand.

---

## [Freepik AI Generator — Asset Stock + AI](https://www.freepik.com/ai)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Web app

200M+ stock assets combinati con generazione AI (Flux, Google Imagen, Kling per video). Nel 2026 è la piattaforma all-in-one per designer che necessitano sia asset pronti che generazione custom.

**Come usarlo:**
```
1. Freepik.com → AI Image Generator → seleziona modello (Flux per realismo, Imagen per illustrazioni)
2. Cerca stock photo esistente → usa "Edit with AI" per modificarla
3. Genera varianti del logo con stili diversi
4. Scarica in formato SVG (vettori) o PNG trasparente (raster)
```

**Snippet integrazione:**
```html
<!-- Asset Freepik ottimizzato per web -->
<picture>
  <source srcset="hero-illustration.avif" type="image/avif">
  <source srcset="hero-illustration.webp" type="image/webp">
  <img src="hero-illustration.png" alt="Hero illustration" loading="lazy">
</picture>
```

**Quando usarlo:** Quando hai bisogno di asset vari in tempi rapidi (illustrazioni, icone, foto, pattern). Abbonamento conveniente per uso professionale continuativo.

---

## [Canva Magic Studio — Design AI No-Code](https://www.canva.com/ai-image-generator/)
**Facilità:** ⭐⭐⭐⭐⭐ (5/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Web app

Il tool più usato per non-designer. Magic Studio nel 2026 genera layout completi da prompt, applica brand kit automaticamente e anima elementi con un click. Esporta in formato ottimizzato per web.

**Come usarlo:**
```
1. Canva → crea design → seleziona dimensione (es. 1920x1080 Hero)
2. Usa "Magic Design" → descrivi il layout desiderato
3. "Magic Animate" → scegli stile animazione per export GIF/video
4. Brand Kit → applica colori e font del brand automaticamente
5. Esporta come PNG ottimizzato o GIF animata
```

**Quando usarlo:** Banner, social media, presentazioni, thumbnail blog. Ideale per team marketing senza designer dedicato.
