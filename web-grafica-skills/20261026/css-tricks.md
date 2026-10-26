# CSS Tricks — Settimana 20261026

## [CSS Scroll-Driven Animations](https://www.sitepoint.com/scrolldriven-css-in-2026-building-carousels-without-javascript/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome ✅ Safari 26 ✅ Firefox ⚠️ (flag) Edge ✅

Anima elementi basandoti sulla posizione di scroll senza JavaScript. Con `animation-timeline: scroll()` e `view()` puoi creare progress bar, fade-in e parallax con solo CSS. Firefox 152 richiede ancora il flag `layout.css.scroll-driven-animations.enabled`.

**Snippet minimo funzionante:**
```css
/* Progress bar in cima alla pagina */
@keyframes grow {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}

.progress-bar {
  position: fixed;
  top: 0; left: 0;
  height: 4px;
  background: #6366f1;
  transform-origin: left;
  animation: grow linear;
  animation-timeline: scroll(root);
}

/* Fade-in di un elemento al suo ingresso nel viewport */
@keyframes fade-in {
  from { opacity: 0; translate: 0 40px; }
  to   { opacity: 1; translate: 0 0; }
}

.card {
  animation: fade-in linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 30%;
}
```

**Quando usarlo:** Progress bar di lettura, reveal di sezioni, effetti parallax, carousel CSS-only.

---

## [CSS Scroll-Triggered Animations (Chrome 145)](https://developer.chrome.com/blog/scroll-triggered-animations)
**Facilità:** ⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome 145 ✅ (altri: in arrivo)

Novità 2026: le `scroll-triggered animations` si differenziano dalle scroll-driven — si avviano quando superi un offset di scroll, ma poi proseguono nel tempo come normali animazioni. Usano la nuova property `animation-trigger`.

**Snippet minimo funzionante:**
```css
@keyframes slide-in {
  from { transform: translateX(-100%); opacity: 0; }
  to   { transform: translateX(0); opacity: 1; }
}

.hero-title {
  animation: slide-in 0.6s ease-out forwards;
  animation-trigger: scroll(root) 300px;
}
```

**Quando usarlo:** Header che si anima una volta raggiunti 300px di scroll, reveal one-shot, onboarding step sequenziali.

---

## [CSS @property — Animare Gradienti e Clip-Path](https://smashingmagazine.com/2024/05/times-need-custom-property-instead-css-variable/)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ⚠️ Safari ⚠️

`@property` registra una custom property con tipo e valore iniziale, rendendola interpolabile in animazioni e transizioni. Sblocca effetti impossibili con le normali `--var`: animazione di gradienti, color wheel, clip-path fluide.

**Snippet minimo funzionante:**
```css
/* Color wheel animato */
@property --hue {
  syntax: '<number>';
  initial-value: 0;
  inherits: false;
}

@keyframes hue-rotate {
  to { --hue: 360; }
}

.rainbow-text {
  --hue: 0;
  color: hsl(var(--hue), 80%, 50%);
  animation: hue-rotate 4s linear infinite;
}

/* Gradiente animato */
@property --stop1 {
  syntax: '<percentage>';
  initial-value: 0%;
  inherits: false;
}

.gradient-bg {
  background: linear-gradient(135deg, #6366f1 var(--stop1), #ec4899 100%);
  animation: shift-gradient 2s ease-in-out infinite alternate;
}

@keyframes shift-gradient {
  to { --stop1: 60%; }
}
```

**Quando usarlo:** Sfondi animati accattivanti, testo multicolore, pulsanti con gradiente che scorre.

---

## [Liquid Glass / Glassmorphism CSS](https://dev.to/devyatov/liquid-glass-on-the-web-6-ways-to-build-it-with-css-and-svg-3m07)
**Facilità:** ⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐⭐ | **Browser:** Chrome ✅ Safari ✅ (-webkit-) Firefox ⚠️

Il "Liquid Glass" di Apple ispira web design 2026. La versione web usa `backdrop-filter: blur()` abbinato a bordi luminosi e highlight per simulare vetro smerigliato. Per la rifrazione vera servono SVG filter (solo Chromium).

**Snippet minimo funzionante:**
```css
.glass-card {
  background: rgba(255, 255, 255, 0.12);
  -webkit-backdrop-filter: blur(16px) saturate(180%) brightness(1.1);
  backdrop-filter: blur(16px) saturate(180%) brightness(1.1);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow:
    0 4px 24px rgba(0, 0, 0, 0.12),
    inset 0 1px 0 rgba(255, 255, 255, 0.4);
  padding: 24px;
}

/* Background richiesto per vedere l'effetto */
.glass-container {
  background: linear-gradient(135deg, #6366f1 0%, #ec4899 100%);
  min-height: 100vh;
}
```

**Quando usarlo:** Cards in overlay su immagini/video, header sticky, modal, widget su sfondi colorati.

---

## [CSS Micro-interactions con :has() e :focus-within](https://css-tricks.com/)
**Facilità:** ⭐⭐⭐⭐ | **Impatto visivo:** ⭐⭐⭐ | **Browser:** Chrome ✅ Firefox ✅ Safari ✅ Edge ✅

Il selettore `:has()` (ora supportato ovunque) permette di reagire a stati di figli dal padre, aprendo micro-interazioni prima impossibili in CSS puro: form che cambiano aspetto quando un input è attivo, card che si trasformano quando l'img è in hover.

**Snippet minimo funzionante:**
```css
/* Form group che si "attiva" quando l'input è in focus */
.form-group {
  transition: background 0.2s, box-shadow 0.2s;
  border-radius: 8px;
  padding: 8px 12px;
}

.form-group:has(input:focus) {
  background: rgba(99, 102, 241, 0.08);
  box-shadow: 0 0 0 2px rgba(99, 102, 241, 0.4);
}

/* Card che scala quando un suo button è in hover */
.card:has(.btn:hover) {
  transform: scale(1.02);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}
```

**Quando usarlo:** Form interattivi, card con CTA, navigazione, ogni volta che lo stato di un figlio deve modificare il padre.
