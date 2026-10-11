---
title: "FortiMail sotto attacco: zero-day critico già sfruttato, aggiornate subito"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/critical-fortimail-zero-day-flaw.html"
data_notizia: "2026-10-08"
tags: ["cybersecurity", "fortinet", "zero-day", "vulnerability", "patch"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: vulnerabilità attivamente sfruttata su sistemi email aziendali, con CVSS 9.8. Perfetto per i lettori che gestiscono infrastrutture o lavorano in aziende con FortiMail. Messaggio chiave: patch adesso, non domani.
---

# FortiMail sotto attacco: zero-day critico già sfruttato, aggiornate subito

Se nella vostra organizzazione usate FortiMail come gateway email, fermate tutto quello che state facendo e andate ad aggiornare. Non esagero: stiamo parlando di un bug con CVSS **9.8 su 10**, già attivamente sfruttato in natura, e già inserito da CISA nel catalogo delle vulnerabilità note ed exploitate.

## Cosa c'è che non va

La vulnerabilità, identificata come **CVE-2026-104286**, riguarda FortiMail, il sistema di email security di Fortinet ampiamente diffuso nelle aziende. Il bug è di tipo *arbitrary file write* non autenticato: in parole povere, un attaccante senza nessuna credenziale può scrivere file arbitrari sul sistema sottostante.

Questo è il tipo di vulnerabilità che fa girare la testa ai sysadmin. Non serve phishing, non servono credenziali rubate, non serve ingegneria sociale. Basta trovare il servizio esposto e si ha una porta sul retro praticamente garantita.

## Cosa rischiate in concreto

Quando si può scrivere file arbitrari su un sistema Linux o Windows che fa girare un mail server aziendale, le possibilità per un attaccante sono enormi:

- **Web shell**: si deposita un file PHP o ASPX in una directory accessibile via web, e si ha accesso permanente al sistema
- **Backdoor**: si sovrascrivono script di avvio o si aggiungono cronjob malevoli
- **Escalation di privilegi**: si possono sovrascrivere file di configurazione critici
- **Lateral movement**: dalla macchina compromessa si può scalare verso altri sistemi interni

Fortinet ha già rilasciato la patch, e CISA ha dato alle agenzie federali americane una scadenza stringente per applicarla. Ma non aspettate di essere un ente governativo americano per muovervi.

## Come verificare se siete vulnerabili

Prima di tutto, controllate la versione di FortiMail che state usando:

```bash
# Accedendo alla CLI di FortiMail
get system status | grep Version
```

Poi andate sul [sito di Fortinet](https://www.fortinet.com/support/psirt) e verificate quali versioni sono affette. In generale, il consiglio è di aggiornarsi sempre all'ultima release stabile disponibile.

Se gestite FortiMail via GUI web, andate su **System → Firmware** per verificare e applicare gli aggiornamenti.

## Mitigazioni temporanee se non potete patchare subito

Se siete in una situazione in cui un aggiornamento immediato non è fattibile (dipendenze, finestre di manutenzione, burocrazia aziendale...), alcune mitigazioni temporanee:

1. **Limitate l'accesso alla management interface**: non dovrebbe mai essere esposta su internet. Usate firewall o ACL per consentire l'accesso solo da IP amministrativi interni.
2. **Monitorate i log attivamente**: cercate scritture di file anomale, specialmente in directory web-accessibili.
3. **Isolate la macchina**: se possibile, riducete il traffico laterale tra FortiMail e il resto della rete interna.

```bash
# Esempio di blocco via iptables sulla porta di management (8443)
iptables -A INPUT -p tcp --dport 8443 ! -s 192.168.1.0/24 -j DROP
```

Ovviamente queste sono misure temporanee. La patch è l'unica vera soluzione.

## Il contesto più ampio

Questa non è la prima vulnerabilità critica che colpisce i prodotti Fortinet negli ultimi anni. FortiOS e FortiGate hanno avuto più volte CVE ad alto impatto. L'azienda in genere risponde rapidamente con le patch, ma il problema è sempre lo stesso: le aziende non aggiornano abbastanza velocemente.

La CISA tiene un catalogo pubblico delle vulnerabilità sfruttate attivamente, e se un CVE finisce lì vuol dire che ci sono attacchi reali in corso, non teorici. In questo caso il rischio è concreto e attuale.

## Cosa fare adesso

1. **Verificate se usate FortiMail** (o se lo usa un fornitore/managed service che gestisce la vostra posta)
2. **Controllate la versione** e confrontatela con l'advisory ufficiale Fortinet
3. **Pianificate l'aggiornamento** per le prossime ore, non le prossime settimane
4. **Avvisate il vostro team** di sicurezza se lo avete

La sicurezza email è spesso sottovalutata, ma è una delle superfici di attacco più critiche per qualsiasi organizzazione. Non regalate un accesso ai vostri sistemi per mancanza di un aggiornamento.
