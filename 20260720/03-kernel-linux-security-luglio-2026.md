---
title: "Kernel Linux 7.1.4, 6.18.39 e 6.12.96: centinaia di fix di sicurezza, aggiorna prima del weekend"
rilevanza: "MEDIA"
fonte: "https://www.linuxcompatible.org/story/linux-kernel-714-61839-and-61296-released-today-with-heavy-security-fixes"
data_notizia: "2026-07-18"
tags: ["linux", "kernel", "sicurezza", "aggiornamento", "LTS", "io_uring", "FUSE", "XFS"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: release importante con un volume insolito di patch (357-534 commit). L'enfasi sui sottosistemi specifici (io_uring, FUSE, XFS) è tecnica ma accessibile e mostra quanto lavoro avviene "sotto il cofano". Ottimo per sysadmin e utenti Linux avanzati.
---

# Kernel Linux 7.1.4, 6.18.39 e 6.12.96: centinaia di fix di sicurezza, aggiorna prima del weekend

Il 18 luglio 2026 Greg Kroah-Hartman ha annunciato il rilascio simultaneo di tre aggiornamenti kernel stable e LTS: **7.1.4**, **6.18.39** e **6.12.96**. Numeri che potrebbero sembrare routine, ma che questa volta portano con sé un volume di patch insolito: da 357 a oltre 534 commit per branch, con un focus pesante sulla sicurezza.

## Cosa cambia in questi aggiornamenti

Le aree principali toccate da questi release:

### io_uring: race conditions critiche

**io_uring** è il sottosistema di I/O asincrono moderno del kernel Linux, usato sempre più spesso da applicazioni ad alte prestazioni: database come RocksDB, runtime async come tokio di Rust, e tante applicazioni server di nuova generazione. Questo ciclo di fix chiude diverse race condition che in condizioni specifiche potevano portare a use-after-free o corruzione di memoria — esattamente il tipo di bug che apre la strada a privilege escalation.

### FUSE: filesystem in userspace

**FUSE** (Filesystem in Userspace) permette di montare filesystem implementati nello spazio utente. Lo usano rclone per accedere a cloud storage come Google Drive o S3, sshfs per montare cartelle remote, strumenti di virtualizzazione e container. I fix in questo batch correggono inconsistenze nella gestione del ciclo di vita degli inode e buffer check mancanti che potevano portare a comportamenti indefiniti.

### XFS: integrità del filesystem

Diversi fix riguardano **XFS**, il filesystem usato di default da molte distribuzioni enterprise (RHEL, Rocky Linux, AlmaLinux) e consigliato per workload intensivi. Le patch correggono problemi di integrità dei metadati in scenari di accesso concorrente — importanti per chi usa XFS su storage di produzione.

### Driver touchscreen: buffer overflow

Alcuni driver touchscreen contenevano buffer overflow che, in scenari con hardware fisico connesso, potevano essere sfruttati localmente. Fix minori ma necessari per sistemi embedded e laptop con touchscreen.

## Gli LTS: l'elenco completo

Insieme alle tre release principali, Greg ha rilasciato anche gli aggiornamenti per i rami LTS attivi:

| Branch | Nuova versione |
|--------|----------------|
| 6.18 LTS | 6.18.39 |
| 6.12 LTS | 6.12.96 |
| 6.6 LTS | 6.6.144 |
| 6.1 LTS | 6.1.177 |
| 5.15 LTS | 5.15.211 |
| 5.10 LTS | 5.10.260 |

Se la tua distribuzione usa uno di questi branch (e quasi certamente lo usa), l'aggiornamento è già disponibile o in arrivo.

## Come aggiornare

Su **Ubuntu/Debian**:

```bash
sudo apt update && sudo apt dist-upgrade
sudo reboot
```

Su **Fedora**:

```bash
sudo dnf update kernel
sudo reboot
```

Su **Arch Linux** (rolling, aggiornato più velocemente):

```bash
sudo pacman -Syu
sudo reboot
```

Dopo il riavvio, controlla la versione del kernel attivo:

```bash
uname -r
```

## Perché questa release è più pesante del solito

Il numero di commit è significativamente più alto rispetto a un ciclo normale. Ci sono alcune spiegazioni plausibili: l'impiego crescente di tool di analisi statica automatizzata, l'uso di AI nella ricerca di vulnerabilità (un tema molto caldo nel 2026), e il fatto che alcune sezioni di codice storicamente poco toccate stiano finalmente ricevendo revisioni sistematiche.

Proprio questa settimana è emersa **Bad Epoll** (CVE-2026-46242), una vulnerabilità critica sempre nel kernel Linux. Il batch di luglio non è correlato direttamente a Bad Epoll — che ha una sua patch dedicata — ma il contesto generale è chiaro: il kernel è sotto esame più che mai.

Se gestisci server, pianifica l'aggiornamento nel prossimo ciclo di manutenzione. Se usi Linux sul desktop, un `update + reboot` durante la pausa caffè risolve tutto. Con exploit pubblici in circolazione su più fronti, non c'è motivo per rimandare.
