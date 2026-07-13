---
title: "Bad Epoll: la falla nel kernel Linux che trasforma un utente qualsiasi in root (e colpisce anche Android)"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/new-bad-epoll-linux-kernel-flaw-lets.html"
data_notizia: "2026-07-13"
tags: ["linux", "kernel", "sicurezza", "cve", "android", "privilege-escalation"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare cos'è epoll in termini semplici (il meccanismo che sta dietro
  a mezzo internet, dai browser ai server web) per far capire perché una falla "banale" in
  apparenza diventi così pericolosa. Buona occasione per un promemoria pratico su come
  controllare la propria versione del kernel e capire se serve patchare subito, con taglio
  rassicurante ma concreto (niente allarmismo, ma nemmeno sottovalutazione).
---

Se gestisci una macchina Linux, oppure hai semplicemente uno smartphone Android in tasca, c'è una vulnerabilità di cui vale la pena parlare: si chiama **Bad Epoll**, ha un nome ufficiale meno simpatico (CVE-2026-46242) e nel giro di poche settimane è passata da scoperta accademica a exploit funzionante al 99% delle volte. Non proprio dettagli da poco.

## Cos'è epoll e perché conta

Partiamo dalle basi. Epoll è un meccanismo del kernel Linux che permette a un programma di "tenere d'occhio" tantissimi file e connessioni di rete contemporaneamente senza sprecare risorse. È il cuore silenzioso che fa girare server web, browser, database, praticamente qualsiasi cosa debba gestire migliaia di connessioni simultanee in modo efficiente. In altre parole: se hai usato internet oggi, hai usato epoll, anche senza saperlo.

Il problema è che dentro epoll si nascondeva, dal 2023, un bug di tipo **use-after-free**: in certe condizioni, due parti del kernel possono provare a "ripulire" lo stesso oggetto di memoria nello stesso istante. Una lo libera, l'altra continua a scriverci sopra. Risultato: memoria corrotta che un attaccante può manipolare per scalare i propri privilegi fino a diventare root, l'utente con accesso totale al sistema.

## Un exploit quasi infallibile

La cosa che ha fatto rizzare le antenne agli esperti di sicurezza è la finestra di attacco: appena sei istruzioni macchina. Sembra un dettaglio da nulla, ma il ricercatore che ha scoperto la falla — Jaeyoung Chung, tramite il programma kernelCTF di Google — è riuscito a costruire un exploit capace di allargare artificialmente quella finestra e ritentare in sicurezza finché non va a segno. Il risultato è un tasso di successo attorno al 99% sui sistemi testati. Per capirci: non è un bug teorico da laboratorio, è un'arma quasi certa nelle mani giuste.

## Chi è a rischio

La lista è lunga: tutti i kernel Linux dalla versione 6.4 in poi, quindi la stragrande maggioranza delle distribuzioni desktop e server moderne (Ubuntu, Fedora, Debian nelle release recenti, e via dicendo), a meno che non abbiano già ricevuto la patch. Ma non finisce qui: **anche Android è coinvolto**, dato che il suo kernel deriva da Linux, con l'eccezione di alcune build più datate basate su kernel 6.1 (come alcuni Pixel 8). È stata dimostrata anche una via per bypassare la sandbox di Chrome, il che apre scenari interessanti (e preoccupanti) per chi pensa che il browser sia un ambiente isolato dal resto del sistema.

La buona notizia, se vogliamo chiamarla così: al momento non risultano attacchi reali osservati "in the wild". Il PoC tecnico è pubblico su GitHub, e una versione specifica per Android è ancora in sviluppo, ma il tempo a disposizione prima che qualcuno la finalizzi non è infinito.

## Cosa fare, concretamente

Non esiste un workaround praticabile: epoll è troppo centrale nel funzionamento del kernel per poterlo semplicemente disattivare. L'unica strada è aggiornare. La patch ufficiale è già stata integrata a monte (commit `a6dc643c6931`) ed è in fase di distribuzione tramite gli aggiornamenti delle principali distribuzioni.

Se usi un server Linux, il consiglio è controllare subito se il tuo gestore di pacchetti ha già rilasciato il kernel corretto e programmare l'aggiornamento — con riavvio, perché per il kernel non ci sono scorciatoie live-patch universali. Su desktop, tieni d'occhio gli update automatici della tua distro. Su Android, per ora l'unica leva è aspettare (e sollecitare) gli aggiornamenti di sicurezza del produttore, dato che qui il controllo dell'utente finale è molto più limitato.

Curiosità che fa riflettere: questa falla è imparentata con un'altra vulnerabilità epoll (CVE-2026-43074) scoperta in precedenza da un modello AI di Anthropic durante un'attività di auditing automatizzato del codice. Entrambe risalgono alla stessa modifica del 2023. Un promemoria utile: anche nel codice più maturo e controllato, un singolo commit può restare "dormiente" per anni prima che qualcuno — umano o AI — se ne accorga.
