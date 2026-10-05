---
title: "OpenAI apre i modelli: GPT-oss-120b e GPT-oss-20b sotto licenza Apache 2.0"
rilevanza: "ALTA"
fonte: "https://www.digitalapplied.com/blog/ai-model-releases-october-2026-tracker"
data_notizia: "2026-10-03"
tags: ["ai", "openai", "open-source", "llm", "apache", "privacy"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: La svolta storica dell'azienda che per anni ha resistito all'open source. Spiega cosa significa Apache 2.0 rispetto alle licenze precedenti, dai istruzioni pratiche per eseguire il modello in locale (Ollama, llama.cpp), e collega al tema privacy — dati sensibili che non escono dall'infrastruttura aziendale.
---

# OpenAI apre i modelli: GPT-oss-120b e GPT-oss-20b sotto licenza Apache 2.0

Per anni OpenAI ha fatto del nome "aperto" una sorta di promessa non mantenuta. Il "Open" in OpenAI era diventato un running joke nella comunità tech. Poi, questa settimana, è arrivato l'annuncio che pochi si aspettavano davvero: due modelli open-weight rilasciati sotto licenza Apache 2.0.

## Cosa sono GPT-oss-120b e GPT-oss-20b

I due modelli si chiamano **GPT-oss-120b** e **GPT-oss-20b**, dove "oss" sta per open-source e il numero indica i parametri in miliardi. Il modello più grande, con 120 miliardi di parametri, è pensato per chi ha hardware serio — GPU con 80GB+ di VRAM, o configurazioni multi-GPU. Il più piccolo, a 20 miliardi, può girare su hardware consumer di fascia alta: una RTX 4090 o una AMD RX 7900 XTX con 24GB di VRAM dovrebbero bastare con quantizzazione a 4-bit.

Entrambi sono **open-weight**: i pesi del modello sono pubblicamente scaricabili, modificabili e redistribuibili. Apache 2.0 è una delle licenze più permissive in circolazione — puoi usarli in produzione, integrarli in prodotti commerciali, distribuire versioni modificate, senza royalty né permessi da chiedere.

## Perché è una notizia enorme

Prima di questa settimana, tutti i modelli GPT erano accessibili esclusivamente via API, con OpenAI che controllava ogni singola inferenza. Ora chiunque può scaricare i pesi, eseguirli localmente, fare fine-tuning su dati proprietari, e distribuire applicazioni GPT-based senza passare per i server di OpenAI.

Per le aziende con requisiti stringenti di privacy — sanità, giustizia, finanza, pubblica amministrazione — questo è potenzialmente rivoluzionario. Dati sensibili che non possono uscire dall'infrastruttura interna potranno essere processati da modelli di qualità GPT senza mandare un byte a server di terze parti.

## Come iniziare con GPT-oss-20b in locale

Il punto di partenza più semplice è Ollama, che gestisce download, quantizzazione e serving in modo trasparente:

```bash
# Installa Ollama se non lo hai già
curl -fsSL https://ollama.ai/install.sh | sh

# Scarica e avvia GPT-oss-20b (circa 12GB in 4-bit)
ollama run gpt-oss-20b

# Per usarlo via API locale (compatibile con OpenAI API)
curl http://localhost:11434/api/generate \
  -d '{"model": "gpt-oss-20b", "prompt": "Spiega Rust in 3 righe"}'
```

Per chi preferisce più controllo con llama.cpp:

```bash
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp && make -j$(nproc)

# Scarica i pesi da Hugging Face
pip install huggingface-hub
huggingface-cli download openai/gpt-oss-20b \
  --local-dir ./models/gpt-oss-20b \
  --include "*.gguf"

# Esegui l'inferenza
./main -m ./models/gpt-oss-20b/model-Q4_K_M.gguf \
  -p "Il ruolo di Linux nell'AI moderna:" \
  -n 200
```

E se vuoi integrarlo in un'applicazione Python:

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
import torch

model_id = "openai/gpt-oss-20b"
tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(
    model_id,
    torch_dtype=torch.bfloat16,
    device_map="auto"
)

inputs = tokenizer("Cos'è il kernel Linux?", return_tensors="pt")
outputs = model.generate(**inputs, max_new_tokens=200)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

## Il confronto con la concorrenza

GPT-oss-20b non è attualmente il modello open-weight più performante in assoluto: il GLM-5.2 di Zhipu AI guida le classifiche con un impressionante 62.1% su SWE-bench Pro. Ma il brand OpenAI porta con sé un ecosistema enorme di strumenti, tutorial e community: molti sviluppatori conoscono già l'API di OpenAI, e la transizione verso GPT-oss in locale richiederà uno sforzo minimo.

Anche Alibaba Qwen 3.7 e Meta Llama rimangono competitor solidi con licenze altrettanto permissive. La buona notizia è che la competizione aperta fa bene a tutti: i modelli migliorano più velocemente e i costi di deployment continuano a scendere.

## Il futuro dell'AI locale

Questa mossa di OpenAI difficilmente è puramente filantropica — serve a guadagnare mindshare degli sviluppatori e a contrastare la crescente popolarità di Qwen e GLM sul fronte open. Ma le motivazioni contano meno del risultato: modelli GPT-quality girano ora sul tuo hardware, sotto la tua piena supervisione, senza inviare un byte a server di terze parti.

L'AI locale non è più un compromesso tecnico. È una scelta matura, a volte la scelta migliore.
