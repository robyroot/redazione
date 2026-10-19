---
title: "KDE Plasma 6.8: addio a X11, benvenuto nel futuro Wayland"
rilevanza: "ALTA"
fonte: "https://news.tuxmachines.org/n/2026/10/14/KDE_Plasma_6_8_Desktop_Environment_Officially_Released_Here_s_W.shtml"
data_notizia: "2026-10-14"
tags: ["KDE", "Plasma", "Wayland", "Linux desktop", "open source"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: un traguardo storico — KDE plasma elimina definitivamente X11. 
  Ideale per spiegare cosa significa per gli utenti desktop Linux e perché Wayland è ormai maturo.
---

# KDE Plasma 6.8: addio a X11, benvenuto nel futuro Wayland

Il 14 ottobre 2026 è una data che gli appassionati di Linux desktop difficilmente dimenticheranno: KDE ha rilasciato Plasma 6.8.0, e con esso ha ufficialmente chiuso i battenti alla sessione X11. Non è uno scherzo, non è una feature sperimentale: se usi Plasma 6.8 e vuoi avviare una sessione grafica, **la tua unica opzione è Wayland**.

Coincidenza non da poco: questa release coincide con il **30° anniversario di KDE**, il progetto che nel 1996 si propose di portare un desktop grafico elegante e usabile su Linux. Trent'anni dopo, KDE cambia le regole del gioco ancora una volta.

## Cosa cambia davvero con Plasma 6.8

La notizia principale è che le sessioni Plasma X11 non esistono più. Dal login screen non vedrai più l'opzione "KDE Plasma (X11)". Esiste solo Wayland.

Ma non preoccuparti per le tue vecchie applicazioni: **XWayland è ancora lì**, il layer di compatibilità che permette alle app scritte per X11 di girare sotto Wayland senza nemmeno accorgersene. Questo significa che il tuo vecchio software — dai giochi ai tool grafici nati nel 2010 — continuerà a funzionare, ma l'infrastruttura sottostante è finalmente moderna.

### Novità pratiche che noterai subito

**Spectacle registra l'audio di sistema.** Lo strumento di screenshot e registrazione schermo di KDE ora può catturare anche l'audio dell'intero desktop. Prima era un limite fastidioso — potevi registrare lo schermo ma non il suono del sistema, solo il microfono. Ora basta selezionare "Audio di sistema" nelle opzioni di registrazione.

**Microsoft Edge su Flatpak con browser integration.** Una novità un po' ironica: KDE ha aggiunto il supporto a Microsoft Edge installato via Flatpak all'interno di Plasma Browser Integration. Questo significa che anche Edge sandboxato può comunicare con il desktop KDE per cose come la riproduzione multimediale e la gestione dei download. Ironico, certo, ma è un segno della maturità dell'ecosistema Flatpak.

**Stabilità e polish generale.** Come ogni major release di Plasma, c.è una valanga di fix, miglioramenti all'accessibilità, e affinamenti all'interfaccia. Plasma 6.8 è stato descritto dagli sviluppatori come il completamento naturale del ciclo iniziato con Plasma 6.0 nel 2024: l'architettura Wayland-first è ora Wayland-only.

## Come aggiornare a Plasma 6.8

Se usi una distro rolling release come **Arch Linux**, **openSUSE Tumbleweed** o **KDE neon**, probabilmente hai già ricevuto o riceverai presto l'aggiornamento automatico.

```bash
# Su Arch Linux
sudo pacman -Syu

# Su openSUSE Tumbleweed
sudo zypper dup

# Su KDE neon
sudo apt update && sudo apt full-upgrade
```

Per chi usa distro LTS come Ubuntu, dovrai aspettare Ubuntu 26.10 (fine ottobre) o usare un repository terzo. Kubuntu 26.10 dovrebbe includere Plasma 6.8 out of the box.

## KDE: 30 anni di desktop Linux

Vale la pena fermarsi un secondo sul traguardo. KDE nacque il 14 ottobre 1996 quando Matthias Ettrich annunciò su Usenet un progetto per creare un "desktop environment completo e bello" per Unix. All'epoca era una mossa audace — GTK e GNOME non esistevano ancora, l'interfaccia grafica di Linux era sostanzialmente inesistente per l'utente comune.

Trent'anni dopo, KDE Plasma è uno dei desktop più potenti e configurabili al mondo, con milioni di utenti e un ecosistema di app (Okular, Dolphin, KCalc, Kdenlive...) che competono alla pari con alternative commerciali.

Il salto a Wayland-only in Plasma 6.8 non è solo un aggiornamento tecnico: è KDE che dice "siamo pronti per i prossimi trent'anni."

## Vale la pena aggiornare?

**Sì**, specialmente se fai già uso di Wayland. Se invece dipendi da qualche vecchia applicazione X11 molto particolare (toolkit obsoleti, hardware legacy con driver antichi), fai qualche test prima in una macchina virtuale. Ma per il 99% degli utenti desktop moderni, Plasma 6.8 su Wayland funzionerà benissimo — probabilmente meglio di prima.
