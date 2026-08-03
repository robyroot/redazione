---
title: "California Delete Act: da agosto 2026 un clic solo cancella i tuoi dati da centinaia di data broker"
rilevanza: "MEDIA"
fonte: "https://www.techtimes.com/articles/319927/20260708/california-drop-enforcement-hits-aug-1-data-brokers-face-200-per-day-fines.htm"
data_notizia: "2026-08-01"
tags: ["privacy", "data-broker", "california", "legislazione", "digital-rights"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: la notizia viene dagli USA ma è uno spunto perfetto per parlare di data broker (spesso sconosciuti al pubblico italiano), spiegare come funziona il GDPR per chi vive in Europa, e suggerire strumenti pratici per ridurre la propria esposizione. Sensibilizza senza essere allarmista.
---

## Prima di tutto: cosa sono i data broker

Hai mai cercato il tuo nome su Google e trovato siti come Spokeo, BeenVerified o Whitepages che mostravano il tuo indirizzo, numero di telefono, età e nome dei familiari? Ecco: quei siti sono gestiti da **data broker**.

I data broker sono aziende il cui unico scopo è raccogliere dati personali — da fonti pubbliche, social network, app, storico degli acquisti, registri immobiliari, dati di geolocalizzazione — e rivenderli a chiunque voglia comprarli. Agenzie di marketing, assicuratori, datori di lavoro, investigatori privati, ma anche truffatori.

Fino a poco tempo fa, togliersi da quei database era un calvario: contattare ogni singola azienda, compilare moduli diversi, aspettare settimane, e spesso venire semplicemente ignorati. In California ci sono oltre **600 data broker registrati**. Fare il giro di tutti sarebbe un lavoro a tempo pieno.

## La svolta: California Delete Act e la piattaforma DROP

Dal **1° agosto 2026**, le cose cambiano — almeno per chi vive in California.

La **California Delete Act** (SB 362), approvata nel 2023, ha raggiunto la sua fase operativa più importante. Attraverso la piattaforma **DROP** (Delete Request and Opt-Out Platform), creata dalla California Privacy Protection Agency (CPPA), bastano **pochi minuti e un singolo invio** per richiedere la cancellazione dei propri dati da tutti i data broker registrati nello stato.

I numeri fanno capire la portata della cosa:

- **600+ data broker** obbligati per legge a rispettare le richieste entro 45 giorni
- **260.000+ californiani** hanno già inviato la propria richiesta tramite DROP da quando la piattaforma è aperta (1° gennaio 2026)
- Chi non si adegua rischia **200 dollari di multa per ogni singola richiesta non evasa, ogni giorno**

La legge non scherza.

## Come funziona DROP in pratica

Gli utenti californiani accedono al portale della CPPA, compilano un modulo con i propri dati identificativi, verificano la propria identità, e la CPPA si occupa di trasmettere la richiesta di cancellazione a tutti i broker registrati. Fine. Nessuna email a 600 aziende diverse, nessun modulo ripetuto all'infinito.

Il limite ovvio è geografico: funziona solo per i residenti in California. Ma è un modello talmente pratico che il resto del mondo sta iniziando a guardarlo con molta attenzione.

## E in Europa? E in Italia?

La buona notizia per noi è che l'Europa ha già il **GDPR** dal 2018, che include all'articolo 17 il **diritto alla cancellazione** — tecnicamente più ampio di quello californiano. Il problema è che non esiste ancora una piattaforma centralizzata come DROP.

In pratica, se vuoi cancellare i tuoi dati dai principali data broker (molti dei quali operano anche in Europa), puoi:

1. **Cercare il form di opt-out** direttamente sul sito del data broker — quasi tutti ne hanno uno, di solito nascosto nel footer alla voce "Privacy" o "Do Not Sell My Data"
2. **Inviare una richiesta GDPR formale** per e-mail, che obbliga l'azienda a risponderti entro 30 giorni

```bash
# Template rapido per richiesta di cancellazione GDPR (copia e adatta)
cat << 'EOF'
Oggetto: Richiesta di cancellazione dei dati personali - Art. 17 GDPR

Gentili Signori,
in qualità di interessato, esercito il diritto alla cancellazione dei miei
dati personali ai sensi dell'articolo 17 del Regolamento UE 2016/679 (GDPR).

Dati relativi a: [NOME COGNOME], [DATA DI NASCITA], [EMAIL], [INDIRIZZO]

Vi chiedo di cancellare tutti i dati personali che mi riguardano e di
confermare l'avvenuta cancellazione entro 30 giorni dalla presente.

Cordiali saluti
[FIRMA]
EOF
```

3. **Usare servizi come Privacy Bee o DeleteMe** — automatizzano il processo contattando decine di data broker per conto tuo (servizi a pagamento, ma fanno risparmiare ore di lavoro)
4. **Segnalare al Garante Privacy** se un'azienda ignora la tua richiesta: [garante.it](https://www.garanteprivacy.it)

## Perché questa notizia conta anche per noi

Il fatto che la California abbia creato una piattaforma centralizzata è un segnale importante. Quando un mercato da 40 milioni di persone inizia a regolamentare i data broker in modo serio, le aziende del settore sono costrette ad adeguarsi anche altrove — pena perdere l'accesso al mercato californiano.

L'ideale sarebbe un DROP europeo, gestito dall'EDPB (il comitato europeo per la protezione dei dati). Non esiste ancora, ma non sarebbe male farlo presente ai propri rappresentanti al Parlamento Europeo.

Nel frattempo, il consiglio pratico è semplice: ogni tanto cercati su Google, guarda cosa viene fuori, e manda qualche richiesta di cancellazione. Non ci vuole molto e fa la differenza.
