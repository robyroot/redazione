---
title: "La Svizzera federale bucata via SharePoint: 200 account compromessi"
rilevanza: "ALTA"
fonte: "https://www.helpnetsecurity.com/2026/08/07/swiss-government-microsoft-sharepoint-vulnerabilities/"
data_notizia: "2026-08-07"
tags: ["cybersecurity", "sharepoint", "pubblica-amministrazione", "vulnerabilita"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: usarla come case study pratico per spiegare perché il "patch Tuesday" non basta
  se non lo accompagni da monitoraggio attivo. Buon gancio per parlare anche di SharePoint on-prem
  come bersaglio ricorrente (richiamo al ToolShell del 2025) e per un box "cosa fare se gestisci SharePoint
  on-prem in azienda". Taglio più tecnico/PA rispetto al solito, ma resta accessibile.
---

Quando si parla di attacchi informatici alla pubblica amministrazione, spesso si pensa a episodi lontani, roba da report annuali che leggono in pochi. Questa volta però il bersaglio è di quelli pesanti: l'ufficio federale svizzero che gestisce l'informatica e le telecomunicazioni dello stato, il BIT (Bundesamt für Informatik und Telekommunikation), ha confermato che gli aggressori sono riusciti a compromettere circa 200 account attraverso una falla nei server SharePoint interni.

**Cosa è successo, in ordine**

Il 28 luglio i tecnici della sicurezza del BIT notano attività anomala sui server SharePoint. Fin qui, nulla di diverso dal solito monitoraggio: succede spesso che un comportamento sospetto venga isolato e analizzato prima di capire se è un vero incidente. Il problema è che tre giorni dopo, il 31 luglio, arriva la conferma peggiore: le credenziali di accesso di diversi account, sia utenti "umani" che account tecnici (quelli usati da servizi e automazioni, spesso più critici perché hanno permessi ampi), risultano effettivamente compromesse.

A quel punto il BIT ha fatto la cosa giusta e l'ha fatta in fretta: accesso a internet della piattaforma bloccato, falle chiuse, password di tutti gli account coinvolti resettate. Sono stati coinvolti anche l'Ufficio federale per la cybersicurezza (BACS) e Microsoft stessa per il supporto tecnico, e gli indicatori di compromissione sono stati condivisi con gli operatori di infrastrutture critiche attraverso la piattaforma del BACS, così che chiunque altro usi sistemi simili potesse controllare di non essere nella stessa situazione.

**Quale falla hanno sfruttato**

Il BIT non ha voluto sbilanciarsi su quale vulnerabilità specifica sia stata usata, ma il sospetto ricade su due CVE di SharePoint rese pubbliche da Microsoft a metà luglio: CVE-2026-56164, una escalation di privilegi già sotto sfruttamento attivo nel mondo reale, e CVE-2026-50522, una remote code execution che in altri attacchi è stata usata per rubare le "machine key" di SharePoint. Questo secondo dettaglio è quello che dovrebbe far drizzare le antenne a chi gestisce SharePoint on-premise: rubare le machine key significa che, anche dopo aver installato la patch ufficiale, un attaccante che le ha già sottratte può continuare a forgiare token validi e mantenere l'accesso. In pratica, patchare non basta sempre: se la chiave è già in mano a qualcun altro, va rigenerata.

**I danni, per ora**

La buona notizia, se così si può dire, è che secondo il BIT sulla piattaforma colpita non è consentito conservare dati riservati o dati personali particolarmente sensibili, e al momento non ci sono prove che sia stato sottratto altro oltre alle credenziali. Non è una garanzia assoluta — le indagini forensi su incidenti di questo tipo richiedono settimane, a volte mesi, per essere davvero complete — ma è comunque un elemento che ridimensiona lo scenario peggiore.

**Perché dovrebbe interessarti anche se non lavori nella PA**

SharePoint on-premise è uno di quei bersagli "gettonati" da tempo per chi fa attacchi mirati contro enti pubblici e grandi aziende: lo stesso schema, con lo sfruttamento di catene di vulnerabilità per ottenere esecuzione di codice da remoto e poi rubare chiavi crittografiche per la persistenza, era già emerso nella campagna ToolShell del 2025 che aveva colpito decine di organizzazioni governative in giro per il mondo. Il punto è che questi server, se esposti su internet e non aggiornati con la stessa rapidità con cui vengono rese pubbliche le patch, restano un bersaglio facile e ricorrente.

Se in azienda o in ente gestisci ancora un'installazione SharePoint on-prem (non la versione cloud di Microsoft 365, che ha un modello di rischio diverso), la lista della spesa dopo una notizia come questa è semplice: verifica di avere installato le patch di luglio 2026, controlla i log di accesso per attività anomale nelle ultime settimane, e soprattutto valuta la rotazione delle machine key se sospetti anche solo lontanamente una compromissione pregressa — perché quella è la parte che una patch, da sola, non risolve.
