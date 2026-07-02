---
title: "Da ieri è illegale usare i tuoi dati per addestrare AI senza dirtelo: la legge USA che cambia le regole"
rilevanza: "ALTA"
fonte: "https://edri.org/our-work/edri-gram-1-july-2026/"
data_notizia: "2026-07-01"
tags: ["privacy", "AI", "legge", "dati-personali", "USA", "CTDPA"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: spiegare in modo chiaro cosa cambia con il CTDPA
  aggiornato (Connecticut), il requisito di disclosure per l'addestramento AI, e
  cosa significa per gli utenti italiani che usano servizi americani. Tono pratico
  e orientato all'azione: cosa controllare, cosa chiedere ai servizi che usi.
---

# Da ieri è illegale usare i tuoi dati per addestrare AI senza dirtelo: la legge USA che cambia le regole

Dal 1° luglio 2026 negli Stati Uniti è scattata una nuova ondata di leggi sulla privacy, e una delle più significative riguarda direttamente l'intelligenza artificiale: in Connecticut, le aziende sono obbligate per legge a **dichiararti esplicitamente se usano i tuoi dati personali per addestrare modelli linguistici** come ChatGPT, Gemini, DeepSeek o Grok.

Non è solo una formalità tecnica. È il primo obbligo legale di questo tipo negli USA, e potrebbe influenzare come vengono scritte le privacy policy di molti servizi che usiamo ogni giorno — anche dall'Italia.

## Cosa dice esattamente la legge

Il Connecticut Data Privacy Act (CTDPA) è stato aggiornato con emendamenti che entrano in vigore oggi, 1° luglio 2026. Le novità principali per il mondo AI:

**Disclosure obbligatoria sull'addestramento AI**: se un'azienda usa i tuoi dati personali per addestrare LLM (Large Language Models), deve dichiararlo in modo "chiaro e ben visibile" nella propria privacy policy. Non basta una nota in fondo alla pagina scritta in legalese — deve essere esplicito.

**I dati neurali diventano "dati sensibili"**: il Connecticut inserisce per la prima volta i **dati neurali** (informazioni sull'attività cerebrale, raccolte da dispositivi come EEG o interfacce neurali) nella categoria dei dati sensibili, che richiedono consenso esplicito (opt-in) per essere raccolti. Con l'avanzare dei dispositivi BCI (Brain-Computer Interface), è una mossa lungimirante.

**Diritto di correzione**: gli utenti possono ora richiedere la correzione di dati personali inaccurati detenuti dalle aziende — non solo la cancellazione, ma la rettifica.

## Perché conta anche per noi italiani

"Ma io vivo in Italia, non in Connecticut" — pensiero legittimo. Il punto è che le grandi piattaforme tech americane servono utenti in tutto il mondo, e spesso adottano gli standard più restrittivi come baseline globale, esattamente come è successo con il GDPR europeo.

Quando il GDPR è entrato in vigore nel 2018, ha cambiato le privacy policy di praticamente tutti i servizi online globali, non solo quelli europei. La stessa dinamica potrebbe ripetersi: se Meta, Google o OpenAI devono dichiarare agli utenti del Connecticut che usano i loro dati per addestrare AI, probabilmente aggiorneranno le loro policy globali.

Inoltre, se sei cliente di un'azienda americana che ha clienti in Connecticut, quella policy ti riguarda.

## Come controllare se i tuoi dati finiscono nel training AI

Ecco alcune azioni pratiche che puoi fare subito:

**1. Controlla le impostazioni di ogni servizio AI che usi**

La maggior parte dei grandi player ha già un'opzione per escludersi dal training:

- **ChatGPT (OpenAI)**: Impostazioni → Controlli dati → "Migliora i modelli per tutti"
- **Google Gemini**: myaccount.google.com → Dati e privacy → Attività web e app
- **Meta AI**: Centro gestione account → Il tuo uso delle informazioni per l'AI

**2. Leggi (davvero) la privacy policy**

Con la nuova disclosure obbligatoria, dovresti trovare una sezione specifica sull'uso per il training AI. Se non c'è, o è vaga, è un segnale.

**3. Usa servizi self-hosted quando possibile**

La scelta più radicale: usare modelli AI in locale (Ollama, LM Studio) che non inviano nulla a server esterni:

```bash
# Installa Ollama per eseguire modelli AI in locale
curl -fsSL https://ollama.com/install.sh | sh

# Scarica e usa un modello senza inviare dati a nessuno
ollama pull llama3.2
ollama run llama3.2
```

## Il quadro più ampio: 20 nuove leggi privacy USA nel 2026

Il Connecticut non è solo. Nel 2026 sono entrate in vigore **20 leggi statali sulla privacy** negli USA, con Arkansas e Utah che aggiungono nuovi diritti degli utenti proprio da luglio. Il clima di enforcement è descritto come "il più aggressivo della storia USA" — con l'FTC che ha intensificato i procedimenti contro le violazioni della privacy.

Parallelamente, l'Europa sta lavorando all'**Euro digitale** come alternativa ai sistemi di pagamento controllati da aziende USA, anche per ridurre la dipendenza tecnologica extraeuropea.

## Cosa aspettarsi nei prossimi mesi

Le aziende hanno già iniziato ad aggiornare le loro policy in risposta a questi nuovi obblighi. Aspettati email di notifica cambio policy da molti servizi nelle prossime settimane — leggile, non cliccare solo "accetto".

Per chi vuole restare aggiornato, il sito di **EDRi (European Digital Rights)** pubblica un digest settimanale in inglese con le novità legislative sulla privacy digitale, ed è una delle fonti più affidabili sull'argomento.
