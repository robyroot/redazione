---
title: "Bad Epoll: la falla nel kernel Linux che regala accesso root (e riguarda anche Android)"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/new-bad-epoll-linux-kernel-flaw-lets.html"
data_notizia: "2026-07-12"
tags: ["linux", "kernel", "cybersecurity", "vulnerabilita", "android"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare in modo semplice cos'è una race condition/use-after-free
  senza tecnicismi eccessivi, sottolineare che riguarda anche Android (quindi utenti comuni,
  non solo sysadmin), e dare istruzioni pratiche di verifica/aggiornamento kernel.
  Interessante anche il dettaglio che un bug "gemello" era stato scovato da un'AI di Anthropic
  (Mythos) ma questo secondo bug le era sfuggito: buono spunto per un box "AI e sicurezza".
---

Se usi Linux, che sia sul tuo PC, su un server o su uno smartphone Android, c'è una notizia che merita la tua attenzione: è stata scoperta una falla nel kernel talmente efficace da avere un tasso di successo del 99% nell'exploit pubblico. Si chiama **Bad Epoll**, ha un nome ufficiale meno simpatico (**CVE-2026-46242**) e permette a un utente normale, senza alcun privilegio speciale, di prendere il pieno controllo del sistema come root.

## Cosa significa in pratica

Partiamo dal problema: normalmente, su un sistema Linux ben configurato, un utente "normale" può fare solo le cose per cui ha il permesso. Non può leggere i file di altri utenti, non può installare software di sistema, non può spegnere il computer altrui. Questo confine tra "utente qualsiasi" e "root" (l'amministratore che può fare tutto) è la base della sicurezza di Linux.

Bad Epoll sfonda proprio questo confine. Un attaccante che ha già un accesso minimo alla macchina — penso a un server condiviso, un servizio di hosting, un container, o anche solo un'app malevola su Android — può usare questa falla per scavalcare i controlli e diventare root. Da lì, il gioco è finito: può leggere tutto, installare qualsiasi cosa, nascondere le proprie tracce.

## Come funziona (in parole semplici)

Il nome "epoll" si riferisce a un meccanismo del kernel Linux usato da moltissimi programmi per gestire in modo efficiente tante connessioni di rete o file contemporaneamente (pensa a un server web che deve tenere d'occhio migliaia di connessioni insieme). È una parte del kernel molto sollecitata, sempre in movimento.

Il bug è quello che i tecnici chiamano una **race condition con use-after-free**: in pratica, due parti del kernel provano a "ripulire" lo stesso pezzo di memoria nello stesso istante. Una lo libera, l'altra sta ancora scrivendoci sopra. Il risultato è memoria corrotta che un attaccante esperto può manipolare per prendere il controllo di una struttura interna del kernel e, da lì, arrivare a root.

La finestra temporale in cui questo può succedere è minuscola — gli esperti parlano di appena sei istruzioni del processore. Eppure il proof-of-concept pubblicato dal ricercatore Jaeyoung Chung (tramite il programma kernelCTF di Google) raggiunge un'affidabilità del 99% su un kernel 6.12. Numeri che fanno capire quanto sia stato lavorato bene l'exploit.

## Chi è a rischio

La vulnerabilità è stata confermata su diverse distribuzioni con kernel recenti (dal 5.14 in poi, a seconda dei backport applicati dai vari vendor), e colpisce sia desktop che server Linux che dispositivi Android, dato che Android si basa proprio sul kernel Linux. Attenzione particolare va data ad ambienti di hosting condiviso, runner CI/CD e container, dove più utenti o processi non fidati condividono la stessa macchina fisica: lì il rischio di sfruttamento è più concreto.

## Una curiosità sull'IA

Un dettaglio interessante: qualche mese fa un sistema di intelligenza artificiale di Anthropic (Mythos) aveva individuato in autonomia una race condition collegata nello stesso pezzo di codice epoll, oggi catalogata come CVE-2026-43074. Ma quel bug era diverso da Bad Epoll, che è sfuggito all'analisi automatica ed è stato invece scovato da un ricercatore umano. Un promemoria utile in questi tempi di hype sull'"AI che trova tutte le vulnerabilità": è un ottimo strumento di supporto, ma non sostituisce ancora la caccia mirata di un esperto.

## Cosa fare

La buona notizia è che la falla è stata segnalata privatamente a febbraio 2026, corretta a monte il 24 aprile e resa pubblica solo il 30 maggio, quando la patch era già ampiamente disponibile. Se usi una distribuzione Linux mantenuta attivamente, il consiglio è semplice:

- **Aggiorna il kernel** il prima possibile e riavvia il sistema (una patch non attiva finché non riavvii);
- **Attiva gli aggiornamenti automatici di sicurezza**, se non l'hai già fatto;
- Se gestisci server condivisi o ambienti multi-utente, **dai priorità assoluta** a questo aggiornamento;
- Su Android, assicurati che il tuo dispositivo riceva ancora le patch di sicurezza mensili — se il produttore ha smesso di rilasciarle, è un altro buon motivo per valutare un cambio.

Non esiste una mitigazione "di configurazione": epoll è una parte troppo fondamentale del kernel per poterla semplicemente disabilitare. L'unica vera difesa è la patch.
