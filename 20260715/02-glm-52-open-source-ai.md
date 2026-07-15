---
title: "GLM-5.2: l'AI open source con licenza MIT che finalmente sfida i modelli proprietari"
rilevanza: "ALTA"
fonte: "https://llm-stats.com/llm-updates"
data_notizia: "2026-06-13"
tags: ["AI", "open-source", "LLM", "GLM", "machine-learning", "privacy"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: sottolineare il valore della licenza MIT e della possibilità di
  eseguire modelli potenti localmente o con costi bassissimi. Parlare di sovranità digitale e
  privacy nell'uso dell'AI. Includere comandi per provare il modello via CLI o API.
---

# GLM-5.2: l'AI open source con licenza MIT che finalmente sfida i modelli proprietari

Per anni abbiamo sentito dire che i modelli AI open source erano "quasi buoni quanto quelli proprietari". Poi arrivava il benchmark e il gap era ancora lì, abbastanza grande da giustificare l'abbonamento mensile a qualche servizio cloud. Oggi, con **GLM-5.2**, quella distanza si è ridotta a un punto percentuale su alcuni test. E il modello ha licenza MIT.

Questo cambia tutto.

## Cosa rende GLM-5.2 speciale

GLM-5.2 è sviluppato dal team di **THUDM (Tsinghua University)** ed è stato rilasciato il 13 giugno 2026 con licenza **MIT** — la più permissiva possibile, senza restrizioni commerciali o clausole strane. Puoi usarlo, modificarlo, distribuirlo e integrarlo nei tuoi prodotti liberamente.

I numeri parlano chiaro:
- **GPQA Diamond: 91.2%** — un benchmark che misura la capacità di rispondere a domande di livello PhD in scienze
- **Contesto da 1 milione di token** — puoi passargli libri interi, codebase enormi, documenti lunghissimi
- **SWE-bench Pro: 62.1%** — misura la capacità di risolvere problemi reali di programmazione

Per confronto, il miglior modello proprietario attuale si attesta all'80.3% su SWE-bench Pro. Il gap è di 18 punti, sì — ma su GPQA Diamond e su altri benchmark la distanza è diventata di singole cifre percentuali.

## Il prezzo cambia la conversazione

GLM-5.2 tramite API costa **$1.40 per milione di token in input**. Per uso personale o piccoli progetti, questo significa costi praticamente irrisori. Ma la cosa davvero rivoluzionaria è che puoi **scaricarlo e farlo girare in locale**.

Niente abbonamento. Niente dati che escono dalla tua macchina. Niente dipendenza da un'azienda che può cambiare i prezzi o chiudere domani.

## Come provarlo subito

Se hai un sistema con GPU decente (o tanta pazienza con la CPU), puoi usarlo tramite Ollama:

```bash
# Installa Ollama se non ce l'hai
curl -fsSL https://ollama.ai/install.sh | sh

# Scarica e avvia GLM-5.2 (attenzione: diversi GB)
ollama run glm5.2

# Oppure usa la versione quantizzata più leggera
ollama run glm5.2:q4_k_m
```

In alternativa, puoi interrogarlo tramite API con un costo minimo:

```bash
curl -s https://api.zhipuai.cn/api/paas/v4/chat/completions \
  -H "Authorization: Bearer $ZHIPUAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "glm-5-2",
    "messages": [{"role": "user", "content": "Spiega il TCP/IP handshake in 3 righe"}]
  }'
```

## Il contesto: una svolta per l'AI open source

Mettendo GLM-5.2 in prospettiva: da aprile a giugno 2026 sono usciti cinque modelli open weight di prima fascia (DeepSeek V4 Pro, Kimi K2.6, Kimi K2.7 Code, GLM-5.2, MiniMax M3). In sei mesi, il panorama è cambiato radicalmente.

Il significato pratico per chi usa Linux e vuole mantenere il controllo sui propri dati è enorme. Finché i modelli open source erano notevolmente peggiori, si poteva giustificare l'uso di servizi proprietari per compiti complessi. Ora quella giustificazione si assottiglia ogni mese.

## Privacy e sovranità digitale

Eseguire un LLM in locale con GLM-5.2 significa:
- I tuoi prompt non vengono inviati a server di terze parti
- Nessun dato di addestramento raccolto dalle tue conversazioni
- Funziona offline
- Zero costi ricorrenti dopo il download

Per chi lavora con dati sensibili — documenti aziendali, codice proprietario, informazioni personali — questa è la differenza tra scegliere la convenienza e scegliere la privacy.

Il futuro dell'AI locale e privata si sta costruendo adesso, e GLM-5.2 con licenza MIT è uno dei mattoni più solidi che siano stati posati finora.
