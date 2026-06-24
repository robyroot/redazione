---
title: "Secure Boot su Linux: il certificato Microsoft scade il 27 giugno — cosa fare adesso"
rilevanza: "ALTA"
fonte: "https://linuxlap.com/news/secure-boot-linux-2026/"
data_notizia: "2026-06-20"
tags: ["secure-boot", "linux", "sicurezza", "uefi", "grub"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: notizia urgente con scadenza a 3 giorni. Tutta la stampa italiana ha coperto solo il lato Windows/enterprise. Questo articolo si rivolge agli utenti Linux: come capire se si è a rischio, come aggiornare shim su Fedora/Ubuntu/Debian, e perché la stragrande maggioranza non ha nulla di cui preoccuparsi (ma è bene saperlo).
---

# Secure Boot su Linux: il certificato Microsoft scade il 27 giugno — cosa fare adesso

**Tre giorni.** Il 27 giugno 2026 scade il certificato `Microsoft UEFI CA 2011`, quello che da quindici anni firma i bootloader Linux per funzionare con Secure Boot attivo. Se usi Linux con Secure Boot abilitato (e molti lo fanno senza nemmeno saperlo), vale la pena capire cosa sta per cambiare — e soprattutto, se devi fare qualcosa entro giovedì.

La buona notizia: la maggior parte degli utenti non ha nulla da fare. Ma per qualcuno potrebbe essere un problema serio, ed è meglio scoprirlo adesso.

## Cos'è Secure Boot e perché c'entra Microsoft

Secure Boot è una funzionalità del firmware UEFI che verifica la firma digitale del bootloader prima di caricarlo. L'idea è impedire che software malevolo si inserisca nel processo di avvio prima ancora che il sistema operativo parta.

Su Linux la catena funziona così: il firmware UEFI si fida dei certificati presenti nel database `db`. Il bootloader Linux, chiamato **shim**, è firmato con il certificato Microsoft — e quindi il firmware lo accetta. Shim a sua volta verifica GRUB, che verifica il kernel.

Il problema è che il certificato `Microsoft UEFI CA 2011` scade il 27 giugno. Dopo quella data, quel certificato non potrà più essere usato per firmare nuovi binari. I sistemi già aggiornati con il nuovo certificato (Microsoft UEFI CA 2023) non noteranno niente. I sistemi vecchi che non riescono ad aggiornare il firmware potrebbero invece trovarsi in difficoltà in futuro, soprattutto se avranno bisogno di installare un nuovo bootloader firmato.

## Il rischio reale: chi è davvero a rischio

Chiariamo subito: **il tuo sistema non smette di avviarsi il 28 giugno**. La scadenza del certificato non tocca i binari già firmati e già caricati sul tuo sistema. Il problema si pone solo quando devi installare un nuovo bootloader (ad esempio dopo una reinstallazione, un aggiornamento critico di shim, o su hardware nuovo).

I sistemi a rischio sono principalmente:
- Server fisici vecchi o appliance che non ricevono aggiornamenti firmware da anni
- Laptop/desktop molto datati con UEFI antichi bloccati dal produttore
- Sistemi embedded con Secure Boot configurato in modo rigido

Se hai un PC acquistato negli ultimi tre o quattro anni e mantieni aggiornato il sistema, probabilmente hai già il nuovo certificato 2023 installato nel firmware o in arrivo via aggiornamento automatico.

## Come verificare la situazione sul tuo sistema

Per prima cosa, controlla se Secure Boot è attivo:

```bash
mokutil --sb-state
```

Se risponde `SecureBoot disabled`, puoi stare tranquillo: Secure Boot non è abilitato sul tuo sistema e questa vicenda non ti riguarda.

Se è abilitato, verifica quale versione di shim hai installato:

```bash
# Su sistemi RPM (Fedora, RHEL, AlmaLinux, Rocky Linux)
rpm -q shim-x64

# Su sistemi DEB (Debian, Ubuntu, Linux Mint)
dpkg -l shim-signed
```

Per vedere i certificati nel firmware:

```bash
mokutil --list-enrolled
```

Cerca `Microsoft UEFI CA 2023`: se lo vedi, sei già al sicuro.

## Come aggiornare shim sulle principali distribuzioni

### Fedora / RHEL / AlmaLinux / Rocky Linux

Red Hat ha già distribuito la nuova versione di shim firmata con entrambi i certificati (2011 e 2023). Basta aggiornare:

```bash
sudo dnf update shim-x64
```

### Ubuntu / Linux Mint

Canonical ha rilasciato l'aggiornamento via `shim-signed`. Se hai gli aggiornamenti automatici di sicurezza attivi, probabilmente è già installato. Verifica con:

```bash
sudo apt update && sudo apt install --only-upgrade shim-signed
```

### Debian

```bash
sudo apt update && sudo apt upgrade shim-signed
```

Dopo l'aggiornamento di shim, su alcuni sistemi potrebbe essere necessario un reboot per permettere al firmware di registrare il nuovo certificato.

## Cosa succede ai sistemi che non possono aggiornarsi

Se hai un server vecchio o un sistema embedded il cui firmware non può ricevere il certificato 2023, il sistema **continuerà comunque ad avviarsi** con la versione di shim attualmente installata. Il rischio si concretizza solo se in futuro ti servirà installare un nuovo shim (reinstallazione, recovery, ecc.) e il firmware non accetterà quello firmato solo con il certificato 2023.

In quel caso, l'unica soluzione è disabilitare temporaneamente Secure Boot durante l'installazione, o aggiungere manualmente il nuovo certificato al database del firmware usando `mokutil`:

```bash
# Aggiungere manualmente un certificato al MOK database
mokutil --import nuovo-certificato.der
```

## La lezione più grande

Questa storia ci ricorda qualcosa di fondamentale: **la catena di fiducia del boot dipende da infrastrutture che scadono**. Il certificato del 2011 ha retto quindici anni, ma prima o poi tutte le PKI devono fare manutenzione. La buona notizia è che il settore (Red Hat, Canonical, SUSE, Microsoft) si è organizzato per tempo — almeno per chi mantiene i propri sistemi aggiornati.

Se gestisci server Linux in produzione con Secure Boot abilitato, controlla lo stato adesso. Tre giorni sono pochi, ma sono ancora sufficienti per aggiornare shim prima della scadenza.
