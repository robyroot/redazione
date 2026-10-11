---
title: "KDE Plasma 6.8 arriva il 14 ottobre: 30 anni di KDE e tante novità"
rilevanza: "ALTA"
fonte: "https://9to5linux.com/kde-plasma-6-8-desktop-environment-is-coming-on-october-14th-heres-what-to-expect"
data_notizia: "2026-10-10"
tags: ["kde", "plasma", "linux", "desktop", "open-source"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: rilascio importante con data simbolica (30° anniversario di KDE), feature tecnica interessante (sistema "Union" per i temi), e novità pratica per gli utenti NVIDIA (triple buffering di default). Ottimo per coinvolgere sia i lettori casual che quelli tecnici.
---

# KDE Plasma 6.8 arriva il 14 ottobre: 30 anni di KDE e tante novità

Segnate la data sul calendario: **14 ottobre 2026**. Non è solo un martedì qualunque, è il giorno in cui KDE Plasma 6.8 farà il suo debutto ufficiale, e il team ha scelto questa data con molta cura. Il 14 ottobre è il **30° anniversario del progetto KDE**, fondato nel lontano 1996 da Matthias Ettrich. Tre decenni di desktop Linux libero meritavano un rilascio speciale.

## Il nuovo sistema "Union": temi uniformi finalmente

La novità più interessante dal punto di vista tecnico è il nuovo sistema di theming chiamato **Union**. Chi usa KDE da un po' conosce bene il problema: i temi funzionano benissimo sulle app native Qt Quick (come il pannello, le impostazioni di sistema, Discover), ma le app "classiche" basate su QtWidgets — come Dolphin, Kate, Konsole — spesso continuano ad avere un aspetto diverso, quasi che vivessero in un'altra era del desktop.

Union risolve questo problema estendendo la coerenza visiva anche alle applicazioni QtWidgets. Tradotto: quando cambiate tema su Plasma 6.8, Dolphin e Kate finalmente *sembrano parte dello stesso desktop*, non reliquie degli anni 2000 con stili grafici diversi.

```bash
# Dopo l'aggiornamento a Plasma 6.8, potete cambiare tema da terminale con:
plasma-apply-lookandfeel --apply org.kde.breeze.desktop
# Oppure esplorare i temi disponibili:
plasma-apply-lookandfeel --list
```

## Triple buffering NVIDIA: finalmente di default

Un'altra novità che farà felici molti utenti è l'**abilitazione del triple buffering per GPU NVIDIA di default**. Il triple buffering riduce il tearing (quell'effetto di "strappo" dell'immagine) e migliora la fluidità dell'animazione del compositor, specialmente su monitor ad alta frequenza di aggiornamento.

Fino ad ora era una funzione che dovevate attivare manualmente scavando nelle impostazioni. Da Plasma 6.8, chi ha una scheda NVIDIA la troverà già attiva senza dover fare nulla.

Per chi vuole verificare le impostazioni del compositor:

```bash
# Controllare le impostazioni di KWin via kwriteconfig
kreadconfig5 --file kwinrc --group Compositing --key LatencyPolicy
```

## Il contesto: 30 anni non sono poca cosa

KDE ha avuto una storia travagliata ma gloriosa. Nato quando il desktop Linux era praticamente inesistente, ha attraversato le polemiche della migrazione a KDE 4 (che all'epoca fu un bagno di sangue), la rinascita con Plasma 5, e più recentemente la transizione a Plasma 6 nel 2024 con il passaggio a Qt6.

Oggi KDE è uno dei desktop Linux più avanzati tecnicamente, con una community attiva e un modello di sviluppo sano. Il progetto [KDE e.V.](https://ev.kde.org/) gestisce le donazioni e supporta gli sviluppatori a tempo pieno.

## Come aggiornare

Su Arch Linux e derivate (Manjaro, EndeavourOS):

```bash
sudo pacman -Syu
```

KDE Plasma 6.8 dovrebbe apparire nei repository pochi giorni dopo il rilascio ufficiale.

Su Kubuntu o KDE neon, l'aggiornamento arriverà tramite i canali usuali. KDE neon tende ad essere la più veloce nell'adottare le nuove versioni.

Su Fedora, probabilmente dovremo aspettare qualche settimana per il testing. Nel frattempo potete usare il repository COPR di KDE:

```bash
# Fedora: abilitare il repo KDE testing (se disponibile)
sudo dnf copr enable @kde/kde-testing
sudo dnf update
```

## Frameworks e Gear: gli altri pezzi del puzzle

KDE non è solo Plasma. Questa settimana sono arrivati anche:

- **KDE Frameworks 6.31.0** (rilasciato l'8-9 ottobre): fix per un bug che faceva ignorare l'impostazione "Contrasto cornici e bordi" in alcune app
- **KDE Gear 26.08.2** (8 ottobre): correzioni di bug per Dolphin e altre app, inclusa la leggibilità del testo selezionato con certi stili

Se usate un rolling release come Arch, li avete probabilmente già. Altrimenti arriveranno con il prossimo ciclo di aggiornamenti della vostra distro.

## Perché KDE merita attenzione

Nel 2026, il desktop Linux è in uno stato di salute eccellente. GNOME 51 è appena uscito a settembre, KDE Plasma 6.8 arriva a ottobre. Abbiamo due desktop maturi, attivamente sviluppati, liberi e con un ecosistema di app in crescita costante.

Se non avete ancora provato KDE negli ultimi anni, Plasma 6.8 è un ottimo momento per dargli un'altra chance. È diventato sorprendentemente rifinito.
