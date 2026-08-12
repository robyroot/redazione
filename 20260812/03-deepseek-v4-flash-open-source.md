---
title: "DeepSeek-V4-Flash è ufficialmente open source (licenza MIT): un altro colosso cinese sul tavolo"
rilevanza: "ALTA"
fonte: "https://www.opensourceforu.com/2026/08/deepseek-open-sources-v4-flash/"
data_notizia: "2026-08-12"
tags: ["ai", "open-source", "deepseek", "llm", "self-hosting"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: pubblico RobyRoot interessato a girare modelli AI open source in locale/self-hosted,
  quindi vale la pena essere onesti sui requisiti hardware reali (284B parametri non girano su un laptop,
  serve GPU server-grade o servizi cloud) e spiegare bene la differenza tra "pesi disponibili" e
  "effettivamente eseguibile a casa". Buon gancio anche per un confronto di costo con i modelli proprietari
  occidentali, dato l'interesse crescente per l'indipendenza da OpenAI/Anthropic/Google sul lato self-hosting.
  Taglio: entusiasta ma con i piedi per terra su cosa serve davvero per usarlo.
---

Il 31 luglio 2026 DeepSeek ha rilasciato ufficialmente la versione di produzione di DeepSeek-V4-Flash, e la notizia più interessante per chi segue il mondo open source non è tanto il modello in sé, quanto la licenza scelta: MIT, la più permissiva che esista nell'ecosistema open source. Vuol dire che chiunque scarichi i pesi del modello può usarlo per qualunque scopo — anche commerciale — senza dover condividere modifiche né pagare royalty a nessuno.

## Cosa c'è sotto il cofano

DeepSeek-V4-Flash è un modello con architettura Mixture-of-Experts (MoE), un approccio che ormai è diventato lo standard per i modelli di grandi dimensioni davvero efficienti. In pratica, invece di attivare tutti i parametri del modello per ogni singola richiesta, il sistema seleziona solo un sottoinsieme di "esperti" specializzati pertinenti al compito da svolgere. Il risultato: il modello ha 284 miliardi di parametri totali, ma per ogni token elaborato ne vengono effettivamente attivati solo 13 miliardi. È il motivo per cui riesce a essere relativamente veloce ed economico da far girare rispetto alla sua mole complessiva.

Altra caratteristica degna di nota è la finestra di contesto: un milione di token, con supporto fino a 384.000 token di output massimo. Per farvi un'idea concreta, un milione di token corrisponde grosso modo a un'intera saga di libri lunga qualche migliaio di pagine, tutta digeribile in un colpo solo dal modello. Utilissimo per chi lavora su codebase enormi, documenti legali lunghissimi o analisi che richiedono di tenere a mente moltissimo contesto contemporaneamente.

Questa versione "ufficiale 0731" (la sigla si riferisce alla data di rilascio, 31 luglio) non cambia la struttura del modello rispetto alla precedente versione preview, ma ha rifatto da capo tutto il post-training: reinforcement learning, supervised fine-tuning e distillazione da modelli "insegnante" più grandi. Il risultato, secondo i benchmark diffusi da DeepSeek, è un salto di qualità significativo soprattutto sui compiti di ingegneria del software e su scenari agentici, cioè quelli in cui il modello deve pianificare ed eseguire più passaggi in autonomia, non solo rispondere a una domanda secca.

## Quanto costa (se non lo fate girare voi)

Chi non ha intenzione di ospitare il modello in proprio può usarlo tramite l'API ufficiale di DeepSeek, con un pricing che resta nella filosofia "aggressiva sui costi" che ha reso famosa l'azienda cinese fin dal lancio di V3 e R1: 0,14 dollari per milione di token in input e 0,28 dollari per milione in output. Per fare un paragone spannometrico, si tratta di una frazione — spesso un decimo o meno — di quanto costano i modelli di punta occidentali di fascia paragonabile.

## Il punto dolente: farlo girare in casa

Qui bisogna essere onesti, perché "open source" non significa automaticamente "lo faccio girare sul mio PC". Con 284 miliardi di parametri totali, anche sfruttando le ottimizzazioni MoE, parliamo di un modello che richiede hardware di livello server: più GPU professionali con decine di gigabyte di VRAM ciascuna, oppure setup a memoria unificata molto generosi. Non è il tipo di modello che scarichi e avvii su una scheda video da gaming, per quanto potente.

Detto questo, avere i pesi disponibili su Hugging Face con licenza MIT — dove tra l'altro il modello è schizzato in cima alle classifiche di popolarità nel giro di poche ore dal rilascio — apre comunque diverse strade concrete: chi ha accesso a infrastrutture cloud GPU può auto-ospitarlo con pieno controllo sui dati, senza passare per API di terze parti; i ricercatori possono studiarne e modificarne il comportamento; e provider più piccoli possono offrire il servizio in concorrenza con DeepSeek stessa, magari con garanzie di privacy diverse.

In un panorama AI ancora dominato da modelli chiusi e costosi, ogni rilascio open weight di questo calibro — soprattutto con licenza permissiva come MIT anziché le licenze più restrittive che si vedono altrove — è una buona notizia per chi crede in un'intelligenza artificiale meno concentrata nelle mani di pochi attori. Vale la pena tenerlo d'occhio, anche solo per vedere come reagirà il resto del settore.
