---
title: "COSMIC 1.4: cosa cambia nel desktop Rust di System76"
rilevanza: "MEDIA"
fonte: "https://www.phoronix.com/news/COSMIC-Epoch-1.4"
data_notizia: "2026-07-27"
tags: ["linux", "desktop", "cosmic", "system76", "rust", "wayland"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: notizia leggera e accessibile, buona per chi si avvicina
  a Linux e sente parlare di COSMIC per la prima volta. Vale la pena inquadrare
  brevemente cos'è COSMIC e perché è interessante (Rust, Wayland nativo,
  alternativa a GNOME/KDE) prima di elencare le novità della 1.4.
---

Se segui il mondo Linux anche solo distrattamente, probabilmente hai già sentito nominare **COSMIC**, il desktop environment sviluppato da **System76**, l'azienda dietro il laptop Pop!_OS. Da qualche giorno è disponibile la versione **1.4**, una release di manutenzione che non stravolge nulla ma sistema parecchi piccoli fastidi — il tipo di aggiornamento che, alla fine, fa la differenza nell'uso quotidiano.

## Prima un ripasso: cos'è COSMIC

Per chi arriva nuovo all'argomento: COSMIC non è l'ennesimo tema o fork di GNOME, ma un desktop environment scritto **da zero in Rust**, pensato nativamente per **Wayland** (il protocollo grafico che sta sostituendo il vecchio X11 su Linux). System76 lo ha sviluppato per Pop!_OS ma è pensato per essere adottabile anche da altre distribuzioni, ed è già disponibile — tra le altre — su **Ultramarine Linux**, una distro basata su Fedora.

L'idea di fondo è offrire un'alternativa moderna a GNOME e KDE Plasma, con un occhio di riguardo alle performance (Rust è notoriamente veloce e sicuro in termini di gestione della memoria) e a un'interfaccia pulita, ispirata al design di Pop!_OS ma pensata per essere più leggera e personalizzabile "out of the box".

## Cosa porta la versione 1.4

COSMIC Epoch 1.4 — questo il nome ufficiale — è principalmente una release di **bugfix e rifiniture**, ma ce n'è per tutti i componenti principali della suite:

- **Nuovo tema sonoro di default** (cosmic-sound-theme), per dare più identità al sistema anche a livello di feedback audio.
- **Compositor più solido**: fix per il fullscreen nei giochi, per lo scaling frazionario (quello che serve, ad esempio, con schermi ad alta densità di pixel non perfettamente multipli del 100%) e per alcuni artefatti grafici che affliggevano le versioni precedenti. Migliorata anche la precisione del puntatore sui bordi dello schermo con lo scaling frazionario attivo.
- **COSMIC Monitor** (l'equivalente del task manager) guadagna la possibilità di **forzare la chiusura** delle applicazioni, oltre alla chiusura "normale", e ora permette di cambiare il tipo di grafico per CPU e GPU e di visualizzare anche la frequenza della GPU — dettagli utili per chi tiene d'occhio le prestazioni del sistema.
- **COSMIC Files, Panel e Launcher** ricevono ottimizzazioni varie, con il Panel che risolve anche alcuni crash segnalati dagli utenti.
- **Supporto NetworkManager migliorato**, per una gestione più affidabile delle connessioni di rete (Wi-Fi e cablate).
- **xdg-desktop-portal-cosmic** diventa un servizio di sistema vero e proprio, un cambiamento "sotto il cofano" che dovrebbe rendere più stabile l'integrazione con le applicazioni Flatpak e in generale il sandboxing delle app.
- Aggiornamenti alle **traduzioni** e alle dipendenze interne del progetto.

Nessuna di queste novità è rivoluzionaria da sola, ma nell'insieme raccontano un progetto che sta maturando: i fix al compositor su fullscreen e scaling frazionario, in particolare, toccano due dei problemi più citati da chi ha provato COSMIC nelle versioni precedenti, specialmente su laptop con schermi ad alta risoluzione o per chi gioca sotto Linux.

## Perché interessa anche a chi non usa COSMIC

Anche se non sei tra i (ancora pochi) utenti di COSMIC, questa release è un buon indicatore dello stato di salute del progetto. Un desktop scritto in Rust e pensato Wayland-first che continua a ricevere aggiornamenti regolari e mirati a risolvere problemi concreti — non solo feature nuove — è un segnale di un progetto che sta uscendo dalla fase sperimentale.

Se sei curioso di provarlo senza reinstallare tutto, la via più semplice resta **Pop!_OS** (che lo include nativamente) oppure **Ultramarine Linux 44**, che lo abbina a KDE Plasma 6.7 e al kernel Linux 7.0 in un'unica distro basata su Fedora. Per chi è già su altre distribuzioni, COSMIC è pacchettizzato anche per diverse distro tramite repository di terze parti, anche se la stabilità in quel caso può variare.

In sintesi: nulla di eclatante, ma è esattamente il tipo di aggiornamento incrementale che serve a un desktop environment giovane per diventare un'alternativa solida a GNOME e KDE nel medio periodo.
