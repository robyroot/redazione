---
title: "EU AI Act: dal 2 agosto scatta l'enforcement — cosa cambia per chi usa o distribuisce AI open source"
rilevanza: "ALTA"
fonte: "https://linuxfoundation.eu/newsroom/ai-act-explainer"
data_notizia: "2026-07-20"
tags: ["ai", "open-source", "privacy", "europa", "regolamentazione", "sviluppatori", "GDPR"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Guida pratica per sviluppatori e aziende italiane. L'AI Act è percepito come qualcosa di lontano — questa scadenza di agosto è concreta e immediata. Focus su cosa devono fare (o non fare) chi usa modelli open-weight o sviluppa strumenti AI.
---

# EU AI Act: dal 2 agosto scatta l'enforcement — cosa cambia per chi usa o distribuisce AI open source

Fra dieci giorni, il **2 agosto 2026**, scatta la fase più importante dell'AI Act europeo: la Commissione UE acquisisce i pieni poteri di enforcement. Non è una scadenza astratta — significa che da quel giorno le sanzioni possono essere comminate, raggiungendo fino a **35 milioni di euro o il 7% del fatturato globale** (superando persino il GDPR).

Se sviluppi software con componenti AI, usi modelli open source in produzione, o gestisci sistemi che prendono decisioni automatizzate, questa scadenza ti riguarda.

## Cosa scatta il 2 agosto

Dal 2 agosto 2026 diventano vincolanti:

- Le **obbligazioni di trasparenza** per i sistemi AI generativi (obbligo di dichiarare che il contenuto è generato da AI)
- Le regole sui **modelli GPAI** (General-Purpose AI) ad alto rischio sistemico
- I requisiti per i **sistemi AI ad alto rischio** in settori come salute, credito, HR e infrastrutture critiche
- Le **responsabilità di documentazione tecnica** per chi sviluppa e distribuisce modelli

C'è un'eccezione temporanea: i sistemi AI generativi già sul mercato prima del 2 agosto hanno tempo fino al **2 dicembre 2026** per conformarsi al requisito di marcatura leggibile automaticamente (machine-readable marking).

## L'esenzione open source: più limitata di quanto pensi

La parte che più interessa la comunità Linux e open source riguarda le esenzioni. L'AI Act riconosce il valore dell'open source e prevede alcune eccezioni per i provider di modelli AI rilasciati sotto licenza libera, **ma con condizioni precise**.

Perché un modello sia considerato "open source" ai fini dell'AI Act, la licenza deve consentire di **accedere, usare, modificare e redistribuire** liberamente pesi del modello, architettura e parametri. Fin qui sembra semplice. Ma ci sono due aspetti critici da conoscere:

**1. La licenza Llama di Meta non è riconosciuta come "free and open"**

L'AI Office UE ha esaminato la licenza di Meta per i modelli Llama e ha stabilito che **non soddisfa i criteri** per l'esenzione open source, principalmente perché contiene restrizioni commerciali e di uso. Se usi Llama in produzione convinto di essere "open source" e quindi esente — devi rivedere la valutazione.

**2. L'esenzione non si applica in contesti ad alto rischio**

Anche se un modello ha una licenza genuinamente libera, l'esenzione decade se il modello viene usato in contesti classificati come "alto rischio" dall'AI Act: selezione del personale, concessione di credito, diagnostica medica, infrastrutture critiche, sistemi educativi. In questi casi si applicano tutti i requisiti completi, indipendentemente dalla licenza.

## Cosa devi fare se usi modelli open-weight

Se usi modelli come **DeepSeek V4, GLM-5.2, Mistral, Falcon** o simili in applicazioni reali, ecco cosa verificare:

**Contesto a basso rischio (chatbot interno, assistente per documentazione, strumenti creativi):**
Probabilmente non hai obbligazioni dirette come deployer, ma devi comunque:
- Dichiarare all'utente finale che sta interagendo con un sistema AI
- Non usare il sistema per decisioni automatizzate su persone senza supervisione umana
- Tenerti aggiornato sulle linee guida del tuo paese (l'Italia applica l'AI Act tramite l'AGID)

**Contesto ad alto rischio (HR, credito, salute, infrastrutture):**
Servono: documentazione tecnica del sistema, valutazione della conformità, registrazione nel database UE dei sistemi AI ad alto rischio, supervisione umana sui risultati.

**Se distribuisci un modello o uno strumento AI ad altri:**
Sei considerato "provider" e hai obblighi più pesanti: trasparenza sul training data, politica di compliance al copyright, documentazione tecnica aggiornata.

## Cosa NON è richiesto (per ora) agli sviluppatori indie

Chiariamo anche cosa non ti si chiede se sei uno sviluppatore individuale o una piccola azienda che usa AI in contesti a basso rischio:

- Non devi registrarti in alcun database UE per uso interno non ad alto rischio
- Non hai obblighi di audit di terze parti per sistemi non ad alto rischio
- Usare strumenti come GitHub Copilot, Cursor o assistant locali con Ollama per il tuo lavoro quotidiano non richiede conformità diretta all'AI Act (è il provider dello strumento ad avere gli obblighi)

## Come prepararsi nei prossimi 10 giorni

Se stai usando AI in produzione e non hai ancora fatto una valutazione:

```bash
# Una lista di controllo minima
# 1. Identifica tutti i componenti AI nei tuoi prodotti
# 2. Classifica il contesto d'uso (basso/alto rischio AI Act)
# 3. Verifica la licenza dei modelli che usi
# 4. Controlla se mostri all'utente che sta interagendo con AI
# 5. Documenta le decisioni principali del sistema
```

Per i sistemi più critici, la Commissione ha pubblicato linee guida pratiche per i provider di modelli GPAI sul sito ufficiale digital-strategy.ec.europa.eu. La Linux Foundation EU ha anche una guida specifica per gli sviluppatori open source.

## Il quadro d'insieme

L'AI Act non è il GDPR versione 2026: è più complesso, più sfumato e con molte più zone grigie. Per la comunità open source, il messaggio principale è che **l'esenzione esiste ma non è automatica** — dipende dalla licenza, dal contesto e dall'uso finale. Chi distribuisce modelli AI come parte di un prodotto commerciale deve prendere sul serio la scadenza di agosto.

Per chi usa AI come strumento di produttività personale o sviluppo interno, l'impatto diretto è limitato. Ma conoscere le regole è il primo passo per non ritrovarsi a dover correre ai ripari in seguito.
