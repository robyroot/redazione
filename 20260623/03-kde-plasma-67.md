---
title: "KDE Plasma 6.7: desktop virtuali per schermo, push-to-talk globale e il nuovo motore Union"
rilevanza: "MEDIA"
fonte: "https://kde.org/announcements/plasma/6/6.7.0/"
data_notizia: "2026-06-16"
tags: ["kde", "plasma", "linux-desktop", "wayland", "gnome", "desktop"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Usa KDE Plasma 6.7 come pretesto per raccontare perché il 2026 sta diventando davvero l'anno del desktop KDE — Steam Deck, Steam Machine, adozione aziendale crescente. Tono entusiasta, adatto anche a chi non usa ancora KDE e potrebbe essere curioso di provarlo.
---

# KDE Plasma 6.7: desktop virtuali per schermo, push-to-talk globale e il nuovo motore Union

Il 16 giugno 2026, il KDE Project ha rilasciato KDE Plasma 6.7, e se stavi aspettando un motivo valido per abbandonare il tuo attuale desktop environment, eccolo servito su un piatto d'argento. Questa release non è una di quelle "migliorie minori": porta con sé funzionalità che gli utenti aspettavano da anni e che cambiano concretamente il modo di lavorare ogni giorno.

## Desktop virtuali per schermo: finalmente

Se hai un setup multi-monitor e usi i desktop virtuali, sai esattamente quanto fosse frustrante avere tutti i monitor che cambiavano workspace insieme. Stavi lavorando sul monitor principale e volevi passare da terminale a browser, ma il monitor secondario con la videochiamata saltava anche lui a un desktop vuoto.

Con Plasma 6.7 questo è storia. Ogni monitor può avere i propri desktop virtuali completamente indipendenti. Puoi configurarlo facilmente dalle Impostazioni di Sistema:

```bash
# Apri le impostazioni di sistema da terminale
systemsettings
# Poi vai in: Display e Monitor → Virtual Desktops
# Attiva "Separate virtual desktops for each screen"
```

Per chi lavora con più schermi questa è la funzionalità più importante dell'intera release. Ci sono voluti anni di richieste dalla community, ma è arrivata.

## Push-to-talk globale: smart working senza interruzioni

Quante volte ti sei trovato a muto su una videochiamata senza saperlo, o peggio, a fare rumore involontario? Plasma 6.7 introduce un tasto **push-to-talk globale** che funziona su qualsiasi applicazione — Zoom, Teams, Discord, chiamate browser — senza dover configurare nulla nelle singole app.

Vai in *Impostazioni di Sistema → Scorciatoie → Scorciatoie globali* e cerca "Push-to-Talk". Assegna il tasto che preferisci (molti usano la barra spaziatrice o il tasto Caps Lock) e da quel momento tieni il tasto premuto quando vuoi parlare, rilascialo per mutarti.

Semplice, efficace, e finalmente integrato a livello di sistema.

## Union: il nuovo motore di theming

Uno dei problemi storici di KDE era che i temi si "rompevano" a ogni aggiornamento maggiore. Installavi un tema, aggiornavi Plasma, e ritrovavi elementi fuori posto, colori sbagliati, icone che non corrispondevano.

**Union** è il nuovo motore di theming introdotto in Plasma 6.7. Separa la logica visiva dal codice del desktop attraverso un sistema di stile più robusto, rendendo i temi molto più stabili nel tempo e più facili da mantenere per i creator.

Come bonus nostalgico: il **tema Oxygen** (KDE 4) e **Air** sono tornati ufficialmente come opzioni supportate. Se usi Linux da più di dieci anni, probabilmente ti è venuto un tuffo al cuore leggendo questo.

## Wayland sempre più solido

Plasma 6.7 continua il percorso verso Wayland come stack grafico di default. I miglioramenti principali includono:

- Miglior supporto per i tablet grafici Wacom
- Fix per le finestre su monitor con scale factor diverse (il classico problema del display 4K accanto a un monitor 1080p)
- Compatibilità migliorata con le app Electron e Qt5 tramite XWayland
- Drag-and-drop più stabile tra app Wayland native e app XWayland

Non siamo ancora al punto in cui Wayland funziona perfettamente per tutti, ma ogni release ci avvicina.

## Altre novità che vale la pena citare

- **Toggle dark/light mode** direttamente nel pannello: un singolo click per passare dal tema chiaro a quello scuro senza entrare nelle impostazioni
- **App per la coda di stampa**: finalmente un'interfaccia dedicata per gestire i lavori di stampa in sospeso
- **Discover migliorato**: il software store di KDE mostra ora i permessi richiesti dalle app Flatpak prima dell'installazione
- **Overview più veloce**: il cambio tra desktop virtuali nell'Overview è notevolmente più fluido

## Come aggiornare

```bash
# Arch Linux (e derivate come Manjaro, EndeavourOS)
sudo pacman -Syu

# Fedora KDE Spin
sudo dnf upgrade --refresh

# openSUSE Tumbleweed
sudo zypper dup

# Verifica la versione installata
plasmashell --version
```

Kubuntu e KDE neon riceveranno l'aggiornamento nelle prossime settimane tramite i loro canali normali.

## Il 2026 è davvero l'anno del desktop KDE

Il cliché "l'anno del desktop Linux" torna ogni anno da decenni, ma nel 2026 per KDE ci sono segnali concreti e misurabili. Steam Deck e il nuovo Steam Machine di Valve girano su SteamOS — Arch Linux con KDE Plasma — portando il desktop KDE nelle mani di milioni di giocatori. Le aziende che cercano alternative a Windows trovano in KDE Plasma un'opzione matura, personalizzabile e con un ciclo di sviluppo affidabile.

KDE Plasma 6.7 è la dimostrazione che il progetto non sta solo mantenendo lo status quo: sta attivamente innovando, ascoltando la community e rilasciando versioni di qualità con cadenza regolare. Non è una rivoluzione improvvisa — è il risultato di anni di lavoro paziente che comincia finalmente a dare i suoi frutti.

Se non hai mai provato KDE Plasma, o non lo provi da qualche anno, questo è un buon momento per dargli un'altra chance.
