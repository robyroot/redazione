---
title: "Zero-Day su FortiMail e Citrix NetScaler: aggiorna subito o sei a rischio"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/weekly-recap-netscaler-and-fortimail-0.html"
data_notizia: "2026-10-05"
tags: ["sicurezza", "zero-day", "FortiMail", "Citrix", "NetScaler", "CISA", "vulnerabilità", "CVE"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Urgente per sysadmin e IT italiani — la CISA ha imposto deadline il 7 ottobre per NetScaler. Articolo pratico con consigli su come verificare le versioni vulnerabili e applicare le patch.
---

# Zero-Day su FortiMail e Citrix NetScaler: aggiorna subito o sei a rischio

Questa settimana la comunità della sicurezza informatica si trova a fare i conti con due vulnerabilità zero-day critiche che vengono già sfruttate attivamente: una colpisce Fortinet FortiMail, l'altra Citrix NetScaler. Se gestisci infrastrutture aziendali con questi prodotti, smetti di leggere e aggiorna adesso. Per il resto, ecco tutto quello che devi sapere.

## FortiMail: scrittura arbitraria di file senza autenticazione (CVSS 9.8)

La falla più grave della settimana porta il codice **CVE-2026-104286** e ha ricevuto un punteggio CVSS di **9.8 su 10** — praticamente il massimo della pericolosità. Il problema riguarda Fortinet FortiMail, la soluzione di email security molto diffusa nelle medie e grandi aziende.

La vulnerabilità consente a un attaccante non autenticato — cioè senza bisogno di credenziali — di scrivere file arbitrari sul sistema sottostante. In pratica, chi conosce il bug può caricare una webshell o un payload malevolo direttamente sul server, ottenendo accesso completo alla macchina. La CISA (Cybersecurity and Infrastructure Security Agency americana) ha già aggiunto questa CVE al proprio catalogo delle vulnerabilità sfruttate attivamente (KEV), il che significa: sta già succedendo per davvero, non è solo teoria.

**Cosa fare:** Controlla immediatamente la versione di FortiMail in uso e applica la patch rilasciata da Fortinet. Se un aggiornamento immediato non è possibile, valuta di isolare il servizio dalla rete pubblica fino a quando non puoi intervenire.

```bash
# Verifica la versione di FortiMail dalla CLI (SSH admin)
get system status | grep "Version"
```

## Citrix NetScaler: zero-day SAML con deadline CISA domani

La seconda emergenza riguarda **CVE-2026-88779**, una falla in Citrix NetScaler con CVSS **8.7**. Questa vulnerabilità colpisce le installazioni che usano SAML per l'autenticazione e può mandare offline l'intera infrastruttura di accesso remoto — un problema devastante per chi usa NetScaler come gateway VPN o per l'accesso alle applicazioni aziendali.

La CISA ha richiesto a tutte le agenzie federali americane di applicare la patch entro il **7 ottobre 2026** — domani. Questo non significa che il problema riguardi solo i governi: la scadenza CISA è un segnale forte che la vulnerabilità è già in mano agli attaccanti e che i tempi per agire sono brevissimi.

Citrix ha rilasciato aggiornamenti di sicurezza per le versioni supportate. Se usi NetScaler ADC o NetScaler Gateway con SAML abilitato, sei potenzialmente esposto.

```bash
# Controlla la build di NetScaler dalla shell NS
show version
# Cerca sul portale Citrix la build corretta per la tua branch
```

## Come capire se sei vulnerabile

Se la tua organizzazione usa FortiMail o Citrix NetScaler, la prima cosa da fare è identificare la versione esatta in produzione e confrontarla con i bollettini di sicurezza ufficiali:

- **FortiMail:** [Fortinet PSIRT Advisory](https://www.fortiguard.com/psirt)
- **Citrix NetScaler:** [Citrix Security Bulletins](https://support.citrix.com/article/CTX)

Vale anche la pena di controllare i log di accesso per anomalie recenti — scritture di file insolite, richieste HTTP malformate verso endpoint di amministrazione, sessioni SAML con origini inaspettate.

## Il contesto più ampio

Questa settimana è stata particolarmente intensa per la sicurezza IT: oltre a queste due CVE, sono emerse anche vulnerabilità critiche su Microsoft Exchange Server (CVE-2026-96940, privilege escalation con CVSS 8.8) e su Rejetto HFS (CVE-2026-61500, session forgery con CVSS 9.3). Il tema comune è che gli attaccanti si stanno concentrando su strumenti di rete e di collaborazione — gateway, mail server, VPN — che sono esposti su internet per loro natura.

## Cosa fare adesso

1. **Inventaria** i prodotti Fortinet e Citrix nella tua infrastruttura
2. **Applica le patch** disponibili il prima possibile
3. **Monitora** i log per attività anomale negli ultimi 7 giorni
4. **Segnala** eventuali compromise al tuo team di sicurezza o al CSIRT italiano

Non aspettare: con un CVSS di 9.8 e sfruttamento attivo in corso, ogni ora di ritardo è un rischio concreto.
