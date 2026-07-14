---
title: "Falla critica in Oracle E-Business Suite: centinaia di aziende sotto attacco proprio ora"
rilevanza: "ALTA"
fonte: "https://www.bleepingcomputer.com/news/security/over-900-oracle-e-business-instances-exposed-to-ongoing-attacks/"
data_notizia: "2026-07-14"
tags: ["cybersecurity", "vulnerabilità", "oracle", "enterprise", "cve"]
livello: "intermediate"
nota_editoriale: |
  Angolo per RobyRoot: meno "guida tecnica alla patch" e più racconto di cosa succede
  quando una falla critica in un software enterprise diffusissimo (e spesso trascurato
  dai reparti IT perché "tanto è dietro il firewall") diventa terreno di caccia attivo.
  Buona occasione per parlare di superficie d'attacco esposta su internet, honeypot
  e tempi di reazione delle aziende rispetto ai criminali. Evitare tecnicismi da CVSS
  vector string, restare sul "perché dovrebbe interessarti anche se non usi Oracle".
---

Se lavori in un'azienda medio-grande, c'è una discreta probabilità che da qualche parte nei sistemi interni giri Oracle E-Business Suite: è quel tipo di software gigantesco e un po' invisibile che gestisce contabilità, paghe, ordini e pagamenti, e che nessuno tocca finché non si rompe. Ecco, in questi giorni si è rotto, e nel modo peggiore possibile: c'è una falla critica che viene già sfruttata attivamente da chi vuole entrare senza permesso.

Parliamo di **CVE-2026-46817**, un problema nel modulo Oracle Payments, con un punteggio di gravità di 9,8 su 10. Numeri come questo si vedono raramente, e quando compaiono di solito significa che qualcuno può fare danni seri con pochissimo sforzo.

## Cosa permette di fare questa falla

Il difetto si trova nella componente "File Transmission" di Oracle Payments, la parte del sistema che si occupa di scambiare file con l'esterno (pensa a bonifici, riconciliazioni bancarie, flussi di pagamento). Il problema è che, per un errore di gestione dei permessi, un attaccante può interagire con questa componente **senza bisogno di credenziali**: basta mandare richieste HTTP mirate al sistema esposto su internet.

Non serve rubare una password, non serve un dipendente disattento che clicca un link sbagliato: basta trovare il server online e colpirlo direttamente. Questo è il motivo per cui il punteggio è così alto, ed è anche il motivo per cui la situazione è già sfuggita di mano.

## Già sotto attacco, non solo "a rischio"

La cosa che distingue questa notizia da un semplice bollettino di sicurezza è che l'exploitation è già in corso, non ipotetica. Il gruppo di threat intelligence Defused ha osservato attività sospette sui propri honeypot — sistemi civetta creati apposta per attirare gli attaccanti e studiarne le mosse — riconducibili proprio a questa vulnerabilità. In pratica, mentre molte aziende stavano ancora valutando se e quando applicare la patch, qualcuno stava già bussando alle porte, letteralmente in tempo reale.

Il servizio di monitoraggio Shadowserver, che scandaglia costantemente internet alla ricerca di sistemi esposti, ha censito circa **950 istanze di Oracle E-Business Suite** raggiungibili pubblicamente. Non è dato sapere quante di queste abbiano già installato la correzione: è del tutto plausibile che una fetta consistente sia ancora vulnerabile in questo momento, mentre leggi questo articolo.

## La patch c'era già, il problema è chi non l'ha installata

Qui arriva la parte più frustrante della storia: Oracle aveva già rilasciato la correzione a **maggio 2026**, dentro il consueto pacchetto trimestrale di aggiornamenti di sicurezza (i famosi Critical Patch Update). Il problema, come capita fin troppo spesso nel mondo enterprise, è che applicare una patch a un sistema che gestisce contabilità e pagamenti non è mai un'operazione "al volo": richiede test, finestre di manutenzione, approvazioni. E mentre le aziende prendono tempo, gli attaccanti no.

È lo stesso schema visto decine di volte con altri software enterprise (pensa a Citrix, Fortinet, SharePoint): la finestra tra "patch disponibile" e "patch installata ovunque" è il momento in cui i criminali fanno festa, perché sanno esattamente cosa cercare grazie all'analisi pubblica della vulnerabilità.

## Perché dovrebbe interessarti anche se non usi Oracle

Anche se non gestisci sistemi Oracle, questa storia è un promemoria utile su due fronti. Primo: se lavori in un'azienda, chiedi (o fatti raccontare) come vengono gestiti gli aggiornamenti di sicurezza sui software "di back office" — spesso sono quelli più trascurati perché considerati meno critici dei sistemi rivolti al pubblico, quando in realtà contengono i dati più sensibili di tutti (paghe, dati bancari, contratti). Secondo: se sei un piccolo imprenditore o gestisci l'IT di una PMI con qualche sistema esposto su internet per comodità di accesso remoto, questo è l'ennesimo caso che dimostra quanto sia rischioso lasciare pannelli di amministrazione raggiungibili da chiunque, invece che dietro una VPN.

## Cosa fare, in pratica

Se in azienda si usa Oracle E-Business Suite con il modulo Payments esposto su internet, la patch di maggio 2026 va verificata e applicata subito, non alla prossima finestra di manutenzione programmata. Non esiste ancora un codice di exploit pubblico completo, ma quando la exploitation è già attiva sul campo, aspettare "il momento giusto" per aggiornare significa scommettere che i criminali non arrivino prima. Vista la storia recente della cybersecurity, è una scommessa che perde quasi sempre.
