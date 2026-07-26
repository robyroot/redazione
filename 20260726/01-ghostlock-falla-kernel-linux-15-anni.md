---
title: "GhostLock: la falla nel kernel Linux vecchia di 15 anni che dà root in 5 secondi"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/15-year-old-ghostlock-flaw-enables-root.html"
data_notizia: "2026-07-26"
tags: ["linux", "kernel", "cybersecurity", "vulnerabilità"]
livello: "intermediate"
nota_editoriale: |
  Angolo pratico: guida rapida per verificare la versione del kernel e aggiornare su Ubuntu/Debian/Fedora.
  Sottolineare il rischio per chi ha home lab con Docker/Kubernetes, dato l'escape da container documentato.
  Buona occasione per ribadire la cultura del patching regolare tipica di Linux vs approccio black-box dei sistemi proprietari.
---

Se usi Linux — e se sei qui probabilmente lo fai — questa è una di quelle notizie che meritano attenzione anche se non sei un sysadmin di professione. Si chiama GhostLock, ha un nome che sembra uscito da un film di spionaggio, ed è una vulnerabilità che si nasconde nel kernel Linux dal lontano 2011. Quindici anni. Per farti un'idea, nel 2011 usavamo ancora Ubuntu 11.04 "Natty Narwhal" e Windows 7 era l'ultimo grido.

La falla, ufficialmente CVE-2026-43499, è stata scoperta dal team di ricerca VEGA di Nebula Security, che l'ha segnalata in modo responsabile il 18 aprile 2026. Il kernel l'ha corretta pochissimi giorni dopo (20 aprile) e la patch è arrivata nelle distribuzioni stabili all'inizio di maggio. Tutto bene, quindi? Non proprio: il 7 luglio Nebula ha reso pubblici i dettagli tecnici insieme a un exploit funzionante, e da lì la corsa alle patch è diventata più urgente, perché ora chiunque può scaricare il codice e provarlo.

## Cosa fa esattamente

GhostLock è un difetto use-after-free nel sottosistema dei futex, la componente del kernel che gestisce i lock a priorità ereditata (quelli dietro alle mutex PTHREAD_PRIO_INHERIT di glibc, per capirci). In parole povere: in un caso raro, quando un'operazione di lock fallisce e deve "tornare indietro", la pulizia della memoria scatta nel momento sbagliato e cancella il record del task sbagliato. Questo lascia un puntatore "fantasma" (da qui il nome) che il kernel continua a usare, aprendo la porta all'esecuzione di codice arbitrario con privilegi di root.

La parte che fa più impressione è la velocità: l'exploit pubblicato da Nebula Security porta un processo non privilegiato a diventare root in circa 5 secondi, con un tasso di successo del 97% nei loro test. E non si ferma alla macchina fisica: il bug permette anche l'escape da container Docker e Kubernetes, il che lo rende particolarmente pericoloso per chi gestisce infrastrutture cloud condivise o home lab con più container in esecuzione.

## Chi è a rischio

Praticamente tutti. Il codice vulnerabile è presente in ogni distribuzione mainstream — Ubuntu, Debian, Fedora, Arch, RHEL e derivate — che monta un kernel costruito a partire da Linux 2.6.39-rc1 (maggio 2011) fino a prima della v7.1-rc1. L'unico prerequisito è avere l'opzione CONFIG_FUTEX_PI=y, attiva di default praticamente ovunque. A inizio luglio, versioni LTS di Ubuntu come 24.04, 22.04 e persino la vecchia 20.04 risultavano ancora esposte in molte installazioni non aggiornate.

Va detto per onestà che non si tratta di un attacco remoto: serve un accesso locale preesistente (una shell, un container compromesso, un utente malintenzionato con un account limitato). Per questo il punteggio CVSS è "solo" 7.8 su 10, alto ma non critico. Il problema è che in tanti scenari reali — server condivisi, hosting multi-tenant, ambienti universitari, container as-a-service — un accesso locale non privilegiato è esattamente il punto di partenza più comune per un attacco.

## Cosa fare adesso

La buona notizia è che la patch esiste già da mesi (commit upstream 3bfdc63936dd) ed è stata distribuita dai principali vendor. Quindi:

1. Aggiorna il kernel della tua distribuzione il prima possibile e riavvia il sistema — un semplice `apt upgrade` o `dnf upgrade` seguito da reboot basta nella maggior parte dei casi.
2. Se gestisci server condivisi, VPS multi-utente o cluster Kubernetes, dai priorità assoluta a queste macchine: sono il bersaglio più goloso.
3. Controlla l'advisory della tua distribuzione specifica (Ubuntu, Debian, Red Hat pubblicano bollettini dedicati) per la versione di kernel corretta.
4. Mitigazioni come RANDOMIZE_KSTACK_OFFSET o STATIC_USERMODE_HELPER aiutano solo in parte: non sostituiscono la patch.

GhostLock è un promemoria utile di una verità scomoda: anche nel software open source più controllato al mondo, un bug può restare invisibile per 15 anni prima che qualcuno lo trovi. La differenza, rispetto al software proprietario, è che qui la correzione è arrivata in due giorni dalla segnalazione e chiunque può verificarla di persona. Aggiorna, e dormi sonni più tranquilli.
