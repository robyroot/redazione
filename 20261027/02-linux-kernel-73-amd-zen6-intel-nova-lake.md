---
title: "Linux Kernel 7.3: novità, AMD Zen6, Intel Nova Lake e tante sorprese"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/linuxiac-weekly-wrap-up-week-43-2026-october-19-25/"
data_notizia: "2026-10-18"
tags: ["linux", "kernel", "AMD", "Intel", "Ubuntu", "Rust"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: il kernel 7.3 è una release di rilievo con hardware support notevole (Zen6 e Nova Lake) e passi avanti significativi su Rust. Ottimo spunto per spiegare perché gli aggiornamenti del kernel contano anche per l'utente normale. Ubuntu 26.10 che lo porta come base è un gancio perfetto per i lettori Debian/Ubuntu.
---

# Linux Kernel 7.3: novità, AMD Zen6, Intel Nova Lake e tante sorprese

Il 18 ottobre 2026 Linus Torvalds ha rilasciato **Linux 7.3**, la nuova versione stabile del kernel che porta con sé un bel po' di novità. Non si tratta di una release rivoluzionaria come può esserlo il passaggio da una major all'altra, ma è una di quelle versioni che gli utenti di hardware recente aspettavano con impazienza.

## Supporto hardware: AMD Zen6 e Intel Nova Lake

La novità più attesa riguarda il supporto hardware di nuova generazione. Il kernel 7.3 introduce l'**abilitazione completa di AMD Zen6**, l'architettura che AMD sta portando nelle CPU Ryzen di settima generazione. Questo significa ottimizzazioni a basso livello, driver aggiornati e performance migliori su sistemi moderni.

Sul fronte Intel, arriva il **supporto stabile per la GPU integrata Intel Xe3P Nova Lake** — la grafica integrata della famiglia di processori Nova Lake. Se hai (o hai intenzione di avere) un laptop con questi chip, con il kernel 7.3 le cose funzioneranno senza bisogno di patch manuali o kernel personalizzati.

## Una nuova system call: fchroot()

Tra le aggiunte a livello di sistema operativo, spicca **`fchroot()`**, una nuova system call che estende le capacità di `chroot()`. Permette di effettuare il chroot utilizzando un file descriptor invece di un path, il che apre la porta a pattern di container isolation più sicuri e flessibili.

```bash
# Per verificare le system call disponibili nel tuo kernel
ausyscall --dump | grep chroot
```

## Rust nel kernel: avanti tutta

Il kernel 7.3 continua il percorso di integrazione di **Rust** come secondo linguaggio ufficiale del kernel Linux. Le novità includono nuove strutture dati implementate in Rust (XArray bindings), miglioramenti al lavoro sui driver e statistiche positive: la base di codice Rust nel kernel continua a crescere release dopo release.

Per chi si chiede perché importa: Rust elimina interi classi di vulnerabilità legate alla memoria (buffer overflow, use-after-free) che storicamente hanno afflitto il codice C del kernel. Non è una rivoluzione immediata, ma è un investimento a lungo termine sulla sicurezza del sistema.

## Miglioramenti allo scheduler e virtualizzazione

Il kernel 7.3 porta miglioramenti allo **scheduler** per sistemi con molti core, in particolare per macchine NUMA di grandi dimensioni usate in ambito server. Sul fronte virtualizzazione, arrivano ottimizzazioni per il **working-set tracking** che migliorano le performance dei guest sotto KVM.

Migliorie anche a **BPF** (Berkeley Packet Filter), lo strumento che ormai è ovunque: networking, sicurezza, tracing, observability.

## BeamFS: un nuovo filesystem proposto

Una novità interessante ancora in fase di proposta: **BeamFS**, un filesystem pensato per storage ad altissima velocità. Il progetto è stato inviato per revisione nella finestra di merge del 7.3 e potrebbe fare capolino nelle prossime versioni. Non c'è ancora molto di pubblico sui dettagli tecnici, ma il nome è già comparso nelle mailing list ufficiali.

## Ubuntu 26.10 porta il kernel 7.3 sul desktop

**Ubuntu 26.10**, rilasciato a sua volta questa settimana, usa Linux 7.3 come base. Questo significa che se hai aggiornato o installato Ubuntu 26.10, stai già girando sul nuovo kernel.

```bash
# Verifica la versione del kernel in uso
uname -r

# Su Ubuntu, per aggiornare
sudo apt update && sudo apt upgrade
sudo reboot
```

## Come installare il kernel 7.3 su distribuzioni rolling

Se usi Arch Linux, Manjaro, openSUSE Tumbleweed o altre rolling release, il kernel 7.3 arriva (o arriverà presto) tramite gli aggiornamenti normali:

```bash
# Arch Linux
sudo pacman -Syu linux linux-headers

# Per vedere il kernel corrente dopo il riavvio
uname -r
```

Per chi usa Ubuntu LTS o Fedora, il backport arriverà più avanti. La pazienza è d'obbligo.

## Falle nel kernel esposte prima del patch

Vale la pena menzionare anche una notizia meno positiva: alcune vulnerabilità critiche del kernel (tra cui due nel KSMBD file server con CVSS 9.0) sono finite per errore su mailing list pubbliche **prima** che le patch fossero pronte. Greg Kroah-Hartman, uno dei maintainer principali, ha commentato con tono irritato la situazione. Le correzioni sono ora disponibili negli aggiornamenti stabili del kernel.

---

Il kernel 7.3 è una release solida con attenzione al hardware moderno e alla qualità del codice. Se hai hardware AMD o Intel di nuova generazione, vale la pena aggiornare.
