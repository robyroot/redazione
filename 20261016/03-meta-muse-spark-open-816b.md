---
title: "Meta lancia Muse Spark Open: 816 miliardi di parametri open weight e gira anche sui Mac"
rilevanza: "ALTA"
fonte: "https://techcrunch.com/2026/10/15/meta-launches-an-open-weight-model-that-runs-on-macs"
data_notizia: "2026-10-15"
tags: ["AI", "Meta", "open source", "LLM", "open weight", "Muse Spark"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: confrontare con Llama e spiegare la differenza tra "open source" e "open weight" — un tema caro al pubblico di RobyRoot. Enfatizzare che gira su Mac (e quindi si avvicina alla possibilità di girare in locale su hardware consumer), e discutere la licenza non completamente libera.
---

# Meta lancia Muse Spark Open: 816 miliardi di parametri open weight e gira anche sui Mac

Meta ha rilasciato ieri i pesi di **Muse Spark Open**, il suo nuovo modello linguistico di grandi dimensioni, rendendolo disponibile a sviluppatori e ricercatori. Con 816 miliardi di parametri e una finestra di contesto da 1 milione di token, è uno dei modelli open weight più grandi mai rilasciati pubblicamente.

La notizia ha fatto rumore soprattutto per un dettaglio pratico: il modello è ottimizzato per girare anche su Mac con chip Apple Silicon. Non è una cosa banale per un modello di queste dimensioni.

## Open weight, non open source: la distinzione che conta

Prima di entusiasmarsi troppo, vale la pena chiarire una distinzione importante che nel mondo AI si tende spesso a ignorare: **open weight non significa open source**.

Con Muse Spark Open, Meta rilascia i **pesi del modello** — cioè i valori numerici che definiscono il comportamento del modello addestrato. Non rilascia il codice di addestramento, i dati usati per l'addestramento, né i dettagli architetturali completi.

È come ricevere un programma compilato senza il codice sorgente: puoi eseguirlo, puoi studiarne il comportamento, puoi anche modificarlo parzialmente, ma non puoi replicare dall'inizio il processo che lo ha creato.

Questa distinzione è importante per la comunità open source: modelli come Muse Spark Open aumentano l'accessibilità, ma non la trasparenza completa.

## La licenza: attenzione se fate business

La licenza di Muse Spark Open ha alcune condizioni da tenere a mente:

- È **gratuito** per uso personale, ricerca e sviluppo
- Richiede l'attributo "**Built with Muse Spark Open**" nelle applicazioni che lo usano
- Chi vuole **vendere accesso API** al modello e supera i 20 milioni di dollari di ricavi annui deve stipulare un accordo commerciale separato con Meta

Per la maggior parte degli sviluppatori e degli utenti di RobyRoot questa licenza è più che accettabile. Ma se state costruendo un prodotto commerciale che si basa su questo modello, leggete attentamente prima di integrarlo.

## Come provarlo adesso

Muse Spark Open è già disponibile su diverse piattaforme:

```bash
# Tramite Ollama (quando disponibile nel registry)
ollama pull muse-spark-open

# Oppure tramite API di OpenRouter
curl https://openrouter.ai/api/v1/chat/completions \
  -H "Authorization: Bearer $OPENROUTER_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "meta/muse-spark-open",
    "messages": [{"role": "user", "content": "Ciao!"}]
  }'
```

Le piattaforme che lo ospitano includono Groq (per inferenza veloce), Together AI, Fireworks AI, Baseten, Modal e Nebius. Per chi ha un Mac con Apple Silicon abbastanza potente, Meta promette che potrà farlo girare in locale — anche se per un modello da 816B parametri servirà hardware enterprise.

## Il contesto: ottobre 2026 è un mese di svolta per i modelli open

Muse Spark Open non è l'unica novità in questo senso. In meno di dieci giorni, dal 6 al 15 ottobre, il panorama dei modelli open weight è cambiato significativamente:

- **Mistral Large 4** (preview il 6 ottobre)
- **Muse Spark Open** di Meta (pesi su Hugging Face il 15 ottobre)
- **Nemotron 3.5 Bolt** di NVIDIA (sempre il 15 ottobre)

Secondo i benchmark di Artificial Analysis, i modelli più competitivi nel segmento open weight di questo momento sono **GLM-5.3** di Zhipu AI e **Kimi K3** di Moonshot AI — entrambi rivali seri per Muse Spark Open.

## Perché importa per chi usa Linux e AI locale

Per il pubblico di RobyRoot, la domanda pratica è: questo avvicina la possibilità di avere un modello di qualità top che gira completamente in locale, senza inviare dati a server di terze parti?

La risposta onesta è: **un po', ma non ancora per l'hardware consumer**. Un modello da 816B parametri in bf16 occupa circa 1.6 TB di RAM/VRAM. Anche quantizzato a 4 bit, si parla di circa 400 GB. Siamo ancora lontani dal "gira sul vostro laptop".

Ma la direzione è quella giusta. Ogni rilascio open weight di questa portata abbassa la barriera alla ricerca e alla sperimentazione, e spinge l'ecosistema di ottimizzazione (quantizzazione, distillazione, fine-tuning) a lavorare su modelli sempre più capaci. Il futuro dell'AI locale è open weight, anche se ci vorrà ancora qualche anno prima che sia davvero alla portata di tutti.
