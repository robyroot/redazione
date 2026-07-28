---
title: "Patch Tuesday Luglio 2026: Microsoft corregge 570 vulnerabilità con 3 zero-day in uso"
rilevanza: "ALTA"
fonte: "https://www.bleepingcomputer.com/news/microsoft/microsoft-july-2026-patch-tuesday-fixes-massive-570-flaws-3-zero-days/"
data_notizia: "2026-07-14"
tags: ["sicurezza", "microsoft", "windows", "patch", "zero-day", "CVE", "sharepoint"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: pur essendo su Windows, molti lettori hanno macchine Windows
  per lavoro o gestiscono ambienti misti. Focalizzarsi sulle tre zero-day più critiche (SharePoint,
  Fortinet) con contesto pratico. Aggiungere nota su perché i lettori Linux dovrebbero comunque
  prestare attenzione.
---

# Patch Tuesday Luglio 2026: Microsoft corregge 570 vulnerabilità con 3 zero-day

Luglio 2026 entrerà nella storia per il **Patch Tuesday più grande di sempre**: Microsoft ha
rilasciato aggiornamenti di sicurezza che coprono la bellezza di **570 vulnerabilità**, di cui 59
critiche e tre zero-day già sfruttati da attaccanti reali prima che la patch fosse disponibile.

Anche se usi Linux come sistema principale, questo è un aggiornamento che vale la pena conoscere.

## I numeri da record

- **570 vulnerabilità** corrette in un solo ciclo mensile (il precedente record era ben più basso)
- **59 vulnerabilità critiche**, suddivise in:
  - 48 di tipo Remote Code Execution (RCE) — esecuzione di codice da remoto
  - 9 di tipo Elevation of Privilege — scalata di privilegi
  - 1 Security Bypass e 1 Spoofing
- **3 zero-day** sfruttati attivamente in attacchi reali prima della patch

La CISA (l'agenzia americana per la cybersicurezza) ha già ordinato a tutte le agenzie federali
statunitensi di correggere le vulnerabilità più critiche entro il 19 luglio — un segnale di quanto
la situazione sia stata presa sul serio.

## Le tre zero-day da conoscere

### CVE-2026-58644 — Microsoft SharePoint (CVSS 9.8)

La più pericolosa del lotto. Si tratta di una **deserializzazione di dati non affidabili** in
SharePoint Server 2016 che permette l'esecuzione di codice da remoto senza nessuna autenticazione,
via rete. Un attaccante da internet può prendere il controllo di un server SharePoint esposto
senza dover possedere nemmeno un account.

Se la tua organizzazione usa SharePoint on-premise (non solo la versione cloud), questa è
priorità assoluta.

### CVE-2026-25089 e CVE-2026-39808 — Fortinet FortiSandbox (CVSS 9.1)

Entrambe le vulnerabilità sono **OS command injection** su Fortinet FortiSandbox — un prodotto
enterprise usato per analizzare file sospetti in ambienti isolati. Un attaccante non autenticato
può eseguire comandi arbitrari sul sistema, compromettendo di fatto lo strumento pensato per
proteggere gli altri sistemi.

L'ironia è pungente: la sandbox usata per analizzare malware diventa essa stessa un vettore di
attacco. Entrambe le CVE sono nel catalogo KEV della CISA.

## Perché 570 vulnerabilità in un mese?

La crescita esponenziale nel numero di CVE mensili non significa necessariamente che il software
sia diventato peggiore. Riflette anche un ecosistema di security research più maturo: più bug
bounty, più ricercatori, più strumenti automatici di analisi del codice. Detto questo, 570 in un
mese è un numero che fa alzare un sopracciglio.

## Cosa fare se usi Windows

Aggiornare il sistema è la risposta principale. In PowerShell:

```powershell
# Avvia il processo di aggiornamento
Start-Process ms-settings:windowsupdate
```

Oppure il percorso classico: **Impostazioni → Windows Update → Verifica aggiornamenti**.

Per chi gestisce macchine Windows in ambiente aziendale, la priorità deve essere:
1. **SharePoint on-premise** → patch immediata, non aspettare il ciclo ordinario
2. **FortiSandbox** → verifica versione e aggiorna all'ultima release
3. **Macchine esposte su internet** → sempre massima priorità

## Perché un lettore Linux dovrebbe preoccuparsi

Buona domanda. Molti di noi vivono in ambienti misti: magari usi Linux sul tuo portatile ma la
tua azienda ha file server Windows, SharePoint, o appliance Fortinet in rete. Un attacco su
SharePoint non si ferma al confine Windows/Linux — colpisce dati, servizi e infrastruttura
condivisa.

Tenersi informati sul panorama delle vulnerabilità è buona igiene digitale, indipendentemente dal
sistema operativo che usi personalmente.

## Conclusione: aggiornare sempre, aggiornare subito

Il Patch Tuesday di luglio 2026 non ha precedenti per dimensioni. Se gestisci Windows o prodotti
Microsoft in qualsiasi forma, è il momento di aggiornare senza rimandare. Per le zero-day critiche
come SharePoint CVE-2026-58644, ogni giorno di ritardo è un giorno di esposizione concreta.

Il calendario aziendale può aspettare. L'aggiornamento no.
