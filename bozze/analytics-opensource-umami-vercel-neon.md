---
title: "Analytics open source sul tuo sito: guida completa con Umami, Vercel e Neon"
date: 2026-06-19
description: "Come installare Umami, un sistema di analytics privacy-first, usando un database gratuito su Neon e un deploy automatico su Vercel. Zero cookie, zero Google, dati tuoi."
tags: ["analytics", "privacy", "umami", "vercel", "neon", "tutorial", "open-source"]
level: "beginner"
stato: "bozza — non pubblicare"
---

Google Analytics traccia i tuoi utenti, li profila, condivide i dati con Big Tech e ti obbliga al banner dei cookie. Esiste un'alternativa migliore, gratuita e open source: **Umami**.

In questa guida ti mostro come mettere online la tua dashboard analytics in meno di 30 minuti, senza spendere nulla, senza cookie e con i dati al sicuro nel tuo database.

---

## Cosa costruiamo

Un sistema composto da tre pezzi:

| Componente | Servizio | Costo |
|-----------|----------|-------|
| **Database** | Neon (PostgreSQL cloud) | Gratis |
| **Dashboard** | Umami su Vercel | Gratis |
| **Script** | Snippet nel tuo sito | Gratis |

Alla fine avrai una dashboard all'indirizzo `stats.tuosito.net` con grafici di visite, pagine più lette, dispositivi, paesi — tutto senza mai salvare un cookie sul browser dei tuoi utenti.

---

## Prima di iniziare

