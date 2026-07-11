---
title: "Bad Epoll: il bug nel kernel Linux che trasformava un utente qualsiasi in root"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/new-bad-epoll-linux-kernel-flaw-lets.html"
data_notizia: "2026-07-11"
tags: ["linux", "kernel", "sicurezza", "cve", "android"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare in modo pratico come verificare la propria versione del kernel (uname -r) e perché conviene tenere aggiornate le distro, anche se il bug è già corretto da mesi. Buon gancio anche per parlare di kernelCTF di Google e di come la ricerca sulla sicurezza kernel sia diventata quasi uno sport. Interessante il parallelo con l'AI: un modello di Anthropic aveva trovato un bug diverso nella stessa porzione di codice ma non questo, spunto per un pezzo di approfondimento separato su AI vs ricercatori umani nel security auditing.
---

Se usi Linux, hai un telefono Android o gestisci server, c'è una notizia di sicurezza delle ultime settimane che vale la pena conoscere, anche se il pericolo peggiore è già alle spalle. Si chiama **Bad Epoll**, ha un nome che sembra uscito da un film di serie B, ma il problema che descrive è tutt'altro che scherzoso: una falla nel kernel Linux che permetteva a un utente normale, senza alcun privilegio speciale, di diventare root sulla macchina. Root, cioè il controllo totale.

## Cos'è epoll e perché è ovunque

Per capire la portata del problema bisogna sapere cos'è epoll. È un meccanismo del kernel Linux che permette a un programma di "tenere d'occhio" contemporaneamente tantissimi file o connessioni di rete senza dover controllare uno per uno se è successo qualcosa. È il cuore pulsante di server web, servizi di rete, database e persino dei browser. In pratica, quasi ogni software che deve gestire tante connessioni insieme (pensa a Nginx, Redis, o al tuo browser con venti schede aperte) si appoggia a epoll. Ed è per questo che un bug in quel punto del kernel fa così tanto rumore: non è un componente esotico usato da pochi, è infrastruttura di base.

## Il bug, spiegato senza troppo gergo

Tecnicamente, Bad Epoll (identificato come CVE-2026-46242) è una **race condition di tipo use-after-free** nel percorso di pulizia (`ep_remove()`) della gestione di epoll. In parole povere: quando un file viene chiuso, esiste una finestra di tempo brevissima in cui due parti del kernel possono "litigare" su chi ha ancora accesso a un certo pezzo di memoria. Se un attaccante riesce a inserirsi esattamente in quella finestra — che è larga quanto l'esecuzione di circa sei istruzioni, quindi minuscola — può far sì che il kernel continui a usare memoria che nel frattempo è stata liberata e riassegnata ad altro. Da lì, con la tecnica giusta, si arriva all'esecuzione di codice con i privilegi più alti del sistema.

La parte inquietante è che, nonostante la finestra minuscola, il ricercatore che ha trovato il bug (Jaeyoung Chung, tramite il programma kernelCTF di Google) ha costruito un exploit capace di allargare artificialmente quella finestra e ripetere il tentativo in loop finché non va a segno, raggiungendo una affidabilità del 99%. Numeri da manuale di scuola per gli exploit, quasi.

## Chi è affetto, e la buona notizia

Le versioni di kernel coinvolte vanno dalla 5.10 alla 6.11, un intervallo enorme che comprende praticamente ogni distribuzione Linux moderna in circolazione negli ultimi anni, dai server aziendali ai desktop, fino ad Android — che è basato sullo stesso kernel Linux e condivide lo stesso codice epoll. Quindi sì, in teoria anche uno smartphone Android non aggiornato potrebbe essere vulnerabile.

Ora la parte buona: il bug non è affatto una sorpresa dell'ultimo minuto lasciata scoperta. Chung lo ha segnalato privatamente a febbraio, gli sviluppatori del kernel lo hanno corretto il 24 aprile, e solo il 30 maggio è stata resa pubblica la falla — con la patch già distribuita da settimane. Non risultano exploit "in the wild", cioè usati da criminali prima della divulgazione: tutto l'exploit pubblico circolato serve a scopi di ricerca e proof-of-concept, non è stato osservato in attacchi reali.

## Cosa fare, concretamente

Se il fix è nel kernel da aprile, la domanda vera è: la tua macchina ce l'ha già? Dipende dalla distribuzione e da quanto sei diligente con gli aggiornamenti. Un comando come `uname -r` ti dice quale kernel stai usando; confrontalo con le note di rilascio della tua distro (Ubuntu, Fedora, Debian e le altre hanno tutte già distribuito il backport della patch nei rispettivi canali di sicurezza). Su Android il discorso è più delicato perché dipende dal produttore del telefono e da quanto è generoso con gli aggiornamenti di sicurezza — un altro capitolo della solita storia della frammentazione Android.

La morale, come sempre con questo tipo di bug: epoll non si può disattivare (è troppo fondamentale), quindi l'unica difesa reale è tenere aggiornato il sistema. Non serve panico, perché il buco è chiuso da mesi, ma è un ottimo promemoria per controllare se le tue macchine — server compreso — stanno davvero installando gli aggiornamenti del kernel, e non solo quelli delle applicazioni.
