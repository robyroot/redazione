---
title: "Attacco supply chain sull'AUR: oltre 1.500 pacchetti Arch Linux compromessi"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/06/over-400-arch-linux-aur-packages.html"
data_notizia: "2026-06-12"
tags: ["security", "arch-linux", "supply-chain", "malware", "aur"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: L'attacco all'AUR è un wake-up call per tutti gli utenti Arch e derivate (Manjaro, EndeavourOS, etc.). Spiega come funziona il processo di adozione dei pacchetti orfani, perché è pericoloso e come proteggersi con best practice concrete. Tono allarmato ma costruttivo.
---

# Attacco supply chain sull'AUR: oltre 1.500 pacchetti Arch Linux compromessi

Se usi Arch Linux, Manjaro, EndeavourOS o qualsiasi altra distribuzione basata su Arch, fermati un momento. Tra il 9 e il 12 giugno 2026 si è consumato uno degli attacchi alla supply chain più gravi che abbia mai colpito il mondo Linux: la campagna "Atomic Arch" ha compromesso oltre 1.500 pacchetti nell'Arch User Repository (AUR).

## Cos'è successo esattamente

L'AUR — l'Arch User Repository — è il repository non ufficiale mantenuto dalla comunità Arch Linux, dove chiunque può pubblicare script di build (PKGBUILD) per installare software non presente nei repo ufficiali. È uno dei punti di forza dell'ecosistema Arch, ma anche la sua principale vulnerabilità.

Gli attaccanti hanno sfruttato il meccanismo di **adozione dei pacchetti orfani**: quando un maintainer abbandona il suo pacchetto, chiunque può richiederne la gestione. I criminali hanno creato decine di account falsi, adottato sistematicamente centinaia di pacchetti abbandonati e modificato i PKGBUILD per includervi codice malevolo.

Il payload veniva attivato tramite script post-install che eseguivano comandi `npm` o `bun install` scaricando un pacchetto chiamato `atomic-lockfile` — da cui il nome della campagna.

## Cosa faceva il malware

Il malware, scritto in Rust, era un infostealer sofisticato progettato per colpire in particolare sviluppatori e ambienti CI/CD. Le sue capacità includevano:

- **Furto di credenziali**: password salvate nel browser, token nel keyring di sistema, chiavi SSH da `~/.ssh`
- **Esfiltrazione di segreti**: variabili d'ambiente con API key, file `.env` nei progetti
- **Rootkit eBPF**: sui sistemi in cui riusciva a ottenere i privilegi di root, installava un rootkit basato su eBPF per la persistenza invisibile
- **Esfiltrazione silenziosa**: tutti i dati venivano inviati a server di comando e controllo remoti

La seconda ondata, scoperta quando gli sviluppatori pensavano di aver risolto il problema, era ancora più preoccupante: il codice era offuscato per eludere le analisi automatiche, segno che gli attaccanti osservavano la risposta difensiva in tempo reale.

## Verificare se sei a rischio

```bash
# Elenca tutti i pacchetti AUR installati sul tuo sistema
pacman -Qm

# Controlla i log di sistema per attività sospette nel periodo dell'attacco
journalctl --since "2026-06-09" --until "2026-06-15" | grep -i "npm\|bun\|atomic-lockfile"

# Usa lo script di detection della community
curl -s https://raw.githubusercontent.com/lenucksi/aur-malware-check/main/check.sh | bash

# Se trovi pacchetti compromessi, rimuovili immediatamente
sudo pacman -R nome-pacchetto-compromesso
```

La lista aggiornata dei pacchetti compromessi è mantenuta su GitHub: [lenucksi/aur-malware-check](https://github.com/lenucksi/aur-malware-check).

## La risposta del team Arch

Appena la portata dell'attacco è diventata evidente, il team Arch Linux ha disabilitato le registrazioni di nuovi account sull'AUR per bloccare ulteriori adozioni malevole. Un'azione necessaria ma che dimostra quanto il sistema fosse esposto: bastava creare account fake per ottenere controllo su pacchetti usati da migliaia di persone.

## Come proteggersi in futuro

L'attacco Atomic Arch non sarà l'ultimo. Il problema è strutturale: l'AUR non ha un processo di revisione del codice. Ecco alcune regole pratiche che vale la pena adottare subito:

**1. Leggi sempre il PKGBUILD prima di installare**. È noioso, lo sappiamo, ma è l'unica difesa reale. Con helper come `paru`, puoi visualizzare le diff prima della compilazione:
```bash
paru -S nome-pacchetto  # chiede conferma e mostra il PKGBUILD
```

**2. Preferisci i repo ufficiali**. Se un software è disponibile in `[extra]` o `[multilib]`, usa quello invece della versione AUR.

**3. Valuta i Flatpak per le app desktop**. Flathub ha un processo di revisione più strutturato e le app girano in sandbox. Non è la soluzione perfetta, ma riduce la superficie di attacco.

**4. Diffida dei pacchetti appena adottati**. Prima di installare un pacchetto AUR, controlla da quanto tempo il maintainer attuale lo gestisce. Un cambio di proprietà recente è un campanello d'allarme.

Questo attacco è un promemoria che nel mondo open source la sicurezza richiede **partecipazione attiva**, non solo fiducia nella comunità. La trasparenza del codice è una garanzia solo se qualcuno si prende il tempo di leggerlo.