Ti servono:
- Un account **GitHub** (gratuito su [github.com](https://github.com))
- Un account **Neon** (gratuito su [neon.tech](https://neon.tech))
- Un account **Vercel** (gratuito su [vercel.com](https://vercel.com)) — puoi registrarti con GitHub
- **Node.js** installato sul tuo computer ([nodejs.org](https://nodejs.org))
- Il terminale — non spaventarti, i comandi sono pochi e semplici

---

## Parte 1 — Il database su Neon

Neon è un database PostgreSQL nel cloud. Umami ci salva dentro tutti i dati delle visite.

### 1.1 Crea l'account

Vai su [neon.tech](https://neon.tech) → **Sign Up** → puoi registrarti con GitHub in un click.

### 1.2 Crea un progetto

Dopo il login:
1. Clicca **"New Project"**
2. **Name:** `umami-analytics` (o come vuoi)
3. **Region:** scegli `EU Central` se i tuoi utenti sono europei
4. Clicca **"Create Project"**

### 1.3 Copia la stringa di connessione

Questa è la parte importante. Neon ti mostrerà una schermata con i dettagli di connessione.

Clicca su **"Connection string"** e copia il testo — sarà qualcosa tipo:

```
postgresql://neondb_owner:passwordsegreta@ep-nome-progetto.c-4.eu-central-1.aws.neon.tech/neondb?sslmode=require
```

> ⚠️ Salvala in un posto sicuro — è come la password del database. Non condividerla mai pubblicamente.

---

## Parte 2 — Umami su Vercel

### 2.1 Installa pnpm

`pnpm` è un gestore di pacchetti Node.js, più veloce di `npm`. Nel terminale:

```bash
npm install -g pnpm
```

Verifica che funzioni:
```bash
pnpm --version
```

### 2.2 Scarica il codice di Umami

```bash
git clone https://github.com/umami-software/umami.git umami-analytics
cd umami-analytics
```

### 2.3 Configura il file .env

Crea un file chiamato `.env` nella cartella `umami-analytics` con questo contenuto:

```env
DATABASE_URL=incolla-qui-la-tua-stringa-di-connessione-neon
APP_SECRET=una-stringa-casuale-lunga-almeno-32-caratteri
```

Per generare l'`APP_SECRET` puoi usare questo comando nel terminale:

```bash
python3 -c "import secrets; print(secrets.token_hex(32))"
```

Copia il risultato e incollalo al posto di `una-stringa-casuale-lunga-almeno-32-caratteri`.

Il file `.env` finale sarà tipo:

```env
DATABASE_URL=postgresql://neondb_owner:passwordsegreta@ep-nome-progetto.c-4.eu-central-1.aws.neon.tech/neondb?sslmode=require
APP_SECRET=a3f7b2c1d9e4f8a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4
```

### 2.4 Abilita le dipendenze

Apri il file `pnpm-workspace.yaml` nella cartella `umami-analytics` e modifica la sezione `allowBuilds` così:

```yaml
allowBuilds:
  '@parcel/watcher': true
  '@prisma/engines': true
  '@swc/core': true
  cypress: false
  esbuild: true
  prisma: true
  sharp: true
ignoredBuiltDependencies:
  - cypress
onlyBuiltDependencies:
  - '@parcel/watcher'
  - '@prisma/client'
  - '@prisma/engines'
  - '@swc/core'
  - esbuild
  - prisma
  - sharp
```

### 2.5 Installa le dipendenze

```bash
pnpm install
```

Attendi qualche minuto — scarica tutto il necessario.

### 2.6 Inizializza il database

Questo comando crea tutte le tabelle nel database Neon:

```bash
DATABASE_URL="incolla-qui-la-stringa-neon" npx prisma migrate deploy
```

Se alla fine vedi **"All migrations have been successfully applied"** sei a posto.

### 2.7 Crea il file vercel.json

Nella cartella `umami-analytics` crea un file `vercel.json` con questo contenuto:

```json
{
  "buildCommand": "pnpm run build",
  "installCommand": "pnpm install",
  "framework": "nextjs"
}
```

### 2.8 Fai il deploy su Vercel

Prima accedi a Vercel dal terminale:

```bash
npx vercel login
```

Ti aprirà il browser per autenticarti — segui le istruzioni.

Poi aggiungi le variabili d'ambiente al progetto Vercel:

```bash
# Dalla cartella umami-analytics
echo "LA-TUA-STRINGA-NEON" | npx vercel env add DATABASE_URL production
echo "IL-TUO-APP-SECRET" | npx vercel env add APP_SECRET production
```

Infine, fai il deploy:

```bash
npx vercel deploy --prod --yes
```

Attendi qualche minuto. Alla fine vedrai un URL tipo:
```
https://umami-analytics-xxxx.vercel.app
```

Questo è il tuo pannello analytics!

---

## Parte 3 — Prima configurazione della dashboard

### 3.1 Accedi

Apri l'URL del deploy nel browser.

- **Username:** `admin`
- **Password:** `umami`

### 3.2 Cambia la password subito

Clicca sull'icona del profilo in alto a destra → **Profile** → cambia la password con una sicura.

### 3.3 Aggiungi il tuo sito

1. Vai su **Settings** (ingranaggio in alto)
2. **Websites** → **Add website**
3. **Name:** il nome del tuo sito (es. `Il mio blog`)
4. **Domain:** il dominio (es. `tuosito.net`)
5. Clicca **Save**

### 3.4 Copia lo script di tracking

Clicca sul sito appena creato → **Edit** → **Tracking code**.

Vedrai uno snippet tipo:

```html
<script defer src="https://umami-analytics-xxxx.vercel.app/script.js" data-website-id="il-tuo-id-univoco"></script>
```

---

## Parte 4 — Inserisci lo script nel sito

### Se usi Hugo

Apri il file `layouts/_default/baseof.html` e aggiungi lo script **prima di `</body>`**:

```html
  <script src="/js/main.js"></script>
  <script defer src="https://umami-analytics-xxxx.vercel.app/script.js" data-website-id="il-tuo-id"></script>
</body>
</html>
```

Poi pubblica:

```bash
git add layouts/_default/baseof.html
git commit -m "Aggiunge tracking Umami"
git push origin main
```

### ⚠️ Se usi un Cloudflare Worker con Content Security Policy

Se il tuo sito passa attraverso un Cloudflare Worker che imposta header di sicurezza (cosa comune e consigliata), devi aggiungere il dominio Umami alla whitelist nella CSP.

Trova nel tuo `src/index.js` (o file equivalente) la riga con `script-src` e aggiorna così:

```javascript
// Prima (blocca tutto ciò che non è 'self')
"script-src 'self'; " +

// Dopo (permette anche Umami)
"script-src 'self' https://umami-analytics-xxxx.vercel.app; " +
```

Fai lo stesso per `connect-src` (serve per inviare i dati):

```javascript
"connect-src 'self' https://umami-analytics-xxxx.vercel.app; " +
```

Salva, committa e pusha. Senza questo passaggio lo script viene bloccato silenziosamente dal browser e non vedrai mai dati nella dashboard.

---

## Parte 5 — Dominio personalizzato (opzionale ma consigliato)

Invece di ricordare `umami-analytics-xxxx.vercel.app`, puoi accedere alla tua dashboard da `stats.tuosito.net`.

### 5.1 Aggiungi il dominio a Vercel

```bash
cd umami-analytics
npx vercel domains add stats.tuosito.net
```

Vercel ti dirà di aggiungere un record DNS tipo:
```
A stats.tuosito.net 76.76.21.21
```

### 5.2 Aggiungi il record DNS

Vai sul pannello del tuo provider DNS (Cloudflare, Infomaniak, ecc.) e aggiungi:

- **Tipo:** A
- **Nome:** `stats`
- **Valore:** `76.76.21.21`
- **Proxy:** disattivato (DNS only, nuvola grigia su Cloudflare)

Dopo qualche minuto `stats.tuosito.net` porterà alla tua dashboard Umami.

---

## Verifica che tutto funzioni

Apri il tuo sito nel browser, poi vai sulla dashboard Umami. Se in tempo reale vedi la tua visita apparire nella sezione **Realtime**, sei a posto.

Se dopo qualche minuto non vedi nulla:

1. **Apri gli strumenti sviluppatore** del browser (F12) → tab **Console**
2. Ricarica la pagina
3. Se vedi errori tipo `Content Security Policy` → hai saltato la Parte 4 ⚠️ sulla CSP
4. Se vedi errori di rete → controlla che l'URL nello script sia quello corretto del tuo deploy Vercel

---

## Perché Umami è meglio di Google Analytics

| Caratteristica | Umami | Google Analytics |
|---------------|-------|-----------------|
| Cookie | ❌ Nessuno | ✅ Molti |
| Banner cookie GDPR | Non serve | Obbligatorio |
| Dati tuoi | ✅ Sul tuo DB | ❌ Su server Google |
| Open source | ✅ | ❌ |
| Gratuito | ✅ | ✅ (piano base) |
| Dashboard semplice | ✅ | ❌ (complessità alta) |
| Peso script | ~2KB | ~45KB |

---

## Costi riepilogati

| Servizio | Piano gratuito include |
|---------|----------------------|
| **Neon** | 0.5 GB storage, 190 ore compute/mese |
| **Vercel** | 100GB banda, deploy illimitati |
| **Umami** | Self-hosted, nessun limite |

Per un blog personale o un sito piccolo/medio, il piano gratuito di entrambi è più che sufficiente.

---

*Hai problemi durante la configurazione? Scrivimi — rispondo a tutti.*
