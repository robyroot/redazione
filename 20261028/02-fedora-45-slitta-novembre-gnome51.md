---
title: "Fedora 45 slitta a novembre: GNOME 51 e le novità che ci aspettano"
rilevanza: "MEDIA"
fonte: "https://phoronix.com/news/Fedora-45-Second-NO-GO"
data_notizia: "2026-10-27"
tags: ["fedora", "linux", "gnome", "distro", "kernel"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: spiegare cosa contiene Fedora 45, perché è stata ritardata, e cosa significa per gli utenti che aspettano la release. Tono informativo e tranquillo, niente allarmismo: i ritardi sono normali nel ciclo di sviluppo.
---

# Fedora 45 slitta a novembre: GNOME 51 e le novità che ci aspettano

Se aspettavi Fedora Linux 45 per ottobre, dovrai pazientare ancora qualche settimana. La release, originariamente pianificata per il 20 ottobre 2026, ha totalizzato ben **due NO-GO** consecutivi dal team di sviluppo. L'ultimo, comunicato il 27 ottobre, sposta ufficialmente la data a **novembre 2026**.

Non è una catastrofe — i ritardi nelle release di Fedora non sono rari — ma vale la pena capire cosa sta succedendo e cosa troveremo quando la distro arriverà finalmente.

## Perché il ritardo?

Il processo di rilascio di Fedora prevede riunioni Go/No-Go in cui i team valutano se la release candidate è abbastanza stabile per essere distribuita agli utenti. In entrambi i casi di ottobre, **non era disponibile una release candidate adatta** per la valutazione: troppi bug bloccanti aperti per procedere in sicurezza.

È la prova che il processo di qualità funziona: meglio aspettare due settimane in più che rilasciare una versione instabile a milioni di utenti.

## Cosa porta Fedora 45

Nonostante il ritardo, le novità programmate per Fedora 45 sono sostanziose.

### GNOME 51

L'aggiornamento più visibile. GNOME 51 porta miglioramenti all'app Files (Nautilus), nuove animazioni nella shell, ottimizzazioni per i display ad alto DPI e un editor di testo aggiornato. Chi usa KDE Plasma troverà invece la versione **6.7**.

### Linux Kernel 7.2

Fedora 45 includerà il kernel 7.2, con supporto migliorato per hardware recente: nuove schede grafiche AMD e Intel, controller NVMe di ultima generazione, e ottimizzazioni per i processori ARM moderni.

### Python 3.15 e GCC 16.2

Per chi sviluppa, questi sono aggiornamenti significativi. Python 3.15 porta importanti ottimizzazioni al garbage collector e nuove funzionalità del linguaggio, mentre GCC 16.2 introduce nuove ottimizzazioni per le architetture moderne.

### KMSCON Console

Una delle novità più interessanti è l'introduzione di **KMSCON**, un emulatore di terminale virtuale che sostituisce il vecchio VT (virtual terminal) del kernel per la console testuale. Il risultato: font migliori, Unicode completo e animazioni più fluide anche senza X11 o Wayland.

### Modifiche alla sicurezza

Fedora 45 introduce alcune modifiche alle policy di sicurezza predefinite, inclusa la disabilitazione di algoritmi crittografici considerati obsoleti come alcune cipher suite TLS legacy.

## Come aggiornare quando uscirà

Per chi già usa Fedora 44, l'aggiornamento sarà disponibile tramite `dnf system-upgrade`:

```bash
# quando Fedora 45 sarà disponibile
sudo dnf upgrade --refresh
sudo dnf install dnf-plugin-system-upgrade
sudo dnf system-upgrade download --releasever=45
sudo dnf system-upgrade reboot
```

Il sistema si riavvierà e completerà l'upgrade offline, riducendo i rischi di conflitti con processi in esecuzione.

## Quando esce davvero?

Non c'è ancora una data ufficiale confermata per novembre. Il calendario di Fedora prevede riunioni go/no-go con cadenza settimanale, quindi seguire il Fedora Magazine o la mailing list `fedora-devel` è il modo migliore per restare aggiornati.

Nel frattempo, se hai bisogno di GNOME 51 subito, puoi testarlo su **Ubuntu 26.10** "Stonking Stingray" (disponibile dal 15 ottobre) o su **Arch Linux** dove GNOME 51 è già nei repository da qualche settimana.

La buona notizia è che il ritardo indica un team che non fa compromessi sulla qualità. Quando Fedora 45 arriverà, dovrebbe essere una release solida.
