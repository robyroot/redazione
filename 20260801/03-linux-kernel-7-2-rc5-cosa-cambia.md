---
title: "Linux Kernel 7.2-rc5: rete a tutto gas e conto alla rovescia verso il 16 agosto"
rilevanza: "MEDIA"
fonte: "https://www.linuxcompatible.org/story/linux-kernel-72-rc5-released-massive-networking-patch-push-targets-stable-on-aug-16"
data_notizia: "2026-08-01"
tags: ["linux", "kernel", "opensource", "sviluppo"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: pezzo più leggero e "da appassionato", buono per il pubblico beginner/intermediate che segue lo sviluppo del kernel senza compilarlo ogni notte. Vale la pena spiegare cos'è una release candidate per chi non mastica il ciclo di sviluppo Linux, e magari chiudere con un invito a testare la rc su una VM per chi vuole dare una mano al progetto. Buon collegamento anche a un pezzo futuro su Fedora 45 quando uscirà, visto l'accenno alla deprecazione di AF_ALG.
---

Se segui lo sviluppo del kernel Linux anche solo per curiosità, la settimana scorsa Linus Torvalds ha rilasciato **Linux 7.2-rc5**, il quinto candidato alla release verso la prossima versione stabile del kernel. E per una volta il titolo non è "release tranquilla" — Torvalds stesso l'ha definita "piuttosto massiccia".

## Cos'è una "rc" e perché dovrebbe interessarti

Per chi non segue da vicino: il ciclo di sviluppo del kernel Linux funziona a release candidate progressive (rc1, rc2, rc3...) che si susseguono ogni settimana per circa sette-otto settimane dopo l'apertura della "merge window" (la finestra di due settimane in cui vengono accettate le nuove funzionalità). Man mano che si avanza nelle rc, il codice dovrebbe stabilizzarsi sempre di più, fino alla release stabile finale. La 7.2-rc5 è arrivata il 26 luglio 2026, e la versione stabile 7.2 è attesa per il **16 agosto 2026** — meno di tre settimane da qui.

## Perché questa rc è "grossa"

La particolarità di questo giro è la quantità di modifiche relative alla **rete**: oltre un terzo di tutte le patch della rc5 riguarda i driver e il sottosistema networking. Il motivo è quasi buffo: molti sviluppatori che lavorano su questa parte del kernel hanno partecipato a una conferenza di settore la settimana precedente, e sono tornati con un bel po' di lavoro arretrato da sottomettere tutto insieme. È uno di quei casi in cui la vita reale degli sviluppatori (voli, conferenze, jet lag) si riflette direttamente nel ritmo delle commit.

Altra curiosità: in questa rc i patch per driver **USB** hanno superato numericamente quelli per le **GPU**, cosa non scontatissima di questi tempi in cui il grafico e il calcolo accelerato dominano spesso le notizie del kernel. Ci sono stati aggiornamenti importanti anche su TTY, storage a blocchi, Firewire, SMB e btrfs, oltre a un bel po' di lavoro sui test automatici — segno che l'infrastruttura di continuous integration del kernel continua a maturare. Curiosamente, gli strumenti di analisi automatica continuano a stanare piccole anomalie hardware specifiche nel sottosistema audio che spesso sfuggono ai revisori umani: un altro segnale di quanto il tooling automatizzato stia diventando parte integrante del processo di revisione del kernel.

## Cosa dice Torvalds

Nel suo consueto annuncio settimanale, Torvalds ha commentato che la dimensione della rc5 è "un po' troppo grande" per i suoi gusti, ma ha rassicurato che "nulla sembra particolarmente strano o spaventoso" nel codice. Non è una frase da prendere sotto gamba: quando Torvalds segnala nervosismo per una release, di solito lo fa esplicitamente — qui il messaggio di fondo resta che il kernel è considerato stabile, pur raccomandando ai tester di tenere d'occhio la prossima rc6 per eventuali sorprese dell'ultimo minuto.

## Cosa aspettarsi nella versione stabile

Tra le novità più interessanti che arriveranno con 7.2 finale ci sono miglioramenti prestazionali per le GPU **Intel Panther Lake Xe3 Arc B390** e ottimizzazioni per **PCIe 5.0** sulle piattaforme AMD EPYC Turin — buone notizie sia per chi ha un laptop recente con Intel di ultima generazione, sia per chi gestisce server con le CPU AMD più moderne. C'è poi un dettaglio che interesserà chi segue da vicino l'ecosistema delle distribuzioni: viene deprecata l'API userspace **AF_ALG crypto**, un passo di pulizia in preparazione dell'arrivo di **Fedora 45**, che si appoggerà a percorsi crittografici più moderni.

## E adesso?

Se sei il tipo di persona a cui piace testare software prima che diventi "ufficiale", una release candidate del kernel è terreno di gioco perfetto — soprattutto su una VM dedicata, mai su un sistema di produzione. Segnalare bug in questa fase è uno dei modi più concreti in cui anche chi non scrive codice C tutti i giorni può contribuire al progetto Linux: bug report ben fatti valgono quanto le patch. Per tutti gli altri, l'appuntamento resta quello del 16 agosto, quando la 7.2 dovrebbe passare ufficialmente da "candidata" a "stabile" e iniziare il suo cammino verso le distribuzioni.
