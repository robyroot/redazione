---
title: "Janus: AI locale con un singolo binario Go, senza Python né Docker"
rilevanza: "MEDIA"
fonte: "https://github.com/Vibra-Ingenn/Janus"
data_notizia: "2026-10-02"
tags: ["ai", "open-source", "linux", "llm", "llama.cpp", "gpu", "go", "gguf"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: perfetto per chi vuole avvicinarsi all'AI locale senza la complessità di Ollama o LM Studio. Un singolo binario Go che funziona su AMD, Intel e Nvidia tramite Vulkan è esattamente il tipo di tool "Linux-first" che piace al pubblico del blog.
---

# Janus: AI locale con un singolo binario Go, senza Python né Docker

Vuoi eseguire un modello AI in locale ma non hai voglia di installare Python, costruire una Docker image, o capire come funziona Ollama? **Janus** potrebbe essere quello che cerchi.

È un singolo binario scritto in Go che scarica, esegue modelli GGUF tramite llama.cpp e li espone con un'API compatibile OpenAI — tutto senza dipendenze esterne, tutto su GPU tramite Vulkan (quindi AMD, Intel e Nvidia), con fallback su CPU quando non c'è accelerazione hardware.

## Il problema che risolve

Lo stack per l'AI locale è diventato... complicato. Hai Ollama, LM Studio, llama.cpp direttamente, jan.ai, vari wrapper Python, Docker con CUDA, e via dicendo. Per chi usa Linux e ama la semplicità, avere una catena di dipendenze da 500MB solo per girare un modello da 4GB è frustrante.

Janus prende un approccio diverso: **un solo eseguibile, zero runtime dipendenze**. Scarichi il binario, punti a un file `.gguf`, e hai un server API locale che risponde al tuo client preferito.

## Come funziona in pratica

Prima di tutto, scarica il binario dal repository GitHub e dai i permessi di esecuzione:

```bash
# Scarica l'ultima release
wget https://github.com/Vibra-Ingenn/Janus/releases/latest/download/janus-linux-amd64
chmod +x janus-linux-amd64
sudo mv janus-linux-amd64 /usr/local/bin/janus
```

Poi ti serve un modello GGUF. Puoi trovarne su Hugging Face — cerca modelli con "GGUF" nel nome. Un buon punto di partenza per chi ha poca VRAM è Qwen 2.5 3B o Phi-3.5 Mini:

```bash
# Scarica un modello (es. Qwen 2.5 3B quantizzato Q4)
wget https://huggingface.co/Qwen/Qwen2.5-3B-Instruct-GGUF/resolve/main/qwen2.5-3b-instruct-q4_k_m.gguf
```

E poi avvia Janus:

```bash
janus --model qwen2.5-3b-instruct-q4_k_m.gguf --port 8080
```

A questo punto hai un server che risponde all'indirizzo `http://localhost:8080` con un'API compatibile con quella di OpenAI. Puoi testarlo così:

```bash
curl -s http://localhost:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "local",
    "messages": [{"role": "user", "content": "Ciao! Come stai?"}]
  }' | python3 -m json.tool
```

## GPU tramite Vulkan: perché è importante

La maggior parte delle soluzioni AI locali per GPU usa CUDA (Nvidia only) o ROCm (AMD only, con supporto variabile). Vulkan è diverso: è un'API grafica/compute cross-vendor che funziona su praticamente qualsiasi GPU moderna, incluse le Intel Arc e le AMD iGPU integrate nelle CPU Ryzen.

Per Janus questo significa che **non devi preoccuparti del driver AI della tua scheda**: se Vulkan funziona (e su Linux quasi sempre funziona), la GPU verrà usata per l'inferenza.

Per verificare che Vulkan sia disponibile:

```bash
# Installa vulkan-tools se non ce l'hai
sudo apt install vulkan-tools  # Debian/Ubuntu

# Verifica le GPU Vulkan disponibili
vulkaninfo --summary
```

## Hot-swap dei modelli

Una feature interessante di Janus è la possibilità di cambiare modello senza riavviare il server. Se stai lavorando con un client che supporta la selezione del modello (come Open WebUI o ChatBot UI), puoi passare da un modello all'altro al volo.

```bash
# Lancia con più modelli disponibili
janus --models-dir /home/user/modelli/ --port 8080
```

## Quando usarlo e quando no

Janus è ottimo se:
- Vuoi la soluzione più semplice possibile su Linux
- Hai una GPU AMD o Intel che non è supportata bene da altri tool
- Hai già un client che parla API OpenAI (Open WebUI, Shell-GPT, ecc.)
- Odi installare dipendenze Python

Potrebbe non essere la scelta giusta se:
- Hai bisogno di un'interfaccia web integrata (Janus è solo il backend)
- Usi modelli multimodali o con embedding particolari
- Preferisci l'ecosistema Ollama che ha più modelli pre-configurati

## Il contesto più ampio

L'AI locale è ormai abbastanza matura da avere un problema di proliferazione di tool. Janus rappresenta una filosofia precisa: meno è di più. Un singolo binario Go compilato staticamente è l'opposto di un ambiente Conda da 3GB.

Per il pubblico Linux che apprezza la semplicità di un tool che fa una cosa sola e la fa bene, è un progetto da tenere d'occhio.
