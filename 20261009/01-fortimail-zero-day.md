---
title: "FortiMail sotto attacco: zero-day critico sfruttato attivamente, aggiorna subito"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/critical-fortimail-zero-day-flaw.html"
data_notizia: "2026-10-07"
tags: ["cybersecurity", "vulnerabilità", "fortinet", "zero-day", "email"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: focalizzarsi sul rischio concreto per le PMI italiane che usano FortiMail come gateway email, con istruzioni chiare su come verificare la versione installata e cosa fare nell'immediato.
---

# FortiMail sotto attacco: zero-day critico sfruttato attivamente, aggiorna subito

Se la tua azienda usa Fortinet FortiMail come gateway email, questa è una notizia che non puoi ignorare. CISA — l'agenzia americana per la sicurezza informatica — ha appena aggiunto una vulnerabilità critica di FortiMail al suo catalogo delle falle attivamente sfruttate. Tradotto: i criminali la stanno già usando adesso.

## Cosa è successo esattamente

La vulnerabilità, catalogata come CVE-2026-104286, ha ricevuto un punteggio CVSS di 9.8 su 10 — praticamente il massimo del rischio. Il difetto permette a un attaccante non autenticato di scrivere file arbitrari sul sistema sottostante FortiMail. Nessun account, nessuna password: basta conoscere l'indirizzo del server e il gioco è fatto.

In pratica, uno sfruttamento riuscito può portare a:
- Installazione di webshell (backdoor persistenti sul server)
- Compromissione completa del server di posta
- Accesso a email archiviate e dati sensibili
- Uso del server come trampolino per attacchi alla rete interna

CISA ha emesso una direttiva alle agenzie federali USA per applicare la patch entro pochi giorni, ma la raccomandazione vale ovviamente per tutti.

## Chi è a rischio

FortiMail è molto diffuso nelle medie e grandi aziende come soluzione di sicurezza email on-premise. Se usi:
- FortiMail in versione self-hosted
- Un gateway email gestito che usa Fortinet sotto
- Qualsiasi appliance FortiMail fisica o virtuale

...allora dovresti verificare immediatamente la versione installata.

## Come verificare la versione

Dal pannello di amministrazione FortiMail puoi controllare la versione così:

```bash
# Via SSH sull'appliance FortiMail
get system status | grep Version
```

Oppure dalla GUI: **System → Dashboard → System Information**.

Controlla anche il sito ufficiale Fortinet PSIRT per le versioni patched:

```bash
# Controlla il bollettino Fortinet (da browser)
# https://www.fortiguard.com/psirt
```

## Cosa fare adesso

**Priorità 1 — Aggiorna subito.** Fortinet ha rilasciato patch per le versioni supportate. Accedi al portale di supporto Fortinet e scarica l'aggiornamento per la tua branch.

**Priorità 2 — Controlla i log.** Se non puoi aggiornare immediatamente, cerca attività sospette nei log del server:

```bash
# Su FortiMail via SSH, controlla i log di sistema recenti
execute log filter field msg "file write"
execute log display
```

**Priorità 3 — Limita l'accesso.** Se l'interfaccia di amministrazione è esposta su internet, rimuovila subito dietro VPN o IP allowlist.

**Priorità 4 — Notifica il tuo team.** Se usi un provider managed, apri un ticket urgente e chiedi conferma che la patch sia stata applicata.

## Il contesto più ampio

Questo è l'ennesimo zero-day che colpisce un prodotto di sicurezza di rete — una tendenza preoccupante degli ultimi anni. I firewall, i gateway email e i concentratori VPN sono diventati bersagli privilegiati proprio perché stano al perimetro della rete e, se compromessi, danno accesso a tutto.

L'ironia amara è che stai comprando un prodotto di sicurezza che diventa il vettore di attacco. La lezione è sempre la stessa: nessun prodotto è immune, e aggiornare tempestivamente non è opzionale.

Per chi gestisce infrastrutture, iscriversi al feed PSIRT di Fortinet (o usare strumenti come OpenVAS per monitoring continuo) è una buona pratica da adottare subito.

---

*Fonti: The Hacker News, CISA KEV Catalog, Security Boulevard OT Security News*
