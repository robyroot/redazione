---
title: "Janus: un singolo binario Go per girare modelli AI locali — no Python, no Docker, no cloud"
rilevanza: "MEDIA"
fonte: "https://github.com/Vibra-Ingenn/Janus"
data_notizia: "2026-10-02"
tags: ["AI", "LLM", "GGUF", "Go", "open-source", "privacy", "local-AI"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: il punto di forza di Janus è la semplicità radicale — nessuna dipendenza Python, nessun Docker. Perfetto per chi vuole AI locale su Linux senza il peso di Ollama o LM Studio. Sottolinea l'aspetto privacy e l'indipendenza dal cloud.
---

# Janus: un singolo binario Go per girare modelli AI locali — no Python, no Docker, no cloud

Chi vuole eseguire modelli linguistici in locale su Linux si scontra spesso con lo stesso problema: l'ecosistema AI è dominato da Python, con virtualenv, dipendenze in conflitto e setup che richiedono mezz'ora anche solo per partire. **Janus** prova una strada diversa: un singolo eseguibile Go che fa tutto, senza installare altro.

## Cos'è Janus

Janus è un server HTTP scritto in Go che carica modelli in formato **GGUF** (il formato portabile di llama.cpp) e li espone tramite un'**API compatibile con OpenAI**. Questo significa che qualsiasi tool che parla con ChatGPT via API — LiteLLM, Open WebUI, VS Code Copilot, Continue.dev — può essere puntato su Janus senza modifiche.

Il progetto è apparso su Hacker News il 2 ottobre 2026 e ha raccolto attenzione per la semplicità radicale dell'approccio: niente stack Python, niente container, niente CUDA obbligatorio. Il backend di inferenza è **llama.cpp con Vulkan**, il che significa supporto per GPU AMD, Intel e Nvidia, più un fallback automatico su CPU.

## Installazione in tre comandi

```bash
# Scarica il binario pre-compilato (Linux x86_64)
wget https://github.com/Vibra-Ingenn/Janus/releases/latest/download/janus-linux-amd64
chmod +x janus-linux-amd64
sudo mv janus-linux-amd64 /usr/local/bin/janus
```

Non serve altro. Nessun `pip install`, nessun `docker pull`, nessun ambiente virtuale.

## Configurazione di base

Crea un file `.env` nella directory da cui vuoi avviare il server:

```env
# Backend: vulkan (GPU) oppure cpu
JANUS_BACKEND=vulkan

# Percorso al modello GGUF
JANUS_MODEL_PATH=/home/utente/modelli/llama-3.2-3b-instruct.Q4_K_M.gguf

# Numero massimo di token in output
JANUS_MAX_TOKENS=2048

# Porta su cui ascoltare
JANUS_PORT=8080
```

Poi avvia:

```bash
janus
# oppure in background
janus &
```

A questo punto hai un endpoint OpenAI-compatibile su `http://localhost:8080`.

## Testare che funzioni

```bash
curl http://localhost:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "local",
    "messages": [{"role": "user", "content": "Ciao! Dimmi una barzelletta su Linux."}]
  }'
```

Dovresti ricevere una risposta JSON standard, identica a quella che restituisce l'API di OpenAI. Da qui puoi usarlo con qualsiasi client.

## Hot-swap dei modelli

Una delle feature più interessanti di Janus è la possibilità di cambiare modello senza riavviare il server:

```bash
# Cambia modello al volo via API
curl -X POST http://localhost:8080/v1/models/load \
  -H "Content-Type: application/json" \
  -d '{"model_path": "/home/utente/modelli/mistral-7b-instruct.Q5_K_M.gguf"}'
```

Utile se stai sperimentando con modelli diversi o se vuoi caricare un modello più piccolo/grande in base al carico.

## Dove trovare i modelli GGUF

Il posto migliore è **Hugging Face**, cercando repository con `-GGUF` nel nome. Alcune partenze valide:

```bash
# Con huggingface-cli (pip install huggingface_hub)
huggingface-cli download bartowski/Llama-3.2-3B-Instruct-GGUF \
  --include "*.Q4_K_M.gguf" \
  --local-dir ~/modelli/

# Oppure con wget diretto (cerca l'URL raw su HF)
wget "https://huggingface.co/bartowski/Llama-3.2-3B-Instruct-GGUF/resolve/main/Llama-3.2-3B-Instruct-Q4_K_M.gguf" \
  -O ~/modelli/llama3.2-3b.gguf
```

Per uso quotidiano su hardware consumer (16 GB RAM), Llama 3.2 3B o Mistral 7B in formato Q4_K_M sono buoni punti di partenza.

## Perché non Ollama?

Ollama fa le stesse cose e ha un ecosistema più maturo. La differenza con Janus è filosofica: Ollama ha il suo runtime, il suo sistema di gestione modelli, i suoi layer di astrazione. Janus è semplicemente "llama.cpp con Vulkan dietro un'API HTTP". Se usi già llama.cpp e vuoi esporlo come API senza installarti l'intero ecosistema Ollama, Janus ha senso. Se stai partendo da zero, Ollama è probabilmente più comodo.

## Il punto sulla privacy

Il vero motivo per cui vale la pena guardarci è questo: **nessun dato esce dalla tua macchina**. Nessuna chiamata a OpenAI, nessun telemetria, nessun log su server remoti. Per uso aziendale, per documenti sensibili o semplicemente per chi preferisce non regalare i propri prompt a qualcuno, l'AI locale resta la scelta più pulita. E con strumenti come Janus, il costo di setup si sta avvicinando a zero.

---

*Fonte: [GitHub — Vibra-Ingenn/Janus](https://github.com/Vibra-Ingenn/Janus), [Google Open Source Blog](https://opensource.googleblog.com/2026/10/this-week-in-open-source-for-october-2-2026.html)*
