---
title: "Atomic Arch: oltre 400 pacchetti AUR infettati in un attacco supply chain"
rilevanza: "ALTA"
fonte: "https://cybersecuritynews.com/arch-linux-aur-packages-compromised/"
data_notizia: "2026-06-11"
tags: ["security", "arch-linux", "supply-chain", "malware", "AUR", "infostealer"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Spiegare il concetto di supply chain attack usando l'AUR come caso concreto e accessibile. Ottimo momento per discutere le best practice per chi usa yay/paru e come proteggersi. Tocca sia Arch puro che Manjaro/EndeavourOS/Garuda.
---

# Atomic Arch: oltre 400 pacchetti AUR infettati in un attacco supply chain

Se usi Arch Linux o una distro basata su di essa — Manjaro, EndeavourOS, Garuda, Artix — e hai installato pacchetti dall'AUR nelle ultime settimane, è il momento di fermarsi e leggere con attenzione. Tra il 9 e il 13 giugno 2026, una campagna coordinata chiamata **"Atomic Arch"** ha compromesso oltre 400 pacchetti nel repository comunitario di Arch Linux, installando silenziosamente malware in grado di rubare credenziali e fare da rootkit sul sistema.

## Come funziona l'AUR e perché era vulnerabile

L'Arch User Repository (AUR) è il punto di forza — e il tallone d'Achille — di Arch Linux. Chiunque può pubblicare un PKGBUILD, lo script che descrive come compilare e installare un software. Quando un maintainer abbandona un pacchetto, questo diventa "orfano" e può essere adottato da altri utenti attraverso un processo standard.

Gli attaccanti di Atomic Arch hanno sfruttato esattamente questo meccanismo: hanno creato decine di account nuovi, adottato sistematicamente i pacchetti orfani più scaricati, e modificato i PKGBUILD per includere una dipendenza malevola: un pacchetto npm chiamato `atomic-lockfile` (e alcune varianti).

Il risultato? Chiunque compilasse uno di quei pacchetti con `yay`, `paru` o anche direttamente con `makepkg` si ritrovava il malware installato. Tutto apparentemente normale, tutto parte del "normale processo di build".

## Cosa fa il malware

Il payload, scritto in Rust (veloce, difficile da analizzare con strumenti tradizionali), ha tre funzioni principali:

**1. Infostealer**: raccoglie credenziali salvate nel browser (Chrome, Firefox, Brave), chiavi SSH (`~/.ssh/`), token API salvati in variabili d'ambiente o file di configurazione, e sessioni di strumenti come `gh`, `aws cli`, `kubectl`.

**2. Esfiltrazione**: invia il bottino a server remoti controllati dagli attaccanti, con focus su ambienti CI/CD dove le credenziali sono particolarmente preziose.

**3. Rootkit basato su eBPF**: se ottiene privilegi root, usa eBPF per nascondersi dai processi di monitoraggio del sistema, rendendo la rilevazione molto più difficile.

Gli ambienti più colpiti sono le workstation di sviluppatori e i runner CI/CD basati su Arch — un target ricchissimo di credenziali ad alto valore.

## Come verificare se sei stato colpito

La community ha già creato strumenti di rilevazione open source. Puoi usare il tool mantenuto da Lenucksi:

```bash
# Scarica il tool di detection della community
git clone https://github.com/lenucksi/aur-malware-check
cd aur-malware-check

# Analizza i pacchetti AUR installati sul sistema
python3 aur-malware-check.py
```

Puoi anche verificare manualmente se il pacchetto npm malevolo è presente:

```bash
# Controlla npm globale
npm ls -g atomic-lockfile 2>/dev/null

# Cerca in node_modules del sistema
find /usr /opt ~ -name "atomic-lockfile" -type d 2>/dev/null

# Controlla i log di pacman per installazioni recenti di pacchetti orfani
grep -i "installed" /var/log/pacman.log | tail -100
```

## Cosa fare se sei stato colpito

Se il tool di rilevazione trova corrispondenze, agisci subito:

1. **Cambia immediatamente tutte le password** accessibili dalla macchina colpita, a partire da quelle più critiche
2. **Revoca i token API** su GitHub, GitLab, AWS, GCP, DigitalOcean — tutti quelli che potresti aver usato sulla macchina
3. **Ruota le chiavi SSH** e aggiorna il file `authorized_keys` su tutti i server a cui hai accesso
4. **Considera una reinstallazione pulita** del sistema — i rootkit basati su eBPF sono difficili da rimuovere completamente senza un wipe
5. **Notifica il tuo team** se la macchina era connessa a infrastrutture condivise o pipeline CI/CD

## Come proteggersi in futuro

La lezione più importante: **controlla sempre il PKGBUILD prima di installare un pacchetto AUR**:

```bash
# Con yay, scarica senza installare e leggi prima
yay -G nome-pacchetto
cat nome-pacchetto/PKGBUILD

# Con paru, puoi abilitare la review automatica
# Aggiungi a ~/.config/paru/paru.conf:
# [options]
# ReviewPkgbuild
```

Altre best practice:
- Evita i pacchetti orfani con pochi voti o con cambio di maintainer recente
- Controlla la data dell'ultima modifica del PKGBUILD su aur.archlinux.org
- Valuta tool come `aurutils` per un workflow più controllato e auditabile
- Non usare `--noconfirm` con i pacchetti AUR: prenditi il tempo di leggere

Arch Linux ha già rimosso tutti i pacchetti compromessi e bannato gli account coinvolti. Ma la finestra di esposizione — almeno 4 giorni — è stata sufficiente per colpire potenzialmente migliaia di utenti. L'AUR non è un repository curato: usarlo richiede consapevolezza e un pizzico di sano paranoidismo.
