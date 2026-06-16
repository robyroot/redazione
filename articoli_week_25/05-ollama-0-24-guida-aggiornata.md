---
title: "Ollama 0.24.0: le novità e i migliori modelli della settimana"
stato: "BOZZA"
fonte: "https://dev.to/pooyagolchian/local-ai-in-2026-running-production-llms-on-your-own-hardware-with-ollama-54d0"
tags: ["ollama", "ai", "linux", "tutorial", "open-source"]
livello: "beginner"
---

Cinquantadue milioni di download al mese. Crescita di 520 volte in tre anni. **Ollama** non è più uno strumento di nicchia per smanettoni: è diventato il modo più semplice al mondo per usare l'intelligenza artificiale sul proprio computer, senza internet, senza abbonamenti.

È appena uscita la versione **0.24.0**. Vediamo cosa porta.

## Cos'è Ollama, per chi non lo conosce

Ollama ti permette di scaricare e usare modelli AI direttamente sul tuo PC — **senza cedere dati a nessuno**. Funziona da riga di comando, ma è semplicissimo:

```bash
# Installa Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Scarica e avvia un modello
ollama run llama3.2
```

Da quel momento hai un assistente AI locale pronto all'uso.

## Le novità di Ollama 0.24.0

### Supporto Codex App
Ollama si integra ora nativamente con la Codex App. Puoi usare l'interfaccia Codex puntandola sui tuoi modelli locali invece che sui server di OpenAI.

### Speculative decoding per Gemma 4
Il speculative decoding velocizza la generazione di testo. Su Gemma 4 l'aumento di velocità è misurabile: risposte più rapide senza perdere qualità. Se usi Gemma 4 regolarmente, aggiorna subito.

## I migliori modelli da provare adesso

Con 135.000 modelli disponibili in formato GGUF su HuggingFace, la scelta può essere paralizzante. Guida rapida:

**PC con 8 GB di RAM (solo CPU):**
```bash
ollama run llama3.2:3b      # Veloce per Q&A
ollama run phi4-mini         # Ottimo per ragionamento
```

**GPU da 6-8 GB VRAM:**
```bash
ollama run qwen2.5:7b        # Tra i migliori nella fascia
ollama run gemma4:9b          # Buono per testi
```

**GPU da 16 GB+ VRAM:**
```bash
ollama run llama3.3:70b      # Qualità vicina ai cloud
ollama run qwen2.5:32b       # Eccellente per coding
```

## L'AI locale ha davvero vinto?

I numeri dicono di sì. La qualità dei modelli locali ha fatto un salto enorme: un anno fa la differenza rispetto a ChatGPT era evidente. Oggi, per molti casi d'uso quotidiani, è quasi impercettibile.

Restano vantaggi ai modelli cloud per compiti molto complessi — ragionamento avanzato, ricerca web in tempo reale. Ma per leggere documenti, scrivere, spiegare codice, rispondere a domande tecniche? Un buon modello locale basta.

E la tua privacy rimane tua.

## Per iniziare adesso

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama run llama3.2
```

Meno di 5 minuti. Poi mi dici se non impressiona.
