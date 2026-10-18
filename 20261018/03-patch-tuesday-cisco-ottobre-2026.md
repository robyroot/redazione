---
title: "Patch Tuesday ottobre 2026: 1.400+ CVE Microsoft e una falla Cisco già sfruttata"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/cisco-warns-of-active-attacks.html"
data_notizia: "2026-10-14"
tags: ["sicurezza", "vulnerabilità", "microsoft", "cisco", "patch", "windows"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: sicurezza pratica. Dividere tra utenti Windows (Patch Tuesday)
  e sysadmin/aziende (Cisco, Nextcloud). Dare priorità chiarissima su cosa aggiornare subito.
  La vulnerabilità Cisco è già sfruttata in the wild: alta urgenza.
---

# Patch Tuesday ottobre 2026: 1.400+ CVE Microsoft e una falla Cisco già sfruttata

Il 13 ottobre Microsoft ha pubblicato il suo aggiornamento mensile di sicurezza, e questa volta i numeri fanno impressione: **oltre 1.400 vulnerabilità corrette**, di cui 69-78 classificate come critiche (le fonti variano leggermente nel conteggio). Ma è una vulnerabilità di Cisco, comunicata il giorno dopo, quella che merita attenzione immediata.

## Cisco Secure Email Gateway: patch subito

La notizia più urgente è questa: Cisco ha avvisato che esiste una **vulnerabilità critica nel Cisco Secure Email Gateway** (il sistema usato da molte aziende per filtrare le email) che è già attivamente sfruttata dagli attaccanti.

La falla permette a chiunque — senza autenticazione, semplicemente inviando un'email appositamente costruita — di **scrivere file arbitrari sul sistema operativo** dell'appliance. Praticamente significa controllo remoto della macchina per chi sa come sfruttarla.

Se la tua organizzazione usa Cisco Secure Email Gateway, non aspettare: aggiorna subito.

```bash
# Verifica la versione installata dall'interfaccia CLI Cisco
show version

# Controlla il bollettino Cisco per la versione corretta
# https://sec.cloudapps.cisco.com/security/center/
```

Questo tipo di vulnerabilità — scrittura arbitraria di file su un gateway email — è particolarmente pericolosa perché il gateway email è per definizione un sistema che riceve traffico da Internet, spesso prima di qualunque altro firewall applicativo.

## Microsoft Patch Tuesday: le cose importanti da sapere

Con 1.400+ CVE è impossibile analizzarle tutte, ma ci sono alcune cose su cui vale la pena concentrarsi:

**CVE-2026-96951 – Windows Shell Security Feature Bypass**: questa è la vulnerabilità già sfruttata attivamente, già nel catalogo CISA KEV (Known Exploited Vulnerabilities). Non è classificata come critica, ma è quella più urgente perché gli attaccanti la stanno usando adesso.

**CVE-2026-100219 e CVE-2026-105016**: entrambe riguardano vulnerabilità nel protocollo QUIC, con CVSS 9.8 su 10. Un punteggio quasi perfetto nel mondo della sicurezza è un segnale chiarissimo.

**CVE-2026-70187 – Windows Remote Desktop Gateway**: falla che permette esecuzione di codice remota senza autenticazione, tramite pacchetti di rete appositamente costruiti. Se usi RD Gateway esposto su Internet, questo è il tuo nemico del mese.

## Come aggiornare Windows (e perché farlo subito)

Se usi Windows su computer personali o aziendali, il modo più diretto è:

```
Impostazioni → Windows Update → Verifica aggiornamenti
```

Da PowerShell (con privilegi di amministratore) puoi forzare il controllo:

```powershell
Get-WindowsUpdate -Install -AcceptAll -AutoReboot
```

Se gestisci una flotta aziendale con WSUS o Intune, dai la priorità ai sistemi con RD Gateway esposto e verifica che CVE-2026-96951 sia tra i patch inclusi nel ciclo corrente.

## Attenzione anche a Nextcloud

Un'altra vulnerabilità da tenere d'occhio è **CVE-2026-110447**, che riguarda l'app **Collabora Online Built-in CODE Server** per Nextcloud. Se usi Nextcloud con l'editing collaborativo di documenti integrato, questa falla è segnalata come già sfruttata.

La correzione è disponibile nell'app store di Nextcloud. Per aggiornare:

```bash
# Con l'interfaccia web: Admin → App → Collabora Online
# Da riga di comando:
php occ app:update richdocuments
```

## E su Linux?

Linux 7.3 (rilasciato oggi, vedi l'articolo dedicato) porta alcune correzioni di sicurezza, come ogni ciclo kernel. Nulla di comparabile per urgenza alle vulnerabilità Windows o Cisco sopra descritte, ma se sei su una versione kernel datata è sempre buon momento per aggiornare.

## Priorità di patching per questa settimana

In ordine di urgenza:

1. **Cisco Secure Email Gateway** — vulnerabilità già sfruttata, aggiorna immediatamente
2. **Windows (CVE-2026-96951)** — già nel catalogo CISA KEV, sfruttata attivamente
3. **Windows RD Gateway (CVE-2026-70187)** — critica, specie se esposta su Internet
4. **Nextcloud + Collabora Online** — sfruttata in the wild
5. **QUIC su Windows (CVE-2026-100219/105016)** — CVSS 9.8, alta priorità anche se non ancora sfruttata

Il messaggio di questo Patch Tuesday è lo stesso di ogni mese, ma stavolta più forte del solito: **aggiorna prima che lo faccia qualcun altro per te**.
