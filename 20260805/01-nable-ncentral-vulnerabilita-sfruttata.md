---
title: "N-able N-central sotto attacco: un bug di autenticazione regala agli hacker l'accesso da amministratore"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/08/n-able-says-attackers-take-over-n.html"
data_notizia: "2026-08-05"
tags: ["cybersecurity", "vulnerabilità", "RMM", "patch", "aziende"]
livello: "intermediate"
nota_editoriale: |
  N-central è una piattaforma RMM (Remote Monitoring and Management) usata soprattutto da MSP che gestiscono l'IT di tante piccole aziende: un solo bug qui significa potenzialmente centinaia di reti compromesse a cascata. Buon angolo per RobyRoot: spiegare cos'è un RMM ai lettori meno tecnici, insistere sulla "supply chain risk" (se il tuo consulente IT usa un tool vulnerabile, il rischio è tuo anche se non lo sai), e dare istruzioni pratiche per chi gestisce N-central in Italia. Tono da allarme concreto ma non terroristico: c'è una hotfix, va applicata subito.
---

Se lavori nell'IT o gestisci la sicurezza di un'azienda, probabilmente conosci N-central: è una delle piattaforme RMM (Remote Monitoring and Management) più usate al mondo dagli MSP, i fornitori di servizi IT gestiti che tengono d'occhio server, PC e reti di centinaia di clienti contemporaneamente. Ed è proprio per questo che la notizia di inizio agosto ha fatto drizzare le antenne a mezzo settore della cybersecurity: N-central ha una falla di autenticazione che permette a un attaccante, senza alcuna credenziale valida, di ottenere accesso amministrativo completo alla console. In pratica, le chiavi di casa di chiunque usi quella piattaforma.

**Cosa è successo, in breve**

Tutto parte da CVE-2026-18556, un bug di authentication bypass reso pubblico i primi giorni di agosto. N-able, l'azienda che sviluppa N-central, ha rilasciato una prima patch pensata per chiuderlo. Peccato che la patch non abbia funzionato del tutto: pochi giorni dopo è saltato fuori un secondo problema, CVE-2026-18577, che descrive esattamente questo scenario, un bypass di autenticazione "secondario" dovuto a una correzione incompleta della prima falla. Risultato: gli aggressori hanno continuato a entrare anche dopo l'aggiornamento iniziale.

La cosa più preoccupante è che non si tratta di teoria. Diverse aziende di sicurezza, tra cui Huntress, hanno confermato sfruttamento attivo in ambienti reali, con almeno un cliente compromesso attraverso questa catena di bug. La CISA americana (l'agenzia che coordina la difesa cyber degli Stati Uniti) ha aggiunto CVE-2026-18577 al suo catalogo delle vulnerabilità note come sfruttate, il famoso KEV Catalog, imponendo alle agenzie federali di sistemare la faccenda entro il 6 agosto.

**Perché dovrebbe interessarti anche se non usi N-central**

Qui sta il punto che rende questa storia più grande di un singolo prodotto: N-central non gestisce solo se stesso, gestisce le reti dei clienti degli MSP. Un attaccante che prende il controllo della console può usarla come trampolino di lancio verso decine o centinaia di endpoint a valle, spesso senza che il cliente finale abbia la minima idea di essere esposto. È lo stesso principio delle catene di fornitura software: se il tuo fornitore di servizi IT è compromesso, lo sei anche tu, anche se il tuo antivirus non ha mai lampeggiato rosso.

Per un piccolo studio, un negozio o una PMI italiana che affida la gestione dei propri computer a un consulente esterno, questo significa una cosa molto semplice: vale la pena chiedere direttamente al proprio fornitore IT se usa N-central e, in caso affermativo, se ha già applicato la correzione.

**Cosa fare adesso**

N-able ha rilasciato una hotfix il 2 agosto, la versione 2026.3.1.7, che a detta dell'azienda risolve definitivamente entrambe le falle, sia per le installazioni cloud che per quelle on-premise. Se gestisci un'istanza N-central, la prima cosa da fare è aggiornare subito a questa versione, senza aspettare la finestra di manutenzione successiva: con un bug già sfruttato attivamente, ogni giorno di ritardo è un giorno di esposizione reale.

Vale anche la pena controllare i log di accesso alla console per attività sospette nei giorni precedenti l'aggiornamento: se qualcuno è entrato prima che tu applicassi la patch, il semplice aggiornamento non basta a "disinnescare" un eventuale accesso già ottenuto, ad esempio tramite account creati ad hoc o modifiche alla configurazione.

**La lezione di sempre**

Non è la prima volta che vediamo uno schema del genere: bug critico, patch rapida, patch che si rivela incompleta, secondo giro di correzioni. Succede, i software sono complessi. Ma è un buon promemoria del perché "ho già aggiornato" non dovrebbe mai chiudere del tutto la questione quando si parla di strumenti che hanno accesso privilegiato a tante reti diverse: vale la pena tenere d'occhio gli advisory ufficiali del fornitore anche nei giorni successivi a un primo fix, perché a volte il secondo capitolo della storia è più importante del primo.
