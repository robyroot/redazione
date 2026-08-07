---
title: "Qwen3.8-Max: Alibaba promette 'open source', ma i pesi del modello non si trovano da nessuna parte"
rilevanza: "MEDIA"
fonte: "https://thecherrycreeknews.com/qwen38max-open-source-weights-hugging-face-missing-analysis-cherry_creek/"
data_notizia: "2026-08-07"
tags: ["ai open source", "qwen", "alibaba", "llm", "open weight", "huggingface"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: usare questo caso per fare educazione sul termine "open source" applicato ai
  modelli AI, spesso usato in modo elastico dal marketing. Utile spiegare la differenza tra
  "open weight" (pesi scaricabili, ma training set/codice non necessariamente pubblici) e vero
  open source, e perché la community (Hugging Face, r/LocalLLaMA) tiene sotto controllo queste
  promesse. Buon gancio anche per parlare di Qwen3/Qwen3.5, già disponibili in Apache 2.0, come
  alternative concrete già utilizzabili oggi.
---

Nel mondo dell'AI open source c'è un rituale che si ripete spesso: un big tech annuncia in pompa magna un nuovo modello "aperto", i titoli dei giornali parlano di svolta epocale, e poi la community si mette pazientemente ad aspettare che i file promessi compaiano davvero su Hugging Face. Questa volta il protagonista è **Alibaba**, con il suo **Qwen3.8-Max**, e l'attesa si sta allungando più del previsto.

## Cosa è stato annunciato

Il team Qwen ha presentato Qwen3.8-Max come un modello mixture-of-experts da **2,4 trilioni di parametri** (di cui circa 95 miliardi attivati per ogni inferenza), con una finestra di contesto fino a **1 milione di token** — abbastanza da digerire l'equivalente di 750.000 parole in un colpo solo. Alibaba lo ha presentato come competitivo con i modelli di punta di OpenAI e Anthropic, sottolineando in particolare le capacità di coding autonomo: il modello avrebbe portato a termine un progetto software durato 16 giorni senza intervento umano, producendo tra l'altro un framework rilasciato pubblicamente chiamato `oh-my-cli`.

La parte che ha fatto drizzare le orecchie alla community open source, però, è un'altra: Alibaba ha dichiarato che Qwen3.8-Max sarebbe stato il **primo modello di classe "Max"** della famiglia Qwen a essere rilasciato come open-weight, segnando un ritorno alla filosofia aperta dopo che alcuni modelli di punta più recenti erano rimasti proprietari. La promessa iniziale parlava dei pesi disponibili "la settimana successiva" all'annuncio.

## Il problema: i pesi non ci sono

Ad oggi, **6 agosto 2026**, su Hugging Face non risulta pubblicata alcuna pagina modello per Qwen3.8-Max, né per la variante più piccola Qwen3.8-27B annunciata in parallelo. Nessun file di pesi, nessuna licenza pubblicata, nessuna data ferma oltre al vago "prossima settimana" ripetuto più volte. Quello che gli utenti possono provare oggi è solo la versione "preview" ospitata sui servizi cloud di Alibaba — quindi, di fatto, un servizio proprietario mascherato da anteprima di un rilascio open.

È una distinzione che conta parecchio, e che nel mondo AI viene spesso appiattita nella comunicazione: una cosa è un modello che gira su server dell'azienda che lo ha creato e a cui accedete solo tramite API o interfaccia web, un'altra è un modello di cui potete scaricare i pesi ed eseguire in locale, magari sul vostro server con una GPU dedicata, senza dipendere dalla disponibilità (o dalla policy sulla privacy) di un servizio terzo.

## Perché la licenza conta quanto i pesi

Anche quando i pesi arriveranno, resta aperta la questione della licenza. Le precedenti generazioni, Qwen3 e Qwen3.5, sono state rilasciate sotto **Apache 2.0**, una delle licenze permissive più amichevoli che esistano per uso commerciale e derivati. Se Alibaba confermerà la stessa scelta per Qwen3.8-Max, sarà una buona notizia concreta per chi vuole costruire prodotti sopra il modello senza vincoli. Ma finché la licenza non è pubblicata nero su bianco, è presto per festeggiare: nella storia recente dei modelli linguistici non sono mancati casi di licenze "open" solo di nome, con clausole che vietano usi commerciali specifici o impongono limiti di scala.

## Cosa fare nel frattempo

Se avete bisogno oggi di un modello open-weight davvero scaricabile e paragonabile per fascia, le alternative concrete non mancano: **Qwen3.5** (già Apache 2.0), **Kimi K3** di Moonshot (rilasciato open-weight pochi giorni prima dell'annuncio di Qwen3.8), o le famiglie Llama e Mistral più recenti. Tenete d'occhio la pagina Hugging Face di Alibaba e i thread su r/LocalLLaMA: di solito, quando i pesi di un modello di questa portata vengono davvero pubblicati, la notizia si diffonde nel giro di poche ore.

La morale, per chi segue l'AI open source, resta sempre la stessa: fidatevi dei pesi scaricabili e delle licenze pubblicate, non dei comunicati stampa. "Open source" nel 2026 è ancora, troppo spesso, una parola che si può usare con parecchia elasticità.
