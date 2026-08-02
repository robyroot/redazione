---
title: "Ernst & Young nel mirino di ShinyHunters: un fornitore compromesso apre le porte a Jira, GitHub e Azure"
rilevanza: "ALTA"
fonte: "https://www.bleepingcomputer.com/news/security/ernst-and-young-data-breach-claimed-by-shinyhunters-extortion-gang/"
data_notizia: "2026-08-02"
tags: ["cybersecurity", "data breach", "supply chain attack", "privacy"]
livello: "beginner"
nota_editoriale: |
  Angolo per RobyRoot: usare questo caso per spiegare in modo semplice cos'è un "supply chain
  attack" e perché rubare le credenziali di un fornitore terzo può valere quanto bucare
  direttamente l'azienda bersaglio. Buon gancio anche per parlare di igiene delle credenziali
  (secret rotation, MFA, accessi di terze parti) rivolto a chi gestisce anche solo un piccolo
  team o un'infrastruttura personale.
---

C'è una frase che nella cybersecurity si sente ripetere sempre più spesso: "non basta essere sicuri tu, deve esserlo anche chi ti sta intorno". Il caso di Ernst & Young (EY), una delle quattro grandi società di revisione e consulenza al mondo (le famose "Big Four"), è l'ultimo promemoria in ordine di tempo di quanto questa frase sia vera.

Il gruppo di estorsione **ShinyHunters** — nome che gli appassionati di sicurezza informatica conoscono bene, avendo già colpito decine di aziende negli ultimi anni — ha rivendicato un attacco a EY, sostenendo di aver ottenuto le credenziali di accesso ad alcuni sistemi dell'azienda **non colpendo direttamente EY, ma attraverso un attacco alla sua supply chain**, cioè alla catena di fornitori e servizi terzi che l'azienda utilizza.

Secondo quanto ricostruito, EY aveva già dichiarato in precedenza una violazione riguardante un sistema di ticket di supporto usato dal proprio personale IT, gestito da terze parti: gli attaccanti avrebbero avuto accesso alla piattaforma tra fine marzo e metà aprile, scaricando diversi documenti che potrebbero contenere informazioni fiscali dei clienti — nomi, indirizzi, codici fiscali, numeri di conto e di carte di credito/debito usati per le pratiche di dichiarazione dei redditi.

Ora ShinyHunters rilancia, affermando che le credenziali ottenute in quell'occasione avrebbero permesso l'accesso ad ambienti ben più delicati: **Jira** (lo strumento di gestione progetti usato da praticamente ogni team tech), **GitHub** (dove finiscono repository di codice, a volte con segreti e configurazioni sensibili) e **Azure**, l'infrastruttura cloud di Microsoft. Il gruppo ha inserito EY nel proprio sito di data leak sul dark web, minacciando di pubblicare tutto il materiale rubato se l'azienda non li avesse contattati entro il 31 luglio. Va detto, per correttezza, che EY non ha confermato la responsabilità di ShinyHunters né l'effettivo accesso a Jira, GitHub e Azure — le rivendicazioni dei gruppi di estorsione, per quanto spesso fondate, non sono automaticamente prove.

**Perché questa storia conta più della singola azienda coinvolta.** Il punto centrale non è "EY è stata bucata", ma *come*: attraverso credenziali rubate a un fornitore terzo che gestiva un servizio di supporto. È lo schema classico del supply chain attack, lo stesso che ha reso celebri casi come SolarWinds: invece di attaccare frontalmente un bersaglio con difese solide, si punta all'anello più debole della catena — un fornitore, un plugin, una libreria, un servizio esterno — e da lì si risale fino ai sistemi che davvero interessano. Per le grandi società di consulenza e revisione, che maneggiano dati fiscali e finanziari di migliaia di clienti aziendali, questo tipo di attacco è particolarmente redditizio: un solo punto d'ingresso può aprire le porte a un patrimonio enorme di informazioni sensibili.

C'è anche una lezione più ampia sulla gestione delle credenziali: se un fornitore terzo ha accesso — anche solo tecnico, anche solo per il supporto — a strumenti interni come Jira o repository su GitHub, quelle credenziali vanno trattate con lo stesso livello di attenzione riservato agli accessi "in casa". Rotazione periodica delle password, autenticazione a più fattori obbligatoria, permessi ridotti al minimo indispensabile (il principio del "least privilege") e monitoraggio degli accessi anomali sono contromisure che valgono per le multinazionali quanto per un piccolo team che si appoggia a servizi SaaS esterni.

Per chi lavora con dati sensibili — dichiarazioni fiscali, documenti finanziari, informazioni personali di clienti — la vicenda EY è un altro caso da tenere d'occhio: se sei un cliente o un dipendente di aziende che si affidano a EY per consulenza fiscale, tenere sotto controllo eventuali comunicazioni ufficiali dell'azienda nelle prossime settimane è la mossa più sensata, insieme alla solita raccomandazione di attivare avvisi antifrode sulle proprie informazioni finanziarie in caso di conferma della violazione.
