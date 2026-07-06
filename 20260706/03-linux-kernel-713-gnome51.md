---
title: "Linux 7.1.3 disponibile con patch critiche, GNOME 51 Alpha in arrivo"
rilevanza: "MEDIA"
fonte: "https://www.linuxcompatible.org/story/linux-kernel-713-released-security-patches-nfs-fixes-and-mips-reboot-resolution/"
data_notizia: "2026-07-04"
tags: ["linux", "kernel", "GNOME", "aggiornamento", "desktop", "KDE"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: riepilogo settimanale del mondo Linux desktop + kernel per chi vuole restare aggiornato senza leggere mille fonti. Tono pratico: cosa è uscito, perché importa, come aggiornare. Buon articolo "da tenere aperto" per chi vuole capire lo stato dell'ecosistema Linux a luglio 2026.
---

# Linux 7.1.3 disponibile con patch critiche, GNOME 51 Alpha in arrivo

Settimana piena di aggiornamenti per l'ecosistema Linux. Il kernel 7.1.3 è uscito con una serie di fix di sicurezza importanti, GNOME 51 ha raggiunto la fase Alpha con novità interessanti, e KDE Gear ha rilasciato l'ultima versione della serie 26.04. Vediamo cosa c'è da sapere.

## Linux Kernel 7.1.3: sicurezza e stabilità

Il kernel 7.1.3 è uscito il 4 luglio 2026, ventuno giorni dopo il rilascio della feature release 7.1. È un aggiornamento di stabilità e sicurezza, e in questa settimana in particolare vale doppio installarla: include le patch per le vulnerabilità DirtyClone e Bad Epoll di cui abbiamo parlato separatamente.

Le correzioni principali riguardano:

- **ksmbd**: fix per un heap read out-of-bounds nel server SMB del kernel (rilevante per chi condivide file in rete locale)
- **KVM AMD SEV**: fix per un page overflow nella virtualizzazione sicura AMD — importante per chi usa VM con crittografia
- **Hyper-V**: fix per un bounds check failure nella virtualizzazione nested su macchine Windows/Azure
- **NFS server**: circa una dozzina di commit per fix su ACL leak e race condition nella gestione dello stato
- **MIPS PREEMPT_RT**: fix per un hang al reboot che bloccava gli upgrade su router OpenWrt

Per aggiornare:

```bash
# Ubuntu / Debian
sudo apt update && sudo apt full-upgrade

# Fedora
sudo dnf upgrade --refresh

# Arch Linux
sudo pacman -Syu

# Verifica versione
uname -r
```

## GNOME 51 Alpha: cosa c'è di nuovo

GNOME 51 è entrato in fase Alpha — significa che è disponibile per chi vuole testare, non è ancora per la produzione, ma dà un'idea chiara di dove sta andando il desktop.

Le novità più interessanti:

- **Luminosità dei monitor salvata e ripristinata**: finalmente! Il livello di luminosità sopravvive al riavvio, GNOME la ricorda per ogni schermo connesso.
- **Griglia delle app più accessibile**: miglioramenti nell'accessibilità (screen reader, navigazione da tastiera).
- **Supporto a elogind come provider libsystemd**: buona notizia per chi usa distro non-systemd — GNOME diventa più portabile.
- **Shelly 2.4.1.1**: il gestore di Flatpak integrato ora permette di installare app direttamente dal sito Flathub cliccando il pulsante "Install" nel browser.

GNOME 51 finale è atteso per settembre 2026, nel ciclo di rilascio semestrale.

## KDE Gear 26.04.3: l'ultima della serie

KDE Gear 26.04.3 è uscito il 2 luglio come ultimo aggiornamento della serie 26.04. Migliorie minori ma utili:

- **Elisa** (music player): small improvements alla UI
- **KDE Itinerary**: aumento della larghezza dei drawer per visualizzare meglio i dettagli dei viaggi
- **Kdenlive** (video editor): fix per crash all'uscita e quando si tenta di registrare senza dispositivo audio

La prossima versione major di KDE Gear sarà la 26.08, attesa per agosto.

## Lo stato del desktop Linux a luglio 2026

Se guardi il quadro d'insieme, il desktop Linux è in ottima forma. KDE Linux, la distribuzione ufficiale del progetto KDE, ha abbracciato completamente Flatpak come formato di distribuzione delle applicazioni aggiuntive. T2 Linux 26.6 ha portato il kernel 7.0 con un desktop Wayland+Plasma completamente riproducibile. Arch Linux ISO di luglio include kernel 7.0.14 e systemd 261.1.

Per chi usa Linux come desktop principale, il consiglio solito: aggiorna regolarmente, non rimandare le patch di sicurezza, e se vuoi sperimentare con GNOME 51 tienilo in una VM o una partizione dedicata prima che arrivi la release stabile.
