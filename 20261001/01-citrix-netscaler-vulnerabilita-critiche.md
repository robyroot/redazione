---
title: "Citrix NetScaler sotto attacco: due vulnerabilità critiche sfruttate attivamente"
rilevanza: "ALTA"
fonte: "https://www.zerodayinitiative.com/blog/2026/9/16/the-apple-security-update-review-for-september-2026"
data_notizia: "2026-09-27"
tags: ["cybersecurity", "vulnerabilità", "citrix", "netscaler", "cve", "patching"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: urgenza pratica — chiunque gestisca un NetScaler deve patchare subito.
  Spiega bene i rischi per le PMI italiane e come verificare la propria esposizione.
---

# Citrix NetScaler sotto attacco: due vulnerabilità critiche sfruttate attivamente

Se nella tua rete c'è un Citrix NetScaler ADC o NetScaler Gateway, metti da parte quello che stai facendo: sono state confermate due vulnerabilità critiche con punteggio CVSS di 9.5 che vengono già sfruttate in the wild.

Citrix ha confermato il 27 settembre 2026 che le CVE-2026-88771 e CVE-2026-88772 sono sotto attacco attivo, con campagne osservate da Mandiant Consulting e dal Google Threat Intelligence Group.

## Cosa sono queste vulnerabilità

**CVE-2026-88771** permette a un attaccante non autenticato di eseguire comandi arbitrari sul sistema remoto. Non serve nessuna credenziale, nessun accesso precedente: basta raggiungere il dispositivo in rete.

**CVE-2026-88772** consente invece l'esecuzione di codice remoto (RCE) o attacchi di tipo denial-of-service. Entrambe le vulnerabilità hanno un vettore di rete, il che significa che l'esposizione a Internet rende i dispositivi immediatamente a rischio.

In pratica: se il tuo NetScaler è accessibile dall'esterno, un attaccante può comprometterlo senza dover fare login.

## Chi è già nel mirino

Gli attacchi osservati a settembre 2026 hanno colpito settori molto eterogenei:

- **Governo e pubblica amministrazione**
- **Servizi finanziari**
- **Tecnologia**
- **Istruzione**
- **Servizi legali e professionali**

Non si tratta di attacchi opportunistici a piccole realtà: i threat actor dietro queste campagne stanno prendendo di mira organizzazioni strutturate, probabilmente con obiettivi di accesso prolungato (initial access per ransomware o spionaggio industriale).

## Come verificare la tua esposizione

Prima di tutto, controlla se hai NetScaler esposto su Internet:

```bash
# Scansione rapida per verificare porte tipiche NetScaler
nmap -p 443,8443,80,8080 tuo-netscaler-ip -sV

# Controlla la versione del firmware dalla CLI NetScaler
ssh nsroot@tuo-netscaler-ip "show version"
```

Puoi anche usare Shodan per cercare dispositivi NetScaler esposti nella tua ASN:

```
shodan search "netscaler" net:TUA_ASN
```

## Come proteggersi

**Aggiorna immediatamente.** Citrix ha rilasciato le patch di sicurezza contestualmente alla disclosure. Le versioni aggiornate che correggono entrambe le CVE sono disponibili nel portale support.citrix.com.

Se non puoi aggiornare subito:

1. **Limita l'accesso al management interface** tramite ACL o firewall — nessuno dovrebbe accedere alla GUI di amministrazione dall'Internet pubblico.
2. **Abilita il WAF integrato** con le signature aggiornate per mitigare i tentativi di sfruttamento.
3. **Monitora i log** per pattern anomali: autenticazioni da IP insoliti, comandi inusuali, traffico verso IP esterni sconosciuti.

```bash
# Su NetScaler, verifica i log di autenticazione sospetti
grep -i "authentication" /var/log/ns.log | tail -100

# Controlla le connessioni attive verso l'esterno
netstat -an | grep ESTABLISHED
```

## La situazione più ampia

Questi attacchi si inseriscono in un trend preoccupante: i dispositivi di rete perimetrale (VPN, load balancer, firewall) sono diventati il bersaglio preferito per l'accesso iniziale alle reti aziendali. Nel 2025-2026 abbiamo visto campagne simili contro Palo Alto, Fortinet, Ivanti e ora Citrix.

Il motivo è semplice: questi apparati spesso vengono dimenticati nell'armadio di rete, senza gli stessi cicli di patching che si applicano ai server. Se gestisci infrastruttura di rete, inserisci questi device nei tuoi processi di vulnerability management con la stessa priorità dei sistemi server.

## Cosa fare ora

1. Vai su support.citrix.com e verifica le versioni corrette
2. Pianifica l'aggiornamento per oggi o domani al massimo
3. Nel frattempo, isola il management plane dal traffico pubblico
4. Controlla i log degli ultimi 30 giorni per eventuali compromissioni già avvenute

Se usi un SIEM, aggiungi subito regole di detection per le IoC (Indicators of Compromise) pubblicate da Mandiant e Google TIG relativamente a queste CVE.

Non aspettare: con un CVSS di 9.5 e sfruttamento attivo confermato, ogni ora conta.
