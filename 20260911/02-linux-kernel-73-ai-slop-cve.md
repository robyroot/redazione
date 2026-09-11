---
title: "Il kernel Linux annega nelle patch scritte dall'AI: benvenuti nel ciclo 7.3"
rilevanza: "ALTA"
fonte: "https://www.phoronix.com/news/Linux-7.3-Rough-Cycle"
data_notizia: "2026-09-11"
tags: ["linux", "kernel", "intelligenza artificiale", "open source", "sicurezza"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: raccontarla come una storia di crescita "dolorosa" dell'open source nell'era AI,
  con Greg Kroah-Hartman e Jakub Kicinski come voci dirette dei maintainer sul campo. Buon gancio per
  aprire una discussione sui commenti: "l'AI nel dev del kernel è un aiuto o un problema?" Evitare toni
  allarmistici sul numero di CVE: spiegare bene che l'aumento è più che altro un effetto della caccia
  automatizzata ai bug, non un peggioramento reale della sicurezza del kernel.
---

Se segui anche solo distrattamente lo sviluppo del kernel Linux, avrai notato che ultimamente il nome che ricorre più spesso non è quello di una nuova feature entusiasmante, ma quello di un problema tutto nuovo: l'intelligenza artificiale che genera patch e bug report a ritmi che i maintainer umani fanno fatica a reggere. Il ciclo di sviluppo di Linux 7.3, appena entrato nella fase "release candidate", è già stato definito da Greg Kroah-Hartman — uno dei maintainer più esperti e rispettati del progetto — come destinato a essere "rough", turbolento.

**Cosa sta succedendo davvero**

Il problema ha due facce. La prima riguarda le patch: sempre più contributori (o presunti tali) inviano correzioni al codice del kernel generate, in tutto o in parte, con l'aiuto di strumenti AI. Jakub Kicinski, che si occupa della manutenzione del sottosistema di rete, ha fatto un calcolo che dà i brividi: su 648 patch ricevute per l'area "net-next" in questo ciclo, tra un terzo e la metà sembrano essere correzioni di basso valore, pulizie cosmetiche o chiarimenti generati con il supporto di un'AI. Non necessariamente sbagliate, ma spesso inutili, ridondanti, o riferite a porzioni di codice che nessuno tocca da anni — inclusi driver per hardware ormai obsoleto.

Kroah-Hartman, che oltre al suo ruolo principale si occupa anche dell'area "staging" del kernel (quella per i driver ancora sperimentali), ha reso pubblico un numero che dà la misura del problema: la sua coda filtrata di messaggi legati al solo sottosistema USB conteneva 1.732 messaggi da processare su un totale di 4.807. Dopo un primo giro di pulizia è riuscito a scendere a 1.094 su 4.170. Sono numeri da far girare la testa per una singola persona che deve valutare, una per una, se ogni patch è legittima, utile, o semplice rumore generato automaticamente.

La sua risposta, per l'area di cui è direttamente responsabile, è stata netta: niente più patch generate da AI/LLM, a meno che non si tratti di correzioni di sicurezza reali e verificabili. Una linea dura, ma che dà l'idea di quanto la situazione fosse diventata insostenibile.

**La seconda faccia: l'esplosione dei CVE**

C'è poi il fronte delle vulnerabilità. Il conteggio dei CVE (gli identificativi standard con cui viene catalogata ogni falla di sicurezza pubblica) associati a ogni release del kernel sta letteralmente esplodendo: si era stabilizzato per anni intorno ai 500 per release durante l'era Linux 6.x, poi ha superato i 1.000 con Linux 7.0, i 1.500 con Linux 7.2, e con Linux 7.3 potrebbe sfondare quota 2.000.

Prima di allarmarti: questo non significa che il kernel sia diventato improvvisamente meno sicuro. La causa principale è che sempre più "cacciatori di bug" stanno usando strumenti AI per scandagliare sistematicamente i circa 40 milioni di righe di codice del kernel, trovando problemi reali (e altri molto meno reali) a una velocità che nessun team di revisione umana aveva mai dovuto gestire prima. È in parte una buona notizia — si trovano più bug, anche vecchi di anni — e in parte un incubo logistico, perché ogni segnalazione va comunque verificata da qualcuno, e quel "qualcuno" sono sempre gli stessi maintainer già oberati di lavoro.

**Perché è importante, anche se non scrivi codice per il kernel**

Non serve essere sviluppatori kernel per capire perché questa storia conta. Il kernel Linux è alla base di miliardi di dispositivi: dai server che fanno girare metà di internet, agli smartphone Android, ai router di casa, ai sistemi embedded nelle auto. Un processo di revisione sovraccarico e potenzialmente meno accurato per colpa del rumore di fondo generato dall'AI è un rischio sistemico che riguarda, indirettamente, chiunque usi un dispositivo con dentro Linux — cioè, di fatto, quasi tutti.

C'è poi un tema più ampio di sostenibilità dell'open source nell'era dell'AI generativa: come si bilancia il valore reale che può portare (trovare bug che l'occhio umano si perde da anni) con il costo di dover filtrare una massa crescente di contributi di qualità incerta? Progetti come il kernel Linux, che si reggono sul lavoro volontario e sulla fiducia reciproca tra maintainer, stanno facendo da apripista — nel bene e nel male — a un problema che toccherà presto anche altri grandi progetti open source.

Per ora, la linea che sembra emergere è quella tracciata da Kroah-Hartman: benvenuto l'aiuto dell'AI per compiti specifici e verificabili come la sicurezza, meno benvenuto il flusso indiscriminato di patch "tanto per fare qualcosa". Vedremo se altri sottoprogetti seguiranno lo stesso approccio, e se basterà a rendere il prossimo ciclo un po' meno "rough" di questo.
