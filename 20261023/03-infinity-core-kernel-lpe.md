---
title: "Infinity Core: sei falle nel kernel Linux portano a root — cosa devi fare subito"
rilevanza: "ALTA"
fonte: "https://lilting.ch/en/articles/linux-infinity-core-kernel-lpe"
data_notizia: "2026-10-17"
tags: ["sicurezza", "linux", "kernel", "vulnerabilità", "privilege-escalation", "patch"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: articolo tecnico ma accessibile. Spiega cosa sono le LPE, quali distro sono colpite, come verificare se il proprio kernel è aggiornato. Utile sia per utenti desktop che per sysadmin.
---

# Infinity Core: sei falle nel kernel Linux portano a root — cosa devi fare subito

Il 17 ottobre 2026 il ricercatore coreano Hyunwoo Kim (conosciuto come V4bel) ha pubblicato dettagli tecnici completi e codice exploit per **sei vulnerabilità nel kernel Linux** raggruppate sotto il nome "Infinity Core". Cinque delle sei permettono di **scalare i privilegi da utente normale a root** — e di scappare dai container. La sesta causa un kernel panic.

Brutta settimana per chi amministra sistemi Linux.

## Cosa sono le LPE e perché preoccupano

LPE sta per *Local Privilege Escalation*: una vulnerabilità che non permette di entrare in un sistema dall'esterno, ma che consente a un utente già loggato (o a un processo già in esecuzione) di ottenere i permessi di root.

Sembra meno grave di una RCE remota, ma è estremamente pericolosa in diversi scenari reali:

- **Hosting condiviso**: un cliente malintenzionato può compromettere l'intero server.
- **Container escape**: i container cloud (Docker, LXC, Kubernetes) usano il kernel del host. Con queste falle si può uscire dall'isolamento e arrivare al sistema fisico.
- **Post-exploitation**: un attaccante che ha già un accesso limitato (tramite una vulnerabilità applicativa) usa una LPE per completare il controllo del sistema.
- **Android**: Kim ha confermato che la falla Timer permette di ottenere full root su Samsung Galaxy S26 Ultra dall'interno di una normale app. L'exploit Android è trattenuto in attesa che Samsung rilasci le patch.

## Le sei falle di Infinity Core

Le vulnerabilità riguardano componenti fondamentali del kernel:

| Nome | Subsystem | Tipo | CVE |
|------|-----------|------|-----|
| Timer | Timer | LPE + container escape | CVE-2026-98260 (CVSS 7.8) |
| Signal | Signal | LPE + container escape | — |
| MM | Memory Management | LPE + container escape | — |
| Futex | Futex | LPE | — |
| Scheduler | Scheduler | LPE | — |
| SLAB | SLAB allocator | Kernel panic | — |

La falla Timer (CVE-2026-98260) è quella con più impatto, perché funziona anche su Android. Le altre CVE non sono state ancora tutte assegnate ufficialmente al momento della pubblicazione.

## Quali distro sono colpite

Non tutte le distro sono uguali: dipende da quali backport del kernel hanno applicato.

- **Debian 12/13 e Ubuntu 24.04 stock**: vulnerabili solo alla falla Timer.
- **RHEL/CentOS/Rocky Linux**: vulnerabili a Futex e Signal, a causa di backport specifici.
- **Kernel mainline non aggiornato**: potenzialmente esposto a tutte e sei.
- **Arch Linux, openSUSE Tumbleweed**: aggiornamenti rolling, il kernel è stato patchato rapidamente.

Il write-up originale su Lilting.ch riporta una mappa dettagliata di quali distro vengono colpite da quali falle.

## Come verificare il kernel e aggiornare

Per prima cosa, controlla la versione del kernel che stai usando:

```bash
uname -r
# Esempio output: 7.3.5-arch1-1
```

### Aggiornamento su Ubuntu/Debian

```bash
sudo apt update && sudo apt upgrade linux-image-generic -y
sudo reboot
```

### Aggiornamento su Fedora/RHEL

```bash
sudo dnf update kernel -y
sudo reboot
```

### Aggiornamento su Arch Linux

```bash
sudo pacman -Syu
sudo reboot
```

Dopo il riavvio, verifica di stare girando sul kernel aggiornato:

```bash
uname -r
```

Se stai usando un kernel LTS (Long Term Support) su una distro stabile, controlla se il tuo provider ha già rilasciato la patch per il tuo branch specifico. Ubuntu Security Notices e i bollettini RHEL sono le fonti più affidabili.

## Un dettaglio sulla divulgazione responsabile

Kim ha seguito il processo di *responsible disclosure* concordando un embargo con i maintainer di linux-distros. Le patch upstream erano pronte prima della pubblicazione, e le principali distro avevano ricevuto la notifica in anticipo.

L'embargo è scaduto il 17 ottobre e Kim ha pubblicato tutto: analisi, PoC e dettagli tecnici. Una pratica standard nel mondo della sicurezza, che incentiva le aziende a patchare velocemente sapendo che l'embargo ha una scadenza.

## Conclusione

Infinity Core è un cluster di vulnerabilità serio, ma gestibile. Le patch esistono, le distro le hanno già distribuite, e nessuno sfruttamento attivo di massa è stato confermato. L'azione corretta è semplice: **aggiorna il kernel, riavvia il sistema**.

Se gestisci server in produzione, aggiungi anche un controllo periodico delle versioni del kernel al tuo workflow di manutenzione. Nel 2026 tenere i kernel Linux aggiornati non è più opzionale.
