---
title: "Linux 7.1 è uscito: NTFS nativo, Intel FRED e addio a 140.000 righe di codice legacy"
rilevanza: "ALTA"
fonte: "https://www.phoronix.com/news/Linux-7.1-Released"
data_notizia: "2026-06-14"
tags: ["kernel", "linux", "ntfs", "filesystem", "aggiornamento", "intel"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: ottimo articolo per chi usa Linux su hardware misto Windows/Linux e si scontra spesso con le partizioni NTFS. Il driver nativo finalmente produzione-ready è una notizia concreta e utile.
---

# Linux 7.1 è uscito: NTFS nativo, Intel FRED e addio a 140.000 righe di codice legacy

Il 14 giugno 2026 Linus Torvalds ha annunciato Linux 7.1, e questa volta il changelog merita davvero una lettura. Non è uno di quei rilasci dove si aggiungono driver per hardware di nicchia e si sistemano micro-fix: il 7.1 porta cambiamenti che toccano il filesystem più usato su Windows, il modo in cui i processori Intel moderni gestiscono le interruzioni, e una pulizia di codice di proporzioni quasi storiche.

## Il driver NTFS che aspettavamo da anni

La novità più pratica per chi usa Linux su macchine dual-boot o collegate a dispositivi Windows è l'arrivo di un **driver NTFS completamente riscritto e finalmente pronto per la produzione**. Se hai mai avuto problemi di corruzione su partizioni NTFS, di montaggi in sola lettura, o di prestazioni scarse durante il trasferimento di file su chiavette USB formattate in NTFS — ecco, questa è la release per te.

Il nuovo driver è costruito con tecnologie moderne del kernel come `iomap` e `folios`, che migliorano l'efficienza di I/O e semplificano la manutenzione futura. A differenza del vecchio driver basato su ntfs3 (aggiunto nel 5.15 ma mai pienamente stabile) e del package userspace `ntfs-3g`, questo è tutto in-kernel e progettato per durare.

```bash
# Verifica che il modulo ntfs3 sia caricato
lsmod | grep ntfs

# Monta una partizione NTFS con il nuovo driver
sudo mount -t ntfs3 /dev/sdb1 /mnt/windows

# Oppure aggiungi a /etc/fstab per il montaggio automatico
# /dev/sdb1  /mnt/windows  ntfs3  defaults,uid=1000,gid=1000  0 0
```

## Intel FRED: interruzioni più efficienti sui chip moderni

Meno visibile per l'utente finale, ma importante sul lungo periodo: Linux 7.1 **abilita di default Intel FRED** (Flexible Return and Event Delivery) sui processori che lo supportano, a partire dalla famiglia Panther Lake.

FRED è il sostituto moderno del meccanismo di gestione delle interruzioni che il x86 si portava dietro dai tempi del 286. L'idea è semplice: invece di usare una cascata di meccanismi legacy per gestire interrupt, eccezioni e transizioni privilege-level, FRED usa un'unica interfaccia più pulita e sicura. Il risultato pratico è meno overhead nelle transizioni kernel/userspace e una base migliore per le ottimizzazioni future.

Se hai un Intel Panther Lake o successivo, questo aggiornamento ti arriva automaticamente con il kernel — nessuna configurazione richiesta.

## 140.000 righe di codice legacy: finalmente cestinato

Uno degli aspetti più interessanti del 7.1 è la **rimozione massiva di codice obsoleto**: oltre 140.000 righe eliminate in un colpo solo. Cosa c'era dentro?

- **Supporto per le sub-architetture x86 486**: se il tuo processore non ha una MMU completa e data la sua età probabilmente non lo stai più usando, il kernel non lo supporta più ufficialmente
- **Componenti PCMCIA legacy**: le schede PCMCIA sono un ricordo dei laptop degli anni '90
- **Driver di rete e subsystem obsoleti**: hardware che non esiste più sul mercato da decenni

Rimuovere codice morto non è banale — ogni riga in meno è una riga che non può introdurre bug, non deve essere aggiornata per le patch di sicurezza, non deve essere testata ad ogni rilascio. Il kernel Linux ha accumulato decenni di cruft, e questa pulizia è un segnale positivo di manutenzione attiva.

## Landlock: sandbox applicativa più potente

Per chi si interessa di sicurezza, il 7.1 espande anche **Landlock**, il security module del kernel per il sandboxing delle applicazioni. Le novità includono controlli aggiuntivi per i **socket di dominio UNIX**, che permettono alle applicazioni di comunicare localmente.

Questo significa che i software che usano Landlock (e la lista sta crescendo) possono ora limitare anche le comunicazioni IPC via Unix socket, non solo l'accesso al filesystem. Un passo avanti per chi costruisce applicazioni con privilege separation.

## Quando arriva nella tua distro?

Linux 7.1 è già disponibile su Arch Linux e derivate. Per le distro che seguono i rilasci LTS o hanno cicli più lunghi:

```bash
# Controlla la versione attuale del kernel
uname -r

# Su Arch: aggiornamento immediato
sudo pacman -Syu

# Su Fedora (versione in arrivo con il prossimo aggiornamento)
sudo dnf update kernel

# Ubuntu userà 7.1 come base per la prossima release intermedia;
# le LTS restano su kernel LTS dedicati
```

## In breve

Linux 7.1 è una delle release più sostanziose degli ultimi tempi: il driver NTFS produzione-ready da solo vale l'aggiornamento per chi lavora con file system misti. Se usi Arch o una rolling, aggiorna subito. Se sei su Fedora o Ubuntu, aspetta qualche settimana e arriva.
