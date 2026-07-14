---
title: "LongCat-2.0: il colosso cinese Meituan regala un modello AI da 1.600 miliardi di parametri, addestrato senza chip Nvidia"
rilevanza: "ALTA"
fonte: "https://venturebeat.com/technology/meituan-open-sources-longcat-2-0-the-1-6t-near-frontier-agentic-coding-model-thats-been-leading-openrouter-trained-entirely-on-chinese-chips"
data_notizia: "2026-07-14"
tags: ["ai", "open source", "modelli linguistici", "cina", "licenza mit"]
livello: "beginner"
nota_editoriale: |
  Angolo per RobyRoot: il pezzo tecnico (quanti parametri, quale MoE) è il meno
  interessante per un lettore da blog generalista. Il vero gancio è geopolitico e
  filosofico: la Cina sta usando le licenze permissive (MIT) come arma commerciale
  e di soft power, mentre i big lab occidentali (OpenAI, Anthropic, Google) restano
  chiusi. Vale la pena collegarlo al pattern GLM-5.2/DeepSeek/Kimi già trattato in
  passato, e mettere in guardia sui benchmark auto-dichiarati non verificati in modo
  indipendente — è un'informazione importante da non far passare in secondo piano.
---

C'è un dettaglio che rende questa notizia diversa dal solito annuncio "nuovo modello AI più bravo del precedente": non è stato realizzato da Meta, Google o una delle solite startup della Silicon Valley, ma da **Meituan**, il colosso cinese delle consegne a domicilio e dei servizi locali che probabilmente conosci meno di Alibaba o Baidu. E soprattutto: lo hanno reso completamente gratuito e riutilizzabile da chiunque, anche per scopi commerciali.

Si chiama **LongCat-2.0**, ed è uno dei modelli linguistici open più grandi mai rilasciati pubblicamente.

## Cosa c'è sotto il cofano

LongCat-2.0 è un modello "Mixture of Experts" (MoE), un'architettura ormai diventata standard tra i modelli di punta: invece di attivare tutto il modello per ogni richiesta, il sistema "sveglia" solo una parte specializzata dei suoi neuroni artificiali a seconda del compito. Nel caso di LongCat-2.0 parliamo di **1.600 miliardi di parametri totali**, di cui in media 48 miliardi attivi per ogni singola risposta generata. Sono numeri da modello di frontiera, nella stessa lega di GPT o Claude in termini di scala grezza (anche se la scala da sola non basta a determinare quanto un modello sia davvero bravo).

Il modello supporta anche un contesto fino a **1 milione di token**, il che significa — in parole povere — che può "leggere" e ragionare su documenti o codebase enormi in un colpo solo, invece di dover spezzettare tutto in piccoli pezzi.

## Perché la licenza conta più dei benchmark

La parte più interessante non è la potenza di calcolo, ma la scelta di rilasciare tutto sotto **licenza MIT**, una delle licenze open source più permissive che esistano: chiunque può scaricare i pesi del modello, modificarlo, integrarlo in un prodotto commerciale, rivenderlo come servizio, senza dover pagare royalty né condividere il codice sorgente della propria applicazione.

Meituan segue così un copione già visto quest'anno con altri laboratori cinesi — pensa a GLM-5.2 di Zhipu AI o ai modelli della famiglia DeepSeek — che stanno rilasciando modelli "frontier" (cioè allo stato dell'arte, o quasi) con licenze completamente aperte, mentre i grandi player occidentali come OpenAI, Anthropic e Google continuano a tenere i propri modelli migliori chiusi dietro un'API a pagamento. Non è filantropia: è una strategia precisa per costruire un ecosistema AI alternativo, dove sviluppatori di tutto il mondo si abituano a costruire sopra strumenti cinesi invece che americani. Più modelli gratuiti e competitivi ci sono in giro, meno potere contrattuale hanno i big lab chiusi.

## L'aspetto più curioso: niente chip Nvidia

Il dettaglio più chiacchierato dell'annuncio è che LongCat-2.0 sarebbe stato addestrato interamente su circa **50.000 processori AI di produzione cinese** (si parla di chip Huawei, Moore Threads e MetaX), senza una singola GPU Nvidia o AMD nella filiera. Se confermato, è un segnale potente: significa che gli export control americani sui chip più avanzati, pensati proprio per rallentare i progressi dell'AI cinese, stanno spingendo l'ecosistema locale a diventare autosufficiente più in fretta del previsto — l'esatto opposto dell'effetto desiderato.

Va detto con onestà, però, che questa specifica affermazione sull'hardware è al momento la meno verificabile della storia: le fonti disponibili la definiscono debolmente supportata da prove indipendenti, ed è ragionevole trattarla come "dichiarazione dell'azienda" più che come fatto accertato.

## I benchmark vanno presi con le pinze

Meituan sostiene che LongCat-2.0 superi Claude Opus in alcuni test specifici, come la capacità di seguire istruzioni complesse (IFEval) e in problemi di matematica olimpica (IMO-AnswerBench). Sono affermazioni interne dell'azienda, non ancora verificate da enti terzi indipendenti come Epoch AI o LMSYS Chatbot Arena, che nel settore AI fanno da arbitri neutrali sulle prestazioni reali dei modelli. Curiosamente, LongCat-2.0 girava già da settimane sotto lo pseudonimo "Owl Alpha" su OpenRouter (una piattaforma che aggrega l'accesso a decine di modelli diversi), scalando le classifiche di utilizzo prima ancora che si sapesse chi ci fosse dietro.

## Perché interessa anche a te

Se ti occupi di sviluppo o semplicemente segui il mondo AI open source, LongCat-2.0 è un altro tassello di un fenomeno che ormai è impossibile ignorare: i modelli gratuiti e scaricabili stanno diventando sorprendentemente competitivi con quelli chiusi a pagamento, e sempre più spesso arrivano dalla Cina. Prima di integrarlo in qualcosa di serio conviene aspettare valutazioni indipendenti, ma il trend di fondo — più opzioni open, meno dipendenza da un singolo fornitore chiuso — è una buona notizia per chiunque creda in un'AI più accessibile.
