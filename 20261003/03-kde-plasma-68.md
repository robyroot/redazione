---
title: "KDE Plasma 6.8 arriva il 14 ottobre: addio X11, triplo buffering NVIDIA e 30 anni di KDE"
rilevanza: "ALTA"
fonte: "https://9to5linux.com/kde-plasma-6-8-desktop-environment-is-coming-on-october-14th-heres-what-to-expect"
data_notizia: "2026-10-01"
tags: ["KDE", "Plasma", "Linux", "desktop", "Wayland", "GNOME", "Flatpak"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: il 14 ottobre coincide con il 30° anniversario di KDE — usa questo come aggancio narrativo. L'eliminazione di X11 è la notizia principale, ma il triplo buffering NVIDIA è la feature più attesa dagli utenti pratici. Parla anche del progetto KDE Linux (BuildStream + Flatpak SDK).
---

# KDE Plasma 6.8 arriva il 14 ottobre: addio X11, triplo buffering NVIDIA e 30 anni di KDE

Il 14 ottobre 2026 KDE compie **30 anni** — e per festeggiare ha deciso di fare una cosa che molti aspettavano da tempo: eliminare definitivamente X11 da Plasma. La versione 6.8 del desktop environment più personalizzabile del mondo Linux è quasi pronta e segna un passaggio storico verso Wayland come unica sessione supportata.

## Wayland diventa l'unica opzione

La notizia più importante di KDE Plasma 6.8 è anche quella più attesa (e per qualcuno, temuta): **il backend X11 viene rimosso dal desktop environment**. Chi avvia una sessione Plasma 6.8 avrà solo Wayland disponibile. X11 non scomparirà dal kernel o dalle librerie di sistema — ma Plasma non lo userà più come sessione grafica.

Per la maggior parte degli utenti, questo non cambierà nulla di pratico: Wayland è lo stack grafico predefinito da Plasma 6.0 e nel corso degli ultimi due anni il team ha colmato praticamente tutti i gap rispetto a X11. Schermo condiviso, supporto multi-monitor con scale factor diverse, input method — tutto funziona. Il passaggio definitivo è più una pulizia del codice che una rivoluzione operativa.

## Triplo buffering per NVIDIA, finalmente di default

Per chi ha una scheda NVIDIA, questa è probabilmente la feature più interessante: **il triple buffering è abilitato di default** in Plasma 6.8. Cosa significa in pratica? Eliminazione quasi totale dello screen tearing su Wayland con driver proprietari NVIDIA, animazioni più fluide e minor latenza percepita nel rendering del desktop.

Fino ad oggi bisognava abilitarlo manualmente. Da 6.8 in poi, funziona senza toccare nulla.

## Le altre novità principali

**Badge colorati per i monitor**: chi usa più schermi identici (stessa marca, stesso modello) sa quanto può essere frustrante capire quale monitor corrisponde a quale nell'interfaccia di impostazioni. Plasma 6.8 assegna un badge numerico colorato a ogni display nelle schermate di configurazione — finalmente.

**Registrazione audio in Spectacle**: il tool di screenshot/screencast integrato supporta ora la registrazione audio durante la registrazione dello schermo. Nessuna dipendenza da OBS per i casi d'uso semplici.

**Animazioni delle icone e notifiche più fluide**: miglioramenti alle transizioni con supporto a Unicode Emoji 17.

**Gestione accessori Bluetooth a batteria bassa**: Plasma 6.8 mostra notifiche quando un dispositivo Bluetooth connesso (mouse, tastiera, cuffie) ha la batteria scarica, anche durante le app a schermo intero.

**Slideshow wallpaper manuale**: puoi ora configurare uno slideshow di sfondi che non avanza automaticamente — cambia solo quando lo dici tu.

## KDE Linux: il sistema operativo basato su Flatpak

Parallelo alla release di Plasma 6.8, il team sta lavorando a **KDE Linux**, una variante del desktop basata su **BuildStream** e il **FreeDesktop Flatpak SDK** — lo stesso usato da GNOME OS. L'idea è un sistema operativo Linux desktop immutabile, aggiornato come un'unità e con le applicazioni gestite interamente via Flatpak.

Il progetto ha rallentato un po' a settembre per via di Akademy 2026, ma la condivisione dell'infrastruttura tra KDE Linux, GNOME OS e il Flatpak SDK significa che la manutenzione sarà distribuita tra più community — un approccio sensato per un progetto ambizioso.

## Come aggiornare quando sarà disponibile

La data di rilascio è il **14 ottobre 2026**. Se usi una distro rolling come Arch, openSUSE Tumbleweed o KDE Neon, l'aggiornamento arriverà nel giro di qualche giorno dopo il rilascio:

```bash
# Arch Linux
sudo pacman -Syu

# openSUSE Tumbleweed
sudo zypper dup

# KDE Neon
sudo pkcon update
```

Per distro con release fisse (Fedora, Ubuntu) bisognerà aspettare il prossimo ciclo di release — o usare Flatpak per alcune componenti.

## 30 anni di KDE

KDE è stato fondato il 14 ottobre 1996 da Matthias Ettrich, che voleva un desktop grafico coerente per Unix. In trent'anni è diventato uno degli ecosistemi open source più produttivi del mondo — non solo un desktop, ma un framework (Qt/KDE Frameworks), un suite di applicazioni (Okular, Dolphin, Kate, Kdenlive...) e ora la base di un potenziale sistema operativo immutabile.

Plasma 6.8 che arriva esattamente il giorno del trentesimo compleanno non sembra una coincidenza. Auguri, KDE.

---

*Fonti: [9to5Linux](https://9to5linux.com/kde-plasma-6-8-desktop-environment-is-coming-on-october-14th-heres-what-to-expect), [KDE Blogs](https://blogs.kde.org/2026/10/01/this-month-in-kde-linux-september-2026/), [Linuxiac](https://linuxiac.com/kde-plasma-6-8-enters-final-polishing-ahead-of-october-14-release/)*
