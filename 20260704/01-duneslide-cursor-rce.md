---
title: "DuneSlide: due falle critiche in Cursor permettono di eseguire codice arbitrario via prompt injection"
rilevanza: "ALTA"
fonte: "https://www.catonetworks.com/blog/duneslide-two-critical-rce-vulnerabilities/"
data_notizia: "2026-07-01"
tags: ["sicurezza", "AI", "cursor", "vulnerabilità", "prompt-injection", "sviluppo"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: tema caldo all'incrocio tra AI e sicurezza. I lettori sviluppatori che usano Cursor (o altri AI editor) devono sapere che la superficie d'attacco si è allargata enormemente. Il fatto che un file di progetto scaricato da GitHub possa diventare un vettore RCE è una notizia concreta e urgente.
---

# DuneSlide: quando il tuo AI editor diventa un'arma contro di te

I ricercatori di Cato AI Labs hanno reso pubbliche il 1° luglio 2026 due vulnerabilità critiche nell'editor di codice Cursor, tracciate come **CVE-2026-50548** e **CVE-2026-50549** e ribattezzate collettivamente **DuneSlide**. Il punteggio CVSS è 9.8 su 10 — praticamente il massimo — e il vettore d'attacco è inquietante: un semplice prompt malevolo nascosto in un file di progetto può sfuggire alla sandbox dell'editor ed eseguire qualsiasi comando sul computer dello sviluppatore.

## Come funziona l'attacco

Per capire DuneSlide bisogna prima capire come funzionano gli agenti AI negli editor moderni. Cursor, come altri strumenti simili, permette all'assistente AI di leggere autonomamente file, pagine web o risposte da server MCP (Model Context Protocol). Il problema è che queste sorgenti esterne possono contenere istruzioni malevole camuffate da testo normale — ed è qui che entra in gioco la *prompt injection*.

Con DuneSlide, le istruzioni iniettate non richiedono alcuna interazione da parte dell'utente. L'AI le legge da sola mentre analizza un file di progetto, una pagina web o una risposta da un tool, e poi le esegue.

**CVE-2026-50548** sfrutta il modo in cui la sandbox si fida della cartella di lavoro scelta dall'agente. Se il contenuto malevolo riesce a far puntare l'agente verso un percorso di sistema invece che alla cartella del progetto, si apre la possibilità di sovrascrivere il componente che fa rispettare la sandbox stessa. Un classico attacco di tipo TOCTOU (Time-Of-Check Time-Of-Use).

**CVE-2026-50549** colpisce invece il controllo sui link simbolici: quando la verifica fallisce, Cursor sceglie di fidarsi del percorso apparente anziché rifiutarlo. Il risultato è lo stesso: l'esecuzione di codice arbitrario fuori dalla sandbox.

## Scenari d'attacco reali

Il vettore più preoccupante è **il repository GitHub avvelenato**. Un attaccante può creare un progetto open source apparentemente legittimo e inserire istruzioni malevole nei file di configurazione, nei file README o in qualsiasi documento che l'agente leggerebbe durante l'analisi del codice. Non serve che la vittima clicchi su nulla — basta aprire il progetto con Cursor e lasciare che l'AI faccia il suo lavoro.

Altri scenari includono:
- Risposte malevole da server MCP compromessi
- Pagine web restituite durante una ricerca dell'agente
- Dipendenze npm/pip con documentazione avvelenata

## Sei vulnerabile? Come verificarlo

DuneSlide colpisce **tutte le versioni di Cursor precedenti alla 3.0**, rilasciata il 2 aprile 2026. Per verificare la tua versione:

```bash
# Su Linux/macOS, da terminale
cursor --version

# Oppure dall'interfaccia: Help → About
```

Se hai una versione < 3.0, aggiorna immediatamente:

```bash
# Su sistemi con Flatpak
flatpak update com.cursor.Cursor

# Su Arch Linux (AUR)
yay -Syu cursor-bin

# Download diretto dal sito ufficiale
xdg-open https://cursor.com/download
```

## Aggiornare non basta: difendersi dalla prompt injection

Il fatto che Cursor 3.0 abbia risolto queste specifiche falle non significa che il problema della prompt injection sia risolto in generale. È una classe di attacchi strutturale contro tutti i sistemi che combinano AI e accesso a risorse esterne.

Alcune buone pratiche da adottare subito:

- **Rivedi i permessi dell'agente**: limita quali strumenti l'AI può usare senza conferma esplicita
- **Modalità "ask before run"**: attiva l'approvazione manuale per tutti i comandi shell
- **Non aprire progetti sconosciuti** con le funzionalità AI agente abilitate
- **Aggiorna regolarmente** tutti gli strumenti AI del tuo workflow

## Il problema più grande

DuneSlide è solo l'esempio più recente di una tendenza preoccupante: gli strumenti AI stanno diventando vettori d'attacco di primo piano. La superficie esposta si è allargata enormemente — ogni documento che l'AI legge è ora potenzialmente un vettore. I ricercatori di sicurezza stanno ancora capendo come si difende da questa nuova classe di minacce, e le patch arriveranno più lentamente dei nuovi attacchi.

Per chi sviluppa software, la lezione è chiara: tratta i tool AI con agente come tratteresti qualsiasi applicazione connessa a internet. Tienili aggiornati, limita i loro permessi e non aprire repository di cui non ti fidi con l'AI agente accesa.
