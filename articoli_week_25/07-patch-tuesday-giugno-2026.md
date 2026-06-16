---
title: "Patch Tuesday Giugno 2026: le 5 vulnerabilità più pericolose da correggere subito"
stato: "BOZZA"
fonte: "https://www.bleepingcomputer.com/news/microsoft/microsoft-june-2026-patch-tuesday-fixes-6-zero-days-200-flaws/"
tags: ["sicurezza", "windows", "patch", "cve", "microsoft"]
livello: "intermediate"
---

Ogni secondo martedì del mese, Microsoft rilascia le patch di sicurezza. Giugno 2026 è stato particolarmente pesante: **206 vulnerabilità corrette**, di cui **6 zero-day** già sfruttati attivamente e **37 critiche**.

Se gestisci sistemi Windows — anche in ambienti misti con Linux — questo è il momento di aggiornare. Ecco cosa non puoi ignorare.

## I numeri del mese

Distribuzione per tipo:
- Privilege escalation: 65 patch (32%) — la categoria più numerosa
- Remote Code Execution: 43 patch
- Information disclosure: 31 patch

Sei di queste erano già conosciute dagli attaccanti prima della patch. Zero-day, appunto.

## Le 5 da correggere subito

### 1. CVE-2026-34482 — Windows Print Spooler (RCE, CVSS 9.8)
Il Print Spooler di Windows è una fonte inesauribile di problemi. Un attaccante sulla stessa rete può eseguire codice sul tuo sistema senza autenticazione. Priorità massima. Se non usi la stampa di rete, considera di disabilitare il servizio.

### 2. CVE-2026-33901 — MSMQ (RCE remota)
MSMQ è un componente spesso dimenticato ma presente su molti server Windows. Vulnerabile sulla porta 1801/TCP. Se non lo usi:

```powershell
Get-Service -Name MSMQ
Set-Service -Name MSMQ -StartupType Disabled
```

### 3. CVE-2026-31199 — Windows Kernel (LPE, zero-day attivo)
Privilege escalation nel kernel Windows, già sfruttata in attacchi reali contro obiettivi corporate. Richiede accesso locale, ma combinata con altri exploit è devastante.

### 4. CVE-2026-35021 — Microsoft Outlook (RCE via preview)
Basta aprire un'email in Outlook per far eseguire codice malevolo. Non serve cliccare allegati. La preview dell'email basta. CVSS 8.8. Aggiorna Outlook immediatamente.

### 5. CVE-2026-32774 — Active Directory Certificate Services
Escalation fino a Domain Admin in ambienti enterprise con AD CS. Se hai Active Directory, questa è critica.

## Come aggiornare

Windows Update → Verifica aggiornamenti → Installa tutto → Riavvia.

Su sistemi gestiti con WSUS o Intune, approva e distribuisci le patch di giugno il prima possibile.

## Per chi usa Linux ma ha Windows in rete

Se nella tua rete ci sono macchine Windows non aggiornate, sei esposto indirettamente. Un sistema Windows compromesso può diventare punto di pivot per attacchi laterali verso il resto della rete.

Controlla i sistemi Windows e assicurati che abbiano le patch di giugno.

## In sintesi

Sei zero-day attivi, due critiche con CVSS sopra 9, e una vulnerabilità in Outlook che colpisce senza che l'utente faccia nulla. Giugno 2026 non è un mese da ignorare.

Aggiorna. Riavvia. E considera di disabilitare Print Spooler e MSMQ se non li usi davvero.
