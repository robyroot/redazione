---
title: "SolarWinds Web Help Desk: bypass SAML critico con CVSS 9.8, aggiornate subito"
rilevanza: "ALTA"
fonte: "https://gbhackers.com/critical-solarwinds-web-help-desk-flaw/"
data_notizia: "2026-07-30"
tags: ["solarwinds", "vulnerabilità", "saml", "patch", "cybersecurity", "enterprise"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: vulnerabilità critica CVSS 9.8 su software enterprise molto diffuso. Utile per sysadmin e IT manager che gestiscono help desk aziendali. Collegare con l'importanza di applicare le patch tempestivamente, e richiamare la storia delle vulnerabilità SolarWinds precedenti (supply chain attack 2020) per dare contesto.
---

## La notizia in una riga

SolarWinds ha rilasciato il 30 luglio 2026 una patch d'emergenza per Web Help Desk: una vulnerabilità critica (CVSS **9.8/10**) permette di bypassare completamente l'autenticazione SAML e accedere al sistema senza credenziali.

## Cos'è SolarWinds Web Help Desk

Web Help Desk (WHD) è una piattaforma di ticketing IT usata da migliaia di organizzazioni — università, ospedali, enti pubblici, aziende — per gestire richieste di supporto, inventario hardware e change management. Se l'IT della tua organizzazione ha un sistema interno per aprire ticket, ci sono buone probabilità che sia proprio WHD o qualcosa di simile.

Molte installazioni usano l'autenticazione **SSO (Single Sign-On) tramite SAML 2.0**, che permette agli utenti di fare login con le credenziali aziendali centralizzate (Microsoft Entra ID, Okta, Google Workspace, ADFS, etc.). Ed è proprio lì che si nasconde il problema.

## CVE-2026-28323: il bypass dell'autenticazione

La vulnerabilità — identificata come **CVE-2026-28323** — risiede nel modo in cui WHD gestisce e valida le risposte SAML durante il flusso di autenticazione. In parole semplici: il server si fida troppo di quello che gli viene inviato, senza verificarlo correttamente.

Un attaccante che conosce l'URL del tuo Web Help Desk può:

- **Bypassare completamente il login** — senza username, senza password, senza MFA
- **Impersonare qualsiasi utente**, inclusi gli amministratori di sistema
- **Leggere tutti i dati gestiti da WHD**: ticket di supporto aperti, informazioni sugli utenti, dati sull'infrastruttura IT, comunicazioni interne tra tecnici e richiedenti

La vulnerabilità è stata scoperta da Dhabaleshwar Das, che l'ha segnalata responsabilmente a SolarWinds prima della pubblicazione.

## Non è l'unico problema

La versione 2026.2.1 (la patch) corregge anche **CVE-2026-28299**, un difetto di denial-of-service con CVSS 8.2: un attaccante non autenticato può mandare in crash il server WHD inondandolo di richieste malformate che esauriscono la memoria disponibile.

Due vulnerabilità gravi in un colpo solo. Non è una patch che si può rimandare.

## Come verificare la versione installata

Accedi alla console web di WHD come amministratore e vai su **Impostazioni > Info > Versione**.

Se hai accesso diretto al server, prova:

```bash
# Cerca il file di versione di WHD (percorso tipico su Linux)
find /opt /usr/local -name "version.properties" 2>/dev/null | xargs grep -i version 2>/dev/null
```

Se la versione è precedente a **2026.2.1**, sei vulnerabile.

## Come aggiornare

1. Scarica la versione **2026.2.1** dal portale clienti SolarWinds (serve un account con contratto attivo)
2. Segui la procedura ufficiale di upgrade dalla documentazione SolarWinds
3. **Dopo l'aggiornamento**, testa il flusso di autenticazione SAML con il tuo identity provider
4. **Controlla i log di accesso** per attività anomale nelle settimane precedenti alla patch

```bash
# Log di accesso WHD (percorso tipico su Linux)
grep -i "saml\|login\|auth\|admin" /usr/local/webhelpdesk/logs/application.log 2>/dev/null | \
  grep -v "200 OK" | tail -200
```

Cerca accessi con orari insoliti, IP non riconosciuti, o sessioni di account amministrativi che normalmente non usano WHD direttamente.

## Il contesto SolarWinds

È impossibile non citare il 2020: il supply-chain attack alla piattaforma Orion di SolarWinds ha compromesso oltre 18.000 organizzazioni, incluse agenzie governative americane. Da allora l'azienda ha investito molto in sicurezza e processi interni. Ma le vulnerabilità continuano a emergere — come in qualsiasi software complesso.

La lezione rimane sempre la stessa: tieni aggiornato il software, monitora i log e non esporre pannelli di amministrazione su internet senza protezioni aggiuntive (VPN, IP allowlist, WAF).
