---
title: "Patch Tuesday ottobre 2026: 1.413 CVE, un zero-day di Windows Shell già sfruttato e due critical RCE a 9.8"
rilevanza: "ALTA"
fonte: "https://www.crowdstrike.com/en-us/blog/patch-tuesday-analysis-october-2026/"
data_notizia: "2026-10-13"
tags: ["windows", "sicurezza", "patch", "microsoft", "CVE", "zero-day"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: vai oltre il semplice comunicato e spiega quali CVE sono davvero urgenti per chi ha infrastrutture miste Windows/Linux. Metti in evidenza il MSMQ e il Remote Desktop Gateway perché sono componenti comuni in ambienti enterprise italiani. Utile aggiungere un reminder su come verificare lo stato di MSMQ e RDG sulla propria macchina.
---

# Patch Tuesday ottobre 2026: il mese più affollato dell'anno con 1.413 CVE e uno zero-day attivo

Microsoft ha rilasciato il suo aggiornamento mensile martedì 13 ottobre 2026, ed è uno dei Patch Tuesday più pesanti di sempre: **oltre 1.400 vulnerabilità risolte**, di cui 75–80 classificate come Critiche, più **uno zero-day già sfruttato attivamente** e due zero-day pubblicamente divulgati.

Se gestisci macchine Windows (o infrastrutture miste), questo mese hai qualcosa da fare subito.

## Lo zero-day che conta: CVE-2026-96951 in Windows Shell

Il bug più urgente è **CVE-2026-96951**, con un punteggio CVSS di **8.8**, e si trova nel componente Windows Shell. È l'unica vulnerabilità confermata come "under active exploitation" in questo ciclo, il che significa che qualcuno sta già usando exploit funzionanti contro sistemi reali.

I dettagli tecnici completi non sono ancora pubblici (Microsoft li trattiene nelle prime settimane per non agevolare i copycats), ma il fatto che sia in Windows Shell — il componente che gestisce l'interfaccia utente, le estensioni e la gestione dei file — significa che potenzialmente può essere sfruttato attraverso azioni comuni come aprire una cartella o visualizzare un'anteprima.

**Aggiorna subito Windows Update** se non l'hai già fatto.

## Le due RCE più pericolose: CVSS 9.8

Oltre allo zero-day, ci sono due vulnerabilità di esecuzione remota di codice (RCE) con punteggio CVSS massimo di **9.8**:

### CVE-2026-100219 e CVE-2026-105016 — Microsoft QUIC

Entrambe riguardano l'implementazione Microsoft del protocollo **QUIC** (il layer di trasporto usato da HTTP/3). Un attaccante può inviare pacchetti di rete appositamente costruiti e potenzialmente eseguire codice arbitrario sul sistema bersaglio — senza autenticazione.

Se la tua infrastruttura usa server Windows esposti su internet con HTTP/3 abilitato, questi bug meritano attenzione immediata.

### CVE-2026-70187 — Remote Desktop Gateway (RDG)

Questo è critico per chi ha infrastrutture enterprise: una RCE non autenticata nel **Remote Desktop Gateway**, il componente che permette l'accesso remoto sicuro a desktop Windows attraverso HTTPS.

```powershell
# Verifica se Remote Desktop Gateway è installato/attivo sul tuo server
Get-WindowsFeature RDS-Gateway

# Se attivo e non aggiornato, questo sistema è a rischio
# Applica le patch di ottobre immediatamente
```

Il RDG è comunissimo nelle aziende italiane come soluzione di accesso remoto, spesso esposto direttamente su internet. Se non hai applicato le patch di ottobre, fallo adesso.

## MSMQ: altro vettore da tenere d'occhio

**CVE-2026-100202** è una use-after-free in **Microsoft Message Queuing (MSMQ)** con CVSS 9.8. La buona notizia è che MSMQ non è abilitato di default sulle installazioni moderne di Windows. La cattiva è che nelle infrastrutture enterprise legacy è ancora molto diffuso.

```powershell
# Controlla se MSMQ è attivo sulla tua macchina
Get-Service -Name MSMQ -ErrorAction SilentlyContinue

# Se non lo usi attivamente, disabilitalo
Stop-Service MSMQ
Set-Service MSMQ -StartupType Disabled
```

## Oltre Microsoft: MikroTik e un CVSS 10.0

Action1 segnala anche due vulnerabilità critiche fuori dall'ecosistema Microsoft degne di nota:

- **CVE-2026-67276** (CVSS 9.2) in **MikroTik RouterOS**: un attaccante può forgiare una firma SSH senza avere la chiave privata. Se hai router MikroTik in rete, aggiorna subito RouterOS.
- **CVE-2026-100103** (CVSS **10.0**) in un prodotto IBM — il punteggio massimo è raro e va trattato come priorità assoluta.

## Come aggiornare in modo ordinato

```bash
# Su Linux con infrastruttura mista, usa Ansible per forzare gli aggiornamenti Windows
# (se hai WinRM configurato)
ansible windows_servers -m win_updates -a "category_names=SecurityUpdates state=installed"

# Oppure verifica lo stato degli aggiornamenti via PowerShell remoto
Invoke-Command -ComputerName server1,server2 -ScriptBlock {
    Get-HotFix | Sort-Object InstalledOn -Descending | Select-Object -First 5
}
```

Il consiglio generale: non rimandare le patch di sicurezza oltre 72 ore dalla release, specialmente quando c'è uno zero-day già sfruttato. Il numero record di CVE di questo mese segnala una tendenza preoccupante — tenersi aggiornati diventa sempre più impegnativo, ma non farlo è peggio.
