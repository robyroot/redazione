# Design Trends & Componenti UI — Settimana 20260928

## [Tailwind CSS v4.3 — CSS-first Configuration](https://tailwindcss.com)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐ (3/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Tailwind v4 ha eliminato `tailwind.config.js`: tutta la configurazione vive nel CSS con direttive `@theme`. Build 10x più veloci grazie al nuovo engine Lightning CSS (Rust). La v4.3 aggiunge scrollbar styling nativo, container queries first-class e nuove utility `zoom` e `tab-size`.

**Snippet minimo funzionante:**
```css
/* Configurazione CSS-first (sostituisce tailwind.config.js) */
@import "tailwindcss";

@theme {
  --color-brand-primary: #6366f1;
  --color-brand-secondary: #ec4899;
  --font-display: "Clash Display", sans-serif;
  --radius-card: 20px;
  --breakpoint-xs: 480px;
}

/* Container queries native */
@container (min-width: 400px) {
  .card-title {
    font-size: theme(--text-2xl);
  }
}
```

```html
<!-- Utility classes Tailwind v4 -->
<div class="glass-card rounded-card p-6 @container">
  <h2 class="font-display text-xl @md:text-3xl text-brand-primary">
    Titolo responsivo con container query
  </h2>
</div>
```

**Quando usarlo:** Qualunque nuovo progetto web. La migrazione da v3 richiede circa 30 minuti con la CLI di migrazione ufficiale.

---

## [shadcn/ui con Base UI (luglio 2026)](https://ui.shadcn.com)
**Facilità:** ⭐⭐⭐⭐ (4/5) | **Impatto visivo:** ⭐⭐⭐⭐ (4/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Dal luglio 2026 shadcn/ui usa Base UI come default (6M+ downloads/settimana). Base UI v1.8.0 offre primitive headless più flessibili di Radix con API più moderna. Tutti i componenti esistenti rimangono su Radix senza deprecation.

**Snippet minimo funzionante:**
```bash
# Nuovo progetto con Base UI (default da luglio 2026)
npx shadcn@latest init

# Componenti disponibili su entrambi i sistemi
npx shadcn@latest add button
npx shadcn@latest add dialog
npx shadcn@latest add command
```

```tsx
// Componente shadcn/ui — copy-paste ownership
import { Button } from "@/components/ui/button";
import { Dialog, DialogContent, DialogTrigger } from "@/components/ui/dialog";

export function FeatureCard() {
  return (
    <Dialog>
      <DialogTrigger asChild>
        <Button variant="outline" size="lg">
          Scopri di più
        </Button>
      </DialogTrigger>
      <DialogContent className="sm:max-w-[425px]">
        {/* contenuto */}
      </DialogContent>
    </Dialog>
  );
}
```

**Quando usarlo:** Dashboard, app SaaS, design system interno. Non è una libreria — i componenti sono tuoi da personalizzare completamente.

---

## [Variable Fonts + Kinetic Typography](https://web.dev/variable-fonts/)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

I variable fonts hanno raggiunto pieno supporto browser e sono centrali nel 2026 web design. La tecnica emergente: mappare il peso/larghezza del font alla posizione di scroll per una tipografia cinematica. WCAG 3.0 impone contrasto accessibile anche su variabili.

**Snippet minimo funzionante:**
```css
/* Font variabile da Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Encode+Sans:wght@100..900&display=swap');

/* Fluid typography con clamp() */
:root {
  --text-hero: clamp(2.5rem, 6vw + 1rem, 8rem);
}

/* Kinetic typography scroll-driven */
@property --font-weight {
  syntax: '<number>';
  inherits: false;
  initial-value: 400;
}

@keyframes weight-up {
  from { --font-weight: 100; }
  to   { --font-weight: 900; }
}

.hero-title {
  font-family: 'Encode Sans', sans-serif;
  font-variation-settings: 'wght' var(--font-weight);
  font-size: var(--text-hero);
  animation: weight-up linear both;
  animation-timeline: view();
  animation-range: entry 0% cover 50%;
}
```

**Quando usarlo:** Hero sections, heading animati, titoli di sezione. Combina scroll-driven animations con @property per effetti cinematici.

---

## [Tactile Brutalism — Design Trend 2026](https://fireart.studio/blog/the-best-web-design-trends/)
**Facilità:** ⭐⭐⭐ (3/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Controtendenza all'UI perfetto: bordi raw, asimmetria intenzionale, elementi sketch-like, imperfezioni umane. Combinato con "Invisible Architecture" (UI che scompare, focus sul contenuto). Dopamine design con colori saturi Y2K.

**Snippet minimo funzionante:**
```css
/* Brutalist card con bordo raw */
.brutalist-card {
  background: #fef08a; /* giallo carico Y2K */
  border: 3px solid #1a1a1a;
  border-radius: 4px;
  box-shadow: 6px 6px 0 #1a1a1a; /* shadow netto, no blur */
  padding: 24px;
  transition: transform 120ms ease, box-shadow 120ms ease;
}

.brutalist-card:hover {
  transform: translate(-3px, -3px);
  box-shadow: 9px 9px 0 #1a1a1a;
}

/* Griglia broken (non regolare) */
.broken-grid {
  display: grid;
  grid-template-columns: 1fr 1.7fr 0.8fr;
  grid-template-rows: auto;
  gap: 16px;
}

.broken-grid > :nth-child(2) {
  grid-row: span 2;
  margin-top: -40px; /* offset intenzionale */
}
```

**Quando usarlo:** Portfolio creativi, brand giovani e anticonvenzionali, landing page che vogliono distinguersi dall'UI standardizzato. Non adatto a fintech/healthcare/enterprise.

---

## [3D Immersive con React Three Fiber](https://docs.pmnd.rs/react-three-fiber)
**Facilità:** ⭐⭐ (2/5) | **Impatto visivo:** ⭐⭐⭐⭐⭐ (5/5) | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

I siti top nel 2026 usano profondità e interazione 3D: modelli interattivi, scroll-triggered 3D, AR preview. React Three Fiber (R3F) è la scelta standard per integrazione con ecosistema React, con Drei per componenti pronti.

**Snippet minimo funzionante:**
```jsx
// React Three Fiber — hero 3D interattivo
import { Canvas, useFrame } from '@react-three/fiber';
import { Float, MeshDistortMaterial, OrbitControls } from '@react-three/drei';

function FloatingBlob() {
  return (
    <Float speed={2} rotationIntensity={0.5} floatIntensity={1}>
      <mesh>
        <sphereGeometry args={[2, 64, 64]} />
        <MeshDistortMaterial
          color="#6366f1"
          distort={0.4}
          speed={2}
          roughness={0.1}
          metalness={0.8}
        />
      </mesh>
    </Float>
  );
}

export function HeroScene() {
  return (
    <Canvas camera={{ position: [0, 0, 6], fov: 45 }}>
      <ambientLight intensity={0.5} />
      <pointLight position={[10, 10, 10]} intensity={1} />
      <FloatingBlob />
      <OrbitControls enableZoom={false} enablePan={false} />
    </Canvas>
  );
}
```

**Quando usarlo:** Hero sections premium, product showcase 3D, portfolio interattivi, siti award-worthy. Richiede ottimizzazione per mobile (LOD, shadow quality).
