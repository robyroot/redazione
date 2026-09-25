---
title: "Microsoft Patch Tuesday settembre 2026: 974 vulnerabilità e due zero-day già sfruttati"
rilevanza: "ALTA"
fonte: "https://www.crowdstrike.com/en-us/blog/patch-tuesday-analysis-september-2026/"
data_notizia: "2026-09-09"
tags: ["cybersecurity", "Windows", "patch", "zero-day", "vulnerabilità", "Microsoft"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: focalizzarsi su come proteggersi concretamente, con un occhio ai sistemi Linux come alternativa più sicura. Utile per sensibilizzare i lettori sull'importanza degli aggiornamenti tempestivi.
---

# Microsoft Patch Tuesday settembre 2026: 974 vulnerabilità e due zero-day già sfruttati

Se pensavi che i mesi scorsi fossero stati pesanti in termini di patch Microsoft, settembre 2026 ha alzato ulteriormente l'asticella. Il Patch Tuesday di questo mese ha stabilito un record assoluto con **974 CVE corretti in un colpo solo**, rendendolo il più grande aggiornamento mensile mai rilasciato da Redmond. Non è solo una questione di numeri: tra le patch ci sono due zero-day attivamente sfruttati e una vulnerabilità con punteggio CVSS massimo di 10.0.

## Il numero record e cosa significa

974 vulnerabilità corrette in un solo ciclo mensile non è una cosa da prendere alla leggera. Per darti un'idea, il precedente record era intorno alle 700. Questo balzo gigantesco riflette sia la complessità crescente dell'ecosistema Microsoft sia, probabilmente, un ritardo accumulato nella disclosure di vulnerabilità note.

Tra le 974 CVE, si contano:
- **113 vulnerabilità classificate come Critical**
- **2 zero-day attivamente sfruttati in the wild**
- **857 vulnerabilità di severità variabile**

## I due zero-day da tenere d'occhio

I due zero-day riguardano l'escalation di privilegi su Windows. Questo tipo di vulnerabilità è particolarmente pericoloso perché un attaccante che ha già un accesso limitato al tuo sistema può usarla per ottenere i privilegi di amministratore o SYSTEM, prendendo di fatto il controllo completo della macchina.

Se usi Windows in ambito lavorativo o gestisci server Windows, questi due CVE devono essere la tua priorità assoluta. Microsoft li ha già visti sfruttati attivamente, il che significa che i criminali informatici li stanno usando adesso.

## La CVSS 10.0: l'autenticazione bypass su Azure AI Foundry

Tra le vulnerabilità critiche spicca un authentication bypass in **Azure AI Foundry** con punteggio CVSS 10.0 — il massimo possibile. Una CVE con questo punteggio significa che la vulnerabilità è:

- Sfruttabile da remoto senza autenticazione
- Di bassa complessità (facile da sfruttare)
- Capace di compromettere completamente il sistema

In pratica, un attaccante non autenticato in rete potrebbe eseguire codice arbitrario. Se la tua azienda usa Azure AI Foundry, applica immediatamente le patch.

## Il problema RDS: attenzione in ambienti enterprise

C'è anche una regressione critica in RDS (Remote Desktop Services) che sta causando problemi di autenticazione di dominio e deadlock di sessioni Remote Desktop in ambienti enterprise. Se usi Active Directory e Remote Desktop, potresti già avere problemi dopo l'aggiornamento — ironicamente, la patch stessa introduce un comportamento anomalo su certi setup.

```bash
# Su Linux, puoi verificare i servizi RDP esposti sulla tua rete con nmap:
nmap -p 3389 --open 192.168.1.0/24
```

## Microsoft Office: attenzione al Preview Pane

Una delle cose più preoccupanti di questo Patch Tuesday riguarda Microsoft Office: **22 patch critiche**, di cui 12 sfruttabili semplicemente aprendo il pannello di anteprima di un file. Nessun clic, nessun allegato aperto, nessuna macro: basta che il client email visualizzi l'anteprima di un documento malevolo per compromettere il sistema.

Questo tipo di attacco è particolarmente subdolo perché gli utenti tendono a fidarsi dell'anteprima, pensando che "guardare" un file non possa essere pericoloso.

## Come proteggersi

Le azioni immediate da fare:

```powershell
# Su Windows, forza la verifica degli aggiornamenti:
# Start > Impostazioni > Windows Update > Verifica aggiornamenti

# Da PowerShell come amministratore:
Get-WindowsUpdate -Install -AcceptAll -AutoReboot
```

Per gli amministratori di sistema in ambienti misti Linux/Windows, questo è un buon momento per rivalutare quali sistemi devono necessariamente girare su Windows e quali possono essere migrati. Le vulnerabilità di questo mese riguardano quasi esclusivamente l'ecosistema Microsoft.

## Il punto di vista Linux

Dal lato Linux, il kernel 7.2 — utilizzato nelle distribuzioni più recenti come Fedora 45 e openSUSE Tumbleweed — ha ricevuto aggiornamenti di sicurezza di routine questa settimana, nulla di paragonabile alla portata di quanto visto su Windows. Non è una critica gratuita: è semplicemente un fatto che la superficie d'attacco e i processi di patch management differiscono profondamente tra i due ecosistemi.

Se gestisci infrastrutture miste, questo mese è un ottimo reminder per mantenere i tuoi sistemi Windows aggiornati il più rapidamente possibile.
