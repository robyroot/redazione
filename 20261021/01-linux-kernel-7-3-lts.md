---
title: "Linux Kernel 7.3: ecco il prossimo LTS con FailFS e scheduler rinnovato"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/linuxiac-weekly-wrap-up-week-42-2026-october-12-18/"
data_notizia: "2026-10-18"
tags: ["linux", "kernel", "lts", "rust", "filesystem"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: approfondire le novità del kernel con focus su Rust e FailFS, utile sia per utenti desktop che per sysadmin.
---

## Linux Kernel 7.3: il prossimo LTS è arrivato

Linus Torvalds ha rilasciato il kernel Linux 7.3 il 18 ottobre 2026, e le notizie per la comunità Linux non potrebbero essere migliori: questa sarà molto probabilmente il prossimo kernel **Long Term Support (LTS)**. Se hai una distribuzione stabile o un server, questo è il kernel che ti accompagnerà per i prossimi anni.

## Cosa c'è di nuovo nel kernel 7.3?

Il changelog di questa release è ricco di novità interessanti. Vediamo le più significative.

### FailFS: il nuovo filesystem per i test

Una delle aggiunte più curiose è **FailFS**, un filesystem pensato appositamente per simulare guasti del disco durante i test. Sembra strano, no? Ma per chi sviluppa applicazioni critiche o vuole testare come il proprio software reagisce a errori di I/O, è un regalo prezioso.

Con FailFS puoi montare un filesystem che fallisce intenzionalmente in modi configurabili, permettendoti di verificare che la tua app gestisca correttamente le eccezioni. Chi si occupa di database, backup automatici o qualsiasi software che scrive su disco troverà questo strumento utilissimo per i propri test di resilienza.

### Scheduler CPU completamente rinnovato

Il **process scheduler** di Linux — il componente che decide quale processo gira su quale CPU e quando — ha ricevuto una revisione importante. Il precedente CFS (Completely Fair Scheduler) era in servizio da quasi vent'anni, e sebbene funzionasse bene, mostrava qualche limite su sistemi moderni con decine di core e workload eterogenei.

Il nuovo scheduler migliora la latenza delle applicazioni interattive (ottimo per il desktop) e ottimizza l'utilizzo dei core sui processori con architetture ibride come gli Intel con P-core ed E-core, o i processori ARM big.LITTLE. In pratica: il tuo desktop dovrebbe sentirsi più reattivo, soprattutto sotto carico.

### Rust avanza ancora

Continua l'espansione del supporto **Rust** nel kernel. Ormai non è più una sperimentazione: diversi driver sono stati riscritti in Rust e altri sono in arrivo. Il vantaggio principale? Rust garantisce a livello di compilatore l'assenza di certi bug di memoria (use-after-free, buffer overflow), rendendo queste porzioni di codice intrinsecamente più sicure.

Per gli utenti finali questo si traduce in un kernel più robusto e meno vulnerabile a certe categorie di attacchi comuni.

### OverlayFS migliorato e supporto hardware espanso

**OverlayFS** — il filesystem usato da Docker, Podman e praticamente tutti i container runtime — ha ricevuto miglioramenti di performance. Chi lavora con container noterà operazioni più veloci, in particolare durante la creazione e la distruzione di container con molti layer.

Il supporto hardware è stato esteso con nuovi driver per GPU, dispositivi NVMe e controller di rete. Le distribuzioni basate su kernel 7.3 dovrebbero avere un hardware coverage migliore out of the box.

## Chi lo ha già adottato?

**Ubuntu 26.10**, uscita il 15 ottobre, è arrivata proprio con il kernel 7.3 a bordo, confermando che questa release è già pronta per l'uso quotidiano. Fedora 45, attesa per il 27 ottobre, lo includerà anch'essa.

Se vuoi provarlo subito su una distribuzione rolling come Arch o openSUSE Tumbleweed:

```bash
# Su Arch Linux (aggiornamento standard)
sudo pacman -Syu

# Su openSUSE Tumbleweed
sudo zypper dup

# Verifica la versione del kernel installata
uname -r
```

Per compilarlo da sorgente — se sei il tipo che ama farlo:

```bash
# Scarica i sorgenti
wget https://cdn.kernel.org/pub/linux/kernel/v7.x/linux-7.3.tar.xz
tar -xf linux-7.3.tar.xz
cd linux-7.3

# Usa la config del kernel attuale come punto di partenza
cp /boot/config-$(uname -r) .config
make olddefconfig

# Compila con tutti i core disponibili
make -j$(nproc)
sudo make modules_install install
```

## Perché il tag LTS conta

Se sei un utente desktop potresti chiederti: perché mi interessa se è LTS? La risposta è semplice: le distribuzioni che puntano alla stabilità — Ubuntu LTS, Debian, RHEL, Rocky Linux, AlmaLinux — basano le proprie release principali sui kernel LTS. Un kernel LTS riceve aggiornamenti di sicurezza e correzioni per 5-6 anni, garantendo una base affidabile nel tempo.

Significa che se installi Ubuntu 28.04 LTS (o qualunque distro LTS uscirà nel 2028), è probabile che sotto il cofano troverai proprio il kernel 7.3.

## Conclusione

Il kernel 7.3 è una release solida che porta innovazioni significative senza stravolgere la stabilità. Con lo scheduler rinnovato, l'avanzamento di Rust, FailFS e i miglioramenti a OverlayFS, chi usa Linux sia sul desktop che in produzione ha buone ragioni per aspettare con entusiasmo che la propria distro lo adotti. E con Ubuntu 26.10 già disponibile, non devi aspettare molto.
