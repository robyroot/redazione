---
title: "Linux 7.2 è arrivato: ecco tutte le novità del nuovo kernel"
rilevanza: "ALTA"
fonte: "https://www.phoronix.com/news/Linux-7.2-rc7-Released"
data_notizia: "2026-08-16"
tags: ["linux", "kernel", "opensource", "ubuntu"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: taglio "cosa cambia per me che uso Linux ogni giorno".
  Puntare sulla battuta AMD Zen 6 + Ubuntu 26.10 per agganciare i lettori
  che aggiorneranno la distro in autunno. Evitare tecnicismi eccessivi su
  btrfs e HWMON, spiegarli con un paio di righe semplici. Buon gancio anche
  per un secondo pezzo più tecnico in futuro sulla race condition di memoria
  vecchia 8 anni.
---

Puntuale come ogni domenica di metà agosto, oggi Linus Torvalds ha tagliato il traguardo della versione stabile di Linux 7.2. Il rilascio arriva dopo sette release candidate e qualche settimana di test intensi, e come da tradizione porta con sé un bel po' di novità sotto il cofano, anche se — come vedremo — la vera notizia di questa release non è tanto una singola funzionalità quanto il modo in cui è stata sviluppata.

## Cosa cambia davvero

Partiamo dalle cose concrete. Linux 7.2 introduce uno scheduling più consapevole della cache della CPU, il che significa in pratica che il kernel diventa più bravo a decidere su quale core far girare un processo tenendo conto di dove si trovano già i dati che quel processo userà. Il risultato, sulla carta, è meno "cache miss" e quindi prestazioni migliori soprattutto sui sistemi multi-core più affollati — server, workstation con tanti thread, ma anche i normali laptop moderni con CPU a decine di core.

Arriva anche il supporto per i processori AMD Zen 6, la nuova generazione di chip Ryzen ed EPYC che inizierà a comparire sul mercato nei prossimi mesi. Chi ha già messo gli occhi su una macchina con questi processori troverà pane pronto quando aggiornerà il kernel.

Sul fronte filesystem, btrfs si è ripreso l'infrastruttura dei "fixup worker", un meccanismo che serve a evitare perdite silenziose di dati in determinate condizioni di scrittura concorrente — roba tecnica, ma buona notizia per chi usa btrfs come filesystem principale (sempre più persone, con Fedora e openSUSE che lo hanno come default). C'è stato anche un bel giro di correzioni al sottosistema HWMON, quello che si occupa di leggere temperature, velocità delle ventole e tensioni: se avete mai usato `sensors` da terminale per controllare quanto scalda la vostra CPU, è merito (anche) di questo sottosistema.

Non manca infine una patch di sicurezza per la vulnerabilità "Safe RET Interrupt", e — dettaglio che fa sempre un certo effetto — è stata sistemata una race condition nella gestione della memoria che si nascondeva nel codice del kernel da otto anni, causando in rari casi un uso della memoria dopo che era già stata liberata (un classico "use-after-free", il tipo di bug più amato dagli exploit developer).

## La vera notizia: l'AI è ormai parte del flusso di lavoro

Quello che rende interessante questa release candidate non è tanto la lista delle funzionalità, quanto un commento dello stesso Torvalds durante il ciclo di sviluppo. Di fronte al volume insolitamente alto di patch arrivate nelle ultime settimane, ha osservato che "it's just that there's a lot here. Most of it is fairly small" — cioè, ce ne sono tantissime, ma quasi tutte piccole. Il motivo? Sempre più sviluppatori usano strumenti di intelligenza artificiale per scovare bug minori, refactoring e piccole correzioni, generando un flusso costante di patch di dimensioni ridotte ma continue.

Torvalds l'ha definita ormai la "nuova normalità" per lo sviluppo del kernel: non uno strumento eccezionale usato ogni tanto, ma parte stabile del ciclo di lavoro quotidiano dei manutentori. È un cambiamento silenzioso ma significativo per un progetto che storicamente ha sempre avuto un rapporto piuttosto burocratico e umano con ogni singola riga di codice che entra nel repository.

## Quando lo trovate sulla vostra distro

Se usate una distribuzione rolling release come Arch o openSUSE Tumbleweed, il nuovo kernel arriverà nel giro di pochi giorni. Per chi usa Fedora o le distro con rilascio più tradizionale, i tempi si allungano un po', ma la notizia più rilevante per il pubblico italiano è probabilmente un'altra: Linux 7.2 diventerà il kernel di base di Ubuntu 26.10, la release che arriverà a ottobre. Chi pianifica di aggiornare la propria macchina Ubuntu in autunno lo farà già con questo kernel sotto il cofano, comprese tutte le novità (e le patch di sicurezza) di cui abbiamo parlato oggi.

Come sempre, il consiglio è di non avere fretta: aspettate qualche settimana che il kernel si stabilizzi ulteriormente prima di installarlo su macchine di produzione, ma se siete tipi da compilare il kernel in autonomia o da testare le ultime novità, i sorgenti di Linux 7.2 sono già disponibili su kernel.org.
