---
title: "GNOME Boxes si trasforma: addio pacchetti distro, tutto su Flatpak"
rilevanza: "MEDIA"
fonte: "https://blogs.gnome.org/feborges/future-of-boxes/"
data_notizia: "2026-08-05"
tags: ["linux", "GNOME", "Flatpak", "desktop", "virtualizzazione"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: GNOME Boxes è lo strumento di virtualizzazione più accessibile per i neofiti Linux. Il passaggio a Flatpak-only è una mossa coraggiosa che semplifica la manutenzione ma solleva domande sulla distribuzione tradizionale. Ottima occasione per spiegare cos'è Flatpak e perché il futuro del software Linux potrebbe andare in questa direzione.
---

# GNOME Boxes si trasforma: addio pacchetti distro, tutto su Flatpak

GNOME Boxes, il tool di virtualizzazione pensato per chi vuole creare macchine virtuali senza impazzire con configurazioni complesse, sta per rinascere. Felipe Borges, unico sviluppatore attivo del progetto, ha annunciato una riscrittura completa dell'applicazione — e la novità più grande è che d'ora in poi **Boxes sarà distribuito solo come Flatpak**.

Niente più pacchetti `.deb`, `.rpm` o installazioni da repository di sistema. Solo Flathub.

## Due anni di lavoro sotto il cofano

Borges ha trascorso gli ultimi due anni a riscrivere Boxes da zero, con tre obiettivi chiari:

**1. Passare a GTK4 e libadwaita**
La versione attuale di Boxes usa ancora GTK3 e si vede: l'interfaccia appare datata rispetto al resto del desktop GNOME moderno. La migrazione a GTK4 e libadwaita porta animazioni fluide, supporto corretto alle preferenze di sistema (dark mode, accenti di colore) e un look finalmente coerente con il resto di GNOME 50.

**2. Adottare Flatpak come unico canale di distribuzione**
Mantenere il codice compatibile con decine di distribuzioni diverse — ognuna con le sue versioni di QEMU, libvirt, virsh — è un incubo di manutenzione per un team di uno. Con Flatpak, Borges può includere l'intera stack di virtualizzazione nel bundle, controllando esattamente quali versioni usare e come configurarle.

**3. Semplificare la gestione di Windows 11**
La nuova versione installa Windows 11 senza i soliti riti: niente workaround manuali per Secure Boot, niente emulazione del TPM fatta a mano. Boxes se ne occupa da solo.

## Cosa cambia per te

Se hai già Boxes installato tramite i pacchetti della tua distro, puoi continuare a usarlo — ma le versioni nei repository non riceveranno più nuove funzionalità. Gli aggiornamenti futuri arriveranno solo via Flathub.

```bash
# Installa Flatpak se non ce l'hai già
sudo apt install flatpak          # Debian/Ubuntu
sudo dnf install flatpak          # Fedora

# Aggiungi il repository Flathub
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

# Installa GNOME Boxes (quando sarà disponibile la versione stabile)
flatpak install flathub org.gnome.Boxes
```

La versione beta è già disponibile per chi vuole provarla. Il rilascio stabile è previsto insieme a **GNOME 51**, in settembre 2026.

## Perché Flatpak è la strada giusta (o quasi)

Il movimento verso Flatpak per le app GNOME non è una novità. Molte app desktop GNOME già distribuiscono su Flathub come canale primario: Foliate, Apostrophe, Amberol. Boxes era rimasto indietro.

Il vantaggio principale è la **prevedibilità**: l'app gira nello stesso sandbox ovunque, con le stesse dipendenze. Niente "funziona su Fedora ma non su Ubuntu" o viceversa.

Lo svantaggio, che alcuni puristi sottolineano, è che i Flatpak tendono ad avere un'impronta su disco maggiore e che il sandboxing può complicare l'accesso a risorse di sistema — rilevante soprattutto per un'app di virtualizzazione che deve parlare direttamente con il kernel.

Borges è consapevole di queste preoccupazioni e ha scritto nel suo blog che il controllo sulla stack di virtualizzazione che ottiene con Flatpak vale ampiamente il trade-off.

## GNOME Boxes: a chi serve?

Se sei un utente Linux intermedio e vuoi creare rapidamente una VM per testare una distro, un software sospetto, o per tenere un ambiente Windows isolato, Boxes è ancora la scelta più semplice. Non ha la potenza di virt-manager o Proxmox, ma si configura in tre click.

Con questa riscrittura, il progetto riceve la cura che meritava. E il fatto che un singolo developer regga tutto questo è, diciamocelo, impressionante.
