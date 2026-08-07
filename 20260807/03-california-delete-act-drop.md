---
title: "Il California Delete Act è operativo: finalmente puoi cancellare i tuoi dati dai broker"
rilevanza: "MEDIA"
fonte: "https://calmatters.org/economy/technology/2026/01/californians-block-personal-data/"
data_notizia: "2026-08-01"
tags: ["privacy", "data-broker", "California", "GDPR", "diritti-digitali"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: anche se è legge californiana, è la prima legge al mondo di questo tipo e apre il dibattito su cosa dovrebbe fare l'Europa (e l'Italia) in ambito data broker. Utile per spiegare cosa sono i data broker, come operano, e perché una legge simile sarebbe necessaria anche da noi. Tono pratico con un occhio alle implicazioni globali.
---

# Il California Delete Act è operativo: finalmente puoi cancellare i tuoi dati dai broker

Dal primo agosto 2026, i broker di dati californiani sono obbligati per legge a processare le richieste di cancellazione dei dati personali attraverso un portale centralizzato gestito dallo Stato. Si chiama **DROP** — Delete Request and Opt-Out Platform — ed è la prima iniziativa del genere al mondo.

Stai pensando "ma io non sono californiano"? Continua a leggere lo stesso: questa legge riguarda tutti, anche chi vive in Italia.

## Cosa sono i broker di dati

Prima di tutto, un passo indietro. I **data broker** sono aziende che raccolgono dati personali su di te — nome, indirizzo, numero di telefono, interessi, abitudini di acquisto, reddito stimato, relazioni, storico medico — e li vendono a chiunque voglia comprarli: assicurazioni, datori di lavoro, agenzie di marketing, investigatori privati, e a volte soggetti meno raccomandabili.

Non hai mai firmato niente con loro. Non sai chi sono. Ma esistono centinaia di aziende che hanno profili dettagliati su di te, costruiti aggregando dati pubblici, dati trapelati da breach, dati comprati da app che hai installato, e molto altro.

In California sono registrati **oltre 500 broker di dati**.

## Come funziona DROP

Prima del Delete Act, chi voleva rimuovere i propri dati da questi archivi doveva contattare **ogni singola azienda separatamente** — compilare moduli diversi, aspettare risposte diverse, ripetere il processo ogni anno perché i dati venivano reinseriti. Un calvario progettato per scoraggiare.

Con DROP, basta una singola richiesta:

1. L'utente va sul portale di CalPrivacy
2. Invia una richiesta di cancellazione
3. DROP la trasmette automaticamente a tutti i broker registrati
4. I broker hanno 45 giorni per processarla e rispondere

Dal primo agosto, i broker devono accedere a DROP almeno ogni 45 giorni, recuperare le richieste pendenti, e processarle. Chi non lo fa rischia **200 dollari al giorno** per ogni violazione — la multa è stata raddoppiata rispetto all'impostazione originale della legge.

## E chi non vive in California?

Qui sta il punto interessante per noi europei. Molti dei broker di dati che operano in California hanno profili su persone in tutto il mondo — inclusa l'Italia. Il meccanismo DROP non vale formalmente per i non-residenti in California, ma:

**1. Alcune aziende si adeguano globalmente** per semplicità operativa — è più facile cancellare tutti piuttosto che fare distinzioni geografiche.

**2. Il GDPR già dovrebbe proteggerci**, almeno sulla carta. Il diritto alla cancellazione (Art. 17 GDPR) esiste, ma richiede di sapere chi ha i tuoi dati e di contattarli uno per uno. Manca uno strumento equivalente a DROP.

**3. La pressione regolamentare cresce**: il Delete Act californiano è il modello che altri stati americani e potenzialmente l'UE guarderanno per costruire leggi simili.

## Come proteggersi adesso, anche senza DROP

In attesa che l'Europa si svegli, alcune cose puoi farle già oggi:

```bash
# Usa Have I Been Pwned per capire se i tuoi dati sono già trapelati
curl -s "https://haveibeenpwned.com/api/v3/breachedaccount/la-tua@email.it" \
  -H "hibp-api-key: TUO_API_KEY"
```

Per i servizi europei, puoi esercitare il diritto GDPR direttamente:
- Scrivere all'azienda richiedendo copia dei tuoi dati (Art. 15)
- Chiedere la cancellazione (Art. 17)
- Segnalare al Garante Privacy italiano se l'azienda non risponde

Strumenti come **Jumbo Privacy**, **DeleteMe** (a pagamento) o il progetto open source **Privacy Bot** automatizzano parzialmente questo processo.

## Il quadro più grande

Il Delete Act californiano dimostra che i governi possono effettivamente costringere i broker di dati a essere accountable. Non è la soluzione definitiva — i dati vengono ricreati continuamente — ma è un passo concreto nella direzione giusta.

In Italia e in Europa, la conversazione su come rendere il GDPR effettivamente applicabile nei confronti dei data broker è ancora troppo timida. Speriamo che il modello californiano acceleri qualcosa anche da questa parte dell'Atlantico.
