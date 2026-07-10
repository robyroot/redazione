---
title: "LongCat-2.0: Meituan rilascia un mega-modello open source da 1,6 trilioni di parametri (senza usare chip Nvidia)"
rilevanza: "MEDIA"
fonte: "https://venturebeat.com/technology/meituan-open-sources-longcat-2-0-the-1-6t-near-frontier-agentic-coding-model-thats-been-leading-openrouter-trained-entirely-on-chinese-chips"
data_notizia: "2026-07-10"
tags: ["ai", "open-source", "llm", "intelligenza-artificiale", "cina"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: spiegare in modo accessibile cosa significa "addestrato su chip cinesi" e
  perché è una notizia geopolitica oltre che tecnica (indipendenza da Nvidia). Buon pezzo per
  lettori meno tecnici, evitare di scendere troppo nei dettagli di architettura MoE. Si può linkare
  a un futuro approfondimento su GLM-5.2 (altro modello cinese open source, già coperto altrove in
  italiano) per dare un quadro della scena AI open source cinese del 2026.
---

Se segui il mondo dell'intelligenza artificiale open source, ultimamente la Cina ne sta sfornando parecchia, e l'ultimo arrivato si chiama **LongCat-2.0**, rilasciato da **Meituan** - sì, proprio l'azienda cinese famosa soprattutto per il food delivery, che negli ultimi anni ha messo su un laboratorio AI niente male.

## I numeri, per farsi un'idea

LongCat-2.0 è un modello enorme: **1,6 trilioni di parametri totali**, anche se grazie a un'architettura **Mixture-of-Experts (MoE)** ne "attiva" solo circa **48 miliardi per ogni token** elaborato. In pratica, il modello ha una capacità teorica gigantesca, ma per rispondere a una singola domanda usa solo una piccola parte di quella capacità, il che lo rende molto più efficiente ed economico da far girare rispetto a un modello denso della stessa dimensione.

Altra caratteristica degna di nota: supporta nativamente una finestra di contesto fino a **1 milione di token**, grazie a un meccanismo chiamato **LongCat Sparse Attention (LSA)** e a un'architettura di embedding basata su n-grammi. Tradotto: può "leggere" e ragionare su quantità di testo enormi in un colpo solo, un'intera codebase o pile di documenti, senza perdere il filo.

## Il dettaglio che fa più notizia: niente Nvidia

La parte davvero interessante di questa storia, però, non è solo tecnica: LongCat-2.0 è stato **addestrato interamente su un cluster di 50.000 acceleratori AI "domestici"**, cioè chip cinesi, senza usare hardware Nvidia. Meituan lo rivendica come il primo caso nel settore di un modello da un trilione di parametri addestrato e messo in produzione end-to-end su una piattaforma non-Nvidia di questa scala.

Perché conta? Per via delle restrizioni USA all'export di chip AI avanzati verso la Cina, che negli ultimi anni hanno spinto le aziende cinesi a cercare alternative interne. Vedere un modello di questa portata nascere completamente fuori dall'ecosistema Nvidia è un segnale che quella strada, tecnicamente complicatissima, sta iniziando a dare risultati concreti. È tanto una notizia tecnologica quanto geopolitica: parla di autonomia infrastrutturale, non solo di benchmark.

## A cosa serve (e come si usa)

Meituan ha progettato LongCat-2.0 soprattutto come motore di ragionamento per **agenti AI e strumenti di coding**: comprensione di codice, modifiche su intere repository, esecuzione automatizzata di task complessi. Non a caso, il modello si è già piazzato ai vertici delle classifiche di utilizzo su **OpenRouter**, la piattaforma che aggrega l'accesso a decine di modelli diversi, segno che gli sviluppatori lo stanno effettivamente adottando e non è rimasto solo un annuncio.

La buona notizia per chi ama l'open source vero è che i pesi del modello sono rilasciati con **licenza MIT**, quindi utilizzabili commercialmente senza troppi vincoli. È disponibile su **Hugging Face** in diversi formati di precisione (BF16, FP8, INT8), con ottimizzazioni pensate anche per girare su architetture hardware diverse da quelle su cui è stato addestrato, oltre che tramite l'API ufficiale di LongCat e, come detto, su OpenRouter.

## Perché ti interessa (anche se non sei un data scientist)

Non serve essere sviluppatori AI per capire perché questa notizia conta: ogni nuovo modello open source di alto livello che arriva sul mercato è una alternativa in più a servizi chiusi come GPT o Claude, spesso a costi molto più bassi e con la possibilità di farlo girare su infrastrutture proprie, un tema caro a chi su RobyRoot ha a cuore anche la privacy e il controllo dei propri dati.

LongCat-2.0 si aggiunge a una lista già lunga di modelli cinesi open weight usciti nel 2026 - penso a GLM-5.2 di Z.ai o DeepSeek V4 Pro - che stanno rendendo la scena dell'AI open source sempre più competitiva e sempre meno dominata dai soliti nomi americani. Per chi vuole sperimentare con modelli potenti senza vendere l'anima a un abbonamento, è decisamente un momento interessante da seguire.
