---
title: "OVSwrap: la falla nel kernel Linux vecchia di 13 anni che regala accesso root"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/08/new-ovswrap-linux-kernel-flaw-lets.html"
data_notizia: "2026-08-08"
tags: ["linux", "kernel", "cybersecurity", "vulnerabilità"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: taglio pratico da "come verifico se sono esposto e cosa faccio subito".
  Sottolineare che il modulo si carica anche se non lo si usa mai (il classico "tanto io OVS non lo uso"
  è un falso senso di sicurezza) e collegarla alla cultura del patching rapido su server Linux.
  Buona occasione per parlare di lsmod, moduli kernel on-demand e hardening di base.
---

Se gestisci anche solo un server Linux, questa è una di quelle notizie da leggere fino in fondo. È stata scoperta una vulnerabilità nel kernel Linux, battezzata **OVSwrap** e identificata come **CVE-2026-64531**, che permette a un utente locale senza privilegi di diventare root. Il bello (si fa per dire) è che il bug esiste da **tredici anni** ed è rimasto lì, silenzioso, dentro il codice che gestisce Open vSwitch (OVS), il sistema usato dal kernel per la gestione avanzata di switch virtuali e reti software-defined.

## Cosa c'è che non va

Il problema è tecnicamente un **integer wraparound**, cioè un errore di overflow, nella gestione degli "action stream" Netlink generati internamente da Open vSwitch. In parole povere: quando il kernel costruisce un'azione annidata troppo grande, un campo di lunghezza a 16 bit "gira" (wraparound) e il parser continua a leggere oltre il limite corretto, finendo dentro byte che l'attaccante può controllare. Questi byte vengono poi interpretati come azioni OVS legittime, aprendo la strada a corruzione di memoria nel kernel.

Il ricercatore che l'ha scoperta, Asim Viladi Oglu Manizada, ha mostrato che da qui si può arrivare a leggere puntatori del kernel, leggere memoria kernel a piacere e infine ottenere una scrittura mirata. Il proof of concept pubblico incatena questi passaggi fino a scrivere una voce in `/etc/sudoers` e aprire una shell root. Tutto questo con un normale account utente, senza bisogno di configurare Open vSwitch, senza un bridge OVS attivo, senza permessi speciali tipo `CAP_NET_ADMIN` e senza essere dentro un container privilegiato.

## Il dettaglio che frega di più

Qui arriva la parte più fastidiosa per chi amministra macchine Linux: **il modulo Open vSwitch si carica automaticamente on-demand**, anche se non l'hai mai configurato e non lo usi. Quindi lanciare `lsmod | grep openvswitch` e trovarlo vuoto non significa affatto essere al sicuro — il modulo è comunque presente sul disco insieme al kernel e un utente locale può innescarne il caricamento quando serve per l'exploit. È il classico caso in cui "tanto io questa roba non la uso" si rivela un ragionamento pericoloso.

## Chi è a rischio

La lista delle distribuzioni coinvolte è lunga e comprende praticamente tutto il mainstream: **Debian 12 e successivi, le derivate RedHat (RHEL, Rocky, AlmaLinux) e Ubuntu dalla 22.04 in poi**. Il punteggio di gravità assegnato è 7.8, quindi da trattare come priorità alta, soprattutto su sistemi multiutente, server condivisi, ambienti hosting, VPS con più clienti sulla stessa macchina o infrastrutture cloud dove più processi/utenti girano sullo stesso host.

La scoperta è stata gestita con responsible disclosure: il ricercatore ha coordinato la segnalazione con il team di sicurezza del kernel Linux e con i maintainer di Open vSwitch prima della pubblicazione, avvenuta a fine luglio 2026.

## Cosa fare adesso

Il consiglio più semplice resta il più efficace: **aggiorna il kernel** appena la tua distribuzione rilascia la patch, se non l'ha già fatto. Controlla i bollettini di sicurezza ufficiali della tua distro (Debian Security Advisories, RHSA per RedHat, USN per Ubuntu) e applica gli aggiornamenti kernel non appena disponibili, senza rimandare al prossimo ciclo di manutenzione pianificato — vista la facilità di sfruttamento, non è un rischio da lasciare in coda.

Se per qualche motivo non puoi patchare subito (magari un kernel custom, un'appliance, un sistema legacy), una mitigazione temporanea è bloccare esplicitamente il caricamento del modulo `openvswitch`, ad esempio aggiungendolo a una blacklist in `/etc/modprobe.d/`, così da impedirne il caricamento automatico finché non applichi la patch definitiva. Non è una soluzione, è un cerotto — ma meglio di niente su sistemi critici che non puoi riavviare subito.

Un'ultima nota generale: episodi come OVSwrap ricordano perché conviene tenere sotto controllo anche i moduli kernel "che tanto non uso mai". Un audit periodico dei moduli caricabili automaticamente su server esposti o multiutente non è paranoia, è manutenzione di base.
