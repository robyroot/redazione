---
title: "SonicWall GMS: due falle critiche permettono l'accesso da remoto, anche se il prodotto è già in pensione"
rilevanza: "ALTA"
fonte: "https://www.securityweek.com/sonicwall-patches-critical-vulnerabilities-in-discontinued-gms-platform/"
data_notizia: "2026-08-12"
tags: ["cybersecurity", "vulnerabilità", "sonicwall", "rce", "sicurezza reti"]
livello: "intermediate"
nota_editoriale: |
  Angolo utile per RobyRoot: non tanto "correte a patchare SonicWall" (pubblico consumer/prosumer,
  pochi useranno GMS), quanto lo spunto più generale e riutilizzabile — "software dismesso non vuol
  dire software sicuro, anzi". Buon gancio per parlare di end-of-life dei prodotti, inventario del
  software in azienda/homelab, e perché conviene comunque monitorare gli avvisi di sicurezza anche
  per strumenti che non si aggiornano più attivamente con nuove funzionalità.
---

C'è un equivoco piuttosto comune quando si parla di software "dismesso" o "in fine vita": molti pensano che, una volta che un prodotto non riceve più nuove funzionalità, il produttore smetta anche di occuparsene sul fronte sicurezza. La storia di questa settimana dimostra che non è così — ed è un promemoria utile anche per chi gestisce solo un homelab o una piccola rete aziendale.

## Di cosa parliamo

SonicWall ha rilasciato il 12 agosto patch per **otto vulnerabilità** distribuite su due dei suoi prodotti, e tra queste ce ne sono due particolarmente serie che riguardano il **Global Management System (GMS)**, la piattaforma centralizzata usata per gestire, monitorare e generare report su interi parchi di firewall e appliance SonicWall. Il dettaglio interessante — e un po' preoccupante — è che GMS è stato **ufficialmente ritirato dal mercato a ottobre 2025**. Meno di un anno dopo il pensionamento, si scoprono due bug critici che permettono l'esecuzione di codice da remoto senza bisogno di autenticarsi.

## Le due falle più gravi

**CVE-2026-66147** (punteggio CVSS 9.4 su 10) è una vulnerabilità di **command injection** nel GMS Dispatcher Service: inviando richieste appositamente costruite, un attaccante remoto non autenticato può far eseguire comandi arbitrari sul sistema.

**CVE-2026-66145** (CVSS 9.1) è forse ancora più insidiosa dal punto di vista tecnico: sfrutta una tecnica nota come **zip slip**, un trucco che consiste nel confezionare un archivio compresso (zip) con percorsi di file manipolati (tipo `../../../etc/cron.d/qualcosa`) in modo che, quando l'applicazione estrae l'archivio, i file finiscano fuori dalla cartella prevista e vadano a sovrascrivere posizioni sensibili del sistema. Il risultato pratico è lo stesso: divulgazione di dati riservati e possibilità di scrittura arbitraria, che si traduce in esecuzione di codice da remoto.

A completare il quadro, ci sono altre due vulnerabilità ad alta severità legate a una validazione insufficiente dei certificati e a una gestione poco sicura degli oggetti serializzati — problemi classici che, combinati con le due falle critiche, aumentano ulteriormente la superficie d'attacco disponibile.

## Chi è a rischio

Le versioni interessate sono **GMS 9.5.1 e precedenti**, sia nella variante Virtual Appliance che in quella per Windows. È coinvolto anche il prodotto **Email Security** su alcune appliance specifiche. Il fix arriva con **GMS 9.5.2** ed **Email Security 10.0.36**.

SonicWall dichiara di non avere, al momento, evidenze di sfruttamento attivo in the wild. Ma va detto con chiarezza: "nessuna evidenza" non equivale a "nessuno sfruttamento" — significa solo che non è stato ancora rilevato, e con un CVSS sopra il 9 e nessuna autenticazione richiesta, è il tipo di falla che finisce rapidamente negli scanner automatici usati dai gruppi ransomware per individuare bersagli facili su scala globale.

## La lezione più larga: il "fine vita" non è una scusa

Il punto davvero interessante di questa vicenda non è tanto GMS in sé — un prodotto enterprise che probabilmente pochi lettori di RobyRoot hanno in casa — quanto il principio che porta con sé. Un software può essere "discontinued" dal punto di vista commerciale, senza nuove feature in arrivo, ma restare **installato e operativo** in centinaia o migliaia di organizzazioni per anni. Se contiene un bug critico, quel bug non sparisce solo perché il produttore ha smesso di venderlo: anzi, più tempo passa, meno persone tengono d'occhio gli avvisi di sicurezza relativi a quel prodotto specifico, perché "tanto è vecchio, chi se ne occupa più".

Vale per SonicWall GMS, ma vale altrettanto per il router che hai in cantina e non aggiorni da tre anni, per il NAS con un firmware che il produttore ha smesso di supportare, o per quel vecchio pannello di gestione lasciato acceso "perché funziona ancora". Un consiglio pratico, valido tanto per un'infrastruttura aziendale quanto per un homelab casalingo: tieni un **inventario aggiornato** di tutto ciò che hai esposto in rete (anche solo sulla rete locale) e, se un prodotto viene dichiarato end-of-life, considera prioritaria la sua sostituzione — non perché smetterà di funzionare da un giorno all'altro, ma perché nessuno ti garantisce più che i bug scoperti in futuro vengano corretti in tempo, o corretti affatto.

Se per lavoro o per hobby gestisci ancora un'istanza GMS, la priorità è chiara: aggiorna subito alla 9.5.2, o — meglio ancora, visto che il prodotto è comunque a fine vita — pianifica la migrazione verso l'alternativa attualmente supportata da SonicWall il prima possibile.
