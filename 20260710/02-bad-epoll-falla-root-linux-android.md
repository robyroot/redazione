---
title: "Bad Epoll: la falla zero-day che trasforma un utente qualsiasi in root su Linux (e Android)"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/new-bad-epoll-linux-kernel-flaw-lets.html"
data_notizia: "2026-07-10"
tags: ["linux", "android", "kernel", "sicurezza", "cve", "zero-day"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: agganciare alla notizia GhostLock (stessa settimana, due falle root diverse)
  per fare un pezzo "settimana nera per il kernel Linux" o comunque linkare i due articoli tra loro.
  Interessante anche il dettaglio umano: un ricercatore ha trovato manualmente ciò che un modello AI
  (Mythos) aveva mancato - buon spunto per parlare dei limiti attuali dell'AI nella security research.
  Specificare bene che riguarda anche Android, tema che interessa un pubblico più ampio del solo
  sysadmin.
---

Non è passata nemmeno una settimana dalla scoperta di GhostLock che il kernel Linux si becca un'altra falla critica: si chiama **Bad Epoll**, il suo nome ufficiale è **CVE-2026-46242**, ed è un'altra vulnerabilità che permette a un utente senza privilegi di diventare **root**. Stavolta però il raggio d'azione è ancora più ampio: colpisce anche **Android**.

## Cosa c'è che non va

Bad Epoll è, come GhostLock, un bug di tipo *use-after-free*: due thread del kernel provano a liberare lo stesso oggetto in memoria contemporaneamente, causando corruzione di memoria. Il nome viene dal fatto che il problema si trova nel codice legato a **epoll**, il meccanismo che Linux usa per gestire in modo efficiente migliaia di eventi I/O contemporaneamente (praticamente ogni server web, database e app di rete lo usa sotto il cofano).

La particolarità tecnica di questo bug è che sfruttarlo richiede una precisione chirurgica: la finestra temporale utile per il race condition è di appena **sei istruzioni CPU**. Per capirci, è un margine di manovra minuscolo, il che rende l'exploit tecnicamente sofisticato da scrivere ma non impossibile, tant'è che un proof-of-concept è già stato pubblicato.

## Chi è a rischio

La falla colpisce i kernel Linux dalla versione **6.4 in poi**, se non patchati. E qui sta il punto che allarga parecchio il bacino di utenza interessata: essendo un problema nel kernel Linux, e Android essendo basato su Linux, **anche gli smartphone Android sono vulnerabili**. Non stiamo parlando solo di server e desktop, ma potenzialmente di centinaia di milioni di dispositivi mobili.

## Una scoperta particolare

C'è un dettaglio che vale la pena raccontare, perché dice qualcosa sullo stato dell'arte della sicurezza informatica nel 2026: la falla è stata trovata dal ricercatore **Jaeyoung Chung**, ma solo dopo che un modello di intelligenza artificiale specializzato in security research, chiamato **Mythos**, aveva già analizzato la stessa porzione di codice, individuando un bug correlato ma **mancando proprio Bad Epoll**. È stato l'occhio umano, alla fine, ad accorgersi di quello che l'AI aveva lasciato scoperto.

È un promemoria utile in un momento in cui si parla tanto di AI capaci di trovare vulnerabilità automaticamente: sono strumenti potenti che accelerano il lavoro, ma non sono (ancora) un sostituto della competenza umana, soprattutto sui bug più sottili e legati a condizioni di temporizzazione precise come questo.

Chung ha comunque segnalato la falla come zero-day al programma **kernelCTF** di Google e ha pubblicato una write-up tecnica completa. La buona notizia è che, al momento, **non risultano exploit attivi in circolazione**: la vulnerabilità non compare nella lista KEV (Known Exploited Vulnerabilities) di CISA, quindi per ora resta una minaccia teorica ma seria, non uno sfruttamento in corso.

## Cosa fare

Anche qui la checklist è semplice:

1. **Aggiorna il kernel** del tuo sistema Linux non appena la patch è disponibile per la tua distribuzione.
2. Su **Android**, aspetta e installa gli aggiornamenti di sicurezza mensili non appena Google e i produttori li rilasciano: qui il controllo è meno nelle tue mani, ma è comunque importante non rimandare gli update del telefono.
3. Se gestisci server esposti o ambienti multi-utente, tratta questa falla con la stessa urgenza di GhostLock: due vulnerabilità root nella stessa settimana non sono un caso isolato, sono un segnale che vale la pena tenere d'occhio gli avvisi di sicurezza del kernel con più attenzione del solito.

Tra Bad Epoll e GhostLock, luglio 2026 si sta confermando un mese impegnativo per chi amministra sistemi Linux. Il consiglio, banale ma sempre valido, resta lo stesso: patchare presto, patchare spesso, e non fidarsi ciecamente nemmeno degli strumenti AI più sofisticati quando si parla di sicurezza.
