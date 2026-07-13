---
title: "Hy3: Tencent rilascia in open source un modello AI da 295 miliardi di parametri con licenza Apache 2.0"
rilevanza: "MEDIA"
fonte: "https://www.tencent.com/en-us/articles/2202386.html"
data_notizia: "2026-07-13"
tags: ["ai", "open-source", "llm", "tencent", "apache-2.0", "self-hosting"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: inquadrare Hy3 nel filone (già trattato su RobyRoot con GLM-5.2 e
  MiniMax M3) dei modelli cinesi open-weight ad alta efficienza, con focus pratico su chi
  può davvero permettersi di farlo girare in self-hosting e con che hardware. Utile anche
  un confronto rapido su licenza Apache 2.0 vs le licenze "quasi aperte" di altri big
  player, per chi segue RobyRoot proprio per il taglio open source/libertà del software.
---

Mentre l'attenzione mediatica resta concentrata sui soliti nomi — OpenAI, Anthropic, Google — c'è un filone parallelo che chi segue RobyRoot conosce già bene: quello dei modelli AI open-weight rilasciati da laboratori cinesi, spesso con licenze più permissive di quanto ci si aspetterebbe e prestazioni che si avvicinano ai modelli proprietari occidentali. L'ultimo arrivato si chiama **Hy3**, ed è opera di Tencent Hunyuan, la divisione AI del colosso cinese che possiede WeChat, QQ e una fetta enorme dell'industria dei videogiochi.

## Le specifiche tecniche, in parole semplici

Hy3 è un modello Mixture-of-Experts (MoE), un'architettura che ormai è diventata lo standard per i modelli di grandi dimensioni: invece di attivare tutti i "neuroni" del modello per ogni singola richiesta, ne attiva solo una parte specializzata. Nel caso di Hy3 parliamo di **295 miliardi di parametri totali, ma solo 21 miliardi attivi** per ogni elaborazione. È proprio questo il trucco che rende il modello sorprendentemente efficiente: secondo Tencent, Hy3 offre un'intelligenza paragonabile a modelli con 2-5 volte i suoi parametri attivi, il che si traduce in costi di calcolo (e quindi hardware necessario) molto più contenuti a parità di capacità.

A completare il quadro c'è una finestra di contesto fino a **256.000 token** — sufficiente per digerire un intero repository di codice di medie dimensioni o un libro corposo in un colpo solo — e miglioramenti dichiarati su ragionamento complesso, generazione di codice e capacità agentiche (cioè la capacità del modello di usare strumenti, pianificare compiti a più passaggi e agire in autonomia).

## La licenza è la vera notizia

Dal punto di vista di chi ha a cuore il software libero e l'indipendenza tecnologica, il dettaglio più interessante non è il benchmark, ma la licenza: **Apache 2.0**, una delle licenze open source più permissive che esistano. Significa che puoi scaricare i pesi del modello, modificarli, usarli commercialmente e redistribuirli senza le limitazioni "quasi aperte" che altri produttori (anche occidentali) tendono a inserire nelle proprie licenze "open" con clausole particolari sull'uso commerciale o sulla scala di adozione.

I pesi sono già disponibili su Hugging Face, ModelScope, GitCode e CNB, quindi accessibili a chiunque abbia l'hardware per farli girare — e qui va fatta una premessa onesta: 295 miliardi di parametri, anche con solo 21 miliardi attivi per volta, non sono alla portata di una macchina consumer media. Servono comunque GPU professionali o cluster multi-GPU per un self-hosting serio, anche se la variante quantizzata FP8 rilasciata insieme al modello base riduce parecchio i requisiti rispetto alla precisione piena.

## A cosa serve davvero

Tencent non nasconde l'ambizione pratica del progetto: Hy3 è già integrato in prodotti reali usati da centinaia di milioni di persone, da WorkBuddy (produttività da ufficio) a Yuanbao (l'assistente AI di Tencent), passando per applicazioni di customer care su WeChat e persino assistenza in-game per titoli come Path of Exile. Non è quindi un esperimento da laboratorio, ma un modello già sotto stress test su scala enorme prima ancora di arrivare alla community open source.

## Perché conta per chi segue RobyRoot

Il pattern è ormai chiaro e lo abbiamo già raccontato parlando di GLM-5.2 e MiniMax M3: i laboratori cinesi stanno usando il rilascio open-weight come leva competitiva contro i modelli chiusi occidentali, offrendo alternative scaricabili, ispezionabili e auto-ospitabili a chi non vuole (o non può, per motivi di budget, privacy o sovranità dei dati) dipendere da un'API a pagamento gestita da un'azienda straniera. Per chi fa self-hosting per principio — che si tratti di un'istanza Ollama in homelab o di un cluster aziendale — Hy3 si aggiunge a una lista di alternative open-weight che cresce mese dopo mese, rendendo sempre più concreta l'idea che l'intelligenza artificiale di frontiera non debba per forza essere una scatola nera controllata da pochi.
