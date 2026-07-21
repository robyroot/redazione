---
title: "KDE Plasma 6.8 arriva il 14 ottobre: è l'addio definitivo a X11 (e non è un male)"
rilevanza: "MEDIA"
fonte: "https://9to5linux.com/kde-plasma-6-8-desktop-environment-is-coming-on-october-14th-heres-what-to-expect"
data_notizia: "2026-07-19"
tags: ["KDE", "Plasma", "Wayland", "X11", "Linux-desktop"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: l'eliminazione di X11 è un momento storico per il desktop Linux. Spiegare in modo semplice cosa cambia per l'utente finale, sfatare i timori più comuni (compatibilità delle app) e sottolineare i vantaggi concreti. Il pubblico italiano Linux ama questi temi.
---

# KDE Plasma 6.8 arriva il 14 ottobre: è l'addio definitivo a X11 (e non è un male)

Il team di KDE ha ufficialmente annunciato la data di rilascio di **Plasma 6.8**: **14 ottobre 2026**. È una data importante non solo per i numeri della versione, ma per quello che rappresenta: **il ritiro completo del supporto nativo a X11**. Da 6.8 in poi, Plasma girerà solo su **Wayland** (con XWayland per retrocompatibilità).

Sì, lo so: c'è sempre qualcuno che sente "fine di X11" e si preoccupa. Vediamo perché questa volta non c'è davvero motivo di farlo.

## Prima di tutto: cosa cambia davvero per te

Se sei un utente normale di KDE su una distribuzione moderna, la risposta è: **quasi nulla**. Le tue app continuano a funzionare tramite **XWayland**, lo strato di compatibilità che "traduce" le applicazioni X11 verso Wayland. Non devi reinstallare niente, non devi cambiare configurazioni.

Quello che sparisce è la possibilità di avviare **l'intero desktop Plasma in modalità X11**. Questo è un cambio rilevante per chi aveva motivi specifici per farlo (certi casi edge con driver proprietari vecchi, setup multi-monitor particolari), ma per la stragrande maggioranza degli utenti è invisibile.

## La data del 14 ottobre non è casuale

KDE ha scelto questa data con un po' di stile: il 14 ottobre 2026 cade vicino al **30° anniversario del progetto KDE**, fondato nell'ottobre del 1996 da Matthias Ettrich. Un compleanno tondo merita un aggiornamento significativo.

## Le novità tecniche che contano

Al di là dell'addio X11, Plasma 6.8 porta alcune migliorie concrete:

**Triple buffering per NVIDIA abilitato di default**
Finalmente. Il triple buffering riduce il tearing visivo su schermo, specialmente nelle animazioni. Su GPU NVIDIA era già disponibile ma non attivo di default; da 6.8 lo sarà.

**CPU Affinity per le finestre**
Puoi assegnare affinità CPU specifiche alle finestre direttamente da Plasma. Utile per chi fa benchmark, streaming o lavora con applicazioni real-time che beneficiano di core dedicati.

**Ombre automatiche per le finestre**
Le finestre che non disegnano già le proprie ombre (molte app Qt/KDE) ricevono automaticamente ombre dal compositor Wayland. Risultato visivo più coerente senza intervento manuale.

**Supporto Flatpak di Microsoft Edge in Plasma Browser Integration**
Sì, anche Edge. Se per qualche ragione lo usi in versione Flatpak, ora si integra correttamente con le funzioni del desktop KDE (notifiche, media controls, ecc).

**Registrazione audio in Spectacle**
L'app di screenshot di KDE potrà registrare anche l'audio durante i video. Piccola comodità, grande comodità quotidiana per chi fa screencast.

## La timeline per arrivare al 14 ottobre

Se vuoi testare prima del rilascio stabile:

- **10 settembre 2026**: Beta 1 (prima beta pubblica)
- **24 settembre 2026**: Beta 2
- **14 ottobre 2026**: Rilascio finale

Per chi usa **Arch Linux** o **Fedora Rawhide**, le beta arriveranno nei repository extra/testing molto velocemente.

```bash
# Su Arch (testing repo)
sudo pacman -Syu plasma-desktop

# Su Fedora (repo kde-testing)
sudo dnf copr enable @kde/plasma-testing
sudo dnf upgrade plasma-desktop
```

## Perché l'addio a X11 è una buona notizia

X11 è un protocollo che nasce nel 1984. Letteralmente 42 anni fa. Nel tempo è stato rattoppato, esteso e piegato in modi che i suoi creatori non avrebbero mai immaginato. Wayland è stato progettato da zero con in testa le esigenze dei desktop moderni: sicurezza (nessun'app può spiare le altre), performance (compositing integrato), HiDPI nativo, gesture multitouch.

Il ritardo nell'abbandono di X11 non era per mancanza di volontà, ma per la lunga coda di casi d'uso da coprire: screen sharing, accessibility, driver grafici, applicazioni legacy. Con KDE 6.x questi casi sono stati affrontati uno per uno.

KDE Plasma 6.7 (uscita a giugno 2026) ha già dichiarato formalmente chiusa "l'era X11". La 6.8 è il sigillo definitivo.

Se sei rimasto su X11 per vecchie abitudini o per qualche problema specifico passato, questo è il momento giusto per passare a Wayland: è maturo, stabile, e il vostro desktop ne beneficerà.
