---
title: "Patch Tuesday luglio 2026: Microsoft chiude 570 falle in un colpo solo — record storico"
rilevanza: "ALTA"
fonte: "https://www.bleepingcomputer.com/news/microsoft/microsoft-july-2026-patch-tuesday-fixes-massive-570-flaws-3-zero-days/"
data_notizia: "2026-07-15"
tags: ["microsoft", "windows", "sicurezza", "patch", "zero-day", "vulnerabilità", "patch-tuesday"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: usa l'angolo "perché così tante CVE?" per spiegare che Microsoft stessa usa AI per trovare bug nel proprio codice — accelerando sia il ritmo delle patch sia quello degli attacchi. Utile per lettori con ambienti misti Linux/Windows o per chi gestisce infrastrutture IT.
---

# Patch Tuesday luglio 2026: Microsoft chiude 570 falle in un colpo solo — record storico

Ogni secondo martedì del mese arriva il Patch Tuesday di Microsoft, di solito con qualche decina di aggiornamenti che nessuno installa subito ma che tutti sanno che bisognerebbe installare. Quello di luglio 2026 però è diverso: si parla di **570 vulnerabilità corrette in un'unica tornata**, un record assoluto nella storia dei Patch Tuesday. E tre di queste erano già sfruttate attivamente dagli attaccanti.

## Un numero che fa girare la testa

Per darti un contesto: il Patch Tuesday medio degli ultimi anni si aggirava su 60-100 vulnerabilità. Arrivare a 570 significa quasi quintuplicare la media. Di queste falle:

- **57 classificate "Critical"** — le più gravi, da trattare con urgenza
- **48 sono Remote Code Execution** — permettono a un attaccante di eseguire codice da remoto senza toccare il sistema fisicamente
- **254 sono Elevation of Privilege** — consentono di scalare i permessi su un sistema già compromesso
- **102 sono Information Disclosure** — espongono dati sensibili
- **3 erano zero-day**, ovvero già note e sfruttate prima del fix ufficiale

## I tre zero-day da tenere d'occhio

Le vulnerabilità più urgenti sono quelle già utilizzate in attacchi reali:

**CVE-2026-56155 — Active Directory Federation Services (AD FS)**: Un'elevazione di privilegi nei servizi di federazione di Active Directory. Un attaccante già autenticato può scalare i propri permessi localmente. Particolarmente critica in ambienti aziendali dove AD FS gestisce l'autenticazione single sign-on.

**CVE-2026-56164 — SharePoint Server**: Elevazione di privilegi via rete, senza privilege pre-esistenti e con bassa complessità di attacco. La combinazione "rete + no credenziali + facile da sfruttare" la rende una delle CVE più pericolose del lotto. Un attaccante sulla rete aziendale può scalare i permessi su SharePoint con relativa facilità.

**CVE-2026-50661 — BitLocker Security Feature Bypass**: Questo non è ancora sfruttato attivamente, ma è stato divulgato pubblicamente prima del fix — il che significa che chiunque potrebbe sviluppare un exploit a breve. Con accesso fisico al dispositivo, è possibile leggere dati protetti da BitLocker. Rilevante soprattutto per laptop aziendali.

## Perché così tante CVE tutte insieme?

La domanda sorge spontanea: come si passa da ~80 a 570 patch in un mese? Microsoft ha risposto apertamente: l'azienda ha iniziato a usare **sistemi AI proprietari per scansionare proattivamente il proprio codebase** alla ricerca di vulnerabilità, trovando i bug prima degli attaccanti.

Il risultato? L'AI scopre falle molto più velocemente di qualsiasi team umano. E quei bug vanno corretti e rilasciati tutti insieme nel ciclo mensile.

È un'arma a doppio taglio: da un lato Microsoft trova e corregge bug prima che vengano sfruttati; dall'altro, lo stesso approccio AI-powered è disponibile anche agli attori malevoli, creando una corsa agli armamenti che accelera continuamente. Il volume di patch crescente è, paradossalmente, un segnale positivo: significa che i bug vengono trovati e chiusi invece di restare silenziosamente aperti.

## Cosa fare se usi Windows (o gestisci una rete mista)

Se sei un utente Linux puro, potresti pensare che questa storia non ti riguardi. Ma se lavori in un ambiente aziendale con macchine Windows, o hai Windows in dual boot o in VM, è il momento di aggiornare:

```
# Su Windows, il modo più rapido:
Impostazioni → Windows Update → Verifica aggiornamenti

# Da PowerShell come amministratore (con il modulo PSWindowsUpdate):
Install-Module PSWindowsUpdate -Force
Get-WindowsUpdate -Install -AcceptAll
```

Se gestisci sistemi aziendali, le CVE più urgenti sono **CVE-2026-56155** (AD FS) e **CVE-2026-56164** (SharePoint), entrambe già sotto attacco attivo. SharePoint in particolare merita attenzione immediata: l'attacco non richiede credenziali e funziona via rete.

## Il trend preoccupante (e inevitabile)

570 patch in un mese non è solo un numero impressionante — è un indicatore di come sta cambiando la sicurezza informatica nell'era dell'AI. Man mano che i sistemi automatizzati vengono usati per trovare vulnerabilità (sia dai vendor che dagli attaccanti), il ritmo della scoperta accelera esponenzialmente.

Per chi lavora in sicurezza informatica, questo significa un carico di patching e monitoraggio sempre più intenso. Per tutti gli altri, significa che ignorare gli aggiornamenti è diventato ancora più rischioso. Un sistema non aggiornato oggi è un bersaglio molto più facile di quanto non fosse anche solo un anno fa.

L'unica risposta sensata è automatizzare il patching dove possibile e avere una chiara prioritizzazione delle CVE critiche. Non si può più fare tutto a mano.
