---
title: "FortiMail Zero-Day CVE-2026-104286: scrittura arbitraria di file senza autenticazione, patch non ancora disponibile"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/critical-fortimail-zero-day-flaw.html"
data_notizia: "2026-10-01"
tags: ["cybersecurity", "fortinet", "zero-day", "CVE", "sysadmin"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: focalizzati sull'aspetto pratico per i sysadmin italiani: quali versioni sono vulnerabili, cosa fare adesso in assenza di patch, e perché un server di posta esposto è un bersaglio critico. Aggiungi un link al catalogo KEV di CISA per chi vuole approfondire.
---

# FortiMail Zero-Day CVE-2026-104286: scrivi file sul server senza neanche fare login

Se gestisci un server di posta basato su Fortinet FortiMail, hai una priorità urgente da mettere in cima alla lista: **CVE-2026-104286**, un bug critico con CVSS 9.8 che viene sfruttato attivamente in questo momento. La cosa brutta? Al momento della scrittura di questo articolo, la patch ufficiale non è ancora disponibile.

## Cosa succede esattamente

La vulnerabilità permette a un attaccante remoto, **senza bisogno di autenticazione**, di scrivere file arbitrari sul sistema operativo sottostante il server FortiMail. Il meccanismo è una combinazione di due debolezze:

- **CWE-22** (path traversal): il software non valida correttamente i percorsi dei file nelle richieste HTTP/HTTPS
- **CWE-158** (gestione errata del byte NULL): caratteri speciali nella richiesta vengono interpretati in modo imprevisto

In pratica, un attaccante invia una richiesta HTTP appositamente costruita all'interfaccia di gestione di FortiMail e riesce a piazzare un file ovunque sul filesystem. Come ben sa chi conosce le tecniche offensive, "scrivere un file sul server" è spesso il primo passo per eseguire comandi: basta piazzare una webshell o sovrascrivere un file di configurazione critico.

## Chi è a rischio

Le versioni vulnerabili sono:

- FortiMail **8.0.0 – 8.0.1**
- FortiMail **7.6.0 – 7.6.6**
- FortiMail **7.4.0 – 7.4.8**

Fortinet consiglia di aggiornare alla versione 8.0.2 appena disponibile, e a versioni analoghe per i branch 7.x. Ma, come detto, le patch sono ancora in arrivo.

## Come mitigare adesso

In assenza di patch, Fortinet ha indicato alcune contromisure temporanee:

```bash
# Verifica se l'interfaccia di gestione FortiMail è esposta su internet
# (da fare sul firewall/router, non sul FortiMail stesso)
# Controlla le regole di accesso all'interfaccia admin
# Tipicamente porta 443 o 8443

# Se usi iptables sul gateway:
iptables -L -n | grep 443

# Isola l'interfaccia di gestione su una VLAN di management separata
# e limita l'accesso solo agli IP dei tuoi amministratori
```

La regola d'oro qui è **non esporre l'interfaccia di gestione di FortiMail su internet**. Se la stai usando come server di posta pubblica, l'interfaccia web di admin dovrebbe essere accessibile solo dalla tua rete interna o tramite VPN.

## La risposta delle autorità

CISA (l'agenzia americana per la cybersecurity) ha inserito CVE-2026-104286 nel suo catalogo **KEV (Known Exploited Vulnerabilities)** il 1° ottobre 2026. Le agenzie federali civili USA hanno avuto tempo fino al 4 ottobre per applicare le mitigazioni. Questo tipo di comunicazione accelerata dal governo americano è un segnale chiaro: il bug viene già sfruttato da attori reali, non è solo teorico.

## Cosa sappiamo degli attaccanti

Al momento Fortinet non ha attribuito gli attacchi a nessun gruppo specifico, né ha comunicato quante istanze sono già state compromesse. I ricercatori di watchTowr hanno confermato che lo sfruttamento della vulnerabilità è tecnicamente fattibile e che l'accesso in scrittura al filesystem può portare rapidamente all'esecuzione di codice.

## Cosa fare subito

1. **Inventario**: identifica tutte le istanze FortiMail nella tua infrastruttura e le loro versioni
2. **Isolamento**: assicurati che l'interfaccia di gestione NON sia raggiungibile da internet
3. **Monitoraggio**: controlla i log di accesso per richieste anomale all'interfaccia admin
4. **Aggiornamento**: monitora il sito di Fortinet e applica la patch appena disponibile
5. **Allarme**: se usi FortiMail 7.4, 7.6 o 8.0, considera questo una priorità P0

La situazione è in evoluzione: tieni d'occhio il [KEV di CISA](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) e il [PSIRT di Fortinet](https://www.fortiguard.com/psirt) per aggiornamenti sulla patch.
