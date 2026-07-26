---
title: "Kimi K3: il modello AI open-weight più grande di sempre (e i pesi arrivano domani)"
rilevanza: "ALTA"
fonte: "https://www.datacamp.com/blog/kimi-k3"
data_notizia: "2026-07-26"
tags: ["ai", "open-source", "llm", "moonshot"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare bene la differenza tra open-weight e open source vero, evitando hype eccessivo.
  Utile un box comparativo con GLM-5.2 e DeepSeek V4 già trattati sul blog, per dare continuità alla serie
  sui modelli cinesi open. Menzionare il limite hardware come reality check per chi pensa di farlo girare in locale.
---

Il 16 luglio 2026 l'azienda cinese Moonshot AI ha presentato Kimi K3, e il mondo dell'intelligenza artificiale open source ha avuto la sua scossa dell'estate. Parliamo del modello open-weight più grande mai rilasciato: 2,8 trilioni di parametri totali, più del doppio del suo predecessore Kimi K2 (che si fermava "solo" a 1 trilione). E la parte più interessante per chi segue RobyRoot: domani, 27 luglio, Moonshot rilascerà i pesi completi, permettendo a chiunque abbia l'hardware giusto di scaricarli, ispezionarli e farli girare in casa propria.

## Cosa vuol dire "open-weight"

Prima di entrare nei dettagli tecnici, vale la pena chiarire un punto che spesso genera confusione. "Open-weight" non è esattamente come "open source" nel senso classico: Moonshot rilascia i pesi del modello (i numeri che ne codificano la "conoscenza"), ma non necessariamente tutto il codice di addestramento o il dataset usato per crearlo. È comunque un passo enorme rispetto ai modelli chiusi come GPT o Claude: puoi scaricare K3, farlo girare sui tuoi server, modificarlo con fine-tuning e usarlo senza dipendere da un'API a pagamento controllata da qualcun altro.

## Le novità tecniche

Sotto il cofano, K3 introduce alcune innovazioni architetturali degne di nota:

- **Kimi Delta Attention (KDA)**: un meccanismo di attenzione ibrida lineare che rende il modello più efficiente nel gestire contesti lunghissimi.
- **Attention Residuals (AttnRes)**: migliora la propagazione delle informazioni lungo sequenze molto estese.
- **Stable LatentMoE**: l'architettura Mixture-of-Experts che attiva solo una piccola frazione dei 2,8 trilioni di parametri per ogni token elaborato, tenendo sotto controllo i costi computazionali reali.

Moonshot dichiara che questa combinazione porta a un'efficienza di scaling circa 2,5 volte superiore rispetto a K2. Il modello supporta anche un contesto fino a 1 milione di token e accetta input multimodali nativi: testo, immagini e video.

## Come se la cava nei benchmark

Sul fronte prestazioni, K3 si è piazzato al primo posto nella Frontend Code Arena con 1.679 punti, superando Claude Fable 5 (1.631), GPT-5.6 Sol (1.618) e il cinese rivale GLM-5.2 (1.587). Su Terminal-Bench 2.1 raggiunge 88,3 punti, meglio di Claude Opus 4.8 (84,6). Moonshot lo presenta come il suo miglior modello per coding agentico: sessioni di lavoro lunghe, navigazione di repository enormi, orchestrazione di tool da terminale con supervisione umana minima.

## Serve un supercomputer per usarlo?

Qui viene il lato meno entusiasmante per chi vuole farlo girare su un PC di casa. Con 2,8 trilioni di parametri, anche con la quantizzazione MXFP4 che Moonshot ha applicato per ridurre lo spazio su disco a circa 1,4 TB, K3 resta un modello pensato per essere ospitato su cluster multi-nodo, non certo su una singola RTX consumer. Chi non ha accesso a hardware di fascia enterprise potrà comunque usarlo tramite API, con un prezzo di 3$/15$ per milione di token in input/output — competitivo con i modelli occidentali chiusi, ma pur sempre a pagamento.

## Perché interessa (anche) a chi non fa AI di mestiere

Il punto, per la community open source, non è tanto "posso farlo girare sul mio laptop" quanto "il fronte dei modelli aperti si sta avvicinando sempre di più a quello dei modelli proprietari, e lo sta facendo a un ritmo impressionante". Nel giro di poche settimane abbiamo visto uscire GLM-5.2, DeepSeek V4, Qwen 3.6 e ora K3: la Cina sta letteralmente inondando il mercato di modelli open-weight di altissimo livello, spesso a costi nettamente inferiori rispetto alle controparti americane closed-source.

Per chi gestisce infrastrutture self-hosted o segue da vicino l'ecosistema Ollama/vLLM, vale la pena tenere d'occhio le prossime settimane: è probabile che vedremo presto versioni quantizzate più leggere pensate per l'auto-hosting su hardware meno estremo, magari distillate in modelli più piccoli utilizzabili anche da chi non ha un data center in garage.
