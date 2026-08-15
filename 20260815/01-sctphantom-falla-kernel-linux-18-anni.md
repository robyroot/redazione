---
title: "SCTPhantom: la falla nel kernel Linux vecchia di 18 anni che regala root e buca i container"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/08/18-year-old-linux-sctp-flaw-could-let.html"
data_notizia: "2026-08-07"
tags: ["linux", "kernel", "sicurezza", "vulnerabilità", "container", "sctphantom"]
livello: "intermediate"
nota_editoriale: |
  Ottimo pezzo per il pubblico "smanettone" di RobyRoot: spiega cos'è SCTP (protocollo poco noto ai più),
  perché una use-after-free può restare nascosta 18 anni, e soprattutto dai indicazioni pratiche —
  come verificare se il modulo sctp è caricato e come disabilitarlo se non serve, oltre al link
  diretto agli aggiornamenti kernel di Debian/Ubuntu. Buon gancio anche per un mini-tutorial
  "come controllare la versione del proprio kernel e aggiornarlo in sicurezza".
---

Ogni tanto salta fuori una di quelle notizie che ti fanno pensare: "aspetta, questo bug esisteva da PRIMA che io avessi il primo smartphone?". È esattamente il caso di **SCTPhantom** (CVE-2026-64564), una vulnerabilità scoperta nel kernel Linux che affonda le radici in codice scritto nel dicembre 2007, ai tempi di Linux 2.6.25. Diciotto anni di onorato servizio, passati totalmente inosservati, prima che qualcuno se ne accorgesse.

## Cos'è successo, in parole povere

Il problema riguarda **SCTP** (Stream Control Transmission Protocol), un protocollo di trasporto meno famoso di TCP e UDP ma comunque presente in tantissimi sistemi Linux, spesso caricato di default anche se non lo usi mai attivamente. Il kernel gestisce male una particolare sequenza di pacchetti ASCONF (quelli che servono a riconfigurare gli indirizzi di una connessione SCTP al volo): un mismatch tra l'indirizzo sorgente del pacchetto e quello dichiarato nel parametro ASCONF permette di liberare (free) una struttura dati che il kernel continua però a usare subito dopo. Questo si chiama **use-after-free**, ed è uno dei bug più pericolosi che puoi avere in un kernel: l'attaccante riesce a manipolare quella memoria "fantasma" (da qui il nome SCTPhantom) per eseguire codice con i privilegi più alti possibili.

Tradotto: un utente locale senza privilegi speciali può ottenere i pieni poteri di **root**. E se il sistema attaccato è un container — Docker, Podman, o qualsiasi altra soluzione basata sui namespace del kernel — l'attaccante può anche **scappare dal container** e prendere il controllo dell'host che lo ospita. Non proprio una buona notizia per chi fa hosting condiviso o gestisce cluster Kubernetes.

Il punteggio di gravità assegnato è 8.5 su 10 (CVSS v4.0), quindi "alto" ma non il massimo assoluto — soprattutto perché per sfruttarla serve comunque un accesso locale al sistema, non è sfruttabile da remoto senza altre condizioni. Ma in un mondo fatto di server multi-utente, VPS condivisi e container che eseguono codice di terze parti, "serve accesso locale" è un requisito che si avvera più spesso di quanto vorremmo.

## Chi è coinvolto

I ricercatori hanno confermato lo sfruttamento con successo su una lista che fa un po' impressione: **Debian 13**, **Ubuntu 24.04**, **Rocky Linux 9** e **RHEL 9**, oltre a una build della famiglia OpenCloudOS e persino un kernel di ricerca mainline. In pratica, se hai una distribuzione Linux moderna con un kernel non aggiornatissimo, sei potenzialmente esposto.

La cosa interessante — e un po' inquietante — è che il bug non è stato introdotto da una modifica recente: era lì, dormiente, da quasi due decadi, probabilmente perché il codice SCTP è poco usato e quindi poco "stressato" dai fuzzer e dagli audit di sicurezza rispetto, ad esempio, al codice di rete TCP/IP.

## E non è la sola: c'è anche Zapscape

Nello stesso giro di patch di sicurezza del kernel di Debian 13, pubblicato il 6 agosto, è stata corretta anche **Zapscape** (CVE-2026-64561), un'altra use-after-free, questa volta nel codice MMU di **KVM**, il modulo che gestisce la virtualizzazione. Qui il rischio è simmetrico: un utente root dentro una macchina virtuale potrebbe risalire fino a ottenere privilegi root sull'host che la ospita, oppure un attaccante potrebbe creare al volo una VM usa-e-getta apposta per attaccare il kernel dell'host dall'interno. Se gestisci VPS o infrastrutture cloud basate su KVM/QEMU, è un altro promemoria da segnare in rosso.

In totale, l'aggiornamento kernel di Debian 13 di inizio agosto ha chiuso **28 falle diverse**, ma SCTPhantom e Zapscape sono quelle che hanno fatto più rumore per potenziale d'impatto.

## Cosa fare adesso

La buona notizia è che le patch esistono già e sono state integrate rapidamente nei kernel stabili delle principali distribuzioni. Quindi il consiglio è semplice quanto noioso da ripetere: **aggiorna il kernel**. Su Debian e derivate basta un classico:

```
sudo apt update && sudo apt upgrade
```

seguito da un riavvio (i moduli del kernel non si "ricaricano a caldo" per questo tipo di fix). Su distribuzioni con kernel live-patching (come alcune configurazioni Ubuntu Pro) l'aggiornamento può avvenire anche senza reboot.

Se invece vuoi ridurre la superficie d'attacco a prescindere dalle patch, puoi verificare se il modulo SCTP è caricato con:

```
lsmod | grep sctp
```

e, se non ti serve (la stragrande maggioranza degli utenti desktop e di molti server non lo usa mai attivamente), bloccarne il caricamento aggiungendo una riga tipo `install sctp /bin/false` in un file sotto `/etc/modprobe.d/`. Non è un sostituto della patch, ma è un buon layer di difesa in più, soprattutto su sistemi che ospitano utenti o servizi non completamente fidati.

Morale della storia: il kernel Linux è uno dei progetti software più controllati al mondo, eppure bug del genere restano nascosti per quasi vent'anni. Un ottimo promemoria che "vecchio e stabile" non significa automaticamente "sicuro", e che gli aggiornamenti di sicurezza — per quanto noiosi — restano il modo più semplice per non finire tra le statistiche sbagliate.
