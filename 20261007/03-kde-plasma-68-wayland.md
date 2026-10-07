---
title: "KDE Plasma 6.8: il 14 ottobre addio X11 e benvenuto al 30° compleanno del desktop"
rilevanza: "ALTA"
fonte: "https://9to5linux.com/kde-plasma-6-8-desktop-environment-is-coming-on-october-14th-heres-what-to-expect"
data_notizia: "2026-10-04"
tags: ["kde", "plasma", "wayland", "x11", "linux", "desktop", "nvidia"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: doppio aggancio narrativo forte — il 30° anniversario di KDE (nostalgia + storia del desktop Linux) e la dismissione definitiva di X11 (milestone tecnica importante). Buona occasione per spiegare ai lettori perché Wayland vince e cosa cambia nella pratica per chi usa NVIDIA. Aggiungere la mini-storia di KDE per il pubblico che non la conosce.
---

# KDE Plasma 6.8: il 14 ottobre addio X11 e benvenuto al 30° compleanno del desktop

Il **14 ottobre 2026** sarà una data da ricordare per chi usa Linux sul desktop. Quel giorno uscirà **KDE Plasma 6.8**, e non sarà un rilascio qualunque: coincide esattamente con il **30° anniversario di KDE**, e porta con sé una decisione storica — **l'abbandono definitivo di X11**.

## Trent'anni fa, un tedesco con un'idea pazza

Il 14 ottobre 1996, Matthias Ettrich postò un messaggio sul gruppo Usenet `de.comp.os.linux.misc` con un titolo provocatorio: *"New Project: Kool Desktop Environment"*. L'idea era semplice ma ambiziosa: creare un desktop integrato, bello e usabile per Linux, ispirato alle interfacce commerciali del tempo come CDE su Unix.

Trent'anni dopo, KDE è uno dei progetti open source più grandi e attivi del mondo, con centinaia di sviluppatori volontari e un ecosistema di applicazioni che spazia dai editor di testo agli strumenti di grafica professionale. Per festeggiare, il team KDE ha preparato una sorpresa speciale: la premiere di **"KDE: The Documentary"**, un film sulla storia del progetto.

## La fine di X11 in KDE: perché è importante

La notizia tecnica più rilevante di Plasma 6.8 è l'abbandono del supporto alla sessione **X11**. Da questa versione, **Wayland è l'unica opzione offerta al login**.

Molti utenti Linux avranno sentito parlare di questa transizione per anni senza capire bene cosa cambia nella pratica. In sintesi:

- **X11** (o X.Org) è il vecchio sistema di finestre, nato negli anni '80. Funziona, ma ha architettura obsoleta e molti problemi di sicurezza (un'applicazione può spiare le altre, per esempio).
- **Wayland** è il sostituto moderno, con isolamento delle applicazioni, migliore gestione del refresh rate, supporto nativo agli schermi ad alto DPI e prestazioni migliori.

KDE ha supportato entrambi per anni, ma il codice legacy di X11 rallenta lo sviluppo e introduce bug. Tagliare il supporto significa poter sviluppare più velocemente senza doversi preoccupare della retrocompatibilità.

```bash
# Verifica se stai già usando Wayland
echo $XDG_SESSION_TYPE
# Output "wayland" = sei già pronto, "x11" = stai ancora usando il vecchio sistema
```

## Le novità più interessanti per gli utenti

Oltre alla dismissione di X11, Plasma 6.8 porta alcune funzionalità concrete:

**Triple buffering per NVIDIA abilitato di default** — Se hai una scheda NVIDIA, questa è forse la novità più sentita. Il triple buffering riduce il tearing (l'effetto "strappo" nello schermo durante le animazioni) e migliora la fluidità generale. Finora bisognava abilitarlo manualmente; da 6.8 è on by default.

**Registrazione audio con Spectacle** — Spectacle è lo strumento di screenshot/registrazione schermo di KDE. Da 6.8 supporta anche la registrazione dell'audio durante i video dello schermo, senza dover installare nessun plugin aggiuntivo.

**Plasma Browser Integration con Flatpak Microsoft Edge** — Non la notizia più emozionante ideologicamente parlando, ma utile per chi lavora in ambienti enterprise che richiedono Edge. La versione Flatpak ora si integra correttamente con il desktop KDE.

**Rilevamento migliorato dei temi GTK scuri** — Se usi applicazioni GTK (come quelle GNOME) insieme ad applicazioni KDE, Plasma 6.8 è più bravo a rilevare il tema scuro attivo e applicare automaticamente l'icona corrispondente.

## Come aggiornare

Se usi una distribuzione rolling come Arch Linux o openSUSE Tumbleweed, Plasma 6.8 arriverà automaticamente nei repository il 14 ottobre. Per le distribuzioni a rilascio fisso come KDE Neon o Kubuntu, potrebbe volerci qualche giorno in più.

```bash
# Su Arch Linux
sudo pacman -Syu plasma

# Su openSUSE Tumbleweed
sudo zypper dup

# Verifica la versione installata di Plasma
plasmashell --version
```

**Nota NVIDIA**: se usi driver NVIDIA proprietari, dopo l'aggiornamento verifica che il triple buffering sia attivo andando in *Impostazioni di sistema → Display e Monitor → Compositor* e controllando le impostazioni di rendering.

## Un compleanno che guarda avanti

KDE compie 30 anni in una posizione di forza: è il desktop Linux più ricco di funzionalità, ha risolto la maggior parte dei problemi storici con Wayland, e ha un ecosistema applicativo enorme. La decisione di abbandonare X11 è coraggiosa ma necessaria — è il tipo di debito tecnico che prima o poi va pagato.

Se non hai ancora fatto il salto su Wayland con KDE, il 14 ottobre è il momento giusto. Sei in buone mani.
