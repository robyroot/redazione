---
title: "KDE Plasma 6.8 arriva il 14 ottobre: triple buffering NVIDIA e 30 anni di KDE"
rilevanza: "MEDIA"
fonte: "https://9to5linux.com/kde-plasma-6-8-desktop-environment-is-coming-on-october-14th-heres-what-to-expect"
data_notizia: "2026-10-01"
tags: ["kde", "linux", "desktop", "plasma", "open-source", "nvidia"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: rassegna delle novità più importanti per gli utenti quotidiani di KDE, con focus su NVIDIA e multi-monitor - due punti dolenti storici finalmente risolti in questa release.
---

# KDE Plasma 6.8 arriva il 14 ottobre: triple buffering NVIDIA e 30 anni di KDE

Il 14 ottobre 2026 KDE festeggia 30 anni di vita e lo fa nel modo migliore: rilasciando **KDE Plasma 6.8**, la prossima versione del desktop environment amato da milioni di utenti Linux nel mondo. Una coincidenza non del tutto casuale — il team di sviluppo ha voluto fare di questa release una piccola celebrazione per un traguardo straordinario.

## Triplo buffering NVIDIA: finalmente

Se usi una scheda NVIDIA con KDE e hai mai sofferto di tearing o stuttering nelle animazioni, questa è la notizia che aspettavi. Plasma 6.8 abilita il **triple buffering per le GPU NVIDIA per impostazione predefinita**.

Il triple buffering è una tecnica di rendering che usa tre buffer di frame invece di due, riducendo drasticamente la probabilità di desincronizzazione tra il frame rate della GPU e il refresh rate del monitor. In pratica, le animazioni diventano più fluide e il tearing quasi scompare, soprattutto su monitor ad alto refresh rate (144Hz e oltre).

Prima di questa release, gli utenti NVIDIA dovevano abilitarlo manualmente modificando le configurazioni del compositor KWin — una procedura non immediata per gli utenti meno esperti. Ora è tutto automatico.

## Multi-monitor: badge colorati e luminosità rapida

Chi lavora con più monitor sa quanto può essere frustrante capire "qual è il monitor 1 e qual è il 2" nelle impostazioni di sistema. Plasma 6.8 risolve elegantemente il problema con **badge numerici colorati** sovrapposti a ciascun monitor nella schermata di configurazione, così da identificare immediatamente quale schermo corrisponde a quale.

Bonus: la regolazione della luminosità su monitor esterni diventa più veloce e reattiva. Non è una feature rivoluzionaria, ma chi passa ore ogni giorno davanti a due o tre schermi lo apprezzerà.

## Registrazione audio in Spectacle

Spectacle, lo strumento di screenshot e screen recording integrato in KDE, si aggiorna con il supporto per la **registrazione audio durante il screen recording**. Finalmente si può registrare lo schermo con l'audio del microfono o del sistema senza dover installare tool di terze parti come OBS per i casi d'uso più semplici — presentazioni, tutorial, demo rapide.

## Supporto Flatpak migliorato

Plasma Browser Integration aggiunge il supporto per la versione Flatpak di Microsoft Edge. Più importante per l'ecosistema, Plasma 6.8 migliora il **supporto automatico per Plasma Login Manager** su distribuzioni con versioni più datate di systemd. Una buona notizia per chi usa distribuzioni conservative come Debian Stable o sistemi embedded.

Viene anche migliorata la configurazione delle reti wireless: dalle impostazioni di sistema si può ora configurare i punti di accesso wireless per selezionare automaticamente il canale più efficiente — meno interferenze, migliori performance.

## Come provare Plasma 6.8 prima del rilascio

Se non vuoi aspettare il 14 ottobre, puoi già testare la release candidate su alcune distribuzioni:

```bash
# Su Arch Linux, aggiorna il sistema normalmente
sudo pacman -Syu
# Plasma RC è già nei repository testing di Arch

# Con Distrobox, senza rischi per il sistema host
distrobox create --name kde-plasma68 --image opensuse/tumbleweed
distrobox enter kde-plasma68

# openSUSE Tumbleweed è già aggiornata con i pacchetti RC
sudo zypper dup
```

openSUSE Tumbleweed è storicamente tra le prime distribuzioni ad adottare le nuove release di KDE — un ottimo banco di prova sicuro.

## I 30 anni di KDE

KDE è nata il 14 ottobre 1996 quando Matthias Ettrich annunciò il progetto su Usenet, con l'obiettivo dichiarato di creare un desktop unificato e facile da usare per i sistemi Unix/Linux. Da allora il progetto ha attraversato KDE 1, 2, 3, il controverso e amato-odiato KDE 4, il ritorno alla semplicità con Plasma 5 e la grande transizione a Qt6 con Plasma 6 nel 2024.

Trent'anni dopo, KDE è ancora uno dei desktop Linux più attivi, innovativi e completi del panorama open source. Gli eventi per il trentennale si tengono tra il 13 e il 14 ottobre in Brasile, Spagna e Turchia. Auguri, KDE.

## Quando arriva nelle distribuzioni?

- **Arch Linux**: praticamente subito dopo il rilascio il 14 ottobre
- **openSUSE Tumbleweed**: entro qualche giorno dal rilascio
- **Fedora 46** (in sviluppo): probabilmente incluso nella release finale
- **Kubuntu 26.10**: previsto con il rilascio di ottobre
- **Debian**: tempi più lunghi, come da tradizione
