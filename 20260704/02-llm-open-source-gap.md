---
title: "GLM-5.2 e LongCat-2.0: l'open source AI sta davvero per raggiungere i modelli proprietari?"
rilevanza: "ALTA"
fonte: "https://llm-stats.com/llm-updates"
data_notizia: "2026-06-30"
tags: ["AI", "LLM", "open-source", "GLM", "LongCat", "modelli-locali", "MIT"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: focus sulla possibilità concreta di usare questi modelli localmente, MIT license = zero restrizioni commerciali. Il pubblico di RobyRoot apprezza l'autonomia tecnologica — avere un modello AI di frontiera che gira su hardware domestico (o quasi) è esattamente il tipo di notizia che tira.
---

# L'AI open source sta chiudendo il gap: GLM-5.2 e LongCat-2.0 cambiano le regole

Per anni il divario tra i modelli AI open source e quelli proprietari sembrava incolmabile. GPT, Claude, Gemini — da una parte i giganti con miliardi di dollari di compute; dall'altra la comunità open source a rincorrere. Ma nell'ultima settimana di giugno 2026 sono arrivati due rilasci che fanno capire quanto velocemente stia cambiando il panorama: **GLM-5.2** di Z.ai e **LongCat-2.0** di Meituan, entrambi con licenza MIT e benchmark che fanno impallidire molti modelli a pagamento di 6 mesi fa.

## GLM-5.2: il modello MIT che sfida i frontier model

Rilasciato il 16 giugno 2026, GLM-5.2 è un'architettura Mixture-of-Experts con **744 miliardi di parametri totali**, di cui solo circa 40 miliardi vengono attivati per ogni token. Questa scelta architetturale — la stessa usata da Mixtral e DeepSeek — permette di ottenere le prestazioni di un modello enorme con i costi computazionali di uno molto più piccolo.

La novità tecnica più interessante è **IndexShare**: un'ottimizzazione all'attenzione sparsa che riduce il compute necessario per token di 2,9× ai contesti lunghi (1 milione di token). In pratica, GLM-5.2 gestisce documenti enormi senza esplodere in termini di VRAM.

I numeri sui benchmark parlano chiaro: sul **SWE-Bench Pro** (il benchmark più usato per valutare le capacità di coding), GLM-5.2 segna **62,1%** — meglio di GPT-5.5 e molto vicino a Claude Opus 4.8. Il modello proprietario di riferimento, Claude Fable 5, è al 80,3%. Il gap si è ridotto a 18 punti percentuali da quello che era una distanza abissale solo un anno fa.

La cosa forse più importante: **licenza MIT** completa. Nessuna restrizione commerciale, nessun filtro di contenuto imposto, nessuna API obbligatoria.

## LongCat-2.0: 1,6 trilioni di parametri per il coding agentivo

Meituan ha rilasciato LongCat-2.0 il 30 giugno 2026, ed è un caso a parte anche nel panorama dei modelli enormi. Parliamo di **1,6 trilioni di parametri** — il primo modello di questa dimensione ad essere addestrato e a girare in inferenza su un cluster di 50.000 GPU cinesi. L'attivazione dinamica va da 33B a 56B parametri per token (media ~48B), quindi in inferenza si comporta come un modello da 48B.

Il focus di LongCat-2.0 è il **coding agentivo**: non solo generare codice, ma ragionare su task complessi, usare strumenti, eseguire codice e iterare. Sul SWE-Bench Pro segna **59,5%**, rendendolo il miglior modello open source per coding agentivo dopo GLM-5.2. Anche questo è MIT.

Entrambi supportano **1 milione di token di contesto** — abbastanza per caricare interi codebase o documenti complessi in una sola query.

## Posso farlo girare localmente?

Dipende dall'hardware. GLM-5.2 con 40B parametri attivi richiede indicativamente 80GB di VRAM per girare in precisione intera (FP16), che scendono a circa 40GB con quantizzazione a 4-bit. Non è roba da consumer desktop, ma chi ha una workstation con due A100 o accesso a un cloud spot è già in pista.

Per chi vuole provare senza hardware dedicato:

```bash
# Con Ollama (modello quantizzato)
ollama pull glm5.2:40b-q4

# Con llama.cpp (se hai il GGUF)
./llama-server -m glm5.2-40b-Q4_K_M.gguf --ctx-size 8192 -ngl 40

# Con vLLM (per chi ha GPU serie A/H)
pip install vllm
python -m vllm.entrypoints.openai.api_server \
  --model THUDM/GLM-5.2 \
  --tensor-parallel-size 2
```

Per LongCat-2.0, essendo un modello da 1,6T, le opzioni consumer sono molto più limitate — ma i quantizzati a 4-bit potrebbero girare con 64-80GB su sistemi con molto RAM unificata.

## Cosa significa per noi

Il messaggio di questi rilasci è chiaro: il monopolio dei modelli proprietari sta cedendo. Non perché gli open source siano già migliori — Claude Fable 5 è ancora davanti — ma perché il gap si sta chiudendo più velocemente di quanto nessuno si aspettasse, e con licenze che permettono a chiunque di usarli senza dover pagare per ogni token o accettare condizioni d'uso restrittive.

Per chi usa AI nel proprio workflow quotidiano — sviluppo, scrittura, analisi — la disponibilità di modelli di questa qualità con licenza MIT cambia concretamente le opzioni sul tavolo. Self-hosting, fine-tuning, integrazione in prodotti propri: tutto senza chiedere il permesso a nessuno.
