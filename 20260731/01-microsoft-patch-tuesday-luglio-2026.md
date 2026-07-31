---
title: "Microsoft Patch Tuesday Luglio 2026: 570 vulnerabilità e 2 zero-day sotto attacco"
rilevanza: "ALTA"
fonte: "https://www.bleepingcomputer.com/news/microsoft/microsoft-july-2026-patch-tuesday-fixes-massive-570-flaws-3-zero-days/"
data_notizia: "2026-07-15"
tags: ["sicurezza", "microsoft", "windows", "patch-tuesday", "zero-day", "cve"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Anche gli utenti Linux usano sistemi misti o gestiscono server Windows. Questo è il Patch Tuesday più grande di sempre, con zero-day attivamente sfruttati su AD FS e SharePoint. Ottimo per sensibilizzare i lettori su come funziona la gestione delle patch nel mondo Windows e cosa possono fare anche loro per proteggersi.
---

## Un Patch Tuesday da record assoluto

Il 15 luglio 2026 è entrato nella storia della sicurezza informatica: Microsoft ha rilasciato il suo aggiornamento mensile tappando la bellezza di **570 vulnerabilità** in una sola tornata. Un record assoluto, mai visto prima. Per dare un senso alle proporzioni: la media storica dei Patch Tuesday si aggirava intorno ai 150-200 CVE al mese. Questo luglio ha triplicato quella media.

Ma il numero non è la parte più preoccupante. Tra le 570 vulnerabilità ci sono **tre zero-day**, di cui **due già sfruttati attivamente** nel mondo reale prima ancora che Microsoft rilasciasse la patch. Questo significa che attaccanti reali stavano usando queste falle per entrare nei sistemi mentre tu stavi leggendo le notizie del mattino.

## I due zero-day sotto attacco

**CVE-2026-56155 — Active Directory Federation Services (AD FS)**

AD FS è il componente che Microsoft usa per l'autenticazione federata, cioè il sistema che consente alle grandi aziende di fare Single Sign-On tra servizi diversi. Una vulnerabilità qui significa potenzialmente accesso non autorizzato a decine o centinaia di sistemi con una sola exploit. Chiunque gestisca un'infrastruttura aziendale basata su AD FS dovrebbe considerare questa patch come emergenza immediata.

**CVE-2026-56164 — Microsoft SharePoint Server**

SharePoint è la piattaforma di collaborazione/intranet più usata nelle aziende. Questa falla permette l'esecuzione di codice da remoto (RCE), che è il peggior scenario possibile: un attaccante può far girare codice arbitrario sul server senza avere credenziali valide. Combinata con la falla AD FS, si apre un vettore di attacco completo che va dall'autenticazione all'esecuzione.

Un terzo zero-day, **CVE-2026-50661** in Windows BitLocker, è stato reso pubblico ma non risulta ancora sfruttato in natura. BitLocker è il sistema di cifratura dischi di Windows: una falla qui potrebbe permettere di aggirare la crittografia, scenario critico soprattutto per laptop aziendali rubati o persi.

## La struttura del mega-aggiornamento

Dei 570 CVE totali, **59 sono classificate "Critiche"**. Nel dettaglio:
- 48 permettono Remote Code Execution — esecuzione di codice arbitrario da remoto
- 9 sono Elevation of Privilege — scalata di privilegi
- 1 è un bypass di sicurezza
- 1 è spoofing

Il resto delle 570 vulnerabilità si divide tra Information Disclosure (102), Denial of Service (35), Security Feature Bypass (17) e Spoofing (16).

## Perché così tanti bug in un solo mese?

Microsoft ha rivelato qualcosa di interessante a margine dell'annuncio: il numero record è in parte dovuto a un **sistema di vulnerability discovery basato su AI** che l'azienda ha recentemente dispiegato per analizzare proattivamente il codice Windows prima che lo facciano gli attaccanti. In pratica, un sistema automatizzato ha trovato centinaia di problemi dormienti nel codice Microsoft.

È un po' paradossale: l'AI aiuta a scoprire i bug in modo più rapido, ma allo stesso tempo rende i Patch Tuesday sempre più pesanti da gestire per i team IT.

## Cosa fare adesso

Se gestisci sistemi Windows in azienda, le priorità sono chiare:

```powershell
# Verifica se AD FS è esposto verso internet
# (da eseguire con RSAT installato)
Get-AdfsProperties | Select-Object HostName, HttpsPort

# Controlla la versione di SharePoint
# Da PowerShell con accesso al server SharePoint
(Get-SPFarm).BuildVersion

# Forza Windows Update da riga di comando
wuauclt /detectnow /updatenow
```

Per gli utenti home, la cosa più semplice è assicurarsi che **Windows Update** sia abilitato. Vai su **Impostazioni → Windows Update → Verifica aggiornamenti** e applica tutto quello che trovi.

## L'angolo Linux

Per chi usa Linux in ambienti misti, questa notizia serve da promemoria utile. Se usi **Samba AD DC** o tool di integrazione con Active Directory (sssd, winbind, realmd), tieni d'occhio i bollettini di sicurezza relativi a questi strumenti nelle prossime settimane: le vulnerabilità nel protocollo Kerberos e NTLM spesso hanno ripercussioni anche sui client Linux che si autenticano contro AD.
