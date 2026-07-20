---
title: "KDE Plasma 6.7: desktop virtuali per schermo, niente più fantasmi Flatpak e tante altre novità"
rilevanza: "MEDIA"
fonte: "https://kde.org/announcements/plasma/6/6.7.0/"
data_notizia: "2026-06-16"
tags: ["kde", "plasma", "linux", "desktop", "flatpak", "wayland", "multimonitor"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: finalmente il multi-monitor su KDE funziona come dovrebbe. È una release di qualità della vita attesa da anni, ottima per chi usa Linux come desktop quotidiano con più schermi o app Flatpak.
---

# KDE Plasma 6.7: desktop virtuali per schermo, niente più fantasmi Flatpak e tante altre novità

Chi usa Linux con più monitor sa bene quanto possa essere frustrante gestire i desktop virtuali su KDE Plasma. Cambiare workspace e vedersi sparire le finestre da tutti gli schermi contemporaneamente è uno di quei comportamenti che ti fanno rimpiangere persino macOS. Con KDE Plasma 6.7, quella frustrazione appartiene al passato.

## La novità più attesa: desktop virtuali per schermo

La feature principale di questa release è finalmente qui: i **desktop virtuali per schermo** (per-screen virtual desktops). In Plasma 6.7, ogni monitor può avere il proprio workspace indipendente. Passi da workspace 1 a workspace 2 sullo schermo principale? Gli altri monitor rimangono esattamente dove sono.

Sembra banale, ma per chi usa configurazioni multi-schermo questo cambia completamente il modo di organizzare il lavoro. Codice su uno schermo, browser sull'altro, terminale sul terzo — e puoi cambiare contesto su uno senza toccare gli altri. Il comportamento è attivo di default; se preferisci il vecchio stile globale, lo trovi nelle impostazioni dei desktop virtuali.

## Addio ai fantasmi nella system tray

Secondo problema storico risolto: il **ghosting delle app Flatpak** nella system tray. Chi usa applicazioni distribuite come Flatpak (Spotify, Signal, Telegram, e tante altre) conosce bene il fenomeno: icone che rimangono "fantasma" nella barra di stato anche dopo che l'app è stata chiusa, o che non appaiono correttamente al primo avvio.

Plasma 6.7 risolve questa inconsistenza migliorando l'integrazione D-Bus tra le app sandbox Flatpak e il pannello di sistema. Niente più click del mouse su icone di app che non rispondono perché tecnicamente non esistono più.

## Notifiche intelligenti e tester microfono

Due piccole aggiunte che migliorano l'usabilità quotidiana:

**Notifiche vicino allo schermo attivo**: prima le notifiche potevano comparire su qualsiasi schermo, a volte su quello meno visibile mentre sei concentrato su un altro. Ora vengono indirizzate automaticamente allo schermo su cui stai lavorando in quel momento.

**Tester microfono integrato**: nelle impostazioni audio di Plasma trovi ora un semplice strumento per testare il microfono senza dover aprire app esterne o usare `arecord` da terminale. Molto utile prima di call o registrazioni.

## Wayland migliorato e anteprima del tema Union

Il lavoro su **Wayland** continua con miglioramenti alla stabilità e al comportamento delle sessioni. Chi usa Wayland come default (scelta sempre più comune nel 2026) noterà meno edge case fastidiosi nella gestione delle finestre e nella risposta al resize.

La novità più curiosa è l'**anteprima del tema Union**: il prossimo sistema di theming di KDE, progettato per rendere la personalizzazione visiva più coerente e potente. Non è ancora pronto per l'uso quotidiano, ma è disponibile come anteprima per chi vuole sbirciare cosa arriverà nelle prossime versioni di Plasma.

## Come ottenere Plasma 6.7

**KDE neon** è la distribuzione ufficiale di KDE che porta Plasma in versione aggiornata su base Ubuntu. Se usi KDE neon, un semplice aggiornamento ti porta a Plasma 6.7:

```bash
sudo pkcon update
```

Su **Arch Linux** e derivate (Manjaro, EndeavourOS):

```bash
sudo pacman -Syu
```

Su **Kubuntu** dovrai aspettare i backport ufficiali o usare il PPA di KDE. Su altre distribuzioni i tempi dipendono dal loro ciclo di rilascio.

Per verificare la versione installata:

```bash
plasmashell --version
```

## Plasma 6.7.3: la versione stabile di luglio

A luglio 2026 è arrivato anche il bugfix release **6.7.3**, che consolida le novità della 6.7 con ulteriori fix mirati. Se stai installando Plasma adesso, trovi direttamente questa versione sui canali stabili. È la scelta consigliata per chi vuole il meglio senza sperimentare con versioni di sviluppo.

Nel complesso, Plasma 6.7 è una release che mette a fuoco la qualità della vita: niente rivoluzioni visive, ma tante cose che finalmente funzionano come dovrebbero. Un bel passo avanti per il desktop Linux quotidiano.
