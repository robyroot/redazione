---
title: "Liquid AI LFM3: sei modelli AI open-weight che girano con 1GB di RAM"
rilevanza: "ALTA"
fonte: "https://etcjournal.com/2026/10/29/top-ai-stories-for-october-27-29-2026-physical-world-simulations-for-robotics"
data_notizia: "2026-10-29"
tags: ["AI", "open-weight", "LLM", "edge", "privacy", "Liquid AI", "locale"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: perfetto per il tema AI locale e privacy. I lettori di RobyRoot amano far girare roba in locale senza mandare dati al cloud. LFM3 con 1GB RAM abbassa la barriera d'ingresso in modo clamoroso — anche un Raspberry Pi o un vecchio laptop ci riesce. Aggiungi istruzioni pratiche con ollama o llama.cpp.
---

# Liquid AI LFM3: sei modelli AI open-weight che girano con 1GB di RAM

Se stai aspettando il momento giusto per iniziare a far girare un modello AI in locale, senza mandare le tue conversazioni a OpenAI o Anthropic, quel momento potrebbe essere arrivato. **Liquid AI** ha appena rilasciato **LFM3**, una famiglia di sei modelli open-weight da circa **2 miliardi di parametri**, e alcuni di loro girano con **appena 1GB di RAM**.

Hai letto bene. Un gigabyte.

## Cos'è Liquid AI e cosa sono i modelli LFM

Liquid AI è una startup americana che non usa i classici transformer (l'architettura alla base di GPT, LLaMA e praticamente tutti i grandi modelli). Usa invece le **Liquid Neural Networks** (LNN), ispirate ai sistemi nervosi biologici, e i cosiddetti **Liquid Foundation Models (LFM)**.

Il vantaggio teorico? Maggiore efficienza computazionale a parità di prestazioni, soprattutto per l'inferenza su hardware limitato. Con LFM3 sembrano aver mantenuto la promessa: sei varianti tutte attorno ai 2B di parametri, pensate per dispositivi edge, mobile e sistemi embedded.

## I sei modelli della famiglia LFM3

Liquid ha rilasciato varianti specializzate per diversi casi d'uso:

| Modello | Focus | RAM minima |
|---------|-------|-----------|
| LFM3-2B | Uso generale | ~2GB |
| LFM3-2B-Mini | Ultra-leggero | ~1GB |
| LFM3-2B-Code | Coding assistant | ~2GB |
| LFM3-2B-Chat | Conversazione | ~2GB |
| LFM3-2B-Instruct | Istruzioni/task | ~2GB |
| LFM3-2B-Edge | Ottimizzato ARM | ~1GB |

Tutti i modelli sono open-weight (i pesi sono scaricabili liberamente) e disponibili su Hugging Face. La licenza è permissiva per uso personale e ricerca — controlla i dettagli prima di usarli commercialmente.

## Prova in locale con Ollama

Il modo più semplice per provare LFM3 sul tuo Linux è usare **Ollama**, che gestisce download, quantizzazione e inferenza in modo trasparente:

```bash
# Installa Ollama (se non l'hai già)
curl -fsSL https://ollama.ai/install.sh | sh

# Scarica e avvia il modello (mini versione)
ollama run lfm3:2b-mini

# Oppure la versione per il coding
ollama run lfm3:2b-code
```

Se preferisci **llama.cpp** per avere più controllo:

```bash
# Clona e compila llama.cpp
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp
make -j$(nproc)

# Scarica il modello quantizzato (Q4_K_M è un buon equilibrio qualità/dimensione)
# I file .gguf sono disponibili su Hugging Face sotto liquid-ai/lfm3

./llama-cli -m ./models/lfm3-2b-mini-q4_k_m.gguf \
  -p "Spiega cosa è Wayland in 3 righe:" \
  -n 200
```

## Su quanti dispositivi gira davvero?

La promessa di "1GB di RAM" si riferisce alla versione quantizzata a 4-bit (Q4) del modello Mini. In pratica, funziona su:

- **Raspberry Pi 5** (4GB o 8GB RAM) — lento ma funziona
- **PC vecchi** con 4GB di RAM totale
- **Laptop entry-level** anche con hardware integrato
- **Android** tramite applicazioni come MLC Chat (supporto in arrivo)
- **Server ARM** come quelli di Oracle Free Tier

La velocità dipende molto dall'hardware. Su un modern laptop con CPU Intel/AMD dovresti aspettarti 5-20 token al secondo, abbastanza per uso interattivo. Su Raspberry Pi sarà più lento, ma rimane utilizzabile per elaborazione in batch.

## Perché questo è importante per la privacy

Far girare un modello AI in locale significa che **nessuna delle tue richieste lascia il tuo dispositivo**. Niente dati mandati a server americani, europei o cinesi. Niente training sui tuoi testi. Niente abbonamenti.

Per chi usa Linux proprio perché tiene alla propria privacy e alla propria autonomia digitale, questo è il punto. LFM3 abbassa la barriera così in basso che anche hardware modesto può partecipare.

Non sarà GPT-4o, questo è certo. Ma per molti compiti — riassumere testi, rispondere a domande, aiutare con il codice, tradurre — un modello da 2B parametri ben addestrato fa già un lavoro decente.

## Confronto con altri modelli open-weight di ottobre 2026

Ottobre è stato un mese ricchissimo per i modelli open-weight:

- **DeepSeek V4.1 Flash** (17 ott, MIT): performante ma richiede hardware serio
- **Reflection Beam 1.0** (5 ott, Apache 2.0): 501B parametri totali, impossibile in locale per i più
- **IBM Granite Switch 4.1 8B** (14 ott, Apache 2.0): ottimo per enterprise, più pesante
- **LFM3** (fine ottobre): il più accessibile della lista

Se il tuo obiettivo è AI locale senza investire in hardware dedicato, LFM3 è probabilmente la scelta più sensata del momento.

## Conclusione

Liquid AI LFM3 è un segnale chiaro di dove sta andando l'AI locale: modelli sempre più piccoli, sempre più capaci, su hardware sempre più comune. Se hai un Linux e vuoi provare cosa significa avere un assistente AI completamente sotto il tuo controllo, questo è il momento di farlo — e bastano pochissimi comandi.

Il cloud non è l'unica opzione. Non lo è mai stato.
