---
title: "SharePoint sotto assedio: CISA lancia un nuovo allarme mentre il ransomware Warlock continua a colpire"
rilevanza: "ALTA"
fonte: "https://www.cisa.gov/news-events/alerts/2026/07/14/cisa-urges-sharepoint-hardening-after-new-exploitations"
data_notizia: "2026-07-15"
tags: ["cybersecurity", "sharepoint", "ransomware", "cisa", "cve"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: chi legge RobyRoot probabilmente non amministra SharePoint in azienda, ma la storia
  è un ottimo caso di studio su "perché le patch datate 'exploitation less likely' vanno comunque applicate
  subito" e su come i gruppi ransomware oggi si muovano in team paralleli sulla stessa vittima. Buon gancio
  anche per parlare di IT hygiene generale (autenticazione, segmentazione di rete, machine key rotation)
  anche per chi gestisce piccoli server/homelab con software simile esposto online.
---

Se pensavi che le grane di SharePoint fossero finite con le patch di maggio, ripensaci. Il **14 luglio 2026** la CISA — l'agenzia americana per la cybersicurezza — ha pubblicato un nuovo alert per spingere le organizzazioni a rafforzare le difese sui propri server SharePoint on-premise, dopo aver rilevato nuove ondate di sfruttamento attivo. E dietro a tutto questo c'è un nome che nel mondo della sicurezza informatica suona già familiare: **Warlock**, un ransomware distribuito dal gruppo **Storm-2603**.

## Le vulnerabilità coinvolte

Al centro della vicenda ci sono tre CVE che colpiscono SharePoint Server nelle versioni Subscription Edition, 2019 e Enterprise Server 2016: **CVE-2026-32201**, **CVE-2026-45659** e **CVE-2026-56164**. La più pericolosa del gruppo è probabilmente CVE-2026-45659, un bug di **deserializzazione di dati non fidati** con un punteggio CVSS di 8,8 (alta gravità).

La cosa che dovrebbe far riflettere è che questa vulnerabilità richiede solo permessi minimi — basta essere un "Site Member" autenticato, non serve essere amministratore — per eseguire codice arbitrario da remoto sul server. Microsoft l'aveva corretta già a maggio 2026, e all'epoca l'aveva persino classificata come "Exploitation Less Likely" (sfruttamento poco probabile). I fatti hanno smentito quella valutazione: CISA ha aggiunto la falla al catalogo delle vulnerabilità note sfruttate attivamente (KEV) il 1° luglio, imponendo alle agenzie federali statunitensi di applicare la patch entro il 4 luglio.

## Chi sta attaccando e come

Il gruppo dietro le quinte si chiama **Storm-2603**, attivo nello sfruttamento di falle SharePoint almeno dalla metà del 2025 per distribuire il ransomware **Warlock**. Quello che rende questa storia particolarmente interessante (e inquietante) dal punto di vista tecnico è il modo in cui operano: non si limitano a un attacco mordi e fuggi, ma restano nell'ambiente compromesso a lungo, rubando le **IIS machine key** del server per garantirsi persistenza anche dopo che la vulnerabilità iniziale viene patchata.

Le indagini Microsoft hanno anche scoperto che Storm-2603 non lavora da solo: in alcune delle infrastrutture compromesse si muovevano contemporaneamente più gruppi di attaccanti diversi, tutti sulla stessa vittima. Un dettaglio da manuale del crimine informatico moderno: una volta che una falla nota diventa di dominio pubblico, non è raro che diventi terreno di caccia condiviso tra bande criminali indipendenti, ognuna con i propri obiettivi (furto dati, ransomware, spionaggio).

Per mantenere l'accesso anche dopo il rilevamento iniziale, gli attaccanti hanno sfruttato una combinazione di strumenti legittimi usati in modo malevolo (la tecnica nota come "living off the land"): tunnel Cloudflare, sessioni Zoho Assist e persino canali SSH incanalati attraverso Visual Studio Code. Tutti strumenti che, presi singolarmente, non farebbero scattare alcun allarme in un'azienda normale — il che li rende particolarmente efficaci per restare sotto il radar.

## Cosa raccomanda CISA

L'alert del 14 luglio non si limita a ribadire "applicate la patch". CISA sottolinea che le organizzazioni che gestiscono SharePoint on-premise devono considerare l'ipotesi di **compromissione già avvenuta**, anche se hanno applicato gli aggiornamenti di maggio, proprio perché la persistenza tramite machine key rubate sopravvive al semplice patching. Tra le raccomandazioni pratiche: ruotare le machine key di IIS, verificare i log per attività anomale risalenti anche a prima della patch, e monitorare l'uso sospetto di strumenti di accesso remoto legittimi.

## Perché conta anche per chi non usa SharePoint

Anche se non gestisci un server SharePoint aziendale, questa vicenda è un caso di studio utile per chiunque amministri servizi esposti su Internet, anche in piccolo — un homelab, un piccolo NAS con servizi web, un self-hosted qualsiasi. La lezione principale è che "patchare" non basta se un attaccante ha già avuto tempo di stabilire persistenza: bisogna anche verificare cosa è successo nel frattempo. E la seconda lezione, forse ancora più importante, è la sana diffidenza verso le valutazioni ottimistiche di gravità ("sfruttamento poco probabile") fatte dai vendor: la storia recente, da Log4Shell in poi, dimostra che i criminali informatici sono spesso più creativi e più veloci di quanto i produttori di software si aspettino.
