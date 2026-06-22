# AI Tools per Grafica Web — Settimana 20260622

## [Figma Make — AI Web Design](https://www.figma.com/solutions/ai-web-design/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Tipo:** Layout + codice

Il 72% dei designer usa AI generativa nel 2026 (Figma State of the Designer 2026). Figma Make genera layout completi da prompt, esporta React/HTML/Tailwind e pubblica direttamente. Integrato con il design system esistente.

**Workflow tipico:**
```
1. Prompt: "Landing page SaaS con hero, features bento grid, pricing table — palette viola/bianco"
2. Figma genera layout con varianti mobile/desktop
3. Raffinamento visivo nel canvas
4. Export React/Tailwind o HTML+CSS
5. Publish con un click
```

**Quando usarlo:** Prototipazione rapida, pitch deck visivi, generazione varianti A/B di layout.

---

## [Midjourney v7 — Immagini Hero e Asset](https://www.midjourney.com/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Tipo:** Image generation

Per hero image e asset visivi supera la stock photography per molti use case nel 2026. `--sref` per stili coerenti, `--cref` per character consistency.

**Prompt efficace per web:**
```
photorealistic product on white background, studio lighting,
minimalist composition, ultra-sharp, 4K --ar 16:9 --style raw --v 7

# Per sfondo hero astratto:
aurora gradient abstract background, purple indigo teal,
soft bokeh depth, dark mode, web hero --ar 3:2 --v 7
```

**Quando usarlo:** Hero section, thumbnail blog, avatar team, texture sfondi, illustrazioni premium.

---

## [Framer AI](https://www.framer.com/ai/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Tipo:** Site builder AI

AI agent integrato in Framer: genera layout, sezioni e stile da prompt direttamente sul canvas. Animazioni scroll/hover già integrate nell'output. Click su qualsiasi elemento per editarlo visualmente.

**Workflow tipico:**
```
Prompt → struttura con sezioni → sostituzione contenuti → animazioni già configurate → publish
```

**Quando usarlo:** Portfolio, landing page evento, siti vetrina — qualità Framer senza partire da zero.

---

## [Aurora Gradient Generator — SyntaxSnap](https://syntaxsnap.com/tools/aurora-gradient)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Tipo:** CSS generator (gratuito)

L'effetto Aurora — blob radiali sfumati con blur elevato — è il background dominante sui SaaS e AI landing page nel 2026. Il tool genera CSS + HTML Tailwind pronto per Next.js/Astro, calcolando blur radius e keyframe ottimali.

**Snippet output tipico:**
```html
<div class="relative overflow-hidden bg-black min-h-screen">
  <div class="absolute inset-0">
    <div class="absolute top-0 left-1/4 w-96 h-96
                rounded-full bg-violet-500/30
                blur-[120px] animate-aurora-1"></div>
    <div class="absolute top-1/3 right-1/4 w-80 h-80
                rounded-full bg-cyan-400/25
                blur-[100px] animate-aurora-2"></div>
  </div>
  <div class="relative z-10">[contenuto]</div>
</div>
```
```css
@keyframes aurora-1 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  50%       { transform: translate(30px, -20px) scale(1.1); }
}
```

**Quando usarlo:** Hero dark di AI products, SaaS landing page, dashboard hero — estetica "premium AI aesthetic".

---

## [CSS Gradient Mesh Generator](https://littleblueinsight.com/tool/technology/css-gradient-mesh-generator/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Tipo:** CSS generator (gratuito)

Gradienti mesh multi-radiali con blur alto per effetti fluidi organici. Alternativa calda all'Aurora, funziona bene su sfondi chiari.

**Snippet minimo funzionante:**
```css
.mesh-bg {
  background:
    radial-gradient(ellipse at 20% 50%, rgba(120,119,198,0.3) 0%, transparent 50%),
    radial-gradient(ellipse at 80% 20%, rgba(255,100,130,0.3) 0%, transparent 50%),
    radial-gradient(ellipse at 50% 80%, rgba(50,200,150,0.3) 0%, transparent 50%),
    #fafafa;
}
```

**Quando usarlo:** Feature section, "About" page, sfondo organico colorato come alternativa a pattern geometrici.

---

## [Canva Magic Studio](https://www.canva.com/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Tipo:** Design AI completo

Il tool più usato dai non-designer nel 2026. Magic Write per testi, Magic Media per immagini AI, Magic Resize per multi-formato. Workflow: prompt → immagine AI → layout → export PNG/SVG → Figma/codice.

**Quando usarlo:** Social media asset, thumbnail, banner email, immagini blog — produzione visiva rapida senza skill avanzate.
