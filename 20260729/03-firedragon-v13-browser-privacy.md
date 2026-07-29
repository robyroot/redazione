---
title: "FireDragon v13: il browser privacy di Garuda Linux si riscrive da zero"
rilevanza: "MEDIA"
fonte: "https://linuxiac.com/firedragon-v13-released-as-a-complete-rewrite-of-garuda-linux-browser/"
data_notizia: "2026-07-26"
tags: ["linux", "browser", "privacy", "Garuda", "Firefox", "fingerprinting", "open source"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: ottimo per chi vuole un browser privacy-first su Linux senza configurare tutto a mano. Confronto con Firefox vanilla e con alternative come Librewolf. Spiegare Resist Fingerprinting e XDG in termini semplici.
---

# FireDragon v13: il browser privacy di Garuda Linux si riscrive da zero

Il 26 luglio 2026 il team di Garuda Linux ha rilasciato **FireDragon v13**, una riscrittura completa del suo browser web basato su Firefox. Non è un aggiornamento incrementale: hanno buttato via il vecchio codice e ricominciato da capo. Il risultato è un browser più mantenibile, meglio integrato con Linux, e con impostazioni privacy ragionevoli già pronte all'uso — senza dover configurare niente a mano.

## Cos'è FireDragon e perché esiste

FireDragon è il browser predefinito di **Garuda Linux**, una distribuzione basata su Arch Linux orientata alla performance e all'estetica. Nasce dalla necessità di avere Firefox con una serie di patch e impostazioni privacy già applicate — una cosa simile a quello che fa LibreWolf, ma con un'identità più legata all'ecosistema Garuda.

Fino alla v12, FireDragon era basato su **Floorp** (un fork di Firefox con molte opzioni di personalizzazione). Con v13, la base è cambiata e l'intero codebase è stato riscritto. La scelta degli sviluppatori è stata prioritizzare la manutenibilità a lungo termine rispetto alla quantità di feature.

## Cosa c'è di nuovo: il Welcome Dialog

La novità più immediata per chi installa o aggiorna FireDragon è il **nuovo Welcome Dialog**: al primo avvio si apre una schermata di configurazione che ti chiede subito le tue preferenze. Niente da cercare nei menu, niente `about:config` — tutto in chiaro, con spiegazioni.

Le opzioni disponibili:

- **Motore di ricerca predefinito**: DuckDuckGo di default, ma ci sono anche Qwant, Brave Search, Startpage (tutti privacy-oriented), e anche Google e Bing se preferisci il comfort al tracciamento
- **Resist Fingerprinting**: on/off
- **Password manager integrato di Firefox**: puoi disabilitarlo se usi già Bitwarden, KeePassXC o 1Password
- **Prefetching**: velocità vs. privacy — il prefetching carica i link prima che tu li clicchi, ma invia richieste a siti che potresti non voler visitare

## Resist Fingerprinting: cosa significa in pratica

Il **fingerprinting** è una tecnica con cui i siti web ti identificano senza usare cookie. Raccolgono informazioni sul tuo browser: risoluzione dello schermo, font installati, fuso orario, versione del browser, sistema operativo, GPU — e combinando questi dati costruiscono un "fingerprint" quasi unico per te.

**Resist Fingerprinting** è una funzione di Firefox che oscura o standardizza queste informazioni per renderti meno identificabile. Per esempio, segnala a tutti i siti la stessa risoluzione generica, indipendentemente da quella reale del tuo monitor.

Il compromesso è che alcuni siti potrebbero comportarsi in modo strano, e alcune funzioni grafiche potrebbero essere meno fluide. FireDragon ti lascia scegliere.

## XDG Base Directories: finalmente Linux-friendly

Questa è la novità che i power user Linux apprezzeranno di più. **XDG Base Directories** è uno standard che definisce dove i programmi devono mettere i loro file di configurazione, dati e cache su Linux:

- Configurazione → `~/.config/firedragon/`
- Dati → `~/.local/share/firedragon/`
- Cache → `~/.cache/firedragon/`

Fino a v12, FireDragon (come Firefox vanilla) usava `~/.firedragon/` nella home, un unico blob che mescola tutto. Con XDG, le cose sono separate e in posizioni standard, il che rende più facile:

```bash
# Backup della sola configurazione (senza cache da GB)
tar -czf firedragon-config-backup.tar.gz ~/.config/firedragon/

# Pulizia della cache senza toccare i profili
rm -rf ~/.cache/firedragon/
```

## Estensioni preinstallate

FireDragon v13 arriva con due estensioni già attive:

- **uBlock Origin** — blocco di pubblicità e tracker, lo standard de facto
- **CanvasBlocker** — blocca il canvas fingerprinting, cioè la tecnica che identifica il tuo browser in base a come disegna elementi grafici su canvas HTML5

Non serve installarle manualmente, sono già lì.

## Come installarlo

Se usi già **Garuda Linux**, l'aggiornamento arriva automaticamente:

```bash
garuda-update
```

Se sei su un'altra distro **Arch-based** (Manjaro, EndeavourOS, CachyOS, ecc.), trovi FireDragon su AUR:

```bash
# Con yay
yay -S firedragon

# Con paru
paru -S firedragon
```

Dopo l'installazione, avvialo con:

```bash
firedragon
```

## Vale la pena rispetto a Firefox o LibreWolf?

Dipende dal tuo punto di partenza:

| | Firefox vanilla | LibreWolf | FireDragon v13 |
|---|---|---|---|
| Privacy out-of-the-box | Bassa | Alta | Alta |
| Configurazione richiesta | Molta | Poca | Pochissima |
| Aggiornamenti automatici | Sì | Dipende | Via pacman/AUR |
| XDG Base Dirs | No | No | Sì |
| Distro-agnostic | Sì | Sì | Arch-based |

**FireDragon v13** è la scelta giusta se vuoi un browser Firefox-based con privacy ragionevole già configurata e una buona integrazione con il sistema Linux, senza dover spendere ore su `about:config`. Se sei già su Garuda, non c'è motivo per usare altro.

Se invece sei su una distro non Arch-based e vuoi qualcosa di simile, **LibreWolf** è probabilmente la scelta più portabile — disponibile su Flathub e come pacchetto per Debian/Fedora.
