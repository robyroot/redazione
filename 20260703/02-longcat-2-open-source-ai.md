---
title: "LongCat-2.0: il modello AI da 1.6 trilioni di parametri open source (e addestrato senza chip Nvidia)"
rilevanza: "ALTA"
fonte: "https://venturebeat.com/technology/meituan-open-sources-longcat-2-0-the-1-6t-near-frontier-agentic-coding-model-thats-been-leading-openrouter-trained-entirely-on-chinese-chips"
data_notizia: "2026-06-30"
tags: ["AI", "open-source", "LLM", "coding", "Meituan", "LongCat", "MIT-license"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: la doppia storia — un modello AI enorme rilasciato con licenza MIT
  (quindi davvero libero) e il fatto che sia stato addestrato su chip cinesi senza Nvidia.
  Perfetto per chi segue sia l'AI open source che le dinamiche geopolitiche del settore.
  Evidenziare come può essere eseguito in locale con le giuste risorse.
---

# LongCat-2.0: il modello AI da 1.6 trilioni di parametri open source (e addestrato senza chip Nvidia)

C'è una notizia che ha fatto alzare qualche sopracciglio nell'ultimo giorno di giugno: Meituan — la grande tech company cinese nota soprattutto per il food delivery — ha rilasciato LongCat-2.0 sotto licenza MIT. Un modello da 1.6 trilioni di parametri, pensato per il coding agentivo, con un contesto di 1 milione di token. E non è stato addestrato con chip Nvidia.

## Chi è LongCat-2.0 e da dove viene

LongCat-2.0 aveva già una storia curiosa prima dell'annuncio ufficiale. Per settimane aveva girato su OpenRouter con il nome anonimo **"Owl Alpha"**, posizionandosi spesso in cima alle classifiche di utilizzo senza che nessuno sapesse chi ci fosse dietro. Il 30 giugno Meituan ha tolto la maschera.

L'architettura è **Mixture of Experts (MoE)**: 1.6T parametri totali, ma solo 33-56 miliardi attivi per token (mediamente ~48B). Questo approccio — lo stesso usato da modelli come Mixtral o DeepSeek — permette di avere capacità da modello enorme senza pagare il costo computazionale pieno a ogni inferenza.

Il pretraining copre **30+ trilioni di token** tra cinese, inglese, multilingue e codice. Il contesto nativo è di 1 milione di token — abbastanza per passarci dentro interi repository.

## Le performance: dove si posiziona

Sui benchmark di coding:

- **SWE-Bench Pro**: 59.5% — in linea con i migliori modelli closed-source
- **Terminal-Bench**: 70.8%

Per fare un confronto, lo stesso range è occupato da modelli come MiniMax M3, Kimi K2.6 e GLM-5.2. L'open source di fascia alta per il coding ha ormai una panchina profonda.

## La parte più interessante: zero chip Nvidia

LongCat-2.0 è stato addestrato interamente su un cluster da **50.000 chip domestici cinesi** — hardware sviluppato in risposta alle restrizioni USA sull'export di GPU Nvidia verso la Cina. È la prima volta che un modello di questa scala completa training e inferenza su infrastruttura completamente non-Nvidia.

Il significato è tecnico e geopolitico insieme: dimostra che le restrizioni all'export non hanno fermato lo sviluppo di AI di frontiera in Cina, anche se probabilmente hanno reso tutto più difficile e costoso.

## Licenza MIT: cosa significa davvero

La licenza MIT è una delle più permissive che esistano. In pratica:

- Puoi usare LongCat-2.0 in produzione commerciale
- Puoi modificarlo e ridistribuirlo
- Puoi integrarlo nei tuoi prodotti senza dover aprire il codice sorgente
- L'unico obbligo è mantenere il copyright notice

È un livello di libertà che molti modelli "open" non offrono — Meta per esempio usa la sua licenza Llama che ha restrizioni commerciali per chi supera certi livelli di utilizzo.

## Posso eseguirlo in locale?

Con 1.6T parametri totali, LongCat-2.0 in forma intera non è roba da macchina consumer. Ma:

1. **Quantizzazione**: versioni quantizzate (GGUF, AWQ) stanno già arrivando su Hugging Face, che riducono drasticamente la RAM necessaria
2. **Versioni distillate**: tipicamente dopo questi rilasci arrivano modelli distillati più piccoli (7B, 14B) con performance simili su task specifici

Se vuoi tenerti aggiornato, cerca su Hugging Face:

```bash
# Con huggingface-cli installato
pip install huggingface_hub
huggingface-cli search "LongCat-2" --type model
```

Per chi ha hardware serio (più A100 o equivalenti), il modello completo è disponibile su [longcatai.org](https://www.longcatai.org/).

## Perché interessa anche a chi non fa AI professionale

LongCat-2.0 è interessante non solo per i benchmark, ma per quello che rappresenta: **l'open source AI di coding ha raggiunto la parità funzionale con i closed-source**. Un anno fa c'era un gap significativo tra ChatGPT/Claude e i modelli open per compiti di programmazione complessa. Quel gap si è chiuso — e la licenza MIT significa che chiunque può costruirci sopra.

La prossima volta che senti parlare di un'app di coding AI, c'è una probabilità non trascurabile che sotto ci sia qualcosa come LongCat-2.0.
