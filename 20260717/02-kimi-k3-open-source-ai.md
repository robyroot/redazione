---
title: "Kimi K3: il modello AI open source da 2,8 trilioni di parametri che sfida i giganti"
rilevanza: "ALTA"
fonte: "https://venturebeat.com/technology/chinas-moonshot-ai-releases-kimi-k3-the-largest-open-source-model-ever-rivaling-top-u-s-systems"
data_notizia: "2026-07-16"
tags: ["AI", "open-source", "LLM", "modelli", "Kimi", "MoE"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Evidenziare che i pesi saranno rilasciati il 27 luglio, rendendo possibile l'esecuzione locale (con hardware adeguato). Sottolineare il trend dei modelli cinesi open weight che colmano il gap con i modelli proprietari occidentali.
---

# Kimi K3: il modello AI open source da 2,8 trilioni di parametri che sfida i giganti

Qualcosa di significativo è successo ieri nel mondo dell'intelligenza artificiale open source. Moonshot AI, startup cinese supportata da Alibaba, ha rilasciato **Kimi K3**: con i suoi **2,8 trilioni di parametri**, è il modello open source più grande mai creato. E i pesi saranno disponibili per il download entro fine luglio.

## Numeri da capogiro

Kimi K3 è un modello **Mixture of Experts (MoE)**: ha 896 esperti specializzati, ma ne attiva solo 16 per volta durante l'elaborazione. Questo approccio permette di avere una capacità enorme senza dover attivare tutta la rete per ogni token — il che rende il modello più efficiente di quanto i 2,8 trilioni di parametri farebbero pensare.

Le caratteristiche principali:

- **Contesto di 1 milione di token** — può elaborare libri interi, interi codebase, enormi raccolte di documenti in un'unica sessione
- **Comprensione visiva nativa** — non richiede moduli separati per le immagini
- **Kimi Delta Attention (KDA)** — un'architettura ibrida di attenzione lineare sviluppata internamente per gestire contesti lunghissimi in modo efficiente
- **Benchmark SWE-bench Verified**: prestazioni competitive con i migliori modelli closed source per attività di coding e problem solving

Il modello è già disponibile tramite API su kimi.com e i pesi open source saranno rilasciati entro il **27 luglio 2026**.

## Il gap con i modelli proprietari si sta chiudendo

Fino a poco tempo fa, c'era un divario netto tra i modelli open source e quelli proprietari come GPT-5 o Claude Fable 5. Kimi K3 contribuisce a ridurlo ulteriormente.

Su alcune benchmark il distacco è ormai a singola cifra percentuale. Su SWE-bench Pro — che misura la capacità di risolvere bug reali in repository open source — il miglior modello open source si attesta al 62,1% contro l'80,3% del miglior modello closed. Un gap che un anno fa era molto più ampio.

Questo è parte di un trend più ampio: i modelli cinesi open weight stanno dominando le classifiche di popolarità su Hugging Face (41% dei download in primavera) e su OpenRouter i sei modelli più usati sono tutti open source di aziende cinesi.

## Come usarlo adesso

Se vuoi provarlo senza aspettare i pesi:

**Via API** (accesso immediato):
```bash
pip install openai  # Kimi K3 supporta l'API compatibile OpenAI

# Esempio di chiamata
curl https://api.moonshot.cn/v1/chat/completions \
  -H "Authorization: Bearer $KIMI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kimi-k3",
    "messages": [{"role": "user", "content": "Ciao!"}]
  }'
```

I prezzi API sono: $0,30 per milione di token in input (cache), $3 per milione in input (no cache), $15 per milione in output.

**Via interfaccia web**: disponibile su [kimi.com](https://kimi.com) già da ora.

## Quando arrivano i pesi open source

Il rilascio dei pesi è previsto per il **27 luglio 2026** e sarà probabilmente su Hugging Face. Con 2,8 trilioni di parametri MoE, eseguire il modello completo localmente richiederà hardware serio: si parla di cluster multi-GPU con decine di terabyte di VRAM.

Detto questo, la community open source è brava a produrre versioni quantizzate che girano su hardware consumer. Nei giorni successivi al rilascio ci si aspettano versioni GGUF per llama.cpp e versioni a 4-bit ottimizzate per chi ha una singola GPU da 24GB o più.

## Perché importa per chi usa Linux e AI locale

L'arrivo di modelli di questa potenza nel mondo open source è una notizia eccellente per chi vuole **AI privata e locale**. Anche se le versioni quantizzate perdono parte delle prestazioni, rimangono strumenti potentissimi — e il fatto che esistano pesi aperti significa che nessun'azienda può ritirarlo, modificarlo silenziosamente o cambiarne i termini di utilizzo.

Per chi segue il progetto **Ollama**, **LM Studio** o gestisce modelli in autonomia: vale la pena tenere d'occhio i repository Hugging Face di Moonshot AI nei prossimi giorni. Kimi K3 quantizzato potrebbe diventare il nuovo riferimento per l'AI locale ad alte prestazioni.

## Conclusione

Kimi K3 è un segnale chiaro: il futuro dell'AI non è solo nelle mani dei grandi laboratori americani. Con 2,8 trilioni di parametri open weight, un contesto da 1 milione di token e prestazioni che sfidano i migliori modelli proprietari, Moonshot AI ha alzato significativamente l'asticella per tutti. Segnati il 27 luglio sul calendario.
