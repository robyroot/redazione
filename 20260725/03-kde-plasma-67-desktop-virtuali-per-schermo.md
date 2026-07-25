---
title: "KDE Plasma 6.7: finalmente i desktop virtuali per schermo, dopo 21 anni di attesa"
rilevanza: "MEDIA"
fonte: "https://www.linuxcompatible.org/story/kde-neon-20260723-ships-fresh-daily-build-with-plasma-673-and-perscreen-virtual-desktops"
data_notizia: "2026-07-23"
tags: ["kde", "plasma", "linux-desktop", "wayland", "flatpak", "multi-monitor"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Una funzionalità attesa da decenni finalmente arriva. Ottimo per mostrare come il desktop Linux continui a migliorare e perché KDE Plasma 6.x vale la pena provare, anche per chi lo ha abbandonato anni fa.
---

# KDE Plasma 6.7: finalmente i desktop virtuali per schermo, dopo 21 anni di attesa

C'è una richiesta che la comunità KDE aspettava da **21 anni**. Ventuuno. Anni. Ed è finalmente arrivata con KDE Plasma 6.7: i **desktop virtuali indipendenti per schermo**.

Se avete mai usato un setup multi-monitor su Linux e vi siete trovati frustrati dal fatto che cambiare desktop virtuale lo cambia su tutti i monitor contemporaneamente — capite bene perché questa è una notizia degna di celebrazione. Birra aperta, torta sul tavolo.

## Cosa sono i desktop virtuali per schermo

In un setup multi-monitor tradizionale su KDE Plasma, i desktop virtuali erano globali: se passavate dal desktop 1 al desktop 2, il cambio avveniva su tutti i monitor in simultanea. Per certi flussi di lavoro va benissimo, ma molti utenti con 2 o 3 monitor vogliono qualcosa di diverso — ogni schermo con la propria serie di workspace indipendente.

Con Plasma 6.7, ogni monitor fisico può ora avere il proprio set di desktop virtuali. Volete tenere il terminale sempre visibile sul monitor laterale mentre scorrete tra le workspace del monitor principale? Volete usare il monitor verticale come bacheca fissa di documentazione mentre lavorate su quello centrale? Ora potete farlo nativamente, senza plugin, senza workaround, senza sceneggiature.

È la stessa funzionalità che macOS ha da anni — ma su Linux, open source, e finalmente arrivata anche qui.

## Le altre novità di Plasma 6.7

I desktop per schermo non sono l'unica cosa interessante in questa release. Vediamo le altre novità più rilevanti.

**Toggle rapido luce/buio nei Temi Globali**
Finalmente un modo veloce per passare dal tema chiaro a quello scuro direttamente dalle impostazioni dei Temi Globali, senza dover andare a cercare la voce nascosta in qualche pannello di controllo sepolto a tre livelli di profondità.

**System tray con supporto al protocollo Flatpak**
Il vassoio di sistema ora rispetta il protocollo per le app Flatpak in esecuzione in background. Le applicazioni installate via Flatpak potranno finalmente integrarsi correttamente con la system tray, senza comportamenti strani o icone fantasma che appaiono e scompaiono a caso.

**Stampa su stampanti Windows condivise via SMB**
Migliore supporto per stampare su stampanti condivise Windows tramite il protocollo SMB — una funzionalità fondamentale in ambienti misti Windows/Linux, specialmente in ufficio.

## Come aggiornare a Plasma 6.7

Se usate **KDE neon**, l'aggiornamento è già disponibile dalla build del 23 luglio:

```bash
sudo pkcon update
```

Su **Arch Linux** (con Plasma dai repository extra):

```bash
sudo pacman -Syu plasma
```

Su **Kubuntu** o altre distribuzioni Ubuntu-based, i pacchetti arriveranno nel PPA backports:

```bash
sudo add-apt-repository ppa:kubuntu-ppa/backports
sudo apt update && sudo apt full-upgrade
```

Per verificare quale versione di Plasma è installata:

```bash
plasmashell --version
```

Se volete abilitare i desktop virtuali per schermo, dopo l'aggiornamento andate in **Impostazioni di sistema → Comportamento → Desktop virtuali** e cercate l'opzione per la gestione per-schermo.

## Perché questo è importante

KDE Plasma è uno dei desktop environment più potenti per Linux, ma spesso viene sottovalutato perché "ci vuole tempo per configurarlo" o "era instabile qualche versione fa". La verità è che Plasma 6.x ha fatto passi da gigante in termini di stabilità, performance su Wayland, e usabilità, e ogni nuova versione colma gap che esistevano da anni.

I desktop virtuali per schermo, in particolare, sono una di quelle funzionalità che sembrano banali ma cambiano radicalmente il modo in cui si lavora con setup multi-monitor. Per chi usa Linux come workstation principale, è probabilmente la feature più richiesta degli ultimi anni sul bug tracker di KDE.

Il fatto che ci siano voluti 21 anni non è un bel primato, ma almeno dimostra che la comunità KDE alla fine ascolta — e quando implementa una feature, la fa bene.

## Cosa aspettarsi da Plasma 6.8

La prossima versione principale, **KDE Plasma 6.8**, è attesa per il **14 ottobre 2026**. Se il ritmo di Plasma 6.7 è indicativo, possiamo aspettarci ulteriori miglioramenti a Wayland, migliore integrazione con Flatpak, e altre funzionalità chieste dalla comunità da tempo immemorabile.

Nel frattempo, Plasma 6.7 è già una buona ragione per dare — o ridare — una chance a KDE. Se lo avevate abbandonato anni fa per GNOME o altro, potrebbe sorprendervi quanto è migliorato.
