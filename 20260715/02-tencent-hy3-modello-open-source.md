---
title: "Tencent apre i pesi di Hy3: un modello da 295 miliardi di parametri che se la gioca con i big"
rilevanza: "MEDIA"
fonte: "https://github.com/Tencent-Hunyuan/Hy3"
data_notizia: "2026-07-15"
tags: ["ai", "open-source", "llm", "hunyuan", "tencent"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: RobyRoot dovrebbe inquadrarlo nel filone "l'open source cinese sta chiudendo il gap
  con i modelli proprietari occidentali" insieme a LongCat-2.0 di Meituan (già coperto altrove in italiano,
  quindi qui va menzionato solo come contesto, non come notizia principale). Buon punto per parlare di
  licenza Apache 2.0 (permissiva, uso commerciale libero) contro le licenze più restrittive di altri
  modelli cinesi. Se possibile, accennare a come provarlo gratis (OpenRouter, Hugging Face) per chi
  vuole sperimentare senza GPU proprie.
---

Mentre le grandi aziende americane rilasciano modelli sempre più chiusi e a pagamento, dalla Cina arriva l'ennesimo promemoria che l'intelligenza artificiale open source è tutt'altro che morta. Tencent ha rilasciato **Hy3**, un modello linguistico da 295 miliardi di parametri, con pesi scaricabili liberamente e licenza Apache 2.0 — la stessa che usano progetti come Kubernetes, quindi via libera anche all'uso commerciale senza troppi grattacapi legali.

## Un modello "sparso" che risparmia risorse

Hy3 non è un modello monolitico, ma segue l'architettura **Mixture-of-Experts (MoE)** che è ormai lo standard per i modelli di grandi dimensioni. In pratica, immagina il modello come un team di 192 "esperti" specializzati: per ogni richiesta, solo 8 di questi esperti vengono attivati (il famoso "top-8"), per un totale di appena 21 miliardi di parametri effettivamente in funzione a ogni passaggio.

Questo è il trucco che rende gestibili modelli enormi: hai la capacità e la conoscenza di un modello da 295 miliardi di parametri, ma il costo computazionale reale per rispondere a una domanda è molto più vicino a quello di un modello 10 volte più piccolo. Il modello gestisce anche un contesto fino a 256.000 token, il che significa che puoi dargli in pasto interi repository di codice o documenti lunghissimi senza che "dimentichi" l'inizio della conversazione.

## Come se la cava contro la concorrenza

Tencent ha fatto valutare Hy3 con un blind test coinvolgendo 270 esperti umani, ottenendo un punteggio di 2,67 su 4, superando GLM-4-5.1 (fermo a 2,51). Il modello si distingue in particolare su compiti di sviluppo frontend e CI/CD — non a caso, Tencent lo presenta come un modello pensato soprattutto per programmazione, lavoro d'ufficio, modellazione finanziaria e design.

Non è il primo rilascio di questa famiglia: Hy3 era già uscito in anteprima ad aprile 2026, e questa versione definitiva incorpora il feedback raccolto da oltre 50 prodotti che lo hanno già integrato nel frattempo. Tra i miglioramenti più concreti: il tasso di "allucinazioni" (risposte inventate con sicurezza) è sceso dal 12,5% al 5,4%, e gli errori di buon senso sono quasi dimezzati (dal 25,4% al 12,7%). Anche le conversazioni lunghe e articolate ne beneficiano, con gli errori nei dialoghi multi-turno scesi dal 17,4% al 7,9%.

## Come provarlo

Se hai una GPU potente in casa (Tencent consiglia hardware di fascia H20-3e o superiore per servire il modello su 8 GPU), puoi scaricare i pesi da Hugging Face, ModelScope, GitCode o CNB, sia in versione standard che quantizzata FP8 per ridurre i requisiti di memoria. L'inferenza è supportata da vLLM e SGLang, con un'API compatibile OpenAI — quindi se hai già del codice scritto per ChatGPT, il porting è relativamente indolore.

Per chi invece non ha voglia (o modo) di procurarsi otto GPU professionali, il modello è disponibile anche tramite piattaforme come OpenRouter, spesso con periodi promozionali gratuiti per i nuovi rilasci — vale la pena controllare le condizioni aggiornate prima di lanciarsi in un progetto.

## Il quadro più ampio

Hy3 arriva a pochi giorni da un altro rilascio open source cinese di peso ben maggiore: **LongCat-2.0** di Meituan, un colosso da 1,6 trilioni di parametri addestrato interamente su chip cinesi, senza una sola GPU Nvidia coinvolta. Se aggiungiamo anche i modelli della famiglia DeepSeek e Qwen, il quadro che emerge è chiaro: le aziende tech cinesi stanno usando l'open source come leva strategica, sia per costruire un ecosistema di sviluppatori attorno ai propri modelli, sia per dimostrare indipendenza tecnologica dalle restrizioni all'export di hardware americano.

Per chi segue RobyRoot e ha a cuore un'intelligenza artificiale libera da vincoli proprietari, questi rilasci sono una boccata d'aria: più opzioni open weight significa meno dipendenza da un'unica azienda, più possibilità di eseguire modelli in locale per motivi di privacy, e prezzi al ribasso anche per chi usa le versioni "cloud" via API. La domanda legittima, come sempre con i modelli cinesi, riguarda i dati di addestramento e l'eventuale allineamento a certe policy di stato — ma sul piano puramente tecnico, la corsa all'AI open source non ha mai avuto così tanti protagonisti validi.
