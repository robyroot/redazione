---
title: "Tails 7.10.1: aggiornamento d'emergenza, da installare subito se usi il sistema anonimo"
rilevanza: "ALTA"
fonte: "https://tails.net/news/version_7.10.1/"
data_notizia: "2026-08-16"
tags: ["privacy", "linux", "tor", "cybersecurity", "anonimato"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: taglio pratico e rassicurante, "cosa fare adesso"
  piuttosto che allarmismo. Spiegare bene chi è Tails per i lettori meno
  esperti (non solo addetti ai lavori, giornalisti, attivisti: anche
  chiunque voglia navigare senza lasciare tracce su un PC non suo). Buon
  gancio per un evergreen futuro "guida a Tails per principianti".
  Sottolineare che non ci sono evidenze di sfruttamento reale ma il rischio
  teorico è deanonimizzazione, quindi va preso sul serio comunque.
---

Se usate Tails — il sistema operativo live pensato per navigare in modo anonimo attraverso Tor senza lasciare tracce sul computer che state usando — questa è una di quelle notizie da non ignorare. Il 5 agosto 2026 il progetto ha rilasciato Tails 7.10.1, un aggiornamento d'emergenza arrivato appena due settimane dopo la versione 7.10, con lo scopo dichiarato di correggere due vulnerabilità che nel peggiore dei casi potrebbero portare alla deanonimizzazione di chi lo usa. Vale la pena capire di cosa si tratta e, soprattutto, cosa fare subito.

## Cos'è Tails, in due righe

Per chi non lo conoscesse: Tails (The Amnesic Incognito Live System) è una distribuzione Linux pensata per essere avviata da una chiavetta USB su qualsiasi computer, senza installazione e senza lasciare tracce sul disco fisso della macchina ospite. Instrada tutto il traffico di rete attraverso Tor e, allo spegnimento, cancella ogni dato dalla memoria. È lo strumento di riferimento per giornalisti, attivisti, avvocati e chiunque abbia bisogno di un livello di anonimato e protezione superiore alla media — ma negli ultimi anni è diventato anche una scelta sempre più comune per chi, semplicemente, tiene molto alla propria privacy digitale quotidiana.

Proprio perché la sua unica ragione d'essere è l'anonimato, ogni falla che rischia di comprometterlo viene trattata dal progetto con la massima urgenza. Ed è esattamente quello che è successo qui.

## Le due vulnerabilità corrette

La prima riguarda il kernel Linux, aggiornato alla versione 6.12.100 per correggere la falla identificata come CVE-2026-64560. Il problema, spiegano gli sviluppatori nel changelog ufficiale, è che "se un sito Web malevolo fosse sfruttato, potrebbe permettere al browser Tor in Tails di ottenere privilegi amministrativi" — in pratica, visitando una pagina appositamente costruita per sfruttare il bug, un attaccante avrebbe potuto in teoria ottenere il controllo completo del sistema, vanificando tutte le protezioni di anonimato che Tails è progettato per garantire.

La seconda vulnerabilità coinvolge invece la libreria Expat, usata per interpretare file XML da diverse applicazioni incluse in Tails come LibreOffice e Audacity. L'aggiornamento alla versione 2.8.2 di Expat risolve i problemi descritti nell'advisory Debian DSA-6404-1: in sostanza, aprire un file XML malevolo appositamente creato con una di queste applicazioni poteva, in determinate condizioni, concedere all'attaccante privilegi amministrativi sul sistema.

La buona notizia, sottolineata a chiare lettere dal team di Tails, è che al momento del rilascio non risultava alcuna evidenza che queste falle fossero già state sfruttate attivamente. Ma per un sistema il cui unico scopo è proteggere l'identità di chi lo usa, "nessuna evidenza di sfruttamento" non equivale a "nessun rischio" — ed è per questo che si è scelto di correre ai ripari con un rilascio fuori programma invece di aspettare il prossimo ciclo regolare di aggiornamenti.

## Le altre novità (minori) del rilascio

Oltre alle due correzioni di sicurezza, Tails 7.10.1 porta anche un paio di migliorie meno urgenti ma comunque gradite: una compressione migliorata dei file usati per gli aggiornamenti incrementali, che dovrebbe velocizzare il download degli update futuri, e una riduzione di circa 70 MB nelle dimensioni complessive del sistema, ottenuta eliminando firmware hardware non più necessari.

## Cosa fare adesso

Se avete già Tails 7.0 o una versione successiva installata su una chiavetta USB, la strada più semplice è lasciare che il sistema di aggiornamento automatico integrato faccia il suo lavoro: al prossimo avvio, Tails dovrebbe rilevare da solo la disponibilità della nuova versione e proporvi di installarla. Il processo è pensato per essere alla portata di chiunque, senza bisogno di terminale o comandi.

Per chi invece sta installando Tails da zero, le immagini USB e i file ISO aggiornati alla versione 7.10.1 sono già disponibili sul sito ufficiale del progetto, con le consuete istruzioni di installazione passo passo per Windows, macOS e Linux.

In generale, vale la regola d'oro di ogni sistema pensato per la sicurezza e l'anonimato: gli aggiornamenti non sono mai opzionali. Rimandare l'installazione di una patch come questa, anche solo per qualche giorno, significa lasciare aperta — per quanto teorica — una porta esattamente sul tipo di rischio che Tails esiste per chiudere.
