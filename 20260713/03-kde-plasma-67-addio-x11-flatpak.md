---
title: "KDE Plasma 6.7: addio X11, finalmente multi-monitor senza impazzire"
rilevanza: "MEDIA"
fonte: "https://9to5linux.com/kde-plasma-6-7-desktop-environment-officially-released-this-is-whats-new"
data_notizia: "2026-06-16"
tags: ["kde", "plasma", "linux", "desktop", "flatpak", "wayland", "x11"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: enfatizzare la fine dell'era X11 come momento
  storico per il desktop Linux, le novità pratiche per chi usa più monitor, e i
  miglioramenti Flatpak che rendono la vita più facile agli utenti quotidiani.
  Tono entusiasta ma onesto sui cambiamenti.
---

# KDE Plasma 6.7: addio X11, finalmente multi-monitor senza impazzire

C'è una versione di KDE Plasma che verrà ricordata nei libri di storia del desktop Linux — ammesso che qualcuno scriva questi libri. **Plasma 6.7**, rilasciato il 16 giugno 2026, segna la fine ufficiale dell'era X11. Il vecchio protocollo grafico che ci ha accompagnato per decenni viene abbandonato, e il futuro è tutto Wayland. Ma prima di lanciarsi in elegie nostalgiche o entusiasmi eccessivi, parliamo delle cose pratiche che cambiano nella vita di tutti i giorni.

## Ciao Wayland, addio X11

Plasma 6.7 rimuove il supporto alla sessione X11 dalle installazioni standard. Chi ancora usava X11 per necessità specifiche — driver legacy, software aziendale vecchio, configurazioni multi-monitor particolari — dovrà fare i conti con questa transizione.

Il team KDE ha lavorato duro negli ultimi anni per rendere Wayland abbastanza maturo da reggere il peso di tutti i casi d'uso. Plasma 6.7 è il punto di arrivo di quel percorso. La maggior parte degli utenti non noterà differenze pratiche, anzi noterà miglioramenti. Ma chi aveva necessità specifiche di X11 dovrà valutare alternative o, in casi estremi, restare su versioni precedenti di Plasma un po' più a lungo.

## Multi-monitor: finalmente ci siamo

Questa è la novità che farà esultare chi usa un setup con più schermi. **Plasma 6.7 introduce i desktop virtuali per-monitor**: ogni schermo ha la sua sequenza di desktop virtuali indipendente dagli altri.

Prima di questo aggiornamento, cambiare desktop virtuale significava cambiare tutto su tutti i monitor contemporaneamente. Se lavoravi su monitor A con il browser su un desktop e il terminale su un altro, ogni cambio di workspace si rifletteva anche su monitor B, spostando le finestre in modo spesso indesiderato. Un incubo per chi lavora con workflow strutturati su più schermi.

Con Plasma 6.7, monitor A e monitor B hanno le loro sequenze di workspace completamente separate. Puoi passare dal desktop del browser a quello del terminale su monitor A, mentre monitor B rimane esattamente dove lo avevi lasciato. Semplice, ovvio in retrospettiva, e incredibilmente utile nella pratica.

## Flatpak: basta fantasmi nella system tray

Un altro bug che tormentava gli utenti Flatpak è finalmente risolto: il **ghosting delle icone nella system tray**. Succedeva che le app Flatpak chiuse lasciassero una icona fantasma nella barra di stato del sistema, oppure che le app Flatpak in esecuzione non comparissero affatto nella system tray.

Plasma 6.7 gestisce correttamente i **Flatpak background portals**, il meccanismo moderno che le app Flatpak usano per comunicare al desktop che stanno girando in background. Risultato: la system tray mostra finalmente quello che c'è, senza fantasmi e senza app invisibili.

Per provare KDE neon con Plasma 6.7 (se vuoi la versione più fresca su Ubuntu LTS):

```bash
# Su sistemi basati su Ubuntu, aggiungi il repository KDE neon
# Scarica l'ISO aggiornata di KDE neon da neon.kde.org
# Oppure, se usi già KDE neon, aggiorna normalmente:
sudo apt update && sudo apt upgrade -y
```

## Notifiche intelligenti e microfono integrato

Due piccole novità che migliorano l'ergonomia quotidiana:

**Notifiche contestuali**: in un setup multi-monitor, le notifiche ora appaiono sul bordo dello schermo più vicino alla finestra attiva, invece di spuntare a caso su uno schermo qualsiasi. Sembra un dettaglio, ma se stai lavorando su monitor B e arriva una notifica su monitor A, il cervello ci mette qualche istante a processarla. Adesso le notifiche vengono dove stai guardando.

**Microfono tester integrato**: finalmente non devi più aprire un'app esterna o cercare impostazioni nascoste per testare il microfono prima di una videochiamata. Plasma 6.7 include un piccolo strumento direttamente nelle impostazioni audio che ti permette di registrare e riascoltare un campione in tempo reale.

## Dark/Light mode con un click

Un'altra novità pratica: il toggle globale per la modalità chiara/scura è diventato più accessibile. Puoi passare da dark mode a light mode con un singolo click dal pannello delle impostazioni rapide, e il cambiamento si applica a tutte le app — incluse quelle Flatpak che rispettano il tema di sistema — senza dover aprire System Settings.

## Come aggiornare

KDE neon 20260709 porta Plasma 6.7 su Ubuntu 24.04 LTS ed è già disponibile per il download. Se usi Arch Linux o derivate, Plasma 6.7 è già nel repository extra da qualche settimana:

```bash
# Arch Linux
sudo pacman -Syu plasma

# openSUSE Tumbleweed
sudo zypper dup

# Fedora (via COPR o aggiornamento futuro)
# Controlla il COPR di KDE per Fedora
```

Per chi usa Ubuntu o derivate come Kubuntu, il porting arriverà con Ubuntu 26.10 o tramite il PPA di Kubuntu Backports per chi vuole averlo prima:

```bash
sudo add-apt-repository ppa:kubuntu-ppa/backports
sudo apt update && sudo apt upgrade -y
```

## Vale la pena aggiornare?

Se usi un setup multi-monitor, la risposta è sì senza esitazioni. I desktop virtuali per-monitor da soli giustificano l'aggiornamento. Se hai mai bestemmiato perché un cambio di workspace ti ha scompigliato entrambi i monitor, capirai immediatamente il valore della novità.

Per chi ha un solo schermo, i miglioramenti Flatpak e il supporto notifiche sono piacevoli ma non urgenti. Vale comunque la pena aggiornarsi per stare su un sistema moderno e ricevere i futuri miglioramenti su Wayland.

E se non hai ancora fatto il salto a Wayland, beh — con X11 ufficialmente fuori dai giochi, è arrivato il momento di farlo.
