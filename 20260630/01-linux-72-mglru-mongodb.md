---
title: "Linux 7.2 e MGLRU: MongoDB vola del 30-100% senza cambiare una riga di codice"
rilevanza: "ALTA"
fonte: "https://www.phoronix.com/news/Linux-7.2-MM"
data_notizia: "2026-06-24"
tags: ["linux", "kernel", "performance", "database", "mongodb", "mglru"]
livello: "intermediate"
nota_editoriale: |
  Angolo pratico per sysadmin e homelab: stessa macchina, stesso database, prestazioni doppie solo aggiornando il kernel.
  Spiega MGLRU in modo accessibile e dai istruzioni su come testarlo già ora con rc1.
---

Il kernel Linux 7.2 non è ancora stabile — RC1 è uscito il 28 giugno 2026 e la versione finale è attesa ad agosto — ma c'è già un motivo molto concreto per tenerlo d'occhio: un miglioramento al sottosistema di gestione della memoria chiamato MGLRU sta tirando fuori fino al 100% di throughput in più su MongoDB. Hai capito bene — stessa macchina, stesso database, stesso carico di lavoro: il doppio delle operazioni al secondo.

## Cos'è MGLRU?

MGLRU sta per Multi-Generation LRU (Least Recently Used). È il meccanismo che il kernel usa per decidere quali pagine di memoria tenere in RAM e quali spedire su disco quando la memoria comincia a scarseggiare. L'algoritmo "classico" del kernel Linux era vecchio di decenni e non teneva conto di come le applicazioni moderne accedono ai dati. Google ha sviluppato MGLRU internamente per i propri server e nel 2022 l'ha proposto per l'inclusione nel kernel mainline, dove è arrivato con Linux 6.1.

Però MGLRU non nasce perfetto, e il lavoro di raffinamento continua. Con Linux 7.2 arriva una serie di patch che migliorano il ciclo di reclaim (il processo di liberare pagine in RAM) e la gestione del dirty writeback — cioè le pagine modificate che devono essere scritte su disco prima di poter essere liberate.

## I numeri che contano

I benchmark pubblicati da Phoronix il 24 giugno 2026 parlano chiaro:

- **Su storage NVMe**: MongoDB registra un aumento del throughput di circa il **30%** con benchmark YCSB (Yahoo Cloud Serving Benchmark)
- **Su storage HDD o I/O lenti**: il miglioramento può arrivare fino al **100%**, ovvero MongoDB esegue il doppio di operazioni al secondo
- C'è anche una **riduzione del 50% nei file fault**, che significa meno interruzioni del kernel durante le operazioni di lettura

Perché su HDD il guadagno è così enorme? Perché con storage lento ogni decisione sbagliata di MGLRU si paga cara: se il kernel butta fuori dalla memoria pagine che MongoDB stava per rileggere, deve aspettare che arrivino dal disco. Su un HDD quell'attesa può costare millisecondi preziosi. L'algoritmo migliorato è molto più conservativo nel liberare pagine "calde" (usate di recente), riducendo drasticamente i page fault evitabili.

## Perché è importante per te

Se gestisci un server Linux con MongoDB — anche in un piccolo homelab, anche con hardware modesto — questo aggiornamento potrebbe cambiare le cose in modo tangibile. Un +30% su NVMe significa che il tuo database risponde più velocemente senza cambiare una riga di codice, senza upgradare l'hardware, senza toccare nulla. Solo aggiornando il kernel.

E non si tratta solo di MongoDB: MGLRU migliora in generale i workload misti read/write con grossi dataset che non stanno interamente in RAM — PostgreSQL, Redis con persistenza, Elasticsearch, script che lavorano su file grossi. Ovunque ci sia pressione sulla memoria, ci si aspettano benefici simili.

Pensa a questo caso pratico: hai un VPS da 4GB di RAM con MongoDB. Con il vecchio MGLRU, il kernel prende decisioni sbagliate su quali dati tenere caldi e il tuo database rallenta sotto carico. Con le nuove patch, lo stesso VPS gestisce il 30% di richieste in più prima di mostrare segni di stress. Non devi spendere nulla.

## Quando arriva a tutti?

Linux 7.2-rc1 è uscito il 28 giugno 2026, il che significa che siamo all'inizio del ciclo di test. La versione stabile è attesa tra il 16 e il 23 agosto 2026. Da lì, le distribuzioni principali (Fedora, Arch, Ubuntu non-LTS) lo integreranno nel giro di settimane. Per Debian Stable o Ubuntu LTS ci vorrà di più, ma nulla vieta di compilare il kernel manualmente o usare distribuzioni come CachyOS o Liquorix che seguono da vicino il mainline.

## Come testarlo adesso

Se hai voglia di sperimentare in un ambiente di test:

1. Scarica i sorgenti di Linux 7.2-rc1 da [kernel.org](https://kernel.org)
2. Compila con `make menuconfig` assicurandoti di avere `CONFIG_LRU_GEN=y`
3. Installa e riavvia
4. Confronta le performance con YCSB prima e dopo il kernel swap

Non è roba per la produzione — siamo in RC1 — ma per un ambiente di test è il momento giusto per capire quanto questo cambio impatterà il proprio stack.

Il bello del kernel Linux è esattamente questo: qualcuno a Google studia per anni come migliorare la gestione della memoria, poi quella conoscenza diventa pubblica e migliora il tuo homelab. Gratis. Senza chiedere nulla in cambio. Questo è l'open source che funziona.
