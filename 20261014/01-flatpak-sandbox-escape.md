---
title: "Flatpak: falla critica permette l'escape dalla sandbox, aggiorna subito"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/flatpak-1-18-1-fixes-sandbox-escape-and-root-privilege-escalation-flaws/"
data_notizia: "2026-08-11"
tags: ["flatpak", "sicurezza", "linux", "cve", "sandbox", "privilege-escalation"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: sicurezza pratica per utenti desktop Linux.
  Molti lettori usano Flatpak ogni giorno senza sapere che una versione vulnerabile
  può compromettere l'intero sistema. Articolo utile con comandi immediati per
  verificare e aggiornare la versione installata.
---

# Flatpak: falla critica permette l'escape dalla sandbox — aggiorna subito

Se usi Flatpak per installare applicazioni su Linux (e probabilmente lo fai, visto che ormai è ovunque), c'è una notizia che non puoi ignorare. Ad agosto 2026 sono state scoperte e corrette circa **dieci vulnerabilità critiche** in Flatpak, alcune delle quali consentono di uscire completamente dalla sandbox e persino di ottenere i privilegi di root.

Il tutto è stato risolto nelle versioni 1.18.1 e successive, ma il problema vero è che molte distribuzioni potrebbero ancora distribuire versioni vulnerabili nei loro repository stabili.

## Cos'è successo esattamente?

Flatpak nasce proprio per isolare le applicazioni dal resto del sistema — la famosa "sandbox". L'idea è che un'app Flatpak non dovrebbe poter accedere a file al di fuori della sua area riservata. Bene, questa garanzia è stata completamente violata da una serie di bug concatenati.

**Il bug principale (CVE-2026-90616)** sfruttava i symlink nelle cartelle dati dell'applicazione. Un'app malevola poteva creare un symlink costruito ad arte all'interno della propria directory `/var/data`, e Flatpak — fidandosi ciecamente del path — lo montava dentro la sandbox tramite `bwrap --bind`. Risultato: accesso completo in lettura e scrittura al filesystem dell'host.

In parole povere: un'app apparentemente innocua poteva leggere i tuoi file privati, le tue chiavi SSH, le tue password salvate in `~/.gnupg`, e molto altro ancora.

## Escalation a root: il sistema revokefs

Non bastasse l'escape dalla sandbox, un altro bug nel componente `revokefs` permetteva a un utente locale non privilegiato di **scrivere file con privilegi di root** al di fuori di `/var/lib/flatpak`. Anche questo sfruttava una vulnerabilità di path traversal via symlink.

Sono stati corretti anche:
- Path traversal durante l'estrazione di app con dati extra
- Buffer overflow a 32 bit nel codice OCI
- Un buco che permetteva il **downgrade di applicazioni già installate** senza permessi

## Come capire se sei vulnerabile

Apri un terminale e digita:

```bash
flatpak --version
```

Se vedi una versione inferiore a **1.18.4**, sei vulnerabile. La versione 1.18.1 ha tappato i buchi principali, ma 1.18.2, 1.18.3 e 1.18.4 hanno aggiunto ulteriori correzioni scoperte in seguito — quindi punta direttamente alla più recente.

Per aggiornare Flatpak stesso (non le app Flatpak), devi passare dal package manager della tua distro:

```bash
# Fedora / RHEL / openSUSE
sudo dnf upgrade flatpak

# Debian / Ubuntu
sudo apt update && sudo apt upgrade flatpak

# Arch Linux
sudo pacman -Syu flatpak
```

Dopo l'aggiornamento, verifica di nuovo la versione:

```bash
flatpak --version
# Output atteso: Flatpak 1.18.4 o superiore
```

## Aggiorna anche le app Flatpak

Mentre ci sei, approfitta per aggiornare tutte le applicazioni installate tramite Flatpak:

```bash
flatpak update
```

Questo scarica gli aggiornamenti per tutte le app da tutti i repository configurati (Flathub incluso).

## Il problema della distribuzione lenta

La notizia meno piacevole è la seguente: anche se Flatpak 1.18.1 è stato rilasciato ad agosto, molte distribuzioni non hanno aggiornato immediatamente i propri repository stabili. Questo è il classico tallone d'Achille del modello "distro stabile": la sicurezza viene sacrificata a favore della stabilità percepita.

Se usi una distro con ciclo di rilascio lento (Debian stable, Ubuntu LTS, ecc.), controlla manualmente la versione di Flatpak disponibile e considera se passare temporaneamente al repository di backports o unstable finché la patch non arriva nei canali ufficiali.

## Conclusione

Questa serie di vulnerabilità è un promemoria importante: la sandbox di Flatpak non è magica, e quando viene violata può compromettere l'intero sistema. Aggiornare subito è la cosa giusta da fare — e richiede letteralmente meno di un minuto.

Se vuoi approfondire i dettagli tecnici, il thread originale su oss-security è un'ottima lettura.
