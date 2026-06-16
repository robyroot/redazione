---
title: "Chrome zero-day n.5 del 2026: aggiorna il browser adesso"
rilevanza: "ALTA — attivamente sfruttata, colpisce tutti gli utenti Chrome/Chromium"
fonte: "https://helpnetsecurity.com/2026/06/09/google-chrome-zero-day-cve-2026-11645/"
fonti_secondarie:
  - "https://thehackernews.com/2026/06/chrome-v8-zero-day-cve-2026-11645.html"
  - "https://www.bleepingcomputer.com/news/security/google-patches-fifth-chrome-zero-day-bug-exploited-in-attacks-this-year/"
  - "https://socradar.io/blog/cve-2026-11645-chrome-v8-bug/"
data_notizia: "8-9 giugno 2026"
tags: ["chrome", "sicurezza", "cve", "browser", "zero-day"]
livello: "beginner"
nota_editoriale: |
  Articolo urgente, accessibile anche ai non tecnici.
  Enfatizzare che vale per Chrome, Edge, Brave, Opera, Vivaldi (tutti Chromium).
  Includere i comandi di verifica versione su Linux.
  Angolo interessante: 5 zero-day in 6 mesi è un pattern, non un caso isolato.
---

Se stai leggendo questo su Chrome — o su un browser basato su Chromium come Edge, Brave, Opera, Vivaldi — fermati un secondo e aggiorna. Sul serio.

Il 9 giugno 2026 Google ha rilasciato una patch di emergenza per **CVE-2026-11645**, una vulnerabilità critica nel motore JavaScript V8 di Chrome che è già sfruttata attivamente da attaccanti reali. È il **quinto zero-day di Chrome nel 2026**. Ci siamo a metà anno.

## Cos'è successo

La vulnerabilità è un **out-of-bounds read/write** in V8, il motore che esegue JavaScript (e WebAssembly) all'interno di Chrome. In parole semplici: un bug nella gestione della memoria che permette a codice JavaScript malevolo di leggere o scrivere in aree di memoria dove non dovrebbe.

L'impatto: un attaccante può costruire una pagina HTML trappola e, quando la visiti, eseguire codice arbitrario all'interno del sandbox del browser. Non serve cliccare su niente di strano. Basta caricare la pagina.

CVSS score: **8.8** su 10. Classificato come alta severità.

Il ricercatore anonimo che ha scoperto la falla l'ha segnalata a Google il 27 aprile. Ha ricevuto un reward di $55.000. Google ha confermato che l'exploit era già in circolazione prima del rilascio della patch.

## Chi è colpito

Tutti gli utenti di browser basati su Chromium con versione inferiore a **149.0.7827.103** (Windows/Mac) o **149.0.7827.102** (Linux):

- Google Chrome
- Microsoft Edge
- Brave Browser
- Opera
- Vivaldi
- Samsung Internet

Firefox e Safari non sono vulnerabili (usano motori diversi da V8).

## Come verificare la versione e aggiornare

### Chrome, Edge, Brave, Opera

Vai su `Impostazioni → Guida → Informazioni su Chrome` (o il browser equivalente). Il browser scarica automaticamente l'aggiornamento e ti chiede di riavviare.

In alternativa, vai direttamente in: `chrome://settings/help`

### Su Linux via terminale

```bash
# Verifica versione Chrome
google-chrome --version

# Aggiornamento (Ubuntu/Debian)
sudo apt update && sudo apt upgrade google-chrome-stable

# Aggiornamento (Fedora)
sudo dnf upgrade google-chrome-stable

# Brave su Ubuntu
sudo apt update && sudo apt upgrade brave-browser
```

La versione sicura è **149.0.7827.102 o superiore**.

## Il pattern preoccupante: 5 zero-day in 6 mesi

Uno zero-day isolato è un incidente. Cinque in sei mesi sono un segnale.

Chrome è il browser più usato al mondo, con una quota di mercato superiore al 65%. Questo lo rende il bersaglio più attraente per i ricercatori (e per chi vende exploit). Ma la frequenza di zero-day sfruttati in the wild nel 2026 è comunque insolita.

Cosa fare beyond l'aggiornamento immediato:

1. **Abilita gli aggiornamenti automatici** — Chrome di solito si aggiorna da solo, ma su Linux a volte richiede intervento manuale
2. **Considera un browser con hardening extra** — Brave ha configurazioni di sicurezza più aggressive di default
3. **Site isolation attiva** — Chrome 149 la ha abilitata per default, ma puoi verificarla in `chrome://flags/#enable-site-per-process`

Aggiorna adesso. Un minuto di riavvio del browser vale più di un'ora di preoccupazioni dopo.

---
**CVE**: CVE-2026-11645 | **CVSS**: 8.8 | **Versione sicura**: Chrome 149.0.7827.102+
