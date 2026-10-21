---
title: "Allerta sicurezza: Cisco Email Gateway e BeyondTrust sotto attacco attivo"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/cisco-warns-of-active-attacks.html"
data_notizia: "2026-10-16"
tags: ["sicurezza", "cisco", "vulnerabilità", "patch", "cybersecurity", "cve"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: informare sysadmin e utenti aziendali su vulnerabilità critiche già sfruttate, con checklist pratica per verificare l'esposizione e indicazioni su come applicare le patch.
---

## Ottobre 2026: due vulnerabilità critiche già sfruttate, aggiorna subito

Ottobre 2026 passerà alla storia come uno dei mesi più impegnativi per la sicurezza informatica. Il Patch Tuesday di Microsoft ha corretto oltre 1.400 vulnerabilità (un record), ma le notizie più urgenti riguardano due falle già sfruttate attivamente: una in **Cisco Secure Email Gateway** e una in **BeyondTrust Remote Support**.

Se gestisci infrastrutture aziendali o lavori come sysadmin, questa non è una lettura opzionale.

## Cisco Secure Email Gateway: scrittura file da remoto senza autenticazione

Cisco ha emesso un advisory urgente per una vulnerabilità critica nel suo **Secure Email Gateway (SEG)**, il prodotto usato da migliaia di aziende per filtrare le email in entrata.

Il meccanismo di attacco è inquietante nella sua semplicità: un attaccante invia un'email con un allegato appositamente costruito. Se l'allegato raggiunge il gateway vulnerabile, il sistema di scansione processa il file in modo non sicuro, permettendo di **scrivere file arbitrari nel sistema operativo dell'appliance**. Da lì, con un po' di fortuna e persistenza, si arriva all'esecuzione di comandi con privilegi di root.

Non serve nessuna credenziale. Non serve nessun account. Basta mandare un'email.

### Sono a rischio?

Se usi Cisco Secure Email Gateway (fisico o virtuale), controlla subito la versione:

```bash
# Dalla CLI dell'appliance Cisco
show version

# Oppure via interfaccia web:
# System Administration > System Information
```

Cisco ha rilasciato le patch. Segui l'advisory ufficiale su cisco.com/security per le versioni interessate e le istruzioni di aggiornamento. Non aspettare — gli attacchi sono attivi in questo momento.

### Workaround temporaneo

Se non puoi patchare immediatamente, Cisco suggerisce di verificare le regole di filtering degli allegati e, dove possibile, di bloccare temporaneamente i tipi di file coinvolti. Ma la patch è l'unica soluzione definitiva.

## BeyondTrust Remote Support: autenticazione bypassata (CVE-2026-102764)

La seconda vulnerabilità riguarda **BeyondTrust Remote Support**, uno strumento usato moltissimo nei contesti di helpdesk e supporto IT enterprise. La falla, identificata come **CVE-2026-102764**, è classificata come **authentication bypass critico**.

In pratica: un attaccante non autenticato può aggirare completamente il meccanismo di login e accedere alle funzionalità riservate agli amministratori. Dato che BeyondTrust viene usato per accedere in remoto ai computer degli utenti, un compromesso di questo sistema equivale potenzialmente a avere accesso a tutta l'infrastruttura supportata.

**CISA** (l'agenzia americana per la sicurezza informatica) ha aggiunto questa vulnerabilità alla propria lista KEV (Known Exploited Vulnerabilities) il 16 ottobre 2026, con deadline di remediation immediata per le agenzie federali USA. Questo è uno dei segnali più forti che una falla viene sfruttata concretamente nel mondo reale.

### Come verificare l'esposizione

```bash
# Verifica se BeyondTrust Remote Support è esposto pubblicamente
# Sostituisci con il tuo IP/hostname
curl -s -o /dev/null -w "%{http_code}" https://tuo-server-beyondtrust/

# Controlla i log di accesso per attività anomale
tail -f /var/log/bomgar-appliance/access.log 2>/dev/null || \
tail -f /var/log/beyondtrust/access.log 2>/dev/null
```

BeyondTrust ha rilasciato le patch — aggiorna immediatamente all'ultima versione disponibile sul portale clienti.

## Il contesto: Patch Tuesday da record

Per completare il quadro: il Patch Tuesday di Microsoft del 13 ottobre ha corretto **oltre 1.413 vulnerabilità**, tra cui:

- **CVE-2026-96951**: un bypass del Mark of the Web in Windows Shell (sfruttato attivamente), che permette di aprire file scaricati da internet senza i normali avvisi di sicurezza
- **CVE-2026-100202**: use-after-free in Windows Message Queuing con CVSS 9.8, potenziale RCE remoto
- **CVE-2026-70187**: RCE in Windows Remote Desktop Gateway senza autenticazione

Se gestisci sistemi Windows, assicurati che Windows Update sia stato eseguito negli ultimi giorni.

## Checklist rapida per sysadmin

Se gestisci infrastrutture, usa questa checklist come punto di partenza:

- [ ] Cisco Secure Email Gateway aggiornato all'ultima versione?
- [ ] BeyondTrust Remote Support patchato (CVE-2026-102764)?
- [ ] Windows Update applicato su tutti i sistemi gestiti?
- [ ] CISA KEV catalog controllato per eventuali altri prodotti in uso?
- [ ] Log di accesso di sistemi critici rivisti per attività anomale?

```bash
# Verifica rapida degli aggiornamenti pendenti su sistemi Debian/Ubuntu
apt list --upgradable 2>/dev/null | grep -i security

# Su RHEL/CentOS/Rocky
dnf check-update --security

# Su Arch (aggiornamenti disponibili)
checkupdates | head -20
```

## Conclusione

Ottobre 2026 è un mese da tenere d'occhio per chi lavora nel settore IT. Le vulnerabilità in Cisco SEG e BeyondTrust non sono teoriche — vengono sfruttate in questo momento da attori reali contro organizzazioni reali. Se usi questi prodotti, la patch non è opzionale.

Aggiungi il sito di CISA ai tuoi feed RSS e tieni d'occhio il loro [KEV catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) per aggiornamenti in tempo reale sulle vulnerabilità più pericolose.
