---
title: "GhostLock: la falla nel kernel Linux vecchia di 15 anni che regala root a chiunque"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/15-year-old-ghostlock-flaw-enables-root.html"
data_notizia: "2026-07-27"
tags: ["linux", "kernel", "sicurezza", "vulnerabilità", "root"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare in modo semplice cos'è una use-after-free e perché
  bug così vecchi restano nascosti per anni. Dare subito indicazioni pratiche
  (aggiornare il kernel, controllare la versione) perché il PoC pubblico rende
  il rischio concreto anche per utenti "normali" con server o VPS Linux.
---

Se gestisci anche solo un server Linux, un VPS o un container, questa è una di quelle notizie che vale la pena leggere fino in fondo. Si chiama **GhostLock**, ha un nome da CVE poco rassicurante — **CVE-2026-43499** — ed è una vulnerabilità che si nascondeva nel kernel Linux da **15 anni**, praticamente da quando è uscita la versione 2.6.39 del 2011. Tradotto: quasi ogni distribuzione mainstream rilasciata negli ultimi tre lustri ne è stata affetta, almeno fino alla patch arrivata ad aprile.

## Cos'è di preciso

Il problema vive nel sottosistema dei **futex** e degli **rtmutex**, cioè i meccanismi che il kernel usa per gestire i lock e la priorità dei processi quando più thread si contendono una risorsa. In particolare, c'è una funzione chiamata `remove_waiter()` che, in certe condizioni, ripulisce il puntatore sbagliato: invece di azzerare quello del processo che sta effettivamente aspettando, tocca quello del processo in esecuzione in quel momento. Il risultato è una classica **use-after-free**, cioè il kernel continua a usare un pezzo di memoria che in teoria ha già liberato — e questo è terreno fertilissimo per un attaccante che vuole prendere il controllo del sistema.

La parte inquietante è che per sfruttarla non serve nulla di esotico: bastano normalissime chiamate di threading fatte da un programma locale qualsiasi. Niente permessi speciali, niente configurazioni particolari, niente accesso di rete. Se hai un account utente non privilegiato su una macchina vulnerabile, in teoria puoi arrivare a root.

## Quanto è grave davvero

I ricercatori che l'hanno scovata hanno dimostrato un exploit affidabile **al 97%** nei test, capace non solo di ottenere root sulla macchina ma anche di **scappare da un container** — uno scenario da incubo per chi ospita servizi multi-tenant o ambienti cloud condivisi. Non a caso Google ha premiato la scoperta con **92.337 dollari** tramite il suo programma kernelCTF, che paga proprio per bug sfruttabili in scenari di container escape.

Il punteggio CVSS assegnato è 7.8 (High), ma nella pratica il rischio percepito da chi lavora in ambito hosting e sicurezza è più vicino a un "critico silenzioso": una falla che è rimasta invisibile per 15 anni e che ora, con l'exploit pubblicato, è alla portata di chiunque sappia compilare del codice C.

## Cosa fare adesso

La buona notizia è che la patch esiste già da mesi ed è stata distribuita a valle nelle varie distribuzioni (le principali distro enterprise come AlmaLinux, CloudLinux e derivate RHEL hanno già rilasciato i kernel corretti). Il problema è che, come sempre, moltissimi sistemi restano indietro con gli aggiornamenti — server dimenticati, VPS mai patchati, immagini container costruite mesi fa e mai ricostruite.

Quindi, checklist pratica se gestisci macchine Linux:

- **Controlla la versione del kernel** con `uname -r` e confrontala con le release patchate della tua distro.
- **Aggiorna appena possibile**, soprattutto su server esposti o multi-utente — non serve nemmeno accesso di rete per sfruttare il bug, quindi anche macchine "isolate" sono a rischio se qualcuno può eseguire codice locale (pensa a hosting condivisi, ambienti CI/CD, o sistemi con più utenti).
- **Se usi container**, verifica che l'host sottostante sia aggiornato: la patch del kernel host protegge tutti i container sopra, ma un kernel vecchio lascia la porta aperta a chiunque abbia una shell in un container.
- **Riavvia** dopo l'aggiornamento: per un bug nel kernel, il classico "hot patch senza reboot" spesso non basta a coprire tutti gli scenari.

GhostLock è un altro promemoria di quanto sia complesso il kernel Linux e di quanto tempo possa restare nascosto un bug in codice che milioni di macchine eseguono ogni giorno senza problemi apparenti. La lezione pratica, però, resta sempre la stessa: patch management noioso ma costante batte qualsiasi firewall.
