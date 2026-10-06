---
title: "KDE Plasma 6.8 arriva il 14 ottobre — e KDE compie 30 anni"
rilevanza: "ALTA"
fonte: "https://9to5linux.com/kde-plasma-6-8-desktop-environment-is-coming-on-october-14th-heres-what-to-expect"
data_notizia: "2026-10-01"
tags: ["KDE", "Plasma", "Linux desktop", "Flatpak", "open source", "anniversario"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Combina notizia tecnica con il milestone storico dei 30 anni di KDE. Ottima occasione per un articolo celebrativo e informativo che parla sia agli utenti Linux esperti che ai curiosi che vogliono scoprire KDE.
---

# KDE Plasma 6.8 arriva il 14 ottobre — e KDE compie 30 anni

Il 14 ottobre 2026 sarà una data doppiamente speciale per il mondo Linux: arriverà KDE Plasma 6.8, il nuovo aggiornamento del popolare ambiente desktop, e contemporaneamente KDE festeggerà il suo **trentesimo compleanno**. Non è un caso che gli sviluppatori abbiano scelto questa data — è un omaggio alla lunga storia di uno dei progetti open source più importanti mai creati.

## Trent'anni di KDE: dalla K Desktop Environment al 2026

KDE nacque il 14 ottobre 1996 per mano di Matthias Ettrich, con l'ambizioso obiettivo di portare un'interfaccia grafica coerente e user-friendly su Unix. In quegli anni, il desktop Linux era frammentato e poco accessibile. L'intuizione di Ettrich — usare le Qt libraries di Trolltech per costruire qualcosa di coeso — fu rivoluzionaria.

Tre decenni dopo, KDE è diventato molto più di un semplice ambiente desktop: è un ecosistema completo di applicazioni, strumenti di sviluppo, framework e persino un'intera distribuzione Linux (KDE Linux). Il progetto ha influenzato in modo profondo l'intero panorama del software libero, spingendo anche GNOME a nascere come alternativa basata su GTK.

## Le novità di Plasma 6.8

La release 6.8 non è un aggiornamento rivoluzionario, ma porta diversi miglioramenti concreti che gli utenti quotidiani apprezzeranno:

### Flatpak e Microsoft Edge in Plasma Browser Integration

Finalmente il supporto a **Flatpak per Microsoft Edge** arriva in Plasma Browser Integration. Questo significa che chi usa Edge come browser Flatpak potrà sfruttare la piena integrazione con il desktop: notifiche, controllo dei media, gestione delle schede e altro ancora. Una notizia che potrebbe sembrare strana in un articolo su Linux — ma Edge è diventato abbastanza diffuso anche su Linux, soprattutto in ambienti aziendali.

### Configurazione Wi-Fi più intelligente

Nelle Impostazioni di sistema, nella sezione Reti, sarà possibile configurare i **punti di accesso wireless** affinché selezionino automaticamente il canale ottimale. Piccola feature, ma utile per chi gestisce reti domestiche o di ufficio direttamente dal desktop.

### Rilevamento migliorato dei temi dark GTK 2

Plasma 6.8 migliora il rilevamento dei **temi scuri GTK 2** e applica automaticamente un tema di icone compatibile. Questo risolve uno dei fastidiosi problemi visivi che gli utenti di applicazioni GTK 2 (ancora in circolazione, sì) si trovavano ad affrontare su Plasma.

## KDE Linux: il progetto BuildStream

Settembre è stato un mese tranquillo per KDE Linux, la distribuzione ufficiale del progetto, perché molti contributor erano impegnati con **Akademy 2026**, la conferenza annuale della comunità KDE. Il lavoro principale riguarda una variante basata su **BuildStream** e l'SDK Flatpak di FreeDesktop — la stessa base tecnica usata da GNOME OS. L'obiettivo è arrivare a ottobre con una decisione definitiva sulla direzione del progetto.

## Come aggiornare a Plasma 6.8

La release ufficiale è prevista per il **14 ottobre 2026**. Se usi una distribuzione rolling come Arch Linux o openSUSE Tumbleweed, l'aggiornamento arriverà automaticamente entro pochi giorni dalla release. Su Kubuntu, KDE neon o Fedora KDE, dovrai aspettare i pacchetti per la tua distribuzione specifica.

```bash
# Su Arch Linux, dopo il 14 ottobre
sudo pacman -Syu plasma

# Su KDE neon / Kubuntu
sudo apt update && sudo apt upgrade

# Verifica la versione di Plasma installata
plasmashell --version
```

## Perché importa

KDE Plasma è uno degli ambienti desktop più usati nel mondo Linux — e il fatto che dopo 30 anni sia ancora qui, in salute e con una community attiva, è una testimonianza del valore del software libero. Se non hai mai provato KDE, il compleanno potrebbe essere l'occasione giusta per dargli un'occhiata.

Buon compleanno, KDE.
