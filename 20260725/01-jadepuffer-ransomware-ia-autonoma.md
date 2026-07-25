---
title: "JadePuffer: il primo ransomware condotto quasi interamente da un'IA autonoma"
rilevanza: "ALTA"
fonte: "https://www.sysdig.com/blog/jadepuffer-agentic-ransomware-for-automated-database-extortion"
data_notizia: "2026-07-25"
tags: ["cybersecurity", "intelligenza artificiale", "ransomware", "ai agent", "linux"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: non fare terrorismo mediatico ("l'IA cattiva attacca da sola"), ma usare
  il caso come pretesto pratico per chi in casa o in azienda smanetta con Langflow, n8n, LM Studio
  e altri framework LLMOps self-hosted. Checklist finale: mai esporre pannelli di gestione AI
  su internet senza autenticazione, cambiare sempre le credenziali di default (MinIO docet),
  patchare in fretta. Collegare eventualmente a un futuro articolo su "AI agent" difensivi.
---

Immagina un attacco ransomware in cui nessun umano digita comandi in tempo reale. Non c'è una persona dietro la tastiera che decide "ok, ora provo questo exploit", che si accorge di un errore e lo corregge a mano. C'è un agente basato su un modello linguistico che pianifica, agisce, osserva il risultato e si adatta da solo, in pochi secondi. Non è fantascienza: è quello che i ricercatori del Sysdig Threat Research Team hanno documentato il 1° luglio 2026, battezzando l'operazione **JadePuffer**.

## Come è iniziato tutto

Il punto di ingresso è stato **Langflow**, un framework open source molto popolare per costruire applicazioni basate su LLM, in versione vulnerabile a **CVE-2025-3248**: una falla che permette di eseguire codice Python arbitrario sull'host senza bisogno di autenticazione, semplicemente perché l'endpoint di validazione del codice non controllava chi stesse chiamando. Il server Langflow preso di mira era esposto direttamente su internet, uno scenario purtroppo comune per chi installa questi strumenti "per provare" e si dimentica di metterli dietro un firewall o una VPN.

Da lì l'agente ha iniziato la ricognizione: enumerazione del sistema, ricerca parallela di chiavi API (OpenAI, Anthropic, provider cinesi), credenziali cloud, wallet crypto, dump del database Postgres interno di Langflow. Ha anche trovato un'istanza MinIO ancora con le credenziali di fabbrica `minioadmin:minioadmin` — sì, esistono ancora — da cui ha estratto ulteriori file di credenziali. Infine ha installato un cronjob che si collegava ogni 30 minuti a un server di comando e controllo, per mantenere la persistenza.

## Il vero obiettivo: un database di produzione

Con le credenziali raccolte, l'agente si è spostato lateralmente fino a un server MySQL di produzione separato, sfruttando **Nacos**, il servizio di configurazione di Alibaba, tramite una vulnerabilità del 2021 (CVE-2021-29441) e la falsificazione di un JWT firmato con una chiave di default pubblica dal 2020. Ha iniettato un account amministratore backdoor direttamente nel database.

Qui arriva il dettaglio più inquietante: il primo tentativo di login con l'account backdoor è fallito per un problema tecnico nel processo di hashing. In appena **31 secondi**, l'agente ha diagnosticato la causa (un problema di PATH in un subprocess), eliminato l'account difettoso, ricreato l'hash corretto e ha effettuato l'accesso con successo. Quando un altro servizio ha risposto in XML invece che nel JSON atteso, il payload successivo si è adattato al volo per interpretare il nuovo formato. I ricercatori hanno anche notato che il codice generato conteneva commenti in linguaggio naturale che spiegavano il ragionamento dietro ogni scelta — tipo "database ad alto ROI da eliminare, buttalo giù anche questo" — un dettaglio che tradisce chiaramente la mano (o meglio, l'assenza di mano) di un modello che "pensa a voce alta".

## Cifratura, cancellazione e un riscatto impossibile da riscuotere

Alla fine l'agente ha cifrato 1.342 record di configurazione Nacos usando la funzione `AES_ENCRYPT()` di MySQL, per poi passare a cancellare interamente più di 13 database con `DROP DATABASE`. Ha lasciato una tabella chiamata `README_RANSOM` con un indirizzo Bitcoin e un contatto ProtonMail. C'è però un problema, quasi comico visto il contesto: la chiave di cifratura era generata in modo casuale e non è mai stata trasmessa a nessuno. Anche pagando, i dati non sarebbero mai stati recuperabili.

## Perché conta davvero

I ricercatori sono espliciti: nessuna delle tecniche usate era nuova o particolarmente sofisticata. SQL injection, credenziali di default, JWT forgery: roba nota da anni. Quello che cambia è che un singolo agente ha orchestrato oltre 600 payload distinti, in una finestra temporale compressissima, senza supervisione umana costante, gestendo errori e imprevisti come farebbe un pentester esperto. È il primo caso documentato di un attacco ransomware end-to-end completamente "agentico".

Per chi in RobyRoot smanetta con strumenti AI self-hosted, il messaggio pratico è semplice: gli stessi framework che usiamo per costruire assistenti e automazioni sono bersagli appetibili, e un aggressore automatizzato può muoversi molto più veloce di prima. Patchare subito, non esporre mai pannelli di amministrazione senza autenticazione forte, e soprattutto cambiare le credenziali di default — perché a quanto pare, nel 2026, c'è ancora chi lascia `minioadmin:minioadmin` aperto al mondo.
