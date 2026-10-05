# Tool AI per Grafica Web — Settimana 20261005

## [Recraft V4.1 — AI SVG Generator](https://www.recraft.ai/ai-vector-generator)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Tipo:** Web app + API

L'unico modello AI che genera **veri file SVG nativi con path editabili** da prompt testuale. V4.1 (maggio 2026) è 2x più veloce e 13–16% più economico della versione precedente. Ideale per UI icons, loghi, illustrazioni hero e qualsiasi grafica vettoriale che deve scalare infinitamente.

**Come usarlo:**
```
Prompt esempio:
"Minimalist SVG icon of a rocket launching, flat design, 
single color, clean lines, suitable for a SaaS dashboard"

Output: file .svg con path reali, apribile e modificabile in Figma/Illustrator
```

**Workflow pratico:**
1. Vai su recraft.ai → seleziona "SVG Vector"
2. Scrivi il prompt descrivendo stile, colore, uso previsto
3. Scarica il `.svg` e modifica i path in Figma o VS Code
4. Integra direttamente nell'HTML: `<img src="icon.svg">` o inline come `<svg>`

**API (per automazione):**
```javascript
// Via Replicate API
const response = await fetch('https://api.replicate.com/v1/predictions', {
  method: 'POST',
  headers: { 'Authorization': `Token ${REPLICATE_TOKEN}` },
  body: JSON.stringify({
    version: "recraft-ai/recraft-v4-svg",
    input: { prompt: "flat icon of a gear, monochrome, minimal" }
  })
});
```

**Quando usarlo:** Icone UI custom, illustrazioni per landing page, loghi concept, asset vettoriali per design system.

---

## [Framer AI — Prompt-to-Site](https://framer.com/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Tipo:** Web app

Genera siti web responsivi completi da una descrizione testuale in ~30 secondi. Ottimo per mockup rapidi, landing page concept, o come punto di partenza per il design. Esporta codice React pulito.

**Workflow:**
```
1. Framer.com → "New Site" → "Generate with AI"
2. Prompt: "Dark mode portfolio for a 3D artist, 
   minimalist, with showcase grid and contact form"
3. Framer genera layout, colori, tipografia e componenti
4. Personalizza visivamente nel canvas drag-and-drop
5. Pubblica direttamente o esporta il codice
```

**Casi d'uso ideali:**
- Prototipo veloce per il cliente (30 sec vs ore)
- Punto di partenza per siti personali/portfolio
- Generare varianti di design da confrontare

**Quando usarlo:** Proof of concept, landing page rapide, mockup client, iterazioni di design veloci.

---

## [Adobe Firefly — Web & UI Assets](https://firefly.adobe.com/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Tipo:** Web app + integrazione Creative Cloud

Generatore AI di immagini/texture/pattern addestrato su contenuti licensed, quindi **sicuro commercialmente**. Particolarmente potente per: texture per sfondi web, hero images stilizzate, varianti colore di asset esistenti (Generative Recolor).

**Workflow per sfondi web:**
```
Prompt per texture/pattern:
"Abstract flowing gradient texture, deep purple and electric blue, 
smooth waves, suitable for hero section background, high contrast"

Formato consigliato: 1920×1080 per hero desktop, 
                    800×800 per card backgrounds
```

**Feature chiave per web designers:**
- **Generative Fill**: rimuovi/aggiungi elementi in immagini esistenti
- **Generative Recolor** (in Illustrator): cambia palette colori di SVG mantenendo la struttura
- **Text Effects**: titoli con texture organiche (fuoco, marmo, vegetazione)

**Quando usarlo:** Hero images commercialmente sicure, texture per sfondi, varianti grafiche per A/B test, illustrazioni per blog posts.

---

## [Google Flow — AI Creative Platform](https://labs.google/flow)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Tipo:** Web app

Combina Imagen 4 (immagini), Veo 3.1 (video), e Gemini in un'unica interfaccia creativa. Permette di generare immagini, integrarle in brevi video, rimuovere oggetti e organizzare asset in una libreria. Nota: Imagen 4 standard viene deprecato il 17/08/2026, migrazione consigliata a Gemini 3.1 Flash Image.

**Workflow immagini per web:**
```
1. Vai su labs.google/flow
2. Seleziona Imagen 4 Fast (~2.7s/immagine, $0.02/gen)
3. Specifica aspect ratio:
   - 16:9 per hero desktop e thumbnail
   - 9:16 per mobile hero e social stories
   - 1:1 per card e avatar
4. Prompt: "Professional product shot on white background, 
   studio lighting, e-commerce style"
5. Esporta e integra nel sito
```

**Quando usarlo:** Immagini per e-commerce, contenuti social, hero sections personalizzate, prototipi che richiedono foto realistiche prima di una sessione fotografica.
