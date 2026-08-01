---
title: "LongCat-2.0: la Cina open-sourca un modello AI da 1,6 trilioni di parametri senza Nvidia"
rilevanza: "ALTA"
fonte: "https://venturebeat.com/technology/meituan-open-sources-longcat-2-0-the-1-6t-near-frontier-agentic-coding-model-thats-been-leading-openrouter-trained-entirely-on-chinese-chips"
data_notizia: "2026-06-30"
tags: ["AI", "open-source", "LLM", "Cina", "coding", "MIT"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: doppio interesse — AI open source accessibile (licenza MIT) e geopolitica tech (addestrato su chip cinesi senza Nvidia). Buono per spiegare cosa significa MoE e perché 1,6T parametri non equivale a "devi un datacenter". Utile per il pubblico curioso di AI locale/open.
---

# LongCat-2.0: la Cina open-sourca un modello AI da 1,6 trilioni di parametri senza Nvidia

Il 30 giugno 2026, Meituan — la grande azienda tech cinese più nota come "il Deliveroo cinese" — ha rilasciato in open source **LongCat-2.0**, un modello AI da 1,6 trilioni di parametri con licenza MIT. Zero restrizioni, pesi disponibili su Hugging Face, codice incluso.

Due cose rendono questa notizia particolarmente interessante: la prima è la licenza MIT, la più permissiva che esiste per un modello di questa taglia. La seconda è che l'intero addestramento è stato completato su oltre 50.000 chip AI cinesi — Huawei, Moore Threads, MetaX — senza un solo GPU Nvidia. Una risposta diretta alle restrizioni all'export imposte dagli USA.

## 1,6 trilioni di parametri: ma quanti me ne servono davvero?

Il numero impressiona, ma va contestualizzato. LongCat-2.0 usa un'architettura **MoE (Mixture of Experts)**: il modello ha tantissimi parametri in totale, ma per ogni token elabora ne attiva solo circa 48 miliardi. In pratica funziona come un team di specialisti — invece di chiedere a tutti di ragionare su ogni parola, delega al sottoinsieme più adatto.

Questo significa che le risorse computazionali effettive per l'inferenza sono molto inferiori rispetto a un modello "denso" da 1,6T. Non è qualcosa che gira sul tuo laptop, ma con hardware adeguato (o tramite API) è accessibile.

## Una finestra di contesto da 1 milione di token

Una delle caratteristiche più notevoli di LongCat-2.0 è il supporto nativo a **1 milione di token di contesto**. Per capire la scala: GPT-4 Turbo arrivava a 128k token, Claude 3 Opus a 200k. Un milione di token significa che puoi dargli un intero codebase medio, decine di documenti, o conversazioni lunghissime senza che il modello perda il filo.

Questa capacità viene gestita attraverso una tecnica chiamata **LongCat Sparse Attention (LSA)**, un meccanismo di attenzione sparsa che riduce la complessità computazionale sull'asse del contesto.

## Addestrato su chip cinesi: l'elefante nella stanza

Più di 35 trilioni di token di dati di addestramento, milioni di ore acceleratore, zero Nvidia. Il training pipeline completo è stato eseguito su chip Huawei Ascend, Moore Threads e MetaX.

Questo è il segnale più politicamente significativo della release: la Cina sta dimostrando di poter costruire e addestrare modelli di frontiera senza accesso all'hardware americano. Le restrizioni all'export di chip Nvidia verso la Cina — in vigore e progressivamente inasprite dal 2022 — miravano proprio a rallentare questo tipo di sviluppo.

LongCat-2.0 non è la prova definitiva che il gap è stato colmato (i chip cinesi restano indietro per efficienza energetica), ma è una dimostrazione pratica e pubblica che uno stack AI end-to-end domestico esiste e funziona.

## Come stanno le performance?

Prima della release pubblica, LongCat-2.0 era già in cima alle classifiche di **OpenRouter** per task di coding — una piattaforma dove migliaia di sviluppatori usano e confrontano modelli in produzione, quindi non benchmark sintetici ma traffico reale.

Sui benchmark di coding a lungo orizzonte, compete con i migliori modelli closed source disponibili. Non è il miglior modello assoluto in ogni categoria, ma per coding e task agentici è tra i top.

## Cosa puoi farci in pratica?

Se vuoi esplorare LongCat-2.0:

1. **Hugging Face** — I pesi sono disponibili su `meituan-longcat/LongCat-2.0` con licenza MIT, quindi scaricabili e utilizzabili liberamente, anche per usi commerciali.

2. **API** — Se non hai hardware sufficiente, puoi accedervi tramite i principali provider di API per LLM che l'hanno già integrato.

3. **Ollama** (quando disponibile) — La comunità sta lavorando a versioni quantizzate che potrebbero girare su hardware consumer per le varianti più piccole.

## Perché conta per noi

La release di LongCat-2.0 è un segnale del momento che stiamo vivendo: modelli AI di frontiera sempre più disponibili in open source, con licenze permissive, da lab che non si chiamano OpenAI o Google. L'ecosistema open source AI si sta consolidando e diversificando, e noi che preferiamo il software libero ne siamo i principali beneficiari.

Con licenza MIT, LongCat-2.0 può essere modificato, ridistribuito, integrato in prodotti commerciali. È esattamente il tipo di modello che la comunità open source stava aspettando a queste dimensioni.
