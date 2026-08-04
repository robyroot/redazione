---
title: "DeepSeek-V4-Flash-0731: il modello open source che batte il fratello maggiore (e costa un terzo)"
rilevanza: "MEDIA"
fonte: "https://www.marktechpost.com/2026/07/31/deepseek-upgrades-deepseek-v4-flash-0731-with-major-agentic-and-coding-gains/"
data_notizia: "2026-07-31"
tags: ["ai", "open source", "deepseek", "llm", "self-hosting"]
livello: "intermediate"
nota_editoriale: |
  Buon pezzo per la rubrica AI open source: taglio consigliato su due assi, uno per chi vuole solo capire cosa succede nel panorama dei modelli aperti, uno più pratico per chi vuole provare a farlo girare in locale (requisiti hardware, quantizzazione). Si presta anche a un confronto futuro con GLM-5.2, altro modello MIT cinese uscito da poco, per un articolo "comparativa" successivo.
---

Nel mondo dei modelli linguistici open weight, DeepSeek continua a essere uno dei protagonisti più prolifici, e il 31 luglio 2026 ha rilasciato la versione ufficiale di **DeepSeek-V4-Flash-0731**, che sostituisce definitivamente la preview uscita in aprile. La notizia interessante non è tanto l'ennesimo modello che esce, quanto il fatto che questa versione "economica" della famiglia V4 riesca a battere sul proprio terreno il modello più grande e costoso della stessa azienda, V4-Pro.

## Cosa cambia rispetto alla preview

Partiamo dai numeri: V4-Flash-0731 ha **284 miliardi di parametri totali, con 13 miliardi attivi per token** (304 miliardi contando anche il modulo DSpark per la decodifica speculativa, una tecnica che accelera la generazione del testo). È lo stesso identico scheletro architetturale della preview di aprile — stessa dimensione, stesso mix di 256 esperti instradati per layer MoE con 6 attivi per token, e la stessa attenzione ibrida che combina Compressed Sparse Attention e Heavily Compressed Attention per gestire in modo efficiente un contesto fino a 1 milione di token.

La differenza sta tutta nel **post-training**: DeepSeek ha ri-addestrato il modello concentrandosi specificamente sulle capacità agentiche, cioè sulla capacità del modello di usare strumenti, ragionare su più passaggi e portare a termine compiti complessi in autonomia — l'area in cui, in questo momento, si gioca davvero la competizione tra modelli.

## I numeri che contano

I miglioramenti sui benchmark interni di DeepSeek sono notevoli: su Terminal Bench 2.1 (un test che misura la capacità di operare in un ambiente a riga di comando) il punteggio sale da 61.8 della preview a 82.7, superando persino il più grande V4-Pro-Preview, fermo a 72.1. Su DeepSWE, benchmark orientato allo sviluppo software agentico, il salto è ancora più netto: da 7.3 a 54.4. Su Cybergym si passa da 38.7 a 76.7.

Va detto con onestà, come nota anche la stessa documentazione tecnica: questi benchmark sono stati misurati con un harness di valutazione interno non ancora reso pubblico, quindi vanno presi come indicazione di tendenza più che come verità assoluta — la prassi giusta, come sempre con i numeri auto-riportati dai laboratori, è aspettare valutazioni indipendenti prima di trarre conclusioni definitive.

## Licenza, prezzo e disponibilità

Il modello è rilasciato con **licenza MIT, senza gate**, quindi utilizzabile anche in contesti commerciali e on-premise senza restrizioni particolari — un punto a favore non scontato in un panorama dove molti modelli "open" nascondono clausole più restrittive nelle condizioni d'uso.

Sul fronte prezzo, via API costa $0.14 per milione di token in input (che scende a $0.0028 in caso di cache hit) e $0.28 per milione in output — circa un terzo del costo di V4-Pro, a fronte di prestazioni agentiche superiori sui benchmark citati. È disponibile dal 31 luglio sia tramite l'API ufficiale DeepSeek sia via chat.deepseek.com, con supporto nativo al formato Responses API e compatibilità con Codex.

## E per chi vuole farlo girare in locale?

Qui arriva la parte più interessante per chi segue RobyRoot: essendo pesi aperti su Hugging Face, è possibile fare self-hosting, ma servono risorse hardware non banali. Per una quantizzazione a 3 bit servono circa 110 GB di memoria, mentre per la full precision serve un nodo GPU completo — quindi stiamo parlando di setup da workstation professionale o piccolo server con più GPU, non certo del vostro laptop. Per chi ha accesso a hardware di quel calibro (o vuole affittare un'istanza cloud a ore), è comunque un'opzione concreta per avere un modello competitivo con i migliori modelli chiusi, senza dipendere da un'API esterna e con pieno controllo sui dati che ci passate.

In un panorama dominato dalle notizie sui modelli chiusi di OpenAI, Google e Anthropic, il fatto che un modello open weight, gratuito da scaricare e modificare, riesca a competere sui benchmark agentici con i migliori modelli commerciali resta una delle storie più interessanti dell'AI nel 2026 — e vale la pena tenerla d'occhio.
