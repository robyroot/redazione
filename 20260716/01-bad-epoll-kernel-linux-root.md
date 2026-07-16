---
title: "Bad Epoll: la falla nel kernel Linux che regala root a chiunque (e colpisce anche Android)"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/new-bad-epoll-linux-kernel-flaw-lets.html"
data_notizia: "2026-07-16"
tags: ["linux", "kernel", "cybersecurity", "vulnerabilita", "android"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare in modo semplice cos'è una use-after-free e perché epoll è così centrale
  nel kernel (viene usato da praticamente ogni programma che gestisce rete o I/O asincrono).
  Consigliato taglio pratico: come verificare la propria versione del kernel e aggiornare su
  Ubuntu/Debian/Fedora/Arch. Buona occasione per parlare anche di Android, dato che tocca un pubblico
  più ampio dei soli sysadmin. Evitare toni allarmistici: nessuno sfruttamento in the wild al momento.
---

Se gestisci un server Linux, usi una workstation con questo sistema operativo o semplicemente hai in tasca un telefono Android, c'è una notizia che vale la pena conoscere: è stata scoperta una vulnerabilità nel kernel Linux, soprannominata **Bad Epoll**, che permette a un utente normale — senza alcun privilegio speciale — di diventare root. Sì, root come nell'amministratore assoluto, quello che può fare letteralmente tutto sulla macchina.

La falla, catalogata come **CVE-2026-46242**, è stata scoperta dal ricercatore Jaeyoung Chung e riguarda una componente del kernel chiamata **epoll**. Se non hai mai sentito questo nome, sappi che è uno dei meccanismi più usati in assoluto: permette a un programma di "tenere d'occhio" contemporaneamente tanti file, socket di rete e descrittori diversi senza dover controllare uno per uno se c'è qualcosa di nuovo. Server web, database, browser, sistemi di messaggistica: quasi tutto ciò che fa I/O in modo efficiente su Linux passa da epoll in un modo o nell'altro.

## Come funziona il bug, spiegato semplice

Tecnicamente si tratta di una **use-after-free**, una delle categorie di bug più temute nella programmazione a basso livello. In pratica: due parti del kernel provano a "ripulire" lo stesso oggetto in memoria nello stesso momento. Una lo libera, pensando che non serva più, mentre l'altra ci sta ancora scrivendo dentro. Il risultato è che quella memoria finisce in uno stato imprevedibile, e un attaccante astuto può sfruttare esattamente quel momento di confusione per prendere il controllo.

La particolarità di Bad Epoll è che la finestra temporale in cui il bug si manifesta è larghissima — appena una manciata di istruzioni macchina — quindi non dovrebbe essere facile da sfruttare per caso. Ma Chung ha costruito un exploit capace di "allargare" artificialmente quella finestra, ottenendo l'accesso root con un tasso di successo del 99% sui sistemi testati. Non proprio rassicurante.

## Chi è a rischio

La vulnerabilità colpisce i kernel Linux dalla versione **6.4 in poi**, quindi la stragrande maggioranza delle distribuzioni moderne: Ubuntu recenti, Fedora, Debian testing, Arch e derivate. Curiosamente i kernel della serie 6.1 (usati ad esempio da alcuni Pixel 8) risultano esclusi.

E qui arriva la parte che interessa anche chi non ha mai aperto un terminale in vita sua: **Android è colpito**. Dato che Android è costruito sopra il kernel Linux, molti smartphone recenti condividono lo stesso codice vulnerabile. Non significa che chiunque possa hackerare il tuo telefono da remoto — l'attacco richiede comunque di eseguire codice sul dispositivo — ma in scenari come app malevole scaricate da store non ufficiali, o computer condivisi in ufficio/università, il rischio è concreto.

Un dettaglio interessante: secondo i ricercatori, l'exploit riesce persino a essere innescato dentro la sandbox di Chrome, un ambiente pensato apposta per isolare il codice web da tutto il resto del sistema. Questo la dice lunga sulla serietà del bug.

## La buona notizia: è già stata corretta

Il difetto è stato segnalato responsabilmente al programma kernelCTF di Google, ed è già disponibile una patch upstream (commit `a6dc643c6931`). Al momento non risultano exploit attivi "in the wild", cioè usati concretamente contro utenti reali — ma il codice proof-of-concept è pubblico, quindi la finestra di tranquillità potrebbe essere breve.

## Cosa fare praticamente

Se usi Linux su server o desktop:

- **Aggiorna il kernel** appena la tua distribuzione rilascia il pacchetto corretto. Su Ubuntu/Debian basta un classico `sudo apt update && sudo apt upgrade`, su Fedora `sudo dnf upgrade`, su Arch `sudo pacman -Syu`.
- Se gestisci server condivisi, container o macchine multi-utente (ad esempio ambienti di hosting o CI/CD), dai priorità assoluta a questo aggiornamento: è proprio lì che una escalation locale a root fa più danni.
- Su Android, tieni d'occhio gli aggiornamenti di sicurezza del produttore del tuo telefono nei prossimi mesi.

Bad Epoll si aggiunge a una serie di vulnerabilità serie scoperte nel kernel Linux nelle ultime settimane, segno che la ricerca sulla sicurezza del kernel è più attiva che mai — nel bene (i bug vengono trovati) e nel male (ce ne sono ancora tanti, anche vecchi di anni, nascosti nel codice). La cosa migliore che puoi fare è la più noiosa di sempre: tenere i sistemi aggiornati.
