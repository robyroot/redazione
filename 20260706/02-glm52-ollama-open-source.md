---
title: "GLM-5.2: il modello AI open source con 1 milione di token che puoi far girare con Ollama"
rilevanza: "ALTA"
fonte: "https://ollama.com/library/glm-5.2"
data_notizia: "2026-06-29"
tags: ["AI", "open-source", "ollama", "LLM", "privacy", "self-hosting", "GLM"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: focus sulla praticità e sulla privacy — puoi usare un modello frontier-level in locale, senza mandare dati a OpenAI. Evidenziare la licenza MIT e il comando ollama run glm-5.2. Menzionare l'opzione cloud di Ollama come alternativa per chi non ha hardware potente. Pubblico: utenti Linux che già conoscono Ollama o vogliono iniziare.
---

# GLM-5.2: il modello AI open source con 1 milione di token che puoi far girare con Ollama

Se segui l'AI open source, probabilmente sai già che il divario tra i modelli closed-source e quelli open si è enormemente ridotto negli ultimi mesi. GLM-5.2, rilasciato da Z.ai (ex Zhipu AI) il 29 giugno 2026, è l'ultimo esempio di questo trend: un modello con 744 miliardi di parametri totali (circa 40B attivi per token, architettura Mixture-of-Experts), finestra di contesto da quasi 1 milione di token, **licenza MIT**, e disponibile su Ollama sia in locale che via cloud.

In termini di benchmark, è il modello open source più forte al momento: 81.0 su Terminal-Bench 2.1 e 62.1% su SWE-bench Pro. Per dare un riferimento, Claude Fable 5 (il modello closed più capace) è all'80.3% su SWE-bench Pro. La distanza si misura ormai in decimali.

## Perché importa per chi usa Linux

La risposta corta: **privacy e controllo**. Con un modello MIT puoi:

- Eseguirlo localmente senza mandare una riga di codice o un documento a server esterni
- Usarlo in pipeline automatizzate senza costi per token
- Modificarlo, fine-tunarlo, redistribuirlo
- Non preoccuparti che i tuoi prompt vengano usati per addestrare versioni future

La finestra di contesto da ~1M token cambia le cose in modo concreto: puoi passargli un'intera codebase, un libro, settimane di log di sistema, e fare domande sull'insieme. Con i modelli da 128K token questo non era possibile senza trucchi di chunking.

## Come installarlo con Ollama

Se hai già Ollama installato, il comando è semplicissimo:

```bash
# Versione locale (richiede hardware potente — vedi sotto)
ollama run glm-5.2

# Versione cloud via Ollama (gira su infrastruttura Z.ai/Ollama)
ollama run glm-5.2:cloud
```

La versione `:cloud` invia i prompt all'infrastruttura cloud di Ollama (GPU Blackwell di NVIDIA), non in locale. Utile se non hai una GPU abbastanza potente, ma ovviamente non offre la privacy del self-hosting.

Se non hai ancora Ollama:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

## Di che hardware hai bisogno per girarlo in locale?

GLM-5.2 è un modello da 744B parametri — non è per tutti. In float16 puro servirebbero circa 1.5 TB di VRAM, che è fuori portata per chiunque non abbia un cluster. Ma con quantizzazione aggressiva (Q4_K_M):

| Precisione | VRAM necessaria | Velocità indicativa |
|---|---|---|
| FP16 | ~1.5 TB | Solo cluster |
| Q8 | ~750 GB | Multi-GPU high-end |
| Q4_K_M | ~375 GB | Multi-GPU prosumer |

Per uso domestico realistico, la versione `:cloud` è quella pratica. Oppure aspetta le versioni distillate che Z.ai sta preparando su scale più piccole.

## Un test pratico con la versione cloud

```bash
# Avvia una sessione interattiva
ollama run glm-5.2:cloud

# Oppure usa in modalità one-shot
ollama run glm-5.2:cloud "Spiega il comando awk in italiano con esempi pratici"

# Integrazione con curl per script
curl http://localhost:11434/api/generate -d '{
  "model": "glm-5.2:cloud",
  "prompt": "Analizza questo log di errore: [incolla il log]",
  "stream": false
}'
```

## Il contesto più ampio: open source AI sta vincendo?

GLM-5.2 non è solo un modello interessante in isolamento. È parte di una tendenza chiara: Meituan ha open-sourcato LongCat-2.0 (1.6T parametri, MIT, 59.5% SWE-bench Pro), Kimi ha rilasciato K2.6, e MiniMax ha M3. Tutti con licenze permissive. Tutti competitivi con i modelli closed.

Il vantaggio dei modelli proprietari rimane reale sulle task più complesse, ma si è ridotto al punto che per la maggior parte degli usi pratici — coding, analisi di testi, assistenza alla scrittura, Q&A su documenti — i modelli open bastano e avanzano. E puoi tenerli sulla tua macchina.

Per chi usa Linux per motivi di libertà digitale, questa è probabilmente la notizia più importante degli ultimi mesi in campo AI.
