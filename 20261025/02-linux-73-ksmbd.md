---
title: "Linux 7.3 è ufficiale: le novità e la falla critica nel file server KSMBD"
rilevanza: "ALTA"
fonte: "https://cybersecuritynews.com/linux-kernel-flaws-accidentally-disclosed/"
data_notizia: "2026-10-18"
tags: ["linux", "kernel", "sicurezza", "ksmbd", "smb", "aggiornamento"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: doppio interesse — le novità del kernel 7.3 per gli entusiasti Linux, e la vulnerabilità KSMBD che riguarda chiunque usi Linux come file server SMB in casa o in azienda. Utile anche per NAS hobbisti con TrueNAS o soluzioni simili.
---

# Linux 7.3 è ufficiale: le novità e la falla critica nel file server KSMBD

La settimana scorsa è stato un momento importante per il mondo Linux: il **kernel 7.3 è stato rilasciato ufficialmente il 18 ottobre 2026**, portando con sé miglioramenti significativi allo scheduler, a BPF e al supporto hardware. Quasi in contemporanea, però, sono emersi dettagli su **due falle critiche nel modulo KSMBD** — il server SMB integrato nel kernel — che chiunque gestisca condivisioni di file Linux dovrebbe conoscere.

## Le novità di Linux 7.3

Il kernel 7.3 non è una release rivoluzionaria, ma porta miglioramenti sostanziali in diverse aree:

### Scheduler migliorato per i grandi sistemi
Il componente che decide quale processo riceve tempo di CPU è stato ottimizzato per sistemi con molti core. Se hai un workstation moderna con 16+ thread o gestisci server, potresti notare una migliore reattività sotto carico intenso.

### BPF con supporto dati globali per CPU
**BPF** (Berkeley Packet Filter, ora rinominato eBPF nel gergo moderno) è la tecnologia che alimenta strumenti di osservabilità come Cilium, Falco e bpftrace. Il 7.3 introduce il supporto per **dati globali per-CPU** nelle mappe BPF, aprendo nuove possibilità per il monitoraggio e la sicurezza a basso overhead.

### Preparativi per AMD Zen 6 e Intel Panther Lake
Già nella finestra di merge di 7.4 (aperta pochi giorni dopo il rilascio di 7.3) sono arrivati i preparativi per le architetture future. Il power management è stato aggiornato per supportare al meglio le prossime CPU di AMD e Intel.

### Ubuntu 26.10 già basato su 7.3
Ubuntu 26.10 è uscito usando una release candidate di Linux 7.3 — la RC5 — come kernel base. Gli utenti Ubuntu che hanno già aggiornato stanno quindi già sperimentando parte di queste novità.

## La falla critica in KSMBD: cosa devi sapere

Nel mezzo delle celebrazioni per il nuovo kernel, Trend Micro's Zero Day Initiative ha reso pubblici accidentalmente i dettagli tecnici di **due vulnerabilità critiche nel modulo KSMBD** prima che le patch fossero pronte.

KSMBD è il server SMB/CIFS integrato nel kernel Linux, introdotto in Linux 5.15. Permette ai sistemi Linux di condividere file in rete usando lo stesso protocollo di Windows, senza necessità di Samba in userspace.

Le due falle hanno un punteggio **CVSS 9.0** e permettono a un attaccante remoto di:
- Eseguire codice arbitrario sul sistema
- Potenzialmente ottenere accesso root

### Sei a rischio?

Il modulo KSMBD è vulnerabile **solo se attivamente caricato e in uso**. Per verificare se lo hai attivo:

```bash
lsmod | grep ksmbd
```

Se il comando non restituisce nulla, non hai KSMBD caricato e non sei esposto.

Se invece lo hai attivo, per disabilitarlo temporaneamente:

```bash
sudo modprobe -r ksmbd
```

Per bloccare il caricamento automatico al riavvio, crea un file di configurazione:

```bash
echo "blacklist ksmbd" | sudo tee /etc/modprobe.d/ksmbd-blacklist.conf
sudo update-initramfs -u
```

### Chi usa KSMBD tipicamente?

Principalmente:
- Chi ha configurato condivisioni SMB native su Linux (senza Samba)
- Alcuni setup NAS con kernel Linux recente
- Container o VM che espongono condivisioni SMB

Se usi **Samba** (il pacchetto `samba` tradizionale in userspace), **non sei vulnerabile** a questi specifici bug — Samba non usa il modulo KSMBD.

## Quando arriveranno le patch?

Al momento della scrittura di questo articolo, le patch non sono ancora state rilasciate ufficialmente — i dettagli sono emersi prima che il processo di disclosure coordinata si completasse. Monitora gli aggiornamenti del tuo kernel distribuito:

```bash
# Su Debian/Ubuntu
apt list --upgradable 2>/dev/null | grep linux-image

# Su Fedora/RHEL
dnf check-update kernel

# Su Arch Linux (rolling release, aggiornamenti frequenti)
pacman -Qu linux linux-headers
```

## Come aggiornare il kernel

Una volta disponibili le patch:

```bash
# Debian/Ubuntu
sudo apt update && sudo apt upgrade linux-image-generic

# Fedora
sudo dnf update kernel

# Arch Linux
sudo pacman -Syu
```

Ricorda che l'aggiornamento del kernel richiede un riavvio per essere effettivo.

## Il quadro generale

Questa storia è un esempio classico di **responsible disclosure che va storta**: i dettagli tecnici di vulnerabilità critiche sono finiti su mailing list pubbliche prima che le fix fossero disponibili. Questo dà agli attaccanti informazioni dettagliate su come sfruttare la falla, con un vantaggio temporale rispetto ai difensori.

Per chi gestisce sistemi Linux esposti su reti non fidate (internet, reti aziendali miste), il consiglio è sempre lo stesso: mantieni aggiornato il kernel, limita i servizi esposti, e monitora gli aggiornamenti di sicurezza.

Il kernel 7.3 nel complesso è un ottimo aggiornamento — solo attenzione a KSMBD finché le patch non arrivano.
