---
title: "GhostLock: la falla nel kernel Linux che dorme da 15 anni e regala root in 5 secondi"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/15-year-old-ghostlock-flaw-enables-root.html"
data_notizia: "2026-07-22"
tags: ["linux", "kernel", "sicurezza", "vulnerabilità", "root"]
livello: "intermediate"
nota_editoriale: |
  Taglio consigliato: pratico e "action oriented" per sysadmin e appassionati Linux — meno
  spiegone accademico sul futex, più "cosa controllo e aggiorno oggi stesso". Buon gancio
  anche per un box di approfondimento che rimanda all'articolo su VEGA (lo strumento AI
  che l'ha scoperta), pubblicato nello stesso giorno.
---

C'è una vulnerabilità che se ne sta buona buona nel kernel Linux dal 2011. Quindici anni: il tempo di due lauree, tre traslochi e probabilmente qualche PC che hai buttato via da un pezzo. Ora è saltata fuori con un nome da film hacker, GhostLock (CVE-2026-43499), e in pratica permette a **qualsiasi utente loggato su una macchina Linux di diventare root in circa 5 secondi**, con un'affidabilità del 97%.

Partiamo dal problema tecnico, spiegato senza troppi tecnicismi. Il kernel Linux usa un meccanismo chiamato futex (fast userspace mutex) per gestire i "lock" con cui i programmi si mettono d'accordo su chi accede a una risorsa condivisa. C'è una variante, PTHREAD_PRIO_INHERIT, pensata per evitare che un task a bassa priorità blocchi per sbaglio uno più urgente. Il problema sta nel codice di "cleanup" di questo meccanismo: in un caso raro, quando un'operazione di lock va in stallo e deve fare marcia indietro, la pulizia della memoria avviene al momento sbagliato e libera il record del task sbagliato. Il risultato è un puntatore che continua a fare riferimento a memoria già liberata — un classico use-after-free, solo che qui succede sullo stack del kernel invece che sull'heap, il che lo rende ancora più insidioso da individuare a occhio.

Un attaccante locale può sfruttare questa finestra per manipolare quella memoria e ottenere l'esecuzione di codice con privilegi root. E la parte "divertente" è che l'unico prerequisito è `CONFIG_FUTEX_PI=y`, opzione attiva di default praticamente ovunque: Ubuntu, Debian, Fedora, RHEL, Arch, praticamente tutte le distro mainstream con kernel dal 2.6.39 in poi. Funziona anche per l'escape dai container, quindi se gestisci server condivisi o pipeline CI/CD la cosa ti riguarda parecchio da vicino.

La scoperta arriva da Nebula Security, che l'ha trovata usando VEGA, un tool di bug-hunting basato su intelligenza artificiale (la storia merita un pezzo a parte, e infatti ne parliamo in un altro articolo di oggi). Il bug è stato segnalato il 18 aprile, corretto a monte nel giro di due giorni con il commit `3bfdc63936dd`, e distribuito via backport all'inizio di maggio — prima della divulgazione pubblica del 7 luglio. Tecnicamente quindi non è uno zero-day: le patch esistono da mesi. Il problema, come spesso succede, è che non tutti hanno aggiornato: a marzo alcune LTS di Ubuntu (24.04, 22.04, 20.04) risultavano ancora scoperte.

Cosa fare, in pratica? Aggiorna il kernel. Ma attenzione a un dettaglio non banale: non fermarti alla prima build patchata, perché ha introdotto a sua volta un altro bug (CVE-2026-53166) — punta quindi all'ultima versione disponibile per la tua distro, non alla prima che trovi in coda agli aggiornamenti. Se per qualche motivo non puoi aggiornare subito, esistono un paio di mitigazioni parziali (non risolutive) come `RANDOMIZE_KSTACK_OFFSET` e `STATIC_USERMODE_HELPER`, ma sono un cerotto, non una cura vera.

Se gestisci più macchine, la priorità di patching dovrebbe essere: prima i sistemi condivisi o multi-tenant, poi i server cloud, poi container e runner CI — cioè tutti gli ambienti dove utenti o processi diversi, non completamente fidati tra loro, condividono lo stesso kernel.

Un dettaglio che fa riflettere: il codice dell'exploit è già pubblico su GitHub (repository NebuSec/CyberMeowfia), quindi il tempo utile per patchare prima che qualcuno lo usi contro di te si sta assottigliando in fretta. Se il tuo server Linux ha utenti multipli o container non completamente fidati, questo weekend non è male per dare una controllata agli aggiornamenti kernel invece che al prato.

Per capire subito se sei esposto, il primo passo è banale: controlla la versione del kernel con `uname -r` e confrontala con quella corretta per la tua distro (su Debian/Ubuntu basta un `apt list --upgradable | grep linux-image`, su Fedora/RHEL `dnf check-update kernel`). Se il kernel installato è precedente alla patch di inizio maggio, sei ancora vulnerabile, punto. Ricordati poi che aggiornare il pacchetto non basta: dopo l'installazione del nuovo kernel serve un riavvio (o, se proprio non puoi permetterti downtime, un live patching tramite strumenti come kpatch o kernel livepatch, dove supportati) perché finché il sistema gira sulla vecchia immagine in memoria il bug resta lì, patch scaricata o no. Un errore comune, soprattutto su server che restano accesi per mesi senza reboot, è pensare che basti lanciare `apt upgrade` per essere al sicuro: il pacchetto sul disco cambia, ma il kernel effettivamente in esecuzione resta quello vecchio finché non riavvii.
