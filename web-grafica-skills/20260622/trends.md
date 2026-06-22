# Design Trends & Componenti UI — Settimana 20260622

## [Tailwind CSS v4.3](https://tailwindcss.com/)
**Facilità:** ⭐⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

La release più importante nella storia di Tailwind. Configurazione **CSS-first** con `@theme` (addio `tailwind.config.js`), engine Lightning CSS (build 5× più veloce, rebuild in millisecondi), rilevamento automatico dei contenuti. v4.2 (febbraio 2026): plugin Webpack, 4 nuove palette. v4.3: scrollbar styling nativo, `zoom` e `tab-size` utilities.

**Snippet minimo funzionante:**
```css
/* CSS-first config */
@import "tailwindcss";

@theme {
  --color-brand-500: oklch(65% 0.2 250);
  --font-display: 'Inter', sans-serif;
  --radius-card: 1rem;
}
```
```html
<!-- Container queries built-in -->
<div class="@container">
  <div class="grid @md:grid-cols-2 @xl:grid-cols-3 gap-4">...</div>
</div>

<!-- not-* variant (v4 new) -->
<button class="bg-blue-500 not-hover:opacity-80">Click</button>

<!-- Scrollbar styling nativo (v4.3) -->
<div class="overflow-y-auto scrollbar-thin scrollbar-thumb-gray-400">...</div>
```

**Quando usarlo:** Ogni nuovo progetto frontend 2026. Migrazione v3→v4 assistita da `@tailwindcss/upgrade`.

---

## [shadcn/ui — CLI v4 e Base UI](https://ui.shadcn.com/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti

La libreria componenti più usata nel 2026 evolve su tre fronti: supporto **Base UI** (MUI) come alternativa a Radix, pacchetto `radix-ui` unificato (febbraio 2026), CLI v4 con scaffolding per Next.js/Vite/Astro/Laravel. Radix UI ha rallentato dopo acquisizione WorkOS; Base UI è ora più attivamente mantenuto.

**Snippet minimo funzionante:**
```bash
npx shadcn@latest init --template nextjs-app
npx shadcn@latest add card button
```
```jsx
import { Card, CardHeader, CardTitle, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';

export function PricingCard({ plan, price, features }) {
  return (
    <Card className="rounded-2xl border-2 border-brand-500/20 hover:border-brand-500/60 transition-colors duration-300">
      <CardHeader>
        <CardTitle className="text-2xl font-bold">{plan}</CardTitle>
      </CardHeader>
      <CardContent>
        <p className="text-4xl font-black">${price}<span className="text-base font-normal">/mo</span></p>
        <ul className="mt-4 space-y-2">
          {features.map(f => <li key={f}>✓ {f}</li>)}
        </ul>
        <Button className="w-full mt-6">Get started</Button>
      </CardContent>
    </Card>
  );
}
```

**Quando usarlo:** Ogni progetto React/Next.js che necessita di componenti accessibili e customizzabili.

---

## [Bento Grid Layout](https://www.figma.com/resource-library/web-design-trends/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Il pattern UI dominante nel 2026: griglia modulare asimmetrica ispirata ai lunch box giapponesi. Celle di dimensioni diverse, contenuto misto (testo, immagini, widget). Usato da Apple, Linear, Vercel, Stripe.

**Snippet minimo funzionante:**
```css
.bento {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
  grid-template-areas:
    "a a b c"
    "a a d d"
    "e f f d";
}
.bento-a { grid-area: a; }
.bento-b { grid-area: b; }
.bento-c { grid-area: c; }
.bento-d { grid-area: d; }
.bento-e { grid-area: e; }
.bento-f { grid-area: f; }

.bento > * {
  background: #f8f8f8;
  border-radius: 1.5rem;
  padding: 1.5rem;
  border: 1px solid rgba(0,0,0,0.06);
}

@media (max-width: 768px) {
  .bento {
    grid-template-columns: 1fr 1fr;
    grid-template-areas: "a a" "b c" "d d" "e f";
  }
}
```

**Quando usarlo:** Feature section, dashboard overview, portfolio, pricing comparison.

---

## [Dark Mode First + oklch()](https://blog.tubikstudio.com/ui-design-trends-2026/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Tutti moderni

Oltre l'80% degli utenti mobile usa dark mode. Workflow 2026: dark-first, poi si deriva il chiaro. `oklch()` produce palette percettivamente uniformi — stessa luminosità percepita su tutti i toni.

**Snippet minimo funzionante:**
```css
:root {
  --brand-100: oklch(95% 0.05 250);
  --brand-500: oklch(60% 0.20 250);
  --brand-900: oklch(25% 0.15 250);

  color-scheme: dark light;
  --bg: var(--brand-900);
  --text: var(--brand-100);
}
@media (prefers-color-scheme: light) {
  :root {
    --bg: var(--brand-100);
    --text: var(--brand-900);
  }
}
body { background: var(--bg); color: var(--text); }
```

**Quando usarlo:** Sempre — adottare oklch per qualsiasi nuova palette. Dark-first per prodotti tech/SaaS.

---

## [Bold Typography + Variable Fonts](https://midrocket.com/en/guides/ui-design-trends-2026/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Tutti

Il testo è grafica nel 2026: headline oversized, font variabili che cambiano peso con hover, gradient text. `clamp()` per tipografia fluida, `font-variation-settings` per animare il peso.

**Snippet minimo funzionante:**
```css
.title-animated {
  font-family: 'Inter', sans-serif;
  font-size: clamp(3rem, 8vw, 8rem);
  font-variation-settings: 'wght' 100;
  transition: font-variation-settings 0.4s ease;
  line-height: 1;
  letter-spacing: -0.03em;
}
.title-animated:hover {
  font-variation-settings: 'wght' 900;
}

/* Testo con gradient (2026 staple) */
.gradient-text {
  background: linear-gradient(135deg, #6366f1, #8b5cf6, #ec4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

**Quando usarlo:** Hero headline, section title, brand statement — testo che deve fare impatto visivo immediato.

---

## [React Three Fiber — 3D Interattivo](https://docs.pmnd.rs/react-three-fiber/)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome/Edge/Firefox/Safari

Il trend più avanzato del 2026: elementi 3D che reagiscono al cursore o allo scroll, rendered via Three.js in JSX. R3F (React Three Fiber) porta Three.js nel paradigma React con hooks e componenti dichiarativi.

**Snippet minimo funzionante:**
```jsx
import { Canvas, useFrame } from '@react-three/fiber';
import { useRef } from 'react';

function RotatingMesh() {
  const mesh = useRef();
  useFrame((state) => {
    mesh.current.rotation.x = state.mouse.y * 0.3;
    mesh.current.rotation.y = state.mouse.x * 0.3;
  });
  return (
    <mesh ref={mesh}>
      <boxGeometry args={[2, 2, 2]} />
      <meshStandardMaterial color="#6366f1" metalness={0.8} roughness={0.2} />
    </mesh>
  );
}

export function Hero3D() {
  return (
    <Canvas camera={{ position: [0, 0, 5] }}>
      <ambientLight intensity={0.5} />
      <directionalLight position={[10, 10, 5]} />
      <RotatingMesh />
    </Canvas>
  );
}
```

**Quando usarlo:** Hero section premium, product showcase, portfolio creativo. Sempre prevedere fallback statico per mobile.
