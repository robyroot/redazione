---
title: "KDE Plasma 6.8: dopo 30 anni X11 è ufficialmente fuori dal gioco"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/linuxiac-weekly-wrap-up-week-42-2026-october-12-18/"
data_notizia: "2026-10-14"
tags: ["kde", "plasma", "wayland", "x11", "linux desktop"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: la fine di X11 in KDE è un momento storico per il desktop Linux. Ottimo per spiegare ai lettori cosa cambia concretamente e perché Wayland vince. La notizia tocca sia utenti casual che sysadmin con setup multi-monitor o remote. Da abbinare a consigli pratici per la migrazione.
---

# KDE Plasma 6.8: dopo 30 anni X11 è ufficialmente fuori dal gioco

Questa settimana KDE ha rilasciato **Plasma 6.8** e con questa versione è arrivato il momento che molti attendevano (e qualcuno temeva): il **supporto alle sessioni X11 è stato rimosso**. Dopo trent'anni, il vecchio protocollo grafico lascia il posto definitivamente a Wayland come unica scelta supportata nel desktop KDE.

## Un addio storico

X11 (o X Window System) è stato il cuore del desktop Linux dal 1984. Per dare un'idea della sua longevità: esiste da prima che nascesse il kernel Linux stesso. Nel corso degli anni ha accumulato strati su strati di complessità, workaround e quirk che lo hanno reso sempre più difficile da mantenere e da estendere.

Wayland nasce nel 2008 proprio come risposta moderna a tutti questi problemi: architettura più pulita, sicurezza migliorata (le applicazioni non possono spiare le altre), migliore gestione degli schermi ad alta risoluzione e dei sistemi multi-monitor. L'unico ostacolo alla sua adozione di massa è stato il tempo necessario per raggiungere la parità di funzionalità con X11.

Con KDE Plasma 6.8, quel momento è arrivato.

## Cosa cambia per te in pratica?

Se usi KDE Plasma su una normale workstation o laptop con hardware recente, la risposta onesta è: **probabilmente non noti niente**. Anzi, potresti notare miglioramenti.

Con Wayland sotto il cofano ottieni:

- **Scaling migliore** su schermi HiDPI e configurazioni miste (es. uno schermo 4K e uno FHD)
- **Sicurezza maggiore**: le app non possono fare screenshotting di altre finestre o intercettare input da tastiera di altre applicazioni
- **Animazioni più fluide**, specialmente su compositing hardware
- **Latenza ridotta** con touchpad e touchscreen

## E se hai hardware o software legacy?

Qui la situazione è più complessa. Ci sono categorie di utenti che X11 continuavano a usare per buone ragioni:

**Remote desktop e VNC**: X11 aveva un supporto nativo per la remotizzazione tramite SSH e altri strumenti. Con Wayland il forwarding di applicazioni remoto tramite `ssh -X` non funziona più. La soluzione moderna è usare strumenti come **KRFB** (il VNC server di KDE), **RDP via KDE**, o soluzioni come **Rustdesk**.

**Touchpad e tablet grafici**: La compatibilità è migliorata molto, ma alcuni tablet Wacom o dispositivi di input meno comuni potrebbero avere ancora qualche problema.

**App X11-only con xwayland**: La maggior parte delle vecchie applicazioni X11 funziona tramite **XWayland**, un layer di compatibilità incluso di default. Non devi fare nulla — le app girano e basta, anche se tecnicamente stanno usando X11 "all'interno" di Wayland.

## Come verificare se stai già usando Wayland

```bash
# Mostra il tipo di sessione corrente
echo $XDG_SESSION_TYPE

# Output atteso:
# wayland   → sei su Wayland
# x11       → sei ancora su X11
```

## Aggiornare a Plasma 6.8

**Arch Linux / Manjaro:**
```bash
sudo pacman -Syu plasma-desktop
```

**KDE neon:**
```bash
sudo apt update && sudo apt dist-upgrade
```

**openSUSE Tumbleweed:**
```bash
sudo zypper dup
```

Dopo l'aggiornamento, al prossimo login seleziona la sessione **"Plasma (Wayland)"** dalla schermata di login se non è già quella di default.

## Anche il KDE LTS dice addio a X11

Un altro dettaglio interessante di questa release: **Plasma 6.6.7**, il primo aggiornamento della serie LTS (Long Term Support), è uscito in contemporanea. Anche la versione LTS è Wayland-only. Non c'è dunque una via di mezzo che permetta di restare su X11 con supporto continuato: la transizione è definitiva.

## Il desktop Linux cresce

La rimozione di X11 da KDE arriva pochi mesi dopo che GNOME aveva già fatto lo stesso passo. I due principali ambienti desktop Linux hanno entrambi deciso: Wayland è il presente e il futuro, X11 è storia.

Non è una notizia da prendere con tristezza — è il segno che il desktop Linux è cresciuto abbastanza da potersi permettere di tagliare il peso del passato. Per gli utenti finali significa un sistema più moderno, sicuro e performante. E per chi ha casi d'uso particolari, gli strumenti di compatibilità ci sono.

Trent'anni di X11 meritano un applauso. E poi si va avanti.
