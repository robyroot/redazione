---
title: "KDE Plasma 6.8 è ufficiale: addio a X11 dopo 30 anni"
rilevanza: "ALTA"
fonte: "https://kde.org/announcements/"
data_notizia: "2026-10-14"
tags: ["kde", "plasma", "x11", "wayland", "linux-desktop"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: storica svolta nel desktop Linux. KDE compie 30 anni e
  celebra l'anniversario togliendo il supporto a X11. È il momento giusto per spiegare ai
  lettori cosa cambia, se devono preoccuparsi e come prepararsi alla transizione Wayland.
---

# KDE Plasma 6.8 è ufficiale: addio a X11 dopo 30 anni

KDE ha compiuto 30 anni il 14 ottobre scorso, e ha deciso di festeggiare nel modo più iconico possibile: rilasciando **KDE Plasma 6.8**, la versione che segna la fine ufficiale del supporto alle sessioni X11. Un addio storico che chiude un'era e apre definitivamente le porte a Wayland come unico protocollo display di riferimento.

## Trent'anni di KDE, una svolta epocale

Il progetto KDE nacque il 14 ottobre 1996, quando lo studente tedesco Matthias Ettrich annunciò su Usenet la sua intenzione di creare un desktop grafico unificato per Unix. Da allora, KDE ha accompagnato milioni di utenti Linux attraverso decenni di evoluzione, da KDE 1 all'era di Plasma.

La versione 6.8 non è solo una release normale: è la **30th Anniversary Edition**, e la rimozione delle sessioni X11 non è un caso. È una dichiarazione d'intenti: il futuro del desktop Linux è Wayland, e KDE ci arriva a 30 anni dalla sua fondazione.

## Cosa cambia con Plasma 6.8

Le sessioni X11 di KDE Plasma vengono rimosse. In pratica, quando avvii una nuova sessione di login, non troverai più l'opzione "KDE Plasma (X11)" nel tuo display manager — solo la versione Wayland.

Per la maggior parte degli utenti, questo **non cambia quasi nulla** in termini di esperienza quotidiana. Wayland è stabile, maturo e in molti casi più performante di X11, specialmente su hardware moderno. Lo screenshot, le scorciatoie da tastiera, il multischermo e le animazioni funzionano bene da Plasma 6 in avanti.

Le novità di Plasma 6.8 includono:
- **Miglioramenti alla gestione multi-monitor** con Wayland
- **Nuova gestione delle gesture touchpad**
- **Task Manager migliorato** con anteprima finestre più fluida
- **KDE Connect** con supporto migliorato per dispositivi Android 15
- Correzioni di bug legate all'anniversary release

## Devo preoccuparmi della migrazione?

In breve: probabilmente no. Se usi già KDE Plasma 6.x su hardware recente, Wayland funziona già come default da Plasma 6.0 (uscito nel febbraio 2024). La rimozione di X11 è formale più che pratica per la maggior parte degli utenti.

I casi in cui potresti avere problemi:

```bash
# Controlla se stai usando X11 o Wayland
echo $WAYLAND_DISPLAY
echo $XDG_SESSION_TYPE
```

Se `XDG_SESSION_TYPE` restituisce `x11`, stai usando X11 e dovresti pianificare la migrazione.

**Casi ancora problematici con Wayland:**
- Applicazioni legacy che usano `xdotool` o `xrandr` direttamente
- Alcuni strumenti di screen recording professionali
- Certi setup multi-monitor con schede grafiche molto vecchie (pre-2015)
- Screen sharing in alcuni client Zoom/Teams vecchi

Per la maggior parte di questi casi esistono workaround o le app sono già state aggiornate.

## XWayland è ancora disponibile

Anche con sessioni X11 rimosse da Plasma, **XWayland** rimane disponibile. XWayland è un server di compatibilità che permette alle applicazioni X11 di girare dentro una sessione Wayland. Quindi le tue app vecchie continueranno a funzionare, semplicemente dentro Wayland invece che in una sessione X11 nativa.

```bash
# Verifica che XWayland sia installato
which Xwayland
# oppure
xwayland --version
```

## Come aggiornare a Plasma 6.8

Su **Arch Linux** (rolling release):
```bash
sudo pacman -Syu
```

Su **KDE Neon** (basato su Ubuntu LTS):
```bash
sudo apt update && sudo apt upgrade
```

Su **Fedora** (con aggiornamento a Fedora 45):
```bash
sudo dnf upgrade
```

Su **openSUSE Tumbleweed**:
```bash
sudo zypper dup
```

Le distribuzioni con ciclo di release fisso (Debian stable, Ubuntu LTS) riceveranno Plasma 6.8 nelle prossime versioni.

## Un traguardo storico

La rimozione di X11 da KDE è un momento che il mondo Linux aspettava da anni. Wayland è in sviluppo dal 2008 e nel 2024 ha raggiunto la maturità sufficiente per diventare default su quasi tutte le distribuzioni. Che KDE lo celebri rimuovendo il vecchio protocollo proprio nel suo 30° anniversario ha qualcosa di poetico.

Benvenuti nel futuro del desktop Linux.
