---
title: "Inkling: Mira Murati rilascia il primo modello AI open-weight di Thinking Machines Lab"
rilevanza: "MEDIA"
fonte: "https://techcrunch.com/2026/07/15/thinking-machines-amps-up-its-bet-against-one-size-fits-all-ai-with-its-first-open-model-inkling/"
data_notizia: "2026-07-16"
tags: ["ai", "open-source", "llm", "mira-murati", "thinking-machines"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: contestualizzare chi e Mira Murati (ex CTO OpenAI) per chi non segue il
  settore da vicino, e spiegare la differenza tra "open-weight" e "open-source" in modo semplice
  (i pesi si possono scaricare e modificare, ma il codice/training pipeline restano proprietari).
  Interessante anche il modello di business via Tinker: nessuno e obbligato a pagare per usare il
  modello scaricato, il ricavo arriva dagli strumenti di fine-tuning. Buon gancio per un pubblico
  italiano interessato ad AI ma non necessariamente addetto ai lavori.
---

Se segui il mondo dell'intelligenza artificiale anche solo da lontano, il nome Mira Murati probabilmente ti dice qualcosa: è stata la Chief Technology Officer di OpenAI fino al settembre 2024, prima di lasciare l'azienda per fondare una startup tutta sua, **Thinking Machines Lab**, con un round di finanziamento iniziale da 2 miliardi di dollari e una valutazione di 12 miliardi. Mercoledì 15 luglio 2026, dopo un anno e mezzo passato a costruire infrastrutture lontano dai riflettori, l'azienda ha finalmente presentato il suo primo modello: si chiama **Inkling**, ed è **open-weight**, cioè scaricabile e modificabile da chiunque.

## Cosa significa "open-weight" (e perché non è la stessa cosa di "open-source")

Prima di entrare nei dettagli tecnici, vale la pena chiarire un punto che genera spesso confusione. Quando un modello è open-weight, significa che i suoi **pesi** — cioè i numeri che rappresentano tutto ciò che il modello ha "imparato" durante l'addestramento — sono pubblicamente scaricabili, ad esempio su Hugging Face. Questo è molto diverso dai modelli di OpenAI, Anthropic o Google, che restano accessibili solo tramite API a pagamento, senza possibilità di scaricarli o eseguirli sul proprio hardware. Non è però detto che tutto il codice di addestramento o la pipeline di dati siano altrettanto aperti: per questo si preferisce parlare di "open-weight" piuttosto che di "open-source" in senso stretto.

## Le specifiche tecniche di Inkling

Inkling è un modello di tipo **mixture-of-experts** con 975 miliardi di parametri totali, di cui però solo circa 41 miliardi vengono effettivamente attivati per ogni singola richiesta — un'architettura che permette di avere un modello enorme mantenendo costi di calcolo ragionevoli. È stato addestrato su 45 trilioni di token che comprendono testo, immagini, audio e video, e riesce a **ragionare nativamente su tutte e quattro le modalità** contemporaneamente, anche se per ora produce solo output testuali (incluso codice).

Un dettaglio che Thinking Machines sottolinea con orgoglio è l'efficienza: secondo l'azienda, Inkling raggiunge le stesse prestazioni di coding di Nvidia Nemotron 3 Ultra usando solo **un terzo dei token**. Il modello è stato addestrato interamente su cluster Nvidia GB300 NVL72, frutto di una partnership con Nvidia risalente al marzo 2024.

Una caratteristica particolare, e piuttosto rara nel panorama attuale, è che Inkling è progettato per dare **risposte calibrate**: invece di "sparare" sempre una risposta con sicurezza assoluta anche quando non la sa, il modello segnala esplicitamente l'incertezza. Gli utenti possono anche regolare quanto "sforzo di ragionamento" applicare a ogni richiesta, bilanciando velocità e accuratezza.

## Una strategia diversa dai big del settore

Quello che rende interessante questo lancio non è tanto il modello in sé — Thinking Machines ammette apertamente che Inkling **non è il modello più forte sul mercato**, né aperto né chiuso — quanto la scommessa di fondo dell'azienda. L'idea è che l'IA su misura, affinata dalle organizzazioni per i propri bisogni specifici, alla lunga batterà i modelli "taglia unica" venduti dai grandi laboratori. A supporto di questa tesi, Thinking Machines cita uno studio con **Bridgewater Associates**: un modello open-source affinato con la loro competenza finanziaria ha raggiunto l'84,7% su test di ragionamento finanziario, superando modelli proprietari di punta e costando circa **un quattordicesimo** da eseguire.

## Come guadagna un'azienda che regala i pesi del modello?

Qui sta forse l'aspetto più interessante dal punto di vista del business. Una volta scaricati i pesi di Inkling, nessuno è tecnicamente obbligato a pagare Thinking Machines per usarli — a differenza dell'accesso a consumo di OpenAI o Anthropic. Il ricavo arriva invece da **Tinker**, la piattaforma proprietaria per il fine-tuning, oltre a una quota dell'ecosistema di hosting che si costruirà attorno al modello. Un po' come Red Hat nel mondo Linux: il prodotto di base è libero, il valore aggiunto (strumenti, supporto, infrastruttura) si paga.

## Perché interessa anche a chi non fa AI di mestiere

Con circa 200 dipendenti, Thinking Machines si posiziona come una delle poche realtà capaci di sfidare i colossi del settore puntando sull'apertura invece che sulla chiusura. Per sviluppatori italiani, ricercatori o semplici curiosi, Inkling è un'altra opzione che si aggiunge ai modelli cinesi open-weight (Qwen, Kimi, DeepSeek) che negli ultimi mesi hanno riempito le classifiche di benchmark. Vale la pena tenerlo d'occhio, soprattutto se lavori con dati sensibili e preferisci eseguire un modello sui tuoi server invece di affidarti a un'API esterna.
